# AngularJS

**Table of content:**

1. Start
    1. Generate project template
    2. Generating
    3. Starting a Development Web Server
    4. Checking Your Coding Style
    5. Running Unit Tests
    6. Building Your Projects
    7. Root module
2. Styles
    1.Basics
3. Component
    1. Basics
    2. More about standalone components
    3. Conceptual preview of Angular components
    4. Input()
    5. Dependency injection
    6. Component's lifecycle methods
    7. Component's core services
    8. @ViewChild() decorator
4. Data
    1. One-way binding
    2. Event one-way binding
    3. Two-way binding
    4. Data flow direction
5. Event
    1. Basics
    2. Mouse bindings
6. Directives
    1. The Basic Built-in Angular Directives
    2. Custom directives
7. Forms
    1. Importing the Forms Module
    2. Form validation
8. Services
    1. Basics
9. Routing
    1. Root routing
    2. Module(submodule, nested, child) routing
10. Modules in Angular, lazy loading and 404 page
    1. Basics
11. Guards
    1. Basics
12. Resolvers
    1. Basics
13. Interceptor pattern
    1. Basics
    2. Changing the request route
    3. Global loader
    4. Angular toasts
    5. Measuring the performance of a request
14. RxJS
    1. Basics
    2. Observables and operators
    3. Another way to subscribe – the async pipe
    4. Connecting information flows – high-order operators
    5. Optimizing data consumption – filter operators
    6. Signals
15. Tests
    1. Basics
    2. Unit testing with Jest
    3. E2E tests with Cypress
16. PWA
    1. Basics
17. Micro frontend
    1. Basics
    2. Angular elements
18. Deploy
    1. Basics
    2. Mounting a Docker image with Nginx
19. Upgrading Angular
    1. Basics

## 1. Start project

### 1.1 Generate project template

```bash
ng new <options...>
```

- _--dry-run_ (Boolean) (Default: false) – Run through without making any changes.
- _--skip-install_ (Boolean) (Default: false) – Skip installing packages.
- _--skip-git_ (Boolean) (Default: false) – Skip initializing a git repository.
- _--standalone_ (Boolean) (Default: false) – Creates an application based upon the standalone API, without NgModules.
- _--style_ (String) (Default: css) – The style file default extension. Your choices are css, scss, sass, or less.
- _--prefix_ (String) (Default: app) – The prefix to use for all component selectors.
- _--routing_ (Boolean) (Default: false) – Generate a routing module.

### 1.2 Generating

```bash
ng generate <blueprint> <options...>
```

- _appShell_
- _application_
- _class_
- _component_
- _directive_
- _enum_
- _guard_
- _interceptor_
- _interface_library_
- _module_
- _pipe_
- _service_
- _serviceWorker_
- _webWorker_

- _--flat_ (Boolean): Flag to indicate if a directory is created. By default, ng CLI will create a separate folder for most blueprints, even if there is only one file. If know you won’t be creating multiple files (templates, tests, etc.), you can pass true to this flag, and the CLI won’t create the separate folder.

- _--spec_ (Boolean): Specifies if a spec file is generated. Pass false to this flag to prevent the CLI from generating test files for you. Use this with caution. There are very few reasons not to have unit tests for your code.

- _--app_ (String): Specifies app name to use.

- _--standalone_ (Boolean): Specifies whether a component or directive should be created without an existing NgModule.

- _--module_ (String): Allows specification of the declaring module. By default, the item being generated will be attached to the “closest containing module.” The CLI will walk up the folder tree, looking for a module. Specifying a different module here will override that behavior.

Example:

```bash
npm i -g @angular/cli
ng new my-new-app
ng serve --open

ng generate component my-component
```

Or

```bash
ng g c my-component --skip-tests --dry-run
ng g c my-component --skip-tests
```

_--dry-run_ flag ask **ng g** command to show what and where will be created.

### 1.3 Starting a Development Web Server

```bash
ng serve <options...>
```

- _--host_ (String): Allows you to change the host being served.
- _--port_ (Number): Allows you to override the port served.
- _--open_ Causes the CLI to open your default browser automatically.

### 1.4 Checking Your Coding Style

```bash
ng lint <options...>
```

- _--fix=true_ Recommended you only run this option on a pristine git repository, making it easy to undo if it breaks something.

### 1.5Running Unit Tests

```bash
ng test <options...>
```

### 1.6 Building Your Projects

```bash
ng build <options...>
```

The Angular development tools automatically add script elements to this HTML, which instruct the browser to request the JavaScript files that provide the Angular framework and the custom features defined in the project.

Run end-to-end (integration) tests in existing project:

```bash
ng e2e <options...>
```

### 1.7 Root module

The term module does double duty in an Angular application and refers to both a JavaScript module and an Angular module. JavaScript modules are used to track dependencies in the application and ensure that the browser receives only the code it requires. Angular modules are used to configure a part of the Angular application.
Every application has a root Angular module, which is responsible for describing the application to Angular. For applications created with the ng new command, the root module is called AppModule, and it is defined in the app.module.ts file in the src/app folder.

When the application starts, Angular processes the index.html file, locates the element that matches the root component’s selector property, and replaces it with the contents of the files specified by the root component’s templateUrl and styleUrls properties. This is done using the Domain Object Model (DOM)
API provided by the browser for JavaScript applications.

## 2.Styles

### 2.1 Basics

By default, a component's style will only apply to elements in that component's template in order to limit the side effects.

While Angular's default style encapsulation prevents component styles from affecting other components, global styles affect all components on the page. This includes &**::ng-deep**, which promotes a component style to a global style.

Every component is associated within an element that matches the component's selector. This element, into which the template is rendered, is called the host element. The **:host** pseudo-class selector may be used to create styles that target the host element itself, as opposed to targeting elements inside the host.

```typescript
@Component({
  selector: 'app-root',
  template: `
    <h1>Tour of Heroes</h1>
    <app-hero-main [hero]="hero"></app-hero-main>
  `,
  styleUrls: ['./hero-app.component.css'],
})
export class HeroAppComponent {
  /* . . . */
}
```

## 3.Component

### 3.1 Basics

An Angular component can be identified by the component suffix (e.g., _my-custom-name.component.ts_) and has the following:

- A decorator to define configuration options for things like:
  - A selector that defines what the tag name is when referring a component in a template
  - An HTML template that controls what is rendered to the browser
- A TypeScript class that defines the behavior of the component. Examples include handling user input, managing state, defining methods, etc.

When defining data that you want the component to manage, this can be accomplished by declaring it by defining **class fields**.

You can define functions for a component by declaring methods within the component class.

```typescript
// todo-list-item.component.ts
@Component({
  standalone: true,
  selector: 'todo-list-item',
  template: ` <p>Title: {{ taskTitle }}</p> `,
  styles: ['li { color: papayawhip; }'],
  imports: [],
})
export class TodoListItem {
  /* Component behavior is defined in here */
  taskTitle = 'Read cup of coffee';
  isComplete = false;

  updateTitle(newTitle: string) {
    this.taskTitle = newTitle;
  }

  completeTask() {
    this.isComplete = true;
  }
}
```

Angular executes template expressions after every change detection cycle. Many asynchronous activities trigger change detection cycles, such as promise resolutions, HTTP results, timer events, key presses, and mouse moves.

Starting with Angular 15.2, the @Component decorator now includes an imports array. This array isn’t related to TypeScript’s import statement. Instead, it’s specific to Angular and is used to provide the compilation context for standalone components. It includes all other components, directives, pipes, and NgModules that are used in the
template of the standalone component.

### 3.2 More about standalone components

