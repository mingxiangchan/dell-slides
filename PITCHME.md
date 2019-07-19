### HTTP POST

+++

| field  | required | example                      |
| ------ | -------- | ---------------------------- |
| url    | yes      | http://insta.nextacademy.com |
| header |          | `{string: string}`           |
| body   |          | `{string: any}`              |

+++

Angular Settings

```ts
const url = 'https://insta.nextacademy.com/api/v1/users'

const params = {
  username: 'Test User',
  email: 'email@example.com',
  password: '12345678',
}

const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type': 'application/json',
  }),
}
```

+++

Using it

```ts
this.http.post(url, params, httpOptions).subscribe(response => {
  console.log(response)
})
```

---

### Stateful Requests

+++

HTTP Requests are stateless by default

+++

#### Analogy

1. check in at hotel
2. get card
3. go to hotel room
4. insert card
5. door opens

- if no card, cannot enter

+++

1. log in with website
2. get auth token
3. make request
4. attach auth token
5. request is allowed to go through

+++

### Auth Token Format

its just a string, basically a password

```ts
const authToken = response['auth_token']
console.log(authToken) // => "lsy877t21g21dad"
```

+++

### Attaching Auth Token

Differs from app to app

```ts
const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type': 'application/json',
    Authorization: `Bearer ${authToken}`,
  }),
}
```

---

### Persistence

+++

All JS variables are cleared on refresh

Some things need to be persisted, e.g.

- layout settings (sidebar closed)
- auth tokens (e.g. remember me)

+++

3 places to persist

1. session
2. cookies
3. localStorage

+++

Local Storage Implementation

```ts
// storing
localStorage.setItem('authToken', authToken)

// retrieving
const authToken = localStorage.getItem('authToken')
```

---

### How to Coordinate

+++

Frontend

```
this is what i will send you
```

Backend

```
this is how i will respond
```

+++

#### Frontend

My request will be like:

```ts
{
  method: 'POST',
  url: "https://insta.nextacademy.com/users",
  headers: {'Content-Type': 'application/json', 'Authorization': 'Bearer dsfa598s6fsaf'},
  body: {
    "name": "Ming Xiang",
    "email": "mingxiang@nextacademy.com",
    "password: "123456"
  }
}
```

+++

#### Backend

My response will be like:

````ts
{
  code: 200,
  body: {
    "message": "Success",
    "auth_token": "986fsdrf7659ffa"
  }
}
```

And if its a failure I will respond with

```ts
{
  code: 404,
  body: {
    "error": "Not Found"
  }
}
````