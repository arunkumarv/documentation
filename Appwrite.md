# Appwrite

## Installation

### Use webpack

Give link to webpack template in github.

## Create an account

[https://appwrite.io/docs/client/account](https://appwrite.io/docs/client/account)
[https://appwrite.io/docs/client/databases](https://appwrite.io/docs/client/databases)

```javascript
import { Client, Account, ID, Databases } from "appwrite";
import randomString from './utils.js';

const apiEndPoint = 'http://localhost/v1';
const projectID = '63387e4f8a27ee542f07';
const databaseID = '633c5f822d4f71fe1ef0';
const collectionID = '633c5f8deacd02cf5528';

const client = new Client().setEndpoint(apiEndPoint).setProject(projectID);
const account = new Account(client);
const databases = new Databases(client);


// Subscribe to files channel
client.subscribe('files', response => {
    if (response.events.includes('buckets.*.files.*.create')) {
        // Log when a new file is uploaded
        console.log(response.payload);
    }
});

function create_button(text, callback) {
    const btn = document.createElement('button');
    btn.style.margin = "10px";
    btn.innerHTML = text;
    btn.onclick = callback;
    return btn;
}

function executePromise(promise){
    promise.then(function (response) {
        console.log(response);
    }, function (error) {
        console.log(error);
    });
}


document.body.appendChild(create_button('create random account', () => {
    const promise = account.create(ID.unique(), `${randomString(4)}@${randomString(7)}.${randomString(3)}`, 'password', `${randomString(4)} ${randomString(4)}`)
    executePromise(promise);
}));

document.body.appendChild(create_button('Create Account Session with Email', () => {
    const promise = account.createEmailSession('me@example.com', 'password');
    executePromise(promise);
}));

document.body.appendChild(create_button('print all docs', () => {
   const promise = databases.listDocuments(databaseID, collectionID);
   executePromise(promise);
}))
```
