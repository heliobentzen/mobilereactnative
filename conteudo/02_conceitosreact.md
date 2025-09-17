# Conceitos Fundamentais de React

Este material aborda os blocos de construção essenciais do React: Componentes e JSX.

---

## 1. Componentes

Em React, interfaces de usuário (UIs) são construídas a partir de pequenas peças reutilizáveis chamadas **componentes**. Um componente é como uma função JavaScript que retorna um elemento de UI. Existem duas formas principais de declarar componentes: Funcionais e de Classe.

### Componentes Funcionais (Functional Components)

Esta é a maneira moderna e recomendada de escrever componentes em React. Um componente funcional é, literalmente, uma função JavaScript que aceita um objeto de "props" (propriedades) como argumento e retorna um elemento React (geralmente escrito em JSX).

**Sintaxe:**

```javascript
function NomeDoComponente(props) {
    // Lógica do componente aqui
    return (
        // JSX que descreve a UI
    );
}

// Ou usando Arrow Function (mais comum)
const NomeDoComponente = (props) => {
    return (
        // JSX
    );
};
```

**Exemplo:**

```javascript
// Componente funcional simples que exibe uma saudação.
function Saudacao(props) {
    return <h1>Olá, {props.nome}!</h1>;
}

// Como usar o componente em outro lugar:
// <Saudacao nome="Mundo" />
```

### Componentes de Classe (Class Components)

Esta era a forma original de criar componentes que precisavam de estado ou métodos de ciclo de vida. Embora ainda sejam suportados, os Hooks (como `useState` e `useEffect`) tornaram possível fazer o mesmo em componentes funcionais, que são mais simples.

**Sintaxe:**

Um componente de classe é uma classe JavaScript que estende `React.Component` e deve implementar um método `render()` que retorna um elemento React.

```javascript
import React from 'react';

class NomeDoComponente extends React.Component {
    render() {
        // As props são acessadas via `this.props`
        return (
            // JSX que descreve a UI
        );
    }
}
```

**Exemplo:**

```javascript
import React from 'react';

// O mesmo componente Saudacao, agora como uma classe.
class Saudacao extends React.Component {
    render() {
        return <h1>Olá, {this.props.nome}!</h1>;
    }
}

// Como usar o componente em outro lugar:
// <Saudacao nome="Mundo" />
```

| Característica | Componente Funcional | Componente de Classe |
| :--------------- | :--------------------- | :--------------------- |
| **Sintaxe** | Função JavaScript | Classe ES6 |
| **Props** | `props` como argumento | `this.props` |
| **Estado** | Hook `useState()` | `this.state` |
| **Uso Atual** | **Recomendado** | Legado / Menos comum |

---

## 2. JSX (JavaScript XML)

JSX é uma extensão de sintaxe para JavaScript que permite escrever uma estrutura semelhante a HTML diretamente no seu código. Não é HTML nem uma string, mas uma forma mais expressiva de chamar `React.createElement()`.

**Por que usar JSX?**

O React acredita que a lógica de renderização está intrinsecamente ligada a outras lógicas de UI (como o estado muda, como os eventos são tratados). O JSX torna a criação de elementos React mais visual e familiar para quem já conhece HTML.

**Exemplo de JSX:**

```javascript
const elemento = <h1>Olá, mundo!</h1>;
```

O código acima parece HTML, mas é JavaScript. Ferramentas como o Babel transpilam (convertem) esse código JSX para chamadas de função `React.createElement()`:

```javascript
// O código JSX acima é convertido para isto:
const elemento = React.createElement('h1', null, 'Olá, mundo!');
```

### Principais Características do JSX

1.  **Expressões JavaScript com `{}`**: Você pode embutir qualquer expressão JavaScript válida dentro de chaves.

        ```javascript
        const nome = "Ana";
        const elemento = <h1>Olá, {nome}!</h1>; // Renderiza: <h1>Olá, Ana!</h1>

        const resultado = <p>2 + 2 = {2 + 2}</p>; // Renderiza: <p>2 + 2 = 4</p>
        ```

2.  **Atributos como em HTML**: Atributos são escritos de forma semelhante ao HTML, mas com algumas diferenças.

        *   Use `className` em vez de `class` (porque `class` é uma palavra reservada em JavaScript).
        *   Atributos com nomes compostos usam camelCase (ex: `onClick`, `tabIndex`).

        ```javascript
        // HTML
        // <div class="meu-app" onclick="minhaFuncao()">

        // JSX
        <div className="meu-app" onClick={minhaFuncao}>
        ```

3.  **Um Único Elemento Raiz**: Um componente deve retornar um único elemento pai. Se precisar retornar múltiplos elementos, envolva-os em um elemento `<div>` ou use um **Fragment** (`<>...</>`).

        ```javascript
        // CORRETO
        function MeuComponente() {
            return (
                <>
                    <h1>Título</h1>
                    <p>Parágrafo</p>
                </>
            );
        }

        // INCORRETO (retornando dois elementos)
        /*
        function MeuComponente() {
            return (
                <h1>Título</h1>
                <p>Parágrafo</p>
            );
        }
        */
        ```
