# Introdução ao React Native

React Native é um framework de código aberto criado pelo Facebook que permite o desenvolvimento de aplicativos móveis nativos para iOS e Android usando JavaScript e React. A principal vantagem do React Native é a capacidade de escrever uma base de código única que funciona em ambas as plataformas, economizando tempo e recursos de desenvolvimento. Ele combina a familiaridade do desenvolvimento web com o desempenho e a aparência de aplicativos nativos.

## Fundamentos Essenciais

Para começar a desenvolver com React Native, é crucial ter uma base sólida em algumas tecnologias e conceitos modernos de desenvolvimento.

### Revisão de JavaScript Moderno (ES6+)

O React Native utiliza as funcionalidades mais recentes do JavaScript. É essencial estar confortável com:

*   **`let` e `const`**: Para declaração de variáveis com escopo de bloco.
*   **Arrow Functions**: Uma sintaxe mais concisa para escrever funções.
*   **Promises**: Para lidar com operações assíncronas de forma mais limpa.
*   **`async/await`**: Uma sintaxe que simplifica o trabalho com Promises, tornando o código assíncrono mais legível.

### Introdução ao TypeScript

TypeScript é um superset do JavaScript que adiciona tipagem estática opcional. Seus principais benefícios incluem:

*   **Detecção de erros em tempo de compilação**: Ajuda a evitar bugs comuns antes mesmo de executar o código.
*   **Melhor autocompletar e inteligência de código**: Facilita o desenvolvimento em editores de código modernos.
*   **Código mais legível e manutenível**: A tipagem explícita torna a intenção do código mais clara.

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
