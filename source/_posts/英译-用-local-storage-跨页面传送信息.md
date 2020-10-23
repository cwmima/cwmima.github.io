---
title: '[英译] 用 local storage 跨页面传送信息'
date: 2019-04-30 22:19:13
intro: 跨页面交流的优雅解决方案
featured_image:
tags: 
    - Front-end
    - Javascript
    - Translation
---

原文：<https://ponyfoo.com/articles/cross-tab-communication>
翻译：辛眉

<br/>

> [SharedWorker](https://developer.mozilla.org/en-US/docs/Web/API/SharedWorker) API 允许我们在不同的 iframe，甚至不同的浏览器标签页和窗口之间传输信息。它在 Chrome，Firefox 上都能运行，但不被 Safari 支持。然而有一个被广泛支持的方法却不为人知，让我们来看看吧！

我想用一种优雅的方法解决以下问题：假设有个人访问了你的网站，登录，打开另一个标签页，然后在那个标签页登出。这时他在第一个标签页仍然是“已登录”的状态，而他点击的所有东西都会重定向到登录页面，或者直接崩掉。一个更好的做法是我们能够知道他在第二个标签页已经登出了，然后显示一个对话框让他重新登录，或者直接显示登录框。

你可以用 WebSocket API 来做，但是杀鸡焉用宰牛刀呢。我想通过更低级的技术来实现，所以我找了很多跨页面通讯的选项。我找到的第一个选项是用 cookies 或者 `localStorage`，然后用 `setInterval` 周期性检查用户是否还在登录状态。我不太满意这个答案，因为反复检查一个可能根本不会发生的事件实在太耗费 CPU 了。如果这样我宁可使用 Comet （一种维持与服务器端的连接并获取实时推送的技术，包括长轮询 long polling 和 iframe 流），Server-sent events 或者 WebSocket。

然而我被骗了，事实上单靠 `localStorage` 就能搞定。

你知道 `localStorage` 会触发事件吗？具体来说，当你进行添加、修改、删除的时候，就会在其他的浏览环境（browsing context）中触发一个事件。也就是说，当你在某个标签页上改动了 `localStorage`，其他标签页都能通过监听 `window` 上的 `storage` 事件来得知这一切：

```javascript
window.addEventListener('storage', function (event) {
  console.log(event.key, event.newValue);
});
```

`event` 对象包含以下相关属性：

| Property   | Description                                      |
| ---------- | ------------------------------------------------ |
| `key`      | The affected key in `localStorage`               |
| `newValue` | The value that is currently assigned to that key |
| `oldValue` | The value before modification                    |
| `url`      | The URL of the page where the change occurred    |
<br/>

当你在某个页面上修改 `localStorage` 时，会在除了该页面以外的其他所有标签页触发事件，这意味着我们可以通过它来跨页面传递信息。

```javascript
var loggedOn;

// TODO: call when logged-in user changes or logs out
logonChanged();

window.addEventListener('storage', updateLogon);
window.addEventListener('focus', checkLogon);

function getUsernameOrNull () {
  // TODO: return whether the user is logged on
}

// 用户在该页面登录时，将登录状态记录进 localStorage
function logonChanged () {
  var uname = getUsernameOrNull();
  loggedOn = uname;
  localStorage.setItem('logged-on', uname);
}

// 用户在其他标签页登出时，捕获事件并更新登录状态
function updateLogon (event) {
  if (event.key === 'logged-on') {
    loggedOn = event.newValue;
  }
}

// 检查登录状态，若未登录则重新加载页面
function checkLogon () {
  var uname = getUsernameOrNull();
  if (uname !== loggedOn) {
    location.reload();
  }
}
```

当用户打开两个标签页，在其中一个登出，再回到另一个标签页，页面会重新加载，然后服务端逻辑会把用户带到其他页面。注意这里我们只在标签页被聚焦（focus）的情况下才检查登录状态，因为用户有可能在登出之后立刻再次登录，这种情况下我们不想把他们从所有标签页都登出。

我们当然还可以改进这段代码，但它已经满足要求了。一个更好的实现可能是要求他们立刻登录，但注意这段代码还可以反过来：当他们登录后回到之前登出的标签页时，重新加载会让他们直接回到已登录状态。

（译者注：接下来作者介绍了他自己做的一个 npm module，简化了 `localStorage` 的语法，并提升了兼容性。但在实际工作中，由于私人维护的包往往有很多不确定性甚至安全隐患，因此需要谨慎对待。因而略过不译。）