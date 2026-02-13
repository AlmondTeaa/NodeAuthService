# JWT Refresh Auth Service

A lightweight authentication microservice built with Node.js, Express, and JSON Web Tokens (JWT). This service implements secure access & refresh token rotation and invalidation, inspired by the Web Dev Simplified tutorial on JWT Authentication.

## ✨ Features

-   **User Registration & Login:** Basic user creation and authentication.
-   **Access Tokens:** Short-lived JWTs for securing API endpoints.
-   **Refresh Tokens:** Long-lived tokens stored server-side to securely issue new access tokens.
-   **Token Rotation:** A new refresh token is issued with each request, enhancing security.
-   **Token Invalidation:** Ability to logout/destroy refresh tokens, preventing their reuse.
-   **Modular Routes:** Clean separation of `auth` and protected routes.

## 🛠️ Built With

-   [Node.js](https://nodejs.org/) - JavaScript runtime
-   [Express](https://expressjs.com/) - Web framework
-   [JSON Web Tokens (jsonwebtoken)](https://www.npmjs.com/package/jsonwebtoken) - For signing & verifying tokens
-   [bcrypt](https://www.npmjs.com/package/bcrypt) - For password hashing
-   [Postman](https://www.postman.com/) / [Insomnia](https://insomnia.rest/) - For API testing (recommended)

## 🚀 Getting Started

### Prerequisites
-   Node.js (v14 or later)
-   npm or yarn
-   A REST client (Postman/Insomnia)

### Installation
1.  Clone the repository:
    `git clone https://github.com/[your-username]/jwt-refresh-auth-service.git`
2.  Navigate into the project directory:
    `cd jwt-refresh-auth-service`
3.  Install dependencies:
    `npm install`
4.  Create a `.env` file in the root directory and add your environment variables:
    ```env
    ACCESS_TOKEN_SECRET=your_super_secret_access_key
    REFRESH_TOKEN_SECRET=your_super_secret_refresh_key
    PORT=3000
    ```
5.  Start the server:
    `npm run dev` (or `node server.js`)

## 📡 API Endpoints

| Method | Endpoint             | Description                                      | Auth Required |
|--------|----------------------|--------------------------------------------------|---------------|
| POST   | `/api/register`      | Register a new user. Body: `name`, `password`    | No            |
| POST   | `/api/login`         | Login user. Body: `name`, `password`            | No            |
| POST   | `/api/token`         | Get a new access token using a refresh token.    | No (via body) |
| DELETE | `/api/logout`        | Invalidate a refresh token.                     | No (via body) |
| GET    | `/api/posts`         | Example protected route.                        | Yes (Bearer)  |

*(*Note: You will build these endpoints following the tutorial.*)*

## 🧠 How It Works (Simplified Flow)

1.  **Registration/Login:** User credentials are validated, password is hashed with `bcrypt`, and a user is stored in memory (or a DB). An **Access Token** and **Refresh Token** are generated and returned.
2.  **Accessing Protected Routes:** The client sends the Access Token in the `Authorization: Bearer <token>` header. The server verifies it before sending the response.
3.  **Refreshing Tokens:** When the Access Token expires, the client sends the Refresh Token to `/api/token`. If valid, the server issues a **new** Access Token and a **new** Refresh Token (rotation).
4.  **Logout:** The client sends the Refresh Token to `/api/logout`. The server removes it from its store, making it unusable.

## 📚 What I Learned / Key Concepts

This project was built to solidify my understanding of:

-   The difference between **Access Tokens** and **Refresh Tokens**.
-   Why refresh tokens are stored server-side, while access tokens are stateless.
-   Implementing secure **token rotation** to prevent replay attacks.
-   The importance of using strong, separate secrets for signing tokens.
-   Structuring a simple Node.js/Express application into routes and middleware.

## 🔮 Future Improvements

-   [ ] Replace the in-memory array storage with a real database (e.g., MongoDB, PostgreSQL).
-   [ ] Add input validation and sanitization.
-   [ ] Implement refresh token expiration and automatic cleanup.
-   [ ] Write unit and integration tests.
-   [ ] Add HTTPS enforcement in production.
-   [ ] Containerize with Docker.

## 🙏 Acknowledgments

-   [Web Dev Simplified](https://www.youtube.com/c/WebDevSimplified) for the excellent [JWT Authentication Tutorial](https://www.youtube.com/watch?v=mbsmsi7l3r4&t=108s) that served as the foundation for this project.

## 📝 License

This project is for educational purposes.