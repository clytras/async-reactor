# async-reactor

> Render async Stateless Functional Components

This is a fork to update all dependencies and particular, React 17 and Babel 7.
Test are not working, need lot of refactoring and probably change to Jest.

## Installation

```shell
npm install --save async-reactor
```

## Usage

```js
asyncReactor(component: Function, loader?: Component, error?: Component): Component
```

| name               | type             | description                                     |
|--------------------|------------------|-------------------------------------------------|
| component          | Function (async) | The `async` component you want to render        |
| loader (optionnal) | Component        | Will be shown until the first component renders |
| error (optionnal)  | Component        | Will be shown when an error occurred            |

The returned value is a regular `Component`.

### Examples

This examples are exporting a regular React component.
You can integrate it into an existing application or render it on the page.

See more examples [here](https://github.com/xtuc/async-reactor/tree/master/examples)

#### Using code splitting

```js
import React from 'react'
import {asyncReactor} from 'async-reactor';

function Loader() {
  return (
    <b>Loading ...</b>
  );
}

async function Time() {
  const moment = await import('moment');
  const time = moment();

  return (
    <div>
      {time.format('MM-DD-YYYY')}
    </div>
  );
}

export default asyncReactor(Time, Loader);
```

#### Using fetch

```js
import React from 'react';
import {asyncReactor} from 'async-reactor';

function Loader() {

  return (
    <h2>Loading ...</h2>
  );
}

async function AsyncPosts() {
  const data = await fetch('https://jsonplaceholder.typicode.com/posts');
  const posts = await data.json();

  return (
    <ul>
      {posts.map((x) => <li key={x.id}>{x.title}</li>)}
    </ul>
  );
}

export default asyncReactor(AsyncPosts, Loader);
```
