# **Angular :**

#### 1- what is angular

* single page app .
* built on typescript . 
* component based framework 
* collection from libraries that include routing / client -server communication /forms



#### 2- essentials :

​	a) components :

* Temlpate : HTML temlpate to render the component .

* A Typescript class that defines behavior.(  import { Component } from '@angular/core';     )

* CSS selector : Iit is as id on how the component is used inside template  .to use the component : <selector></selectore>

*   CSS  style of the HTML elements .

  



​	b- Templates:

​	(HTML ) template .

* **data binding** (between  {{}}  double curly-brackets  ): use values from variables in ts class to appear in html template .

  ex:  <p>{{message}}</p> this display dynamic value from component ts class .

* **property bindings** (between [] square-brackets ): set values of properties and attributes to elements in HTML  ( say that we binding the property or attribute to a value in the component class): 

  ex:  

  ```html
  <p [id]="sayhello"
     [style.color]="colorfront"
   >
      hello all
  </p>
  
  <!-- sayhello & colorfront are values from ts class component >
   
  ```
  
  also for  **binding event listeners** (listen click , mouse movement , touch )
  
  ​         ex :  
  
  ```html
  <button [disabled]="diasalbled property" 
          (onclick)="onclick()"
          >
      send
  </button>
  <!-- disabledproperty is a value inside ts class component >
  <!-- on click() is a method inside ts class component 
  ```
  
  
  
  
  



c- Dependency injection :  declare typescript classes dependencies without initialized them . 

```tsx
import {Injectable} from '@angular/core' ;

@Injectable({providedIn : 'root'})
export class Logger {

writeCount(count : number){
console.warn(count);
}
}
/////////////////////////////////////////////////////////////////////////////////////////////////////////

import {Component} from '@angular/core'
import {Logger} from '../logger.service'
@Component ({
    selector : 'hello-world-di' ,
    templateUrl : './hello-world-di.html'
})
export class HelloWorldComponent{
    count= 0 ;
    constructor(private logger :Logger){}
    
    onLogMe(){
        this.logger.writeCount(this.count) ;
        this.count++ ;
    }
}

//here we inject Logger class (logger object ) in the counstructor argument , angular will initilize it so we can use it as this.logger


```



d- Angular CLI :

```tsx
ng build : build(compile) the angular app in the output directory(it is specified in specific file ) .
ng serve : build/rebuild+serve angular app in specific port 
ng test : run unit tests
ng e2e : build+serve angukar app + run e2e tests .
ng generate : generate/modified files base on schema
```



e- libraries

Angular router / angular forms/angular httpclient/angular animations /angular PWA /ANGULAR SCHEMATICS .

******************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************************

Angular (Udemy) :

section 1 : Getting started 

* Angular : it is a js framework , allow us to build reactive single page applications SPAs .with one HTML FILE (ROOT ) , instead of connect or get data from server for each page so the js is much faster to reload the changed (the data is got from server in the backgroung ) and js willl changed the DOM(change what the browser must displayed so it is changed the html during run time ). 

* Angular versioning :

  ![](/home/duaa/Pictures/s1.png)

  * Angular command Line (CLI) :

    used to create and optimize projects using  nodejs , nodejs is a server side language  . it is used npm (node package management)  this used to manage dependencies (include angular dependencies ) 

```
npm install -g @angular/cli       // g : global    this install angular cli from npm 
```

* create new project 

  1- go to directory 

  2- 

  ```
  ng new nameOfNewProject .
  ng new nameOfNewProject --no-strict      // nostrict mode , there is also optimize mode .
  ```

  *there is more setup because angular uses typescript which is a super set of js with additional features 

  3- go to directory of created project .

  4-

  ```
  ng serve    // this will build and serve the app with port 4200 by default .
  ```

  *inside package.json : 

  ​    dependecies : like animation/forms//http that from angular . which will adde to **node_modules** folder 

  

   * notes : 

      1-

     ```html
     <app-route> </app-route> this tag inside html is indicates for app-route component 
     ```

     2- when we inspict the page , we see a   bunch of script imports at the bottom. That is our build code and the Angular framework .These dynamically-injected script imports and these script imports will dynamically replace

     app-root with our own component (ts-html-css...) .

     3-  {{value inside ts }} this called data binding .

     4- angular split up into modules (sub packages ) . in app.modules : this till the angular which pieces is belong to our app . including the features like FormsModule (it is a typescript feature ) 

     ```ts
     //inside app.module.ts
     import { FormsModule } from '@angular/forms';
     //inside imports
     imports: [
         BrowserModule,
         AppRoutingModule,
         FormsModule
       ],
     
     ```

     

```html
<input type= "text" [(ngModel)]="name">    //ngmodel : is aform feature
<p >
    {{name}}
</p>

```



* TypeScript : 

  it is superset of js with more fetures like  types,classes , interfaces  .

  in ts we defined the type of variable (string,number) but in js we dont define them .

  ts does not run in the browser it is compiled into js by the CLI (that one of the reasons that why we need CLI (as project management ))

![](/home/duaa/Pictures/s2.png)



** Setup using bootstrap : 

```
npm install --save bootstrap@3  
// this will install bootstrap v3 locally in this project                                        not gloabally . (this will store in  node_modules) . we want piut the downloaded bootstrap css in main style (we will put it the path of it (fron node_modules) inside file called angular.json -> this file we will not change it but only added the new styles like bootstrap .)



```



******************************************************

*********************

***********

SECTION 2 :The Basics .

* how does our browser or server hosting our app by CLI  : 

  *the html component not the file thaht served by the server but  the main html (index.html) this served by the server .

  *inside index.html (in inspect) there are scripts below that injected by the CLI automatically  . these not appear inside file inside vs code but it appear after ng serve > ng serve will rebuild app it will create js bundles (include the compiled ts)a dded automatically  to final file (index.html) these scripts contains our code . 

  ![](/home/duaa/Pictures/s7.png)

  ![](/home/duaa/Pictures/s3.png)

  

  after ng serv and ing=jected the scripts these script start our project (the first file that will executed is main.ts)

  ​      *main.ts is the first file that will be executed . inside main.ts : we can enable productions ,etc ... but the most important things is that there is bootstrap module that start    our angular app by passing app module (app.module.ts) . inside this app module there are bootstrap section include boostrap which is  an array contained all components(their selctor name) that tell angular to analyze the index.html(must added/insert  to index.html as tag (by selector name )) . so the angular will read each component with its setup (html/css)

  ![](/home/duaa/Pictures/s4.png)

![](/home/duaa/Pictures/s5.png)



** very important note : the component that we put inside bootstrap is the root components not all components .

* Components :

  root component holds entire app that we will composit or add other component to it .(add to app.compont.html the other html  )

   each component has own HTML /MAYBE STYLE/ AND OWN BUSINESS LOGIC . This is benefit that  split complex app into reusable part /reusable component , maybe use the component more tha once and easily replicate the business logic or styling , istead of put every thing inone html file with single style 

** very important note : the component that we put inside bootstrap is the root components not all components . the other comonent tags(selector) will added inside html of root component

*name convention : server.component.ts  . the name of class ts  : ServerComponent 

*decorator : typescript feature allow us to enhance a class .

*Selector is the component tag that can we use as tag inside other components template(html).

* Modules:

*after create component ts  we need to use it so we must added into specific module . create the component not enough anguler will not know it if we dont put it inside module 

*angular uses the component to build web pages nd uses modules to bundle differnet pieces(component)

*in big project we may need to add more than one module but in general or in simple project we use app

 *module is a bundle of functionality that tell angular which features that app use .

we must import ng module from angular core to use @NgModule decorator . 

* there are 4 parts in module : 

  1-bootstrap : used to telll angular which component should aware when app start (i.e recognize in index.html).

  2-declarations : in this section we must put all component that belong to this module , without this angular will not knows them and we cant use them 

  3-imports : allow us to add other modules to this modules . also we add some modules built in angular (because angular itself is split into modules) like browsermodule/formsmodule/httpmodule

![](/home/duaa/Pictures/s8.png)



* inside root componet html i used other component tag  

  ```
  <app-server></app-server>    // this will teel angualr to read the setup files of this                                  component 
  ```

  component is reuasable ,we can use it more than one time with differrent business logic

  ```
  <app-server></app-server>
  <app-server></app-server>
  ```

  

** we can create component manualy or using CLI 

```
ng g c servers      // or ng generate component servers 
                    // this will create component with setup files and make selector and put                      //it inside app moduke by defoaulre but we must check it 
                  
```

//we can put inline template 

```
@Component({
  selector: 'app-servers',
  template: 
  `
  <app-server> </appserver>
  `,
  styleUrls: ['./servers.component.css']
})

// this `` used to put multi lines
```

//each created component will impelemnt(OnInit)



**Styling : 

  inside html we can use <div> (.nameof class will create new div wih this class name) to be nicer

inside style template we can putmore than one style url because it is an array .also we can write inline style 

```
styles:[ 
`
h1{
color:dodgerblue;
}
` ]
```



**data binding : 

  communicate betwenn ts code and html .  

1- output data:from ts to html    (string interpolation ,prperty binding )/2- events:from html to ts(event binding)

3-two way communication : first react event then output data at the same time

![](/home/duaa/Pictures/s9.png)



1- string interpolation :

```
{{String}}   // inside {{}} it can be any exepression that get string . if the data                      is number it will take it and convert it as string ( somthing                        can converted to string , may be it a method return a string or                      somthing can convert to string) so we can call it 


//inside ts 
  serverId:number = 12 ;
  serverStatus:String='offline';
  serverPort =4200
  getServerPort(){
    return this.serverPort ;
  }


//in html 
<p>server with id {{serverId}} is {{serverStatus}} and port {{getServerPort()}} </p> 
```

2- property binding

 for example for buttuns , the property is dynamically (once changed at run time  it is will changed in DOM)

it used for property for html elements or for directives/component  properties 

```
// in ts
  allowNewServer = false ;
  constructor() {
    setTimeout(
          ()=>{this.allowNewServer=true;}
      ,
      2000
    )

   }
   
   // in html 
   
   <button class="btn btn-primary" 
[disabled]="allowNewServer"
>addNewServer</button>
or 
<button class="btn btn-primary" 
[disabled]="!allowNewServer"
>addNewServer</button>


//these get the same result (string interpolation and property binding )
<p> {{allowNewServer}} </p>  // this return trur or false (convert to string)
<p [innerText="allowNewServer"]></p>    // this also return true/false so it is get                                           the value and put asstring(text )
```



3- event binding :

for each event (for eample for button ) we must create method in ts (onCreateSomthing()) start with on .

```
//in ts 
  createServerStatus ='no server was created'

onCreateServer(){
  this.createServerStatus='server is created'
  }


//in html 
<button class="btn btn-primary" 
[disabled]="!allowNewServer"
(click)="onCreateServer()"                // this is event binding from htmml to ts
>addNewServer</button>
<p>{{createServerStatus}}</p>
<p>{{allowNewServer}}</p>
```

4- two way binding :

----without wow way :

```
// we have input with event binding to set value in ts with method and because we get value from user we put inside ($event) this used to catch the value that put insid input from user . then i will use it as string binding or property binding , 

// inside html
<label>ServerName</label>
<input type="text" class="form-control"
   (input)="onUpdateServerName($event)"
>
<p>{{serverName}}</p>

//inside ts
  serverName ='';
  ....
   onUpdateServerName(event: any){
    console.log(event.target.value);
    this.serverName=event.target.value ;
  }

```

---with two way binding that provides from angular we need FormModule which is built in angualrmodule , we must put it inside app modules in import section

```
import { FormsModule } from '@angular/forms';  

//two way:combined property binding with event binding like this [(ngModel)]="valueInside-ts"  it is not call method but it must value  , it is trigger on input event then update the value automaticaly without need to implemnt method to update also it udate the input value that appear in input automaticaly 

// in ts 
  serverName ='dudu';  wihtout need method to get event then update
  
// in html 
<input type="text" class="form-control"
   [(ngModel)]="serverName"         // this is two way binding 
>
<p>{{serverName}}</p>               //here we can use it because it is updated 												automaticaly 

```

