<div>
  <h1>redux-fast-logger</h1>

  <a href="https://www.npmjs.com/package/fast-redux-logger">
    <img src="https://img.shields.io/npm/dm/fast-redux-logger.svg" alt="npm downloads" />
  </a>
</div>

This is an alternative implementation of redux-logger that should be included directly in your application code.

The goal of `fast-redux-logger` is to remain workable when working with huge stores, at the point `redux-devtools` starts to slow down a bit.

It doesn't have all the features of the real redux-devtools (like time travel), so if you want to use something like that you might still need to use the full redux-devtools. fast-redux-logger is purpose built only for inspecting/debugging action history.

Installation Instructions
---

Add the required middleware and reducer interceptor to your configureStore method, and add the component that will display action history somewhere in your application (probably hidden behind some sort of toggle that you can click in your development environment).

```javascript
// configure store
import { fastLoggerMiddleware, reducerWrapper } from 'fast-redux-logger'

configureStore({
  reducer: reducerWrapper(rootReducer),
  middleware: [fastLoggerMiddleware],
})

// app.tsx
import store from './store'
import { StoreActions } from 'fast-redux-logger'

const [open, setOpen] = useState(false)
return <>
  <Trigger onClick={() => setOpen(true)} />
  <StoreActions isOpen={open} onClose={() => setOpen(false)} store={store} />
</>
```
