# firestore-export-import
NPM package for backup and restore Firebase Firestore

You can export and import data from firestore with sub collection. 

## Installation 

Install using [__npm__](https://www.npmjs.com/).

```sh
npm install firestore-export-import
```

## Get Google Cloud Account Credentials from Firebase

You can __Generate New Private Key__ from Project Settings from [Firebase Console](https://console.firebase.google.com).

After that you need to copy the __databaseURL__ for initiating the App. 

## Usage 

You have to import this package in a JavaScript file and work from there.

### Export data from firestore 

You can export collection and sub collection from your data. The sub collection is optional.

```
// In your index.js 

const firestoreService = require('firestore-export-import');
const serviceAccount = require('./serviceAccountKey.json');

// Initiate Firebase App
firestoreService.initializeApp(serviceAccount, databaseURL);

// Start exporting your data
firestoreService
  .backup('collection-name', 'sub-collection-optional')
  .then(data => console.log(JSON.stringify(data)))
```

### Get all collections data

This is a suggestion from [jcummings2](https://github.com/jcummings2) and [leningsv](https://github.com/Leningsv)

The ['collectionName1', 'collectionName2'] is OPTIONAL, you can remove this parameter to get all of the current collections in your firestore.

The result is an object of collection's data.

```
firestoreService
  .backups(['collectionName1', 'collectionName2']) // Array of collection's name is OPTIONAL 
  .then(collections => {
    // You can do whatever you want with collections
    console.log(JSON.stringify(collections));
  })

```

### Import data to firestore 

This code will help you to import data from a JSON file to firestore

```
// In your index.js 

const firestoreService = require('firestore-export-import');
const serviceAccount = require('./serviceAccountKey.json');

// Initiate Firebase App
firestoreService.initializeApp(serviceAccount, databaseURL);

// Start importing your data
// The array of date fields is optional
firestoreService.restore('your-file-path.json', ['date1-field', 'date2-field']);
```

The JSON is formated as below. The collection name is __test__. __first-key__ and __second-key__ are document ids. 

```
{
  "test" : {
    "first-key" : {
      "email"   : "dungnq@itbox4vn.com",
      "website" : "dalenguyen.me",
      "custom"  : {
        "firstName" : "Dale",
        "lastName"  : "Nguyen"
      },
      "date": {
        "_seconds":1534046400,
        "_nanoseconds":0
      }
    },
    "second-key" : {
      "email"   : "test@dalenguyen.me",
      "website" : "google.com",
      "custom"  : {
        "firstName" : "Harry",
        "lastName"  : "Potter"
      },
      "date": {
        "_seconds":1534262435,
        "_nanoseconds":0
      }
    }
  }
}
```

## Contributions

This project is based on [firestore-import-export](https://github.com/dalenguyen/firestore-import-export), feel free to report bugs and make feature requests in the [Issue Tracker](https://github.com/dalenguyen/firestore-backup-restore/issues), fork and create pull requests!