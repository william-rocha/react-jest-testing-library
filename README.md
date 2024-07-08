+++
# Como testar aplicações React usando Jest & Testing Library

## Introdução

- **Ferramentas:** Jest e Testing Library
  - **Jest:** Biblioteca para criação de **testes unitários** em aplicações **JavaScript**. Fornece funções, ferramentas e um ambiente para rodar testes.
  - **Testing Library:** Fornece utilitários para escrita de cenários de testes unitários, suportando bibliotecas como **React**, **Angular** e **Vue**.

## Configuração do Jest

1. **Criação de aplicação com Create React App (CRA):**
   - CRA já vem pré-configurado com Jest.
2. **Configuração manual:**
   - Seguir a documentação oficial do Jest para configurar.

## Testing Library

- Fornece utilitários para interagir com a **DOM** e simular ações do usuário.
- Suporte a diversas bibliotecas **frontend** como **React**, **Angular** e **Svelte**.

## Exemplo de aplicação para testes

- **Aplicação:** Editor de texto online
  - Funcionalidades:
    - Criação de novos arquivos de texto.
    - Visualização, exclusão e favoritação de arquivos.

## Escrevendo testes unitários

### Testando o componente Navbar

1. **Estrutura inicial:**
   - Criação de um teste para o componente Navbar.
   - Uso de extensão `.test.tsx` para os arquivos de teste.

2. **Configuração do teste:**
   - Criação do **teste suite** usando `describe`.
   - Importação de `render` da Testing Library para renderizar componentes React.

3. **Verificação de elementos:**
   - Uso do objeto `screen` e método `getByText` para buscar elementos na DOM virtual.
   - Uso do método `expect` para verificar se os elementos estão no documento.

4. **Teste de navegação:**
   - Mocagem de funções usando `jest.fn()`.
   - Verificação de chamadas de funções específicas.

5. **Refatoração de código:**
   - Criação de função `renderComponent` para reduzir repetição de código.
   - Uso de padrão **AAA (Arrange-Act-Assert)** para organizar os testes.

### Testando a página FileList

1. **Configuração inicial:**
   - Criação de pasta `__tests__` dentro da pasta de páginas.
   - Teste inicial para verificar a renderização dos arquivos.

2. **Mocagem de hooks:**
   - Uso de `jest.spyOn` para observar e modificar o comportamento de hooks.
   - Simulação de retornos diferentes para testar vários cenários.

3. **Verificação de estados:**
   - Testes para verificar se o componente mostra um elemento de loading.
   - Uso de `data-testid` para identificar elementos específicos na DOM.

4. **Teste de arquivos favoritados:**
   - Verificação se a lista exibe apenas os arquivos favoritados com base na URL.
   - Uso de métodos de busca como `queryByText` para verificar ausência de elementos.

5. **Refatoração final:**
   - Uso de funções auxiliares como `mountFile` para simplificar a criação de arquivos nos testes.
   - Aplicação de `beforeEach` para configuração de mocks padrão.

+++
