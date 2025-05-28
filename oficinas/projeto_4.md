
# 🎮 Missões do Jogo Clicker - React Native

## 🎯 Desafios

---

### ✅ Missão 1: Personalize o Visual do App

Sua primeira missão é deixar o app com a sua cara! Para isso, vamos alterar os estilos utilizados na interface.

1. Localize a variável `estilos`, que é criada com o `StyleSheet.create(...)`.
2. Dentro dela, você encontrará várias configurações visuais — como cores, tamanhos, margens, etc.
3. Escolha um dos blocos de estilo e modifique algum valor para ver o resultado no app.

💡 Dica: Procure por este trecho no código:

```jsx
const estilos = StyleSheet.create({
  // Altere os valores aqui
});
```

Use sua criatividade e experimente diferentes combinações!

---

### ✅ Missão 2: Modal de Mensagem

#### 🎯 Objetivo  
Substituir os alerts nativos por um modal personalizado para exibir mensagens (por exemplo: falta de doces).

#### 🔌 Importações
```jsx
import { Modal } from 'react-native';
```

#### 🧠 Estados:
```jsx
const [mensagemModal, setMensagemModal] = useState('');
const [modalVisivel, setModalVisivel] = useState(false);
```

#### 🔧 Função para exibir mensagens:
```jsx
const mostrarMensagem = (mensagem) => {
  setMensagemModal(mensagem);
  setModalVisivel(true);
};
```

#### 🧁 Componente do Modal:
```jsx
<Modal transparent visible={modalVisivel} animationType="fade">
  <View style={estilos.modalFundo}>
    <View style={estilos.modalCaixa}>
      <Text style={estilos.texto}>{mensagemModal}</Text>
      <TouchableOpacity onPress={() => setModalVisivel(false)} style={estilos.botao}>
        <Text style={estilos.textoBotao}>Fechar</Text>
      </TouchableOpacity>
    </View>
  </View>
</Modal>
```

#### 🎨 Estilos para o modal:
```jsx
modalFundo: {
  flex: 1,
  justifyContent: 'center',
  alignItems: 'center',
  backgroundColor: 'rgba(0,0,0,0.5)',
},
modalCaixa: {
  backgroundColor: 'white',
  padding: 20,
  borderRadius: 10,
  alignItems: 'center',
  width: '80%',
}
```

---

### ✅ Missão 3: Conquista de 100 Doces

#### 🎯 Objetivo  
Mostrar uma conquista visual quando o jogador atingir um certo número de doces (começando com 100).

#### 🧠 Estado:
```jsx
const [conquista, setConquista] = useState(0);
```

#### ⚡ Efeito:
```jsx
useEffect(() => {
  if (doces >= custoRebirth && conquista < multiplicador) {
    setConquista(multiplicador);
    mostrarMensagem(`🏆 Conquista: Docinho Mestre nível ${multiplicador}!`);
  }
}, [doces, multiplicador]);
```

#### 🖼 Exibição da conquista:
```jsx
{conquista > 0 && (
  <Text style={[estilos.texto, { color: 'gold', fontWeight: 'bold' }]}>
    🏆 Conquista: Docinho Mestre nível {conquista}!
  </Text>
)}
```

---

### ✅ Missão 4: Rebirth (Renascimento)

#### 🎯 Objetivo  
Permitir que o jogador reinicie o jogo ao atingir uma meta de doces, ganhando um bônus de multiplicador que aumenta a produção de doces por clique e ajudantes.

#### 🧠 Estados adicionais:
```jsx
const [multiplicador, setMultiplicador] = useState(1);
const [custoRebirth, setCustoRebirth] = useState(100);
```

#### 🔁 Função de Rebirth:
```jsx
const fazerRebirth = () => {
  if (doces >= custoRebirth) {
    const novoMultiplicador = multiplicador + 1;
    setMultiplicador(novoMultiplicador);
    setDoces(0);
    setPoderDoClique(1 * novoMultiplicador);
    setCustoMelhoriaClique(5);
    setAjudantes(0);
    setCustoAjudante(20);
    setCustoRebirth(custoRebirth * 2);
    setConquista(novoMultiplicador);
    mostrarMensagem(`🌟 Rebirth feito! Multiplicador agora é x${novoMultiplicador}`);
  } else {
    mostrarMensagem(`✨ Você precisa de ${custoRebirth} doces para fazer Rebirth`);
  }
};
```

#### ➕ Botão:
```jsx
<TouchableOpacity
  style={[estilos.botao, doces < custoRebirth && estilos.botaoDesativado]}
  onPress={fazerRebirth}
  disabled={doces < custoRebirth}
>
  <Text style={estilos.textoBotao}>✨ Rebirth (x{multiplicador}) - {custoRebirth} doces</Text>
</TouchableOpacity>
```

---

### ✅ Missão 5: Reiniciar o Jogo

#### 🎯 Objetivo  
Adicionar um botão que reseta completamente o jogo, inclusive as conquistas e o progresso de Rebirth.

#### 🔁 Nova função de reinício:
```jsx
const reiniciarJogo = () => {
  setDoces(0);
  setMultiplicador(1);
  setPoderDoClique(1);
  setCustoMelhoriaClique(5);
  setAjudantes(0);
  setCustoAjudante(20);
  setCustoRebirth(100);
  setConquista(0);
  mostrarMensagem('🔁 Jogo reiniciado!');
};
```

#### ➕ Botão:
```jsx
<TouchableOpacity style={estilos.botaoSecundario} onPress={reiniciarJogo}>
  <Text style={estilos.textoBotao}>🔁 Reiniciar Jogo</Text>
</TouchableOpacity>
```
