# Redux for React

- defining the store
- define presentation components
- define container components
- CRUD

## Get started

 We need to install a couple of dependencies for this:
 
```
yarn add redux react-redux
```
Once we have those we are ready to begin

## Adding Redux to React

We need to do the following to make it work:

- create a store
- expose the store with a Provider
- create a container component

### Creating a store
Creating a store is about creating the needed reducers use a few helper functions to tell Redux about it. Let's have a look at what creating the reducers might look like:

```js
// store.js
import { combineReducers } from 'redux';

const listReducer = (state = [], action) => {
  switch(action.type) {
    case 'CREATE_ITEM':
      return [ ...state, { ...action.payload }];
    case 'REMOVE_ITEM':
      return state.filter(item => item.id !== action.payload.id);
    default:
      return state;
  }
};

const store = combineReducers({
  list: listReducer
});

export default store;

```

Above we have only defined one reducer, in the same file as `store.js` no less. Normally we would define one reducer per file and have them imported into `store.js`. Now we have everything defined in one file to make it easy to understand what is going on. One thing worth noting is our usage of the helper function `combineReducers`. This is the equivalent of writing:

```js
calc = (state, action) => {
  return {
    list: listReducer(state.list, action)
  }
}
```
It's not an exact match but it is pretty much what goes on internally in `combineReducers`. 

### Expose the store via a provider

 
