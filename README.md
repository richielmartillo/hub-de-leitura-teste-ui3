# Hub de Leitura - Testes UI

Projeto de automação de testes de interface desenvolvido no **Módulo 18** do curso de **Engenharia de Qualidade de Software - EBAC**.

Este repositório tem como objetivo automatizar cenários da aplicação **Hub de Leitura** utilizando **Cypress**, com integração ao **Jenkins** para execução em pipeline e ao **Cypress Cloud** para acompanhamento das execuções.

## Objetivo do projeto

Automatizar fluxos principais da aplicação Hub de Leitura, aplicando conceitos de testes end-to-end e integração contínua vistos durante o módulo.

## Tecnologias utilizadas

- JavaScript
- Node.js
- Cypress
- Jenkins
- Cypress Cloud
- Git
- GitHub
- Allure Report

## Funcionalidades testadas

Os testes automatizados cobrem cenários como:

- Cadastro de usuário
- Login
- Contato
- Catálogo
- Busca no catálogo

## Estrutura do projeto

```bash
.
├── cypress
│   ├── e2e
│   │   ├── cadastro.cy.js
│   │   ├── catalogo-busca.cy.js
│   │   ├── catalogo.cy.js
│   │   ├── contato.cy.js
│   │   └── login.cy.js
│   ├── fixtures
│   ├── screenshots
│   ├── support
│   │   ├── commands.js
│   │   ├── e2e.js
│   │   └── pages
├── allure-results
├── cypress.config.js
├── package.json
├── package-lock.json
├── Jenkinsfile
├── Jenkinsfile-win
└── README.md
```

## Pré-requisitos

Antes de executar o projeto, é necessário ter instalado:

- Node.js
- npm
- Git

## Instalação

Clone o repositório:

```bash
git clone https://github.com/richielmartillo/hub-de-leitura-teste-ui3.git
```

Acesse a pasta do projeto:

```bash
cd hub-de-leitura-teste-ui3
```

Instale as dependências:

```bash
npm install
```

## Como executar os testes

### Executar em modo interativo

```bash
npx cypress open
```

### Executar em modo headless

```bash
npx cypress run
```

## Execução com Cypress Cloud

O projeto também está configurado para integração com o **Cypress Cloud**, permitindo gravar e acompanhar a execução dos testes.

Exemplo de execução:

```bash
npx cypress run --record
```

> Para esse tipo de execução, é necessário que a configuração do projeto esteja correta no ambiente, incluindo `projectId` e `record key` no Cypress Cloud.

## Integração com Jenkins

Este projeto possui arquivos de configuração para execução automatizada com Jenkins:

- Jenkinsfile
- Jenkinsfile-win

A pipeline pode realizar etapas como:

- clonagem do repositório
- instalação das dependências
- execução dos testes automatizados
- integração com Cypress Cloud

## Relatórios

O projeto possui suporte para geração de resultados com **Allure**, armazenados na pasta:

```bash
allure-results
```

## Aprendizados aplicados no módulo

Durante o desenvolvimento deste projeto, foram praticados conceitos como:

- automação de testes UI com Cypress
- organização de estrutura de testes
- integração contínua com Jenkins
- execução de testes em pipeline
- integração com Cypress Cloud
- versionamento com Git e GitHub

## Autor

Desenvolvido por **Richard Marlon Balestrim** como atividade prática do **Módulo 18** do curso de **Engenharia de Qualidade de Software - EBAC**.
