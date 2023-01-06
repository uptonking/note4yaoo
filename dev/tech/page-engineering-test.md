---
title: page-engineering-test
tags: [engineering, testing]
created: 2020-12-31T12:06:19.343Z
modified: 2020-12-31T12:07:18.316Z
---

# page-engineering-test

# [How to mock data in React with a fake API](https://www.robinwieruch.de/react-mock-data)

- react app starter

``` JS
import * as React from 'react';

import { getUsers, createUser, updateUser, deleteUser } from './api';

const App = () => {
  const [users, setUsers] = React.useState(null);

  if (!users) {
    return null;
  }

  React.useEffect(() => {
    const doGetUsers = async () => {
      const result = await getUsers();
      setUsers(result);
    };

    doGetUsers();
  }, []);
  return <div>Hello React</div>;
};

export default App;
```

- REACT FOR CREATING MOCK DATA

- The actual creation of the additional mock data should work, however, you will not see the result reflected in the React UI. 
  - That's because we are not updating the mock data in the UI. 
- There are two ways to keep the UI in sync after a request which modifies data on the backend:
  - After the request finishes, we know about the mock data which we just created, so we could update the React's state with it (.e.g. updating the users state with the new user).
  - After the request finishes, we could refetch all the mock data from the backend. That's another network roundtrip to the backend (which is our fake API here), but it keeps our data in sync with the rendered UI as well.

- UPDATING AND DELETING MOCK DATA IN REACT

- we will introduce a button which will be used to flip the boolean for one property of our mock data
  - What's missing is the handler which updates the mock data via our fake API and which refetches all mock data afterward for keeping the data in sync

- we will implement a button to remove mock data and a handler which does the actual deletion of it

# [JavaScript fake API with Mock Data](https://www.robinwieruch.de/javascript-fake-api)

- ## JAVASCRIPT FAKE API

``` JS
import { v4 as uuidv4 } from 'uuid';

const idOne = uuidv4();
const idTwo = uuidv4();

let users = {
  [idOne]: {
    id: idOne,
    firstName: 'Robin',
    lastName: 'Wieruch',
    isDeveloper: true,
  },
  [idTwo]: {
    id: idTwo,
    firstName: 'Dave',
    lastName: 'Davddis',
    isDeveloper: false,
  },
};

const getUsers = () =>
  Promise.resolve(Object.values(users));

// usage (1)
getUsers()
  .then(result => {
    console.log(result);
  });

// usage (2)
const doGetUsers = async () => {
  const result = await getUsers();
  console.log(result);
};
doGetUsers();
```

``` JS
// longer promise version

const getUsers = () =>
  new Promise((resolve, reject) => {
    if (!users) {
      return setTimeout(
        () => reject(new Error('Users not found')),
        250
      );
    }

    setTimeout(() => resolve(Object.values(users)), 250);
  });

// usage (1)
getUsers()
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  });

// usage (2)
const doGetUsers = async () => {
  try {
    const result = await getUsers();
    console.log(result);
  } catch (error) {
    console.log(error);
  }
};

doGetUsers();
```

- ## JAVASCRIPT FAKE REST API

- read a single item

``` JS
const getUser = (id) =>
  new Promise((resolve, reject) => {
    const user = users[id];

    if (!user) {
      return setTimeout(
        () => reject(new Error('User not found')),
        250
      );
    }

    setTimeout(() => resolve(users[id]), 250);
  });

// usage
const doGetUsers = async (id) => {
  try {
    const result = await getUser(id);
    console.log(result);
  } catch (error) {
    console.log(error);
  }
};

doGetUsers('1');
```

- create an item

``` JS
const createUser = (data) =>
  new Promise((resolve, reject) => {

    if (!data.firstName || !data.lastName) {
      reject(new Error('Not all information provided'));
    }

    const id = uuidv4();
    const newUser = { id, ...data };

    users = { ...users, [id]: newUser };

    setTimeout(() => resolve(true), 250);

  });

// usage
const doCreateUser = async (data) => {
  try {

    const result = await createUser(data);
    console.log(result);

  } catch (error) {

    console.log(error);

  }
};

doCreateUser({ firstName: 'Tanner', lastName: 'Linsley' });
```

- update an item

``` JS
const updateUser = (id, data) =>
  new Promise((resolve, reject) => {
    if (!users[id]) {
      return setTimeout(
        () => reject(new Error('User not found')),
        250
      );
    }

    users[id] = { ...users[id], ...data };

    return setTimeout(() => resolve(true), 250);
  });

// usage
const doUpdateUser = async (id, data) => {
  try {
    const result = await updateUser(id, data);
    console.log(result);
  } catch (error) {
    console.log(error);
  }
};

doUpdateUser('1', { isDeveloper: false });
```

- delete an item

``` JS
const deleteUser = (id) =>
  new Promise((resolve, reject) => {
    const {
      [id]: user, ...rest
    } = users;

    if (!user) {
      return setTimeout(
        () => reject(new Error('User not found')),
        250
      );
    }

    users = { ...rest };

    return setTimeout(() => resolve(true), 250);
  });

// usage
const doDeleteUser = async (id) => {
  try {
    const result = await deleteUser(id);
    console.log(result);
  } catch (error) {
    console.log(error);
  }
};

doDeleteUser('1');
```

# [How to run a WebPageTest test_202012](https://nooshu.github.io/blog/2020/12/31/how-to-run-a-webpagetest-test/)

- I’m going to examine all the individual settings from the homepage of WebPageTest (WPT). 
- Simple testing tab
  - URL input field
  - Test Configuration
  - Include Repeat View
  - Run Lighthouse Audit
- Advanced Testing tab
  - URL input field
  - Test Location
  - Browser
