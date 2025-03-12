## Olá, Mundo! - React Native

Vamos criar um simples aplicativo usando Expo Snack. O objetivo é imprimir no centro da tela o texto "Olá, Mundo!" e mudar o estilo do texto.

### Passo 1: Criar um novo projeto

1. Acesse o [Expo Snack](https://snack.expo.dev/).
2. Clique em "Create New Snack".
3. No arquivo `App.js`, apague todo o conteúdo e adicione o seguintente código:

```jsx
import React from 'react';
import { Text, View } from 'react-native';
export default function App() {
    return (
        <View
          style={{
            flex: 1,
            justifyContent: 'center',
            alignItems: 'center',
        }}>
        <Text style={{ fontSize: 30 }}>Olá, Mundo!</Text>
        </View>
    );
}
```

4. Clique em "Run" para visualizar o aplicativo.
5. Clique em "Save" e dê um nome ao projeto.

### Passo 2: Mudar o estilo do texto

1. No arquivo `App.js`, altere o estilo do texto para:

```jsx
<Text style={{ fontSize: 30, color: 'blue', fontWeight: 'bold' }}>Olá, Mundo!</Text>
```

### Passo 3: Adicionar um botão

1. No arquivo `App.js`, adicione um botão abaixo do texto:

```jsx
import { Button, Alert } from 'react-native';
<Button title="Clique aqui" onPress={() => Alert.alert('Olá, Mundo!')} />
```

### Passo 4: Mude mais alguns estilos

1. No arquivo `App.js`, altere o estilo do botão para:

```jsx
<Button title="Clique aqui" onPress={() => Alert.alert('Olá, Mundo!')} style={{ backgroundColor: 'blue', color: 'white' }} />
```

### Código Final

O código final do arquivo `App.js`, com os estilos separados, deve ser:

```jsx
import React from 'react';
import { StyleSheet, Text, View, Button, Alert } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Olá, Mundo!</Text>
      <Button
        title="Clique aqui"
        onPress={() => Alert.alert('Olá, Mundo!')}
        style={styles.button}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  title: {
    fontSize: 30,
    color: 'blue',
    fontWeight: 'bold',
    marginBottom: 20,
  },
  button: {
    backgroundColor: 'blue',
    color: 'white',
  },
});
```