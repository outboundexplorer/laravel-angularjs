##using $q.all to specify that all included promises must first be fulfilled

#####simple implementation of form validation			
#####using angular.bind to equate controller as 'this' and $scope 'this'			
#####injecting $scope when using controller as syntax			


https://egghead.io/lessons/angularjs-q-all 

```html
<!DOCTYPE html>
<!-- /angularjs/sandbox/test01.php -->
<html  ng-app="app">
<head>
    <title> AngularJS</title>
    <link rel="stylesheet" href= "/angularjs/sandbox/vendor/bootstrap.css" >
</head>
<body ng-controller= "AppController as appVm" >

<script type= "text/javascript" src= "/angularjs/sandbox/vendor/angular.js" "></ script>
<script type ="text/javascript" src ="/angularjs/sandbox/app.js"></script>
</body>
</html> 
```

```javascript
// angularjs/sandbox/app.js
(function(){
    'use strict' ;

    angular .module('app',[])
        .controller( 'AppController',AppController)
    ;

    function AppController($q, $timeout){
        var vm = this ;

        // Step 1: First of all we set up our deferred object by using var deferred = $q.defer();
        var dOne = $q.defer();
        var dTwo = $q.defer();
        var dThree = $q.defer();

        // Step 2: We resolve the deferred object and return some data to the promise object
        $timeout( function(){
            dOne.resolve("one done");
        }, Math.random ()*3000 );

        $timeout(function(){
            dTwo.resolve("two done");
        }, Math.random ()*3000 );

        $timeout(function(){
            dThree.resolve("three done");
        }, Math.random ()*3000 );

        // Step 3: Once the promise object has been fulfilled, we can perform further actions upon the output data
        dOne .promise .then (success);
        dTwo .promise .then (success);
        dThree .promise .then (success);

        //By using $q.all([]) we can specify that all the promises must be fulfilled before performing further actions
        var all = $q.all([
            dOne.promise,
            dTwo.promise,
            dThree.promise
        ]);
        all .then (success);

        function success(data){
            console. log(data)
        }
    }
})();
```




