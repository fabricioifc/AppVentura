## Olá, Mundo! - React Native

Vamos criar um simples aplicativo usando Expo Snack. O objetivo é desenvolver um jogo clicker básico.

### Passo 1: Criar um novo projeto

1. Acesse o [Expo Snack](https://snack.expo.dev/).
2. Clique em "Create New Snack".
3. No arquivo `App.js`, apague todo o conteúdo e adicione o seguinte código:

### Código Final

O código final do arquivo `App.js`, com os estilos separados, deve ser:

```jsx

import React, { useState, useEffect } from 'react';
import { View, Text, TouchableOpacity, StyleSheet, ScrollView } from 'react-native';

export default function App() {
  const [money, setMoney] = useState(0);
  const [clickPower, setClickPower] = useState(1);
  const [clickUpgradeCost, setClickUpgradeCost] = useState(10);

  const [employeeCount, setEmployeeCount] = useState(0);
  const [employeeCost, setEmployeeCost] = useState(50);

  const [multiplier, setMultiplier] = useState(1);
  const [companyLevel, setCompanyLevel] = useState(1); // Até 6

  const [modalVisible, setModalVisible] = useState(false);
  const [modalMessage, setModalMessage] = useState('');

  useEffect(() => {
    const id = setInterval(() => {
      setMoney(prev => prev + employeeCount * 2 * multiplier);
    }, 1000);
    return () => clearInterval(id);
  }, [employeeCount, multiplier]);

  const showModal = (message) => {
    setModalMessage(message);
    setModalVisible(true);
  };

  const handleClick = () => {
    setMoney(prev => prev + clickPower * multiplier);
  };

  const buyClickUpgrade = () => {
    if (money >= clickUpgradeCost) {
      setMoney(money - clickUpgradeCost);
      setClickPower(prev => prev + 1);
      setClickUpgradeCost(prev => prev + 10);
    } else {
      showModal(`💸 Você precisa de R$${clickUpgradeCost}`);
    }
  };

  const hireEmployee = () => {
    if (money >= employeeCost) {
      setMoney(money - employeeCost);
      setEmployeeCount(prev => prev + 1);
      setEmployeeCost(prev => prev + 50);
    } else {
      showModal(`💸 Você precisa de R$${employeeCost}`);
    }
  };

  const resetForNewCompany = () => {
    const nextCost = companyLevel * 200;

    if (companyLevel >= 6) {
      showModal('📢 Limite: você já abriu todas as empresas possíveis!');
      return;
    }

    if (money >= nextCost) {
      showModal(`🏢 Nova Empresa aberta!\n\nVocê agora recebe x${multiplier + 1} vezes mais!\nSeu progresso foi reiniciado.`);
      setMoney(0);
      setClickPower(1);
      setClickUpgradeCost(10);
      setEmployeeCount(0);
      setEmployeeCost(50);
      setMultiplier(multiplier + 1);
      setCompanyLevel(companyLevel + 1);
    } else {
      showModal(`💸 Você precisa de R$${nextCost} para abrir nova empresa.`);
    }
  };

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text style={styles.title}>Clicker do Cofrinho</Text>

      <View style={styles.statusBox}>
        <Text style={styles.stat}>💵 Saldo: <Text style={styles.bold}>R${money}</Text></Text>
        <Text style={styles.stat}>🖱 Clique: +R${clickPower * multiplier}</Text>
        <Text style={styles.stat}>👨‍💼 Funcionários: {employeeCount}</Text>
        <Text style={styles.stat}>🏢 Empresa Nível: {companyLevel} / 6</Text>
        <Text style={styles.stat}>📈 Multiplicador: x{multiplier}</Text>
      </View>

      <TouchableOpacity style={styles.coinButton} onPress={handleClick}>
        <Text style={styles.coin}>💰</Text>
      </TouchableOpacity>

      <View style={styles.buttonsContainer}>
        <TouchableOpacity style={styles.button} onPress={buyClickUpgrade}>
          <Text style={styles.buttonText}>Melhorar Clique (R${clickUpgradeCost})</Text>
        </TouchableOpacity>

        <TouchableOpacity style={styles.buttonSecondary} onPress={hireEmployee}>
          <Text style={styles.buttonText}>Contratar Funcionário (R${employeeCost})</Text>
        </TouchableOpacity>

        <TouchableOpacity
          style={[styles.buttonTertiary, companyLevel >= 6 && styles.buttonDisabled]}
          onPress={resetForNewCompany}
          disabled={companyLevel >= 6}
        >
          <Text style={styles.buttonText}>
            {companyLevel >= 6 ? 'Nova Empresa (Máx)' : `Nova Empresa (R$${companyLevel * 200})`}
          </Text>
        </TouchableOpacity>
      </View>

      {companyLevel > 5 && (
        <Text style={styles.success}>🎉 Parabéns! Você criou todas as empresas possíveis!</Text>
      )}

      {modalVisible && (
        <View style={styles.modalContainer}>
          <View style={styles.modalBox}>
            <Text style={styles.modalText}>{modalMessage}</Text>
            <TouchableOpacity
              style={styles.modalButton}
              onPress={() => setModalVisible(false)}
            >
              <Text style={styles.modalButtonText}>Fechar</Text>
            </TouchableOpacity>
          </View>
        </View>
      )}
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#053959',
    alignItems: 'center',
    justifyContent: 'flex-start',
    padding: 20,
    paddingTop: 50,
    flexGrow: 1,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#F2A20C',
    marginBottom: 20,
  },
  statusBox: {
    backgroundColor: '#FFFFFF',
    padding: 16,
    borderRadius: 12,
    marginBottom: 20,
    width: '100%',
    elevation: 2,
  },
  stat: {
    fontSize: 16,
    marginBottom: 4,
  },
  bold: {
    fontWeight: 'bold',
  },
  coinButton: {
    backgroundColor: '#F2A007',
    padding: 30,
    borderRadius: 100,
    marginVertical: 20,
    elevation: 4,
  },
  coin: {
    fontSize: 50,
  },
  buttonsContainer: {
    width: '100%',
    alignItems: 'center',
  },
  button: {
    backgroundColor: '#F2BF27',
    padding: 12,
    borderRadius: 10,
    marginVertical: 6,
    marginTop: 40,
    width: '100%',
    alignItems: 'center',
  },
  buttonSecondary: {
    backgroundColor: '#F2A20C',
    padding: 12,
    borderRadius: 10,
    marginTop: 10,
    width: '100%',
    alignItems: 'center',
  },
  buttonTertiary: {
    backgroundColor: '#BF3706',
    padding: 12,
    borderRadius: 10,
    marginTop: 15,
    width: '100%',
    alignItems: 'center',
  },
  buttonDisabled: {
    backgroundColor: '#B0BEC5',
  },
  buttonText: {
    color: '#03045E',
    fontWeight: 'bold',
    fontSize: 16,
  },
  success: {
    marginTop: 30,
    fontSize: 16,
    color: 'green',
    fontWeight: 'bold',
    textAlign: 'center',
  },
  modalContainer: {
    position: 'absolute',
    top: 0,
    left: 0,
    right: 0,
    bottom: 0,
    backgroundColor: 'rgba(0, 0, 0, 0.5)',
    justifyContent: 'center',
    alignItems: 'center',
    zIndex: 10,
  },
  modalBox: {
    backgroundColor: '#fff',
    padding: 20,
    borderRadius: 12,
    width: '80%',
    alignItems: 'center',
  },
  modalText: {
    fontSize: 16,
    textAlign: 'center',
    marginBottom: 20,
  },
  modalButton: {
    backgroundColor: '#00B4D8',
    paddingVertical: 10,
    paddingHorizontal: 20,
    borderRadius: 8,
  },
  modalButtonText: {
    color: '#fff',
    fontWeight: 'bold',
    fontSize: 16,
  },
});


```