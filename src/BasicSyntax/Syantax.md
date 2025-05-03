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
