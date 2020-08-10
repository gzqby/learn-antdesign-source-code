## 1.前言  
React是现在最受欢迎的前端框架之一，作为前端开发人员，掌握react应用的高阶技巧是评估一个React工程师是否优秀的标准。  
AntDesign是阿里开源的优秀的React前端UI框架，广受社区欢迎，并逐渐发展为很多公司前端的基础技术栈。所以以Antd为契机，学习源码，学习React的高阶技巧，是一举多得的事情。  
## 2.整体规划  
### 2.1 学习目录
```
├─components
│  ├─affix
│  ├─alert
│  ├─anchor
│  ├─auto-complete
│  ├─avatar
│  ├─back-top
│  ├─badge
│  ├─breadcrumb
│  ├─button
│  ├─calendar
│  ├─card
│  ├─carousel
│  ├─cascader
│  ├─checkbox
│  ├─col
│  ├─collapse
│  ├─comment
│  ├─config-provider
│  ├─date-picker
│  ├─descriptions
│  ├─divider
│  ├─drawer
│  ├─dropdown
│  ├─empty
│  ├─form
│  ├─grid
│  ├─icon
│  ├─input
│  ├─input-number
│  ├─layout
│  ├─list
│  ├─locale
│  ├─locale-provider
│  ├─mention
│  ├─mentions
│  ├─menu
│  ├─message
│  ├─modal
│  ├─notification
│  ├─page-header
│  ├─pagination
│  ├─popconfirm
│  ├─popover
│  ├─progress
│  ├─radio
│  ├─rate
│  ├─result
│  ├─row
│  ├─select
│  ├─skeleton
│  ├─slider
│  ├─spin
│  ├─statistic
│  ├─steps
│  ├─style
│  ├─switch
│  ├─table
│  ├─tabs
│  ├─tag
│  ├─time-picker
│  ├─timeline
│  ├─tooltip
│  ├─transfer
│  ├─tree
│  ├─tree-select
│  ├─typography
│  ├─upload
│  ├─version
│  ├─_util
│  └─__tests__
├─docs
├─scripts
├─site
├─tests
└─typings
```
从以上的结构可以看出，Antdesign整个项目包括components、docs、scripts、site、tests、typings等，学习的目标主要是学习组件技巧，所以我们重点关注components。  
### 2.2 学习路线
拿到一个前端项目，第一件事肯定是看项目结构与package.json，对项目有一个认知。作为一个UI库，重点欺切入到components。  
component学习从易到难，一步步梳理所以的组件。所以我选择从文档中第一个组件开始。（这个过程不是在教学，是我的学习记录，可能到最后会有个更优的总结。怎样快速到掌握技巧的目的）  
```
通用：
Button -> config-provide -> locale-provide -> Icon -> Typography  
通用这块是一个小缓冲，能看到一些全局的东西，但又不会因为组件太难很思路卡顿，不能进行。到下一阶段也会更能集中精力理解组件问题，包括思想什么的。  
从上也能看到一些架构思想，小型组件由props决定，各种逻辑由组件内部根据props处理，算是服务到位的操作。  
再大一点，可以形成分组，分组处理不同逻辑，以Base类处理分组，多一层抽象。  
覆盖默认事件传递参数。  
布局：
导航：
Menu -> Dropdown -> Pagination
通过进一步深入，AntD多是基于Rc基础组建的再封装，形成整体的生态，加一些补充直接antd内部以Base组件形式的一层。进一步掌握技巧以Rc为主。
数据录入：
数据展示：
反馈：
Rc:
RcMenu ->
根据组件实现目标定义属性，划分属性类型（两类）：由外部驱动更新或者说初始化后不更新，由组件自身维护更新。
封装组件可以给以可识别的实属，eg.name,isThat
方法封装应贴近标准方法使用逻辑
RcMenu把组件的方法抽象到顶层组件，以static组织组件，以render props分发顶层的的方法属性（在分发过程中处理当前层的数据，即分发过程经过层级的需求而定是否在当前层做具体操作，还是直接传递函数暴露正常的事件）。
Dropdown ->  
样式机制以传入为主，默认为辅，无传入走默认。事件机制callback形式暴露。
Trigger ->
onClick, onMouseDown, onTouchStart: click鼠标点下松开才执行，mouseDown,touchStart直接执行; click落入点不在此处不执行。事件对象不能直接event出来详细信息了。（怎么做到的？）
trigger和Portal组成，trigger是自己的children；利用event.pageX,event.pageY定位
Align -> 
使用hook技术，  
附加ref, 使用的和内部ref分离  
useImperativeHandle给父级定义返回的ref内容  
```
React.useEffect(() => () => {})作为unmount什么周期
React.useEffect分离分别处理更新逻辑
在分离的基础上利用useEffect(arg1,arg2)第二个参数做，针对个别配置项eg:
React.useEffect(() => {
  if (monitorWindowResize) {
<!-- 配置为true去addEventListenner -->
    if (!winResizeRef.current) {
      winResizeRef.current = addEventListener(window, 'resize', forceAlign);
    }
  } else if (winResizeRef.current) {
    winResizeRef.current.remove();
    winResizeRef.current = null;
  }
}, [monitorWindowResize]);
<!-- 这个配置项正常开发是不会变化的，但是利用这个更简洁的做了变化的处理 -->
```
RcTable -> 
-- jsx可以是指向有意义的字符串
```
const Com = 'div'
<Com></Com>
```
-- React.memo(FunCom, areEqual),不影响state,context变更
-- tbody第一列监听onResize
RcResizeObserver ->
-- 使用ResizeObserver监听子元素的boundingClientRect
rcFieldForm ->
-- 通过useForm形成form方法集合，SO 无论是传入的form还是自生产的都不能少useForm  
```
### 2.3 学习输出
通过一步步的进行，我准备输出以下几项：  
-- 以文字形式记录学习过程体会  
-- 源码中写注释，方便翻阅  
-- 一个更优学习方法的建议，或者以另一个高度给出总结  

# Summary. 
基本烂尾了，因为组件太多了，手里事也比较多。中间也处理了antd的几个issue，有需要改代码的，也有只是看一看代码发现是提issue者没搞清楚用法的。做一个总结，假如让我写一个reactUI库，我可能只记得2件事：
1. 数据驱动React  
2. 合理抽象  
