# 学习WCM相关
## 一、关于WCM
#### 1 什么是WCM
TRS WCM内容协作平台是一套完全基于Java和浏览器技术的网络内容管理软件，TRS WCM集中了浏览器内容创建和协作、内容交付、基于模板的内容发布、强大的站点管理于一身，并提供企业级的团队协作服务。利用TRS WCM可以轻松创建企业内部站点、外部资源门户、企业信息管理平台、企业工作协作平台等等。
TRS WCM面向非专业人员创建内容门户和实现信息共享，提供所有流行文档格式的转换，并且支持产生多种发布媒体支持多种信息终端。易于管理和使用的浏览器平台让使用者可以在极短的时间内完成内容的创建和发布。
#### 2 基本概念
- **库**：相同类型站点的集合，分为文字库、图片库、视频库和资源库。
- **站点**：WCM系统最主要的对象，负责组织和管理栏目。一个站点相当于一个Internet网站，可以按照网站的结构来设计站点及栏目。
- **栏目**：站点的下一级管理单元，用来组织和管理文档。栏目的存在必须依附于站点，没有站点便不能建立栏目。
- **文档**：WCM系统的基本单元，也是系统的核心数据内容。系统中的每一篇文档都必须建立在某个栏目下，由具备特定权限的用户来操作和管理。
- **模板**：带有TRS置标的HTML文件，用来控制发布页面的显示。系统中的站点、栏目、文档都可以分别配备不同类型模板。
- **发布**：将系统中的数据结合模板置标生成HTML页面的过程。设置了完整发布属性的站点、栏目及文档都可以执行发布操作。
- **预览**：在对象发布之前，通过预览功能可以提前查看站点、栏目和文档发布后的效果。

#### 3 WCM相关操作
###### 3.1 建立站点：
a、选择需要建立的库，点击鼠标右键，选择新建站点。
![](http://i1.piimg.com/581766/c995b7cc4ecc106f.png)

b、在弹出的对话框中填写必要信息，点击确定。需要注意：站点的唯一标识和存放位置不能和系统中已有的站点重名。
![](http://i1.piimg.com/581766/06d5d3031f224232.png)
###### 3.2 建立模板
a、依次点击左侧导航区新建的站点，点击下方标签栏中的模板，点击右侧站点模板操作任务新建一个模板
![](http://i1.piimg.com/581766/9dd645c5fabf091c.png)
b、在弹出的对话框中填写模板名称，选择模板类型为概览
![](http://i1.piimg.com/581766/5594b7d1cf3f92a5.png)

c、选择合适的置标类型，编辑置标属性，将代码插入并保存。
![](http://p1.bpimg.com/581766/aa742f41f00cda31.png)
![](http://p1.bpimg.com/581766/882338de336d4010.png)
![](http://p1.bpimg.com/581766/b8deed00f3d05dc8.png)
d、重复以上步骤建立一个细览模板
![](http://i1.piimg.com/581766/1fdde1ca42dc802d.png)
###### 3.3 建立栏目
a、选择要创建栏目的站点，点击鼠标右键，新建栏目。
![](http://p1.bqimg.com/581766/7265a85df3a09239.png)

b、在弹出的对话框中填写唯一标识、显示名称、存放位置，以及选择首页模板、细览模板。
![](http://p1.bqimg.com/581766/20c6a34b7e1e2a94.png)
![](http://p1.bqimg.com/581766/7e3ee3c32cf912dc.png)
###### 3.4 建立文档
填写文档标题、文档内容，选择模板，点击保存并关闭。
![](http://p1.bpimg.com/581766/54e67b6ac57c5d61.png)
![](http://p1.bqimg.com/581766/6ede7a1f0b5f1f69.png)
## 二、发布产品列表页和详情页
#### 1 预览和发布
###### 1.1 选中一篇文档，点击预览这篇文档
![](http://p1.bqimg.com/581766/d30c1f83162fc6cas.png)
###### 1.2 选择一个栏目，点击预览这个栏目
![](http://i1.piimg.com/581766/80c3e37a0baeb44f.png)
###### 1.3 对栏目进行增量发布
![](http://p1.bpimg.com/581766/a08fe5d47a4f4daa.png)
###### 1.4 网页预览效果
![](http://p1.bqimg.com/581766/1270f02bb52a7aa7.png)
![](http://p1.bqimg.com/581766/f8d63217151adf8c.png)
#### 2 模板代码
###### 2.1 概览模板
```
<HTML>
<HEAD>
	<META http-equiv="Content-Type" content="textml; charset=utf-8" />
	<TITLE>产品列表</TITLE>
</HEAD>
<BODY>
<font style="font-size: 10.8pt">
<TRS_CURPAGE value="->" only="FALSE" autolink="TRUE" target="_blank"  homepagedesc="首页">当前位置</TRS_CURPAGE>

<table width="100%" cellspacing="0" cellpadding="0" border="0">
<TRS_DOCUMENTS id="OWNER"  channeltype="0"  num="50" startpos="0" automore="FALSE" moretarget="_blank" moretext="更多..."      enablelimit="FALSE">
	<tr>
		<td width="100%" align="left">
			<TRS_DOCUMENT FIELD="DOCTITLE">冰箱</TRS_DOCUMENT>
		</td>
	</tr>
</TRS_DOCUMENTS>
</table>
</font>
</BODY>
</HTML>
```
###### 2.2 细览模板
```
<HTML>
<BODY>
 <font style="font-size: 10.8pt;line-height: 150%">
    <TRS_CURPAGE value="->" only="FALSE" autolink="TRUE" target="_blank"  homepagedesc="首页"></TRS_CURPAGE>
 <p align="center">
<font style="font-size: 12pt">
    <b>
    <TRS_DOCUMENT field="DOCTITLE"  dateformat="yyyy-MM-dd HH:mm:ss" autocolor="TRUE" autoformat="FALSE" autoformattype="HTML" autolink="FALSE"  target="_blank" linkalt="FALSE" >海尔冰箱5000</TRS_DOCUMENT>
    </b>
    </font>
<br><br>
<font style="font-size: 12pt" color=red>
来源：<TRS_DOCUMENT field="DOCSOURCENAME"  dateformat="yyyy-MM-dd HH:mm:ss" autocolor="TRUE" autoformat="FALSE" autoformattype="HTML" autolink="FALSE"  target="_blank" linkalt="FALSE" >来源</TRS_DOCUMENT><TRS_DATETIME dateformat="yyyy-MM-dd HH:mm:ss">时间</TRS_DATETIME>
</font>
</p>
<table border="0" cellspacing="0" cellpadding="0">
	<tr>
		<td>
			<TRS_APPENDIX field="APPDESC" mode="PIC" index="-1" target="_blank"   autolink="TRUE"  memo="FALSE"   seperator="<BR>" upload="FALSE">图片</TRS_APPENDIX>
		</td>
	</tr>
</table>
<TRS_DOCUMENT field="DOCHTMLCON"  dateformat="yyyy-MM-dd+HH:mm:ss" autocolor="TRUE" autoformat="FALSE" autoformattype="HTML" autolink="FALSE"  target="_blank" linkalt="FALSE" >正文</TRS_DOCUMENT>
<p>
相关新闻：
<table border="0" cellspacing="0" cellpadding="0">
<TRS_RELNEWS startpos="0" num="10" mode="USERDEF">
	<tr>
		<td>
			<TRS_DOCUMENT FIELD="DOCTITLE">标题</TRS_DOCUMENT>
		</td>
	</tr>
</TRS_RELNEWS>
</table>
    </font>

</BODY>
</HTML>
```
