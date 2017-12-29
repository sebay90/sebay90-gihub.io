<!doctype html>
<html ng-app="myApp">
<head>
    <meta charset="utf-8">
</head>
<body>
<div ng-controller="phoneController">
    <p>Название: {{phone.name}}</p>
    <p>Цена: {{phone.price}} $</p>
    <p>Производитель: {{phone.company.name}}</p>
    <input type="text" ng-model="name" />
    <p >Name: {{name}}</p>
    <my-div></my-div>
    <my-name-div my-name="'test'"></my-name-div>
</div>

<div class="container">
    <my-to-do></my-to-do>
</div>

<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
<link rel="stylesheet" href="styles.css" >
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
<script type="text/javascript">
    var myApp=angular.module('myApp', []);
    myApp.controller('phoneController', function($scope) {

        $scope.phone = {

            name: 'Nokia Lumia 630',
            year: 2014,
            price: 200,
            company: {
                name: 'Nokia',
                country: 'Финляндия'
            }
        }
    });

    function toDoListContoller(){
        console.log("todo");

//        this.todo = [
//            {
//                name: "survive"
//            },
//            {
//                name: "some work"
//            }
//        ]
        this.todo = (localStorage.getItem('todo')!== null) ? JSON.parse(localStorage.getItem('todo')): [];


        this.addTodo = function (){
            console.log(this.todoname);
            this.todo.push({
                id: Math.random().toString(36).substr(2, 10),
                name: this.todoname,
                edit: false
            });
            console.log(this.todo);
            localStorage.setItem("todo", JSON.stringify(this.todo));
        }

        this.delete = function (index){
            this.todo.splice(index,1);
            localStorage.setItem("todo", JSON.stringify(this.todo));
        }

        this.edit = function (index){
            this.todo[index].edit = true;
        }

        this.save = function(index){
            this.todo[index].edit = false;
            localStorage.setItem("todo", JSON.stringify(this.todo));
        }
    }

    function MyDivController() {
        console.log("test");
    }

    function MyNameController () {
        console.log("name");
    }

    myApp.component('myNameDiv', {
        transclude: false,
        restrict: 'E',
        scope: {},
        bindings:{
            myName: '='
        },
        controller: MyNameController,
        template: '<div>{{$ctrl.myName}}</div>'
    });

    myApp.component('myDiv', {
        transclude: false,
        restrict: 'E',
        scope: false,
        controller: MyDivController,
        template: '<div>MyDiv <p>321321</p></div>'
    });

    myApp.component('myToDo', {
        transclude: false,
        restrict: 'E',
        scope: {},
        controller: toDoListContoller,
        controllerAs: 'vm',
        templateUrl: 'my-todo.html'
    });

</script>
</body>
</html>
