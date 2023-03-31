---
title: 最佳情侣pk赛活动
index_img: >-
  /images/cp-pk-event.png
author: Dylan
tags:
  - 接口文档
  - H5
math: true
mermaid: true
sticky: 100
date: 2023-03-27 11:12:00
---

> 最佳情侣 pk 赛活动接口文档，Ticket: https://github.com/olachat/veeka/issues/6199

<!-- more -->

## 最佳情侣 pk 赛活动

### 1. Get Main API

Desc: Main API before tab

URL: /activity/best_cp_pk_event/BestCpPkEventInfo

Sample Response:

```json lines
{
  "event_period": "2023.1.21-2023.1.25",
  "subtitle": "累积爱心💗，争夺Veeka第一情侣",
  "my_cp_content": {
    "left_user_info": {
      "uid": 110298,
      "name": "boy",
      "icon": ".png"
    },
    "right_user_info": {
      "uid": 110299,
      "name": "girl",
      "icon": ".png"
    },
    "is_cp_available": 1, // 1 for available, 0 for not-available (display find cp btn)
    "cp_heart_point": 30,
    "cp_rank": 1 //rank of the cp, start from 1
  },
  "receive_heart_point_content": {
    "gift_tab_content": {
      "currency_exchange_rate": 1, // 1金豆 = ？爱心
      "prize_list": [
        {
          "prize_type": "gift",
          "name": "钱兔似锦",
          "gold_bean_price": "100",
          "gift": {
            "gift_id": 0,
            "icon": "/.png"
          }
        }
      ]
    },
    "cp_ring_tab_content": {
      "currency_exchange_rate": 2, // 1金豆 = ？爱心
      "prize_list": [
        {
          "prize_type": "gift",
          "name": "钱兔似锦",
          "gold_bean_price": "100",
          "gift": {
            "gift_id": 0,
            "icon": "/.png"
          }
        }
      ]
    },
    "friend_help_tab_content": {
      "currency_exchange_rate": 2, // 1助力值 = ？爱心
      "accumulated_heart_point": 300,
      "friend_list": [
        {
          "uid": 110298,
          "name": "boy",
          "icon": ".png"
        }
      ] // top 5 friend who voted for you, if empty return []
    }
  },
  "rule_content": {
    "reward_list": [
      {
        "rank": "TOP 1",
        [
        {
          "prize_type": "gift",
          "name": "钱兔似锦",
          "gold_bean_price": "100",
          "desc": "x2",
          "gift": {
            "gift_id": 0,
            "icon": "/.png"
          }
        }
      ]
      }
    ]
  }
}
```

### 2. Submit to request for friend vote

Desc: User tab on 获得助力 button -> Open in app modal to pick friends to ask for help -> Click submit -> Submit this api with friends list to send 系统消息

URL: /activity/best_cp_pk_event/RequestFriendVote

Sample Request:

```json lines
{
  "friend_uid_list": ["112805", "112803"]
}
```

### 3. Get Task list

Desc: For display Love letter inbox, display all inbox

URL: /activity/best_cp_pk_event/GetTaskList

Sample Response:

```json lines
{
  "error_message": "", //没有信息不会放在这里
  "task_list": [
    {
      "task_idx": 3,
      "title": "任务 1",
      "desc": "情侣签到",
      "current_progress_point": 1,
      "max_progress_point": 3,
      "cp_heart_point": 30,
      "btn_text": "签到",
      "status": "UNCLAIMED" //enum of {UNCLAIMED, CLAIMED, UNAVAILABLE, GO_POST_MOMENT}
    }
  ]
}
```

### 4. Submit Claim Task list

Desc: For display Love letter inbox, display all inbox

URL: /activity/best_cp_pk_event/ClaimTaskList

Sample Request:

```json lines
{
  "task_idx": 3
}
```

Sample Response:
return success: true by default

### 5. Get Friend Help Vote Billboard Tab

Desc: 助力好友 Billboard tab

URL: /activity/best_cp_pk_event/FriendHelpVoteBillboardTab

Sample Request:

```json lines
{
  "friend_uid": "112805" // friend_uid is empty if no extra filtering is required (user is not enter from 系统消息)
}
```

