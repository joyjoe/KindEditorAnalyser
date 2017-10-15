# plugins插件
编辑器插件分为内置插件和第三方插件  
内置插件，主要与浏览器自带的command有关  

第三方插件，则是为扩展功能而开发的  
* image
* multiimage
* flash
* media
* insertfile
* table
* hr
* emoticons
* map
* baidumap
* pagebreak
* anchor
* link
* unlink
* filemanager

line 5013  
JS库加载完毕执行创建时，需要执行KEditor的create方法
line 5073  
代码会遍历self.items这个集合生成html字符串，然后将其传入KToolbar这个构造函数中生成工具栏  
系统内置实现的插件:
* source (line 5657)
* undo (line 5399)
* redo (line 5402)
* preview
* print
* template
* code
* cut (line 5791)
* copy (line 5791)
* paste (line 5791)
* plainpaste
* wordpaste
* justifyleft
* justfiycenter
* justifyright
* justifyfull
* insertorderedlist
* insertunorderedlist
* indent
* outdent
* subscript
* superscript
* clearhtml
* quickformat
* selectall
* fullscreen (line 5681)
* formatblock (line 5717)
* fontname (line 5746)
* fontsize (line 5762)
* forecolor (line 5779)
* hilitecolor (line 5779)
* bold
* italic
* underline
* strikethrough
* lineheight
* removeformat
* about (line 5801)


afterSetHtml
afterCreate
beforeGetHtml
beforeSetHtml  


line 4998 `addContextmenu`方法的目的是添加右键菜单项到数组`_contextmenus`中  
line 5842, line 5870这两部分代码就添加了30个右键菜单项  
* editLink
* editImage
* editFlash
* editMedia
* editAnchor
* deleteLink
* deleteImage
* deleteFlash
* deleteMedia
* deleteAnchor
* tableprop
* tablecellprop
* tablecolinsertleft
* tablecolinsertright
* tablerowinsertabove
* tablerowinsertbelow
* tablerowmerge
* tablecolmerge
* tablerowsplit
* tbalecolsplit
* tablecoldelete
* tablerowdelete
* tableinsert
* tabledelete  
编辑器在创建时就为文档的鼠标右键绑定了事件`line4652`  
针对每一个菜单项目，判断是否为分隔符。如果不是分隔符则执行condition条件判断函数，满足添加的菜单项目才会被添加到最终的右键菜单项数组中。  
`fontsize`菜单项中罗列的字体大小集合是在`options.fontSizeTable`(line 280)配置项中设置的  