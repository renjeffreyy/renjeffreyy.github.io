# React-Redux

[React Redux Documentation](https://react-redux.js.org/introduction/quick-start)

**Getting started**

install redux into your project directory

> npm install react-redux

add the provider `<Provider />` into your app. this makes the redux store available to your entire app

Into the file containing your root element(usually index.js). import provider from react-redux
the file should look something like the below

```javascript
import React from 'react';
import ReactDOM from 'react-dom';

import { Provider } from 'react-redux';
import store from './store';

import App from './App';

const rootElement = document.getElementById('root');
ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  rootElement
);
```

**Note** the provider doesnt have to be in the root element. it just has to wrap around all the react componenets that you want to have access to the store.

I prefer to put the provider in my app.js.

the below also works

```javascript
const App = () => {
  return (
    <Provider store={store}>
      <Router>
        <Fragment>
          <Navbar />
        </Fragment>
      </Router>
    </Provider>
  );
};
```

**create your store**

- import create store and apply middleware. create store creates the store and applymiddleware lets you use middleware in your store.

- if you want to use redux devtools in your browser you can install redux-devtools-extenstion as a dependency

- thunk makes it so you can easily pass your actions in the connect method that will be wrapping each of our componenets

- set your initial state
- create a middleware variable to hold all the middleware that you are going to use in your project

The Below is an example of what your store should look like. you can create your store in the same folder as your index.js depending on the scope of your project

```javascript
import { createStore, applyMiddleware } from 'redux';
import { composeWithDevtools } from 'redux-devtools-extension';
import thunk from 'redux-thunk';
//import from wherever your root reducer is
import rootReducer from './reducers';

const initialState = {};

const middleware = [thunk];

const store = createStore(
  rootReducer,
  initialState,
  composeWithDevtools(applyMiddleware(...middleware))
);

export default store;
```

## Reducers

**Root Reducer**

In the root reducer you combine all your reducers and pass them along to the store.

- usually put all the reducers in their own folder
- the root reducer in the past has been inside the reducer folder as index.js
- import combieReducer from redux
- import all of your other reducers and pass them into combine reducers

**Root Reducer code example**

```javascript
import { combineReducers } from 'redux';
import auth from './auth';
import alert from './alert';
import schedule from './schedule';
import reviews from './reviews.reducer';

export default combineReducers({
  auth,
  alert,
  schedule,
  reviews,
});
```

**Other Reducers**

The other reducers funnel into the root reducer.

- import your action types from your action types file in your actions folder
- I like to create the initial state as an empty array
- we pass in the initial state and the action
- we use a switch statement to handle the different action types

example of reducer

```javascript
import { SET_ALERT, REMOVE_ALERT } from '../actions/types';

const initialState = [];

export default (state = initialState, action) => {
  const { type, payload } = action;

  switch (type) {
    case SET_ALERT:
      return [...state, payload];
    case REMOVE_ALERT:
      return state.filter((alert) => alert.id !== payload);
    default:
      return state;
  }
};
```

## Actions

I put all the actions into a single folder, seperating them by what they do and a single types file

**Action Types**

I like to put all the types into a single folder, assign them to a variable that contains the string of the action.

action Types example

```javascript
export const REGISTER_SUCCESS = 'REGISTER_SUCCESS';
export const USER_LOADED = 'USER_LOADED';
```

**Action Functions**

These are just functions that take in dispatch. dispatch sends your action type and payload to the reducer.

**example of action**

```javascript
export const fetchReviews = () => async (dispatch) => {
  try {
    const reviews = await api.get('/reviews');

    dispatch({
      type: GET_REVIEW,
      payload: reviews.data,
    });
  } catch (error) {
    setAlert('something went wrong with loading the reviews');
    console.log(error);
  }
};
```

**Connecting components to Redux store**

In order for the componenets to have access to the store we need to wrap the component with the connect function.

- We import the connect function from react-redux
- we add the connect function to the export expression at the end of the file
- the connect function takes in 2 arguments
  - map state to props
  - map dispatch to props

**example of connect function**

```javascript
export default connect(mapStateToProps, { setAlert, registerUser })(Register);
```
