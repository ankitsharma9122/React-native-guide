## SafeAreaView

SafeAreaView is a component that ensures content is rendered within the safe boundaries of a device’s screen, avoiding areas like the notch, status bar, home indicator, or curved screen edges.

```js
import React from 'react';
import { SafeAreaView, Text, StyleSheet } from 'react-native';

const MyScreen = () => {
  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Welcome to My App</Text>
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
  },
  title: {
    fontSize: 24,
    marginTop: 20,
  },
});

export default MyScreen;

```
## Text 
This  component is used to display and style text — it’s the equivalent of `<p>, <span>, or <h1>` in HTML, but with mobile-friendly behavior.

Text must be wrapped in `<Text>` to be rendered — you can't place raw strings inside `<View>` directly.

```js
 <View style={styles.container}>
      <Text style={styles.heading}>Hello, React Native!</Text>
      <Text style={styles.paragraph}>This is a paragraph of text.</Text>
    </View>
```

| Prop                   | Type                                        | Description                                     |
| ---------------------- | ------------------------------------------- | ----------------------------------------------- |
| `style`                | `object` or `array`                         | Style the text (color, size, weight, etc.)      |
| `numberOfLines`        | `number`                                    | Limits text to a certain number of lines        |
| `ellipsizeMode`        | `'head'` / `'middle'` / `'tail'` / `'clip'` | How to truncate text if it overflows            |
| `selectable`           | `boolean`                                   | Allow users to select/copy text                 |
| `onPress`              | `function`                                  | Handle tap events on text (like a link)         |
| `adjustsFontSizeToFit` | `boolean`                                   | Shrinks text to fit its container (iOS/Android) |


## View 

The `<View>` component is the fundamental building block for layout and UI design — similar to a `<div>` in HTML.

```js
<View style={styles.container}>
      <View style={styles.box}>
        <Text>Hello inside a View</Text>
      </View>
    </View>
```

| Prop            | Type               | Description                                        |
| --------------- | ------------------ | -------------------------------------------------- |
| `style`         | `object` / `array` | Controls layout, color, borders, etc.              |
| `onLayout`      | `function`         | Called when layout changes (gives size & position) |
| `pointerEvents` | `string`           | Controls if the view receives touch events         |
| `accessible`    | `boolean`          | Makes view accessible for screen readers           |


## TextInput

```js
 <TextInput
        style={styles.input}
        placeholder="Type here..."
        value={text}
        onChangeText={setText}
      />
```

| Prop              | Type       | Description                                            |
| ----------------- | ---------- | ------------------------------------------------------ |
| `value`           | `string`   | The current value of the input                         |
| `onChangeText`    | `function` | Called when the text changes                           |
| `placeholder`     | `string`   | Gray hint text when empty                              |
| `secureTextEntry` | `boolean`  | Hides input (for passwords)                            |
| `keyboardType`    | `string`   | Type of keyboard (e.g. `'numeric'`, `'email-address'`) |
| `multiline`       | `boolean`  | Enables multi-line input                               |
| `maxLength`       | `number`   | Limits number of characters                            |
| `editable`        | `boolean`  | Disables input when false                              |
| `autoFocus`       | `boolean`  | Focuses input on mount                                 |


## Button

- **Use Case:** Simple, out-of-the-box button.
- **Customization:** Minimal (title, onPress, color).
  

```jsx
import { Button } from 'react-native';

<Button
  title="Click Me"
  onPress={() => alert('Pressed!')}
  touchSoundDisabled
/>
```

## Pressable
- **Use Case:** Fully customizable button or touchable element.
- **Customization:**  High (e.g., press feedback, hover effects).

```js
<Pressable
  onPress={(event) => {
  console.log(event.nativeEvent);
  }}
  onLongPress={() => console.log('Long Pressed')}
  style={({ pressed }) => ({
    backgroundColor: pressed ? '#aaa' : '#4CAF50',
    padding: 10,
    borderRadius: 5,
  })}
>
  <Text style={{ color: '#fff' }}>Submit</Text>
</Pressable>
```

Note : so pressable have more flexibility over button.

# FlatList

`FlatList` is an efficient way to render large, scrollable lists in React Native. It only renders items that are visible on screen, improving performance, especially for large datasets.

