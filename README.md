# Restaurant Booking System
A booking system for restaurants where users can signin/signup and reserve tables for a given date and time.

![alt text](./prototype/images/screenshots.png)

# Table of Contents
[General Info](#general-info) \
[Technologies](#technologies) \
[Architecture](#architecture) \
[Application Structure](#application-structure) \
[Set Up](#set-up)

# General Info
The goal of this project was to **design, develop and deploy** in the **Cloud** a full stack web app using **Figma**, the **[MERN](https://www.mongodb.com/mern-stack)** stack and **AWS** services. **[MVCS](https://quantiphi.com/an-introduction-to-mvcs-architecture/)** pattern was used in the backend of this application. This project was for training purposes.

# Technologies
- UI
  - Figma
- Frontend
  - ```React```
  - Yarn
  - Typescript
  - Redux (redux-persist)
  - React Router
  - Axios
  - Konva
- Backend
  - ```Node.js```
  - ```Express```
  - ```MongoDB Atlas (mongoose)```
  - JSON Web Tokens
  - Bcrypt
- Backend Infrastructure ```(AWS)```
  - EC2
    - Ubuntu 22.04
    - PM2
    - Snap
    - Apache (Reverse Proxy)
    - Certbot (SSL Certificate)
  - Elastic IPs
  - Route53
# Architecture

![alt text](./prototype/images/architecture-4.png)

# Application Structure

```
backend
├── config
│   └── database.js
├── controllers
│   └── User.controller.js
│   └── Company.controller.js
├── middleware
│   └── auth.js
├── models
│   └── User.js
│   └── Company.js
├── routes
│   └── User.routes.js
│   └── Company.routes.js
├── services
│   └── UserService.js
│   └── CompanyService.js
├── server.js
└── .env
```
- **config/ -** Mongoose config to connect with MongoDB.
- **controllers/ -** Serves the responses.
- **middleware/ -** Verifies JWT Token.
- **models/ -** Schema definitions for mongoose models.
- **routes/ -** Routes for API.
- **services/ -** Business logic between controllers and models.
- **server.js -** Entry point of application.
- **.env -** Environment Variables
```
client
└── src
    ├── apps
    │   ├── auth-app
    │   │   └── components
    │   └── internal-app
    │       ├── components
    │       ├── containers
    │       └── pages
    │           ├── booking
    │           ├── home
    │           └── settings
    ├── hooks
    │   └── hooks.ts
    ├── public
    └── store
    │   ├── features
    │   └── store.ts
    └── index.js
```
- **src/ -** Source Files.
- **apps/ -** Applications within the main app.
- **hooks/ -** Hooks for Redux.
- **public/ -** Assets folder.
- **store/ -** Redux Store and reducers.
- **index.js -** Entry point of the main app.
  
# Set Up

## **Backend**
- Clone this repo 
```https://github.com/luisgcenci/restaurant-booking-system.git```
- Install Dependencies
    ```
    cd backend/
    yarn install
    ```
- Open .env file and insert mongodb uri and replace TOKEN_KEY with a random string.
    > TOKEN_KEY is used to create JWT Auth.
    ```
    MONGO_URI="mongodb+srv://username:password@databasename.bmpbw.mongodb.net/?retryWrites=true&w=majority"
    TOKEN_KEY="RANDOMSTRING"
    ```
- SSL/HTTPS Config

  ```Adjust server.js to server https when deployed in EC2 Instance.``` 
  ``` js
  const https = require('https');
  const fs = require('fs');

  const options = {
  key: fs.readFileSync('privkey.pem'),
  cert: fs.readFileSync('cert.pem')
  }

  const httpsServer = https.createServer(options, app);
  httpsServer.listen(port, () => console.log(`Listening on port ${port}`));
  ```
- How to Run \
  ```node server.js```
- How to Deploy \
    [Deploy NodeJS in AWS EC2 - My Notes from Notion](https://various-postage-17e.notion.site/NodeJS-Deployment-in-AWS-d5dffccb7d1d486487bac7bf2cc48eb2)

## **Frontend**
- Clone this repo 
```https://github.com/luisgcenci/restaurant-booking-system.git```
- Install Dependencies
    ```
    cd client/
    yarn install
    ```
- Open index.js file and insert and point ```axios default baseUrl``` to your API endpoint.
    ``` js
    axios.defaults.baseURL = 'https://restaurant-booking-system.ga:5000/'
    ```
    Now you can send axios requests through the app like this
    ``` js
        axios.get('api/v1/user/auth').
        then( (response) =>{
            //do something with response
        }).catch((err) => {
            // handle errors
        });
    ```
- How to Run \
  ```yarn start```
- How to Deploy \
  [Deploy React on Netlify](https://www.netlify.com/with/react/?utm_source=google&utm_medium=paid_search&utm_campaign=12755510787&adgroup=118788139417&utm_term=deploy%20react%20app%20netlify&utm_content=kwd-1262801015200&creative=514583565966&device=c&matchtype=e&location=9025398)

# Status and Bugs
* Table Reserations for some dates and times might fail. Further debugging needed.
* Multiple sign ups with same username is allowed as of now. Backend needs to be adjusted to handle that.
* UI Design needs improvement.
* [Transformer doesn't work on Brave with Shields enabled #1111](https://github.com/konvajs/konva/issues/1111).

This is the readme file(readme.md)
