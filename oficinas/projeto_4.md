## 🎯 Desafios

### ✅ Missão 1: Reiniciar o Jogo

#### 🎯 Objetivo
Permitir que o jogador possa resetar o jogo para o estado inicial.

#### 🧠 Função:
```jsx
const reiniciarJogo = () => {
  setDoces(0);
  setPoderDoClique(1 * multiplicador);
  setCustoMelhoriaClique(5);
  setAjudantes(0);
  setCustoAjudante(20);
};
```

#### ➕ Botão:
```jsx
<TouchableOpacity style={estilos.botaoSecundario} onPress={reiniciarJogo}>
  <Text style={estilos.textoBotao}>🔁 Reiniciar Jogo</Text>
</TouchableOpacity>
```

---

### ✅ Missão 2: Modal de Mensagem

#### 🎯 Objetivo
Substituir os alerts nativos por um modal personalizado para exibir mensagens, como falta de doces.

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
Mostrar uma conquista visual quando o jogador atingir 100 doces.

#### 🧠 Estado:
```jsx
const [conquista, setConquista] = useState(false);
```

#### ⚡ Efeito:
```jsx
useEffect(() => {
  if (doces >= 100 && !conquista) {
    setConquista(true);
    mostrarMensagem('🏆 Conquista: Docinho Mestre!');
  }
}, [doces]);
```

#### 🖼 Exibição da conquista:
```jsx
{conquista && (
  <Text style={[estilos.texto, { color: 'gold', fontWeight: 'bold' }]}>
    🏆 Conquista: Docinho Mestre!
  </Text>
)}
```

---

### ✅ Missão 4: Rebirth (Renascimento)

#### 🎯 Objetivo
Permitir que o jogador reinicie o jogo após atingir uma meta de doces, ganhando um bônus de multiplicador que aumenta a produção de doces por clique e ajudantes.

#### 🧠 Estados adicionais:
```jsx
const [multiplicador, setMultiplicador] = useState(1);
const [custoRebirth, setCustoRebirth] = useState(100);
```

#### 🔁 Função de Rebirth:
```jsx
const fazerRebirth = () => {
  if (doces >= custoRebirth) {
    setMultiplicador(m => m + 1);
    setDoces(0);
    setPoderDoClique((1) * (multiplicador + 1));
    setCustoMelhoriaClique(5);
    setAjudantes(0);
    setCustoAjudante(20);
    setCustoRebirth(custoRebirth * 2);
    mostrarMensagem(`🌟 Rebirth feito! Multiplicador agora é x${multiplicador + 1}`);
  } else {
    mostrarMensagem(`✨ Você precisa de ${custoRebirth} doces para Rebirth`);
  }
};
```

#### ➕ Botão para Rebirth:
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
