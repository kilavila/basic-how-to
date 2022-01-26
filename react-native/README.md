# React Native tags

## View

Import

```js
import { View } from 'react-native';
```

Usage

```html
<View style={styles.className}>
    ...
</View>
```

Use `View` to make layouts similar to HTML's `div` tag.

---

## Text

Import

```js
import { Text } from 'react-native';
```

Usage

```html
<Text style={styles.className}>
    Some paragraph
</Text>
```

All text must be rendered inside a `Text` tag.

---

## Buttons

Import

```js
import { Button } from 'react-native';
```

Usage

```html
<Button title='Click me'
        color='orange'
        onPress={() => {
            // run functions
        }}
/>
```

The button can't have a style like the other tags, which means we can't style it.<br>
We can however do a workaround, after all we might want a text, card or image to be clickable.<br>

```js
import { Text, TouchableOpacity } from 'react-native';
```

```html
<TouchableOpacity style={styles.button}
                  onPress={() => {
                      // run functions
                  }}
>
    <Text>
        Click me
    </Text>
</TouchableOpacity>
```

TouchableOpacity allows us to make a view with an onPress just like the button, here we can add styles.<br>
We get an opacity feedback on this view, if we don't want that then we can use `TouchableWithoutFeedback`.

```js
import { TouchableWithoutFeedback } from 'react-native';
```

Set it up and use it the same way as the TouchableOpacity.

---
<br>
<br>

# Custom components

## Parameters

Send `parameters` from one component to another.

```js
// App.js

import { Header } from './Header';

export default function App() {
    return (
        <View>
            <Header title='Some title'
                    description='Some description'
            />
        </View>
    );
}
```

```js
// Header.js

export default function Header({ title, description }) {
    return (
        <View>
            <Text>
                { title }
            </Text>
            <Text>
                { description }
            </Text>
        </View>
    );
}
```

We render the Header in App.js, but we add two parameters; title and description.<br>
In this case we use plain strings: `'string'`<br>
But we could easily use a variable: `{variableName}`

In Header.js we take in the parameters in the Header function.<br>
We can now use these variables inside this functional component.

---
<br>
<br>

# React Native functionality

## State (useState)

Import `useState` from `react` like shown below

```js
import React, { useState } from 'react';
```

We can now create states in the app, and update these states.<br>
We use this when making dynamic content.

```js
export default function App() {
    const [name, setName] = useState('John');

    const changeName = () => {
        setName('Jane');
    }

    return (
        <View>
            <Button title={name} onPress={() => changeName()} />
        </View>
    );
}
```

Initially the variable `name` has the value `John`.<br>
The title of the button is the name variable, and the buttons `onPress` function creates an anonymous `arrow function`, which in turn calls the `changeName function`.<br>
The changeName function then has the `setName function` inside it, it is this one that changes the name of the variable from John to `Jane`.

Another way to do the same thing:

```js
export default function App() {
    const [name, setName] = useState('John');

    return (
        <View>
            <Button title={name} onPress={() => setName('Jane')} />
        </View>
    );
}
```

In this case the second example is a better way of doing it.<br>
If this component was much bigger and more complicated the first example would probably be better.<br>
The first example would also be much better if we were running multiple functions, using animations or just doing more stuff in general.<br>
This is a way of keeping the code clean, and you can look at it this way:

```
IMPORTS

FUNCTIONS

ITEMS TO RENDER

STYLES
```

Each part can be long and complicated, if we had all our functions mixed in with the items we render then it would take longer to read and edit the code.

---

## Effect (useEffect)

Import `useEffect` from `react`.

```js
import React, { useState, useEffect } from 'react';
```

Syntax

```js
export default function App() {
    useEffect(() => {
        ...
    }, []);

    return (
        ...
    );
}
```

In vanilla Javascript we `defer` a script to run it on page load.<br>
In React Native we need `useEffect`, and everything we add inside this arrow function will run when we render the view.

The empty array: `[]` at the end of the useEffect function makes sure that we only run this on load(mount) and on destroy(unmount). We can add logic here to run it on timer, if something is true or triggered etc.

Take a look at the example below.

```js
import React, { useState, useEffect } from 'react';
import { Button, StyleSheet View } from 'react-native';

export default function App() {
    const [name, setName] = useState('John');

    const firstFunction = () => {
        setName('Jane');
    }

    const secondFunction = () => {
        setName('Mary');
    }

    useEffect(() => {
        firstFunction();
        // add functions here
    }, []);

    return (
        <View style={styles.container}>
            <Button title={name}
                    onPress={() => secondFunction()}
            />
        </View>
    );

    const styles = StyleSheet.create({
        container: {
            flex: 1,
            alignItems: 'center',
            justifyContent: 'center'
        }
    });
}
```

We have a name variable.<br>
We have 2 functions; `firstFunction` which changes the name from John to Jane, and `secondFunction` which would change the name to Mary.<br>
Below we have the `useEffect` with the `firstFunction` inside. `firstFunction` will run as we render the view, we won't see the name John, because the name variable has been changed to Jane immediately.<br>
`secondFunction` won't run until the user clicks the button.