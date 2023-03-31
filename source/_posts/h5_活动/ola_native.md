---
title: ee-front/native
index_img: >-
  /images/cp-pk-event.png
author: Dylan
tags:
  - 接口文档
  - H5
math: true
mermaid: true
date: 2023-03-27 11:12:00
---
# @ee-front/native

ola平台下各app提供的native接口

如果你在业务中碰到了新的需求, 增加了新的native接口, 请在此包中补充

```typescript

export function getUserInfo() {
  // 获取用户信息
  return callAppFunc<{
    lan?: string
    server_env: string
    token: string
    uid: number
    package: string
    icon: string
  }>('getUserInfo')
}
// 跳转客户端登录
export function login() {
  return callAppFunc('login')
}
// 进入指定房间
export function openRoom(rid: number | string) {
  return callAppFunc('openRoom', { rid: Number(rid) })
}
// 进入指定大神的订单邀约界面
export function openOrderScreen(toUid: number) {
  return callAppFunc('openOrderScreen', { uid: toUid })
}
// 设置页面标题
export function setTitle(title: string) {
  window.document.title = title
  return callAppFunc('setTitle', { title })
}
// 保存图片
// url --url为网路图片地址
// content  ---base64内容
export function saveImage(type: 'url' | 'content', data: string) {
  return callAppFunc('saveImage', { [type]: data })
}
// 分享图片 canvas绘制的图片 分享到QQ微信等
export function shareByImage(type: string, imgUrl: string) {
  const tpMap = {
    wechat: 1,
    moment: 2,
    qq: 3,
    qzone: 4,
    face: 5
  }
  const tp = tpMap[type]
  return callAppFunc('shareDirect', { type, tp, imgUrl })
}
// 签到/补签
export function checkin(params: { [key: string]: any }) {
  return callAppFunc('checkin', params)
}
// 领取奖励
export function getAward(params: { [key: string]: any }) {
  return callAppFunc('getAward', params)
}
// 客户端重新回到H5
export function onReturnToWeb(callback: () => void) {
  return listenAppMethod('onReturnToWeb', callback)
}

// 分享到微信
export function shareWechat(tp: number) {
  return callAppFunc('shareDirect', { type: 'wechat', tp })
}
// 分享到朋友圈
export function shareWechatMoment(tp: number) {
  return callAppFunc('shareDirect', { type: 'moment', tp })
}
// 分享到QQ
export function shareQQ(tp: number) {
  return callAppFunc('shareDirect', { type: 'qq', tp })
}
// 分享到QQ空间
export function shareQZone(tp: number) {
  return callAppFunc('shareDirect', { type: 'qzone', tp })
}
// 分享到facebook
export function shareFacebook(tp: number) {
  return callAppFunc('shareDirect', { type: 'facebook', tp })
}
// 分享到twitter
export function shareTwitter(tp: number) {
  return callAppFunc('shareDirect', { type: 'twitter', tp })
}
// 分享到line
export function shareLine(tp: number) {
  return callAppFunc('shareDirect', { type: 'line', tp })
}
// 跳转到我的字符页
export function showVipMall() {
  return callAppFunc('showVipMall')
}
// 跳转到我的字符页榜单
export function showRank(param: { [key: string]: any }) {
  return callAppFunc('showRank', param)
}
// 跳转到web页
export function showScreen(url: string) {
  return callAppFunc('showCommonWebScreen', { url })
}
// 跳转到个人主页
export function showImageScreen(uid: number | string) {
  return callAppFunc('showImageScreen', { uid: Number(uid) })
}
// 进入附近
export function showNearby() {
  return callAppFunc('showNearby')
}
// 进入粉丝列表
export function showFansList() {
  return callAppFunc('showFansList')
}
// 进入首页
export function showHomePage() {
  return callAppFunc('showHomePage')
}
// 进入发现-娱乐房列表
export function showJoyRoom() {
  return callAppFunc('showJoyRoom')
}
// 进入余额充值
export function showChargeBalance(refer?: string) {
  return callAppFunc('showChargeBalance', refer ? { refer } : undefined)
}
// 进入身份验证
export function showChargeOrBindPhoneNumber() {
  return callAppFunc('showChargeOrBindPhoneNumber')
}
// 进入选择你要创建的类型页面
export function showCreateRoom() {
  return callAppFunc('showCreateRoom')
}
// 随机进入画猜、卧底、狼人杀房间
export function showSocialGame() {
  return callAppFunc('showSocialGame')
}
// 随机进入画猜、卧底、狼人杀、娱乐房
export function showSocialGameAndJoyRoom() {
  return callAppFunc('showSocialGameAndJoyRoom')
}
// 进入朋友圈
export function showMoment() {
  return callAppFunc('showMoment')
}
// 进入与指定好友聊天界面
export function showPrivateChat(params: { [key: string]: any }) {
  return callAppFunc('showPrivateChat', params)
}
// 身份验证剧本杀
export function idAuth() {
  return callAppFunc('idAuth')
}
// 剧本杀首页
export function juben() {
  return callAppFunc('juben')
}
// 小游戏 游戏id
export function littleGame(params: { [key: string]: any }) {
  return callAppFunc('littleGame', params)
}
// 消息Tab关注列表
export function showFollowList() {
  return callAppFunc('showFollowList')
}
// 发现页
export function showDiscoveryPage() {
  return callAppFunc('showDiscoveryPage')
}
// 剧本库列表
export function jubenList() {
  return callAppFunc('jubenList')
}
// 跳转话题页
export function openTopicDetail(topicId: number) {
  return callAppFunc('openTopicDetail', { topicId })
}
// 获取系统信息
export function getSystemInfoSync() {
  return callAppFunc('getSystemInfoSync')
}

// 返回
export function navigateBack() {
  return callAppFunc('navigateBack')
}

// 跳转到首页某个tab
export function showHomePageWithTab(tab: string) {
  return callAppFunc('showHomePageWithTab', { tabType: tab })
}
// 跳转到背包
export function openMyBag(params: { [key: string]: any }) {
  return callAppFunc('openMyBag', params)
}

// 打开指定页面
export function schema(schemaUrl: string) {
  return callAppFunc('schema', { schema_url: schemaUrl })
}

```