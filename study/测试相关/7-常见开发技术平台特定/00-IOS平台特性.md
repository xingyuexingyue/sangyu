## Android和iOS比较

1. Android开发者可以控制蓝牙权限，而iOS需要用户前往系统设置才能开启蓝牙。
2. Android既可以在应用市场升级，也可以应用内升级，iOS必须调用官方接口才能升级
3. Android对于列表的操作，需用户长按，跳出操作选项。而iOS，需用户左滑列表。
4. Android平台在设备底部有一个通用导航栏，使用导航栏里的返回按钮，会返回上一个页面或步骤;iOS没有全局导航栏，页面设计时左上角要有返回按钮
5. Android的原生APP通过向右滑则只能进行标签的切换；iOS中向右滑的手势，可以回到上一步
6. Android菜单使用抽屉式导航，通过点击汉堡菜单图标从页面左侧或右侧滑出；iOS标签栏放在APP的底部，不超过5个，可以在APP中的各个主要功能模块之间进行快速切换。
7. 日期选择器iOS中，常见的老虎机卷轴式的日期选择器的，Android APP中使用这种样式的日期选择器需要自定义视图开发
![](https://upload-images.jianshu.io/upload_images/2765653-8bde7fb2ff576b64.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
8. 单选按钮、复选框以及切换按钮等
![](https://upload-images.jianshu.io/upload_images/2765653-bc3351aa0ee9b2fd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
9. Android悬浮操作按钮，iOS中行为召唤按钮，一般位于标签栏的中间。悬浮操作按钮表示APP中的主要操作命令，例如：邮件APP中的写邮件按钮，或社交网络APP中的发布新帖子按钮。
![](https://upload-images.jianshu.io/upload_images/2765653-22abd945a42884c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 原生 APP 嵌入 H5

### 1. 手机 App 可以分成三类

1) 原生 APP

只能用于特定手机平台的开发的 APP 。比如，Android 的 Java，IOS 平台的 Object-C 或者 Swift

2) 混合 APP

把 Web 网页放到特定的容器中，然后再打包成各个平台的原生APP。所以，混合 APP 其实是 H5 + 原生 APP，H5 访问平台接口需要借助 PhoneGap、Cordova、Ionic 等框架

这里简单说下 PhoneGap 是什么？

- 打包：PhoneGap 可以帮助你打造成不同平台 Android 和 iOS 的应用
- 提供接口：PhoneGap 提供一系列的接口访问本地特性的接口，比如摄像头、电话簿等等，不同平台特性是不同的

所以 PhoneGap、Cordova、Ionic 这些框架提供了标准的接口帮助我们去访问平台的接口

3) 跨平台 App 

同时支持多个手机平台。它与混合APP的区别是，不使用 Web 技术，所以跨平台APP页面不是 H5 页面，而是使用自己的语法写的 UI 层，然后编译成各平台的原生 App。比如 React Native、Xamarin、Flutter

比如 React Native 使用 javascript 来构建界面，在运行时翻译成原生组件展示出来，实际上所有界面都是用原生组件。支持跨平台，性能和用户体验高于 webview，接近原生应用，是当前热门的跨平台开发技术。

### 2. WebView 控件

1）原生 APP：需要开发者自己把 WebView 控件放到页面上

iOS ：启动 App 加载视图的时候（loadView()），新建一个 WebView 控件的实例。视图加载成功后（viewDidLoad()），WebView 再去加载外部网页
Android ：页面上添加并设置 WebView 实例，指定生成视图的时候（onCreate()），WebView 实例去加载外部网页。

2）混合APP：利用 Android 和 IOS 上的 WebView 容器，APP 能够执行 html、css 和 js 脚本，展示web页面。如果需要原生功能就添加 bridge 供 javascript 调用。

框架种类：PhoneGap，Cordova，两者之前的关系是 Cordova 是 PhoneGap 的内核，PhoneGap 是 Cordova 的发行版

所有这些框架的共同点，都是使用 Web 技术（HTML5 + CSS + JavaScript）开发页面，再由框架分别打包成 iOS 和安卓的 App 安装包。

基于Cordova加载外部网页，由于页面本身就是网页，所以直接用iframe标签插入外部网页

3) 跨平台 App ：混合 APP 使用 HTML 语言编写页面，再用 WebView 控件加载页面，所以只写一次页面，就能支持多个平台。跨平台APP也能做到多平台支持，但是原理完全不同。

跨平台 APP 的框架，都是使用自己的语法编写页面，不使用 Web 技术，编译的时候再将其转为原生控件，生成原生 APP 。这样就完成解决了 Web 页面性能不佳的问题。下面介绍三个这样的框架

- React Native：使用 JavaScript 语言编写页面
- Xamarin：使用 C# 语言编写页面
- Flutter：使用 Dart 语言编写页面

