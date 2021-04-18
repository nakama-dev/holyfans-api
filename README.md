# Holyfans | Design your best fortune : API / Web Services

Project Phase 1 by Group 1 Section 3

## How to DEV

```bash
# Install Dependencies
yarn

# Dev on local machine
yarn dev

# Build for Production
yarn build

# Start the app
yarn start
```

```bash
# Install Dependencies
npm install

# Dev on local machine
npm run dev

# Build for Production
npm run build

# Start the app
npm start
```

## Members

- Thanapat Jumnongrat (Palm) ID: 6288018
- Veerakit Prasertpol (Pete) ID: 6288035
- Supakarn Laorattanakul (Prompt) ID: 6288087
- Thanaboon Sapmontree (Time) ID: 6288123

# Web Services Documentation

This web services created by Node.js, Express.js, and Google Firebase in TypeScript Language

## Platform Choice

### Why we choose Firebase as a services for database and storage

Firebase is a service that is built for web and mobile developers to ease the production time of mobile and web applications. It provides a lot of small services like Authentication, Cloud Firestore, Real-time Database, and Storage.

We choose Cloud Firestore, a Firebase service, as a database because we want to experiment with NoSQL and its document-based structure.

Although Firebase provides the authentication service, for this project, we will implement our own authentication services using Cloud Firestore, Express.js, and JSON Web Token (JWT).

We designed a database as 2 collections: `holyfans_users` and `holyfans_teller`

The document structure in `holyfans_users` is

```
xxxxxx (Unique ID auto-generated by Firestore)
|_ role : user | admin
|_ firstName : string
|_ lastName : string
|_ isActive : boolean
|_ email : string
|_ password : string (Encrypted)
|_ dateCreated : Timestamp
|_ dateModified : Timestamp
|_ log (Sub-Collection)
   |_ xxxxxx (Unique ID auto-generated by Firestore)
      |_ action : string
      |_ time : timestamp
```

The document structure in `holyfans_teller` is

```
xxxxxx (Unique ID auto-generated by Firestore)
|_ nameTH : string
|_ nameEN : string
|_ img : string
|_ region : boolean
|_ subPrice : string
|_ bio : string
|_ address : geolocation (lat, lng)
|_ dateCreated : Timestamp
|_ category : string[]
|_ contact : map
|  |_ email : string
|  |_ facebook : string
|  |_ instagram : string
|  |_ line : string
|  |_ phoneNum : string
|  |_ twitter : string
|  |_ website : string
|
|_ posts (Sub-Collection)
   |_ xxxxxx (Unique ID auto-generated by Firestore)
      |_ content : string
      |_ img : string
      |_ dateCreated : timestamp
```

## API Endpoint

We separated in to 3 route:

- `/auth` : For Authentication services
- `/tellers` : For Holo Teller services
- `/users` : For Users Management services

### Route `/auth`

#### Endpoint : POST `/auth/login`

```JSON
// Body : <application/json>
{
  "email": "",
  "password": ""
}

// Response : <application/json>
{
  "status" : "success",
  "payload" : {
    "token": "/* JWT token (save for usage) */",
    "user": {
      /* User Data */
    }
  }
}
```

#### Endpoint : POST `/auth/logout`

```JSON
// Authorization: JWT token from login
// Body : None

// Response : <application/json>
{
  "status" : "success"
}
```

#### Endpoint : POST `/auth/register`

```JSON
// Body : <application/json>
{
  "firstName": "",
  "lastName": "",
  "email": "",
  "password": ""
}
// Response : <application/json>
{
  "status": "success",
  "payload": {
    "token": "/* JWT token (save for usage) */",
    /* User Data */
  }
}
```

### Route `/tellers`

#### Endpoint : GET `/tellers/all`

```JSON
// Body : None

// Response : <application/json>
{
  "status": "success",
  "payload": [{
    /* Teller Data */
  }]
}
```

#### Endpoint : GET `/tellers?tId=...`

```JSON
// Body : None

// Response : <application/json>
{
  "status": "success",
  "payload": {
    /* Teller Data with posts data */
  }
}
```

#### Endpoint : GET `/tellers/search?search_keyword=...&categories=...&area=...&price_range=...`

```JSON
// Body : None

// Response : <application/json>
{
  "status": "success",
  "payload": [{
    /* Teller Data */
  }]
}
```

#### Endpoint : POST `/tellers`

```JSON
// Authorization : JWT token from login (Requires admin privilege)
// Body : <application/json>
{
  "nameTH": "",
  "nameEN": "",
  "bio": "",
  "img": "",
  "region": "",
  "subPrice": ,
  "category": [""],
  "contact": {
    "instagram": ""
  },
  "address": {
    "_latitude": ,
    "_longitude":
  }
}

// Response : <application/json>
{
  "status": "success",
  "payload": {
    /* Teller Data */
  }
}
```

#### Endpoint : PUT `/tellers`

```JSON
// Authorization : JWT token from login (Requires admin privilege)
// Body : <application/json>
{
  "id": "",
  "nameTH": "",
  "nameEN": "",
  "img": "",
  "bio": "",
  "subPrice": ,
  "region": "",
  "category": [""],
  "contact": {
    "instagram": ""
  },
  "address": {
    "_latitude": ,
    "_longitude":
  }
}

// Response : <application/json>
{
  "status": "success",
  "payload": {
    "_writeTime": {
      "_seconds": ,
      "_nanoseconds":
    }
  }
}
```

#### Endpoint : GET `/tellers/search?search_keyword=...&categories=...&area=...&price_range=...`

```JSON
// Body : None

// Response : <application/json>
{
  "status": "success",
  "payload": [{
    /* Teller Data */
  }]
}
```

#### Endpoint : DELETE `/tellers?tId=`

```JSON
// Authorization : JWT token from login (Requires admin privilege)
// Body : None

// Response : <application/json>
{
  "status": "success",
  "payload": {
    "_writeTime": {
      "_seconds": ,
      "_nanoseconds":
    }
  }
}
```
