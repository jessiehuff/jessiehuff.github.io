---
layout: post
title:      "Another Day, Another Framework"
date:       2019-02-19 16:27:40 -0500
permalink:  another_day_another_framework
---

One of my favorite things in the world is trying new things, and I’ve recently been trying out Angular. Having a pretty solid understanding of React, it seems that there are a lot of similarities between the two frameworks. While I haven’t been learning Angular long, I thought I’d cover some basics I’ve learned so far. 

## Components and Modules

Components are the building blocks of an Angular application, just like in React. A **component** in Angular is a class that serves as a controller for the user interface. It consists of three parts – some TypeScript code, an HTML template, and CSS styles. 

A **module** is a collection of providers, services, directives, etc. and optionally config and run blocks which get applied to the application during the bootstrap process. Essentially, an Angular application uses modules to bundle different pieces/components into packages. 

Example of structure: 

![https://i.imgur.com/4e0e05Z.png](https://i.imgur.com/4e0e05Z.png)
 
 

## Databinding

**Binding**- a way to connect data from the TypeScript code to the HTML. 

![https://i.imgur.com/aF3bEXK.png?1](https://i.imgur.com/aF3bEXK.png?1)



We can** bind to attributes using square brackets [ ]**. 
 
For example, we might want to disable a button after it has been clicked.


```
@Component(...)

export class SomeComponent {
  
	clicked = false
}
<button [disabled]="clicked"></button>
```


We can also **bind to events using ( ) parenthesis**. Let’s setup a method to change the clicked property to false – this is basic event handling in Angular. 


```
@Component(...)
export class SomeComponent {
  clicked = false;

  handleClick() {
    this.clicked = true;
  }
}
<button [disabled]="clicked" (click)="handleClick()"></button>
```


**Interpolation**- can interpolate values from the TypeScript using handlebars syntax

```
@Component(...)
export class SomeComponent {
  appName = 'Cool App';
}
<h1>{{ appName }}</h1>
```



## Loading Components: 
1.	Declare the component in the HTML
`<app-cool></app-cool>`

2.	Load the component with the router. This tells Angular to imperatively load the component when you navigate to http://localhost:4200/cool. 
`const routes: Routes = [{ path: 'cool', component: CoolComponent }];`

3.	Load the component dynamically as an Entry Component. This is the most common for things like popups or modals, which usually get rendered after initialization, but don’t trigger a route change. A good example is the AlertController in the Ionic Framework. 
Convert it to a web component with Angular Elements. This allows us to export a component to be used outside of Angular altogether. 


## Directives

**Directives** allow you to extend HTML elements with custom attributes. They are instructions for the DOM. Angular comes with several built-in directives:
* *ngIf - Renders some HTML if condition is true.
* *ngFor - Repeats elements by looping over an array of data.
* ngClass - Applies CSS classes conditionally
* ngStyle - Applies styles conditionally


**Structural directives** start with a * and can determine which elements are rendered in the DOM. 
```
// Conditional 
<div *ngIf="clicked">Clicked!</div>

// Loop
<div *ngFor="let boat of boats">
  {{ boat.name }}
</div>

// This will loop through all elements in this array (boats) and assign the individual elements to the dynamic boat variable.

```


**Attribute directives-** don’t add or remove elements. They only change the element they were placed on. 
Other built-in directives can do things like apply conditional CSS classes. The left side contains a CSS class which will be applied when the right side evaluates to true. 


Examples:

`<p [ngStyle]="{'backgroundColor': (i+1 > 4) ? 'blue' : 'clear'}">Photos</p>`

```
<h3 [ngClass]="{
'green': boat.name === 'Starfire',
'red'  : boat.name === 'Oracle'  
}">
```

`<p [ngClass]= ”{online: serverStatus === ‘online’}”></p>`


You can also build your own. A **custom directive** in Angular is just a component minus the HTML/CSS. Instead of creating its own template, the directive becomes its own custom attribute that attaches to a host element. Let’s say we want a directive that magnifies an image when hovered. 

-	When should you use a directive over a component? When you don’t need to customize the HTML structure you probably want a directive


Ex: 

```
ng g directive magnifier  //generator CLI command to create a directive
import { Directive, HostBinding, HostListener } from '@angular/core';

@Directive({
  selector: '[magnifier]'
})
export class MagnifierDirective {
  // The image's width property
  @HostBinding('width') width = 200;

  // Fires when the user hovers
  @HostListener('mouseenter', ['$event'])
  onHover(e) {
    this.width = 300;
  }
}
```

Now you can apply it to any element in the HTML and it will increase width from 200px to 300.

`<img [src]="imgURL" magnifier>`


## Smart vs Dumb Components (Container vs Presentational) 

One of the most common component patters in Angular is the smart-dumb pattern - aka Container vs Presentational or Stateful vs Stateless. In a more general sense, it is just a separation of concerns to keep our code predictable. (Another similarity between Angular and React). 

Your smart components are concerned with how the code works while the dumb component deals with how it looks.


## Lifecycle Hooks 

By far the most common Lifecycle hook is ngOnInit which happens after the class is instantiated and the data-bound properties have been checked. You use this hook to perform any logic needed right away, like fetching data with HTTP calls, form setup, property definitions, and stuff like that.

```
constructor() {
  // first thing to happen, class instantiation
}

ngOnInit() {
  // second thing to happen, bindings are available
}

ngAfterViewInit() {
  // child views loaded
}

ngDoCheck() {
  // happens on each change detection check
}

ngOnDestroy() {
  // teardown
}
```


A lot of definitions and examples in this post come from Angular Firebase so check them out for more details! They have an awesome tutorial video explaining all of these concepts further: 
[https://angularfirebase.com/lessons/angular-components-basics-top-ten/ ](https://angularfirebase.com/lessons/angular-components-basics-top-ten/)


There is still so much to learn about Angular, and I'm currently working on a project now with it. I'll have to update you all with how that goes when I finish it! 



![https://i.imgur.com/HauM8Rk.png](https://i.imgur.com/HauM8Rk.png)


 

