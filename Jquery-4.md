```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Jquery-4</title>
    <script src="jquery-1.8.3.js"></script>
    <script src="chajian.js"></script>
    <script>
        $(function () {
            //判断是否为空
            $("#username").isEmpty({msg:"请输入用户名且不允许为空",msgid:"span1"});
            //判断手机号、邮箱是否合法（传入正则表达式）
            $("#tel").isLegal({regular:/^1[3|4|5|8][0-9]\d{4,8}$/,msg:"手机号码输入有误，请重新输入",msgid:"span2"});
            $("#email").isLegal({regular:/^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+(.[a-zA-Z0-9_-])+/,msg:"邮箱输入有误，请重新输入",msgid:"span3"});
            $("#name").isLegal({regular:/^([a-zA-Z0-9\u4e00-\u9fa5\·]{1,10})$/,msg:"姓名输入有误，请重新输入",msgid:"span0"});
            $("#pass1").isLegal({regular:/^[a-zA-Z]\w{5,17}$/,msg:"密码要以字母开头，长度为6-18位,只能包含字符、数字和下划线,请重新输入",msgid:"span5"})
            //判断qq的合法性
            $("#qq").isqq();
            //密码相等验证
            $("#pass2").equal({msgid1:"pass1",msgid2:"pass2",msgid:"span6"});
            //提交判断
            $("#submit").click(function () {
                $.each($("input"),function (i,value) {
                    if($(this).val()==""){
                      $(this).parent().next().children().first().html("请输入信息");
                    }
                })
            });
        });
    </script>
    <style>
        span{color: red}
        #ee{font-size: small;color: darkturquoise}
    </style>
</head>
<body>
<table>
    <tr>
        <td>姓名：</td>
        <td><input type="text" id="name" placeholder="请输入姓名"></td>
        <td><span id="span0"></span></td>
    </tr>
    <tr><td>用户名：</td>
        <td><input type="text" id="username" placeholder="请输入用户名"></td>
        <td><span id="span1"></span></td>
    </tr>
    <tr>
        <td>手机号：</td>
        <td><input type="tel" id="tel" placeholder="请输入手机号" maxlength="11"></td>
        <td><span id="span2"></span></td>
    </tr>
    <tr>
        <td>邮箱：</td>
        <td><input type="email" id="email" placeholder="请输入邮箱"></td>
        <td><span id="span3"></span></td>
    </tr>
    <tr>
        <td>QQ:</td>
        <td><input type="text" id="qq" placeholder="请输入QQ" maxlength="11"></td>
        <td><span id="span4"></span></td>
    </tr>
    <tr>
        <td>密码：</td>
        <td><input type="password" id="pass1" placeholder="以字母开头，长度为6-18位" maxlength="18"></td>
        <td><span id="span5"></span></td>
    </tr>
    <tr>
        <td>确认密码：</td>
        <td><input type="password" id="pass2" placeholder="请再次输入密码" maxlength="18"></td>
        <td><span id="span6"></span></td>
    </tr>
    <tr>
        <td></td>
        <td><input id="submit" type="submit" value="提交"></td>
        <td></td>
    </tr>
</table>
</body>
</html>
```
#### chajian.js源码
```
/**
 * Created by LiJie on 2017/1/3.
 */
(function(){
    //判断密码相等
    $.fn.equal=function (param) {
        $("#"+param.msgid2).blur(function () {
            if($("#"+param.msgid2).val()!=$("#"+param.msgid1).val()){
                $("#"+param.msgid).html("两次输入的密码不相等，请重新输入");
                $("#"+param.msgid2).val("");
            }
        });
        $("#"+param.msgid2).focus(function () {
            $("#"+param.msgid).html("");
        });
    }
    //判断qq的合法性
    $.fn.isqq=function (param) {
        $(this).blur(function () {
            if($(this).val().replace(/(^\s*)|(\s*$)/g,'')==""||isNaN($(this).val())){
                $("#span4").html("请输入正确的QQ号，不允许使用空格等非法字符");
                $("#qq").val("");
            }else if($(this).val().length<4||$(this).val().length>11){
                $("#span4").html("请输入正确位数的QQ号")
            };
        });
        $(this).focus(function () {
            $("#span4").html("");
        });
    }
    //判断输入是否合法（正则表达式)
    $.fn.isLegal=function(param){
        $(this).blur(function () {
            if(!(param.regular.test($(this).val()))){
                $("#"+param.msgid).html(param.msg);
            };
        });
        $(this).focus(function () {
            $("#"+param.msgid).html("");
        });
    }
    //定义判断输入是否为空的插件
    $.fn.isEmpty=function(param) {
        //获得焦点时
        $(this).focus(function () {
            $("#"+param.msgid).html("");
        });
        //失去焦点时判断是否为空
        $(this).blur(function () {
            if($(this).val()==""){
                $("#"+param.msgid).html(param.msg);
            }else{
                $("#"+param.msgid).html("");
            }
        });
    }
    
    //定义表格变色插件
    $.fn.bianse=function(p){
        //默认样式
        var defaults={thcolor:"#ccc",evencolor:"red",oddcolor:"green",hovercolor:"blue"};
        //将传入的样式与默认样式合并
        var result=$.extend(defaults,p);
        //找到当前元素的th孩子，设置背景色
        $(this).find("th").css("background-color",result.thcolor);
        //找到当前元素的tr偶数行，设置背景色
        $(this).find("tr:even").css("background-color",result.evencolor);
        //找到当前元素的tr奇数行，设置背景色
        $(this).find("tr:odd").css("background-color",result.oddcolor);
        //浮动变色
        $(this).find("tr").hover(function () {
            $(this).css("background-color",result.hovercolor);
        },function () {
            $(this).parent().find("tr:even").css("background-color",result.evencolor);
            $(this).parent().find("tr:odd").css("background-color",result.oddcolor);
        });
    }
})(jQuery);
```
