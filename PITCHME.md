## Assignment Review: Shopping Cart

---

#### Clone the following links and run npm install
```js
//Resume App
//To Do List
```

---

### Resume App
![resume-site](./resume.jpg)

---

### Multi Components

+++

#### Recap: Creating New Components
```bash
ng generate component <name>
```

+++

Components are arranged in HTML.

```html
<!-- app.component.html -->
<app-parent></app-parent>
```

```html
<!-- parent.component.html -->
<app-child1></app-child1>
<app-child2></app-child2>
```

+++

Parent-Child components communicate via inputs

```ts
// child.component.ts
// make sure Input is imported
import { Component, OnInit, Input } from '@angular/core'
```

```ts
// child.component.ts
@Input isHidden = false
```

```ts
// parent.component.ts
firstChildHidden = false
secondChildHidden = false
```

```html
<!-- parent.component.html -->
<app-child [isHidden]="firstChildHidden"></app-child>
<app-child [isHidden]="secondChildHidden"></app-child>
```

+++

Can render multiple of the same component with for loops

```html
<div *ngFor="let pokemon of pokemons;">
  <app-child [pokemon]="pokemon"></app-child>
</div>
```

+++

#### Exercise

1. Convert the current app to multiple components
2. Store the data at the highest parent
3. Pass the data down to each child component

---

### Passing Events From Child to Parent

+++

```js
class ChildComponent {
  @Output eventName = new EventEmitter<type>()

  // varName must be the same type specified in eventEmitter 
  methodName(varName){
    this.eventName.emit(varName)
  }
}
```

+++
```html
<!-- Parent component template -->
  <app-child (eventName)="eventHandler($event)"></app-child>
```
```js
class ParentComponent{
  eventHandler(varName){
    // The varName received is what you send in child component
  }
}
```

+++

### Exercise

1. On click `edit resume` (Which is a child component, change the information in for `About Me`)
2. Add a button to toggle navbar display as a child component of `AboutMe`
3. On click NavBar Item, change the page displayed.

+++

### Services

+++

```bash
ng generate service <name>
```

+++

- holds certain data
- can provide ways to access that data
- can provide ways to change that data
- independent of componeny hierarchy

+++

```ts
export class MiscService {
  isRed = false // data, can be accessed

  constructor() {}

  // ways to change the data
  changeToRed() {
    this.isRed = true
  }
}
```

+++

Can be injected into a component

```ts
  // firstChild.component.ts
  constructor(private miscService: MiscService)

  clickedButton() {
    this.miscService.changeToRed()
  }
```

```ts
// secondChild.component.ts
  constructor(public miscService: MiscService)
```

```html
<!-- secondChild.component.html -->
<div [style.color]="miscService.isRed"></div>
```

+++

### Exercise
1. Store the data specific to user in a UserService
2. Inject the service in to components that use User data
3. Access the User data in these components through service
4. On click edit resume, change User data in the service

---

#### Routing

+++

```ts
// app.module.ts
import { AppRoutingModule } from './app-routing.module'

// add AppRoutingModule under the existing imports
{
  imports: [BrowserModule, AppRoutingModule],
}
```

+++

```ts
// app-routing.module.ts

const routes: Routes = [
  { path: 'user/:userId', component: UserProfileComponent },
  { path: '', component: HomePageComponent },
]
// make sure you type out your component manually, and use autocomplete, so the component is imported
```

```ts
// user-profile.component.ts
import { ActivatedRoute } from '@angular/router'

constructor( private route: ActivatedRoute ) {}

ngOnInit() {
  const userId = this.route.snapshot.params.userId
  console.log(userId)
}

```

+++

### Exercise 

- Use routing to complete the following paths
  - users (show list of users)
  - users/:id/about_me
  - users/:id/resume
  - users/:id/portfolio
  - users/:id/blog
  - users/:id/contact_me
- Changing :id should show a different user's information

---

### HTTP

---

```ts
// app.module.ts
import { HttpClientModule } from '@angular/common/http'

{
  imports: [BrowserModule, AppRoutingModule, HttpClientModule],
}
```

```ts
// user.service.ts
import { HttpClient } from '@angular/common/http'

constructor(private http: HttpClient)

getUserImages(userId) {
  return this.http.get(`https://insta.nextacademy.com/api/v1/images?userId=${userId}`)
}
```

```ts
// user-profile.component.ts
constructor(private service: UserService) {}

ngOnInit() {
  const userId = const userId = this.route.snapshot.params.userId
  this.service.getUserImages(userId).subscribe(response => {
    console.log(response)
  })
}
```

+++

### Exercise
- Access data from the provided API endpoints and use the provided data to display on resume

---

### Culmination: To Do List
Using the provided ToDoList template
- Separate into 
  1. ListsIndex (Shows all the list titles, onClick navigate to ShowList)
  2. ShowList (Shows a specific list and it's todo's, onClick todo go to ShowToDo)
  3. List (Component to display a List with title and Todos)
  4. ToDo (Component to display task description, and whether it is completed)
  5. ShowToDo (Shows a specific todo)

+++

- Data must be stored in a service
- User must be able to edit the todo to be completed or not completed
- Have a button to change user viewing the list
- Different user can view different lists, or view some shared lists.