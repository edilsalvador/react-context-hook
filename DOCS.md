<!-- Generated by documentation.js. Update this documentation by updating the source code. -->

### Table of Contents

-   [createStore][1]
    -   [Parameters][2]
    -   [Examples][3]
-   [useStore][4]
    -   [Parameters][5]
    -   [Examples][6]
-   [useStoreState][7]
    -   [Examples][8]
-   [useSetStoreValue][9]
    -   [Parameters][10]
    -   [Examples][11]
-   [useDeleteStoreValue][12]
    -   [Parameters][13]
    -   [Examples][14]
-   [useGetAndset][15]
    -   [Parameters][16]
    -   [Examples][17]
-   [useGetAndDelete][18]
    -   [Parameters][19]
    -   [Examples][20]
-   [useSetAndDelete][21]
    -   [Parameters][22]
    -   [Examples][23]
-   [useStoreValue][24]
    -   [Parameters][25]

## createStore

### Parameters

-   `WrappedComponent` **ReactElement** the component to connect with the store
-   `initialValue` **[Object][26]** the initial store value or nothing
-   `config` **[Object][26]** the custom configuration. If nothing is passed will use the default config
    -   `config.listener` **[Function][27]** a function that is triggered each time the store is modified.
    -   `config.proxyStore` **[boolean][28]** default `true` - if true the store will be protected by a Proxy. Set to false if your environment does not support Proxy. If you use `react-context-hook` in the browser set it to true

### Examples

```javascript
const initialState = { count: 10 }

const storeConfig = {
 listener: state => {
   console.log('state changed', state)
 },
 logging: true //process.env.NODE_ENV !== 'production'
}

export default createStore(App, initialState, storeConfig)
```

## useStore

### Parameters

-   `key` **[string][29]** The lookup key to find the saved value in the store
-   `defaultValue` **any** The value if the value in the store is missing
-   `createIfMissing` **[boolean][28]** if true and the data is missing it will be created in the store

### Examples

```javascript
import {useStore} from 'react-context-hook'
const [username, setUsername, deleteUsername] = useStore('username')
<div>hello {username}</div>
<button onClick={()=> setUsername('my_username')}>set username</button>
```

Returns **[array][30]** an array with length 3:<br>
position 0 - the value of the data in the store.<br>
position 1 - a function _setValue_ to modify the data in the store. When used, this function return a promise that resolve nothing, thus you can use `setValue('a value').then(() => {doSomething() //when the store did update})`<br>
position 2 - a function _deleteValue_ to delete the value from the store. When used, this function return a promise that resolve nothing, thus you can use `deleteValue('a value').then(() => {doSomething() //when the store did update})`

## useStoreState

Returns the whole store value, with all the variables stored in it. Changes to this object will not change the store

### Examples

```javascript
import {useStoreState} from 'react-context-hook'
const store = useStoreState()
console.log('the store is', JSON.stringify(store))
```

Returns **[object][26]** An object representing the whole store value in read only mode.

## useSetStoreValue

Returns a function to set or update a variable in the store. You want to use this hook when you just need to modify the store, not read or delete a value from it.

### Parameters

-   `key` **[string][29]** the name of the variable to set in the store

### Examples

```javascript
import {useSetStoreValue} from 'react-context-hook'
const setUsername = useSetStoreValue('username')
<button onClick={()=> setUsername('my_username')}>set username</button>
```

Returns **[Function][27]** a function to set a variable in the store with the given name When used, this function return a promise that resolve nothing, thus you can use `setValue('a value').then(() => {doSomething() //when the store did update})`

## useDeleteStoreValue

Returns a function to delete a variable in the store. You want to use this hook when you just need to delete a value in the store, not read or set a value from it.

### Parameters

-   `key` **[string][29]** the name of the variable to set in the store

### Examples

```javascript
import {useDeleteStoreValue} from 'react-context-hook'
const deleteUsername = useDeleteStoreValue('username')
<button onClick={()=> deleteUsername('my_username')}>set username</button>
```

