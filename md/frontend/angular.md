# AngularJS

## Start project

### Generate project template

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

### Generating

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

### Starting a Development Web Server

```bash
ng serve <options...>
```

- _--host_ (String): Allows you to change the host being served.
- _--port_ (Number): Allows you to override the port served.
- _--open_ Causes the CLI to open your default browser automatically.

### Checking Your Coding Style

```bash
ng lint <options...>
```

- _--fix=true_ Recommended you only run this option on a pristine git repository, making it easy to undo if it breaks something.

### Running Unit Tests

```bash
ng test <options...>
```

### Building Your Projects

```bash
ng build <options...>
```

Run end-to-end (integration) tests in existing project:

```bash
ng e2e <options...>
```

## Component

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

Angular executes template expressions after every change detection cycle. Many asynchronous activities trigger change detection cycles, such as promise resolutions, HTTP results, timer events, key presses, and mouse moves.

### Conceptual preview of Angular components

Angular apps are built around components, which are Angular's building blocks. Components contain the code, HTML layout, and CSS style information that provide the function and appearance of an element in the app. In Angular, components can contain other components. An app's functions and appearance can be divided and partitioned into components.

In Angular, components have metadata that define its properties. When you create your HomeComponent, you use these properties:

- **selector**: to describe how Angular refers to the component in templates.
- **standalone**: to describe whether the component requires a NgModule.
- **imports**: to describe the component's dependencies.
- **template**: to describe the component's HTML markup and layout.
- **styleUrls**: to list the URLs of the CSS files that the component uses in an array.

starting with Angular 15.2, the **@Component** decorator now includes an imports array. This array isn’t related to TypeScript’s import statement. Instead, it’s specific to Angular and is used
to provide the compilation context for **standalone components**. It includes all other components, directives, pipes, and NgModules that are used in the template of the standalone component.

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
inject() must be called from an injection context such as a constructor, a factory function, a field initializer, or a function used with `runInInjectionContext`.

The singleton pattern is a design pattern of the creational type and allows the creation of objects whose access will be global in the system.

----------------------------------------------------------------------------

## Data binding

In Angular, data binding is a core concept that allows you to synchronize data between the model (component) and the view (template). There are two main types of data binding: one-way binding and two-way binding.

### One-way binding

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

### Two-way binding

Two-way binding allows data to flow in both directions: from the component to the view and from the view back to the component. This is particularly useful for form inputs where you want to keep the component's state in sync with user input.

```tsx
<input [(ngModel)]="username" />
```

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

## Modules in Angular + lazy loading + 404 page

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
  
## Guards in Angular

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

## Resolvers in Angular

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

## Interceptor Pattern

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

### Changing the request route

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

### Global loader

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

### Angular toasts

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
//    {
//      provide: HTTP_INTERCEPTORS,
//      useClass: NotificationInterceptor,
//      multi: true,
//    },
// . . .
// ]
```

### Measuring the performance of a request

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
//    {
//      provide: HTTP_INTERCEPTORS,
//      useClass: TelemetryInterceptor,
//      multi: true,
//    },
// ],
// . . .
```

```typescript
getInitialList(): Observable<ExerciseSetListAPI> {
  const headers = new HttpHeaders().set('X-TELEMETRY', 'true');
  return this.httpClient.get<ExerciseSetListAPI>(this.url, { headers});
}
```

## RxJS

The RxJS library that makes up the Angular ecosystem aims to make controlling asynchronous flows simpler using declarative and reactive programming.

- Observables and operators
- Handling data – transformation operators
- Another way to subscribe – the async pipe
- Connecting information flows – high-order operators
- Optimizing data consumption – filter operators

### Observables and operators

With **observable** data structure, we can capture a series of events in time and declaratively make our application react to these events. Regarding the use of promises for HTTP requests, we can use them, but tasks that are verbose and complex to perform when using promises can be done using observables and RxJS instead.

The **pipe()** method also returns an observable, and when the component calls the subscribe method, its result will go through all the operators and deliver the result.

### Another way to subscribe – the async pipe

One detail that you may have noticed is the $ symbol here. Using this postfix for variables and attributes that are observables is a community convention. It is not an obligation, but you will often see this symbol in code bases that use RxJS.

```angular
*ngFor="let suggestion of exercises$ | async"
```

Another advantage that the async pipe provides is that the framework controls the life cycle of the observable; that is, when the component is destroyed, Angular automatically triggers the unsubscribe method.

### Connecting information flows – high-order operators

```typescript
public exercises$ = this.entryForm.valueChanges.pipe(
  switchMap((model) => this.exerciseService.getExercises(model?.exercise))
);
```

The **switchMap** operator is a higher-order observable because it takes an observable as input and returns an observable as output. This is in contrast to the **map** operator, which takes an observable as input and returns a value as output.

### Optimizing data consumption – filter operators

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

### Signals

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

## Testing

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

### Component testing

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

### E2E tests with Cypress

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

## Micro frontend

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

### Angular elements

An Angular element component is a common component but transpiled to the Web Components standard, packaging not only our code but also the Angular rendering engine,
making it framework agnostic.

```bash
npm install @angular/elements --save
```

## Deploy

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

### Mounting a Docker image with Nginx

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
docker run -p 8080:80 myapp
```