```

//here we get value input using two way binding then i used this value (that updated automaticaly ) inside event binding (click) that call method uthat used this value to update another value and display it  

//in html 

<label>ServerName</label>
<input type="text" class="form-control"
   [(ngModel)]="serverName"
>

<button class="btn btn-primary" 
[disabled]="!allowNewServer"
(click)="onCreateServer()"
>addNewServer</button>

<p>{{createServerStatus}}</p>


// in ts

serverName ='dudu';
  createServerStatus ='no server was created'

  onCreateServer(){
  this.createServerStatus='server is created with name '+this.serverName
  }
```

  assignment : 

```
// html 
<ol>
  <li>Add a Input field which updates a property ('username') via Two-Way-Binding</li>
  <li>Output the username property via String Interpolation (in a paragraph below the input)</li>
  <li>Add a button which may only be clicked if the username is NOT an empty string</li>
  <li>Upon clicking the button, the username should be reset to an empty string</li>
</ol>

<label> user name </label>
<input type="text" class="form-control"
[(ngModel)]='username'
>
<p>{{username}}</p>

<button class="btn btn-primary" 
  [disabled]="!allowClickStatus()"       // or direct [disabled]="username===''"
                                         if usrename empty make it disabled
  (click)='onClickResetUser()'>          // or direct "username=''" reset empty
 Reset User
</button>


//ts 

export class AppComponent {
  username = ''
  allowClick = false ;

  allowClickStatus(){
    if(this.username!=='')
      {this.allowClick=true ;}

      return this.allowClick ;

  }

  onClickResetUser(){
    this.username=''
    this.allowClick = false
  }

}
```



*****************************

* DIRECTIVE :

   directives are instructions in the DOM  , like if we want to put paragrah conditionaly so we use *ngif , 

  the star is important because ngif is astructural directive that means it changes the structure of DOM so it a property inside html 

  1- ngIF

```
in html //
<label>ServerName</label>
<input type="text" class="form-control"
   [(ngModel)]="serverName"
>

<button class="btn btn-primary" 
[disabled]="!allowNewServer"
(click)="onCreateServer()"
>addNewServer</button>

<p *ngIf="createsever">{{createServerStatus}}</p>

/////if with else 
//instead of the above   but this not usually used there is  another way later 
<p *ngIf="createsever; else noserver">{{createServerStatus}}</p>
<ng-template #noserver>                         
   <p>
      no server created
   </p>
</ng-template>
note: ng template used if we want to save somthing in DOM and used it later if we need 


/////////////in ts
   createsever=false ;
 onCreateServer(){
  this.createServerStatus='server is created with name '+this.serverName
  this.createsever=true
  }
  
```

2-ngStyle : usually used it as property for tag , we can use it with property binding and put some properties from ts value , inside[] we dont put *   , ngStyle dynamicaly updated style .

 it take js object (key value pair ehich is property with its value) 

```
//inside html 
<p [ngStyle]="{backgroundColor:getColor()}">server with id {{serverId}} is {{serverStatus}}  </p> 

//inside ts 
 serverId:number = 12 ;
  serverStatus:String='offline';

   constructor() {
     this.serverStatus = Math.random() > 0.5 ?'online':'offline';
   }
   getColor(){
     return this.serverStatus==='online' ? 'green':'red'
   }

```

 

3- ngClass : used to dynamically add or remove css classes .

ng class also used as databinding [ngCLass]="" , it tak js object (key value pair which key is the Css class name , value is condition if this class should attached or not )

```
// inside ts i made css class inside styles 

@Component({
  selector: 'app-servers',
  templateUrl: './servers.component.html',
 // styleUrls: ['./servers.component.css' ],
  styles:[`
     .online{
       color : blue 
     }
  `]
})

// inside html 

<p 
[ngStyle]="{backgroundColor:getColor()}"
[ngClass]="{online:serverStatus==='online'}"
>server with id {{serverId}} is {{serverStatus}}  </p> 
```

4- ngFor:

in parent thers is list . inside html parent i used child component with ng for (without reding values )

```
\//in ts 
servers=['hi','dudu']
onCreateServer(){
  this.servers.push(this.serverName);
  this.createServerStatus='server is created with name '+this.serverName
  this.createsever=true
  }
  
  
//  in html 
<label>ServerName</label>
<input type="text" class="form-control"
   [(ngModel)]="serverName"
>
<button class="btn btn-primary" 
[disabled]="!allowNewServer"
(click)="onCreateServer()"
>addNewServer</button>

 <app-server *ngFor="let server of servers"></app-server>   //these for loop inside servers and make each loop as app server without read the values 
 
 the output :
 
```

![](/home/duaa/Pictures/s10.png)

// assignment 3 : 

```
<div class="container">
  <div class="row">
    <div class="col-xs-12">
      <ol>
        <li>Add A button which says 'Display Details'</li>
        <li>Add a paragraph with any content of your choice (e.g. 'Secret Password = tuna')</li>
        <li>Toggle the displaying of that paragraph with the button created in the first step</li>
        <li>Log all button clicks in an array and output that array below the secret paragraph (maybe log a timestamp or simply an incrementing number)</li>
        <li>Starting at the 5th log item, give all future log items a blue background (via ngStyle) and white color (ngClass)</li>
      </ol>
    </div>
  </div>
</div>
```

** to toggle the button or shoe paragraph  (my answer is to set inside onclick with watit time  but max inside html direct allowDisplay =!allowdisplay  inside (click) )

my-sol :  there is problem with ngclass/style  because i fill list with objects date .get time so has error .

```
//inside ts :
 allowDispaly= false ;
  allowClick=true;
  numOfClicked=[];
  secretPassword = "tuna" ;
  



  onClickButton(){
  this.allowDispaly=true ;
  this.allowClick=false ;
  this.numOfClicked.push(new Date().getTime);

  setTimeout(
    ()=>{this.allowDispaly=false;
      this.allowClick=true;
    }
    ,
    2000
    )

  }


  getColor(){
    if (this.numOfClicked.length>4)
     return 'blue';
}

  getclickedColor(){

    if (this.numOfClicked.length>4)
    return true ;
}
  

}


//inside html 
div class="container">
<div class="row">
  <button class="btn btn-primary"
  [disabled]="allowDispaly"
    (click)= "onClickButton()"
    >
    Display Details
  </button>
  <p  
    *ngIf = "allowDispaly"
  >  
      Secret Password = {{secretPassword}} 
  </p>

<p 
    *ngFor='let clickTime of numOfClicked   '
    [ngStyle]="{backgroundColor:numOfClicked.indexOf(clickTime)>=4? 'blue': 'transparent'}"
    [ngClass]="{'clickColor':numOfClicked.indexOf(clickTime)>=4}" 
    > {{clickTime}}  </p>
</div>
</div>

```

```
the right sol :instead of loop above (loobing with number )

//in ts :   this.numOfClicked.push(this.numOfClicked.length+1);
in html :
 <p 
    *ngFor='let clickTime of numOfClicked '
    [ngStyle]="{backgroundColor:clickTime>=5? 'blue': 'transparent'}"
    [ngClass]="{'clickColor':clickTime>=5}" 
    > {{clickTime}}  </p>
    
    // note clickTime is cinsiderd as value . we use it with {{}} inside html .
    //name of css clase must be inside ' ' if we use it from css file
    // we can used div instead of p .
    
    
    // insead of set time wait we can di this    
    this.allowDispaly=!this.allowDispaly
    
   
```

```
//for looping with date . 
//we add new let thate reserved  the index 
// or as i solved  above  :  :[ngStyle]="{backgroundColor:numOfClicked.indexOf(clickTime)>=4? 'blue': 'transparent'}"


in ts : 
  this.numOfClicked.push(new Date());
 <p 
    *ngFor='let clickTime of numOfClicked ; let i = index  '
    [ngStyle]="{backgroundColor:i>=4? 'blue': 'transparent'}"
    [ngClass]="{'clickColor':i>=4}" 
    > {{clickTime}}  </p>
    
//    p or div 
```





//////////////////////////////////////////////////////////////////////////

//////////////////////////////////////////////////////////////////////////////

# Course Project 1 :

![](/home/duaa/Pictures/s11.png)

![](/home/duaa/Pictures/s12.png)

Steps :

1- create project and add bootstrap 3 

2- generate component without tests (ng g c  name --skipTests true)

// app component : root component d

​    ->  1) header component  : inside app component folder (parent).

​        2) recipe component :  inside app component folder(parent )(overall component of each recipe(list-item ....) ) we 					considered as component  

  	  3) recipe-list component : inside recipe component folder (parent  )  ng g c recipes/recipe-list --skipTests true     (we    			put 			path)   

​		 4)recipe-detail :inside recipe component  folder (parent  ) ng g c recipes/recipe-detail--skipTests true 

​        5)recipe-item : inside recipe-list component folder  ng g c recipes/recipe-list/recipe-item --skipTests true 

/// another order : we can consider recipe list as parent component and inside it we put recipe item  and recipe detail 

6)shopping list : inside app component folder(parent) 

7)shopping -edit : inside shopping list component folder(parent)

 3- using the component : the child inside the parent 

4- edit the header : 

  using default bootstrap header :

![](/home/duaa/Pictures/s15.png)

```html

// to make navigator with header . (navbar navbar-default)
  //to have my own view (container-fluid)
// click header 
// collaps navbar for list 
     
         
<nav class="navbar navbar-default">
<div class="container-fluid">
    <div class="navbar-header">
        <button type="button" class="navbar-toggle" (click)="collapsed = !collapsed">
          <span class="icon-bar" *ngFor="let iconBar of [1, 2, 3]"></span>
        </button>
        <a routerLink="/" class="navbar-brand">Recipe Book</a>
      </div>
      <div class="navbar-collapse" [class.collapse]="collapsed" (window:resize)="collapsed = true">
     <ul class="nav navbar-nav">
         <li><a href="#">Recipes</a></li>
         <li><a href="#">ShoppingList</a></li>
     </ul> 
     <ul class="nav navbar-nav navbar-right">
         <li class ="dropdown">
             <a href="#" class="dropdown-toggle" role="button">Manage<span class="caret"></span></a>
             <ul class="dropdown-menu">
                 <li><a href="#">Save Data</a></li>
                 <li><a href="#">Fetch Data</a></li>
             </ul>
         </li>
     </ul>
    </div>
</div>
</nav>



```





5-create recipe model and use it to create arrays of it inside recipelistcomponent

  ![](/home/duaa/Pictures/s16.png)

fill the list then inside recipelist hrml using ng for  of this list 

```
recipes: Recipe[] =[]
```

```
<div class="row">
    <div class="col-xs-12">
        <button class="btn btn-success">New Recipe</button>
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        <a href="#"
         class="list-group-item clearfix"
         *ngFor="let recipe of recipes">
           <div class="pull-left">
               <h4 class="list-group-item-heading"> {{recipe.name}}</h4>
               <p class="list-group-item-text">{{recipe.description}}</p>
           </div>
           <span class="pull-right">
               <img
                                         
                [src]="recipe.imagePath"      /// or this <!-- src="{{recipe.name}}" -->
                alt="{{recipe.name}}"
                class="img-responsive" 
                style="max-height: 50px;">
           </span>



        </a>
        <app-recipe-item></app-recipe-item>
    </div>
</div>

```

instead of recipe list these the result . 

![](/home/duaa/Pictures/s17.png)

6- add the needed rows and cols in recipe-details . later we will connect these 3 component togheter (recipe list with reciipe details )

![](/home/duaa/Pictures/s18.png)

7- shopping list : 

create ingredient model( we will used in both shopping list an recipes so we create folder called shared and create it inside app folder  ) . 



****************************************

Section 4 : Debugging

**source maps : inside inspect -> source : this is the maps from ts to js . we can debugging the code . 

but if we nedd to debug our code as it self from ->sources -> webpack ....

Section 5 : Component and datbinding deep dive 

** CMP-DATABINDING-START  PROJECT :

- WE HAVE APP COMPONENT WITH 2 CHILD COMPONENT (COCKPIT AND SERVER ELEMENT ) . 

- app component has array of server elements . 

- cockpit has to get input values and fill the array inside app component : so need to talk with app component (cockpit with app component ).
- server element is showing the info of element from the array that exist in app component (so server element compentnt will talk with app component ).