Standalone components represents SCAM pattern (Single Component Angular Module). [More about it.](https://angular-training-guide.rangle.io/modules/module-scam-pattern)

- [Tree-shaking in SkyEng](https://habr.com/ru/companies/skyeng/articles/757498/)

### 3.3 Conceptual preview of Angular components

Angular apps are built around components, which are Angular's building blocks. Components contain the code, HTML layout, and CSS style information that provide the function and appearance of an element in the app. In Angular, components can contain other components. An app's functions and appearance can be divided and partitioned into components.

In Angular, components have metadata that define its properties. When you create your HomeComponent, you use these properties:

- **selector**: to describe how Angular refers to the component in templates.
- **standalone**: to describe whether the component requires a NgModule.
- **imports**: to describe the component's dependencies.
- **template**: to describe the component's HTML markup and layout.
- **styleUrls**: to list the URLs of the CSS files that the component uses in an array.

starting with Angular 15.2, the **@Component** decorator now includes an imports array. This array isn’t related to TypeScript’s import statement. Instead, it’s specific to Angular and is used
to provide the compilation context for **standalone components**. It includes all other components, directives, pipes, and NgModules that are used in the template of the standalone component.

### 3.4 Input()

```typescript
@Input('exercise-set') exerciseSet!:ExerciseSet; or @Input() exerciseList!: ExerciseSetList;
```

trackBy:

Separating responsibilities – Smart/Container and Presentation (Smart and Dump) components

The EventEmitter class uses TypeScript’s type-checking capability, making it possible for us to
determine what type of object we are going to emit to the parent component.

@Output attribute must be done with parentheses –
( ) – and this $event parameter represents the object that the child component will emit.

### 3.5 Dependency injection

Angular has a dependency injection mechanism. This feature allows us to compose a class just by declaring the object we need in its constructor (args).

```typescript
export class DiaryComponent {
  constructor(private exerciseSetsService: ExerciseSetsService) {}
  exerciseList = this.exerciseSetsService.getInitialList();
. . .
}
```

```typescript
inject()
import { Component, inject } from '@angular/core';
export class DiaryComponent {
  private exerciseSetsService = inject(ExerciseSetsService);
  exerciseList = this.exerciseSetsService.getInitialList();
. . .
}
```

prefer composition over inheritance!
inject() must be called from an injection context such as a constructor, a factory function, a field initializer, or a function used with `runInInjectionContext`.

The singleton pattern is a design pattern of the creational type and allows the creation of objects whose access will be global in the system.

### 3.6 Component's lifecycle methods

1. **constructor** -> The constructor is called when the component is created. This happens before any Angular-specific initialization methods occurs.
2. **ngOnChanges** -> Runs after an input/output binding has been changed.
3. **ngOnInit** ->  Runs after a component has been initialized. Input bindings are ready.
4. **ngDoCheck** -> Allows developers to perform custom actions during change detection.
5. **ngAfterContentInit** -> Runs after the content of a component has been initialized. You would typically use ngAfterContentInit when you need to perform some initialization logic based on the content that has been projected into the component using ```<ng-content>```. This is useful for components that accept content from their parent components.
6. **ngAfterContentChecked** -> Runs after every check of a component's content.
7. **ngAfterViewInit** ->  Runs after the view of a component has been initialized.  This lifecycle hook is called after Angular has fully initialized a component's view and its child views. It is invoked once after the first ngDoCheck for the component.
8. **ngAfterViewChecked** -> Runs after every check of a component's view.
9. **ngOnDestroy** -> Runs before a component is destroyed.

### 3.7 Component's core services

#### ChangeDetectorRef

ChangeDetectorRef is a service that is part of the @angular/core package. It is used to control the change detection mechanism of Angular applications. Change detection is the process by which Angular checks for changes in component data and updates the view accordingly.

Purpose: ChangeDetectorRef allows you to manually trigger change detection or control how it operates in your components. This can be particularly useful in scenarios where Angular's default change detection strategy does not behave as expected, such as when working with third-party libraries, asynchronous operations, or when optimizing performance.

- **detectChanges()**: This method can be called to run change detection for the component and its children immediately. It is useful when you know that the data has changed, but Angular hasn't detected it.

- **markForCheck()**: Marks the component and its ancestors as needing to be checked for changes. This is useful when using the OnPush change detection strategy.

- **detach()**: Detaches the change detector from the change detection tree, meaning that Angular will not check this component for changes unless it is explicitly reattached.

- **reattach()**: Reattaches a previously detached change detector, allowing Angular to check for changes again.

#### Change Detection Strategies

Angular uses two change detection strategies: _Default_ and _OnPush_.
The default strategy checks the component and all its children whenever any event occurs.
**On Push** strategy only checks the component when its input properties change, an event occurs within the component, or a manual trigger occurs (like calling **markForCheck()**).

```typescript
import { Component, ChangeDetectorRef } from '@angular/core';

@Component({
  selector: 'app-example',
  template: <div>{{data}}</div>
             <button (click)="updateData()">Update Data</button>
})
export class ExampleComponent {
  data: string = 'Initial Data';

  constructor(private cdr: ChangeDetectorRef) {}

  updateData() {
    this.data = 'Updated Data';
    // Manually trigger change detection
    this.cdr.detectChanges();
  }
}
```

### 3.8 @ViewChild() decorator

In Angular, @ViewChild is a decorator that allows you to access a child component, directive, or DOM element from a parent component's class. It provides a way to interact with the child component's properties and methods directly.

1. Accessing Child Components: You can use @ViewChild to get a reference to a child component and call its public methods or access its properties.

2. Manipulating DOM Elements: If you need to directly manipulate a DOM element (e.g., focusing an input field), @ViewChild can be used to get a reference to that element.

3. Interacting with Directives: You can also use @ViewChild to access custom directives applied to elements in your template.

```typescript
import { Component, ViewChild } from '@angular/core';

// parent.component.html:
// <child-component #childComp></child-component>
// <input #inputField type="text">

@Component({
    selector: 'app-parent',
    templateUrl: './parent.component.html'
  })
  export class ParentComponent {
    @ViewChild('childComp') childComponent!: ChildComponent; // Reference to the child component
    @ViewChild('inputField') inputField!: ElementRef; // Reference to the input field

    ngAfterViewInit() {
      // Accessing properties or methods of the child component
      this.childComponent.someMethod();

      // Manipulating the input field
      this.inputField.nativeElement.focus();
    }
  }
```

Lifecycle Hooks: You typically access the @ViewChild properties after the view has been initialized, which is why you often see it used in the ngAfterViewInit() lifecycle hook.

Static Option: As of Angular 8, you can specify whether you want to resolve the query results before or after change detection runs by passing an options object as the second argument to @ViewChild. For example:

```typescript
@ViewChild('childComp', { static: false }) childComponent!: ChildComponent;
```

----------------------------------------------------------------------------

## 4.Data binding

In Angular, data binding is a core concept that allows you to synchronize data between the model (component) and the view (template). There are two main types of data binding: one-way binding and two-way binding.

Data bindings can be applied to any HTML element in a template, and an element can have multiple bindings, each of which can manage a different aspect of the element’s appearance or behavior.

### 4.1 One-way binding

One-way binding means that data flows in one direction only, either from the component to the view or from the view to the component.

1.From Component to View:

- This is often done using interpolation ({{ }}), property binding ([property]), and event binding ((event)).

This is an Angular “one-way” binding expression.

```typescript
{{ taskTitle }}. 
```

```tsx
<
  *ngFor="let name of names"
  [name]="name"
/>
```

2.From View to Component:

- This is generally achieved through event binding.

```tsx
<input (input)="onInputChange($event)" />
```

When you need to dynamically set the value of attributes in an HTML element, the target property is wrapped in square brackets. This binds the attribute with the desired dynamic data by informing Angular that the declared value should be interpreted as a JavaScript-like statement (with some Angular enhancements) instead of a plain string.

```typescript
<button [disabled]="hasPendingChanges"></button>
```

If the binding target doesn’t correspond to a directive, then Angular checks to see whether the target can be used to create a property binding. There are five different types of property binding:

- [property]
- [attr.name]
- [class.name]
- [style.name]

The square brackets (the [ and ] characters) tell Angular that this is a one-way data binding that has an expression that should be evaluated. Angular will still process the binding if you omit the brackets and the target is a directive, but the expression won’t be evaluated, and the content between the quote characters will be passed to the directive as a literal value.

The Angular Brackets:

1. [target]="expr" - The square brackets indicate a one-way data binding where data flows from the expression to the target. The different forms of this type of binding are the topic of this chapter.
2. {{expression}} - This is the string interpolation binding.
3. (target) ="expr" - The round brackets indicate a one-way binding where the data flows from the target to the destination specified by the expression. This is the binding used to handle events.
4. [(target)] ="expr" - This combination of brackets—known as the banana-in-a-box—indicates a two-way binding, where data flows in both directions between the target and the destination specified by the expression.

One-way data bindings must be idempotent, meaning that they can be evaluated repeatedly without changing the state of the application.

The expression context means you can’t access objects defined outside of the template’s component, and in particular, templates can’t access the global namespace.
If you want to access functionality in the global namespace, then it must be provided by the component, acting on behalf of the template.

### 4.2 Event one-way binding

Reference variables are defined using the # character, followed by the variable name.
Angular won’t update the data bindings in the template when the user edits the contents of the input
element unless there is an event binding on that element. Setting the binding to false gives Angular
something to evaluate just so the update process will begin and distribute the current contents of the input element throughout the template.

```html
<input #product class="form-control" (input)="false" />

<td (mouseover)="product.value = item.name ?? ''">{{i + 1}}</td>
```

### 4.3 Two-way binding

Two-way binding allows data to flow in both directions: from the component to the view and from the view back to the component. This is particularly useful for form inputs where you want to keep the component's state in sync with user input.

```html
<input
  class="form-control
  (input)="selectedProduct=$any($event).target.value"
  [value]="selectedProduct ?? ''"
/>
```

#### Using the ngModel Directive

```html
<input [(ngModel)]="username" />
<input class="form-control" [(ngModel)]="selectedProduct" />
```

The target for the binding is the ngModel directive, which is included in Angular to simplify creating two-way data bindings on form elements, such as the input elements used in the example.
The ngModel directive knows the combination of events and properties that the standard HTML
elements define. Behind the scenes, an event binding is applied to the input event, and a property binding is applied to the value property.
You must remember to use both brackets and parentheses with the ngModel binding. If you use
just parentheses—(ngModel)—then you are setting an event binding for an event called ngModel, which
doesn’t exist. The result is an element that won’t be updated or won’t update the rest of the application. You can use the ngModel directive with just square brackets—[ngModel]—and Angular will set the initial value of the element but won’t listen for events, which means that changes made by the user won’t be automatically reflected in the application model.

### 4.4 Data flow direction

A data flow model where the component tree is always checked for changes in one direction from parent to child, which prevents cycles in the change detection graph.

In practice, this means that data in Angular flows downward during change detection. A parent component can easily change values in its child components because the parent is checked first. A failure could occur, however, if a child component tries to change a value in its parent during change detection (inverting the expected data flow), because the parent component has already been rendered. In development mode, Angular throws the **ExpressionChangedAfterItHasBeenCheckedError** error if your application attempts to do this, rather than silently failing to render the new value.

To avoid this error, a lifecycle hook method that seeks to make such a change should trigger a new change detection run. The new run follows the same direction as before, but succeeds in picking up the new value.

## 5.Event Handling

### 5.1 Basics

You can bind event listeners by specifying the event name in parenthesis and invoking a method on the right-hand-side of the equals sign:

```typescript
<button (click)="saveChanges()">Save Changes</button>
```

If you need to pass the event object to your event listener, Angular provides an implicit $event variable that can be used inside the function call:

```typescript
<button (click)="saveChanges($event)">Save Changes</button>
```

### 5.2 Mouse bindings

```html
<td (mouseover)="selectedProduct=item.name">{{i + 1}}</td>
```

The event binding can also be used to introduce data from the event itself, using details that are provided by the browser - **$event**.

```html
<input class="form-control" (input)="selectedProduct=$any($event).target.value" />
```

When the browser triggers an event, it provides an Event object that describes it. There are different types of event objects for different categories of events (mouse events, keyboard events, form events, and so on), but all events share the three properties:

- **type** (This property returns a string that identifies the type of event that has been triggered.)
- **target** (This property returns the object that triggered the event, which will generally be the object that represents the HTML element in the DOM.)
- **timeStamp** (This property returns a number that contains the time that the event was triggered,
expressed as milliseconds since January 1, 1970.)

Unfortunately, Angular assumes that the $event variable is always assigned an **Event object**, which defines the features common to all events. The Event.target property returns an InputTarget object, which defines just the methods required to set up event handlers and doesn’t provide access to element-specific features.
Angular templates do support the special $any function, which disables type checking by treating a
value as the special any type:

```html
<input class="form-control" (input)="selectedProduct=$any($event).target.value" />
```

```typescript
handleInputEvent(ev: Event) {
  if (ev.target instanceof HTMLInputElement) {
    this.selectedProduct = ev.target.value
  }
}
```

By passing $event to the $any function, I can read the target.value property without causing a compiler error.

> Behind the scenes, Angular uses the Reactive Extensions package to distribute events. The **EventEmitter<T>** interface extends the RxJS **Subject<T>** interface, which, in turn, extends the **Observable<T>** interface.

Bindings on the host element are defined using two decorators, @HostBinding and @HostListener, both
of which are defined in the @angular/core module.

The **@HostBinding** decorator is used to set up a property binding on the host element and is applied to a directive property. The listing sets up a binding between the class property on the host element and the decorator’s bgClass property.

```typescript
@HostBinding("class")

The @HostListener decorator is used to set up an event binding on the host element and is applied to
a method.

@HostListener("click")
  triggerCustomEvent() {
    if (this.product != null) {
      this.click.emit(this.product.category);
    }
  }
```

## 6.Directives

### 6.1 The Basic Built-in Angular Directives

- *ngClass
- *ngStyle
- *ngIf
- *ngFor
- *ngSwitch
- *ngSwitchCase
- *ngSwitchDefault
- *ngTemplateOutlet

The asterisk before the name of directive is required because the directive is using a micro-template.

#### *ngFor

```html
<tr *ngFor="let item of getProducts(); let i = index; let c = count; let d = odd; let e = even; let f = first; let g = last; trackBy:getKey">
```

```typescript
getKey(index: number, product: Product) {
  return product.id;
}
```

*ngTemplate + *ngFor:

```html
<table class="table table-sm table-bordered text-dark">
    <tr><th></th><th>Name</th><th>Category</th><th>Price</th></tr>
     <ng-template ngFor let-item [ngForOf]="getProducts()"
             let-i="index"  let-c="count" let-odd="odd">
         <tr class="text-white" [class.bg-primary]="odd" [class.bg-info]="!odd">
            <td>{{ i + 1 }} of {{ c }}</td>
            <td>{{item.name}}</td>
            <td>{{item.category}}</td>
            <td>{{item.price}}</td>
         </tr>
     </ng-template>
</table>
```

When there is a change to the data model, the ngFor directive evaluates its expression and updates the elements that represent its data objects. The update process can be expensive, especially if the data source is replaced with one that contains different objects representing the same data.

#### *ngTemplateOutlet and *ngTemplateOutletContext

The **ngTemplateOutlet** directive is used to repeat a block of content at a specified location, which can be useful when you need to generate the same content in different places and want to avoid duplication.

```html
<ng-template #titleTemplate let-title="title">
    <h4 class="p-2 bg-success text-white">Repeated Content</h4>
</ng-template>

<ng-template [ngTemplateOutlet]="titleTemplate"></ng-template>
  
<div class="bg-info p-2 m-2 text-white">
  There are {{getProductCount()}} products.
</div>

<ng-template [ngTemplateOutlet]="titleTemplate"></ng-template>
```

The **ngTemplateOutlet** directive can be used to provide the repeated content with a context object that can be used in data bindings defined within the element.
To receive the context data, the **ng-template** element that contains the repeated content defines a _let-attribute_ that specifies the name of a variable, similar to the expanded syntax used for the **ngFor** directive. The value of the expression assigns the _let-variable_ a value.

```html
<ng-template #titleTemplate let-title="title">
    <h4 class="p-2 bg-success text-white">{{ text }}</h4>
</ng-template>

<ng-template [ngTemplateOutlet]="titleTemplate" [ngTemplateOutletContext]="{title: 'Header'}"></ng-template>
  
<div class="bg-info p-2 m-2 text-white">
  There are {{getProductCount()}} products.
</div>

<ng-template [ngTemplateOutlet]="titleTemplate" [ngTemplateOutletContext]="{title: 'Footer'}"></ng-template>
```

#### *ng-container

The ng-container element doesn’t appear in the HTML displayed by the browser, which means that it can be used to generate content within elements.

#### *ngIf

```html
<section class="admin-controls" *ngIf="hasAdminPrivileges">
  The content you are looking for is here.
</section>
```

### 6.2 Custom directives

Directives are classes to which the @Directive decorator has been applied. The decorator requires
the selector property, which is used to specify how the directive is applied to elements, expressed using a standard CSS style selector.
Custom Angular directives can be identified by the directive suffix (e.g., _my-custom-name.directive.ts_).

> The prefix Ng/ng is reserved for use for built-in Angular features and should not be used.

The directive constructor defines a single ElementRef parameter, which Angular provides when it creates a new instance of the directive and which represents the host element. The ElementRef class defines a single property, nativeElement, which returns the object used by the browser to represent the element in the Document Object Model(DOM). This object provides access to the methods and properties that manipulate the element and its contents, including the classList property.

```typescript
@Directive({
  selector: '[appHighlight]',
})
export class HighlightDirective {
  private el = inject(ElementRef);
  constructor() {
    this.el.nativeElement.style.backgroundColor = 'yellow';
  }
}
```

```html
<p appHighlight>Look at me!</p>
```

Directives can also leverage user events, take input for additional customization.

```typescript
import { Directive, ElementRef, Attribute } from "@angular/core";

@Directive({
    selector: "[pa-attr]",
})
export class PaAttrDirective {
    constructor(element: ElementRef, @Attribute("pa-attr-class") bgClass: string) {
        element.nativeElement.classList.add(bgClass || "table-success", "fw-bold");
    }
}
```

```html
<td pa-attr pa-attr-class="table-warning">{{item.category}}</td>
```

```typescript
import { Directive, ElementRef, Attribute } from "@angular/core";

@Directive({
    selector: "[pa-attr]",
})
export class PaAttrDirective {
    constructor(element: ElementRef, @Attribute("pa-attr-class") bgClass: string) {
        element.nativeElement.classList.add(bgClass || "table-success", "fw-bold");
    }
}
```

```html
<td pa-attr pa-attr-class="table-warning">{{item.category}}</td>
```

Directives can support two-way bindings, which means they can be used with the banana-in-a-box bracket style that ngModel uses and can bind to a model property in both directions.

```typescript
import {
    Input, Output, EventEmitter, Directive,
    HostBinding, HostListener, SimpleChange
} from "@angular/core";

@Directive({
    selector: "input[paModel]"
})
export class PaModel {
    @Input("paModel")
    modelProperty: string | undefined = "";

    @HostBinding("value")
    fieldValue: string = "";

    ngOnChanges(changes: { [property: string]: SimpleChange }) {
        let change = changes["modelProperty"];
        if (change.currentValue != this.fieldValue) {
            this.fieldValue = changes["modelProperty"].currentValue || "";
        }
    }

    @Output("paModelChange")
    update = new EventEmitter<string>();

    @HostListener("input", ["$event.target.value"])
    updateValue(newValue: string) {
        this.fieldValue = newValue;
        this.update.emit(newValue);
    }
}
```

```html
    <div class="form-group bg-info text-white p-2">
        <label>Name:</label>
        <input class="bg-primary text-white form-control"
            [paModel]="newProduct.name"
            (paModelChange)="newProduct.name = $event" />
    </div>
```

## 7.Forms

### 7.1 Importing the Forms Module

Declaring a Dependency in the app.module.ts File in the src/app Folder:

```typescript
import { FormsModule } from "@angular/forms";

@NgModule({
  declarations: [ProductComponent],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [ProductComponent]
})
export class AppModule { }
```

When using a form element, the convention is to use an event binding for a special event called
ngSubmit like this:

```html
<form (ngSubmit)="addProduct(newProduct)">
```

In Angular forms there are three pairs of validation classes:

- ng-untouched/ng-touched
- ng-pristine/ng-dirty
- ng-valid/ng-invalid
- ng-pending

Display error messages:

```html
<ul class="text-danger list-unstyled mt-1"
    *ngIf="name.dirty && name.invalid">
    <li *ngIf="name.errors?.['required']">
       You must enter a product name
     </li>
     <li *ngIf="name.errors?.['pattern']">
        Product names can only contain letters and spaces
     </li>
     <li *ngIf="name.errors?.['minlength']">
       Product names must be at least
       {{ name.errors?.['minlength'].requiredLength }} characters
     </li>
</ul>
```

### 7.2 Form validation

```typescript
import { Component } from "@angular/core";
import { Model } from "./repository.model";
import { Product } from "./product.model";
import { NgModel, ValidationErrors, NgForm } from "@angular/forms";

@Component({
    selector: "app",
    templateUrl: "template.html"
})
export class ProductComponent {
    model: Model = new Model();
    // ...other methods omitted for brevity...
    formSubmitted: boolean = false;
    submitForm(form: NgForm) {
        this.formSubmitted = true;
        if (form.valid) {
            this.addProduct(this.newProduct);
            this.newProduct = new Product();
            form.resetForm();
            this.formSubmitted = false;
        }
    }
}
```

```html
<div class="p-2">
    <form ngForm="productForm" #form="ngForm" (ngSubmit)="submitForm(form)">
        <div class="bg-danger text-white p-2 mb-2"
                *ngIf="formSubmitted && form.invalid">
             There are problems with the form
        </div>
        <div class="form-group">
            <label>Name</label>
            <input class="form-control"
                name="name"
                [(ngModel)]="newProduct.name"
                #name="ngModel"
                required
                minlength="5"
                pattern="^[A-Za-z ]+$" />
            <ul class="text-danger list-unstyled mt-1"
                    *ngIf="(formSubmitted || name.dirty) && name.invalid">
                <li *ngFor="let error of getValidationMessages(name)">
                    {{error}}
                </li>
            </ul>
        </div>
        <button
          class="btn btn-primary mt-2"
          type="submit"
          [disabled]="formSubmitted && form.invalid"
          [class.btn-secondary]="formSubmitted && form.invalid"
        >
            Create
        </button>
    </form>
</div>
```

## 8.Services

### 8.1 Basics

When you need to share logic between components, Angular allows you to create a “service” which allows you to inject code into components while managing it from a single source of truth.

Angular services can be identified by the service suffix (e.g., _my-custom-name.service.ts_).

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
class CalculatorService {
  add(x: number, y: number) {
    return x + y;
  }
}
```

```typescript
import { Component } from '@angular/core';
import { CalculatorService } from './calculator.service';

@Component({
  selector: 'app-receipt',
  template: `<h1>The total is {{ totalCost }}</h1>`,
})
export class Receipt {
  private calculatorService = inject(CalculatorService);
  totalCost = this.calculatorService.add(50, 25);
}
```

When we create a service, it has an @Injectable decorator, as in our example:

```typescript
@Injectable({
  providedIn: 'root',
})
export class ExerciseSetsService {
```

The provideIn metadata determines the scope of the service. The value 'root' means that the
instance of the service will be unique for every application; that’s why, by default, Angular services
are singleton.

The onInit method is called after building the component, but before rendering the component.

## 9.Routing

### 9.1 Root routing

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

import { NotFoundPageComponent } from './pages/not-found-page/not-found-page.component';
import { MainPageComponent } from './pages/main-page/main-page.component';
import { LoginPageComponent } from './pages/login-page/login-page.component';
import { AdminPageComponent } from './pages/admin-page/admin-page.component';
import { authGuard } from './common/guards';

export const routes: Routes = [
  {
    path: '',
    component: MainPageComponent,
  },
  {
    path: 'login',
    component: LoginPageComponent,
  },
  {
    path: 'admin',
    component: AdminPageComponent,
    canActivate: [authGuard],
  },
  {
    path: '**',
    pathMatch: 'full',
    component: NotFoundPageComponent,
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes, { useHash: true })],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### 9.2 Module(submodule, nested, child) routing

The RouterModule.forChild method is used to define the routing configuration for the feature module,
which is then included in the module’s imports property.

```typescript
let routing = RouterModule.forChild([
    { path: "auth", component: AuthComponent },
    { path: "main", component: AdminComponent },
    { path: "**", redirectTo: "auth" }
]);
```

## 10.Modules in Angular + lazy loading + 404 page

### 10.1 Basics

ngModel is an object managed by the FormModule module that represents the form’s data model.

The use of square brackets and parentheses [(someGood)]="doOrGetSomeGood" signals to Angular that we are performing a two-way data
binding on the property.

we need to add the ReactiveFormsModule module responsible
for all the functionality that Angular makes available to us for this type of form

For Angular to recognize the form validation function, it must return a new function with the
signature described in the ValidatorFn interface. This signature defines that it will receive
AbstractControl and must return an object of type ValidationErrors that allows the
template to interpret the new type of validation.

A dynamically loaded module must be self-contained and include all the information that Angular requires, including the routing URLs that are supported and the components they display. If any other part of the application depends on the module, then it will be included in the JavaScript bundle with the rest of
the application code, which means that all users will have to download code and resources for features they won’t use.
However, a dynamically loaded module is allowed to declare dependencies on the main part of the application. This module relies on the functionality in the data model module, which has been added to the module’s imports so that components can access the model classes and the repositories.

```typescript
private formBuilder = inject(NonNullableFormBuilder);

. . .
import { ErrorPageComponent } from './error-page/error-page.component';

const routes: Routes = [
  { path: '', pathMatch: 'full', redirectTo: 'home' },
  {
    path: 'home',
    loadChildren: () =>
      import('./home/home.module').then((file) => file.HomeModule),
  },
  { path: 'error', component: ErrorPageComponent },
  { path: '**', redirectTo: '/error' },
];
. . .

  ngOnInit(): void {
    this.entryId = this.route.snapshot.paramMap.get('id');
    if (this.entryId) {
      this.exerciseSetsService
        .getItem(this.entryId)
        .subscribe((entry) => this.updateForm(entry));
    }
  }
```
  
## 11.Guards in Angular

### 11.1 Basics

Angular offers several built-in guard types like **CanActivate**, **CanDeactivate**, **CanLoad**, and **Resolve**, each serving a specific purpose in the navigation life cycle.

- User access control: Guards can be used to control which users have access to certain routes based on their roles or permissions.
- Data protection: They can protect data on a page from being lost when the user navigates away.
- Load optimization: They can prevent lazy-loaded modules from loading until certain conditions are met.
- Data pre-fetching: Guards can fetch the data required for a specific route in advance using Resolve guards. We’ll look more at the resolver later.

```bash
ng g guard login/auth
```

```typescript
 export const authGuard: CanActivateFn = (route, state) => {
  const authService = inject(AuthService);
  const router = inject(Router);
  if (authService.isLogged) {
    return true;
  } else {
    return router.parseUrl('/login');
  }
};
```

the **canActivateChild** attribute to call the route’s guard, so we don’t need to repeat all the routes in this module.

```typescript
export dateGuard: CanActivateFn = (route, state) => {
  dateParam = route.params['date'];
  const date = new Date(dateParam);
    if (!isNaN(date.getTime()) && date > new Date()) {
      return true;
    } else {
      alert('Invalid or past date!');
      return false;
    }
  }
```

```typescript
import { dateGuard } from "./date.guard";
const routes: Routes = [
  {
    path: "event/:date",
    component: EventComponent,
    canActivate: [dateGuard],
  },
];
```

## 12.Resolvers in Angular

### 12.1 Basics

We are using the resolve property, much like configuring a route guide, with the difference that
we associate an object with the function, which will be important for the component to consume the
data generated by it.

```bash
ng g resolver diary/diary
```

```typescript
export const diaryResolver: ResolveFn<ExerciseSetListAPI> = (route,
state) => {
  const exerciseSetsService = inject(ExerciseSetsService);
  return exerciseSetsService.getInitialList();
};
```

```typescript
{
  path: '',
  component: DiaryComponent,
  title: 'Diary',
  resolve: { diaryApi: diaryResolver },
},
```

```typescript
// 
private route = inject(ActivatedRoute);

// 
  ngOnInit(): void {
    this.route.data.subscribe(({ diaryApi }) => {
      this.exerciseList = diaryApi.items;
    });
  }

```

The component is now consuming the data attribute of the route. It returns an observable that has
an object with the diaryApi attribute – the same one we configured in the routes module.
When we run our project again, we see that the behavior of the screen does not change externally;
however, internally, we are fetching information from the gym diary before the component is loaded.

## 13.Interceptor pattern

### 13.1 Basics

```bash
ng g interceptor login/auth
```

```typescript
@Injectable()
export class AuthInterceptor implements HttpInterceptor {
  private authService = inject(AuthService);

  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
    const token = this.authService.token;

    if (request.url.includes('auth')) {
      return next.handle(request);
    }
    if (token) {
      const reqAuth = request.clone({
        headers: request.headers.set(`Authorization`, `Bearer ${token}`),
      });
      return next.handle(reqAuth);
    }
    return next.handle(request);
  }
}
```

```typescript
@NgModule({
  declarations: [AppComponent, ErrorPageComponent],
  imports: [BrowserModule, AppRoutingModule, HttpClientModule],
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi:
true },
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

### 13.2 Changing the request route

```bash
ng g interceptor shared/host
```

```typescript
@Injectable()
export class HostInterceptor implements HttpInterceptor {
  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
    const url = 'http://localhost:3000';
    const resource = request.url;
    if (request.url.includes('http')) {
      return next.handle(request);
    }
    const urlsReq = request.clone({
      url: `${url}/${resource}`,
    });
    return next.handle(urlsReq);
  }
}
```

For this interceptor to be triggered by Angular, we need to add it to the providers array of the AppModule module:

```typescript
@NgModule({
  declarations: [AppComponent, ErrorPageComponent],
  imports: [BrowserModule, AppRoutingModule, HttpClientModule],
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi:
true },
    { provide: HTTP_INTERCEPTORS, useClass: HostInterceptor, multi:
true },
  ],
  bootstrap: [AppComponent],
})
export class AppModule {}
```

### 13.3 Global loader

```bash
ng generate component loading-overlay
ng generate service loading-overlay/load
ng generate interceptor loading-overlay/load
```

We will implement the LoadService service, which will maintain and control the loading state:

```typescript
@Injectable({
  providedIn: 'root',
})
export class LoadService {
  #showLoader = false;
  showLoader() {
    this.#showLoader = true;
  }
  hideLoader() {
    this.#showLoader = false;
  }
  get isLoading() {
    return this.#showLoader;
  }
}
```

```typescript
@Injectable()
export class LoadInterceptor implements HttpInterceptor {
  private loadService = inject(LoadService);
  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
    if (request.headers.get('X-LOADING') === 'false') {
      return next.handle(request);
    }
    this.loadService.showLoader();
    return next
      .handle(request)
      .pipe(finalize(() => this.loadService.hideLoader()));
  }
}
```

```typescript
@NgModule({
  declarations: [AppComponent, ErrorPageComponent,
LoadingOverlayComponent],
  imports: [BrowserModule, AppRoutingModule, HttpClientModule],
  providers: [
    { provide: HTTP_INTERCEPTORS, useClass: AuthInterceptor, multi:
true },
    { provide: HTTP_INTERCEPTORS, useClass: HostInterceptor, multi:
true },
    { provide: HTTP_INTERCEPTORS, useClass: LoadInterceptor, multi:
true },
  ],
  bootstrap: [AppComponent],
})
export class AppModule {
```

### 13.4 Angular toasts

```bash
npm install ngx-

ng interceptor notification/notification
```

```typescript
import { ToastrService } from 'ngx-toastr';
@Injectable()
export class NotificationInterceptor implements HttpInterceptor {
  private toaster = inject(ToastrService);
  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
    return next.handle(request).pipe(
      tap((event: HttpEvent<any>) => {
        if (event instanceof HttpResponse && event.status === 201) {
          this.toaster.success('Item Created!');
        }
      })
    );
  }
}
```

```typescript
providers: [
. . .
   {
     provide: HTTP_INTERCEPTORS,
     useClass: NotificationInterceptor,
     multi: true,
   },
. . .
]
```

### 13.5 Measuring the performance of a request

```bash
ng g interceptor telemetry/telemetry
```

```typescript
@Injectable()
export class TelemetryInterceptor implements HttpInterceptor {
  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
      if (request.headers.get('X-TELEMETRY') !== 'true') {
      return next.handle(request);
    }
    const started = Date.now();
    return next.handle(request).pipe(
      finalize(() => {
        const elapsed = Date.now() - started;
        const message = `${request.method} "${request.urlWithParams}" in ${elapsed} ms.`;
        console.log(message);
      })
    );
  
```

```typescript
. . .
providers: [
. . .
   {
     provide: HTTP_INTERCEPTORS,
     useClass: TelemetryInterceptor,
     multi: true,
   },
],
. . .
```

```typescript
getInitialList(): Observable<ExerciseSetListAPI> {
  const headers = new HttpHeaders().set('X-TELEMETRY', 'true');
  return this.httpClient.get<ExerciseSetListAPI>(this.url, { headers});
}
```

## 14.RxJS

### 14.1 Basics

The RxJS library that makes up the Angular ecosystem aims to make controlling asynchronous flows simpler using declarative and reactive programming.

- Observables and operators
- Handling data – transformation operators
- Another way to subscribe – the async pipe
- Connecting information flows – high-order operators
- Optimizing data consumption – filter operators

### 14.2 Observables and operators

With **observable** data structure, we can capture a series of events in time and declaratively make our application react to these events. Regarding the use of promises for HTTP requests, we can use them, but tasks that are verbose and complex to perform when using promises can be done using observables and RxJS instead.

The **pipe()** method also returns an observable, and when the component calls the subscribe method, its result will go through all the operators and deliver the result.

### 14.3 Another way to subscribe – the async pipe

One detail that you may have noticed is the $ symbol here. Using this postfix for variables and attributes that are observables is a community convention. It is not an obligation, but you will often see this symbol in code bases that use RxJS.

```angular
*ngFor="let suggestion of exercises$ | async"
```

Another advantage that the async pipe provides is that the framework controls the life cycle of the observable; that is, when the component is destroyed, Angular automatically triggers the unsubscribe method.

### 14.4 Connecting information flows – high-order operators

```typescript
public exercises$ = this.entryForm.valueChanges.pipe(
  switchMap((model) => this.exerciseService.getExercises(model?.exercise))
);
```

The **switchMap** operator is a higher-order observable because it takes an observable as input and returns an observable as output. This is in contrast to the **map** operator, which takes an observable as input and returns a value as output.

### 14.5 Optimizing data consumption – filter operators

```typescript
const DEBOUNCE_TIME = 300;

public exercises$ = this.entryForm.valueChanges.pipe(
  debounceTime(DEBOUNCE_TIME),
  map((model) => model?.exercise ?? ''),
  filter((exercise) => exercise.length >= 3),
  distinctUntilChanged(),
  switchMap((exercise) => this.exerciseService.getExercises(exercise))
);
```

The distinctUntilChanged operator checks whether the stream’s data, has changed from one iteration to another and triggers the next operator only if the value is different, saving even more unnecessary calls to the backend.

### 14.6 Signals

```typescript
let a = signal<number>(2);
let b = signal<number>(3);
let sum = computed(() => a() + b());
console.log(sum());
a.set(9);
console.log(sum());
b.update((oldValue) => oldValue * 2);
console.log(sum());
```

The computed type is, in our analogy of a spreadsheet, a cell that contains a formula where you can read the values of other cells to determine its value.

```typescript
export class LoadService {
  isLoading = signal<Boolean>(false);
  showLoader() {
    this.isLoading.set(true);
  }
  hideLoader() {
    this.isLoading.set(false);
  }
}
```

```tsx
@if (loadService.isLoading()) {
  <app-loading-overlay />
}
<router-outlet></router-outlet>
```

```typescript
export class ExerciseSetsService {
// . . .
  exerciseList = signal<ExerciseSetList>([] as ExerciseSetList);
  getInitialList() {
    const headers = new HttpHeaders().set('X-TELEMETRY', 'true');
    this.httpClient
      .get<ExerciseSetListAPI>(this.url, { headers })
      .pipe(map((api) => api?.items))
      .subscribe((list) => this.exerciseList.set(list));
  }
  deleteItem(id: string) {
    this.httpClient.delete<boolean>(`${this.url}/${id}`).subscribe(()
=> {
    this.exerciseList.update((list) =>
      list.filter((exerciseSet) => exerciseSet.id !== id)
    );
    });
  }
// . . .
}
```

```typescript
export class ListEntriesComponent {
  @Output() editEvent = new EventEmitter<ExerciseSet>();
  @Output() deleteEvent = new EventEmitter<string>();
  private exerciseSetsService = inject(ExerciseSetsService);
  exerciseList = this.exerciseSetsService.exerciseList;
}
```

```tsx
<section class="mb-8">
  <h2 class="mb-4 text-xl font-bold">List of entries</h2>
  <ul class="rounded border shadow">
  @for (item of exerciseList(); track item.id) {
    <li>
      <app-entry-item
        [exercise-set]="item"
        (deleteEvent)="deleteEvent.emit($event)"
        (editEvent)="editEvent.emit($event)"
      />
    </li>
    } @empty {
      <div>
        No Items!
      </div>
    }
  </ul>
</section>
```

## 15.Tests

### 15.1 Basics

```typescript
describe('AppComponent', () => {
  beforeEach(async () => {
    await TestBed.configureTestingModule({
     declarations: [AppComponent],
     imports: [RouterTestingModule],
   }).compileComponents();
  });
  it('should create the app', () => {
    const fixture = TestBed.createComponent(AppComponent);
    const app = fixture.componentInstance;
    expect(app).toBeTruthy();
  });
});
```

```typescript
beforeEach(() => {
  TestBed.configureTestingModule({
    declarations: [LoginComponent],
    imports: [ReactiveFormsModule],
    providers: [
      AuthService,
      {
        provide: AuthService,
        useValue: jasmine.createSpyObj('AuthService', ['login']),
      },
    ],
  });
  fixture = TestBed.createComponent(LoginComponent);
  component = fixture.componentInstance;
  fixture.detectChanges();
});
```

### 15.2 Unit testing with Jest

Angular component unit tests not only examine logic but also assess the values that will be presented on the screen.

```typescript
describe('DiaryComponent', () => {
//   . . .
  let exerciseSetsService: ExerciseSetsService;
  beforeEach(async () => {
  await TestBed.configureTestingModule({
//    . . .
  }).compileComponents();
//    . . .
    exerciseSetsService = TestBed.inject(ExerciseSetsService);
  });
  it('should call delete method when the button delete is clicked',
fakeAsync(() => {
    exerciseSetsService.deleteItem = jasmine.createSpy().and.
returnValue(of());
    component.deleteItem('1');
    tick();
    expect(exerciseSetsService.deleteItem).
toHaveBeenCalledOnceWith('1');
  }));
});
```

```typescript
import { Location } from '@angular/common';
describe('DiaryComponent', () => {
  let location: Location;
  beforeEach(async () => {
    await TestBed.configureTestingModule({
// . . .
      imports: [
        RouterTestingModule.withRoutes([
          {
            path: 'home/diary/entry/:id',
            component: NewEntryFormReactiveComponent, },
        ]),
      ]
     }).compileComponents();
    location = TestBed.inject(Location);
  });
  it('should direct to diary entry edit route', fakeAsync(() => {
    const set: ExerciseSet = { date: new Date(), exercise: 'test',
reps: 6, sets: 6, id: '1' };
    component.editEntry(set);
    tick();
    expect(location.path()).toBe('/home/diary/entry/1');
  }));
});
```

If a test is failing, one of the first things to check should be whether the test is failing when it's the only test that runs. To run only one test with Jest, temporarily change that test command to a test.only:

```javascript
test.only('this will be the only test that runs', () => {
  expect(true).toBe(false);
});
```

### 15.3 E2E tests with Cypress

```bash
ng add @cypress/schematic
```

```bash
ng e2e
```

```typescript
describe('Login Page:', () => {
  it('should login to the diary with the correct credentials.', () =>
{
    cy.visit('/');
    cy.get('#username').type('mario');
    cy.get('#password').type('1234');
    cy.get('[data-cy="submit"]').click();
    cy.contains('Workout diary');
  });
});
```

```typescript
describe('New Entry Form:', () => {
  beforeEach(() => {
    cy.visit('/');
    cy.get('#username').type('mario');
    cy.get('#password').type('1234');
    cy.get('[data-cy="submit"]').click();
  });
  it('Should register a new entry in the workout diary', () => {
    cy.get('[data-cy="new-entry-menu"]').click();
    cy.contains('Date');
    cy.get('#date').type('2023-08-08');
    cy.get('#exercise').type('Front Squat');
    cy.get('#sets').type('4');
    cy.get('#reps').type('6');
    cy.get('[data-cy="submit"]').click();
    cy.contains('Item Created!');
  });
});
```

----------------------------------------------------------------------------

## 16.PWA

### 16.1 Basics

```bash
ng add @angular/pwa
```

The _@angular/pwa_ package configures the application so that HTML, JavaScript, and CSS files are cached, which will allow the application to be started even when there is no network available.

In an Angular application, especially when using the Angular Service Worker (SW) for Progressive Web Apps (PWAs), the ngsw-config.json file plays a crucial role in configuring the behavior of the service worker. This file is used by the Angular CLI to create a service worker configuration, allowing developers to define caching strategies, data paths, and other service worker-related settings.

Caching Strategy: It defines how different assets (like application shell files, images, API responses, etc.) should be cached and served. You can specify different strategies (e.g., "cache-first," "network-first," etc.) for different types of resources.

Asset Management: You can specify which files or assets should be included in the caching strategy. This includes the files that need to be pre-cached when the service worker is installed.

Data Groups: For dynamic content (like API calls), you can define data groups that describe how the data should be fetched, cached, and refreshed, which is essential for ensuring that users get the latest data while still benefiting from offline capabilities.

Versioning: It can help manage cache invalidation by allowing you to specify a version for your service worker. When you update the version, previously cached files are invalidated, prompting the service worker to fetch and cache the latest resources.

Basic example:

```json
{
  "index": "/index.html",
  "assetGroups": [
    {
      "name": "app",
      "installMode": "prefetch",
      "resources": {
        "files": [
          "/favicon.ico",
          "/index.html",
          "/assets/**",
          "/styles.css",
          "/main.js"
        ]
      }
    },
    {
      "name": "icons",
      "installMode": "lazy",
      "resources": {
        "files": [
          "/assets/icons/**"
        ]
      }
    }
  ],
  "dataGroups": [
    {
      "name": "api",
      "urls": [
        "https://api.example.com/**"
      ],
      "cacheConfig": {
        "maxSize": 100,
        "maxAge": "1h",
        "timeout": "10s",
        "version": 1
      }
    }
  ]
}
```

```typescript
import { Injectable } from "@angular/core";
import { Observable, Subject } from "rxjs";

@Injectable()
export class ConnectionService {
    private connEvents: Subject<boolean>;

    constructor() {
        this.connEvents = new Subject<boolean>();
        window.addEventListener("online",
            (e) => this.handleConnectionChange(e));
        window.addEventListener("offline",
            (e) => this.handleConnectionChange(e));
    }

    private handleConnectionChange(event: any) {
        this.connEvents.next(this.connected);
    }

    get connected() : boolean {
        return window.navigator.onLine;
    }

    get changes(): Observable<boolean> {
        return this.connEvents;
    }
}
```

```typescript
@Component({
    templateUrl: "cartDetail.component.html"
})
export class CartDetailComponent {
    public connected: boolean = true;
    constructor(public cart: Cart, private connection: ConnectionService) {
        this.connected = this.connection.connected;
        connection.Changes.subscribe((state) => this.connected = state);
    }
}
```

```html
<div class="row">
  <div class="col">
  <div class="text-center">
    <button class="btn btn-primary m-1" routerLink="/store">
        Continue Shopping
    </button>
    <button class="btn btn-secondary m-1" routerLink="/checkout"
            [disabled]="cart.lines.length == 0 || !connected">
      {{  connected ?  'Checkout' : 'Offline' }}
    </button>
  </div>
</div>
```

> When you add progressive features to an application, you must deploy it so that it can be accessed over secure HTTP connections. If you do not, the progressive features will not work because the underlying technology—called service workers—won’t be allowed by the browser over regular HTTP connections. You can test progressive features using localhost, as I demonstrate shortly, but an SSL(Secure Sockets Layer)/TLS(Transport Layer Security) certificate is required when you deploy the application.

## 17.Micro frontend

### 17.1 Basics

There are several ways to share micro frontends, from the simplest (and obsolete), with the use of iframes, to more modern, but complex, solutions such as module federation.

Web Components is a specification that aims to standardize components created by different frameworks into a model that can be consumed between them. In other words, by creating an Angular component
following this specification, an application created in React or Vue could consume this component. Although Web Components was not created with micro frontend projects in mind, we can see that its
definition fits perfectly for what we need.

```bash
ng add ngx-build-plus
npm i http-server
```

```json
"scripts": {
  "ng": "ng",
  "start": "ng serve",
  "build": "ng build --single-bundle --bundle-styles --keep-
styles --output-hashing=none",
  "serve-mfe": "http-server dist/gym_exercises",
}
```

The serve-mfe script uses the http-server service to publish the contents of the dist folder that will contain the compiled micro frontend.

```bash
npm run build
npm run serve-mfe
```

Let’s prepare main application to consume the micro frontend. To do this, let’s start by creating a new module in the application.

```bash
ng g m some-name --routing
ng g c some-name/some-name
```

With the preceding commands, we create the module with the generated route file and a component that will be responsible for loading mfe.
We now have the task of including the micro frontend generated in the other project in our interface. For this, we have a community package
called @angular-extensions that allows us to load our micro frontend simply using a directive.

```bash
npm i @angular-extensions/elements
```

```typescript
import { CUSTOM_ELEMENTS_SCHEMA, NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { ExerciseRoutingModule } from './exercise-routing.module';
import { ExerciseComponent } from './exercise/exercise.component';
import { LazyElementsModule } from '@angular-extensions/elements';
@NgModule({
  declarations: [ExerciseComponent],
  imports: [CommonModule, LazyElementsModule, ExerciseRoutingModule],
  schemas: [CUSTOM_ELEMENTS_SCHEMA],
})
export class ExerciseModule {}
```

In this file, we are first adding the library module called LazyElementsModule to have access to the directive that we will use in the component. Furthermore, we have a new property in the metadata
called schemas. In it, we are informing Angular with the CUSTOM_ELEMENTS_SCHEMA token that this module will receive elements from outside the project. By default, Angular checks whether
the tag used in the template exists in the project or in the HTML standard, such as the input tag.

```typescript
import { Component } from '@angular/core';
@Component({
  selector: 'app-exercise',
  templateUrl: './exercise.component.html',
  styleUrls: ['./exercise.component.css'],
})
export class ExerciseComponent {
  elementUrl = 'http://localhost:8080/main.js';
}
```

Here, we are defining the address where the micro frontend’s main files will be served.

```html
<exercise-form *axLazyElement="elementUrl"> </exercise-form >
```

Here, we are declaring the new exercise-form element, and to load it, we use the **axLazyElement** directive assigning the micro frontend address.

To run our project, make sure the micro frontend is being served with the npm run serve-mfe command.

### 17.2 Angular elements

An Angular element component is a common component but transpiled to the Web Components standard, packaging not only our code but also the Angular rendering engine,
making it framework agnostic.

```bash
npm install @angular/elements --save
```

## 18.Deploy

### 18.1 Basics

The ng build command performs the production compilation process, and the bundles it produces are smaller and contain only the code that is required by the application.

```bash
ng build
```

```bash
ng generate environments
```

```typescript
export const environment = {
  production: false,
  apiUrl: 'http://localhost:4200'
};
```

```typescript
export const environment = {
  production: true,
  apiUrl: 'https://your-server/api',
};
```

```typescript
import { environment } from 'src/environments/environment';

@Injectable()
export class HostInterceptor implements HttpInterceptor {
  intercept(
    request: HttpRequest<unknown>,
    next: HttpHandler
  ): Observable<HttpEvent<unknown>> {
    const url = environment.apiUrl;
// . . .
}
```

To run our Angular project as a production build, we can use the following command:

```bash
ng serve --configuration production
```

The environmental needs of a frontend application running in production are different from the development environment.

```bash
ng build
```

In the configurations property, we have definitions of the types of environments that we can have in our project. Initially, the Angular CLI creates two configurations:
production and development.

In the production configuration, we have the budgets property, which determines the maximum size that our package must have in addition to defining the maximum size that a unitary component
must have. If your project exceeds this size, Angular may show a warning in the production console or even not build your project.

The outputHashing attribute ensures that the files generated by the application have their names added to a hash.
This is important because most public clouds and Content Delivery Networks (CDNs) cache the application based on the name of the files. When we generate a new version of our app, we want this cache to be invalidated to deliver the new version to our users.
Finally, the _defaultConfiguration_ property determines that if no parameter is passed, the **ng build** command will execute with the configuration indicated in it, in this case, production.

angular.json:

```json
"configurations": {
  "production": {
    "budgets": [
      {
        "type": "initial",
        "maximumWarning": "500kb",
        "maximumError": "1mb"
      },
      {
        "type": "anyComponentStyle",
        "maximumWarning": "2kb",
        "maximumError": "4kb"
      }
    ],
    "outputHashing": "all"
  },
  . . .
  "defaultConfiguration": "production"
```

When running the build in production configurations, Angular performs the following processes:

- Ahead-of-Time (AOT) compilation: Angular compiles templates and CSS files in addition to TypeScript files.
- Production mode: The application has some validations optimized for running in production.
- Bundling: It bundles all component files, templates, services and libraries in files separated by modules.
- Minification: From the files generated by TypeScript, it concatenates and eliminates whitespace and comments to generate the smallest files possible.
- Uglification: It rewrites generated code for variables, function names, and small, cryptic modules to make it difficult to reverse engineer the frontend code delivered to the user’s browser.
- Dead code elimination: Also known as tree shaking, this is the process of not including components in bundles that are not referenced in the code and do not need to be present in the production package.

### 18.2 Mounting a Docker image with Nginx

nginx.default.conf:

```nginx
server {
  listen 80;
  sendfile on;
  default_type application/octet-stream;
  gzip on;
  gzip_http_version 1.1;
  gzip_disable      "MSIE [1-6]\.";
  gzip_min_length   1100;
  gzip_vary         on;
  gzip_proxied      expired no-cache no-store private auth;
  gzip_types        text/plain text/css application/json application/
javascript application/x-javascript text/xml application/xml
application/xml+rss text/javascript;
  gzip_comp_level   9;
  root /usr/share/nginx/html;
  location / {
    try_files $uri $uri/ /index.html =404;
  }
}
```

In this configuration file, the first three properties (listen, sendfile, and default_type) aim to configure the exposed port and prepare the server to send our project’s package files.
The properties starting with gzip configure the delivery of files with the native web compression data gzip, further reducing the files delivered to our user’s browser.
The last part of the file determines the first page to be served. As we are in a Single-Page Application (SPA), the first file to be delivered is index.html.
With this configuration, we can run Nginx, but instead of installing it natively on our local machine, we will use Docker to run it.

Keep in mind that the image and the service that will be run from it (called a container in the Docker ecosystem) is as if it were a new machine and we will only copy what our application needs to run.

dockerfile:

```dockerfile
FROM node:18-alpine as build

COPY package.json package.lock.json ./

RUN npm ci && mkdir /my-app && mv ./node_modules ./my-app

WORKDIR /my-app

COPY . .

RUN npm run build

FROM nginx:1.25-alpine

COPY nginx.default.conf /etc/nginx/conf.d/default.conf

RUN rm -rf /user/share/nginx/html/*

COPY --from=build /my-app/dist/my-app /usr/share/nginx/html

CMD ["nginx", "-g", "deamon off;"]
```

In this file, we are using the multi-stage build technique to create our image. First, we build the application and then use the result of this build to create the final image. This way, our image becomes smaller and more optimized.
The first stage, which we call build here, is based on the _node:18-alpine_ image, which is a minimal image with the Alpine Linux distribution and version 18 of Node.js included.
Then, the _package.json_ and _package-lock.json_ files are copied and the npm ci command is run to install the package.
Then, with the **COPY . .** command, all project code is copied (except the _node_modules_ folder).
At the end of this stage, our application bundle is generated using the **npm run build** command.
The next stage, which will be production, is based on the _nginx:1.25-alpine_ image because to run a web server, we only need a Linux distribution such as Nginx installed.
The next task is to copy the configuration file for the Nginx installation, delete the example file that comes with the tool, and copy the files generated in the previous stage to this one.
The line ["nginx", "-g", "daemon off;"] runs Nginx and makes it ready to deliver our application.

To run the Docker container locally, use the following command:

```bash
sudo docker build -t my-image .
sudo docker run --name my-container -d -rm -p 8080:80 myapp
```

## 19.Upgrading

### 19.1 Basics

[Update Guide](https://angular.dev/update-guide)

1. ensure the project was on the latest current version of Angular (Angular CURRENT.x to CURRENT.y)

2. update with cli

```bash
ng update @angular/cli@17 @angular/core@17
```

2.1 If something went wrong it is safe to stable current npm install with (allowing the install process to continue even if there are incompatible versions):

```bash
npm install --legacy-peer-­deps
```

3. Then step by step (version by version) up to the desired latest stable version

```bash
ng update @angular/cli@18 @angular/core@18
```
