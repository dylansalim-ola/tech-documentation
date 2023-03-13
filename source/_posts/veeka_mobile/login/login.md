---
title: Auth failed issue upon login
index_img: >-
  https://rmt.dogedoge.com/fetch/fluid/storage/hello-fluid/cover.png?w=480&fmt=webp
author: Dylan
tags:
  - Authentication
  - Login
math: true
mermaid: true
sticky: 100
date: 2023-03-08 18:26:00
---
>Existing issue with Auth failed when switching dev and prod environment when user is logged in

## Background
If user change environment while logged in, and click restart to take effect button in developer options, it will show 'Auth failed' error message on the next app start. This happens because of the globalProviders was set on the application.dart level instead on the after login part of the code.

- Line 151, application.dart
```
globalProviders.addAll([
      ChangeNotifierProvider(create: (_) => UserModel(), lazy: false),
      ChangeNotifierProvider(create: (_) => MomentModel(), lazy: false),
      ChangeNotifierProvider(create: (_) => ProfilePayload(), lazy: false),
      ChangeNotifierProvider(create: (_) => GiftMediaModel(), lazy: false),
      ChangeNotifierProvider(create: (_) => ThemeProvider(), lazy: false),
      ChangeNotifierProvider(create: (_) => MomentVideoProvider(), lazy: false),
      ChangeNotifierProvider(create: (_) => PersonalInfoProvider(), lazy: false),
      ChangeNotifierProvider(create: (_) => RechargePackageProvider(), lazy: false),
      ChangeNotifierProvider(create: (_) => GiftDecorateProvider(), lazy: false),
      ChangeNotifierProvider(create: (_) => MomentPostGuideProvider(), lazy: false),
      if (Constant.isDevMode) ChangeNotifierProvider(create: (_) => hotupdater, lazy: false),
    ]);
```

- This part of code will triggered actively and will trigger the api calls to get information such as taskCenterShowRedDot

- Snippet from ProfilePayload
```
ProfilePayload() {
    eventCenter.addListener(System.EventLogin, _onLogin);
    eventCenter.addListener('TaskCenter.noRedDot', _removeTaskDot);
    eventCenter.addListener(EventConstant.TaskCenterClaimableChange, _taskCenterClaimableChange);

    reload();
    loadMomentsInfo();
    loadMomentUnreadMsg();
    loadVipMallRedPoint();
    loadGiftWallPoint();
    loadMentorShipRedPoint();
    loadPopularityRedPoint();
    loadVipRedPoint();
    loadGoldBeanRedPoint();
    functionCenterHasRedDot();
    taskCenterShowRedDot();
    loadInvitePrizeRedDot();

    _momentRedPointTimer =
        Timer.periodic(Duration(seconds: 60), (timer) => loadMomentsInfo());
    _momentUnReadMsgTimer =
        Timer.periodic(Duration(seconds: 90), (timer) => loadMomentUnreadMsg());
  }
```

- You might think that adding a check on the session.isLogined() might solve the issue, but actually it will not. This part of code will be called upon app startup which is before it checks that the app session is valid or not. Calling the Session here will only get the previous session status, which in turns causing the session.isLogined() to be true. 

## Possible fix for this issue
1. Destroy the session upon clicking the '重启生效', but it creates extra steps for developer and QA during testing (Need to relogin if we change environment)


## Why we opt to not fixing this issue
1. Currently it only affects dev environment and it is not a fatal issue (Online users does not have the rights to switch environment)
