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
