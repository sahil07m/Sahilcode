App.js:

import React, { useState } from 'react';
import { StyleSheet, View, Text, TouchableOpacity } from 'react-native';
import { Provider as PaperProvider } from 'react-native-paper';

const App = () => {
  const [input, setInput] = useState('');
  const [result, setResult] = useState('');

  const handlePress = (value) => {
    if (value === '=') {
      try {
        setResult(eval(input)); // Use eval carefully in production.
      } catch (error) {
        setResult('Error');
      }
    } else if (value === 'C') {
      setInput('');
      setResult('');
    } else {
      setInput((prev) => prev + value);
    }
  };

  const buttons = ['7', '8', '9', '/', '4', '5', '6', '*', '1', '2', '3', '-', 'C', '0', '=', '+'];

  return (
    <PaperProvider>
      <View style={styles.container}>
        <Text style={styles.input}>{input}</Text>
        <Text style={styles.result}>{result}</Text>
        <View style={styles.buttons}>
          {buttons.map((button) => (
            <TouchableOpacity
              key={button}
              style={styles.button}
              onPress={() => handlePress(button)}
            >
              <Text style={styles.buttonText}>{button}</Text>
            </TouchableOpacity>
          ))}
        </View>
      </View>
    </PaperProvider>
  );
};

const styles = StyleSheet.create({
  container: { flex: 1, justifyContent: 'center', backgroundColor: '#f5f5f5' },
  input: { fontSize: 36, textAlign: 'right', marginRight: 10, marginBottom: 20 },
  result: { fontSize: 48, textAlign: 'right', marginRight: 10, marginBottom: 20 },
  buttons: { flexDirection: 'row', flexWrap: 'wrap', justifyContent: 'center' },
  button: { width: '20%', padding: 20, margin: 5, backgroundColor: '#d4d4d2', borderRadius: 5 },
  buttonText: { textAlign: 'center', fontSize: 20 },
});

"calc by sahil"
