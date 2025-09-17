# Estado (useState) e Propriedades (props) em React

Em React, componentes são os blocos de construção da sua interface de usuário (UI). Para tornar esses componentes dinâmicos e interativos, utilizamos dois conceitos fundamentais: **`props`** e **`state`**.

## Propriedades (Props)

Props (abreviação de "properties") são usadas para passar dados de um componente pai para um componente filho. Pense nelas como argumentos de uma função. A principal característica das props é que elas são **somente leitura** (imutáveis). Um componente filho não pode modificar as props que recebe.

### Como funcionam?

1.  **Pai para Filho:** Os dados fluem em uma única direção: de cima para baixo na árvore de componentes.
2.  **Imutabilidade:** Garante que a UI seja previsível, pois um componente filho não pode alterar o estado de um componente pai inesperadamente.

### Exemplo de Código

Vamos criar um componente `BoasVindas` que recebe um nome através de props e o exibe.

```jsx
// Componente Filho: BoasVindas.js
function BoasVindas(props) {
    return <h1>Olá, {props.nome}!</h1>;
}

// Componente Pai: App.js
function App() {
    return (
        <div>
            <BoasVindas nome="Maria" />
            <BoasVindas nome="João" />
        </div>
    );
}
```

Neste exemplo, o componente `App` passa a prop `nome` para o componente `BoasVindas`, que a utiliza para renderizar uma mensagem personalizada.

## Estado (State)

O estado é usado para gerenciar dados que **mudam ao longo do tempo** dentro de um componente. Diferente das props, o estado é privado e controlado pelo próprio componente. Quando o estado de um componente muda, o React o re-renderiza automaticamente para refletir essa mudança na UI.

### O Hook `useState`

Em componentes de função, usamos o hook `useState` para adicionar estado.

-   **Declaração:** `useState` retorna um par de valores: a variável de estado atual e uma função para atualizá-la.
-   **Sintaxe:** `const [variavelDeEstado, setVariavelDeEstado] = useState(valorInicial);`

### Exemplo de Código

Vamos criar um componente `Contador` que tem um botão para incrementar um número.

```jsx
import React, { useState } from 'react';

function Contador() {
    // Declara uma nova variável de estado chamada "contagem"
    // O valor inicial é 0
    const [contagem, setContagem] = useState(0);

    return (
        <div>
            <p>Você clicou {contagem} vezes</p>
            {/* Ao clicar, chama a função setContagem para atualizar o estado */}
            <button onClick={() => setContagem(contagem + 1)}>
                Clique aqui
            </button>
        </div>
    );
}
```

Neste exemplo:
1.  `useState(0)` inicializa o estado `contagem` com o valor `0`.
2.  Sempre que o botão é clicado, a função `setContagem` é chamada com o novo valor (`contagem + 1`).
3.  O React detecta a mudança no estado e re-renderiza o componente `Contador`, exibindo o novo valor de `contagem`.

## Resumo: Props vs. State

| Característica | Props (Propriedades) | State (Estado) |
| :--- | :--- | :--- |
| **Origem** | Passadas de um componente pai. | Gerenciado dentro do próprio componente. |
| **Mutabilidade** | Imutáveis (somente leitura). | Mutáveis (podem ser alteradas). |
| **Quem controla?** | O componente pai. | O próprio componente. |
| **Fluxo de Dados** | De cima para baixo (pai -> filho). | Interno ao componente. |
| **Uso Principal** | Configurar e passar dados para um componente. | Lidar com dados que mudam com a interação do usuário ou eventos. |

Entender a diferença entre `props` e `state` é crucial para construir aplicações React eficientes e organizadas. Use **props** para configurar um componente e **state** para gerenciar seus dados internos e interativos.
