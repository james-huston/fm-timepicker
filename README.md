fm-timepicker
=============

[Demo site](http://hartwig-at.github.io/fm-timepicker/demo.html)

A simple time picker for **AngularJS** based on **Bootstrap** and **Moment**.

![](http://i.imgur.com/CvrVZXX.png) 

##Setting Dropdown List Classes
You can set the classes of the list and list items with the following parameters to the directive.

###list-class
Set the CSS class that is used on the ```<ul>``` element wrapping the dropdown list. The default here is "dropdown-menu form-control" to keep it bootstrap friendly and generally speaking you should keep these. If you want to add your own class in addition to the defaults to something like this:

```
<fm-timepicker ... list-class="dropdown-menu form-control my-list-class">
```

If you want to completely override the class on the list and get rid of the default styling, do something like this.

```
<fm-timepicker ng-model=... list-class="my-list-class"></fm-timepicker>
```

###list-item-class
To set the CSS class of each item in a list, pass in a list-item-class attribute to your time picker. There is no default for this value.

```
<fm-timepicker ng-model=... list-item-class="my-list-item-class"></fm-timepicker>
```

###list-style
The default list ```<ul>``` has an inline style that is provided to make things display correctly. It is:

```
height:auto; max-height:160px; overflow-y:scroll;
```
If you need to modify/change this for any reason, you can do so by specifying the list-style attribute. Note that if you change it the default is dropped so you either need to add it to your list-style or put the default setting in a CSS class, set your list-class, and set list-style equal to an empty string (which from a CSS perspective is preferred).

##Some implementation notes
The way the directive currently is implemented all of the time/interval related attributes MUST point to scope variables and cannot be the value you want to use. For example, don't try this:

```
<fm-timepicker ng-model=...
	time-start="08:00"
	time-end="12:00"
	interval="60"
></fm-timepicker>
```
Things won't work out very well for you because the type conversion doesn't happen automagically. Instead set those values on your scope and then reference them from your element tag. You will be much happier with the results.

```
var timeFormat = "HH:mm";
$scope.timeData = {
	start: moment('08:00', timeFormat),
	end: moment('12:00', timeFormat),
	interval: moment.duration(60, 'minutes')
};
```
```
<fm-timepicker ng-model=...
	time-start="timeData.start"
	time-end="timeData.end"
	interval="timeData.interval"
></fm-timepicker
```

Non time related attributes such as ```btn-class```, ```list-style```, ```list-class```, and ```list-item-class``` can have their values direction in the tag like their examples above.

