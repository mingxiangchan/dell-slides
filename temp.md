1. Restricted/Public endpoints
2. What is the authorization header, stateless requests
3. What is JWT
4. Implementing login/signup (in-memory DB)
5. Integrating against DB
    - signup
        - generating JWT token for user
        - password encryption
    - login
        - check user's JWT
        - custom user details service
        - principal
    - subsequent requests
        - accessing the current user
        - logging out
