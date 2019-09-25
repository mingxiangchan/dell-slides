### Ionic-2 
- Forms
- HTTP

+++

- Generate a demo project
  ```
    ionic start Demo2 tabs
  ```
- Generate project for exercise
  ```
    ionic start LaptopBuilder blank
  ```

---

### Tools

+++

### To view ios and android view
- `npm install @ionic/lab`
- `ionic serve --lab`
- open `localhost:8200`

---

### Laptop Builder Prototype
- Group Activity (3 per group)
- OS, CPU, Model, RAM, HDD, Graphics Card, Design

+++

- Design the app page (draw.io)
- Decide on the available options
- Find images

---

### User Input via Forms

+++

### Angular Reactive Form Module
- Add the ReactiveFormModule to the app module
- Create FormControl/ FormGroup in component/page.ts
- Create `<form>`/`<ion-input>` tags to retrieve user input

+++

### Demo: Profile Form
- Create page to display profile
- On Click Edit button, navigate to profile edit form

+++

### Exercise: LaptopBuilder - (OS)
- Create a home page
  - Has a `Build Laptop` button, on click navigates to OS selection page
- Create a OS selection form page
  - Shows `Phase 1: OS Selection` as title
  - Has a list of Operating System for User to select
  - Has `OS Notes` section for user input
  - On Footer has a Submit button to confirm selection
    - If OS not selected, Submit button is disabled  

---

### Form Wizard - Multi Page Forms

+++ 

### Demo: LaptopBuilder - (CPU)
- Use service to store component selections
- Update service with component selection on submit
- Filter selection on page based on previous option selected

+++ 

### Exercise: LaptopBuilder
- Model
  - Brand: Inspiron, Latitude, XPS
  - Description: What are you looking for?
- RAM
  - Amount of RAM per stick
  - Quantity of sticks
- HDD
  - Type: HDD, SSD
  - Storage Amount(Number Input)

+++

- Graphics Card
  - Brand: AMD, NVIDIA, Intel
  - Model Options
- Design
  - Casing Color
  - Keyboard (Mechanic/Butterfly/Backlight)
  - Notes

+++

- Customer Details
  - Shipping Address
  - Name
  - Contact
  - Email

+++

- After Design, complete laptop building and navigate back to homepage
  - display laptop created
  - on tap laptop created, navigate to laptop built

---

### Backend Integration - HTTP
- 2 options: Native HTTP vs Angular HTTP
- We'll focus on Angular HTTP

+++

### Angular HTTP
- Add HTTP Client Module to app modules
- Inject HttpClient into component
- Subscribe to request results

+++

### Demo: Pokedex
- Display list of pokemon
- On tap pokemon, display pokemon specific details

+++

### Exercise: Build your backend
You will need to provide the following APIs:
- list of available options for each form
- get all laptops
- save laptop to DB