Returns **[Function][27]** a function to delete a variable in the store with the given name. When used, this function return a promise that resolve nothing, thus you can use `deleteValue('a value').then(() => {doSomething() //when the store did update})`

## useGetAndset

This React hook returns an array to read and modify a value in the store:
`const [value, setValue] = useGetAndset('a_lookup_key_in_the_store')`. The name of the variable in the arry is arbitrary and you can choose any string you like.

### Parameters

-   `key` **[string][29]** The lookup key to find the saved value in the store

### Examples

```javascript
import {useGetAndset} from 'react-context-hook'
const [username, setUsername] = useGetAndset('username')
<div>hello {username}</div>
<button onClick={()=> setUsername('my_username')}>set username</button>

 const [value, setValue] = useGetAndset('a_lookup_key_in_the_store')
```

Returns **[array][30]** an array with length 2:<br>
position 0 - the value of the data in the store.<br>
position 1 - a function _setValue_ to modify the data in the store. When used, this function return a promise that resolve nothing, thus you can use `setValue('a value').then(() => {doSomething() //when the store did update})`<br>

## useGetAndDelete

This React hook returns an array to read and delete a value in the store:
`const [value, deleteValue] = useGetAndDelete('a_lookup_key_in_the_store')`. The name of the variable in the arry is arbitrary and you can choose any string you like.

### Parameters

-   `key` **[string][29]** The lookup key to find the saved value in the store

### Examples

```javascript
import {useGetAndDelete} from 'react-context-hook'
const [username, deleteUsername] = useGetAndDelete('username')
<div>hello {username}</div>
<button onClick={()=> deleteUsername('my_username')}>set username</button>
```

Returns **[array][30]** an array with length 2:<br>
position 0 - the value of the data in the store.<br>
position 1 - a function _deleteValue_ to delete the data in the store. When used, this function return a promise that resolve nothing, thus you can use `deleteValue('a value').then(() => {doSomething() //when the store did update})`<br>

## useSetAndDelete

This React hook returns an array to set and delete a value in the store:
`const [setValue, deleteValue] = useGetAndDelete('a_lookup_key_in_the_store')`. The name of the variable in the arry is arbitrary and you can choose any string you like.

### Parameters

-   `key` **[string][29]** The lookup key to find the saved value in the store

### Examples

```javascript
import {useGetAndDelete} from 'react-context-hook'
const [username, deleteUsername] = useGetAndDelete('username')
<div>hello {username}</div>
<button onClick={()=> deleteUsername('my_username')}>set username</button>
```

Returns **[array][30]** an array with length 2:<br>
position 0 - a function _setValue_ to modify the data in the store. When used, this function return a promise that resolve nothing, thus you can use `setValue('a value').then(() => {doSomething() //when the store did update})`<br>
position 1 - a function _deleteValue_ to delete the data in the store. When used, this function return a promise that resolve nothing, thus you can use `deleteValue('a value').then(() => {doSomething() //when the store did update})`<br>

## useStoreValue

### Parameters

-   `key` **[string][29]** the name of the variable / value to be retrieved in the global store.
-   `defaultValue` **any?** an optional default value, if the value in the global store is not present.

Returns **any** the value on the global store, or the default value if passed, or `undefined`

[1]: #createstore

[2]: #parameters

[3]: #examples

[4]: #usestore

[5]: #parameters-1

[6]: #examples-1

[7]: #usestorestate

[8]: #examples-2

[9]: #usesetstorevalue

[10]: #parameters-2

[11]: #examples-3

[12]: #usedeletestorevalue

[13]: #parameters-3

[14]: #examples-4

[15]: #usegetandset

[16]: #parameters-4

[17]: #examples-5

[18]: #usegetanddelete

[19]: #parameters-5

[20]: #examples-6

[21]: #usesetanddelete

[22]: #parameters-6

[23]: #examples-7

[24]: #usestorevalue

[25]: #parameters-7

[26]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Object

[27]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/function

[28]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Boolean

[29]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String

[30]: https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Array