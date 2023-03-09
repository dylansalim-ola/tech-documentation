title: 最佳情侣pk赛活动
index_img: >-
  https://rmt.dogedoge.com/fetch/fluid/storage/hello-fluid/cover.png?w=480&fmt=webp
author: Dylan
tags:
  - 接口文档
  - H5
math: true
mermaid: true
sticky: 100
date: 2023-03-08 18:26:00
---
>最佳情侣pk赛活动接口文档，Ticket: https://github.com/olachat/veeka/issues/6199

<!-- more -->
## 最佳情侣pk赛活动

### 1. Main API

Desc: Main API before tab

URL: /activity/best_cp_pk_event/main

Sample Response:

```json lines
{
  "event_period": "2023.1.21-2023.1.25",
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
    "cp_vote_accumulated": 52000,
    "is_cp_available": 1 // 1 for available, 0 for not-available (display find cp btn)
  },
  "prize_list": [
    {
      "prize_type": "gift",
      "name": "钱兔似锦",
      "desc": "100金豆",
      "gift": {
        "gift_id": 0,
        "icon": "/.png"
      }
    }
  ],
  "reward_category_list": [
    {
      "category_id": 0,
      "category_name": "TOP1",
      "reward_list": [
        {
          "prize_type": "gift",
          "name": "钱兔似锦",
          "desc": "100金豆",
          "gift": {
            "gift_id": 0,
            "icon": "/.png"
          }
        }
      ]
    },
    {
      "category_id": 1,
      "category_name": "TOP2",
      "reward_list": [
        {
          "prize_type": "gift",
          "name": "钱兔似锦",
          "desc": "100金豆",
          "gift": {
            "badge": "10天",
            "gift_id": 0,
            "icon": "/.png"
          }
        }
      ]
    }
  ]
}
```

### 2. CP Voting & Prize Box Tab

Desc: CP Voting Tab content

URL: /activity/best_cp_pk_event/GetCPVotingTab

5 votes per day, recharge once get another voting chance

Sample Response:

```json lines
{
  "vote_remaining": 3, //if vote left is 0, then the user is not allowed to vote
  "can_open_box": true, // if user can open the box
  "reward_list": [
    {
      "prize_type": "gift",
      "name": "钱兔似锦",
      "desc": "100金豆",
      "gift": {
        "badge": "10天",
        "gift_id": 0,
        "icon": "/.png"
      }
    }
  ]
}
```

### 3. Best CP Billboard Tab

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
  "my_rank": {
    "rank_idx": 3,
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
    "cp_vote_accumulated": 52000,
    "is_cp_available": 1 // 1 for available, 0 for not-available (display find cp btn)
  }
}
```

### 4. Love Letter Tab

Desc: For display love letter content

URL: /activity/best_cp_pk_event/GetLoveLetterBillboardTab

Contain sent love letter by the user, disappear after 24 hours

- Normal Love Letter limits at 20 words
- Premium Love Letter limits at 40 words<br>
  Sample Request:

```json lines
{
  "can_send_normal_letter": true, // if the normal letter have send limit
  "can_send_premium_letter": true, // if the premium letter have send limit
  "not_rank_tips": {
    // if there isn't any user in the rank return this, this will only display if the user rank list is empty, len(user_rank_list) == 0
    "title": "暂时还没有情书",
    "sub_title": "快去填写情书吧！"
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
      "cp_vote_accumulated": 52000,
      "letter_content": "꧅你好(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅꧅",
      "letter_date": "2023年7月10日",
      "letter_time": "12:02"
    }
  ]
}
```

### 5. Display Voting CP List

Desc: For display Voting CP List

URL: /activity/best_cp_pk_event/GetInitialVotingCPList

Return 50 entries of Voting CP List
Sample Request:

```json lines
{
  "error_message": "你已经投票五次了", // default: ""
  "cp_list_to_vote": [
    {
      "cp_vote_idx": 3,
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
      "can_vote": 1 // 1 for can vote, 0 for cannot
    }
  ]
}
```

### 6. Search Related Voting CP List

Desc: Search request for Related Voting CP List, by uid and name

URL: /activity/best_cp_pk_event/SearchCPList

This api only call if user searched

Sample Request

```json lines
{
  "search_text": "112"
}
```

Sample Response:

```json lines
{
  "msg": "没有资料",
  "cp_list_to_vote": [
    {
      "cp_vote_idx": 3,
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
      "can_vote": 1 // 1 for can vote, 0 for cannot
    }
  ]
}
```

### 7. Vote for CP

Sample Request

```json lines
{
  "cp_vote_idx": 3
}
```

Sample Response:
return success: true by default

### 8. Send Love Letter

Disclaimer: The get friend list api was skip if the UI for friend selection to send love letter can be done via mobile
& if the letter can send to the same user multiple times

Desc: API for sending love letter

URL: /activity/cp_valentine_event/SendLoveLetter

Sample Request

```json lines
{
  "cp_vote_idx": 3
}
```

Sample Response:
return success: true by default

### 9. Send Normal Love Letter

### 10. Send Premium Love Letter

Disclaimer: The get friend list api was skip if the UI for friend selection to send love letter can be done via mobile
& if the letter can send to the same user multiple times

Desc: API for sending love letter

URL: /activity/cp_valentine_event/SendNormalLoveLetter
URL: /activity/cp_valentine_event/SendPremiumLoveLetter

Sample Request

```json lines
{
  "love_letter_msg": "꧅你好(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅(ؓؒؒؑؑؖؔؓؒؐؐ⁼̴̀ωؘؙؖؕؔؓؒؑؐؕ⁼̴̀ )꧅꧅"
}
```

Sample Response:
return success: true by default

### 11. Display Love letter inbox

Desc: For display Love letter inbox, display all inbox

URL: /activity/best_cp_pk_event/GetLoveLetterInboxList

Sample Response:

```json lines
{
  "error_message": "", //没有信息不会放在这里
  "cp_list_to_vote": [
    {
      "cp_vote_idx": 3,
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
      "can_vote": 1 // 1 for can vote, 0 for cannot
    }
  ]
}
```

### 12. Display Task list

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
      "status": "UNCLAIMED" //enum of {UNCLAIMED, CLAIMED, UNAVAILABLE}
    }
  ]
}
```

### 13. Claim Task list

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