in-house functionality : virtualization,refreshing, and pagination and Better for long lists compared to .map() in a ScrollView.

## Example:

```jsx
import React, { useState } from 'react';
import { FlatList, Text, View, StyleSheet, RefreshControl } from 'react-native';

const DATA = [
  { id: '1', title: 'Apple' },
  { id: '2', title: 'Banana' },
  { id: '3', title: 'Cherry' },
];

const App = () => {
  const [refreshing, setRefreshing] = useState(false);
  const [data, setData] = useState(DATA);

  const onRefresh = () => {
    setRefreshing(true);
    // Simulate a data refresh operation (e.g., fetching data from an API)
    setTimeout(() => {
      setRefreshing(false);
      // Optionally, you can update the data here
    }, 2000);
  };

  const renderItem = ({ item }) => (
    <View style={styles.item}>
      <Text style={styles.title}>{item.title}</Text>
    </View>
  );

  return (
    <FlatList
      data={data}
      renderItem={renderItem}
      keyExtractor={(item) => item.id}
      refreshControl={
        <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
      }
    />
  );
};

const styles = StyleSheet.create({
  item: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#ccc',
  },
  title: {
    fontSize: 18,
  },
});

export default App;
```

| Prop                     | Description                                       |
| ------------------------ | ------------------------------------------------- |
| `data`                   | Array of items to render                          |
| `renderItem`             | Function to render each item                      |
| `keyExtractor`           | Returns a unique key for each item                |
| `ItemSeparatorComponent` | Renders a separator between items                 |
| `ListHeaderComponent`    | Adds a header above the list                      |
| `onEndReached`           | Called when the end is near (for infinite scroll) |
| `refreshing`             | Boolean for pull-to-refresh state                 |
| `onRefresh`              | Function triggered on pull-to-refresh             |
| `horizontal`             | Makes the list scroll horizontally                |

##  Image

Displaying an image is done using the built-in `<Image>` component.

```js
import React from 'react';
import { Image, View, StyleSheet } from 'react-native';

const App = () => {
  return (
    <View style={styles.container}>
      <Image
        source={{ uri: 'https://reactnative.dev/img/tiny_logo.png' }}
        style={styles.image}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  image: {
    width: 100,
    height: 100,
  },
});

export default App;

```

**Source Url :**
| Type               | `source` Format                                                         |
| ------------------ | ----------------------------------------------------------------------- |
| **Remote**         | `{ uri: 'https://example.com/image.png' }`                              |
| **Local (static)** | `require('./assets/image.png')` – only works for static, bundled assets |
| **Base64**         | `{ uri: 'data:image/png;base64,...' }`                                  |


**Properties :**

| Prop            | Description                                                                                 |
| --------------- | ------------------------------------------------------------------------------------------- |
| `source`        | Required. Image source, either local or remote                                              |
| `style`         | Set image size and styling (must set `width` and `height`)                                  |
| `resizeMode`    | Defines how to scale the image: `'cover'`, `'contain'`, `'stretch'`, `'center'`, `'repeat'` |
| `onLoad`        | Callback when image is loaded                                                               |
| `onError`       | Callback if image fails to load                                                             |
| `defaultSource` | Local placeholder image (iOS only: It improves user experience by avoiding a blank space during loading. like a fallback of lazy loading)                                                          |

## ImageBackground
```js
import React from 'react';
import { ImageBackground, Text, StyleSheet } from 'react-native';

const App = () => {
  return (
    <ImageBackground
      source={{ uri: 'https://example.com/background.jpg' }}
      style={styles.background}
       imageRef={imgRef}// instead of ref key, here imageRef used
    >
      <Text style={styles.text}>Hello, world!</Text>
    </ImageBackground>
  );
};

const styles = StyleSheet.create({
  background: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    color: '#fff',
    fontSize: 24,
    fontWeight: 'bold',
  },
});

export default App;

```

**Properties:**
| Prop         | Description                                   |
| ------------ | --------------------------------------------- |
| `source`     | Image source (local or remote)                |
| `style`      | Style for the container                       |
| `resizeMode` | `'cover'`, `'contain'`, `'stretch'`, etc.     |
| `imageStyle` | Style applied to the actual image inside      |
| `children`   | Any nested components you want over the image |

