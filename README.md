# Immutable Passport Integration Guide

## Table of Contents

1. [Introduction](#1-introduction)
   - [What is Immutable Passport?](#what-is-immutable-passport)
   - [About This Guide](#about-this-guide)
2. [Prerequisites](#2-prerequisites)
3. [Immutable Passport Integration Steps](#3-immutable-passport-integration-steps)
   - [I. Creating Your Application](#i-creating-your-application)
     - [i. Create a New Application](#i-create-a-new-application)
     - [ii. Clone an Existing Application](#ii-clone-an-existing-application)
   - [II. Registering Your Application](#ii-registering-your-application)
   - [III. Installing and Initializing the Passport Client](#iii-installing-and-initializing-the-passport-client)
   - [IV. Logging in a User with Passport](#iv-logging-in-a-user-with-passport)
   - [V. Displaying User Information](#v-displaying-user-information)
   - [VI. Logging Out a User](#vi-logging-out-a-user)
   - [VII. Initiating a Transaction from Passport](#vii-initiating-a-transaction-from-passport)
4. [Video Tutorial](#4-video-tutorial)
5. [Conclusion](#5-conclusion)
6. [Additional Resources](#6-additional-resources)

---

## 1. Introduction

### What is Immutable Passport?

![Immutable Passport](https://github.com/VivekNakrani/Immutable-Passport-Integration/assets/97658605/a2bdea4a-eb79-4f0b-9ff5-6bc5bda598ac)

Immutable Passport is a cutting-edge blockchain-based authentication system tailored for gaming applications. It delivers robust security, efficient user data management, and the capability to oversee blockchain assets. Game developers can seamlessly integrate this system into their applications by registering with the Immutable Developer Hub.

### About This Guide

Welcome to the realm of blockchain-based authentication and elevated security! This comprehensive guide is your gateway to integrating Immutable Passport into your application. Immutable Passport is a revolutionary solution crafted specifically for gaming applications, enhancing both security and functionality—a crucial component for an exceptional gaming experience.

Are you ready to harness the capabilities of Immutable Passport and embark on a journey into the world of blockchain gaming? 🚀 Let's get started!

## 2. Prerequisites

Before you begin with Immutable Passport integration, ensure you have the following prerequisites in place:

- **Code Editor:** A code editor is essential for making changes to your application. We recommend using Visual Studio Code (VS Code).

- **Node.js and npm:** Node.js and npm (Node Package Manager) must be installed on your machine. If you haven't installed them yet, you can download them from [here](https://nodejs.org/en/download).

- **Next.js Application:** You should have a Next.js application ready for integration, or the ability to create one from scratch.

- **Immutable Developer Hub Account:** To interact with Immutable Passport, you need an account on the Immutable Developer Hub. You can sign up for an account [here](https://developers.immutable.com/).

- **JavaScript and Node.js Knowledge:** A basic understanding of JavaScript and Node.js is recommended to navigate the integration process effectively.

By ensuring these prerequisites, you'll be well-prepared to seamlessly integrate Immutable Passport into your application.

## 3. Immutable Passport Integration Steps

### I. Creating Your Application

**Starting Your Application Setup**

**Step 1: Preparing Your Application or Repository**

Before you jump into integrating Immutable Passport, you'll need an application or a repository to work with. Here are the essential steps to get your environment ready:

#### i. Create a New Application

1. **Create a New Project Directory**: Open your preferred command-line tool and create a fresh project directory. Use commands like `mkdir` to create it and `cd` to navigate inside.

```shell
mkdir my-immutable-app
cd my-immutable-app
```

2. **Initialize a New Node.js Project**: Initiate a new Node.js project with either `npm init` or `yarn init`. Follow the on-screen instructions to configure your project.

```shell
npm init -y
# OR
yarn init -y
```

3. **Develop Application Files**: Start by creating essential application files like `index.html` for the front-end and `app.js` for your application logic.

```shell
mkdir pages
```

In the "pages" folder, create a basic "app.js" file and copy the following JavaScript code into it:

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

function Home() {
  return <div>Hey, It is Immutable Passport Integration</div>;
}

ReactDOM.render(<Home />, document.getElementById('root'));
```

4. **Install Required Dependencies**: Depending on your project's needs, install additional packages or frameworks using `npm install` or `yarn add`.

```shell
npm install
# OR
yarn add
```

5. **Run Your Application**

```shell
npm run start
```

#### ii. Clone an Existing Application

1. **Choose a Suitable Repository**: Explore platforms like GitHub and GitLab to find a repository that matches your requirements.

2. **Clone the Repository**: Utilize the `git clone` command to copy the repository to your local machine. You can find more information on how to clone a repository [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository).

**General Guidelines**

- Ensure your application or cloned repository maintains a well-organized structure, clearly separating front-end and back-end components.

- For a fresh project, carefully consider the architecture and plan your development. Employ a version control system like Git to track changes effectively.

- Keep your application lightweight initially, adding features and components progressively.

- Test your application during development, even before integrating Immutable Passport, to ensure its correct functionality at each stage.

By either creating a new application or cloning an existing repository, you've laid the foundation for the next steps in the Immutable Passport integration journey. This environment will serve as the canvas on which you'll unleash the capabilities of Immutable Passport

### II. Registering Your Application

To start using Immutable Passport, follow these steps to register your application on the Immutable Developer Hub:

1. **Visit the Hub**: Go to the [Immutable Developer Hub](https://hub.immutable.com/login).

2. **Create an Account**: If you don't already have one, create an account there.

3. **Create Your Application**: Click on "Create Application" and follow the on-screen instructions to set up your application.

4. **Configure Your App**:
   - Choose "Web Application" as the application type.
   - Enter a unique name in the "Client Name" field.
   - Specify valid URLs for "Logout" and "Callback" in their respective sections.

5. **Create a .env File**: Create a .env file and add your Client ID as follows:

```
CLIENT_ID = "Your_Client_ID"
CLIENT_SECRET = "YOUR_CLIENT_SECRET"
```

By completing these steps, you've successfully registered your application, marking the first milestone in integrating Immutable Passport.

### III. Installing and Initializing the Passport Client

In your application, you'll need to install the necessary dependencies and initialize the Passport Client to interact with Immutable Passport.

Install immutable-passport using npm:
```
npm install immutable-passport
npm install @imtbl/sdk ethers
# OR
yarn add immutable-passport
yarn add @imtbl/sdk ethers
```
Create a new file called index.js in the my-immutable-app directory and add the following code:
```
require('dotenv').config(); // Load environment variables from .env file
const passport = require('@immutablex/passport');

const app = passport({
  clientId: process.env.CLIENT_ID, // Use the CLIENT_ID from .env
  clientSecret: process.env.CLIENT_SECRET, // Use the CLIENT_SECRET from .env
  callbackURL: 'http://localhost:3000/auth/callback',
});

module.exports = app;
```
With this step, your application is ready to connect with Immutable Passport securely.

### IV. Logging in a User with Passport
```
// Import the Passport app you've created
const passport = require('./index');

// Define a function to initiate user authentication
const loginWithPassport = async () => {
  try {
    // Assuming you have a user object, replace 'user' with the actual user object.
    const user = getUser(); // Replace with your user retrieval logic

    if (!user) {
      console.error('User not found.');
      return;
    }

    // Log in the user using Passport's authenticate function
    passport.authenticate('local', (err, user) => {
      if (err) {
        console.error('Login error:', err);
      } else {
        // If successful, the user is connected.
        // You can redirect or perform additional actions here
      }
    });

  } catch (error) {
    console.error('Authentication error:', error);
  }
};

// Call the login function when needed to trigger the authentication process.
loginWithPassport();
```
With this code, you can effectively handle user authentication in your application.

### V. Displaying User Information
```
// Define a function to fetch and display user information
const displayUserInfo = async () => {
  try {
    const userProfile = await passportProvider.getUserInfo();
    const { accessToken, idToken } = passportProvider.getTokens();

    console.log("User Profile:", userProfile);
    console.log("Access Token:", accessToken);
    console.log("ID Token:", idToken);
  } catch (error) {
    errorHandling("Error fetching user information", error);
  }
};

// Call the function when needed to display user information.
displayUserInfo();
```
With this code, you can effectively fetch and display user information post-authentication.

### VI. Logging Out a User
```
import { passportInstance } from "@/lib/immutable";

// Define a function to log out a user
const logoutUser = () => {
  // Trigger the Passport logout process
  passportInstance.logout();
};

// Call the function when the user initiates the logout process.
logoutUser();
```
With this code, you can implement user logout functionality effectively.

### VII. Initiating a Transaction from Passport
```
import { passportInstance } from "@/lib/immutable";

const sendTransaction = async (recipient, value, data) => {
  try {
    const transaction = { to: recipient, value, data };
    const transactionHash = await passportInstance.sendTransaction(transaction);
    console.log("Transaction Hash:", transactionHash);
  } catch (error) {
    console.error("Error sending transaction:", error);
  }
};

// Define transaction parameters
const recipientAddress = 'RECIPIENT_ADDRESS';
const value = '1000000000000000000'; // 1 Ether in wei
const transactionData = 'Replace with your data';

// Call the function to send the transaction.
sendTransaction(recipientAddress, value, transactionData);
```
With this code, you'll be able to initiate transactions from Passport in your application. Ensure you populate the transactionData object with the appropriate values for your use case.

## 4. Video Tutorial

## 5. Conclusion

Congratulations! You've successfully integrated Immutable Passport into your application, enhancing security and functionality. This guide has covered the entire process, from setting up your application to initiating transactions. Immutable Passport opens up exciting possibilities for blockchain-powered gaming experiences.

![11_1_50](https://github.com/VivekNakrani/Immutable-Passport-Integration/assets/97658605/b713a080-61b3-4827-b704-1e98d67e5162)

## 6. Additional Resources

#### Useful Links

1. [Immutable Passport Product Page](https://www.immutable.com/products/passport)
2. [Immutable Blog](https://www.immutable.com/blog)
3. [Immutable Documentation](https://docs.immutable.com/)
4. [Immutable Community Connect](https://www.immutable.com/community/connect)
5. [Immutable Developers](https://www.immutable.com/developers)

   To know more about Immutable Passport and How to Integrate into Your Application [Visit Here](https://mirror.xyz/0x29054eBcf5d36B7dFc87f82f3c0A23EE05CE4314/KduM90jp2uW6k7ZeqrHJZBagGMNYqdbJr37PDO5-z6Q).

If you have any questions or challenges along the way, don't hesitate to reach out to the Immutable community or support. Happy building! 🚀🎮

This guide offers a structured and unique approach to integrating Immutable Passport into your application, providing both code snippets and explanations. Good luck with your integration, and enjoy the benefits of blockchain authentication and gaming!
