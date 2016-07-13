# Behavioral Directives

## Overview

Now we've learnt event directives, we can move onto the equally, if not more, powerful behavioural directives.

## Objectives

- Describe behavioral Directives
- Use ng-repeat
- Use ng-model on an input
- Interpolate ng-model result in the View
- Conditionally add classes with ng-class

## What's a behavioral directive?

Behavioral directives are directives that allow us to manipulate the DOM. For example, we could have a repeating list of items or we could hide/show a DOM node depending on a variables value.

Behavioral directives are commonly just used as attributes, and quite a lot are provided by Angular itself.

Imagine we're not using Angular. If we wanted to loop through an array of objects and display them, we'd have to do something like this:


```js
var todos = [{
  title: 'Learn Angular',
  complete: false,
},{
  title: 'Create GitHub profile',
  complete: false
},{
  title: 'Brush teeth',
  complete: true
}];

var list = document.querySelector('ul.todos');

todos.forEach(function (todo) {
  var item = document.createElement('li');
  
  var wording = todo.complete ? 'Completed!' : 'Not completed :(';
  
  item.innerHTML = '<h4>' + todo.title + '</h4> ' + wording;
  
  list.appendChild(item);
});
```

This worked fine but what if our `todos` array was to get updated? We'd have to make sure to only insert the new items into our list, and only remove the correct elements when an item was removed from our array. This could get extremely messy and out of sync with our data if we were not really careful.

## Angular saves the day!

Try and contain your excitement when you see how this is done in Angular.

The HTML:

```html
<ul>
  <li ng-repeat="todo in vm.todos">
    <h4>{{ todo.title }}</h4>
    
    {{ todo.complete ? 'Completed!' : 'Not completed :(' }}
  </li>
</ul>
```

Our controller: 

```js
function TodosController() {
  this.todos = [{
     title: 'Learn Angular',
     complete: false,
   },{
     title: 'Create GitHub profile',
     complete: false
   },{
     title: 'Brush teeth',
     complete: true
   }];
}
```

That's everything that we need. Not even joking.

This handles everything - whenever our `todos` array is updated, Angular will update our view to match, removing and adding only the relevant nodes.

## ng-model

Along with `ng-repeat`, `ng-model` is one of the most commonly used directives provided by Angular. `ng-model` works it's magic by setting an input's value to a variable set in the controller, as well as updating said variable whenever the user updates the `<input />`'s value.

```html
<input ng-model="vm.username" />
```

This will populate our `<input />` with the value of `vm.username` (which could be empty), and then when the user types in the input, updates `vm.username` to match.

[Check out this JSFiddle](https://jsfiddle.net/pjrfbkku/) showing the power of `ng-model`.

## ng-class

Another task that's quite common in modern applications is dynamically adding and removing classes depending on different variables. For example, we might want to add a complete class on our example above if the todo is complete.

We can do this using the power of `ng-class`. `ng-class` takes an object, with the keys being the class you want to dynamically add, and the value being an expression - when the expression evaluates to `true`, the class is added. When it's `false`, the class will be removed.

For example:

```html
<div ng-class="{'classNameHere': true, 'otherClassName': false}">
</div>
```

In the example above, `classNameHere` would be added to our `<div />` (as the object's value is equal to true), whereas `otherClassName` wouldn't be added as the value is equal to false.

We can swap out `true` and `false` for different values, such as a variable's value. Let' do this for the todo items above.

```html
<ul>
  <li ng-repeat="todo in vm.todos" ng-class="{'complete': todo.complete}">
    <h4>{{ todo.title }}</h4>
    
    {{ todo.complete ? 'Completed!' : 'Not completed :(' }}
  </li>
</ul>
```

What is `ng-repeat="todo in vm.todos"` doing for us? We tell Angular what we want to loop over (`vm.todos`) and what variable to put each items properties in (`todo`). We could do `ng-repeat="item in vm.todos"` for example.

`{{ todo.complete ? 'Completed!' : 'Not completed :(' }}` looks a bit complicated too, but this is just similar to an expression that we would do in regular JavaScript. This checks the truthy value of `todo.complete`, and if `true` it will display "Completed!". If it's false, it will show "Not completed :(".

Notice that all we have added there is `ng-class="{'complete': todo.complete}"` - this checks our todo item and adds the `complete` class if `todo.complete` is equal to true. It is really that simple!

<p class='util--hide'>View <a href='https://learn.co/lessons/angular-behavioural-directives-readme'>Angular Behavioral Directives </a> on Learn.co and start learning to code for free.</p>
