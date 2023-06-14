# Arquitetura Limpa

Este é um exemplo simples de um aplicativo TODO que demonstra uma abordagem de arquitetura limpa em VueJs.

Tecnologias usadas:

- **VueJs** com **TypeScript**
- **Vite** como ferramenta de construção
- **Vuex** para gerenciamento de estado com **Decoradores de Módulo Vuex**
- **Inversify** para injeção de dependência
- **Tailwindcss** para uma interface de usuário bonita e simples
- **PurifyTs** para uso de Either nos casos de uso

Este projeto é dividido em 3 camadas.

A estrutura do pacote é **orientada por recursos**.
Isso significa que para cada recurso, existe um pacote.
Em cada recurso, as 3 camadas são representadas como seus próprios sub-pacotes.

Neste caso, há apenas um recurso 'todo', que lida com a criação, leitura, atualização e exclusão de tarefas a serem feitas.

```
├── core
│ └── app
│       ├── App.vue
│       ├── components
│       ├── store
│ └── domain
│       ├── failure.ts
│       ├── usecase.ts
│ └── infrastructure
├── features
│ └── foofeature
│       └── application
│       └── domain
│           ├── model
│           ├── port
│           ├── usecase
│       └── infrastructure
│           ├── entity
```

## App

O ponto de entrada e a camada mais externa para a aplicação.
Inclui todo o código específico do Vue, como arquivos .vue, configuração do vuex e seus módulos.

O ponto de entrada em um SPA (Single Page Application) é, neste caso, o App.vue, que reside no pacote **core/app**.

### Store

O gerenciamento de estado é feito pelo vuex, que por sua vez lida com a comunicação com o domínio, também conhecido como casos de uso.
Cada recurso é representado por seu próprio módulo, portanto, para o recurso Todo, existe um todoModule.ts.

## Domain

A camada interna que contém todos os serviços para lidar com a lógica de negócios e as regras de negócios.

A camada em si é dividida em **model**, **ports** e **usecases**.

### Model

A representação dos dados recuperados nos ports e utilizados nos casos de uso.

### Port

Ou portas externas, são as interfaces de porta para se comunicar com o mundo externo (infraestrutura).
(Regra de inversão de dependência)

### Usecases

Ou portas internas, definindo as interfaces para a lógica de negócios e as regras de negócios.
Cada caso de uso é implementado por seu serviço.

## Infrastructure

Código específico do framework e/ou implementação das portas externas do domínio para acessar os dados do "mundo externo".
O exemplo mais proeminente seria a camada para acessar algum servidor externo via http/s.

---

### Para simplificar:

Imagine que você tem um aplicativo que precisa criar, ler, atualizar e excluir tarefas (conhecido como TODO). O VueJs é o framework principal que você está usando para criar esse aplicativo. Você também

usa **TypeScript** para escrever seu código, o que fornece recursos de programação mais avançados e seguros do que o JavaScript padrão.

O `Vite` é a ferramenta que você usa para construir (ou seja, compilar e empacotar) seu aplicativo. Vuex é a ferramenta que você usa para gerenciar o estado do seu aplicativo. Em outras palavras, Vuex ajuda você a manter o controle dos dados que estão sendo usados e modificados em seu aplicativo.

`Inversify` é uma ferramenta que você usa para a injeção de dependência. Isso significa que ele ajuda a organizar seu código de maneira que diferentes partes de seu aplicativo possam trabalhar juntas de maneira mais eficiente.

`PurifyTs` é uma biblioteca que você usa para implementar um padrão de programação chamado "Either". Esse padrão pode ajudá-lo a lidar com erros e situações imprevistas em seu código.

Seu aplicativo é dividido em três "camadas": `App`, `Domain` e `Infrastructure`. A camada App é a parte mais externa do aplicativo, que lida com a interação do usuário e a exibição de informações na tela. A camada Domain é a parte interna do aplicativo que lida com a lógica de negócios. A camada Infrastructure é a parte do aplicativo que lida com a comunicação com o mundo exterior, como fazer solicitações de rede.

Cada recurso (como a funcionalidade TODO) tem seu próprio pacote, que contém suas próprias subcamadas.

Por exemplo, no caso do recurso TODO, a camada de `Model` (**features/todo/infrastructure/model**) representaria a estrutura de dados de uma tarefa, a camada de `Ports` (**features/todo/domain/ports**) seria responsável pela comunicação com o mundo exterior (como uma base de dados ou um serviço web) e a camada de `Use cases` (**features/todo/domain/usecases**) seria onde a lógica para criar, ler, atualizar e deletar uma tarefa seria implementada.
