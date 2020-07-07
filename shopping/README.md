# Shopping

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 9.1.7.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Learning

[propety] = "vaiable"
property = "string"
#local reference : Template variable : Html Type
@ViewChild('#localreference') or @viewChild(compponent) Element Ref ( agnular type ) : native property
viewChildVariable;

- ngonchanges (changes<input property>: only work for referenc change)>ngoninit>Ngdocheck<on every CD>AfterContentInit>AfterContentChecked>AfterViewInit>AfterViewChecked>onDestroy
- @contentChild : projected content access via reference vaariable similar to viewChild

- [ngClass] = "{odd:odd%2 !==0}
- [ngStyle] ={bakcgorund: od ? red: black}

## Creating Attribute Directive :

- inject elementRef(element on which directive sit)
- render2: this.renderer.setStyle(this.eleRef.nativeElement, 'backGround-color: blue')
- Via @HostListener('mouseEnter) mouseover
- Via @HostBinding
- passing properties to directive :

# Structural Directive \*:

- inject templateRef : template to display
- injjectvc Ref : viewContainerRef :where to display
- this.vcref.createEmbeddedView(this.templateRef)
- <div *ngIf= '!onlyOdd'>  >>>>>>> <ng-template [ngIf] = '!onlyOdd> </ng-tempalte>

# Services

-

- <a routerLink = "/servers">
- <a [routerLink ]= ["'/servers'"]> absolute path ./ relative path
  -Template routerLinkActive ="active" : apply class on activate
- Programtically: this.router.navigate(['/servers],{relativeTo: this.activatedRoute})
- accessing parameter: this.activatedroute.snapshot.param['id'] , Reatively : this.activatedRoute.params.subscribe((params)=>{} )

# Query Parameter and Fragment

- passing :<tmpalte> [routerLink] = "['/servers',5,'edit']'
  [qeryParams] = {allowEdit:1}
  <program> : this.router.navigate(['/servers',id,'edit],{queryParams: {allowEdit:1}})

# Nested Route

- childredn in route Array
- <route-outlet> added in parent component

# Template Form

- ngmodel & name added to eletment to make it form control
- access form #f='ngForm' : onSubmit(f) : f is form angular object of type ngForm contain(value,controls, valid....); same can be accessed via viewChild form
  - access formcontrol via #control = 'ngModel'
  - [ngModel] = "value' one way binding
  - [(ngModel)] = "vlaue" two way binding
  - [ngModelGroup] = 'userGroup'

# Reactive Form

- this.signupForm: formGroup = {
  'username': new FormControl(initialstate,validator)
  }
- `in html` <form [formGroup= 'singupFrom']>
  <input formControlName= "userName">

# custom validator

- validationFn (control:FC,): {[l:string:boolean]}
- async validator : validationFn (control:FC,): promist<any> | observable<any>

# statuschagnes and valuechagnes observable on reactive form

# Pipe

- custom pipe : implement pipetranfrom : function transform(value
- impure pipe : whenever data changes it is reflected immeditaley similar to onhchangepush strategy)

# Http

- Intercept : httpintercepteor interface : interceptor(req,next) method
- appmodule : providers: (provide:http_interceptor,use cals:)

# Dynamic component e.g entry component <ngmodal>

- component factory : componentFactoryResolver service
- const alertcomponent = this.componentfactoryResolver.resolve(alertComponent)
- viewContainerRef:
- helper direcitve : appplaceholder (viewContainerREf)
- <ng-template appplaceholder>
- access it in component via viewchild(appplaceholder).viewcontainerREf
- use component = viewContainerREf.createComponent
- pass data : component.instance.inputproperty = "dsaa"

# Modules

- services are availabe in all module
- router.forchild() in feature module and export it
- `Shared Module` , `core mdoule`
- `Lazy Module` : loadChildren: 'modulepath #module class name', rmeove it from appmoduleimport

- lazily loaded module have seperate service instance (child injector ) so provide only in rootmodule to have same instance

- # service worker
- single thread
- additional thread
- can listen to outgoing request
- cache the request/rewponse
- ng add `@angular/pwa`
  -appmoudle `serviceworkerreqister(/ngsw-worker.js)`
- `ngsw-confign.json` : what is need to cache

# Platform

- browserlist : brower to support : polyfill and css prefix as per browser list
- tsconfig.json : target : es2015
- angular.json file :multiple project , projectType: applicaton or library
-

ng generate angularmaterial:nav

- `Differential Loading`
- ng g application (app under projects)
- ng g library

>

# PERFORMANCE

` Speed, memory pressure, cpu usage(battery consumtion)

1. Load Time
2. Reload Time
3. Run Time

**Load Time**

- `Asset size`
- `Tree Shaking` Bundle size(webpack): remove : non-import library/file - non used method for imported file will be added - `service` provided in NgModule will be added irrespective of their use, however, if we use `provideIn` then if service not refered in app then it will not be part of final bundle - `image/asset optimization` : [asset optimizatio](https://web.dev/fast/#optimize-your-images)
- `compress asset`
- `Lazy Loading\pre-loading`
- `AOT` : compile typescript & template at build time
- `JIT`: Angular compiler added to bundle
- `ServerSide Rendering`: html page generate and serve from server instead of single index.html. 2. @angular universal pacakge help 3. crawlable by search
  **Re-Load Time**
  - `CACHING` : configure server to add header
    1. `Cache busting` to get always updated asset
  - `Service Worker` to cache and serve

> **Run Time** > **virtual scrolling/Infinte Scrolling**

- only show content as per viewport and add/remove as per scrolling [virtual scroll explain](https://medium.com/frontend-journeys/how-virtual-infinite-scrolling-works-239f7ee5aa58)
  > **PROFILLING** **CHANGE DETECTION** -

```javascript
main.ts
platformBrowserDynamic().bootstrapModule(AppModule)
  .then(moduleRef => {
    const applicationRef = moduleRef.injector.get(ApplicationRef);
    const componentRef = applicationRef.components[0];
    // allows to run `ng.profiler.timeChangeDetection();`
    enableDebugTools(componentRef);
  })
  .catch(err => console.log(err));
   - Then go to the page you want to profile, open your browser console, and execute the following instruction:
```

> ng.profiler.timeChangeDetection()
> ran 489 change detection cycles
> 1.02 ms per check

- You can also record the CPU profile during these checks to analyze them with ng.profiler.timeChangeDetection({ record: true }).

```
 - `trackBy in ngFor`  : if referennce changes of any item then node list is recreated , however , if we use `trackBy` then node will be recreted only when trackby attribute change, this save lots of dom node recreation
```

- `Change dectection strategies` : On push
- `ChangeDetectorRef` service inject:
  - detach()
  - detectChanges()
  - markForCheck()
  - reattach()
- `NGzone` service inject - runoutsidezone - run

* Unnecessary use of third-party packages for small use cases (
* **Gzip Compression**

```javascript
var compression = require("compression");
var express = require("express");
var app = express();
app.use(compression());
```

- use of `Web Worker`
- Avoid complex computations in the template

> (Angular Performance) [https://medium.com/faun/44-quick-tips-to-fine-tune-angular-performance-9f5768f5d945]
