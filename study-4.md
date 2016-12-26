# 综合实战
## 1、创建数据库
![](http://p1.bpimg.com/581766/7893ca9c53b372fa.png)
## 2、创建新的maven项目
项目整体结构：

![](http://p1.bpimg.com/581766/463551e0a2da4acd.png)
#### 2.1 配置pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>trs.com.cn</groupId>
    <artifactId>product_comment</artifactId>
    <version>1.0-SNAPSHOT</version>

    <packaging>war</packaging>

    <parent>
        <artifactId>season-parent</artifactId>
        <groupId>trs.com.cn</groupId>
        <version>1.4-SNAPSHOT</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>trs.com.cn</groupId>
            <artifactId>season-core</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <finalName>CommentTest</finalName>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>haier-maven-repository</id>
            <url>http://test.haier.com/nexus/content/groups/public/</url>
        </repository>
    </repositories>

</project>
```
#### 2.2 创建启动类
```
public class App extends SeasonApplication{
    public static void main(String[] args) {
        SeasonRunner.run(App.class);
    }
}
```
#### 2.3 连接数据库
在resource中添加配置文件application.properties
```
server.context-path=/season
season.datasources[0].id=master
season.datasources[0].url=jdbc:mysql://localhost:3306/product?useUnicode=true&characterEncoding=UTF-8&autoReconnect=true&failOverReadOnly=false&zeroDateTimeBehavior=convertToNull
season.datasources[0].username=root
season.datasources[0].password=123
```
#### 2.4 创建实体类
```
package com.trs.model;

import com.season.core.db.Pojo;
import com.season.core.db.annotation.TableInfo;

import java.util.Date;

/**
 * Created by LiJie on 2016/12/22.
 */
@TableInfo(tableName = comment.tableName,pkName = "id")
public class comment extends Pojo<comment>{

    public static final String tableName="comment";
    private int id;
    private String name;
    private String content;
    private String date;

    public comment() {
    }

    public comment(String name, String content) {
        this.name = name;
        this.content = content;
    }

    public comment(int id, String name, String content, String date) {
        this.id = id;
        this.name = name;
        this.content = content;
        this.date = date;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public String getContent() {
        return content;
    }

    public String getDate() {
        return date;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setContent(String content) {
        this.content = content;
    }

    public void setDate(String date) {
        this.date = date;
    }
}
```
#### 2.5 创建数据层
```
package com.trs.dao;

import com.season.core.db.Dao;
import com.trs.model.comment;
import org.springframework.stereotype.Repository;

/**
 * Created by LiJie on 2016/12/22.
 */
@Repository
public class commentDao {
    //查询所有评论
    public java.util.List<comment> getAllComment(){
        return Dao.findAll(comment.class);
    }
    //新增评论
    public void addComment(comment comment){
        Dao.save(comment);
    }
    //修改评论
    public void editComment(comment comment){
        Dao.update(comment);
    }
    //删除评论
    public void deleteComment(int id){
        Dao.deleteById(comment.class,id);
    }
}
```
#### 2.6 创建服务层
```
package com.trs.service;

import com.trs.dao.commentDao;
import com.trs.model.comment;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

/**
 * Created by LiJie on 2016/12/22.
 */
@Service
public class commentService {
    @Autowired
    private commentDao commentDao;
    //查询所有评论
    public List<comment> getAllComment(){
        return commentDao.getAllComment();
    }
    //增加评论
    public void addComment(comment comment){
        commentDao.addComment(comment);
    }
    //修改评论
    public void editComment(comment comment){
        commentDao.editComment(comment);
    }
    //删除评论
    public void deleteComment(int id){
        commentDao.deleteComment(id);
    }
}
```
#### 2.7 创建控制层
```
package com.trs.controller;

import com.season.core.ActionKey;
import com.season.core.Controller;
import com.season.core.ControllerKey;
import com.trs.model.comment;
import com.trs.service.commentService;
import org.springframework.beans.factory.annotation.Autowired;

import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.List;

/**
 * Created by LiJie on 2016/12/23.
 */
@ControllerKey("comment")
public class commentController extends Controller{
    @Autowired
    private commentService commentService;
    //查询所有
    @ActionKey("getAllComment")
    public void getAllComment(){
        List<comment> all=commentService.getAllComment();
        renderJson("comments",all);
    }
    //新增
    @ActionKey("addComment")
    public void addComment(){
        comment comment=new comment();
        comment.setContent(getPara("comment"));
        comment.setDate(new SimpleDateFormat("yy-MM-dd HH:mm:ss").format(new Date().getTime()));
        comment.setName("冰箱");
        commentService.addComment(comment);
        renderJson();
    }
    //删除
    @ActionKey("deleteComment")
    public void deleteComment(){
        int id=getParaToInt("id");
        commentService.deleteComment(id);
    }
    //修改
    @ActionKey("editComment")
    public void editComment(){
        comment comment=new comment();
        comment.setId(getParaToInt("id"));
        comment.setContent(getPara("comment"));
        comment.setName("冰箱");
        comment.setDate(new SimpleDateFormat("yy-MM-dd HH:mm:ss").format(new Date().getTime()));
        commentService.editComment(comment);
        renderJson();
    }
}
```
#### 2.8 前台页面
```
<!DOCTYPE html>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
<html>
<head>
    <meta charset="UTF-8">
    <title>商品详情</title>

    <script type="text/javascript" src="jquery-1.8.3.js"></script>

    <script type="text/javascript">
    $(document).ready(function() {

        $(function bb() {
            //查询显示所有评论
            $.ajax({
                type: "get",
                dataType: "json",
                url: "http://localhost:8080/season/comment/getAllComment",
                data: null,
                success: function (data) {
                    $("#commentDiv").empty();
                    var commentsText = "";
                    $.each(data.comments, function (commentIndex, comment) {
                        commentsText += "<li>" +
                                "<div style='background-color: #d9fff7'>" + "游客" + comment.id + "说：</div>" +
                                "<div style='background-color: #fff3f3'><b>" + comment.content +
                                "&nbsp&nbsp" + "<button id='" + comment.id + "' onclick='dd(" + comment.id + ",\"" + comment.content + "\")'>" + "修改" + "</button>" +
                                "&nbsp&nbsp" + "<button id='" + comment.id + "' onclick='cc(" + comment.id + ")'>" + "删除" + "</button>" + "</b></div>" +
                                "<div style='background-color: #ffff00'>" + "评论时间：" + comment.date + "</div>" +
                                "</li>";
                    });
                    $("#commentDiv").append(commentsText);
                }
            });
        });


        $("#a_c").click(function aa () {
            //发表提交评论
            var enterComment = $("#comment").val().replace(/(^\s*)|(\s*$)/g, "");

            if(enterComment==""){
                alert("评论内容不能为空，请先填写评论再发表");
            }else{
                if(confirm("确定发表评论？"))
                {
                    $.ajax({
                        type: "post",
                        dataType: "json",
                        url: "http://localhost:8080/season/comment/addComment",
                        data: {
                            comment: enterComment
                        },
                        success: function (data) {
                            location.href="http://localhost:8080/season/index.html"
                        }
                    });
                    alert("评论成功")
                }else{
                    alert("评论失败，评论未发表")
                }
            }
        });
    });
    function cc(id) {
        //删除评论
        if(confirm("确认删除此条评论？")){
            $.ajax({
                type: "post",
                dataType: "json",
                url: "http://localhost:8080/season/comment/deleteComment?id=" + id,
                data: id,
                success: function (data) {
                    location.href = "http://localhost:8080/season/index.html"
                }
            });
            alert("删除成功")
        }else{
            alert("删除取消")
        }
    }

    function dd(id, content) {
        //修改评论
        $("#comment").val(content);
        $("#a_c").hide();
        $("#b_c").remove();
        $("#c_c").remove();
        $("#div1").append("<button id='b_c' >确认修改</button><button id='c_c' >取消</button>");
        $("#b_c").click(function () {
            var changeComment = $("#comment").val().replace(/(^\s*)|(\s*$)/g, "");
            if(changeComment==""){
                alert("评论内容不能为空，请先填写评论再修改");
            }else{
                if(confirm("确定修改评论？"))
                {
                    $.ajax({
                        type: "get",
                        dataType: "json",
                        url:"http://localhost:8080/season/comment/editComment?id="+id,
                        data: {
                            comment: changeComment
                        },
                        success: function (data) {
                            location.href = "http://localhost:8080/season/index.html"
                        }
                    })
                    alert("评论修改成功")
                }else{
                    alert("评论修改失败")
                }
            }
        })
        //点击取消按钮，放弃评论
        $("#c_c").click(function () {
            window.location.reload();
        })
    }

    </script>
    <script type="text/javascript">
    function test() {
    alert("ok");
    }
    </script>

</head>


<body>
<p align=center>
    <font style="font-size:14pt" color="blue">
        <span> Haier/海尔 BCD-580WBCRH 卡萨帝铂晶对开门冰箱 </span>
    </font>
    <br><br>

    <button onclick="test()">测试</button>

    <FONT style="font-size:9pt" color="red">
        来源：<TRS_DOCUMENT FIELD="DOCSOURCE" AUTOLINK="TRUE">淘宝网  </TRS_DOCUMENT>
        时间：<TRS_DATETIME>2016.12.23 10:42:15</TRS_DATETIME>
    </FONT>
    <br><br>


    <img align="center" style="width: 25%; height: 50%" src='1.jpg' border=0/>
    <br><br>

    <font style="font-size:15pt" >
        <span style="background-color: aquamarine"> 铂晶对开门冰箱，vc保鲜；光波增鲜,风冷无霜制冷技术，冷冻速度快，食材由内到外均匀冻透，保鲜效果好；VC保鲜，实现保湿、保鲜、杀菌除异味三重功效；光波增鲜，释放5种仿自然光波，让果蔬在冰箱也能进行光合作用 </span>
    </font>
    <br><br>

</p>
<br><br>

<div id="div1">
    请发表您的评论：<br>
    <textarea type="text" id="comment" cols="80" rows="2"></textarea>
    <input type="button" id="a_c" value="发表" style="border: antiquewhite "/>
</div>

<div id="commentDiv"></div>

</body>
</html>
```
## 3、项目运行结果
![](http://p1.bqimg.com/581766/47776ccda3d7200f.png)
#### 3.1 显示全部评论
![](http://p1.bqimg.com/581766/67e2055dab69dfaf.png)
#### 3.2 添加评论
在录入框中填写评论，点击发表按钮添加评论
![](http://i1.piimg.com/581766/ffdca6362b82f7e6s.png)
![](http://i1.piimg.com/581766/207eb57099dd9463.png)
#### 3.3 修改评论
点击要修改的评论对应后面的修改按钮；
录入框中会出现要修改的评论的内容，同时后面的发表按钮消失，出现确认修改和取消按钮；

![](http://p1.bqimg.com/581766/b5ae66debb97a8e1s.png)

输入要修改的评论，点击确认修改；
![](http://p1.bpimg.com/581766/f83d35b0e408647d.png)
评论修改成功~~

![](http://p1.bpimg.com/581766/40d3f0d16477e1d6.png)
#### 3.4 删除评论
点击要删除的评论后的删除按钮；
![](http://p1.bqimg.com/581766/26392793fc2c852a.png)
成功删除~

![](http://p1.bqimg.com/581766/ffa3e9ece1995474.png)
