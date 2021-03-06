# angular-cron-jobs
UI Component For Creating Cron Job Syntax To Send To Server

##[DEMO](http://jacobscarter.github.io/angular-cron-jobs/#/)
##Installation

Install using bower:

`bower install angular-cron-jobs`

##Use:

Include the component in your application:

    angular.module('myApp', ['angular-cron-jobs']);

Insert the directive where you would like it to appear in your application:

    <cron-selection output="myOutput"></cron-selection>

By setting the output attribute equal to a value in your controller (i.e. `$scope.myOutput` in the example above) you have access to the cron syntax output.  

For example, a job selected to run every month on the 11th at 4:10 AM would output the follow:

    '10 4 11 * *'

as a string.

##Configuration:

The directive takes an optional attribute of `config`

    <cron-selection output="myOutput" config="myConfig"></cron-selection>

This is an object in your controller you can use to remove options from the user.  For example if you would like the user to be able to set Minute, Hour, and Day but not Week, Month, and Year you would create the following object in your controller:

    $scope.myConfig = {
        options: {
            allowWeek : false,
            allowMonth : false,
            allowYear : false
        }
    }

Currently the config object accepts an options property with an object of allowed selections.  These include:

* allowMinute
* allowHour
* allowDay
* allowWeek
* allowMonth
* allowYear

Setting the keys as booleans will turn the selection on and off.

You can also set whether or not you want to allow a user to select multiple calues for a cron:

    $scope.myConfig = {
        allowMultiple: true
    }

Setting allowMultiple to either true or false will toggle the ability.

A complete config object may look like the following:

    $scope.myConfig = {
        allowMultiple: true,
        options: {
            allowWeek : false,
            allowMonth : false,
            allowYear : false
        }
    }

##Custom Templates:

As noted by [TimotheeJeannin](https://github.com/TimotheeJeannin) you can use custom template by setting the template attribute on your cron DOM element:

    <cron-selection template="path/to/my/template.html"></cron-selection>

##Initializing UI with data from server

The directive takes an optional attribute of `init`

    <cron-selection output="myOutput" config="myConfig" init="serverData"></cron-selection>

This is a string in your controller of cron syntax that was recieved from your server or any other source:

    $scope.serverData = "30 2 4 * *"
    
Thew directive will properly build out the UI to reflect this data.

##Setting Cron after directive load

The `init` attribute also works as a reset attribute

    <cron-selection output="myOutput" config="myConfig" init="serverData"></cron-selection>

This is an expression paired with a value in your controller.  Whenever the value changes (or is set for the first time) and passed the `angular.isDefined()` method the cron will reset itself to match that value

    $timeout(function(){
       $scope.serverData = "0 0 * * *"
    }, 3000);
    
The directive will properly build out the UI to reflect this data.

##Contributors

[@wowo](https://github.com/wowo)

[@immertreu] (https://github.com/immertreu)

[@TSteele27] (https://github.com/TSteele27)


##Coming Soon:

The next big to-do's on my list include:

* Support generlized selections such as a one button click for "Every Five Minutes" or "Last Thursday of Every Month"
