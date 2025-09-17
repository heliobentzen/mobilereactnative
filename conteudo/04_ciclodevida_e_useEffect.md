# Ciclo de Vida de Componentes e o Hook `useEffect`

## Introdução ao Ciclo de Vida

Todo componente React passa por um **ciclo de vida**: uma série de fases desde sua criação até sua destruição. Entender esse ciclo é fundamental para executar ações no momento certo, como buscar dados de uma API ou limpar recursos.

As três fases principais do ciclo de vida são:

1.  **Montagem (Mounting):** O componente é criado e inserido no DOM.
2.  **Atualização (Updating):** O componente é renderizado novamente devido a uma mudança em suas `props` ou `state`.
3.  **Desmontagem (Unmounting):** O componente é removido do DOM.

Em componentes de classe, essas fases eram gerenciadas por métodos como `componentDidMount`, `componentDidUpdate` e `componentWillUnmount`. Em componentes funcionais, usamos o Hook `useEffect` para lidar com esses "efeitos colaterais" (side effects).

## O que é o `useEffect`?

O `useEffect` é um Hook que permite executar efeitos colaterais em componentes funcionais. Efeitos colaterais são quaisquer ações que interagem com o "mundo exterior" fora do fluxo de renderização do React.

Exemplos de efeitos colaterais:
*   Buscar dados de uma API (data fetching).
*   Manipular o DOM diretamente.
*   Configurar e limpar assinaturas (subscriptions) ou timers (`setInterval`).
*   Atualizar o título da página (`document.title`).

### Sintaxe Básica

```jsx
import React, { useState, useEffect } from 'react';

function MeuComponente() {
    // O código dentro do useEffect será executado após cada renderização.
    useEffect(() => {
        console.log('Componente renderizou ou atualizou!');
    });

    return <div>...</div>;
}
```

## Controlando a Execução com o Array de Dependências

A chave para dominar o `useEffect` é o seu segundo argumento opcional: o **array de dependências**. Ele controla *quando* o efeito deve ser executado novamente.

### 1. Executar Apenas na Montagem

Para executar um efeito apenas uma vez, quando o componente é montado (semelhante a `componentDidMount`), passe um array vazio `[]`.

**Uso:** Ideal para buscar dados iniciais.

```jsx
useEffect(() => {
    // Este código executa apenas uma vez, após a primeira renderização.
    console.log('Componente montado!');
}, []); // <-- Array de dependências vazio
```

### 2. Executar em Resposta a Mudanças

Para executar o efeito sempre que um valor específico (uma `prop` ou um `state`) mudar, adicione esse valor ao array de dependências.

**Uso:** Buscar novos dados quando um ID muda, ou reagir a uma mudança de estado.

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
    // Este código executa na montagem E sempre que 'count' mudar.
    document.title = `Você clicou ${count} vezes`;
}, [count]); // <-- Depende da variável 'count'
```

### 3. Executar em Toda Renderização

Se você omitir o array de dependências, o efeito será executado **após cada renderização**, seja na montagem ou em qualquer atualização. Use com cuidado, pois pode levar a loops infinitos se o efeito atualizar um estado.

```jsx
useEffect(() => {
    // CUIDADO: Executa em toda renderização.
    console.log('Renderizou de novo!');
}); // <-- Sem array de dependências
```

## A Função de Limpeza (Cleanup)

O `useEffect` pode retornar uma função. Essa função, chamada de "função de limpeza" (cleanup function), é executada antes de o componente ser desmontado (semelhante a `componentWillUnmount`).

Ela também é executada antes de o efeito ser executado novamente (em caso de atualizações).

**Uso:** Essencial para evitar vazamentos de memória (memory leaks), como cancelar assinaturas, limpar timers ou remover event listeners.

```jsx
useEffect(() => {
    // Efeito: Inicia um timer
    const timerId = setInterval(() => {
        console.log('Tick');
    }, 1000);

    // Função de Limpeza: É executada quando o componente é desmontado.
    return () => {
        clearInterval(timerId);
        console.log('Timer limpo!');
    };
}, []); // Executa o efeito na montagem e a limpeza na desmontagem.
```

## Exemplo Prático: Buscando Dados de uma API

Vamos juntar tudo em um exemplo que busca uma lista de usuários de uma API quando o componente é montado.

```jsx
import React, { useState, useEffect } from 'react';

function ListaDeUsuarios() {
    const [usuarios, setUsuarios] = useState([]);
    const [loading, setLoading] = useState(true);
    const [error, setError] = useState(null);

    useEffect(() => {
        // Função assíncrona para buscar os dados
        const fetchUsuarios = async () => {
            try {
                const response = await fetch('https://jsonplaceholder.typicode.com/users');
                if (!response.ok) {
                    throw new Error('Falha ao buscar dados');
                }
                const data = await response.json();
                setUsuarios(data);
            } catch (err) {
                setError(err.message);
            } finally {
                setLoading(false);
            }
        };

        fetchUsuarios();
    }, []); // Array vazio para executar apenas na montagem

    if (loading) {
        return <div>Carregando...</div>;
    }

    if (error) {
        return <div>Erro: {error}</div>;
    }

    return (
        <div>
            <h1>Lista de Usuários</h1>
            <ul>
                {usuarios.map(user => (
                    <li key={user.id}>{user.name}</li>
                ))}
            </ul>
        </div>
    );
}

export default ListaDeUsuarios;
```

### Resumo

| Quando executar o efeito? | Como fazer? | Equivalente em Classe |
| :--- | :--- | :--- |
| **Após cada renderização** | `useEffect(() => { ... });` | `componentDidMount` + `componentDidUpdate` |
| **Apenas na montagem** | `useEffect(() => { ... }, []);` | `componentDidMount` |
| **Na montagem e quando um valor `v` muda** | `useEffect(() => { ... }, [v]);` | `componentDidUpdate` (com verificação `if`) |
| **Na desmontagem (limpeza)** | `useEffect(() => { return () => { ... } }, []);` | `componentWillUnmount` |
