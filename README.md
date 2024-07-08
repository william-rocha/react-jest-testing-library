+++
# Como testar aplicações React usando Jest & Testing Library

## Introdução
- Oi pessoal, tudo bem? Eu sou a Fer e no vídeo de hoje eu vou te ensinar como testar sua aplicação frontend usando o **Jest** e a **Testing Library**.
- Vamos entender o que são essas ferramentas, o papel delas e como elas auxiliam na criação de testes unitários.

## Jest
- **Jest** é uma biblioteca para criação de testes unitários em aplicações JavaScript.
- Fornece funções, ferramentas e ambiente para rodar e criar testes unitários.
- Documentação detalha a configuração do Jest.
- **Create React App** já traz o Jest pré-configurado.
- Se você não usou Create React App, pode seguir o passo a passo da documentação do Jest para configurar.

## Testing Library
- **Testing Library** fornece utilitários para escrever cenários de testes unitários.
- Diferente do Jest, não fornece um ambiente para rodar testes, mas sim funções utilitárias.
- Suporte para várias bibliotecas frontend como **React**, **Angular**, **Vue**, **Svelte**.
- Funções para interação com a **DOM** e simulação de ações do usuário.

## Aplicação Exemplo
- Aplicação é um editor de texto online onde o usuário pode criar, salvar, visualizar, excluir e favoritar arquivos.
- Vamos escrever testes unitários para os componentes dessa aplicação.

## Criando Testes
### Configuração Inicial
- Arquivos de teste devem ter a extensão `.test.tsx`.
- Jest identifica e roda arquivos de teste automaticamente.

### Testando a NavBar
- **NavBar**: componente lateral onde o usuário pode clicar para abrir abas.
- Vamos criar um teste para manipulação da **DOM**: cliques nos elementos e verificação de elementos em tela.

#### Configuração e Renderização
- Criar o arquivo de teste para o componente `NavBar`.
- Utilizar o método **describe** do Jest para declarar um **test suite**.
- Métodos **it** ou **test** são usados para declarar **test cases**.
- Utilizar a função **render** da Testing Library para renderizar o componente.

#### Verificação de Elementos
- Utilizar **screen** para acessar a **DOM virtual**.
- Métodos **getByText** e **findByText** ajudam a buscar elementos na DOM.
- **getByText** lança erro se não encontrar o elemento, enquanto **findByText** retorna `undefined`.

#### Verificação de Ações
- Utilizar **fireEvent** da Testing Library para disparar eventos como cliques.
- Utilizar **jest.mock** para simular importações reais.
- Verificar se funções são chamadas corretamente usando **jest.fn**.

#### Exemplo de Teste
```jsx
import { render, screen, fireEvent } from '@testing-library/react';
import NavBar from '../components/NavBar';
import { BrowserRouter } from 'react-router-dom';
import { jest } from '@jest/globals';

describe('NavBar Component', () => {
  beforeEach(() => {
    jest.resetModules();
  });

  it('should render without errors', () => {
    render(
      <BrowserRouter>
        <NavBar />
      </BrowserRouter>
    );

    expect(screen.getByText('All files')).toBeInTheDocument();
    expect(screen.getByText('Favorites')).toBeInTheDocument();
  });

  it('should call navigate on click', () => {
    const mockNavigate = jest.fn();
    jest.mock('react-router-dom', () => ({
      ...jest.requireActual('react-router-dom'),
      useNavigate: () => mockNavigate,
    }));

    render(
      <BrowserRouter>
        <NavBar />
      </BrowserRouter>
    );

    fireEvent.click(screen.getByText('All files'));
    expect(mockNavigate).toHaveBeenCalledWith('/');
  });
});
```

### Testando a Página FileList
- Página que lista todos os arquivos do usuário.
- Verificação se a página está listando corretamente os arquivos.

#### Configuração e Renderização
- Criar função `renderComponent` para evitar repetição de código.
- Utilizar **beforeEach** para configurar mocks antes de cada teste.

#### Mocando Funções e Valores
- Utilizar **jest.spyOn** para espiar métodos e objetos.
- Utilizar **faker.js** para gerar valores randômicos.

#### Verificação de Elementos
- Verificar se arquivos são renderizados corretamente.
- Verificar se elementos de loading são mostrados corretamente.

#### Exemplo de Teste
```jsx
import { render, screen } from '@testing-library/react';
import FileList from '../pages/FileList';
import { BrowserRouter } from 'react-router-dom';
import { jest } from '@jest/globals';
import faker from 'faker';

describe('FileList Page', () => {
  beforeEach(() => {
    jest.resetModules();
  });

  it('should render all files correctly', () => {
    const files = [
      { id: faker.datatype.uuid(), title: faker.lorem.words(), favorited: false }
    ];

    jest.spyOn(useFiles, 'default').mockReturnValue({
      files,
      favoritedFiles: [],
      isLoading: false,
    });

    render(
      <BrowserRouter>
        <FileList />
      </BrowserRouter>
    );

    expect(screen.getByText(files[0].title)).toBeInTheDocument();
  });

  it('should show loading element when isLoading is true', () => {
    jest.spyOn(useFiles, 'default').mockReturnValue({
      files: [],
      favoritedFiles: [],
      isLoading: true,
    });

    render(
      <BrowserRouter>
        <FileList />
      </BrowserRouter>
    );

    expect(screen.getByTestId('loading')).toBeInTheDocument();
  });
});
```

## Considerações Finais
- Testes seguem o padrão **AAA** (Arrange, Act, Assert).
- Abstração de código repetitivo melhora a legibilidade dos testes.
- Documentação do Jest e Testing Library é fundamental para entender todas as funcionalidades disponíveis.

## Feedback
- Deixe nos comentários se gostariam de ver uma parte 2 com testes mais complexos ou outros tópicos.
- Siga o canal e deixe seu like!

+++