![](/home/duaa/Pictures/s21.png)



-start with  sever-element component with app component : 

inside app html we make for loop of array inside app ts  and will pass each element to server element html . :

steps : 

1)  (passing value from parent to child these need input element so  we must must define the element with input decorator inside child (server element) and define the type of it  )  input (parent بدو ياخد داتا من ال passing data to the component  )

   ```
     @Input () element : {type:string , name:string , content : string}   //or create model 
     constructor() { }
   ```

2) (pinding to custom property )using property binding we pass each element from arrary to elemnt input that defined inside child (server-element)

   ```
   //inside app ts :
     serverElements = [{type:'server' , name:'Testserver' , content : 'just a test '}];
   
   
   //inside app html
   <div class="container">
     <app-cockpit></app-cockpit>
     <hr>
     <div class="row">
       <div class="col-xs-12">
         <app-server-element 
         *ngFor="let serverElement of serverElements"
         [element]="serverElement"></app-server-element>         ** here 
       </div>
     </div>
   </div>
   ```

   ** we can add alias instead of using element input name to binding  so the property(element) inside child and data from parent (App)

```
  //inside ts child
  @Input ('svrElement') element : {type:string , name:string , content : string}
//inside html parent 
<div class="container">
  <app-cockpit></app-cockpit>
  <hr>
  <div class="row">
    <div class="col-xs-12">
      <app-server-element 
      *ngFor="let serverElement of serverElements"
      [svrElement]="serverElement"></app-server-element>
    </div>
  </div>
</div>
```



-  cockpit  component with app component : 

  1) when component has changes (like click button )and then it inform (give data to )the parent component  .

     from child to parent (@output() parent بدو يعطي داتا لل  passing event output the component  ) here we must defined the events as output inside child(cockpit) that inform data to parent (app)  so the event property is inside child.and the action inside parent(app)

​           2.  inside parent we define the actions when get the data and inside the child we defined the output(event                         property ) as event emmiter that define inside it the expected object that must emit (so we defined also functions to emit   this events with objects )

```
inside child ts : 
  newServerName = '';
  newServerContent = '';  // for inputs 

  @Output() serverCreated = new EventEmitter<{name:string,content:string}>() ;
  @Output() blueprintCreated= new EventEmitter<{name:string,content:string}>() ;

  constructor() { }

  ngOnInit(): void {
  }

  onAddServer() {
    this.serverCreated.emit({name:this.newServerName,content:this.newServerContent})
  }

  onAddBlueprint() {
    this.blueprintCreated.emit({name:this.newServerName,content:this.newServerContent})
  }
  
  //inside parent ts : 
   serverElements = [{type:'server' , name:'Testserver' , content : 'just a test '}];
  
  

  onServerCreated(serverData:{name:string,content:string}) {
    this.serverElements.push({
      type: 'server',
      name: serverData.name,
      content: serverData.content
    });
  }

  onBlueprintCreated(blueprintServerData:{name:string,content:string}) {
    this.serverElements.push({
      type: 'blueprint',
      name: blueprintServerData.name,
      content: blueprintServerData.content
    });
  }
}

//inside html chidl :
<div class="row">
    <div class="col-xs-12">
      <p>Add new Servers or blueprints!</p>
      <label>Server Name</label>
      <input type="text" class="form-control" [(ngModel)]="newServerName">
      <label>Server Content</label>
      <input type="text" class="form-control" [(ngModel)]="newServerContent">
      <br>
      <button
        class="btn btn-primary"
        (click)="onAddServer()">Add Server</button>    // its normaly but the event is the 
      <button                                         // function that emit .
        class="btn btn-primary"
        (click)="onAddBlueprint()">Add Server Blueprint</button>
    </div>
  </div>
  
  inside html parent : 
  //
  <div class="container">
  <app-cockpit
  (serverCreated)="onServerCreated($event)"             //here
  (blueprintCreated)="onBlueprintCreated($event)">   // here
  </app-cockpit>
  <hr>
  <div class="row">
    <div class="col-xs-12">
      <app-server-element 
      *ngFor="let serverElement of serverElements"
      [svrElement]="serverElement"></app-server-element>
    </div>
  </div>
</div>

```

 ** we can use alias instead of using the name of event output inside ts . we use this alias  in outside(inside parent component )

```
// in ts child cookpit 
  @Output('bpcreated') blueprintCreated= new EventEmitter<{name:string,content:string}>() ;

//in html parent(app)

```

* View Encapsulation : 

  **angular gives same attribute (in css component ) to all elements in component (that we put this attribute to it ).

  **angular added strange attribute to each element . 

  **the default is on(encapsulation.emulated) but we can added Encapsulation inside component decorator  to disable the view encapsulation , here id we defined attribute inside css then this will affect globally and may affect other component 

  ** if we defined style for element inside html and inside css component there is defined style it take the style that put inside html not css component 

*  DOM: Document Object Model 

​     is a programming API for HTML and XML documents. , It defines the logical structure of documents and the way a        document is accessed and manipulated. 

​     

* Local reference in template : 

  if we want to get input value to use them inside function just  and we dont need to use them inside ts so we can put local reference to this element inside html and use this refrence inside html and base it for example for button function and inside this function i put argument of this reference . but to use it we call .value     

  but if we want to use it inside ts in many funcction we need to get it using 2 way binding .

  ```
  //inside html 
  <div class="row">
    <div class="col-xs-12">
      <p>Add new Servers or blueprints!</p>
      <label>Server Name</label>
      <!-- <input type="text" class="form-control" [(ngModel)]="newServerName"> -->                                                                       // instead  of this 
      <input type="text"                                         //we put reference 
      class="form-control" 
      #serverNameInput>
      
      <label>Server Content</label>
      <input type="text" class="form-control" [(ngModel)]="newServerContent">
      <br>
      <button
        class="btn btn-primary"
        (click)="onAddServer(serverNameInput)">Add Server</button> //we use reference 
      <button
        class="btn btn-primary"
        (click)="onAddBlueprint()">Add Server Blueprint</button>
    </div>
  </div>
  
  
  //inside ts :
  onAddServer(nameInput:HTMLInputElement) {   // here we dont need  to define value above
      console.log(nameInput.value)
      this.serverCreated.emit(
        {name:nameInput.value,
         content:this.newServerContent})
    }
  
  ```

  * View child 

  ** w e can also direct access to elements in our Dom in our template through at view child :

   first we define local reference to html element then inside ts make view value decorator for it and read it as follow : 

  ```
  //inside html 
  <input type="text" 
      class="form-control" 
     #serverContentInput>
     
  //inside ts : 
    @ViewChild('serverContentInput',{static:true}) serverContentInput: ElementRef ; 
    onAddServer(nameInput:HTMLInputElement) {
      console.log(nameInput.value)
      this.serverCreated.emit(
        {name:nameInput.value,
         content:this.serverContentInput.nativeElement.value})  // here to read it 
    }  
  ```

  //in complex projects when component need to get data from parents component(more than one component ) its prefer to show the data not in child component html but inside parent component html between child tag  , but inside child component we must add (ng-content) tag this tell angular where it must show values (it still display inside component html ) as follow 

   // in other word : tell the angular to put in ng content place what there is inside the component tag .(projected to component )

  ///angular does not take care about any thing between  curly brachet {{}} but if we use ng-content it will care about it  
  
  //here we didint use the input directive 
  
  ```
  //inside parent html : 
  <div class="row">
      <div class="col-xs-12">
        <app-server-element 
        *ngFor="let serverElement of serverElements"
        [svrElement]="serverElement">
      
        <p class='p'>
          <strong *ngIf="serverElement.type === 'server'" style="color: red">{{ serverElement.content }}</strong>
          <em *ngIf="serverElement.type === 'blueprint'">{{ serverElement.content }}</em>
        </p>
      
      </app-server-element>      //between child tag we put what ng content must show
      </div>
    </div>
    
    
    
  //inside child html 
  <div
  class="panel panel-default"
  >
  <div class="panel-heading">{{ element.name }}</div>
  <div class="panel-body">
    <ng-content></ng-content>   //here
  </div>
  </div>
  ```
  
  

*  Component life cycle hooks: 

  -ngOnChange : @input  , ngOnInit: execute afterConstructot , ngDoCheck : executed alot 

  -run in order 

  -we nust import interfaces from it them from angular core  before use them 

![](/home/duaa/Pictures/s23.png)

```
//inside ts 
export class AppComponent implements OnInit ,
OnChanges,
DoCheck,
AfterContentInit,
AfterContentChecked,
AfterViewInit,
AfterViewChecked,
OnDestroy{....}

//we can added implentaion inside them as we need 
ngOnChanges(changes:SimpleChanges){
    console.log('ngOnChanges called')
  }

  ngOnInit(){
    console.log('ngOnInit called')

  }

  ngDoCheck(){
    console.log('ngDoCheck called')

  }

  ngAfterContentInit(){
    console.log('ngAfterContentInit called')

  }


  ngAfterContentChecked(){
    console.log('ngAfterContentChecked called')

  }

  ngAfterViewInit(){
    console.log('ngAfterViewInit called')

  }

  ngAfterViewChecked(){
    console.log('ngAfterViewChecked called')

  }

  ngOnDestroy(){
    console.log('ngOnDestroy called')

  }


```

// when we read local instance using view child (from dom ) this will be exist after ngAfterViewInit not befor it . (after the view rendered )

**video 78-79more details on lifecycle hooks

* @ContentChild : 

  if we define reference inside html component we can get it inside same ts component using viewChild .

  but if we using ng content and we put content of child inside parent(app) html and we put local reference inside this child tag content , we can get value of this reference inside parent ts using viewchild but inside child ts we cannot use viewchild but we can use ContentChild . 

  also ContentChild will not exist until ngAfterContentInit is called .

  

////TODO :  ASSIGMENT NOT SOLVED

COURSE-PROJECT : 



1- first we need header to tell parent(app) which recipe or shopping-list must appear , so header child need to pass feature to parent app (output data ).

```html
//inside child (header)html :
  <ul class="nav navbar-nav">
                <li><a href="#" (click)="onSelect('recipe')">Recipes</a></li>
                <li><a href="#"(click)="onSelect('shopping-list')">ShoppingList</a></li>
            </ul>
```

```ts
//inside child (header) ts : 

    @Output() featureSelected = new EventEmitter<string>() ;

    onSelect(feature:string){
        this.featureSelected.emit(feature);
        }
}

```

```ts
//inside parent(app) ts :

  loadedFeature='recipe';

  onNavigate(feature:string){
 this.loadedFeature=feature;
  }


```

```html
//inside parent app (html)
<app-header
 (featureSelected)="onNavigate($event)"
 ></app-header>

<div class="container">
<div class="row">
  <div class="col-md-12">
    <app-recipes *ngIf="loadedFeature==='recipe'"></app-recipes>
    <app-shopping-list *ngIf="loadedFeature!=='recipe'"></app-shopping-list>
  </div>
</div>

</div>
```