React Native 虽然也使用 JavaScript 语言，并且写法看上去像 Web 页面，但其实所有控件都是自己定义的，编译时再一一翻译为对应的原生控件。举例来说，React Native 的文本渲染控件是<Text>，翻译成 iOS 控件为UIView，翻译成安卓控件为TextView。这种做即保证了性能，又做到了跨平台支持，所以一诞生就引起开发者的关注，成了热门技术。

### 3. 内嵌H5与原生APP实现交互

不管 iOS 还是 Android 都有因为有了 WebView 这个 APP 内嵌浏览器视图，从而使H5可以嵌入到原生 APP 中（原理几乎和PC端请求，加载，选择是一样的）

一般将 H5 开发好后将可以有两种方式请求到原生 APP 中，一种是将 html 代码放到服务器上， 一个是放在当前 app 项目目录中本地请求（这种方式一般用于调试）

因此，原生APP如何与Web交互以及数据传递等等

3.1 如何实现交互：使用第三方插件JsBridge

1) 通过js伪造请求，原生拦截请求并获取数据

![](https://upload-images.jianshu.io/upload_images/2765653-4aa0197573a59823.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2765653-b53776033aa699d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2) 原生app传递数据给H5界面

原理类似于jsonp  首先在js中定义一个函数并挂载在window下，然后在原生中调用这个函数并传值

js部分：

![](https://upload-images.jianshu.io/upload_images/2765653-d04744e127265bef.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

原生部分：

![](https://upload-images.jianshu.io/upload_images/2765653-6710944a2e9a4695.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 4. H5与native交互测试点

4.1 登录相关

1) 登录态获取及保持，H5与native相互联通，在H5页面操作登录的请求需要调起native登录，双方保持会话相通；若客户端已登录，那么进入H5后仍然是登录状态
2) 登录态刷新，在app中访问H5页面，登录态有一定的刷新处理机制，根据定义的机制，验证刷新方法、刷新时机、刷新成功与否
3) 登录异常，保持登录态的情况下，需关注验证点是H5页面内操作发起每个请求发生登录超时等登录异常场景需要跳转到native登录页，或者重定向到哪个native页面

4.2 数据共享相关

1) H5与native双方共享数据，H5获取的用户信息等信息，验证迁移或同步数据的正确性
2) 设置和获取存储数据，H5可能需要设置临时和永久数据，如 首次访问H5页面时需要授权等操作，H5会设置临时存储数据，下次进来会获取临时存储的数据，不需重新授权。验证其数据存储是否正确。

4.3 页面相关

1) H5页面导航栏，对导航栏按钮的控制也是js调用native的方法，验证native提供的展示、屏蔽、关闭、返回等方法
2) H5页面之间跳转及逐级返回操作，H5页面运行在webview中，根据项目需求及用户体验验证跳转和逐级返回操作是否正常。例如有多个H5页面时，其中一个为数据加载失败的情感页，在刷新情感页后，验证查看情感页是否消失，否则返回操作时会出现情感页。

4.4 翻页

1) 分页数据加载，快速操作场景中，请求页数是不是依次递增，快速操作（如第一页尚未loading出来的时候仍然继续上拉操作）时是否发出去对应的请求了。
                  
4.5 刷新

1) 下拉刷新是否仍然处于当前页面
2) 用户主动点击刷新按钮是否仍然处于当前页面

4.6 数据的请求与返回

1) 提交了数据，数据是否正确的整理到后台管理系统
2) 发送了请求，是否正确返回你要求的数据

4.7 H5适配相关

1) 大屏（如720*1280，重点关注页面背景是否完全撑开页面，刷新是否有抖动）

2) 小屏手机（如320*480，重点关注下弹框样式和文案折行）
   
3) android2.3、android4.X随机找一个即可
   
4) ios5、ios6、ios7
   
5) 浏览器上也要能够进行完美展示

4.8 体验相关

1) 页面中有图片的话，淘宝那边建议图片一般不大于50kb，本着一个原则，尽量缩小图片

2) 资源是否压缩、是否通过CDN加载。---CDN是什么？---就近地区访问，服务速度会更快

3) 对于一些不会变化的图片，如游戏动画效果相关图片，不需要每次都请求的东西，做本地缓存

4) 数据较多时是否做了分页加载

5) 关注页面首屏加载时间

6) 弱网络下，数据加载较慢，是否有对应的loading提示

7) 接口获取异常时，提示是否友好

8) 刷新页面或者加载新内容时页面是否有抖动

9) 锁屏之后展示页面

10) 回退到后台之后，重新呼出在前台展示

11) 手指滑动是否流畅，手指点击时焦点是否定位正确，不同机型会不一样。焦点地位后点击是否灵敏

12) 清除APP缓存，因为图片和文件会被缓存下来，所以首次访问和二次访问体验不一样。

4.9 如何判断一个应用界面是native还是web界面

1) 打开开发者选项，在开发者选项中勾选上显示布局边界再返回到App界面，如果App是Html的界面，那界面不会有布局边界显示，有就是native的

2) 利用手机复制功能，长按屏幕出现复制选项的话就说明是H5




                  

