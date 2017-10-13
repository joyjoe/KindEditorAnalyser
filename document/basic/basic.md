# KindEditor编辑器源码分析
本项目是针对4.1.11版本源码进行的分析
## 源码结构
使用闭包功能，全局只暴露KindEditor变量给开发者使用  
KindEditor变量是一个函数对象(line 1832)，包含如下静态成员(line 22 ~ 182)  
* 静态属性和方法
    * VERSION 版本号
    * IE 是否为IE
    * NEWIE 是否为NEWIE
    * GECKO 是否为GECKO
    * WEBKIT 是否为WEBKIT内核
    * OPERA 是否为OPERA
    * MOBILE 是否为MOBILE
    * QUIRKS 是否为QUIRKS
    * V 浏览器版本号
    * TIME 加载JS库时间
    * each 遍历类数组对象(与Jquery一致)
    * isArray 判断是否为数组
    * isFunction 判断是否为函数
    * inArray 查找元素第一次出现的位置
    * inString 判断字符是否出现在字符串中
    * trim 清除字符串两边空白
    * addUnit 为数字类型添加单位(默认px)
    * removeUnit 清除单位
    * escape 特殊字符转义(&,<,>,")
    * unescape 将转义后的字符转回字符
    * toCamel 字符串转驼峰形式
    * toHex 将RGBA格式字符串转换为16进制格式字符串
    * toMap 将数组或字符串转换为Map数据格式value都为true
    * toArray 将类数组转换为数组
    * undef 当参数值为undefined时读取指定默认值
    * invalidUrl 判断URL格式是否正确
    * addParam 拼接get形式URL
    * extend 实现类的继承
    * json 将JSON字符串转换为JSON对象
    * editor
    * Static Method
      * create
      * remove
      * sync
      * html
      * appendHtml
      * insertHtml  
      * ctrl
      * ready
      * query
      * queryAll

这些静态成员都可以在官方文档>基础API中查看详细信息  
其中最重要的方法就是extend了，在源码内部正是利用了这个方法来实现类的定义及类的继承  
如：dialog tab都是继承自widget  
全局变量有一个options这个属性，定义了编辑器的配置参数(line 234 ~ 316)  
这些配置参数包括:  
* designMode
* fullscreenMode
* filterMode
* wellFormatMode
* shadowMode
* loadStyleMode
* basePath
* themesPath
* langPath
* pluginsPath
* themeType
* langType
* urlType
* newlineTag
* resizeType
* syncType
* pasterType
* dialogAlignType
* useContextmenu
* fullscreenShortcut
* bodyClass
* indentChar
* cssPath
* cssData
* minWidth
* minHeight
* minChangeSize
* zIndex
* items
* noDisableItems
* colorTable
* fontSizeTable
* htmlTags
* layout
## 如何生成一个编辑器实例对象
有两种方法可以生成编辑器实例对象:  
* 直接使用构造函数new一个实例  
KindEditor.editor
构造函数是KEditor(对外暴露为KindEditor.EditorClass)  
```
KindEditor.editor(options);
new KindEditor.EditorClass(options);
```
* 利用ready事件的回调函数让系统内部生成一个实例并返回  
```
KindEditor.ready(function(KindEditor){
  // KindEditor 系统内部的构造函数
  // KindEditor.create() 生成KEditor实例
});
```
### 编辑器对象的源码分析
编辑器对象KEditor的源码(line 4885 ~ 5526)  
构造函数接收options参数，同时原型上定义了如下方法:  
* lang
* loadPlugin
* handler
* clickToolbar
* updateState
* addContextmenu
* afterCreate
* beforeRemove
* beforeGetHtml
* beforeSetHtml
* afterSetHtml
* create
* remove
* resize
* select
* html
* fullHtml
* text
* isEmpty
* isDirty
* selectedHtml
* count
* exec
* insertHtml
* appendHtml
* sync
* focus
* blur
* addBookmark
* undo
* redo
* fullscreen
* readonly
* createMenu
* hideMenu
* hideContextmenu
* createDialog
* hideDialog
* errorDialog
## 编辑器内部对象
* KEvent
* KNode
* KRange