2- passing recipe data with property bindings . (from parent (recipe-list to child (recipe-item)) (input property in child .)

```html
inside parent html (recipe-list) 
<div class="row">
    <div class="col-xs-12">
        
        <app-recipe-item 
        *ngFor="let recipeEl of recipes " 
        [recipe]="recipeEl"></app-recipe-item>
    </div>
</div>

```

```tsx
//inside child ts (recipe-item)
  @Input () recipe : Recipe 

```

```html
//inside  child html (recipe-item)
<a href="#"
         class="list-group-item clearfix"
         >
           <div class="pull-left">
               <h4 class="list-group-item-heading"> {{recipe.name}}</h4>
               <p class="list-group-item-text">{{recipe.description}}</p>
           </div>
           <span class="pull-right">
               <img
                [src]="recipe.imagePath" 
                alt="{{recipe.name}}"
                class="img-responsive" 
                style="max-height: 50px;">
           </span>

 </a>
```

3- we want if we click on any recipe-item it will appeare recipe in recipe detail . this sol is complex it will solve by a nother  solution later :

 first recipe-item give his parent (recipe-list) the recipe using event (output) . then recipe-list give his parent(recipes) this recipe using event (output). then recipes give his child(recipe-detail) this recipe using property binding (input)   

```
//inside recipe-item html 
<a href="#"
         class="list-group-item clearfix"
         (click)="onSelected()"
         >
         ....
         ***************************************
         
 //inside recipe-item ts 
 
 @Output () recipeSelected=new EventEmitter<void>(); 
  constructor() { }
  onSelected(){
  this.recipeSelected.emit()
;
***************************************
//inside recipe-list html 
<div class="col-xs-12">
        
        <app-recipe-item 
        *ngFor="let recipeEl of recipes " 
        [recipe]="recipeEl"
        (recipeSelected)="onRecipeSelected(recipeEl)"></app-recipe-item>
    </div>
    ***************************************
  //inside recipe-list ts 
  @Output() recipeWasSelected = new EventEmitter<Recipe>();
  
  nRecipeSelected(recipe:Recipe){
    this.recipeWasSelected.emit(recipe);
  }
***************************************
//inside recipes ts 
  selectedRecipe : Recipe ; 

//inside recipes html : 
<div class="row">
    <div class="col-md-5">
        <app-recipe-list (recipeWasSelected)="selectedRecipe=$event"></app-recipe-list> 
    </div>
    <div class="col-md-7">
        <app-recipe-detail
        *ngIf="selectedRecipe ; else infoText"        //here
        [recipe]="selectedRecipe"> </app-recipe-detail>  //here

        <ng-template #infoText>                  //here
            <p>Please select a Recipe !</p>
        </ng-template>
    </div>
</div>
  
  ***************************************
  //inside recipe-detail ts :
    @Input() recipe :Recipe ;
//inside recipe-detail html :
div class="row">
    <div class="col-xs-12">
        <img [src]="recipe.imagePath"        //here
        alt="{{recipe.name}}"            //here
        class="img-responsive"
      style="max-height: 300px;" >
           > 
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        <h1>{{recipe.name}}</h1>        //here
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        <div class="btn-group">
            <button 
            type="button"
            class="btn btn-primary dropdown-toggle">
            ManageRecipe <span class="caret"></span>
           </button>
        <ul class="dropdown-menu">
            <li><a href="#">To SHopping List</a></li>
            <li><a href="#">Edit Recipe</a></li>
            <li><a href="#">Delete Recipe</a></li>
        </ul>
        </div>
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        {{recipe.description}}                  //here
    </div>
</div>
<div class="row">
    <div class="col-xs-12">
        Ingredient
    </div>
</div>
```

4- Allowing the User to Add Ingredients to the Shopping List :

  we need to make the shopping-edit take the inputs(input and amount) so we used @ViewChild and give them to parent(shopping-list) (output event ) to add them in ingredients list that shopping list it self display them . 

```html
//in child (shopping-edit) html 
<div class="row">
    <div class="col-xs-12">
        <form >
            <div class="row">
                <div class="col-sm-5 form-group">
                    <label for="name">Name</label>
                    <input 
                    type="text" 
                    id="name" 
                    class="form-control"
                    #nameInput>                  //here
                </div>
                <div class="col-sm-2 form-group">
                    <label for="amount">Amount</label>
                    <input 
                    type="number" 
                    id="amount" 
                    class="form-control"
                    #amountInput>               //here
                </div>
            </div>
            <div class="row">
                <div class="col-xs-12">
                    <button class="btn btn-success" type="submit" (click)="onAddItem()">Add</button>                                   //here
                    <button class="btn btn-danger" type="button">Delete</button>
                    <button class="btn btn-primary" type="button">Clear</button>
                </div>
            </div>
        </form>
    </div>
</div>
```

```ts
//in child (shopping-edit) ts  
 @ViewChild('nameInput') nameInputRef : ElementRef ;
  @ViewChild('amountInput') amountInputRef : ElementRef ;
  @Output() ingredientAdded = new EventEmitter<Ingredient>();
  constructor() { }
  
  onAddItem(){
    const ingName= this.nameInputRef.nativeElement.value;
    const ingAmount=this.amountInputRef.nativeElement.value;
    const newIngredient = new Ingredient(ingName,ingAmount)
    this.ingredientAdded.emit(newIngredient)
  }

```

```html
// in parent(shopping-list) html 
<div class="row">
    <div class="col-xs-10">
        <app-shopping-edit  
        (ingredientAdded)="onIngredientAdded($event)"></app-shopping-edit>      //here
        <hr>
        <!-- <p>The list</p> -->
        <ul class="list-group">
            <a
             class="list-group-item" 
             style="cursor: pointer"
             *ngFor="let ingredient of ingredients "
             >
                {{ingredient.name}} ({{ingredient.amount}})
            </a>
        </ul>
    </div>
 </div>  
   
```

```ts
// in parent(shopping-list) ts 
 onIngredientAdded(ingredient:Ingredient){
    this.ingredients.push(ingredient) ;

  }

```

DIRECTIVES DEEP DIVE : 

** attribute directives set on element  , structural directives : also do the same but it is also change the structure of the DOM around this element  . for example : If we have *ngIf on a paragraph, if that condition is false, this paragraph is removed from the DOM, so the overall view container is affected so it is structural directive . but in attribute directive we never destroy the element inside DOM it just changes some property of this element   .

![](/home/duaa/Pictures/s24.png)

-> PROJECT CALLED :DIRETIVES-START

* we can't use 2 directives(ex: *ngIf & *ngFor ) for the same element . we can put the element inside div and put the second directive to div

  * we want to implement directive : 

    ```ts
    import { Directive, ElementRef, OnInit } from "@angular/core";
    
    @Directive({
        selector : '[appBasicHighlight]'     // here we put [] to use it inside html                                                 without [] 
    })
     export class BasicHighlightDirective implements OnInit {
        constructor (private elementRef: ElementRef){}    //must have ref 
    
        ngOnInit(){
         this.elementRef.nativeElement.style.backgroundColor='green' //set the syle 
    
        }
    }
    //then we can use it in any component html as directive 
    <p appBasicHighlight > Style me with basic Directive !</p>
    
    ```

    this is not good practice since it access the element directly , the best practice is to use render with element to build directive . as follow 

    1- to generate directive using CLI  : ng g d name . 

    2- 

    ```ts
    import { Directive, ElementRef, OnInit, Renderer2 } from '@angular/core';
    
    @Directive({
      selector: '[appBetterHighlight]'
    })
    export class BetterHighlightDirective implements OnInit{
    
      constructor(private elRef:ElementRef , private renderer:Renderer2) { }  // here we used Renderer2 
    
      ngOnInit(){
        this.renderer.setStyle(this.elRef.nativeElement,'background-color','blue') // here we can access the DOM ex:this.renderer.setProperty , this.renderer.createElement
      }
    }
    // in app component  html :
    <p appBetterHighlight > Style me with better Directive !</p>
    
    ```

    the above is better approach of accessing the DOM, because the first approach may not access the DOM in some places .

    we can also use HostListener inside directive to react with user events . as follow :

    ```ts
    import { Directive, ElementRef, HostListener, OnInit, Renderer2 } from '@angular/core';
    
    @Directive({
      selector: '[appBetterHighlight]'
    })
    export class BetterHighlightDirective implements OnInit{
    
      constructor(private elRef:ElementRef , private renderer:Renderer2) { }
    
      ngOnInit(){
      }
    
      @HostListener('mouseenter') mouseover(eventData:Event){
        this.renderer.setStyle(this.elRef.nativeElement,'background-color','blue')
      }
      @HostListener('mouseleave') mouseleave(eventData:Event){
        this.renderer.setStyle(this.elRef.nativeElement,'background-color','red')
      }
      //  inside html just set it as before .
        <p appBetterHighlight > Style me with better Directive ! </p>
    
    ```

    * There is another way to working with element inside directive using HostBinding . used if we need to bind this to some property which value will become important, HostBinding tells  Angular is on the element this directive sits, please access the style , then using this bind property inside HostListener instead of renderer . (use HostBinding instead of renderer  )

    ```ts 
    @HostBinding('style.backgroundColor') backgroundColor :string ='transparent'
    
    @HostListener('mouseenter') mouseover(eventData:Event){
        // this.renderer.setStyle(this.elRef.nativeElement,'background-color','blue')
        this.backgroundColor="blue"
      }
    @HostListener('mouseleave') mouseleave(eventData:Event){
        // this.renderer.setStyle(this.elRef.nativeElement,'background-color','red')
        this.backgroundColor="red"
    
      }
    ```

    but there is thing , the developer using this directive should be able to dynamically set the value. so we can use custom property binding (inputs) get the value from where directive is used like this : 

    ```ts
    export class BetterHighlightDirective implements OnInit{
      @Input() defaultColor :string= 'transparent'
      @Input() highlightColor :string= 'blue'
    
      @HostBinding('style.backgroundColor') backgroundColor:string;
      constructor(private elRef:ElementRef , private renderer:Renderer2) { }
    
      ngOnInit(){
        // this.renderer.setStyle(this.elRef.nativeElement,'background-color','blue')
        this.backgroundColor=this.defaultColor ;     //here we initilize it 
      }
    
      @HostListener('mouseenter') mouseover(eventData:Event){
        // this.renderer.setStyle(this.elRef.nativeElement,'background-color','blue')
        this.backgroundColor=this.highlightColor;       // here will use property binding                                                        value 
      }
      @HostListener('mouseleave') mouseleave(eventData:Event){
        // this.renderer.setStyle(this.elRef.nativeElement,'background-color','transparent')
        this.backgroundColor=this.defaultColor;// here will use property binding                                                        value 
    
      }
    }
    ```

    ```html
          <p appBetterHighlight [defaultColor]="'yellow'" [highlightColor]="'red'" > Style me with better Directive !</p>        //here we put the color  we need 
                                         //notice that the color must between '' 
    
    ```

    * structural directives with that star actually are just a nicer way for us to use them basically ,Angular will transform them into something else because there is no star in Angular syntax  . *ngIf on directive is equal as ng-template as follow : 

      

    ```html
     <div *ngIf="!onlyOdd">
              <li
              class="list-group-item"
              *ngFor="let even of evenNumbers"
              [ngClass]="{odd: even%2!==0}"
              [ngStyle]="{backgroundColor: even%2!==0 ? 'yellow' : 'transparent' }"
              > {{even}}
            </li>
            </div>
            
            
            /// equal to :
            
            
            <ng-template [ngIf]="!onlyOdd">
            <div>
              <li
              class="list-group-item"
              *ngFor="let even of evenNumbers"
              [ngClass]="{odd: even%2!==0}"
              [ngStyle]="{backgroundColor: even%2!==0 ? 'yellow' : 'transparent' }"
              > {{even}}
            </li>
    ```

    * implement own structure directive like (*ngIf) we will name unless .

      ```tsx
      import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';
      
      @Directive({
        selector: '[appUnless]'
      })
      export class UnlessDirective {
      
        @Input() set appUnless(condition : boolean ){   //must the same                                                       name of selector 
          if(! condition){
            this.vcRef.createEmbeddedView(this.templateRef)
          }else{
            this.vcRef.clear();
          }
        }
        constructor(private templateRef:TemplateRef<any> , private vcRef:ViewContainerRef) { }
      
      }
      ```

      ```html
      //instead of write two ngif we put this 
      <!-- <ul class="list-group">
              <div *ngIf="onlyOdd">
                <li
                class="list-group-item"
                *ngFor="let odd of oddNumbers"
                [ngClass]="{odd: odd%2!==0}"
                [ngStyle]="{backgroundColor: odd%2!==0 ? 'yellow' : 'transparent' }"
                > {{odd}}
              </li>
              </div>
          
            </ul>
            <ul class="list-group">
              <div *ngIf="!onlyOdd">
                <li
                class="list-group-item"
                *ngFor="let even of evenNumbers"
                [ngClass]="{odd: even%2!==0}"
                [ngStyle]="{backgroundColor: even%2!==0 ? 'yellow' : 'transparent' }"
                > {{even}}
              </li>
              </div>
              <ng-template [ngIf]="!onlyOdd">
              <div>
                <li
                class="list-group-item"
                *ngFor="let even of evenNumbers"
                [ngClass]="{odd: even%2!==0}"
                [ngStyle]="{backgroundColor: even%2!==0 ? 'yellow' : 'transparent' }"
                > {{even}}
              </li>
                
              </div>
              </ng-template>
            </ul> -->
            <div *appUnless="onlyOdd">        //we use custom structural                                                   directive 
              <li
              class="list-group-item"
              *ngFor="let even of evenNumbers"
              [ngClass]="{odd: even%2!==0}"
              [ngStyle]="{backgroundColor: even%2!==0 ? 'yellow' : 'transparent' }"
              > {{even}}
            </li>
      ```

      * built in ngSwitch  

        ```
        inside ts :  
          value=10;
        inside html :
        <div [ngSwitch]="value">
          <p *ngSwitchCase="5"> Value is 5</p>
          <p  *ngSwitchCase="10"> Value is 10</p>
          <p *ngSwitchCase="100"> Value is 100</p>
          <p *ngSwitchDefault> Value is Defualt</p>
        </div>
        ```

        * course-project : 

           we want to add directive for dropdown ,  and want to add some functionality to this directive  which allows us to add a certain CSS class to the element it.                                     so once this element the directive sits on is clicked and removes the class once we click again let's say.(dropdown)  implementing such a method which basically listens to clicks and then toggles some property  . the class we need to attach. in recipe-detail there is aclass called btn-group  . we can add open css class (btn-group open) will open the dropdown .(so once click we added this open class css)

```ts
 import { Directive, HostBinding, HostListener } from "@angular/core";


@Directive({
    selector: '[appDropdown]'
})
export class DropdownDrective{
@HostBinding('class.open') isOpen = false ; 

@HostListener('click') toogleOpen(){
    this.isOpen=!this.isOpen
}

}
```

​                    

```html
//inside recipe-detail (inside group button )
  <div appDropdown class="btn-group ">  //here
//inside header in list group
   <li  appDropdown class="dropdown">    //here
```

​         //   Closing the Dropdown From Anywhere   we can edit like this :

​               

```tsx
import { Directive, ElementRef, HostBinding, HostListener } from "@angular/core";


@Directive({
    selector: '[appDropdown]'
})
export class DropdownDrective{
@HostBinding('class.open') isOpen = false ; 

@HostListener('document:click',['$event']) toogleOpen(event: Event){
    this.isOpen = this.elRef.nativeElement.contains(event.target) ? !this.isOpen : false;}

constructor(private elRef: ElementRef) {}
}
```

*  SECTION 9 : USING SERVICES AND DEPENDENCY INJECTION : 

  ![](/home/duaa/Pictures/s25.png)

   ** service does not has decorator it just a ts class . 

  

dependency injector  : new account component depends on the loggingService because we want to call a method then dependency injector simply injects this dependency, injects an instance of this class into our component automatically. Angular  response to initialize the dependency . we inject dependency inside constructor + added this service inside providers array inside component decorator . 

```ts
//servive class
export class LoggingService {
    logStatusChange(status:string){
        console.log('A server status changed, new status: ' + status);

    }
}


//component inject thsi service 
@Component({
  selector: 'app-account',
  templateUrl: './account.component.html',
  styleUrls: ['./account.component.css'],
  providers:[LoggingService]           //here
})
export class AccountComponent {
  @Input() account: {name: string, status: string};
  @Input() id: number;
  @Output() statusChanged = new EventEmitter<{id: number, newStatus: string}>();

   constructor(private loggingService:LoggingService){}   //here

   onSetTo(status: string) {
    this.statusChanged.emit({id: this.id, newStatus: status});
   this.loggingService.logStatusChange(status)  }          //here
}


```



 if we have a child of the app component, if we provide service it on that child, all the children of this child will have the same instance and the child itself but not the app component. The instances don't propagate up they only go down  that tree of components

![](/home/duaa/Pictures/s26.png)

//instead of set the action inside parent component and the output inside child  we put the action and list inside service and we inject this service inside parent (inside providers and constructor ) and if we need to use the same instance we don't put the service inside providers array inside child components . ( i.e : the child gives the parent data using output(event binding ) it emit event    the parent create action inside this action the parent fill array and gives data array to another child : instead of this approach  we create a service and inject this service in parent and 2 child but we need one instance so we put this service inside parent provider list only  , and inside service we have array and functions and inside parent we create array and initialize it from service array and inside childs we use this service and inside child we remove the output an emit function and use the service also we remove the event binding inside parent html  ) this gives the same results. )

```
//inside service : 
export class AccountsService {
    accounts = [
        {
          name: 'Master Account',
          status: 'active'
        },
        {
          name: 'Testaccount',
          status: 'inactive'
        },
        {
          name: 'Hidden Account',
          status: 'unknown'
        }
      ];
     
  addAccount(name:string,status:string){
    this.accounts.push({name:name,status:status});
  }   
  
  updateAccount(id:number,status:string){
    this.accounts[id].status = status;

  }
```

```
//inside parent : 
import { Component, OnInit } from '@angular/core';
import { AccountsService } from './accounts.service';

@Component({
  selector: 'app-root',  
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
  providers:[AccountsService]          //here
})
export class AppComponent implements OnInit {
 accounts:{name:string ,status:string}[]=[] ;    //here

 constructor(private accountsService: AccountsService){}

 ngOnInit(){
   this.accounts=this.accountsService.accounts ;
 }
 
}

```

```
//inside child : 
import { Component, EventEmitter, Input, Output } from '@angular/core';
import { AccountsService } from '../accounts.service';
import { LoggingService } from '../logging.service';

@Component({
  selector: 'app-account',
  templateUrl: './account.component.html',
  styleUrls: ['./account.component.css'],
  providers:[LoggingService]
})
export class AccountComponent {
  @Input() account: {name: string, status: string};
  @Input() id: number;
  // @Output() statusChanged = new EventEmitter<{id: number, newStatus: string}>();

   constructor(private loggingService:LoggingService , private accountsService:AccountsService){}

   onSetTo(status: string) {
    // this.statusChanged.emit({id: this.id, newStatus: status});
    this.accountsService.updateAccount(this.id ,status);
    this.loggingService.logStatusChange(status)  }
}
```

```
//inisde another child : 
import { Component, EventEmitter, Output } from '@angular/core';
import { AccountsService } from '../accounts.service';
import { LoggingService } from '../logging.service';

@Component({
  selector: 'app-new-account',
  templateUrl: './new-account.component.html',
  styleUrls: ['./new-account.component.css'],
  providers:[LoggingService]
})
export class NewAccountComponent {
  // @Output() accountAdded = new EventEmitter<{name: string, status: string}>();

  constructor(private loggingService:LoggingService , private accountsService:AccountsService){}

  onCreateAccount(accountName: string, accountStatus: string) {
    // this.accountAdded.emit({
    //   name: accountName,
    //   status: accountStatus
    // });
    // co`
```

// but if we put the service inside providers array inside app module -> application receives the same instance of the service unless it overrides it as we did before. 

//if we inject service inside a nother service we must tell angular (using decoratore ) , we must put @Injectable on t service  is injectable or that something(another service ) can be injected in there. but it prefer to only added If you expect to get something injected.

```
// in app-module 
  providers: [AccountsService,LoggingService]
// in account service :
 import { Injectable } from "@angular/core";
import { LoggingService } from "./logging.service";

@Injectable()
export class AccountsService {
    accounts = [
        {
          name: 'Master Account',
          status: 'active'
        },
        {
          name: 'Testaccount',
          status: 'inactive'
        },
        {
          name: 'Hidden Account',
          status: 'unknown'
        }
      ];
     
  constructor (private loggingService :LoggingService)  {}  

  addAccount(name:string,status:string){
    this.accounts.push({name:name,status:status});
    this.loggingService.logStatusChange(status);
  }   
  
  updateAccount(id:number,status:string){
    this.accounts[id].status = status;
    this.loggingService.logStatusChange(status);

  }
}		

```

​	Note : you don't have to build these complex output input chains where you pass events and properties to get data from component A to component B

//------> cross-component communication through a service with the event emitter  :  we want to provide some event inside service which we can trigger in one component and listen to in another. I do have cross-component communication through a service with the event emitter  so the event emitter lives in our service (emit the event in component (emit ) and listen to it in other (subscribe) ) .  we're communicating between components through a service which really can save you a lot of time 

//------> Instead of adding a service class to the `providers[]` array in `AppModule` , you can set the following config in `@Injectable()` :

```
@Injectable({providedIn: 'root'}) export class MyService { ... }
```

This is exactly the same as:inte

```
export class MyService { ... }
```

and

```
import { MyService } from './path/to/my.service'; @NgModule({    ...    providers: [MyService]})export class AppModule { ... }
```

Using this new syntax is **completely optional**, the traditional syntax (using `providers[]` ) will still work. The "new syntax" does offer one advantage though: Services **can be loaded lazily** by Angular (behind the scenes) and redundant code can be removed  automatically. This can lead to a better performance and loading speed - though this really only kicks in for bigger services and apps in  general.

-----> assignment 5 :practice services . 

- -----> course projec t :

- 1- create 2 service RecipeService and ShoppingListService .

  2- inside  RecipeService we put the recipeList(from the recipe-list component ) andefine these methods :

  ​	getRecipe : return recipe but using slice() , because we dont need any class change this list so return copy of                    						this list using slice .

   3-

  put RecipeService in provider of recipesComponent (which their child will use the same instance that it use )

    4- before :  first recipe-item give his parent (recipe-list) the recipe using event (output) . then recipe-list give his parent(recipes) this recipe using event (output). then recipes give his child(recipe-detail) this recipe using property binding (input)  . after : we will use cross-component communication (add event to servie emit in one component and listen in another(subscribe )  ,emit in recipe-item component and listen on recipes component

  because recipes gives the recipe that listen to child recipe-detail .)  

  

  // instead of input then output then input we use cross-component communication (remove the outputs add event to servie emit(the pass element  ) in one component(child which give the parent) and listen in another(subscribe ) in component that need the pass element to give to another componnet )

  // beacuse we need ShoppingListService inside recipe service ( we put it inside provider list inside app module / or put @injectable ({provided:'root'})) . 

  // instead of output(eventbinding) we use the service direct .  but when we use adddIngredient and pass the ingredient we will not notice any change on list -> sol : using event emiter ( emit the list after added(inside the service ) and listen to it where we get this list(inside one of component (parent usually))) .

    

  5-Passing Ingredients from Recipes to the Shopping List (via a Service)

```
  addIngredients (ingredients:Ingredient[]){
    //    for(let ingredient of ingredients){
    //        this.addIngredient(ingredient)
    //    }  // this will take several emit (to update list) insted add all then emit 
              // spread our ingredients into a list of single ingredients which are now pushed without

    }
```

* CHANGING PAGES WITH ROUTING : 

  In our app, we got three sections:

  - Home
  - Servers
    - View and Edit Servers
    - A Service is used to load and update Servers
  - Users
    - View Users

  This app will be improved by adding routing but definitely feel free to play around with it - besides routing, everything should be working fine.

1-  Setting up and Loading Routes  :   first we should define the routes in apll module  (path: which path should rendered  and component(which component should displayed ) ) // to register the routes that we defined in RouterModule.forRoot(   ). in app component we use router-outlet 

```
//inside //app-module : 
const appRoutes : Routes=[
{path:'',component: HomeComponent },
{path:'users',component: UserComponent },
{path:'servers',component: ServersComponent }
]

 imports: [
    BrowserModule,
    FormsModule,
    RouterModule.forRoot(appRoutes)      //here to register our routes
  ],
  
//inside app html (instead of call 3 child component we put the following).
 //instead of this : 
 <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <app-home></app-home>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <app-users></app-users>
    </div>
  </div>
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <app-servers></app-servers>
    </div>
  </div>
</div>

//we put this : 
 <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <router-outlet></router-outlet>
    </div>
</div>

```



** like we crach into parts ( parents component (routes)) and each parent has child component 

2-  Navigating with Router Links  : 

inside app html there are roe containe list of Home/server/users  for each one we navigate with router link using href="/users" inside < a> i.e : <a href="/servers" , but this will refresh the app with every link we click . That however is not the best behavior because it means it restarts our app on every navigation , we must not use href but use special directive that angular gives us which is routerLink  either by passing a string or this array which allows us to define our individual path elements this will not reload the page . 

```
// inside app html : 
<div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <ul class="nav nav-tabs">
        <li role="presentation" class="active"><a routerLink="/">Home</a></li>
        <li role="presentation"><a routerLink="/servers">Servers</a></li>
        <li role="presentation"><a [routerLink]="['/users']">Users</a></li>
      </ul>
    </div>
  </div>
```

* we must put /servers : this mean base route then servers  as localhost:4200/servers . but if we but servers without slash inside routes this will means  localhost:4200/servers/servers  but if we use without slsh inside app then it will be localhost:4200/servers (beacause we are in base path ) . so always used /servers (with slash) if we want it and if we are in base path we it still working without or with slash .

​     *we can use routerLinkActive (if click active it ) but empty path segment is part of all paths(it will be active     always , the solution is to use routerLinkActiveOptions for empty Router path ), like  this : 

```
 <ul class="nav nav-tabs">
        <li role="presentation"
        routerLinkActive="active"
        [routerLinkActiveOptions]="{exact:true}"
        ><a routerLink="/">Home</a></li>

        <li role="presentation"
        routerLinkActive="active"
        ><a routerLink="/servers">Servers</a></li>
        
        <li role="presentation"
        routerLinkActive="active"
        ><a [routerLink]="['/users']">Users</a></li>
      </ul>
```

*Navigating programmitcally : navigate from component to router path using router class . if we put button inside home component then this buttun navigate to the server Route . 

```
//inside home html :
<button class="btn btn-primary" (click)="onLoadServers()" > Load Servers</button> 
//inside home ts : 
export class HomeComponent implements OnInit {

  constructor( private router:Router) { }      //here

  ngOnInit() {
  }

  onLoadServers(){
   this.router.navigate(['/servers']);      //here
  }
}

```

// note : navigate method  doesn't know on which route you are currently ( so using / or without it still working )  but The ''routerLink'' always knows in which component , but in navigate we can tell in second parameter the object of parameter which include ''relativeTo'' with ''ActivatedRoute'' class from angular



* Passing Parameters to Routes : 

  we can add parameters to our routes, dynamic segments in our paths. 'users/:id' we are able to load a component, the user component with this dynamic piece sent so /:id is indeed interpreted as dynamic, 

```
 //inside app-module :
 {path:'users/:id/:name ',component: UserComponent },
```

​          

* Fetching Route Parameters :  using in component that used in route . and using ''ActivatedRoute''  by this.route.snapshot.params['id'] to get the param .  

```
// inside UserComponent 
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor( private route : ActivatedRoute) { }

ngOnInit() {
    this.user={
     id:this.route.snapshot.params['id'],
     name:this.route.snapshot.params['name']
    }
  
  //inside useer html :
   <p>User with ID {{user.id}} loaded.</p>
   <p>User name is {{user.name}}</p>

```

// if we put   http://localhost:4200/users/1/max will get this . 

![](/home/duaa/Pictures/s30.png)

// if we  put <a [routerLink]="['/users',10,'ahmad']">ahmad </a> the url will change but data will not  change ( it must reload to change it ) .  before the snapshot object is used to load data since angular doesn't really instantiate this component(we put it inside onInit) . so we can use snapshot for first initialization  .this.route.params ,Params here is an observable ,observables are a feature added by some other third-party package, not by Angular but heavily used by Angular which allow you to easily work with asynchronous tasks , this is an asynchronous task because the parameters of your currently loaded route might change at some point in the future if the user clicks this link ,So an observable is an easy way to subscribe to some event which might happen in the future, to then execute some code when it happens without having to wait for it now so  route.params it is obsevable and we can subscribed to it , and it will be executed each time the params changed . (but if params does not changes we can just use snapshot (for initialize ). ) here we need snahpshot for initialize and params as observable . 

```ts
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor( private route : ActivatedRoute) { }

  ngOnInit() {
    this.user={
     id:this.route.snapshot.params['id'],
     name:this.route.snapshot.params['name']     //here
    }
    this.route.params.                          //here
    subscribe( 
      (params:Params)=>{
        this.user.id= params['id'];
        this.user.name=params['name'];
      }
    )
  }


}

```

note : Rxjs is the package offering all these observables functionality .  ( if componant died the subscription (which is the params return from subscribe ) You don't need to unsubscribe here, Angular will handle it on ngOnDestroy : once the component destroyed we unsubscribe this subscription  )

```ts
import { Component, OnDestroy, OnInit } from '@angular/core';
import { ActivatedRoute, Params } from '@angular/router';
import { Subscription } from 'rxjs';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit ,OnDestroy {
  user: {id: number, name: string};
  paramsSubscription :Subscription
  constructor( private route : ActivatedRoute) { }

  ngOnInit() {
    this.user={
     id:this.route.snapshot.params['id'],
     name:this.route.snapshot.params['name']
    }
   this.paramsSubscription= this.route.params.
    subscribe(
      (params:Params)=>{
        this.user.id= params['id'];
        this.user.name=params['name'];
      }
    )
  }
 
  ngOnDestroy (){
    this.paramsSubscription.unsubscribe();
  }
```





*  passing  Query Parameters and Fragments :  query parameters and fragments on both the programmatical routing approach : 

  routing link : 

  ```
  <div class="list-group">
        <a
          [routerLink]="['/servers',5,'edit']"
          [queryParams]="{allowEdit: '1' }"
          fragment='loading'
           href="#"
          class="list-group-item"
          *ngFor="let server of servers">
          {{ server.name }}
        </a>
      </div>
  ```

  on click button inside component : 

  ```
  //inside home html  :
  <button class="btn btn-primary" (click)="onLoadServers(1)" > Load Servers</button> 
  //inside home ts :
   onLoadServers(id : number){
     this.router.navigate(['/servers/',id,'edit'] ,{queryParams:{allowEdit:'1'},fragment:'loading'});
    }
  ```

  * Retrieving Query Parameters and Fragments

    we can use ActivatedRoute.snapshot.queryParams / ActivatedRoute.snapshot. fragment ( but as before this in initilizing if the data not change we use it )  but if changed we can use subscription . 

     

    ```ts
     console.log(this.route.snapshot.queryParams);
        console.log(this.route.snapshot.fragment); 
        
        // or 
        this.route.queryParams.subscribe(()=>{})
    ```

    //inside Server ts : 
    
    ```ts
    export class ServerComponent implements OnInit {
      server: {id: number, name: string, status: string};
    
      constructor(private serversService: ServersService , 
                  private route : ActivatedRoute) { }
    
      ngOnInit() {
        const id=+this.route.snapshot.params['id'];//+ for return as number not string
        this.server = this.serversService.getServer(id);
        this.route.params.subscribe(
          (params:Params)=>{this.server =            this.serversService.getServer(+params['id']);
          }
        )
      }
    
    ```
    
    

* Nested (Child) Routing : when we click on servers or on users we load a brand new page It would be nicer if we would load it next to this menu 

  before we put  <router-outlet></router-outlet> inside app html to enable reload routing component inside it Now that is reserved for all our routes on the top level but but the child routes of servers need a separate outlet because they can't overwrite the parent component,

    so inside servers component html which is parent of  his childs (server component/edit server component) we need to put router-outlet This       now adds a new hook which will be used on all child routes of the route being loaded on the servers (all these child routes will be loaded in this router at the place now(router-outlet).) . 

  note :  we put router links in row /col and put the router-outlet(or children ) in row if we want render below or col inside the same row if we want next to . 

  ```ts
  //inside app modules : 
  const appRoutes : Routes=[
  {path:'',component: HomeComponent },
  {path:'users',component: UsersComponent,children:[
    {path:':id/:name',component: UserComponent }
  ] },
  {path:'servers',component: ServersComponent , children:[
    {path:':id',component: ServersComponent },
    {path:':id/edit',component :EditServerComponent}
  ] },
  
  ]
  ```

  

  ```html
  //inside servers html : 
  <div class="row">
    <div class="col-xs-12 col-sm-4">
      <div class="list-group">
        <a
          [routerLink]="['/servers',server.id]"
          [queryParams]="{allowEdit: '1' }"
          fragment='loading'
           href="#"
          class="list-group-item"
          *ngFor="let server of servers">
          {{ server.name }}
        </a>
      </div>
    </div>
    <div class="col-xs-12 col-sm-4">
      <router-outlet></router-outlet>      //here in colomn inside row (next to links)
      <!-- <button class="btn btn-primary" (click)="onReload()"> Reload</button>
      <app-edit-server></app-edit-server>
      <hr>
      <app-server></app-server> -->
    </div>
  </div>
  
  //inside users html : 
  
  <div class="row">
    <div class="col-xs-12 col-sm-4">
      <div class="list-group">
        <a
          [routerLink]="['/users', user.id , user.name]"
          href="#"
          class="list-group-item"
          *ngFor="let user of users">
          {{ user.name }}
        </a>
      </div>
    </div>
    <div class="col-xs-12 col-sm-4">
      <router-outlet></router-outlet>        //here in colomn inside row (next to links)
      <!-- <app-user></app-user> -->
    </div>
  </div>
  ```

  here we lose the information when navigate to another route so we must use  "queryParamsHandling" takes a string as a value and this could be merge, to merge our old query params with any new we might add here if we need but if we not  we put preserve which will overwrite the default behavior which to simply drop them and make sure that the old ones are kept.

  ```ts
  //inside server component : 
   onEdit(){
      this.router.navigate(['edit'],{relativeTo:this.route ,queryParamsHandling:'preserve'}) ;
    }
  
  ```

  * 404 error handling

```ts 
{path:'something',redirectTo:'/page-not-found'},
{path:'page-not-found',component:PageNotFoundComponent}
```

​          path: '**' -> this is the wildcard route which means catch all paths you don't know but it must br the last rout in the routes array 

```ts
{path:'**',component:PageNotFoundComponent}
```

note :  { path: ' ', redirectTo: '/somewhere-else' } will always works since  Angular checks if the path you entered in the URL does **start with the path** specified in the route. Of course every path starts with `''` (Important: That's no whitespace, it's simply "nothing").  To fix this behavior, you need to change the matching strategy to` "full"` :             { path: '', redirectTo: '/somewhere-else', pathMatch: 'full' }

* Outsourcing the Route Configuration : 

  make the routes in another module and put this new module to app modules in imports . inside this new we must exports the RouteModule . 

  ```ts
  //app-routing module :
  onst appRoutes : Routes=[                             //here
      {path:'',component: HomeComponent },
      {path:'users',component: UsersComponent,children:[
        {path:':id/:name',component: UserComponent }
      ] },
      {path:'servers',component: ServersComponent , children:[
        {path:':id',component: ServerComponent },
        {path:':id/edit',component :EditServerComponent}
      ] },
      {path:'**',component:PageNotFoundComponent}
      ]
      @NgModule({
          imports:[
              RouterModule.forRoot(appRoutes)      //here
          ] ,
          exports:[RouterModule]           //here
      })
  export class AppRoutingModule{
  
  }
  
  //inside app module : 
  @NgModule({
    declarations: [
      AppComponent,
      HomeComponent,
      UsersComponent,
      ServersComponent,
      UserComponent,
      EditServerComponent,
      ServerComponent,
      PageNotFoundComponent
    ],
    imports: [
      BrowserModule,
      FormsModule,
      HttpClientModule,
      AppRoutingModule                   //here 
    ],
    providers: [ServersService],
    bootstrap: [AppComponent]               
  })
  export class AppModule { }
  
  ```

  * Routing Guards(Protecting Routes) : 

    we want to use a feature built into the Angular router, running some code before the component we will use the CanActivateGuard  implements CanActivate  , canActivate method can run both asynchronously, returning an observable or a promise or synchronously  because you might have some guards which execute some code which runs completely on the client therefore it runs synchronously or you might have some code which takes a couple of seconds to finish because you use a timeout in there or you reach out to a server, so it runs asynchronously and both is possible with canActivate  

* we want to of user log in he can shoe servers tab if not navigate to home .

```
// inside auth service 
export class AuthService {
    loggedIn =false;

    isAuthenticated(){
    const promise =new Promise (
      (resolve, reject)=>{
          setTimeout(()=>{
              resolve(this.loggedIn)
          },800)
      })

        return promise ;
    }
    
    login(){
        this.loggedIn=true;
    }

    logout(){
        this.loggedIn=false;

    }

}
//inside authguard service
@Injectable()
export class AuthGuard implements CanActivate {
    constructor(private authService:AuthService,
                private router: Router){}
    canActivate(route: ActivatedRouteSnapshot,
                state:RouterStateSnapshot):Observable<boolean> | Promise<boolean> | boolean{

    return    this.authService.isAuthenticated()
        .then(
            (authenticated:boolean)=>{
                if(authenticated){
                    return true
                }else{
                    this.router.navigate(['/'])
                }
            }

        )
                }
}
```

```ts
//inside app routing : 
// determine the route we ant to protect . 
{path:'servers',canActivate:[AuthGuard],component: ServersComponent , children:[
      {path:':id',component: ServerComponent },
      {path:':id/edit',component :EditServerComponent}
    ] }

```

//if we want to protect child route (we can add for each child canActivate) but if the child are big number this not preferred (we an implement method call canActivateChild   in  the same AuthService or in a new service) 

```ts 
//inside authGaurd 
export class AuthGuard implements CanActivate ,CanActivateChild {
    constructor(private authService:AuthService,
                private router: Router){}
    canActivate(route: ActivatedRouteSnapshot,
                state:RouterStateSnapshot):Observable<boolean> | Promise<boolean> | boolean{

    return    this.authService.isAuthenticated()
        .then(
            (authenticated:boolean)=>{
                if(authenticated){
                    return true
                }else{
                    this.router.navigate(['/'])
                }
            }

        )
                }

    canActivateChild(route: ActivatedRouteSnapshot,
        state:RouterStateSnapshot):Observable<boolean> | Promise<boolean> | boolean{
            return this.canActivate(route,state);
        }           //here
```

```ts 
// inside  routing module

{path:'servers',
    // canActivate:[AuthGuard],
    canActivateChild:[AuthGuard]
    ,component: ServersComponent , 
    children:[
      {path:':id',component: ServerComponent },
      {path:':id/edit',component :EditServerComponent}
    ] },             
```

**if click update ok and navigate to last loaded server  but  maybe forgot to click update server first(here we use canDeactivate (make action before leave route . ask user if really want to leave ))

```ts
//inside server edit ts : 
 changesSaved=false ;
 ...
 
  onUpdateServer() {
    this.serversService.updateServer(this.server.id, {name: this.serverName, status: this.serverStatus});
    this.changesSaved=true; //here
    this.router.navigate(['../'],{relativeTo:this.route}) //here

  }

```

```

export interface CanComponentDeactivate{
    canDeactivate:()=> Observable <boolean> | Promise<boolean> | boolean ;
}

export class CanDeactivateGuard implements CanDeactivate<CanComponentDeactivate>{
 canDeactivate(component:CanComponentDeactivate,
               currentRoute : ActivatedRouteSnapshot,
               currentState : RouterStateSnapshot,
               nextState?:RouterStateSnapshot):Observable <boolean> | Promise<boolean> | boolean 
            {
           return component.canDeactivate();
               }
}
```

```ts
// inside routing-module 
 {path:'servers',
    // canActivate:[AuthGuard],
    canActivateChild:[AuthGuard]
    ,component: ServersComponent , 
    children:[
      {path:':id',component: ServerComponent },
      {path:':id/edit',component :EditServerComponent,canDeactivate:[CanDeactivateGuard]}                                                                                    //here 
    ] },
```

```ts 
// inside EditServerComponent
 canDeactivate():Observable <boolean> | Promise<boolean> | boolean {
    if(!this.allowEdit){
      return true ;
    }
    if ((this.serverName!==this.server.name ||this.serverStatus!== this.server.status)&&!this.changesSaved){
      return confirm('Do you want to discard Changes ?')
    }else {
      return true ;
    }
  }
```

* Passing Static Data to a Route :

  

```
 {path:'not-found' ,component:ErrorPageComponent,data:{message:'page ot found'}},

```

```
export class ErrorPageComponent implements OnInit {

  errorMessage : string
  constructor(private route: ActivatedRoute) { 
  }

  ngOnInit(): void {
    this.route.data.subscribe(
      (data:Data)=>{this.errorMessage=data['message']}
    )
  }

}

```

```
<p>{{errorMessage}}</p>
```

*  Resolving Dynamic Data with the resolve Guard

​    if we have some dynamic data we have to fetch before a route can be displayed or can be rendered.   we need resolver will allow us to run some code  before a route is rendered , the difference to canActivate is that the resolver will not decide whether this route should be rendered or not, whether the component should be loaded or not

 , the resolver will always render the component in the end but it will do some pre-loading(fetch some data the component will then need later on.) berfor (Of course the alternative is to render the component or the target page instantly and in the onInit method of this page, you could then fetch the data and display some spinner whilst you are doing so as we do before  ) but if you want to load it before actually displaying the route, this is you would add such a resolver.



// if we want to get the servers before render the route  for server Component .  

```ts 
// 1 create rsolver service 
interface Server {    this data that need to fetch
    id: number ;
    name : string ;
    status : string ;
}
@Injectable()
export class ServerResolver implements Resolve <Server >{
 
    constructor ( private serversService :ServersService){}
    
    resolve(route:ActivatedRouteSnapshot , state :RouterStateSnapshot): 
    Observable<Server> | Promise<Server> | Server {  //pass the data that need to                                                              fetch
        return this.serversService.getServer(+route.params['id']);
    }
}
```



```ts
// 2- put resolver in to params inside route : 
   {path:':id',component: ServerComponent ,resolve:{server:ServerResolver}},  // this resolver gives us back and remember, it gives us back some data with this resolve method and save it inside server property

```



```ts
3- //inside server component (instead of get data after in ngOnInit  using params we use the resolver using this.route.data.subscribe ): 

ngOnInit() {
    this.route.data.subscribe(
      (data:Data)=>{this.server=data['server']}
    );
    // const id=+this.route.snapshot.params['id'];
    // this.server = this.serversService.getServer(id);
    // this.route.params.subscribe(
    //   (params:Params)=>{this.server = this.serversService.getServer(+params['id']);
    //   }
    // )
```

COURSE PROJECT :

before we implemented the navigation in our application with ngIf though and that is not really the best way of navigating around (select recipes/shopping list) , we will also add one new component, the recipe-edit component to create new recipes or edit existing ones

![](/home/duaa/Pictures/s49.png)

1- Setting up routes :

```html
//1-  create app routing 
const appRoutes: Routes = [
  {path:'' , redirectTo :'/recipes' , pathMatch: 'full'} , 
  {path:'recipes' , component :RecipesComponent} ,
  {path:'shopping-list' , component :ShoppingListComponent}

];

@NgModule({
  imports: [RouterModule.forRoot(appRoutes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }

***********************************************************
//2- inside app-html : 
//instead of the tag of childs we put router-outlet and later we added links to them . 
<div class="container">
<div class="row">
  <div class="col-md-12">
    <!-- <app-recipes *ngIf="loadedFeature==='recipe'"></app-recipes>
    <app-shopping-list *ngIf="loadedFeature!=='recipe'"></app-shopping-list> -->
    <router-outlet></router-outlet>
  </div>
</div>

```

2- adding Navigation to the App  (links :)

```html
// instead of href and click onSelected event we remove them also featureSelected eventEmiiter (output ) and using router link  instead .  

  <!-- <li><a href="#" (click)="onSelect('recipe')">Recipes</a></li>
  <li><a href="#"(click)="onSelect('shopping-list')">ShoppingList</a></li> -->

   <li><a routerLink="/recipes">Recipes</a></li>
  <li><a routerLink="/shopping-list">ShoppingList</a></li>

```

  3- Marking active route : 

```html
// if click active it . 
 <li  routerLinkActive="active"
                 > <a  routerLink="/recipes">Recipes</a></li>
                <li  routerLinkActive="active" ><a routerLink="/shopping-list">ShoppingList</a></li>
```

 4- Fixing Page Reload issues : 

each href=# will reload the app . so we must remove it and also add (cursor=pointer if we need to put pointer whn we above click ) .

 

5- adding child route : 

we add new component called recipe-start   (added recipe start and rrecipe detail as childe of recipes component ) and instead of calling tag recipe-detail . we call router-outlet in side recipes html .

```ts
//inside app routing:
const appRoutes: Routes = [
  {path:'' , redirectTo :'/recipes' , pathMatch: 'full'} , 
  {path:'recipes' , component :RecipesComponent , children : [
    {path:'' , component : RecipeStartComponent},
    {path:':id', component:RecipeDetailComponent}
  ]} ,
  {path:'shopping-list' , component :ShoppingListComponent}

];
```



```html
//inside recipes html : 
<div class="row">
    <div class="col-md-5">
        <app-recipe-list ></app-recipe-list>
    </div>
    <div class="col-md-7">
        <!-- <app-recipe-detail
        *ngIf="selectedRecipe ; else infoText"
        [recipe]="selectedRecipe"> </app-recipe-detail>

        <ng-template #infoText>
            <p>Please select a Recipe !</p>
        </ng-template> -->
        <router-outlet></router-outlet>
    </div>
</div>
```

3-

we use input to get the recipe that selected in recipe-detail  we want change how we receive the recipe here, how we set the recipe and we can change it ( by read the id that we define in route )

```
// 
  recipe :Recipe ;
  constructor(private recipeService:RecipeService , 
              private route : ActivatedRoute) { }

  ngOnInit(): void {
     this.route.params.subscribe(
       (params:Params )=> { 
         this.recipe =this.recipeService.getRecipe(+params['id'])}
     );
  }

```

4- 

when click recipe item we want to route to route to recipe detail ( we put index just beacause                                        we are inside (/recipes)) so it will be recipes/1 .. .  

```
//inside recipe list html ( pass the index) 
 <app-recipe-item 
        *ngFor="let recipeEl of recipes ;let i= index" 
        [recipe]="recipeEl"
        [index]= "i"
  ></app-recipe-item>
  
 // inside recipe item ts :  
  @Input () index :number
  
  // inside recipe item html  : 
   style="cursor: pointer;"
         [routerLink] = "[index]"      //route to recipe detail ( we put index just beacause                                        we are inside (/recipes)) so it will be recipes/1 ... 
         class="list-group-item clearfix"
```

5- add recipe-edit component and added new routes .  addd route to (New Recipe and edit recipe  ) . 

```ts
//inside routing-ts
{path:'recipes' , component :RecipesComponent , children : [
    {path:'' , component : RecipeStartComponent},
    {path:'new' , component : RecipeEditComponent},
    {path:':id', component:RecipeDetailComponent} ,
    {path:':id/edit' , component : RecipeEditComponent}
  ]} ,
  
 
```

```ts
//inside recipe-detail  html : 
 <li><a style="cursor: pointer;" (click)="onEditRecipe()">Edit Recipe</a></li>
     
//inside recipe-detail ts  :
 onEditRecipe() { 
  this.router.navigate(['edit'],{relativeTo:this.route}) //since we are
                                                       //  in recipes/id(we have id we dont need to pass it )
  }      // we can use this complex :  this.router.navigate(['../,this.id ,'edit'],{relativeTo:this.route})

```

```html
// inside recipe-list html : 
 <div class="col-xs-12">
        <button class="btn btn-success" (click)="onNewRecipe()">New Recipe</button>
    </div>

// inside recipe-list ts  :
  onNewRecipe(){
    this.router.navigate(['new'],{relativeTo:this.route})
  }
```

* Observable : 

  Now in our Angular project, an observable basically just is an object we import from a third-party package (RxJS),So the observable could emit data because you trigger it to do so,it could be connected to a button and therefore whenever the button is clicked, an event in a data package is emitted automatically or as the Angular HTTP service does it, . Observer this his actually is your code you could say. It's the subscribe function you saw earlier or at least it.  

  There, you have three ways of handling data packages :

  of course you use it to handle asynchronous tasks because all these data sources here, user events ,triggered in your code or a HTTP request are asynchronous tasks, you don't know when they will happen and how long it does it take . So if you execute your normal application code, you don't want to wait for these events or you don't want to wait for the completion of such a HTTP request because that would block your program, would block .Therefore, we need methods of handling such asynchronous tasks and historically you might have used callbacks or promises

  ![](/home/duaa/Pictures/s50.png)

  

   // inside project : 

when we use route(ActivatedRoute ).params .  params here is an observable to which we subscribe . observables are that stream of data and whenever a new data piece is emitted, our subscription will know about it. params is an observable its stream of route parameters   that stream gives us a new route parameter whenever we go to . angular use thers built in observable and  you only subscribe to them, you don't need to create them but to understand them, it certainly doesn't

 *build new own observable :   we import interval from RXJS . , we have interval which will fire a new value every second and in this function here, IF WE DONT SUBSCRIBE  if that keeps on emitting whilst you're not interested in it anymore, you should unsubscribe from any observable in which values you are no longer interested and that's really important because before we do that, and of course we can repeat that. We get more and more of observables counting and that of course is verybad.If that happens behind the scenes, you quickly run out of resources and you slow down your app, you introduce a memory leak here because your memory gets occupied a lot by data you don't need.

BUT THE BUILT IN THAT ANGULAR USE THEM WE DONT NEED TO UNSUBSCRIBE The answer simply is Angular does that for you. For the observables provided by Angular, like params. 

```ts
//inside homecocmponent : 
export class HomeComponent implements OnInit ,OnDestroy{

  private firtsObsSubscription :Subscription ; 
  constructor() { }

  ngOnInit() { 
 this.firtsObsSubscription= interval(1000).subscribe(count=>{console.log(count)});
  }

  ngOnDestroy(){
    this.firtsObsSubscription.unsubscribe();
  }

}
```

*we can create Observable from Observable . and make observer inside it and we can (observer.next (the next emit value) OR observer.complete() to finish emmiting we needed in HTTP after finished  Or observer.error to throw error it cancle the observer not complete it   )  . then subscribe the observale we created it and it take 3 args ( the data , the error , the complete message  ) . theh code inside Observable understanding section .

* operators using pip from rxjs/operators like(map ,filter ) .

* subject : event emmiter ..... 

  ![](/home/duaa/Pictures/s51.png)

*  Course project : we can replace event emiter with subject . 

  inside shopping-list there is an event Emitter for emit changed in the list of ingredients . we will replace it with subject . instead event emitter we put subject and instead of emit we call next  and we already subscribe to it . it prefer to store subscription in a property and on destroy unsubscribe from it 

  

* Forms : 

   Angular's job now is to allow you to retrieve the values the user , and also to check some other things, like is the form valid, did the user enter valid information . 

  ![](/home/duaa/Pictures/form1.png)

 Angular actually offers two approaches when it comes to handling forms.

![](/home/duaa/Pictures/form2.png)

```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <form>
        <div id="user-data">
          <div class="form-group">
            <label for="username">Username</label>
            <input type="text" id="username" class="form-control">
          </div>
          <button class="btn btn-default" type="button">Suggest an Username</button>
          <div class="form-group">
            <label for="email">Mail</label>
            <input type="email" id="email" class="form-control">
          </div>
        </div>
        <div class="form-group">
          <label for="secret">Secret Questions</label>
          <select id="secret" class="form-control">
            <option value="pet">Your first Pet?</option>
            <option value="teacher">Your first teacher?</option>
          </select>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
    </div>
  </div>
</div>

```

in this form there is no action put because we  don't want a HTTP request to be the result of me clicking the submit button, instead Angular should handle this form and therefore, I don't have an action on it. Angular infers such forms, create such a Javascript object for us as it does when using the template , we must omport fomsModule in appModule so With this imported, Angular will actually automatically create a form for you, so a Javascript representations of the form when it detects a form element in HTML code  that form element serving as a selector for some Angular directive, which then creates such a Javascript representation of the form for you. you can't see that form representation but one thing does not happen automatically, Angular will not automatically detect your inputs in this form because not every input in your HTML code might be a control you want to have in your Javascript form so we must tell angular to which controls do we want to have . This will be enough to tell Angular, hey this input is actually a control of my form, so ngModel  is a directive made available in the forms module **ngModel** (without square bracket  ) . ngModel plus name attribute(which is normal html attribute .) then  we can see these key-value pairs representing what the user entered into which input  . 

//in default js and html each element (button/input) ,If you have a button in a form element, this button will submit the form, will send a request normally the submit event that's built into Javascript, built into HTML but  angular takes advantage of this and gives a directive  we can place on this form element as a whole, it is called **ngSubmit** and it actually only gives us one event we can listen to, This event made available by the ngSubmit directive will be fired whenever this form is submitted, and to access the form element we must put local reference like  **#f**  . to expose some data we can fetch here on this form element we assign value to this ref element which is ngForm  #f=ngForm  this tells Angular to give us access to this form we  created automatically. then pass this ref to method (ngSubmit)=onSubmit(f) and inside ts it will be of type **NgForm** . this form object that the angular created for us  has many property one of them called **value** which object of key an value pairs of the names of the controls that we added   . also there is a property called **controls** contains the controllers that we add **ngModel** to it with their names  and for each control there are a properties like **dirty** , **enable** ,**disable**  ,**error**  . dirty will be true if we change or fill the form then submit but if we dint fill it it will be false .  **invalid** is false because we haven't added any validators

```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <form (ngSubmit)="onSubmit(f)" #f="ngForm">   //here
        <div id="user-data">
          <div class="form-group" >
            <label for="username">Username</label>
            <input 
            type="text" 
            id="username" 
            class="form-control"
            ngModel              //here
            name="username"       //here
            >
          </div>
          <button class="btn btn-default" type="button">Suggest an Username</button>
          <div class="form-group">
            <label for="email">Mail</label>
            <input 
            type="email"
             id="email" 
             class="form-control"
             ngModel       //here
             name="email"  //here
             > 
          </div>
        </div>
        <div class="form-group">
          <label for="secret">Secret Questions</label>
          <select 
          id="secret" 
          class="form-control"
          ngModel          //here
          name="secret"   //here
          >
            <option value="pet">Your first Pet?</option>
            <option value="teacher">Your first teacher?</option>
          </select>
        </div>
        <button class="btn btn-primary" type="submit">Submit</button>
      </form>
    </div>
  </div>
</div>

```

```
//inside ts : 
 onSubmit(form:NgForm){
    console.log(form) ;
  }
```

// another way of getting access to the form in our TypeScript is to used @ViewChild  . without pass it to method we can read it as viewChild .  

```html
//inside html : 
      <form (ngSubmit)="onSubmit()" #f="ngForm"> // without pass the element

```

```tsx
//inside ts : 
  @ViewChild('f') submittedForm :NgForm ;
 onSubmit(){
  console.log(this.submittedForm) ;
  }

```

* Adding Validation to check User Input :  we can make the validation in server side but also we can do it in client side  

    want to make sure that none of the fields here is empty and that the e-mail address actually is a valid e-mail address.

  there are built in html ***directive*** like **required**  ,it is act as a selector for a built-in directive shipping with Angular and it will automatically configure.

  there is an build in ***validators*** like **email** ,  An e-mail is simply another directive made available by Angular . if it is not valid the valid attribute will be false   angualr will add to controller   ng-dirty ng-touched ng-valid or ng-invalid .

  // built-in validators link : https://angular.io/api/forms/Validators  ((and which you later can add when using the reactive approach)

  // For the template-driven approach, we need built in  directives https://angular.io/api?type=directive

  // Additionally, you might also want to enable HTML5 validation (by default, Angular disables it). You can do so by adding the `ngNativeValidate` to a control in your template. 

* Using the form state . 

  1- like we disable the button if the form is not valid  . 

  ```html
   <button 
          class="btn btn-primary" 
          type="submit"
          [disabled]="!f.valid"       //here
          >Submit</button>
  ```

  2-  add style if invalid red it but not initial time after touched . we can use directives that angular added like 

  ng-valid / ng-touched/ng-valid ,etc ...  but we apply it not in all form we determine if it for input /button .etc ..

  ```css
  //inside css 
  input.ng-invalid.ng-touched{
    border: 1px solid red;
  }
  
  ```

  3- if we want to put as hint bellow the input we want to check if the email control is valid or not we can put reference to this control by add #email ="ngModel" so we can access this inside html .

  ```html
   <div class="form-group">
              <label for="email">Mail</label>
              <input 
              type="email"
               id="email" 
               class="form-control"
               ngModel
               name="email"
               required
               email
               #email="ngModel">
               <span class="help-block" *ngIf="!email.valid && email.touched">please enter valid email ! </span> //here 
            </div>
  ```

  4- Set Default Values with ngModel Property Binding [ngMode]="propertyDefinedIntsWithDefaultValue".

  ```html
  // ts 
    defaultQuestion="pit" //one of options
  // html 
  <div class="form-group">
            <label for="secret">Secret Questions</label>
            <select 
            id="secret" 
            class="form-control"
            [ngModel]="defaultQuestion"
            name="secret">
              <option value="pet">Your first Pet?</option>
              <option value="teacher">Your first teacher?</option>
            </select>
   </div>
  ```

  

  //we can use ngModel with no binding to tell the angular that this is a control , one way binding for example to put the first or initial value and two way binding for get value from user and output it 

  ```html
  // case3 : two way binding for get value from user and output it 
    <div class="form-group">
            <textarea
            class="form-control"
            [(ngModel)]="answer" 
            name="questionAnswer"
            row="3"
            ></textarea>
            <p> answer : {{answer}}</p>
          </div>
  ```

  * Grouping form conttrol : 
  
    if we want to group controls ( this may be needed in big forms) ,  also check the validity of this overall control and access it it with ref . 
  
    ex : we have 2 input controls (div foreach) inside dive has id=user-data  . we put for it ngModelGroup="key" this make big control has 2 controls(input controls)  and to acces it we put #ref="ngModelGroup" . 
  
     
  
    ```html
     <div id="user-data"
             ngModelGroup="userData"    //here
             #userData="ngModelGroup" >    //here
              <div class="form-group" >
                <label for="username">Username</label>
                <input 
                type="text" 
                id="username" 
                class="form-control"
                ngModel
                name="username"
                required
                >
              </div>
              <button class="btn btn-default" type="button">Suggest an Username</button>
              <div class="form-group">
                <label for="email">Mail</label>
                <input 
                type="email"
                 id="email" 
                 class="form-control"
                 ngModel
                 name="email"
                 required
                 email
                 #email="ngModel">
                 <span class="help-block" *ngIf="!email.valid && email.touched">please enter valid email ! </span>
              </div>
            </div>
            <p *ngIf="!userData.valid && userData.touched" >userdata is invalid</p> //here
    
    ```
  
    * handle radio button .
  
      

```html
<div class="radio" *ngFor="let gender of genders">
          <label>
            <input         // here for circle(radio)
            type="radio"
            ngModel
            name="gender"
            [value]="gender"
            >
            {{gender}}      //here the label next to rsfdio
          </label>
        </div>
```

* setting and patching from value 

  -> setting value : we must put all values 

  ```ts
  //inside suggest event
   suggestUserName() {
      const suggestedName = 'Superuser';
      this.signupForm.setValue({  //here 
        userData:{
          username:suggestedName,
          email:''
        },
        secret:'pet',
        questionAnswer:'',
        gender:'male'
      })            //if we dont specify one field it will not work
    }
  ```

  

​       -> patch value : overwrite specific certain controls.(better approach) 

```tsx
// we just put the suggest name only 

suggestUserName() {
    const suggestedName = 'Superuser';
    this.signupForm.form.patchValue({
      userData:{
            username:suggestedName,
      }
    })
  }
```

so setValue to set your whole form, patch value to overwrite parts of the form. 



////////////////////////////

there is no connection between the last time we ran this Angular app on this web page and the current .So there is no connection and the memory is lost, we can store them in  file system on your device but you can work with cookies or with local storage, which is an API exposed by the browser to store simple key-value pairs basically on the file system but controlled by the browser

///////////////////////////////////////////

deploy project : 

ng build --prod . this build ts classes and convers into js bundle . the generated files (build artifacts) we will deploy it into static host 