Properties are almost similar to Image.


## KeyboardAvoidingView
UI automatically adjust or "move" when the on-screen keyboard appears—preventing input fields from being hidden behind the keyboard.

```js
import { KeyboardAvoidingView, TextInput, Platform } from 'react-native';

<KeyboardAvoidingView
  style={{ flex: 1 }}
  behavior={Platform.OS === 'ios' ? 'padding' : 'height'}
>
  <TextInput placeholder="Type here..." />
</KeyboardAvoidingView>

```

React Native’s KeyboardAvoidingView behaves differently on each platform, so:

| Platform    | Recommended behavior | Why                                                                 |
| ----------- | ---------------------- | ------------------------------------------------------------------- |
| **iOS**     | `'padding'`            | Smoothly pushes content up above the keyboard                       |
| **Android** | `'height'`             | Resizes the view's height properly (padding doesn’t work well here) |


## Modal 

Modal component is a built-in way to display content on top of the current screen, blocking interaction with the rest of the UI until the modal is dismissed.

```js
import React, { useState } from 'react';
import { Modal, View, Text, Button, StyleSheet } from 'react-native';

const App = () => {
  const [visible, setVisible] = useState(false);

  return (
    <View style={styles.container}>
      <Button title="Open Modal" onPress={() => setVisible(true)} />

      <Modal
        visible={visible}
        animationType="slide" // 'slide', 'fade', or 'none'
        transparent={true} // Makes background transparent
        onRequestClose={() => setVisible(false)} // Android back button support
      >
        <View style={styles.modalBackground}>
          <View style={styles.modalContent}>
            <Text>This is a modal!</Text>
            <Button title="Close" onPress={() => setVisible(false)} />
          </View>
        </View>
      </Modal>
    </View>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', alignItems: 'center' },
  modalBackground: {
    flex: 1,
    backgroundColor: 'rgba(0,0,0,0.5)', // Dimmed background
    justifyContent: 'center',
    alignItems: 'center',
  },
  modalContent: {
    backgroundColor: 'white',
    padding: 20,
    borderRadius: 10,
    width: '80%',
  },
});

export default App;

```

| Prop                | Description                                           |
| ------------------- | ----------------------------------------------------- |
| `visible`           | Controls whether the modal is shown or hidden         |
| `animationType`     | `'none'`, `'slide'`, or `'fade'`                      |
| `transparent`       | Makes the modal background transparent                |
| `onRequestClose`    | Required on Android — handles hardware back button    |
| `presentationStyle` | iOS only — can be `'fullScreen'`, `'pageSheet'`, etc. |

## refreshControl

it used inside a ScrollView or ListView to add pull to refresh functionality. When the ScrollView is at scrollY: 0, swiping down triggers an onRefresh event.

```js
import React from 'react';
import {RefreshControl, ScrollView, StyleSheet, Text,SafeAreaView} from 'react-native';

const App = () => {
  const [refreshing, setRefreshing] = React.useState(false);
  const onRefresh = React.useCallback(() => {
    setRefreshing(true);
    setTimeout(() => {
      setRefreshing(false);
    }, 2000);
  }, []);

  return (
      <SafeAreaView style={styles.container}>
        <ScrollView
          contentContainerStyle={styles.scrollView}
          refreshControl={
            <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
          }>
          <Text>Pull down to see RefreshControl indicator</Text>
        </ScrollView>
      </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  scrollView: {
    flex: 1,
    backgroundColor: 'pink',
    alignItems: 'center',
    justifyContent: 'center',
  },
});

export default App;
```

| Prop                 | Type       | Platform | Description                                                                           |
| -------------------- | ---------- | -------- | ------------------------------------------------------------------------------------- |
| `refreshing`         | `boolean`  | All      | **Required.** Shows/hides the refresh indicator. Must be controlled via state.        |
| `onRefresh`          | `function` | All      | Called when a pull-to-refresh is triggered. Use this to run logic like fetching data. |
| `enabled`            | `boolean`  | Android  | Enables/disables pull-to-refresh interaction. Default: `true`.                        |
| `colors`             | `string[]` | Android  | Array of color strings used in the loading spinner (e.g. `['red', 'blue']`).          |
| `tintColor`          | `string`   | iOS      | Color of the spinner (iOS only).                                                      |
| `title`              | `string`   | iOS      | Text shown under the spinner.                                                         |
| `titleColor`         | `string`   | iOS      | Color of the `title` text.                                                            |
| `progressViewOffset` | `number`   | Android  | How far the refresh indicator is from the top.                                        |

