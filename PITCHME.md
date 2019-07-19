## Recap

---

### Multi Components

+++

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

#### Exercise: Todo List

1. Create a todo list similar to trello
2. Have multiple stages (Backlog, WIP, Done, Archived)
3. The overall container contains all the tasks to be done
4. The overall container passes down a subset of tasks to each stage

---

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

#### Exercise: Todo List + Service

1. Create a service holding all the tasks in the todo list
2. Attach the service to each todos stage
3. Add a button on item that will shift the item rightwards
      - will shift `backlog` to `wip`
      - will shift `wip` to `completed`

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

#### Exercise: Todo List + Routes

1. Create a page specifically for 1 item
2. Clicking an item from the overall view will lead to this page

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
    debugger
  })
}
```