Sample Response:

```json lines
{
  "not_rank_tips": {
    // if there isn't any user in the rank return this, this will only display if the user rank list is empty, len(user_rank_list) == 0
    "title": "活动还没开始",
    "sub_title": "活动将在-月-日至-月-日"
  },
  "vote_owned": "300",
  "max_vote_per_request": 10,
  "user_rank_list": [
    // if there is any user in the rank return the list of items, if not, return empty array, do not return null
    {
      "cp_id": 12,
      "rank_idx": 1,
      "left_user_info": {
        "uid": 110298,
        "name": "boy",
        "icon": ".png"
      },
      "right_user_info": {
        "uid": 110299,
        "name": "girl",
        "icon": ".png"
      },
      "cp_vote_accumulated": 52000
    }
  ]
}
```

### 6. Submit to cast vote CP Friends

Desc: For display Love letter inbox, display all inbox

URL: /activity/best_cp_pk_event/VoteCpFriend

Sample Request:

```json lines
{
  "cp_id": 3,
  "vote_amount": 2
}
```

### 7. Best CP Billboard Tab

Desc: Billboard tab content

URL: /activity/best_cp_pk_event/GetBestCPBillboardTab

Sample Response:

```json lines
{
  "not_rank_tips": {
    // if there isn't any user in the rank return this, this will only display if the user rank list is empty, len(user_rank_list) == 0
    "title": "活动还没开始",
    "sub_title": "活动将在-月-日至-月-日"
  },
  "count_down": {
    "left_second": 10000 // left countdown seconds in milliseconds
  },
  "user_rank_list": [
    // if there is any user in the rank return the list of items, if not, return empty array, do not return null
    {
      "rank_idx": 1,
      "left_user_info": {
        "uid": 110298,
        "name": "boy",
        "icon": ".png"
      },
      "right_user_info": {
        "uid": 110299,
        "name": "girl",
        "icon": ".png"
      },
      "cp_vote_accumulated": 52000
    }
  ],
  "my_cp_content": {
    "left_user_info": {
      "uid": 110298,
      "name": "boy",
      "icon": ".png"
    },
    "right_user_info": {
      "uid": 110299,
      "name": "girl",
      "icon": ".png"
    },
    "is_cp_available": 1, // 1 for available, 0 for not-available (display find cp btn)
    "cp_heart_point": 30,
    "cp_rank": 1 //rank of the cp, start from 1
  }
}
```

### 8. Heart Transaction History

Desc: CP Heart Transaction History

URL: /activity/best_cp_pk_event/GetHeartTransactionHistory

Sample Response:

```json lines
{
  "transaction_history": [
    {
      "title": "收获礼物",
      "cp_heart_point": 200
    }
  ]
}
```

### 8. Friend Help Transaction History

Desc: Friend Help Transaction History

URL: /activity/best_cp_pk_event/GetFriendHelpTransactionHistory

Sample Response:

```json lines
{
  "transaction_history": [
    {
      "title": "收获礼物",
      "cp_heart_point": 200
    }
  ]
}
```

### IM extra fields for api 5 [5. Get Friend Help Vote Billboard Tab]

- extra['url'] = <EVENT_URL>
- extra['image_url'] = <IMAGE_URL> by 大区
- extra['type'] = 'event_invite'
- extra['highlight'] = <DESC> -> desc text grey in color
- message.content = <EVENT_TITLE> by 大区 -> will be bold in im message

### Complicated Flow

#### 1. For request vote from friends

Click on the 助力好友 btn on the third tab -> mobile display the bottom sheet to select friends -> click submit ->
Server side send IM message using the user account to the selected friends with clickable link <EVENT_LINK>?friendUid="<FRIEND_UID>" ->
Open the event page and auto scroll to the 助力好友 billboard section ->
the api 5 [5. Get Friend Help Vote Billboard Tab] should provide the friendUid as param, and the return array should have the selected friend CP as first item

#### 2. Task Center
Task 1 签到任务 only have UNCLAIMED | CLAIMED status
Task 2 will have UNCLAIMED | CLAIMED | GO_POST_MOMENT
Task 3 will have UNCLAIMED | CLAIMED 