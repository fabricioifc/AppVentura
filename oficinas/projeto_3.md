# 🍭 Click do Docinho - Tutorial com React Native (Expo Snack)

Um jogo estilo **clicker** com tema de doces, onde o jogador ganha 🍬 clicando, contrata ajudantes 🧸 e melhora o poder de clique 👆!

Ideal para crianças ou iniciantes em programação com React Native usando **Expo Snack**.

---

## 🎯 Objetivo

- Ganhar doces clicando no botão 🍭  
- Melhorar o clique para ganhar mais doces por toque  
- Contratar ajudantes que produzem doces automaticamente  
- Mostrar alertas sempre que faltar doces

---

## 🚀 Começando no Expo Snack

1. Acesse o site: [https://snack.expo.dev/](https://snack.expo.dev/)
2. Clique em **"Create New Snack"**
3. Apague o conteúdo de `App.js`
4. Cole o código abaixo e siga os comentários no tutorial

---

## 🧠 Estados do jogo

```jsx
const [doces, setDoces] = useState(0);              // Total de doces 🍬
const [poderDoClique, setPoderDoClique] = useState(1); // Quantos doces ganhamos por clique
const [custoMelhoriaClique, setCustoMelhoriaClique] = useState(5); // Preço para melhorar o clique

const [ajudantes, setAjudantes] = useState(0);      // Quantos ajudantes temos
const [custoAjudante, setCustoAjudante] = useState(20); // Custo do próximo ajudante

const [mostrarAviso, setMostrarAviso] = useState(false); // Mostra um aviso na tela?
const [mensagemAviso, setMensagemAviso] = useState('');  // Qual mensagem mostrar
```

---

## ⏲ Ajudantes produzem doces automaticamente

```jsx
useEffect(() => {
  const intervalo = setInterval(() => {
    setDoces(valorAtual => valorAtual + ajudantes);
  }, 1000);
  return () => clearInterval(intervalo);
}, [ajudantes]);
```

A cada 1 segundo, cada ajudante gera 1 doce automaticamente.

---

## ✋ Clique para ganhar doces

``` jsx
const clicar = () => {
  setDoces(valorAtual => valorAtual + poderDoClique);
};
```

Cada clique gera doces baseado no poder do clique atual.

---

## 🛠 Melhorar clique

``` jsx
const melhorarClique = () => {
  if (doces >= custoMelhoriaClique) {
    setDoces(doces - custoMelhoriaClique);
    setPoderDoClique(poder => poder + 1);
    setCustoMelhoriaClique(custo => custo + 5);
  } else {
    mostrarMensagem(`🍬 Você precisa de ${custoMelhoriaClique} doces!`);
  }
};
```

Ao clicar, você:

- Gasta doces

- Aumenta o poder de clique

- Aumenta o custo da próxima melhoria

---

## 🧸 Contratar Ajudantes

``` jsx 
const comprarAjudante = () => {
  if (doces >= custoAjudante) {
    setDoces(doces - custoAjudante);
    setAjudantes(quantidade => quantidade + 1);
    setCustoAjudante(custo => custo + 10);
  } else {
    mostrarMensagem(`👦 Você precisa de ${custoAjudante} doces!`);
  }
};
```

Cada ajudante custa doces. A cada compra, o próximo fica mais caro.

---

## 🔔 Mensagem de Aviso

``` jsx 
const mostrarMensagem = (mensagem) => {
  setMensagemAviso(mensagem);
  setMostrarAviso(true);
};
```

Função para exibir mensagens de erro ou alerta ao usuário.

---

## 🧁 Interface (UI)

``` jsx
return (
  <ScrollView contentContainerStyle={estilos.container}>
    <Text style={estilos.titulo}>Click do Docinho 🍭</Text>

    <View style={estilos.caixaStatus}>
      <Text style={estilos.texto}>🍬 Doces: <Text style={estilos.negrito}>{doces}</Text></Text>
      <Text style={estilos.texto}>👆 Clique: +{poderDoClique} doces</Text>
      <Text style={estilos.texto}>🧸 Ajudantes: {ajudantes}</Text>
    </View>

    <TouchableOpacity style={estilos.botaoDoce} onPress={clicar}>
      <Text style={estilos.doce}>🍭</Text>
    </TouchableOpacity>

    <TouchableOpacity style={estilos.botao} onPress={melhorarClique}>
      <Text style={estilos.textoBotao}>Melhorar Clique ({custoMelhoriaClique} doces)</Text>
    </TouchableOpacity>

    <TouchableOpacity style={estilos.botaoSecundario} onPress={comprarAjudante}>
      <Text style={estilos.textoBotao}>Chamar Ajudante ({custoAjudante} doces)</Text>
    </TouchableOpacity>

    {mostrarAviso && (
      <View style={estilos.modal}>
        <View style={estilos.modalCaixa}>
          <Text style={estilos.modalTexto}>{mensagemAviso}</Text>
          <TouchableOpacity onPress={() => setMostrarAviso(false)} style={estilos.modalBotao}>
            <Text style={estilos.modalBotaoTexto}>OK!</Text>
          </TouchableOpacity>
        </View>
      </View>
    )}
  </ScrollView>
);
```

---

## 🎨 Estilos com StyleSheet

``` jsx
const estilos = StyleSheet.create({
  container: {
    flexGrow: 1,
    backgroundColor: '#361459',
    alignItems: 'center',
    paddingTop: 60,
    paddingHorizontal: 20,
  },
  titulo: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#FFF',
    marginBottom: 20,
  },
  caixaStatus: {
    backgroundColor: '#FFF',
    padding: 16,
    borderRadius: 10,
    width: '100%',
    marginBottom: 20,
  },
  texto: {
    fontSize: 16,
    marginBottom: 5,
  },
  negrito: {
    fontWeight: 'bold',
  },
  botaoDoce: {
    backgroundColor: '#762EA6',
    padding: 30,
    borderRadius: 100,
    marginTop: 90,
    marginBottom: 110,
  },
  doce: {
    fontSize: 48,
  },
  botao: {
    backgroundColor: '#F27F1B',
    padding: 12,
    borderRadius: 8,
    width: '100%',
    alignItems: 'center',
    marginBottom: 10,
  },
  botaoSecundario: {
    backgroundColor: '#D91438',
    padding: 12,
    borderRadius: 8,
    width: '100%',
    alignItems: 'center',
  },
  textoBotao: {
    color: '#FFF',
    fontWeight: 'bold',
    fontSize: 16,
  },
  modal: {
    position: 'absolute',
    top: 0,
    left: 0,
    right: 0,
    bottom: 0,
    backgroundColor: 'rgba(0,0,0,0.5)',
    justifyContent: 'center',
    alignItems: 'center',
  },
  modalCaixa: {
    backgroundColor: '#FFF',
    padding: 20,
    borderRadius: 10,
    width: '80%',
    alignItems: 'center',
  },
  modalTexto: {
    fontSize: 16,
    marginBottom: 15,
    textAlign: 'center',
  },
  modalBotao: {
    backgroundColor: '#FF69B4',
    paddingVertical: 8,
    paddingHorizontal: 20,
    borderRadius: 8,
  },
  modalBotaoTexto: {
    color: '#FFF',
    fontWeight: 'bold',
    fontSize: 16,
  },
});
```

---

# ✅ Finalizado!

Seu clicker está pronto! Agora é só brincar, aprender e melhorar!

---