## Reactive Forms

+++

### A module to manage forms
- stores the form state in Component (input values, status of form, errors etc)
- form edits will update this form state
- `FormControl` for single inputs
- `FormGroup` for a group of inputs

---

## How to use Form Control: 3 Steps

+++

#### Add Module
```js
    // app.module.ts
    import { ReactiveFormsModule } from '@angular/forms';

    @NgModule({
        imports: [
            // other imports ...
            ReactiveFormsModule
        ],
    })
```

+++

#### Create FormControl in Component
```js
    // app.component.ts
    import { FormControl } from '@angular/forms';

    @Component({
        // component config
    })
    export class NameEditorComponent {
        fieldName = new FormControl('defaultData');
    }
```

+++

#### Register/ Link control to HTML input
```html
    <!-- app.component.html -->
    <input type="text" [formControl]="fieldName"/>
```

---

### Interacting with FormControl
- Access value
    ```js
        fieldName.value
    ```
- Set value
    ```js
        fieldName.setValue('Test')
    ```

+++

### Setting up field validations
```js
    fieldName = new FormControl(
        'defaultData', 
        [Validators.required]
    )
```

+++

### Getting form field errors
```js
    fieldName.errors
```

+++ 

### Retrieving Form Status
```js
    fieldName.status => string
    fieldName.invalid => boolean
    fieldName.dirty => boolean
    fieldName.touched => boolean
```

---

## How to use FormGroup: 3 Steps


+++

#### Add Module
```js
    // app.module.ts
    import { ReactiveFormsModule } from '@angular/forms';

    @NgModule({
        imports: [
            // other imports ...
            ReactiveFormsModule
        ],
    })
```

+++

#### Create FormGroup with list of FormControls in Component
```js
    // app.component.ts
    import { FormControl, FormGroup } from '@angular/forms';
    
    @Component({
        // component config
    })
    export class NameEditorComponent {
        formName = new FormGroup({
            'fieldName1': new FormControl('defaultValue1'),
            'fieldName2': new FormControl('defaultValue2')
        });
    }
```

+++

#### Register/ Link group to HTML form
```html
    <!-- app.component.html -->
    <form  [formGroup]="formName" >
        <input type="text" formControlName="fieldName1"/>
        <input type="text" formControlName="fieldName2"/>
    </form>
```

---

## Form Submission

+++
```js
    @Component({
        // component config
    })
    export class NameEditorComponent {
        onSubmit(){
            // submit function
        }
    }
```


```html
    <!-- app.component.html -->
    <form [formGroup]="profileForm" (ngSubmit)="onSubmit()">
        <!-- Form Fields -->
    </form>
```