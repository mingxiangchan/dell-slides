### JS Interactivity

---

### 3 Step Process

1. target HTML element
2. set trigger (optional)
3. do JS things

---

### Target HTML Elements

```ts
// return first element
document.querySelector(".first")

// return all elements
document.querySelectorAll(".first")
```

+++

```ts
const buttons = document.querySelectorAll("button")

const form  = document.querySelector("#login-form")

---

### Set Trigger

```ts
button.addEventListener("click", e => {
  // do something here
  // the variable e is the event
});

div.addEventListener("mouseenter", e => {
  // do something here
  // the variable e is the event
});
```

+++

### List of Possible Events

- click
- mouseenter
- mouseleave
- submit
- [Complete List](https://developer.mozilla.org/en-US/docs/Web/Events)

---

### Manipulate CSS

```ts
div.style.backgroundColor = "red";
div.style.fontFamily = "Arial";
```