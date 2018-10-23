# Overview
A project of angular developing template

## Directives:
- There are three kinds of directives in Angular:
  - Components —directives with a template.
  - Structural directives—change the DOM layout by adding and removing DOM elements.
  - Attribute directives—change the appearance or behavior of an element, component, or another directive.

## Decorator:
- Expression that evaluates to a function allowing annotation of classes at design time.

## Component:
```
@Component()
@ -> Decorator indicator
Component -> Decorator name
() -> Argument goes here
```

- @NgModule() >> import { NgModule } from '@angular/core';
- BrowserModule >> import { BrowserModule } from '@angular/platform-browser';
- @Component() >> import { Component } from '@angular/core';
- @Input() >> import { Input } from '@angular/core';
- @Output() >> import { Output } from '@angular/core';
- @Directive() >> import { Directive } from '@angular/core';
- @HostBinding() >> import { HostBinding } from '@angular/core';
- @HostListener() >> import { HostListener } from '@angular/core';
- @Pipe() >> import { Pipe } from '@angular/core';
- FormsModule >> import { FormsModule } from '@angular/forms';
- ReactiveFormsModule >> import { ReactiveFormsModule } from '@angular/forms';
- FormGroup >> import { FormGroup } from '@angular/forms';
- FormControl >> import { FormControl } from '@angular/forms';
- Validators >> import { Validators } from '@angular/forms';
- FormBuilder >> import { FormBuilder } from '@angular/forms';
- @Inject() >> import { Inject } from '@angular/core';
- @Injectable() >> import { Injectable } from '@angular/core';
- InjectionToken  >> import { InjectionToken } from '@angular/core';
- HttpClientModule >> import { HttpClientModule } from '@angular/common/http';
- HttpClient  import { HttpClient } from '@angular/common/http';
- HttpXhrBackend >> import { HttpXhrBackend } from '@angular/common/http';
- `` << ES2015 syntax backticks
- ${} << ES2015 string interpolation
- RouterModule >> import { RouterModule } from '@angular/router';
- Routes >> import { Routes } from '@angular/router';
- Router >> import { Router } from '@angular/router';

- Bootstrapping Angular: For Browser Plateform >>  import { plateformBrowserDynamic } from '@angular/platform-browser-dynamic';
  Note: other plateforms are also be supported by 3rd party bootstrapping functions or classes.

### Angular Template Syntax:
  1. Interpolation: is the way get data display in the view. `{{}}` << pair of curly brackets
	    - Nonsupported in {{}}
          - Assignments
	      - Newing up variables
	      - Chaining expressions
	      - Incrementing/decrementing
  2. Binding: 
     	- Property binding by [DOM-Element-Property] = "expression"
        - Event binding by (native DOM Events or own custom events) = "expression"
        ** If you have a one-way binding to ngModel with [] syntax, changing the value of 
           the domain model in the component class will set the value in the view. If you 
           have a two-way binding with [()] syntax (also known as 'banana-box syntax'), the 
           value in the UI will always be synced back to the domain model in your class as well.
  3. Expressions
  4. Conditional templating
  5. Template variable
  6. Template expression operators

### Input decorator
  - @Input() >> import { Input } from '@angular/core';
  - Design to use class property

### Output decorator
  - @Output() >> import { Output} from '@angular/core';
  - Design to use class property
  - To use, set the property by angular EventEmitter object
    - import { EventEmitter } from '@angular/core';

## Directive:
### Angular has two types of Directive
  - Structural
  - Attribute

### Structural: 
  - change the DOM by adding or removing layout. Evaluate * template syntax.
### Structural Directives are: 
  - *ngIf="statement" or <ng-template [ngIf]="statement">--innerHtml DOM--</ng-template>
  - *ngFor="let variableName of listSourceName << (this is micro syntax statement)"
  - The Angular NgSwitch is actually a set of cooperating directives: NgSwitch, NgSwitchCase, and NgSwitchDefault.
    - More to visit: https://angular.io/guide/structural-directives#inside-ngswitch-directives

### Attribute Directive: changes the appearance or behavior of a DOM element.
  - [ngClass]="conditional statement"

### Custom Own Attribute Directive:
  * Hosting value setup: @HostBinding decorator: 
    - import { Directive, HostBinding } from '@angular/core';
    - passing object literal to directive metadata: selector: '[mwFavorite]'
    - @HostBinding('class.is-favorite') isFavorite = true;
    - property binding: [mwFavorite]="mediaItem.isFavorite"
    - set the value in custom directive class by @Input() decorator with setter method: @Input() set mwFavorite(value)
      and name of setter method is same as property element name.
  * Hosting event Listener setup: @HostListener decorator:
    - import { Directive, HostBinding, HostListener } from '@angular/core';
    - @HostBinding('class.is-favorite-hovering') hovering = false;
    - @HostListener('mouseenter') onMouseEnter() { this.hovering = true; }
    - @HostListener('mouseleave') onmouseleave() { this.hovering = false; }

## Pipes:
 - A template expression operator that takes in a value and returns a new value representation.
 - Pipe also take parameters and seperated by ':'.
 - import { DatePipe } from '@angular/common';
 - {{ value | date: 'shortDate' }}
 - multiple parameters: {{ value | slice: 0: 10 }}
 - pipe also be chain: {{ value | slice: 0: 10 | uppercase }}

 * Custom own pipe:
   - @Pipe() >> import { Pipe } from '@angular/core';
   - import { Pipe, PipeTransform } from '@angular/core';
   - pipe is by nature stateless.
   - implement PipeTransform interface and transform() method.

## Forms: 
 - Built-In validators
 - Custom Validators
 - Async Validators
 - Form Object Representation
 * two types of approach support in angular form
   - Template Driven
   - Model Driven (reactive)

### Template Driven Forms:
  - import { FormsModule } from '@angular/forms' to app.module.ts;
  - ngForm directive
  - ngModel directive
  - ngSubmit directive
    - (ngSubmit)="onSubmit(mediaItemForm.value)"
  - '#' template reference variable to get the form control element data object
    - #mediaItemForm="ngForm"

### Model Driven Forms:
  - import { ReactiveFormsModule} from '@angular/forms' to app.module.ts;
  - Form field contract
  - Field validation rules
  - Change tracking
  - Can be unit tested
  - import { FormGroup } from '@angular/forms'; >> to create form group objects.
  - import { FormControl } from '@angular/forms'; >> to create form group controls object property literal.
  - directive property binding: [formGroup]="form"
  - ngSubmit directive
    - (ngSubmit)="onSubmit(form.value)"
  - formControlName directive set the matched name property of form group object's form control object.
  - **FormBuilder is the latest class approach. (need to read)
  - FormArray object

### Validation: we can apply validator to form control objects in form group and even to the form group object.
  - Support two validations: 
    - built in validation
    - custom validation

  - built in validation:
    - import { Validators } from '@angular/forms';
    - set the validation rules as regx inside formControl object's 2nd parameter
    - to prevent the invalid submission, bind the submit button 
      native disable property as : [disable]="!form.valid"
    - Validators.compose([]) << set multiple validation rules in a FormControl
    - **FormBuilder class validation rules apply is different syntax. (need to read)

  - Custom validation:
    - custom validation function is apply to formcontrol as a 2nd parameter with function parentheses'()'

### Errors Handling (old approach):
  - angular will an add errors property to the form control, 
    form group and form array objects when they are invalid.

## Dependency Injection and Services:
 - DI does work in 2 step
   - service registration
   - retrival those services which can be done with constructor() {} injection
     - by leveraging TypeScript type annotations,
     - or by using the angular Inject decorator: @Inject()
