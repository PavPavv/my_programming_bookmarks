# AngularJS

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

When you need to dynamically set the value of attributes in an HTML element, the target property is wrapped in square brackets. This binds the attribute with the desired dynamic data by informing Angular that the declared value should be interpreted as a JavaScript-like statement (with some Angular enhancements) instead of a plain string.

```typescript
<button [disabled]="hasPendingChanges"></button>
```

Angular executes template expressions after every change detection cycle. Many asynchronous activities trigger change detection cycles, such as promise resolutions, HTTP results, timer events, key presses, and mouse moves.

## Unidirectional data flow

A data flow model where the component tree is always checked for changes in one direction from parent to child, which prevents cycles in the change detection graph.

In practice, this means that data in Angular flows downward during change detection. A parent component can easily change values in its child components because the parent is checked first. A failure could occur, however, if a child component tries to change a value in its parent during change detection (inverting the expected data flow), because the parent component has already been rendered. In development mode, Angular throws the **ExpressionChangedAfterItHasBeenCheckedError** error if your application attempts to do this, rather than silently failing to render the new value.

To avoid this error, a lifecycle hook method that seeks to make such a change should trigger a new change detection run. The new run follows the same direction as before, but succeeds in picking up the new value.

## Event Handling

You can bind event listeners by specifying the event name in parenthesis and invoking a method on the right-hand-side of the equals sign:

```typescript
<button (click)="saveChanges()">Save Changes</button>
```

If you need to pass the event object to your event listener, Angular provides an implicit $event variable that can be used inside the function call:

```typescript
<button (click)="saveChanges($event)">Save Changes</button>
```

## Styles

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

## Directives

### Conditional rendering (\*ngIf)

```html
<section class="admin-controls" *ngIf="hasAdminPrivileges">
  The content you are looking for is here.
</section>
```

### Rendering a list (\*ngFor)

```html
<ul class="ingredient-list">
  <li *ngFor="let task of taskList">{{ task }}</li>
</ul>
```

### Custom directives

Custom Angular directives can be identified by the directive suffix (e.g., _my-custom-name.directive.ts_).

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

Directives can also leverage user events, take input for additional customization...

## Services

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

## Organization

### Conceptual preview of Angular components

Angular apps are built around components, which are Angular's building blocks. Components contain the code, HTML layout, and CSS style information that provide the function and appearance of an element in the app. In Angular, components can contain other components. An app's functions and appearance can be divided and partitioned into components.

In Angular, components have metadata that define its properties. When you create your HomeComponent, you use these properties:

- **selector**: to describe how Angular refers to the component in templates.
- **standalone**: to describe whether the component requires a NgModule.
- **imports**: to describe the component's dependencies.
- **template**: to describe the component's HTML markup and layout.
- **styleUrls**: to list the URLs of the CSS files that the component uses in an array.

## Angular CLI

```bash
npm i -g @angular/cli
ng new my-new-app
ng serve --open

ng generate component my-component
```

## From Angular books

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 17.1.1.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The application will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.

## From Angular book

### Input()

```typescript
@Input('exercise-set') exerciseSet!:ExerciseSet; or @Input() exerciseList!: ExerciseSetList;
```

trackBy:

Separating responsibilities – Smart/Container and Presentation (Smart and Dump) components

The EventEmitter class uses TypeScript’s type-checking capability, making it possible for us to
determine what type of object we are going to emit to the parent component.

@Output attribute must be done with parentheses –
( ) – and this $event parameter represents the object that the child component will emit.

### Dependency injection

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
inject() must be called from an injection context
such as a constructor, a factory function, a field initializer,
or a function used with `runInInjectionContext`.

The singleton pattern is a design pattern of the creational type and
allows the creation of objects whose access will be global in the system.

----------------------------------------------------------------------------

### Services in Angular

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

----------------------------------------------------------------------------

### Modules in Angular + lazy loading + 404 page

ngModel is an object managed by the FormModule module that represents the form’s data model.

The use of square brackets and parentheses [(someGood)]="doOrGetSomeGood" signals to Angular that we are performing a two-way data
binding on the property.

we need to add the ReactiveFormsModule module responsible
for all the functionality that Angular makes available to us for this type of form

For Angular to recognize the form validation function, it must return a new function with the
signature described in the ValidatorFn interface. This signature defines that it will receive
AbstractControl and must return an object of type ValidationErrors that allows the
template to interpret the new type of validation.

```typescript
private formBuilder = inject(NonNullableFormBuilder);

. . .
import { ErrorPageComponent } from './error-page/error-page.
component';
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

----------------------------------------------------------------------------
  
### Guards in Angular

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

the canActivateChild attribute to call the route’s guard, so we don’t need to repeat
all the routes in this module.

----------------------------------------------------------------------------

### Resolvers in Angular

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

----------------------------------------------------------------------------

### Interceptor Pattern

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

#### Changing the request route

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

#### Global loader

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

#### Angular toasts

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
// providers: [
// . . .
//    {
//      provide: HTTP_INTERCEPTORS,
//      useClass: NotificationInterceptor,
//      multi: true,
//    },
// . . .
// ]
```

#### Measuring the performance of a request

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
// . . .
// providers: [
// . . .
//    {
//      provide: HTTP_INTERCEPTORS,
//      useClass: TelemetryInterceptor,
//      multi: true,
//    },
// ],
// . . .
```

```typescript
getInitialList(): Observable<ExerciseSetListAPI> {
  const headers = new HttpHeaders().set('X-TELEMETRY', 'true');
  return this.httpClient.get<ExerciseSetListAPI>(this.url, { headers});
}
```

### RxJS

The RxJS library that makes up the Angular ecosystem aims to make controlling asynchronous flows simpler using declarative and reactive programming.

- Observables and operators
- Handling data – transformation operators
- Another way to subscribe – the async pipe
- Connecting information flows – high-order operators
- Optimizing data consumption – filter operators

#### Observables and operators

With **observable** data structure, we can capture a series of events in time and declaratively make our application react to these events. Regarding the use of promises for HTTP requests, we can use them, but tasks that are verbose and complex to perform when using promises can be done using observables and RxJS instead.

The **pipe()** method also returns an observable, and when the component calls the subscribe method, its result will go through all the operators and deliver the result.

#### Another way to subscribe – the async pipe

One detail that you may have noticed is the $ symbol here. Using this postfix for variables and attributes that are observables is a community convention. It is not an obligation, but you will often see this symbol in code bases that use RxJS.

```angular
*ngFor="let suggestion of exercises$ | async"
```

Another advantage that the async pipe provides is that the framework controls the life cycle of the observable; that is, when the component is destroyed, Angular automatically triggers the unsubscribe method.

#### Connecting information flows – high-order operators

```typescript
public exercises$ = this.entryForm.valueChanges.pipe(
  switchMap((model) => this.exerciseService.getExercises(model?.exercise))
);
```

The **switchMap** operator is a higher-order observable because it takes an observable as input and returns an observable as output. This is in contrast to the **map** operator, which takes an observable as input and returns a value as output.

#### Optimizing data consumption – filter operators

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

