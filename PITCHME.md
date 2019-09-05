## Node Web Apps (With Express)

---

### How the web works
- browser sends request to server
- server checks data in DB
- server sends response to browser

+++

### Responses can be 
- a web page of:
  - HTML
  - JS
  - CSS
- OR data of various types:
  - text
  - json
  - etc...

+++

<img src="https://kroki.io/mermaid/svg/eNpljUEKwjAURPc9xayF0n0W3SRRkdaCyQW-9SMBTWuS6vVNFHHRmd17DBP5sbAfWTm6BrpXyJkpJDe6mXyCBEXIm2OfVs4UZzg8OaycKk5RojNFrlCaI-u2NQI7bdEskUP8UJOpEjC609Jig-1p6PHXqv6uCkGYXr9RplJgb_uuOZjhiEt-ewPywDw6">

---

### GET Request
- used to `GET`/obtain data

+++

### Exercise: Make a GET Request with Postman

```bash
# url
https://script.google.com/macros/s/AKfycbxFHnzXZn95MraVopLjA5Rfx5JInmuJ105yJpQ4EuyNEvG29tt3/exec
```

---

### POST Request
- use to submit data, i.e make changes to a database within an application

+++

### Exercise: Post Data to storage

```bash
# url
https://script.google.com/macros/s/AKfycbxFHnzXZn95MraVopLjA5Rfx5JInmuJ105yJpQ4EuyNEvG29tt3/exec
```

Body:

```json
{
    "name": "abc", 
    "message": "abc"
}
```
---

## Express JS
- a framework to build simple web applications

---

### Barebones Express App
- Clone from [this](https://github.com/cmh114933/express-barebones)

+++

```javascript
app.get("/helloWorld", (req: Request, res: Response) => {
    res.json({
        message: "Hello World"
    })
});

app.<action>("/<path>", (req: Request, res: Response) => {
  // retrieve information from req
  req.params
  req.query
  // send response using res
  res.send(data) // sends data
  res.json(data) // sends json
  res.sendStatus(statusCode) // sends status
  res.status(statusCode).send(data) // sends data with status

})
```

---

### Basic Express template 
- Clone [here](https://github.com/cmh114933/express-basic)

+++

### Folder Structure
<img src="./folder_structure.png">

+++

- `controller` stores the logic for each route
- `routes` stores the configuration for all the routes

---

### Nextagram
- v1: return json data of all users (GET)
- v2: add data to application (POST)

---

### Phase 1: Return data (Raw JSON String)
- hardcodes users data
  ```javascript
    [
      {
        "id": 1,
        "avatar": "http://img_store/test_user_1.img",
        "username": "Test User 1"
      },
      {
        "id": 2,
        "avatar": "http://img_store/test_user_2.img",
        "username": "Test User 2"
      },
      // ...
    ]
  ```
- return raw json data

+++

### Phase 1: Render Static Pages (Homepage)
- render a HTML page with CSS styles

+++

### Controller
```javascript
// controller/HomePageController.ts
export class HomePageController {
    async home(request: Request, response: Response, next: NextFunction) {
        response.sendFile(ABSOLUTE_HTML_FILEPATH)
    }
}
```

+++

```javascript
// routes.ts
export const Routes = [{
    method: "get", // request method
    route: "/home", // path
    controller: HomePageController, // controller
    action: "home" // controller method name
}];
```

+++

#### Defining Parameters
```javascript
// routes
export const Routes = [{
    method: "get",
    route: "/testing/:testValue",
    controller: TestController,
    action: "test"
}]
```

+++

#### Setting Parameters/Query Strings
```bash
# Parameters: sets parameter key testValue as 1
localhost:3000/testing/1

# Query String: sets query string key testValue as 1
localhost:3000/testing?testValue=1
```

+++

#### Using Parameters/Query Strings
```javascript
  // controller
  class TestController {
    async test(request: Request, response: Response, next: NextFunction) {
        // Getting path variables
        request.params[path_key] // request.params.path_key
        // Getting query strings
        request.query[query_key] // request.query.query_key
    }
  }
```

---

### Exercise

GET <span class="text-blue">/api/users/1</span>

```javascript
{
    "id": 1,
    "username": "Test User 1",
    "avatar": "http://img_store/test_user_1.img",
    "images": [
    "http://img_store/users/1/img_1",
    "http://img_store/users/1/img_2",
    "http://img_store/users/1/img_3",
    ]
}
```

+++

GET <span class="text-blue">/api/messages</span>

```javascript
[
    {
    "id":1,
    "text": "Hello world!",
    "user_id": 1,
    "datetime": "2019/08/19 16:01:37"
    },
    // ...
]
```

---

### Phase 2: Add data (POST)

POST <span class="text-blue">/api/sign_up</span>

```json
{
    "username": "Test User 3",
    "avatar": "http://test_image_link.jpg"
}
```

+++

#### Reading request body data

```ts
  // controller
  class TestController {
    async testPost(request: Request, response: Response, next: NextFunction) {
        // returns the body in POST request
        request.body
    }
  }
```
+++

### Exercise

POST <span class="text-blue">/api/messages</span>

```json
{
    "text": "Hello!!!",
    "user_id": 1,
    "datetime": "2019/08/19 16:01:37"
}
```

+++

POST <span class="text-blue">/api/users/1/images</span>

```json
{
    "image_url": "http://image_link.jpg"
}
```

---

## Deployment: Part 1

---

### What is a Live Site?
- running on a server
- accessible on a public URL
- connected to LiveDB and other services

---

### Heroku
- Cloud Provider
- provides servers running 24/7
- Visit [this](https://devcenter.heroku.com/articles/getting-started-with-nodejs) link to learn more

+++

### Setup


- Sign up Account [here](https://signup.heroku.com)
- Download CLI

```bash
npm install -g heroku
```

+++

### CLI Login

```bash
  # Enter the following and follow instructions
  heroku login
```

---

### Basic Express App Deployment

+++

Stop push `node_modules` and `build` folder to heroku

```javascript
// .gitignore
node_modules/*
build/*
```

+++

Specify commands to run server
```javascript
  // Procfile
  web: node build/index.js
```

+++

Use `process.env.PORT` instead of directly writing the port.

+++

Create a heroku app using terminal command
```bash
heroku create
```

+++

After commiting all changes to git, push to heroku
```bash
git push heroku master
```

---

### Angular Deployment: Netlify

---

### Exercise/ Assignment: Bitly Clone
- Deploy an Angular App on Netlify that queries an express backend
- Express backend:
  - <span class="text-blue">POST bit.ly/urls</span>: receive new urls for shorten
  - <span class="text-blue">GET bit.ly/urls</span>: view lists of urls
  - <span class="text-blue">GET bit.ly/urls/{id}</span>: Redirect to shortened link destination
- Angular App:
  - A form to add new links for shortening
  - A lists to show all urls