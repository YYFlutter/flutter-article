# 你应该知道的Flutter
公司有团队最近在做一个语音房app，ui层面使用flutter实现，在第一版完成之际做了一次分享。做一下会议笔记，备忘。

## 文件名命名规范

由于是第一次做flutter项目，加上团队小伙伴开发经验不是很足，在满足需求的同时，对其他之外的事情考虑的比较少，每个人在创建dart文件的时候考虑的比较少，当然取名字也是一个很专业的事情，好的名字决定了app的一生。

比如登录页面，login.dart这样简单粗暴，但是要是登录涉及到一些校验，需要弹窗，或者输入验证码，或者第三方登录，或者手机号登录，密码登录，另外又有封禁等，难到这些都怼到一个文件内部吗，那login就不能满足要求了，需要拆分login的其他模块，在这一块的考虑不是很周全。

## 内存问题
flutter启动就有一百兆的内存，业内也有一些解决方案可以部分降低内存，但是也会有崩溃的风险，这是engine内部实现的问题。


图片加载内存过大，这是开发不小心把几张3M+的图片放进去，内存就暴涨，猜其内部实现没有对Image的图片缓存做大小的现在，比如UIImage内部在图片占用内存达到100M的时候会自动回收一部分内存，使用方式也可以根据path加载路径，这样加载完就释放了。这个问题开发其实也是可控的。

## 包体大小

flutter的engine默认加进来就多10兆+的大小，问题说大不大说小不小，因为是海外项目，国外很多低端机型，这个engine的大小又是不可避免的，至少在领导看来是应该需要解决的。虽然很多开发不情愿。

## 日志分类
在原生开发的项目到了一定的复杂程度，日志分析必不可少，然而日志的产生就是编写代码的时候自己加上去的，为了给日后分析线上问题提供唯一的途径。

日志分类在flutter内部几乎是没有规划，尤其对于小项目。目前flutter的日志都是和原生的日志混在一起，如果项目做大，未来跟踪线上问题肯定麻烦事情。
简单说flutter日志应该单独放在一个文件里面。

格式还和原生格式类似 时间+文件名+行号+方法名+tag+log内容

## 崩溃收集
flutter崩溃不同于原生，不会crash，但是会白屏或者一片红，导致用户不得不杀进程才能操作。目前市面有这样的崩溃分析系统，但是不符合公司标准。公司希望统一一套标准，崩溃自动上报到公司内部崩溃系统，带上堆栈信息，另外可以一键提bug指定给对应的人。
游离于公司系统之外，毕竟在项目管理层面来说不是个好消息。

## 性能问题fps、cpu、gpu、耗电量
都是流畅性，跨平台是flutter的优点。

但是也是仅此而已吧，不用太吹嘘，这些是陈词滥调，但是它的cpu，gpu，耗电量对于简单的app来说当然没什么问题，但是涉及到音视频这些项目，原生来说都是个问题，对于flutter更是问题，问题不在于语言，而在于分析的工具侧不完善，performance是个不错的选择，但是用惯了原生性能检测的如instrument这种来说就会觉得flutter的很弱了。

举一个痛点问题，音频上麦，在iphonex 半个小时耗电35%，在flutter上麦怎么查。 鸡贼的办法就是丢给sdk去查了。如果以后这些sdk模块用flutter写了，又怎么查。

## 事件通知处理方式混乱

eventbus和stream都可以处理事件发送接收问题。每个人也有自己的方式，这个在之前没有一个统一的规范写法，导致混乱。跨模块问题目前在flutter方向有一些好的解决方案，如闲鱼的 fish redux

## 跨模块封装问题

flutter代码多了，需要考虑重用问题，沉淀一些东西出来，封装和跨模块，解耦是终极问题，其实和语言已经没关系了，借鉴行业经验，解耦就是需要抽象再抽象，思路不一样，写法不一样。插拔模式思路，应该就抽象出组件，提供注册的方法，提供反注册的方法，再提供一个取的方法。每个模块遵循一些协议。

## 其他项目和sdk的flutter计划

一个音视频的sdk不一定仅仅是这个sdk，它其实也依赖了其他的sdk，如日志，统计，人脸识别，还有其他第三方的。当然全部要用flutter是不现实的。目前来说，公司是有意愿部分通用的慢慢flutter化，但是过程会很漫长效果也不会理想。

然而对于新的app，使用flutter是没有悬念的事情，从成本上面来说这是个优势，另一方面性能上面不损失，就相当于花更少的钱办了同样的事情。当然乐见其成。

## 后续计划
为了在性能上面不损失，不能依赖flutter做ui这些表层的事情了。必须再深入下去，减少包体，降低内存，提高cpu使用效率等等。

### 作者
<table>
  <tbody>
    <tr>
      <td align="center" valign="top">
        <img height="80" width="80" src="https://avatars2.githubusercontent.com/u/3379261?s=128">
        <br>
        <a href="https://github.com/Natoto">共田君</a>
      </td>
     </tr>
  </tbody>
</table>