## scrollView 

The ScrollView in React Native is a built-in component that lets you scroll vertically or horizontally through a list of components or content that doesn't fit on the screen.

```js
<ScrollView style={styles.scrollView}>
        <Text style={styles.text}>
          culpa qui officia deserunt mollit anim id est laborum.
        </Text>
      </ScrollView>
```

| Prop                           | Type                                   | Description                                      |
| ------------------------------ | -------------------------------------- | ------------------------------------------------ |
| `stickyHeaderIndices`          | `number[]`                             | Indices of children that should stick to the top |
| `horizontal`                   | `boolean`                              | Enable horizontal scrolling                      |
| `contentContainerStyle`        | `object`                               | Styles the inner scrollable area                 |
| `showsVerticalScrollIndicator` | `boolean`                              | Show/hide the scrollbar                          |
| `refreshControl`               | `ReactElement`                         | Add pull-to-refresh logic                        |
| `keyboardShouldPersistTaps`    | `'never'` \| `'handled'` \| `'always'` | Controls keyboard dismissal behavior             |


## SectionList

The SectionList component in React Native is a powerful way to display grouped (sectioned) lists — like a list of contacts grouped by the first letter of their names, or settings grouped by categories.

Better than FlatList when you need `headers per group`

```js
import React from 'react';
import { SectionList, Text, View, StyleSheet } from 'react-native';

const DATA = [
  {
    title: 'Fruits',
    data: ['Apple', 'Banana', 'Mango'],
  },
  {
    title: 'Vegetables',
    data: ['Carrot', 'Spinach', 'Tomato'],
  },
];

const App = () => {
  return (
    <SectionList
      sections={DATA}
      keyExtractor={(item, index) => item + index}
      renderItem={({ item }) => <Text style={styles.item}>{item}</Text>}
      renderSectionHeader={({ section: { title } }) => (
        <Text style={styles.header}>{title}</Text>
      )}
    />
  );
};
export default App;

```

| Prop                          | Type       | Description                                                   |
| ----------------------------- | ---------- | ------------------------------------------------------------- |
| `sections`                    | `Array`    | Required. Each section must have a `title` and `data` array.  |
| `renderItem`                  | `function` | How to render each item inside a section.                     |
| `renderSectionHeader`         | `function` | How to render the header for each section.                    |
| `keyExtractor`                | `function` | Unique key for each item.                                     |


## switch 
the Switch component is a built-in UI control used for binary on/off toggles — similar to a checkbox or toggle switch in web apps.

```js
 <Switch
        trackColor={{ false: '#767577', true: '#81b0ff' }}
        thumbColor={isEnabled ? '#f5dd4b' : '#f4f3f4'}
        ios_backgroundColor="#3e3e3e"
        onValueChange={toggleSwitch}
        value={isEnabled}
      />
```


## TouchableHighlight

 TouchableHighlight is a pressable component used to wrap views (like Text, Image, etc.) that respond to touch by darkening (or showing a custom underlay color) when pressed.

 ```js
  <TouchableHighlight
        onPress={handlePress}
        underlayColor="#DDDDDD"
        style={styles.button}
      >
        <Text style={styles.buttonText}>Touch Me</Text>
      </TouchableHighlight>
 ```

 | Prop                                | Type       | Description                                           |
| ----------------------------------- | ---------- | ----------------------------------------------------- |
| `onPress`                           | `function` | Called when pressed                                   |
| `underlayColor`                     | `string`   | Background color shown on press                       |
| `activeOpacity`                     | `number`   | Opacity of child when pressed (if no `underlayColor`) |
| `style`                             | `object`   | Styles the outer wrapper                              |
| `onShowUnderlay` / `onHideUnderlay` | `function` | Callbacks when touch state changes                    |

## TouchableOpacity

