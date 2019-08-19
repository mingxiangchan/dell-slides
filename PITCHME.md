### Spring Session and Security

---

Recap:

1. render HTML
2. render JSON
3. query database using JDBC
4. query database using Spring Data/Hibernate

---

How do we differentiate logged in / non logged in users?

---

### HTTP is Stateless

+++

#### Each HTTP Request is:

- completely separate from the previous ones
- must prove it is authorized

+++?color=linear-gradient(90deg, white 50%, black 50%)

@snap[north-west span-40 text-white text-09]
@box[bg-green](Step 1. # Check in at hotel)
@snapend

@snap[west span-40 text-white text-09]
@box[bg-blue](Step 2. # Get room key)
@snapend

@snap[south-west span-40 text-white text-09]
@box[bg-gold](Step 3. # Every time you enter the room, tap key)
@snapend

@snap[north-east span-40 text-white text-09]
@box[bg-green](Step 1. # Login with username/password)
@snapend

@snap[east span-40 text-white text-09]
@box[bg-blue](Step 2. # Get authorization token)
@snapend

@snap[south-east span-40 text-white text-09]
@box[bg-gold](Step 3. # Attach token in HTTP headers for every request)
@snapend

+++

@snap[north span-100]
#### Authorization Storage Mechanisms
@snapend

@snap[east span-40 text-white text-09]
@box[bg-green](# sessions)
@snapend

@snap[midpoint span-40 text-white text-09]
@box[bg-blue](# cookies)
@snapend

@snap[west span-40 text-white text-09]
@box[bg-gold](# tokens)
@snapend

+++

### In this course...

- only teach token auth
- sessions/cookies inapplicable to API auth
- do you want to write Thymeleaf?

---

### 4 Main Sections

- Signing Up
- Logging In
- Authorized Requests
- Logging Out

+++

#### Group Activity: Understanding Auth Flow

Note:

- 3 ppl manage sign up - record details
- 2 ppl manage login - issue token
- 2 ppl manage post-login(1) - get lottery number
- 2 ppl manage post-login(2) - reset password
- everyone else act as requesters

- backend ppl share a google sheet of users
- each signup requires a username and password, add a random lottery number
- issue a 3 letter token
- use token to check which user

+++

#### 4 Stations:

- getLotteryNumber
- signUp
- login
- resetPassword

+++

![graph](https://kroki.io/mermaid/svg/eNpLL0osyFDwCeJSUCgujQ7OTM9TCC2IVdDVtVNIL4l2Ty1RCMnPTs2LBcrnpEf75KcreObBpIFi6SUQdmqJT35JSWpRJUKsKLU4tSQgsbi4PL8oBQBfMyAB)

---

### Create a Auth Test DB

- users table
  - username: string
  - password: string
---

### Auth Libs In Spring

- Spring Security
- JWT Token Auth

+++

### Create a New Spring Project

- name: jwt
- add usual dependencies

+++

#### Add Maven Dependencies

1. jjwt-jackson
2. jjwt-impl
3. jjwt-api
4. spring-boot-starter-security

---

### Example Repo

[Clone it Here](https://github.com/mingxiangchan/spring-jwt)

+++

#### Explore it...

Then import it to your own repo!

+++

#### Don't Roll Your Own

- Auth is too complicated
- learn how to configure it
- no need to write from scratch

---

### Endpoints

```bash
# unsecured endpoint
/public

# secured endpint
/restricted

# sign up endpoint
/signup

# log in endpoint
/authenticate

# check current user info endpoint
/currentUser
```

+++

### Interesting Files

```
configuration/SecurityConfiguration.java
constants/SecurityConstants.java
security/JwtUtils.java
security/JwtAuthorizationFilter.java
security/JwtAuthenticationFilter.java
security/CustomUserDetailsService.java
```

---

#### Secured vs Non Secured Endpoints

- check <span class="text-blue">configuration/SecurityConfiguration.java</span>
- restrict all endpoints by default
- selectively enable certain endpoints to be insecure

+++

### How does it check?

- parses response header for "Authorization" header
- processes it as JWT if present
- check if user_id is present in JWT

+++

### Why Authorization Header

- the standard header for sensitive authorization data
- automatically filtered by logging/browsers etc.

+++

### Exercise

1. create a new endpoint <span class="text-blue">/testing</span>
2. make your endpoint restricted
3. create a new endpoint <span class="text-blue">/testing2</span>
4. make your endpoint public

---

### Signing Up

- check <span class="text-blue">controllers/SignupController.java</span>
- send username, password
- create user in DB
- generate JWT token
- return JWT token in response

+++

### Sign Up Endpoint

```
localhost:8080/signup
```

Request Body

```json
{
  "username": "mingxiangchan",
  "password": "123123"
}
```

Response Body

```json
{
  "token": <token>
}
```

+++

### Using JWT

- in Postman
- send the signup request
- get the token
- send a request to the restricted endpoints using the token

+++

### Password Encryption

- check the password in DB
- check the setPassword method on UserEntity

+++

### Exercise

- change the signup endpoint to <span class="text-blue">/api/signup</span>
- sign up 3 times, save the token each time

---

### Logging In

- check <span class="text-blue">security/JwtAuthenticationFilter.java</span>
- send username, password
- check login credentials for match
- return JWT token in response if success
- a lot of internal workings hidden by Spring Security

+++

### Login Endpoint

```
localhost:8080/api/authenticate
```

Request Body

```json
{
  "username": "mingxiangchan",
  "password": "123123"
}
```

Response Header

```json
{
  "Authorization": <token>
}
```

+++

### Exercise

1. change login endpoint to <span class="text-blue">/api/authenticate</span>
2. log in 3 times and store the tokens

---

### Encryption

- check the password column in DB
- is it the password you entered?

+++

### One Way vs Two Way Encryption

- what are they?
- which one is more secure
- is Bcrypt a 1 way or 2 way encryption method



---

### Final Exercise

1. Add email to <span class="text-blue">users</span> table (migration)
2. Log in with <span class="text-blue">email</span> and password
2. Store email inside JWT instead of <span class="text-blue">users.id</span>
3. Change code to use <span class="text-blue">users.email</span> to identify current user

+++

### Documentation

[Read the docs here](https://gist.github.com/mingxiangchan/eb3a5388e93182d7c8cc5c6263b378c2)
