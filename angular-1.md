```

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>angular-1</title>
    <script src="angular.min.js"></script>
    <script src="angular1.js"></script>
    <style>
        td{border: solid 3px #eeeeee;width: 173px;height: 20px;}
        input{border: solid 1px black}
    </style>
</head>
<body ng-app="test">
    <table ng-controller="test1">
        <tr>
            <td><span ng-show="showspan1">{{hello}}</span>
                <input type="text" ng-show="showtext1" ng-model="hello">
            </td>
            <td><span ng-show="showspan1">{{world}}</span>
                <input type="text" ng-show="showtext1" ng-model="world">
            </td>
            <td><input type="button" id="1" value="编辑" ng-click="edit($event)"></td>
        </tr>
        <tr>
            <td><span ng-show="showspan2">{{ni}}</span>
                <input type="text" ng-show="showtext2" ng-model="ni">
            </td>
            <td><span ng-show="showspan2">{{hao}}</span>
                <input type="text" ng-show="showtext2" ng-model="hao">
            </td>
            <td><input type="button" id="2" value="编辑" ng-click="edit($event)"></td>
        </tr>
    </table>
</body>
</html>
```
####　angular1.js源码
```
/**
 * Created by LiJie on 2017/1/4.
 */
var test=angular.module("test",[]);
test.controller("test1",
    function ($scope) {

        //默认是显示span，即span的显示为true
        $scope.showspan1=true;
        $scope.showspan2=true;

        //默认显示的内容
        $scope.hello="Hello";
        $scope.world="World";
        $scope.ni="你";
        $scope.hao="好毒";

        //修改的方法，点击按钮调用
        $scope.edit=function ($event) {
            if($event.target.value=="编辑"){
                $event.target.value="确认修改"
                panduan($event.target.id);
            }else {
                $event.target.value="编辑";
                panduan($event.target.id);
            }
        };
        //判断点击的哪一行的按钮，从而进行操作
        function panduan(id) {
            if(id==1){
                $scope.showspan1=!$scope.showspan1;
                $scope.showtext1=!$scope.showspan1;
            }else if(id==2){
                $scope.showspan2=!$scope.showspan2;
                $scope.showtext2=!$scope.showspan2;
            }
        }
})
```