TouchableOpacity is a component used to create pressable UI elements that give visual feedback by fading (changing opacity) when pressed.

```js
      <TouchableOpacity onPress={handlePress} style={styles.button}>
        <Text style={styles.buttonText}>Press Me</Text>
      </TouchableOpacity>
```

| Prop            | Type       | Description                                                |
| --------------- | ---------- | ---------------------------------------------------------- |
| `onPress`       | `function` | Called when the user taps the element                      |
| `activeOpacity` | `number`   | The opacity when the element is pressed (default is `0.2`) |
| `style`         | `object`   | Style the wrapper View                                     |
| `disabled`      | `boolean`  | Disable interaction and visual feedback                    |

**When to Use vs Other Touchables**
| Use Case                                          | Recommended Component                        |
| ------------------------------------------------- | -------------------------------------------- |
| Want fade on touch                                | `TouchableOpacity`                           |
| Want highlight color                              | `TouchableHighlight`                         |
| Need full control (e.g. long press, press in/out) | `Pressable` (recommended for advanced usage) |
| Simple button                                     | `Button`                                     |


## TouchableWithoutFeedback

It does not show any visual change (like color, ripple, or opacity),
But it can still detect touches and run a function when tapped.

Imagine a form with a keyboard open, and the user wants to close the keyboard by tapping anywhere outside the input. You wrap the whole screen with TouchableWithoutFeedback, and when the user taps, it dismisses the keyboard.

```js
import React, { useState } from 'react';
import {
  TextInput,
  View,
  Text,
  StyleSheet,
  Keyboard,
  TouchableWithoutFeedback,
} from 'react-native';

const App = () => {
  const [text, setText] = useState('');
  return (
    <TouchableWithoutFeedback onPress={Keyboard.dismiss}>
      <View style={styles.container}>
        <Text>Enter something:</Text>
        <TextInput
          style={styles.input}
          value={text}
          onChangeText={setText}
          placeholder="Type here"
        />
      </View>
    </TouchableWithoutFeedback>
  );
};


export default App;

```

TouchableWithoutFeedback supports only one child. If you wish to have several child components, wrap them in a View. 


So, what happens if I tap on the input itself?
If you tap inside the TextInput, two things happen:
Result: The input remains focused.

Ans Why? :  Because TextInput’s behavior takes priority over the outer TouchableWithoutFeedback.

## VirtualizedList
VirtualizedList is a base class used by components like FlatList and SectionList for efficiently rendering long lists of data.When you need custom behavior that FlatList or SectionList doesn't provide like

1. You have a list that contains multiple types of items (e.g., text items, image items, and buttons) and need to render them differently based on their type.

2. FlatList and SectionList are great for static lists, but if you have dynamic data structures that change frequently (e.g., you need to insert, delete, or reorder items), VirtualizedList gives you more flexibility to handle these changes manually.

3. While FlatList and SectionList support headers and footers, VirtualizedList allows you to manually define how to handle them, giving you more control over their appearance and behavior.


```js
import React from 'react';
import { VirtualizedList, Text, View, StyleSheet } from 'react-native';

const data = Array.from({ length: 1000 }, (_, i) => `Item ${i}`);

const getItem = (data, index) => ({
  key: String(index),
  title: data[index],
});

const getItemCount = (data) => data.length;

const App = () => {
  return (
    <VirtualizedList
      data={data}
      initialNumToRender={10}
      renderItem={({ item }) => (
        <View style={styles.item}>
          <Text>{item.title}</Text>
        </View>
      )}
      keyExtractor={(item) => item.key}
      getItem={getItem}
      getItemCount={getItemCount}
    />
  );
};

export default App;

```

| Prop                 | Description                                                                                       |
| -------------------- | ------------------------------------------------------------------------------------------------- |
| `data`               | The array of data to display in the list                                                          |
| `renderItem`         | Function to render each item in the list                                                          |
| `keyExtractor`       | Function to extract the unique key for each item                                                  |
| `initialNumToRender` | Number of items to render initially (important for performance)                                   |
| `getItem`            | Function that gets an item given its index (you have to define this when using `VirtualizedList`) |
| `getItemCount`       | Function that returns the total number of items in the list                                       |
