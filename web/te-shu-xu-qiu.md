# 特殊需求

## 添加书签到Google在线书签

```javascript
javascript:(function(){var a=window,b=document,c=encodeURIComponent,d=a.open("https://www.google.com/bookmarks/mark?op=edit&output=popup&bkmk="+c(b.location)+"&title="+c(b.title),"bkmk_popup","left="+((a.screenX||a.screenLeft)+10)+",top="+((a.screenY||a.screenTop)+10)+",height=510px,width=550px,resizable=1,alwaysRaised=1");a.setTimeout(function(){d.focus()},300)})();
```

## 添加QQ好友

from: [分享一个直接加QQ好友的链接或会话的](https://blog.csdn.net/qq_2300688967/article/details/52162230)

```text
# 打开临时会话
tencent://message/?Menu=yes&uin=2300688967&Service=300&sigT=4
# 加好友(Mac无效)
tencent://AddContact/?fromId=45&fromSubId=1&subcmd=all&uin=2300688967&website=www.oicqzone.com
```

