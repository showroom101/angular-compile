# ng2-compile-html

[![Build Status](https://travis-ci.org/patrikx3/ng2-compile-html.svg?branch=master)](https://travis-ci.org/patrikx3/ng2-compile-html)

Angular 2 Service to compile an HTML into a component

It is only using ```TypeScript``` right now. It can be built though.
  
##Install
  
```bash
npm install p3x-ng2-compile-html
```

##Test
   
```bash
git clone https://github.com/patrikx3/ng2-compile-html.git
cd ng2-compile-html
npm install
grunt run
```

[http://localhost:8080](http://localhost:8080)

##Usage
Check out the example, here [test/angular2/app/Page.ts](test/angular2/app/Page.ts).

###HTML
  
```html
<div #container>loading ...</div>
<div [p3xCompileHtml]="data" [p3xCompileHtmlRef]="ref">loading ...</div>
```

###TypeScript
  
```typescript
import {
     Component,
     Injectable,
     ViewChild,
     ViewContainerRef,
     OnInit
 } from '@angular/core';
 
 import {CompileHtmlService } from '../../../src';
 
 @Component({
     selector: 'p3x-ng2-compile-html-text',
     template: `
     <div #container>loading ...</div>
     <div [p3xCompileHtml]="data" [p3xCompileHtmlRef]="ref">loading ...</div>
 `,
 })
 @Injectable()
 export class Page implements OnInit {
 
     @ViewChild('container', {read: ViewContainerRef}) container: ViewContainerRef;
 
     data: string = `
     <div>Done</div>
     <a href="javascript:void(0);" (click)="ref.alert('ok')">
     If click works it says OK!
     </a>`;
 
     ref: Page;
 
     constructor( private compileHtmlService: CompileHtmlService ) {
         this.ref = this;
     }
 
     alert(string: string ) {
         alert(string);
     }
 
     ngOnInit() {
         this.compileHtmlService.compile({
             template: this.data,
             container: this.container,
             ref: this,
         })
     }
 
 }
```

by [Patrik Laszlo](http://patrikx3.tk)