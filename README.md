# Magic Link Authentication with React, Flask, and Authsignal

**Authentication is the process of verifying the identity of a user or system. It ensures that only authorized individuals or systems can access certain resources or perform specific actions.**

Magic Link Authentication offers a simple yet secure way for users to log in without passwords. This project is the implementation of Magic Link Authentication using React for the front end, Flask for the back end, and the authentication service provided by [Authsignal](https://www.authsignal.com/)

## Understanding Magic Link Authentication

Magic Link Authentication is a convenient and secure authentication method that simplifies users' login process. Instead of entering a username and password, users receive a unique link via email. This link, known as a magic link, grants them access to their account without traditional credentials.

One key difference between magic link authentication and authentication with email verification is the user experience. With magic link authentication, users can authenticate with just a single click. They don't need to remember or enter a password, which can be especially beneficial for users who struggle with password management or find it inconvenient to type in their credentials repeatedly.

While email verification adds an extra layer of security, it may require the user to remember additional credentials or go through multiple steps before accessing their account.

## How to Configure Authsignal

[Authsignal](https://www.authsignal.com/) is a service that makes implementing modern authentication methods (like Magic Links and Passkeys) easier. It provides simple tools to integrate secure login methods into your web apps without hassle.

For this project implementation, you need to create an Authsignal account. To do that, you can follow these steps:

1. First, go to [authsignal.com](https://portal.authsignal.com/users/sign_up) and click on "Create Free Account".

2. In the next step, create your first tenant. Choose any name for your tenant and select the data storage region.

3. Next, you need to configue the authenticators you want to use for your application. For this project, I have enabled Email Magic Link and Authenticator App (TOTP).

4. Once you have configured the authenticator, navigate to the API Keys option. Here, you will find your Secret Key, which will be necessary for implementing the authentication.

## Application Flow

Let's understand the flow of the application:

### Initial Visit

- The user visits the application's user interface. On the user interface, they see a login input box and a signup option. Since the user is new, they opt to sign up.

### Signup Flow

- Upon clicking the signup link, the user is directed to a page to enter their chosen username.

- After entering the username and clicking the signup button, the front and triggers a POST API call to /api/signup, sending the username in the request body.

- The backend receives the request and communicates with the Authsignal server for user authentication.

- Authsignal prompts the user to set up Magic Link authentication by entering their email address.

- Authsignal sends a magic link to the provided email address.

- After clicking the magic link, the user is authenticated and redirected the the home page, where they receive a welcome message displaying their email addresss. The page also included a logout button.

### Login Flow

- The user logs out and returns to the login page.

- Here, the user enters their registered username and clicks the Login button.

- Upon clicking Login, the front end triggers a POST API call to /api/login, passing the username in the request body.

- The backend again communicates with Authsignal for user authentication, prompting the setup of Magic Link authentication.

- The user is directed to a page to enter their email address.

- Authsignal sends a magic link to the provided email address.

- After clicking the magic link, the user is authenticated and redirected to the home page, greeted with a welcome message displaying their email address.

This flow ensures users can sign up using a chosen username, and set up Magic Link authetication via email for both signup and login.

## Authsignal Actions

Authsignal allows you to create actions to track and manage user interactions in your application. Actions are events that can be triggered by users, such as signing up or logging in. By creating custom actions, you can have more control over the authentication process and implement specific authentication methods like Magic Link Authentication.

To create an action on your Authsignal dashboard, follow these steps:

1. Click on **"Actions"** in your Authsignal dashboard.

2. Click on **"Click a new action"** to create a new action.

3. Enter a name for the action that describes its purpose or the user interaction it represents.

4. Next, you can configure the rule for the action. In our case, since we want to implement Magic Link Authentication, we will add a rule to challenge users with Email Magic Link. This will send a magic link to the user's email for authentication.

5. Save the action the apply the rule and make it active.

## How to Run the Application

To run the backend application, run `python app.py` from your back-end folder in your terminal. This will start your back-end server on port 5000. Next, run the frontend application using the `npm start` command. This will start your frontend application on the port 3000.
