# Mac 版迅雷去广告

Mac的应用本质也就是一个文件夹，查看内容需要通过右键-显示包内容来进入，迅雷的内容如下 ![image.png](https://upload-images.jianshu.io/upload_images/1845254-b0769023e5217901.png?imageMogr2/auto-orient/strip|imageView2/2/w/800)

去广告只要把对应的Plugin删除或者命令禁用执行权限就行。删除就不必介绍了，但是有些文件不能删除比如xlplayer，只能通过命令禁用，打开终端输入 `chmod a-x` （结尾有个空格），再把要禁用的插件拉到终端会补全内容，比如禁用进入的推荐，完整内容是 `chmod a-x /Applications/Thunder.app/Contents/PlugIns/featuredpage.xlplugin`。下面给出些名字对应的功能，可以根据自己需求可以选择删除或者命令禁用。反之启用则是 `chmod a+x`。

```bash
# 推荐影评
chmod a-x /Applications/Thunder.app/Contents/PlugIns/featuredpage.xlplugin
# 底部垃圾消息
chmod a-x /Applications/Thunder.app/Contents/PlugIns/advertising.xlplugin
# 资源评论
chmod a-x /Applications/Thunder.app/Contents/PlugIns/details.xlplugin
# 应用
chmod a-x /Applications/Thunder.app/Contents/PlugIns/applications.xlplugin
# 活动中心
chmod a-x /Applications/Thunder.app/Contents/PlugIns/activitycenter.xlplugin
# 迅雷快鸟
chmod a-x /Applications/Thunder.app/Contents/PlugIns/bbassistant.xlplugin
# 浏览器支持
chmod a-x /Applications/Thunder.app/Contents/PlugIns/browserhelper.xlplugin
# 手机迅雷
chmod a-x /Applications/Thunder.app/Contents/PlugIns/iOSThunder.xlplugin
# 离线空间
chmod a-x /Applications/Thunder.app/Contents/PlugIns/lixianspace.xlplugin
# 应用卸载
chmod a-x /Applications/Thunder.app/Contents/PlugIns/softmanager.xlplugin
# 会员中心
chmod a-x /Applications/Thunder.app/Contents/PlugIns/myvip.xlplugin
# 开通会员
chmod a-x /Applications/Thunder.app/Contents/PlugIns/viprenew.xlplugin
# 下载宝
chmod a-x /Applications/Thunder.app/Contents/PlugIns/xiazaibao.xlplugin
# 搜索
chmod a-x /Applications/Thunder.app/Contents/PlugIns/xlbrowser.xlplugin
```

#### 参考

[删除Mac版迅雷垃圾组件 - 知乎专栏](https://zhuanlan.zhihu.com/p/26882055)

