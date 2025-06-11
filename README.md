# Perguntas de entrevistas para vagas de QA

## 1 - Se eu não tenho acesso ao _backend_, mas quero verificar se uma mesma resposta da _API_ sempre gera o mesmo resultado no _frontend_, como posso fazer isso?

<details>
  <summary>Mostrar resposta</summary><br>

`cy.intercept(method, url, staticResponse)`

</details>

---

## 2 - Quais são os _design patterns_ mais comuns utilizados com Cypress?

<details>
  <summary>Mostrar resposta</summary><br>

- _Custom Commands_
- _App Actions_
- _Page Objects_ (infelizmente na minha opinião)
- _Gherkin_ (infelizmente também na minha opinião)
- _fixtures_ para dados de testes e _mocks_
- …

</details>

---

## 3 - Se você está usando um seletor CSS que muda com frequência, exigindo constantes ajustes no script de teste, o que você faria?

<details>
  <summary>Mostrar resposta</summary><br>

1. Procurar um seletor mais estável
2. Adição de atributos `data-testid` para fins de testabilidade
3. Uso das diferentes combinações possíveis com o comando `cy.contains()`.
Ex. `cy.contains('label', 'Phone Number').next().type('5555555') // Imaginando que o próximo elemento depois do label seria o input com o qual quero interagir`

</details>

---

## 4 - Se você precisa testar uma funcionalidade, mas uma parte dela está demorando para renderizar, como você lida com essa situação?

<details>
  <summary>Mostrar resposta</summary><br>

1. Identificar o motivo pelo qual está demorando.

</details>

---

## 5 - Em que situações devo usar `.should()` ou `.then()` no Cypress?

<details>
  <summary>Mostrar resposta</summary><br>

- [`.should`](https://docs.cypress.io/api/commands/should) para _assertions_ (devido ao mecanismo de _retriability_ do Cypress)

**Exemplos:**

```js
cy.get('ul li').should('have.length', 5) // Primeiro aguarda pela quantidade certa de list items
cy.get('li').last().should('have.text', 'some-text') // Para então verificar o conteúdo do último

// Também é possível passar ao comando .should uma função de callback a qual recebe o "sujeito" gerado pelo comando anterior
cy.get('ul li').should(($listItems) => {
  cy.wrap($listItems).each(() => {/* do something with each list item */})
})

```

- [`.then`](https://docs.cypress.io/api/commands/then) para trabalhar com o "sujeito" gerado pelo comando anterior.

```js
cy.request(method, url, body).then((response) => {
  /* lógica que busca um token e o armazena em uma variável "global" que possa ser utilizada por outro comando (ou teste) */
})

```

</details>

## 6 - Como você testaria se um elemento deixou de estar visível na tela?

<details>
  <summary>Mostrar resposta</summary><br>

Primeiro, faço uma asserção positiva para garantir que estou no lugar certo, e então, faço algo como `.should('not.be.visible')` ou `.should('not.exist')` dependendo se o elemento está "escondido" por uma regra de CSS ou se deixou de estar no DOM.

</details>
