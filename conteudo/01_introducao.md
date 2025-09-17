# Introdução ao React Native

React Native é um framework de código aberto criado pelo Facebook que permite o desenvolvimento de aplicativos móveis nativos para iOS e Android usando JavaScript e React. A principal vantagem do React Native é a capacidade de escrever uma base de código única que funciona em ambas as plataformas, economizando tempo e recursos de desenvolvimento. Ele combina a familiaridade do desenvolvimento web com o desempenho e a aparência de aplicativos nativos.

## Fundamentos Essenciais

Para começar a desenvolver com React Native, é crucial ter uma base sólida em algumas tecnologias e conceitos modernos de desenvolvimento.

### Revisão de JavaScript Moderno (ES6+)

O React Native utiliza as funcionalidades mais recentes do JavaScript. É essencial estar confortável com:

*   **`let` e `const`**: Para declaração de variáveis com escopo de bloco.
    ```javascript
    const taxaFixa = 1.5; // Não pode ser reatribuída
    let contador = 0;     // Pode ser reatribuída
    contador = 1;
    ```

*   **Arrow Functions**: Uma sintaxe mais concisa para escrever funções.
    ```javascript
    // Sintaxe tradicional
    function dobrar(numero) {
      return numero * 2;
    }

    // Com Arrow Function
    const dobrar = (numero) => numero * 2;
    ```

*   **Promises**: Para lidar com operações assíncronas de forma mais limpa.
    ```javascript
    const buscarDados = new Promise((resolve, reject) => {
      // Simula uma chamada de API
      setTimeout(() => {
        resolve({ id: 1, nome: "Usuário Teste" });
      }, 1000);
    });

    buscarDados.then(dados => console.log(dados));
    ```

*   **`async/await`**: Uma sintaxe que simplifica o trabalho com Promises, tornando o código assíncrono mais legível.
    ```javascript
    async function carregarUsuario() {
      console.log("Carregando...");
      const dados = await buscarDados; // Espera a Promise ser resolvida
      console.log("Usuário carregado:", dados);
    }

    carregarUsuario();
    ```

### Introdução ao TypeScript

TypeScript é um superset do JavaScript que adiciona tipagem estática opcional. Seus principais benefícios incluem:

*   **Detecção de erros em tempo de compilação**: Ajuda a evitar bugs comuns antes mesmo de executar o código.
*   **Melhor autocompletar e inteligência de código**: Facilita o desenvolvimento em editores de código modernos.
*   **Código mais legível e manutenível**: A tipagem explícita torna a intenção do código mais clara.

    ```typescript
    // Exemplo de uma função com tipos
    function cumprimentar(nome: string, idade: number): string {
      return `Olá, ${nome}! Você tem ${idade} anos.`;
    }

    // O TypeScript apontaria um erro na linha abaixo:
    // cumprimentar("Ana", "vinte");
    ```

## Componentes Básicos e Estilização

No React Native, a interface do usuário é construída a partir de componentes. Os mais básicos são `View`, `Text` e `StyleSheet`.

*   **`View`**: É o contêiner mais fundamental. Corresponde a uma `<div>` no desenvolvimento web.
*   **`Text`**: Usado para exibir qualquer tipo de texto. Todo texto deve estar dentro de um componente `<Text>`.
*   **`StyleSheet`**: Fornece uma forma otimizada de criar e gerenciar estilos, semelhante ao CSS.

```jsx
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

const CartaoDeVisita = () => {
  return (
    <View style={styles.cartao}>
      <Text style={styles.nome}>João da Silva</Text>
      <Text style={styles.cargo}>Desenvolvedor React Native</Text>
    </View>
  );
};

const styles = StyleSheet.create({
  cartao: {
    backgroundColor: '#e0e0e0',
    padding: 20,
    borderRadius: 8,
    alignItems: 'center',
    margin: 16,
  },
  nome: {
    fontSize: 22,
    fontWeight: 'bold',
  },
  cargo: {
    fontSize: 16,
    color: '#555',
  },
});

export default CartaoDeVisita;
```

### Configuração do Ambiente de Desenvolvimento

Para criar e executar aplicativos React Native, você precisará configurar seu ambiente com as seguintes ferramentas:

*   **Node.js**: Ambiente de execução para JavaScript.
*   **Watchman**: Ferramenta do Facebook para observar mudanças no sistema de arquivos.
*   **JDK (Java Development Kit)**: Necessário para o desenvolvimento Android.
*   **Android Studio**: Fornece o SDK do Android, emuladores e outras ferramentas essenciais para o desenvolvimento Android.
*   **Xcode**: Necessário para o desenvolvimento iOS (disponível apenas em macOS).

### Criando seu Primeiro Projeto com a React Native CLI

Após configurar o ambiente, você pode criar um novo projeto usando a interface de linha de comando (CLI) do React Native.

1.  **Instale a CLI do React Native (se necessário):**
    ```bash
    npm install -g react-native-cli
    ```

2.  **Crie um novo projeto:**
    Execute o seguinte comando para iniciar um novo projeto. Substitua `MeuPrimeiroApp` pelo nome desejado para o seu aplicativo.
    ```bash
    npx react-native init MeuPrimeiroApp
    ```

3.  **Navegue até o diretório do projeto:**
    ```bash
    cd MeuPrimeiroApp
    ```

4.  **Execute o aplicativo:**
    *   **Para Android:**
        ```bash
        npx react-native run-android
        ```
    *   **Para iOS:**
        ```bash
        npx react-native run-ios
        ```
