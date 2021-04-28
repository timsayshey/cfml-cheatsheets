# API - createStore()
**Why**: it's the base method <br/>
**Return**: a store object







```js
const store = createStore(reducer,state,enhancer)
```


# API - combineReducers()
**Why**: to combine various reducers <br/>
**Arguments**: object with at least two reducers <br/>
**Return**: one reducer to rule them all <br />
```js
const rootReducer = combineReducers({reducerA, reducerB, reducerC})
```


# API - applyMiddleware()

**Why**: to be able to deal with async data<br/>
**Arguments**: a middleWare function <br/>
**Return**: a store enhancer
<!-- * We can create a custom middleware to keep it simple.  -->

```js
const store = createStore(reducer,state, applyMiddleware(yourMiddleware))
```


# API - bindActionCreators()

**Why**: to pass action creators to a component that isn't aware of Redux and you don't want to pass dispatch <br/>
**Arguments**: an action creator and a dispatch function avaible on the store <br/>
**Return**: a dispatch function mutated with the passeds action creators

```js
bindActionCreators(YoursActionsCreators, dispatch)
```
