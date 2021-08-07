---
description: react global state management library
---

# Redux

## Redux

component에 종속되지 않고 global state management를 합니다. props지옥을 탈출할 수 있습니다.

### Flux pattern

redux는 기본적으로 flux 패턴을 따릅니다.

> Action -&gt; Dispatch -&gt; Store -&gt; View

### Installation

```bash
yarn add redux react-redux redux-devtools-extension @reduxjs/toolkit
```

### Reducer definition

reducer는 꼭 불변성을 지켜야 합니다. 그래야 redux가 이전 상태와 바뀐 상태를 구분할 수 있습니다. 왜냐하면 참조 값이 바뀌었는지를 가지고 변경 여부를 판단하고, 바뀌었다고 판단해야 re-render가 일어납니다.

1. Root reducer definition

   ```javascript
   // libraries
   import { applyMiddleware, combineReducers, compose, createStore } from 'redux';
   import { composeWithDevTools } from 'redux-devtools-extension';

   // customs
   import branchManagementReducer from 'modules/branch/reducer/branchManagement.reducer';

   const rootReducer = combineReducers({
     branchManage: branchManagementReducer,
   });

   const middleware = applyMiddleware();
   const enhancer =
     process.env.NEXT_PUBLIC_ENV_NODE === 'production'
       ? compose(middleware)
       : composeWithDevTools(middleware);

   export const store = createStore(rootReducer, enhancer);
   ```

2. detailed reducer definition

   ```javascript
   // store/counter.js

   const SET_DIFF = 'counter/SET_DIFF';
   const INCREASE = 'counter/INCREASE';
   const DECREASE = 'counter/DECREASE';

   export const setDiff = diff => ({ type: SET_DIFF, diff });
   export const increase = () => ({ type: INCREASE });
   export const decrease = () => ({ type: DECREASE });

   const initialState = {
     number: 0,
     diff: 1
   };

   export default function counter(state = initialState, action) {
     switch(action.type) {
       case SET_DIFF:
         return {
           ...state,
           diff: action.diff
         };
       case INCREASE:
         return {
           ...state,
           number: state.number + state.diff
         };
       case DECREASE:
         return {
           ...state,
           number: state.number - state.diff
         };
       default:
         return state;
     }
   }
   ```

3. 전역 컴포넌트에 store 생성하고 반영하기

   ```javascript
   import React from 'react';
   import ReactDOM from 'react-dom';
   import App from './App';
   import { Provider } from 'react-redux';
   import store from 'store';

   // import './excercise';

   ReactDOM.render(
     <React.StrictMode>
       <Provider store={store}>
         <App />
       </Provider>
     </React.StrictMode>,
     document.getElementById('root')
   );

   // If you want to start measuring performance in your app, pass a function
   // to log results (for example: reportWebVitals(console.log))
   // or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
   reportWebVitals();
   ```

## [Redux-toolkit](https://redux-toolkit.js.org/usage/usage-guide)

1. Root reducer definition

   ```javascript
   // libraries
   import { configureStore } from '@reduxjs/toolkit';

   // customs
   import branchManagementReducer from 'modules/branch/reducer/branchManagement.reducer';

   export const store = configureStore({
     reducer: {
       branchManage: branchManagementReducer,
     },
     devTools: process.env.NEXT_PUBLIC_ENV_NODE !== 'production',
   }); 
   ```

2. detailed reducer definition

   ```typescript
   // libraries
   import { createSlice } from '@reduxjs/toolkit';

   interface State {
     brandInfoDetail: {
       [key: string]: unknown;
     };
   }

   const initialState: State = {
     brandInfoDetail: {},
   };

   const slice = createSlice({
     name: 'branchManagement',
     initialState,
     reducers: {
       updateBranchInfoDetail(state, action) {
         state.brandInfoDetail = action.payload;
       },
     },
   });

   export const { updateBranchInfoDetail } = slice.actions;
   export default slice.reducer;
   ```

3. dispatch

   ```typescript

   ```

4. 5. 6. 
## [Redux-persist](https://github.com/rt2zz/redux-persist)

redux-persist는 browser storage에도 저장하여 새로고침하여도 데이터가 유실되지 않는 라이브러리 입니다.

### Installation

```bash
yarn add redux-persist
```

### Configure

```javascript
// store/index.js
import { createStore, combineReducers, applyMiddleware, compose } from 'redux';
import { composeWithDevTools } from 'redux-devtools-extension';
import { persistStore, persistReducer } from 'redux-persist';
// import storage from 'redux-persist/lib/storage'; // local storage
import storageSession from 'redux-persist/lib/storage/session';

import counter from './counter';
import todos from './todos';

// 전역으로 persist 쓰고자 할 
// const persistConfig = {
//   key: 'root',
//   storage: storageSession,
//   // whitelist: [], // whitelist에 있는 값들만 persist한다.
//   // blacklist: [], // blacklist에 있는 거 빼고 전부 persist한다.
// };

const persistConfig = {
  key: 'counter',
  storage: storageSession,
  // whitelist: [], // whitelist에 있는 값들만 persist한다.
  // blacklist: [], // blacklist에 있는 거 빼고 전부 persist한다.
};

const rootReducer = combineReducers({
  counter: persistReducer(persistConfig, counter),
  todos
});

// const persistedReducer = persistReducer(persistConfig, rootReducer); // 전역으로 persist쓰고자 할 때

const middlewares = []; // 미들웨어들을 넣으면 된다.

const enhancer =
  process.env.NEXT_PUBLIC_NODE_ENV === 'production'
    ? compose(applyMiddleware(...middlewares))
    : composeWithDevTools(applyMiddleware(...middlewares));

const configureStore = () => {
  let store = createStore(rootReducer, enhancer);
  let persistor = persistStore(store);
  return { store, persistor }
}

export default configureStore;
```

```javascript
// _app.jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import { Provider } from 'react-redux';
import { PersistGate } from 'redux-persist/integration/react'
import configureStore from './store';

const { store, persistor } = configureStore();

ReactDOM.render(
  <React.StrictMode>
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistor}>
        <App />
      </PersistGate>
    </Provider>
  </React.StrictMode>,
  document.getElementById('root')
);

```

## redux-toolkit

reference: [https://kyounghwan01.github.io/blog/React/redux/redux-toolkit/\#%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%B2](https://kyounghwan01.github.io/blog/React/redux/redux-toolkit/#%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%92%E1%85%A1%E1%84%82%E1%85%B3%E1%86%AB-%E1%84%8B%E1%85%B5%E1%84%8B%E1%85%B2)

