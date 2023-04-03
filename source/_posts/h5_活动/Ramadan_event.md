---
title: Ramadan 活动
index_img: >-
  /images/ramadan-event.png
author: Dylan
tags:
  - 接口文档
  - H5
math: true
mermaid: true
sticky: 100
date: 2023-03-08 18:26:00
---

> Ramadan 活动接口文档，Ticket: https://github.com/olachat/veeka/issues/6465

<!-- more -->

## Ticket Information

BRD: Pending
Modao: https://modao.cc/app/NSgmTIeirraexeRRE0g2Ki
Design: https://lanhuapp.com/link/#/invite?sid=lx0QPhKb
Animation Requirement: https://docs.google.com/document/d/1X6ViGg0xngI2VCbZFB8tUDPAwUtkiVOX5tfcLwgyi9g/edit
Deadline - 18 April 2023

To-do:

- 发送卡片邀请和接收卡片邀请的页面交互得调整
- 免费抽奖和 1 次抽奖的按钮做在一块
- 集成卡默认置灰
- 动效资源
- 4 月 18 日上线

Developer todo:

- [ ] POC on react VAP implementation, Study how vap works in room and try to implement in H5 -> @linboyuan-ola
- [ ] Project setup, API specs, API caching & definition and Theming of the project -> @dylansalim-ola
- [ ] H5 Frontend -> Boyuan & Dylan (To be split, Boyuan - VAP focus)
- [ ] Backend -> @ziyu-ola

Note: Boyuan will be on leave for a week during this activity development period, Dylan will help to cover the remaining parts

## 最佳情侣 pk 赛活动

### 1. Get Main API

Desc: Main API

URL: /activity/RamadanEvent/GetEventInfo

Sample Response:

```json lines
{
  "event_period": "2023.1.21-2023.1.25",
  "marquee": ["XXX got it XXX", "XXX got it XXX"],
  "jackpot_prize_list": [
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
}
```

### 2. Get Jackpot Data

Desc: Jackpot data and potential update the card stack data

URL: /activity/RamadanEvent/GetJackpotData

Sample Response:

```json lines
{
  "free_lottery_available": true,
  "wallet_amount": 33333,
  "jackpot": {
    "amount": 32636,
    "desc": "Currently, there are 2000 cards combined by 500 lucky people"
  },
  "card_stack_info": {
    "synthesized_amount": 2,
    "synthesizable": false,
    "card_1": {
      "amount": 1
    },
    "card_2": {
      "amount": 0
    },
    "card_3": {
      "amount": 3
    },
    "card_4": {
      "amount": 1
    },
    "card_5": {
      "amount": 0
    }
  } // same as API 4
}
```

### 3. Submit draw prize request

Desc: Free lottery for Ramadan/Draw a prize once/Ten sweeptakes, return data from API 2 if success

URL: /activity/RamadanEvent/RequestDrawPrize

Sample Request:

```json lines
{
  "draw_type": "FREE" // Types -> "FREE", "ONCE", "TEN"
}
```

Sample Response:

```json lines
{
  "jackpot_data": {
    "free_lottery_available": true,
    "wallet_amount": 33333,
    "jackpot": {
      "amount": 32636,
      "desc": "Currently, there are 2000 cards combined by 500 lucky people"
    },
    "card_stack_info": {
      "synthesized_amount": 2,
      "synthesizable": false,
      "card_1": {
        "amount": 1
      },
      "card_2": {
        "amount": 0
      },
      "card_3": {
        "amount": 3
      },
      "card_4": {
        "amount": 1
      },
      "card_5": {
        "amount": 0
      }
    }
  }, // SAME AS API 2
  "reward": {
    "prize_type": "gift",
    "name": "钱兔似锦",
    "gold_bean_price": "100",
    "gift": {
      "gift_id": 0,
      "icon": "/.png"
    }
  }
}
```

### 4. Get Card Stack Info

Desc: For display Love letter inbox, display all inbox

URL: /activity/RamadanEvent/GetCardStackInfo

Sample Response:

```json lines
{
  "card_stack_info": {
    "synthesized_amount": 2,
    "synthesizable": false,
    "card_1": {
      "amount": 1
    },
    "card_2": {
      "amount": 0
    },
    "card_3": {
      "amount": 3
    },
    "card_4": {
      "amount": 1
    },
    "card_5": {
      "amount": 0
    }
  }
}
```

### 5. Submit Request for One Bond Synthesis

Desc: One Bond Synthesis button

URL: /activity/best_cp_pk_event/FriendHelpVoteBillboardTab
