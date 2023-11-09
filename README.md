#  StorageSculptor: Crafting Convenience with useLocalStorage
StorageSculptor is a custom React hook to simplify the use of the Local Storage API with React's state management system.
<br>
### Official published site: [https://www.npmjs.com/package/use-local-storage-hook-simplified](https://www.npmjs.com/package/use-local-storage-hook-simple)

## Installation:
Before using the hook, ensure that you've installed the package:
```
    npm install use-local-storage-hook-simple

```

## Usage
```
import useLocalStorage from 'use-local-storage-hook-simple';

```

## API

`useLocalStorage(key, initialValue)`

**Parameters**:

- key (string): The key for the local storage entry.
- initialValue (any): An initial value to be set for the key if it doesn't already exist in local storage. This can be of any data type.

**Returns**:

- An array of two items:
1. Current value (reflects the value in local storage and React state)
2. Setter function (to set a new value for both React state and local storage)

## Example

```
import React from 'react';
import useLocalStorage from 'use-local-storage-hook-simple';

function App() {
  const [name, setName] = useLocalStorage('name', 'your_name');

  return (
    <div>
      <input
        value={name}
        onChange={e => setName(e.target.value)}
        placeholder="Enter your name"
      />
      <p>Hello, {name}!</p>
    </div>
  );
}

export default App;

```

> In the above example, the name state will initialize with either the value from local storage (if it exists) or the string `your_name` (replace your_name with the string that you want). When the input changes, it updates the React state and also the local storage.

## Notes
- Local Storage only supports strings. The hook automatically stringifies non-string data types when saving and parses them when retrieving. This makes it possible to store more complex data types, like objects or arrays, without any additional handling in the component.

- If there are existing values in local storage for the provided key, those will be used instead of the initialValue.

- Always ensure that the key you provide is unique and specific enough to avoid unintentionally overwriting other local storage data.

### Extra: WHY we are using WHAT we are using!

Local Storage is a web API that provides a method for web pages to store key-value pairs in a web browser with a much larger limit than cookies. Its limitations and design are influenced by a combination of historical and practical reasons:

1. **Simplicity**: By restricting Local Storage to store only strings, the API remains simple. If you need to store more complex data structures, you can easily serialize them to strings using JSON methods (JSON.stringify() and JSON.parse()) or other serialization techniques.
2. **Consistency Across Browsers**: Limiting the data type to strings ensures a consistent behavior across all web browsers. If the Local Storage API allowed various data types, different browsers might implement these data types differently, leading to inconsistencies.
3. **Historical Precedent**: Cookies, which predate Local Storage, can only store strings as well. When Local Storage was introduced, it made sense to follow a similar pattern, especially since many early use cases for Local Storage were similar to those for cookies (like storing simple settings or identifiers).
4. **Performance**: Serializing and deserializing more complex data types might introduce performance overhead if done automatically by the browser every time data is read from or written to Local Storage. By limiting to strings and leaving serialization/deserialization to developers, the browser ensures maximum performance for the most common use cases.
5. **Avoiding JavaScript Specifics**: By storing only strings, Local Storage avoids tying itself to specific JavaScript implementations or versions. This ensures broader compatibility, even with browsers or environments that might interpret JavaScript objects or arrays differently.
6. **Security and Isolation**: Reducing the data type complexity can mitigate certain types of vulnerabilities or bugs. If browsers had to deal with deserializing more complex data automatically, there could be potential security implications.

**While the string-only design does introduce an extra step when you want to store more complex data types, it's relatively trivial in modern JavaScript to convert back and forth between strings and objects using JSON methods, so this limitation isn't a major hindrance for most applications.**
