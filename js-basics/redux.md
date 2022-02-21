# Store

```js
/store
    index.js // Main file where the store is configured and slices are imported
    /slices
        userSlice.js
        counterSlice.js

```

Create `/store/index.js`, the entry point for all `slices`:

```js
import { confirgureStore } from "@reduxjs/toolkit";
import userReducer from "./slices/userSlice";
import counterReducer from "./slices/counterSlice";

export default configureStore({
  reducer: {
    user: userReducer,
    counter: counterReducer,
  },
});
```

Use `Provider` to wrap the app giving access to the `store` and all its `slices` throughout the application:

`/pages/_app.js`:

```js
import "../styles/globals.css";
import { store } from "../store";
import { Provider } from "react-redux";

function MyApp({ Component, pageProps }) {
  <Provider store={store}>
    <Component {...pageProps} />
  </Provider>;
}

export default MyApp;
```

create slices:

```js
import { createSlice } from '@reduxjs/toolkit'

export const counterSlice = createSlice({
  name: 'counter',
  initialState: {
      count: 0
  }
  reducers: {
    increment: (state) => {
      state.count += 1
    },
    decrement: (state) => {
      state.count -= 1
    },
    incrementByAmount: (state, action) => {
      state.count += action.payload
    },
  },
})

// Action creators are generated for each reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```

Slices within components:

```js
import React from "react";
import { useSelector, useDispatch } from "react-redux";
import { decrement, increment } from "../../store/slices/counterSlice";

export function Counter() {
  const { count } = useSelector((state) => state.counter);
  const dispatch = useDispatch();

  return (
    <div>
      <div>
        <button
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          Increment
        </button>
        <span>{count}</span>
        <button
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </button>
      </div>
    </div>
  );
}
```
