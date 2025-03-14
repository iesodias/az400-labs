# Laboratório Prático: Pipeline no Github Actions (Workflows)

*Este guia é baseado no artigo original de [Ieso Dias](https://www.iesodias.com/post/primeiros-passos-com-o-github-actions-parte-1).*

## Introdução

O **GitHub Actions** é uma ferramenta de automação de fluxos de trabalho integrada ao GitHub, permitindo automatizar processos como integração contínua (CI) e entrega contínua (CD). Este tutorial aborda os conceitos básicos e a criação de um fluxo de trabalho simples.

## O que é o GitHub Actions?

O GitHub Actions permite a automação de tarefas dentro do repositório GitHub, como:

- **Integração Contínua (CI):** Automatizar testes e builds a cada commit.
- **Entrega Contínua (CD):** Automatizar deploys após a aprovação de PRs.
- **Automação de Tarefas:** Executar scripts ou comandos em resposta a eventos.

## Componentes Principais

- **Workflows:** Definem um processo automatizado, composto por um ou mais jobs.
- **Jobs:** Conjuntos de etapas que serão executadas.
- **Steps:** Comandos individuais ou ações que são executadas em um job.
- **Actions:** Tarefas reutilizáveis que podem ser compartilhadas entre workflows.

## Criando um Workflow Básico

1. **Estrutura de Pastas:**
   - Dentro do repositório, crie a pasta `.github/workflows/`.

2. **Arquivo de Workflow:**
   - Dentro da pasta `workflows`, crie um arquivo YAML, por exemplo, `ci.yml`.

3. **Definindo o Workflow:**
   - No arquivo `ci.yml`, defina o nome do workflow e o evento que irá acioná-lo:

     ```yaml
     name: CI Pipeline
     on:
       push:
         branches:
           - main
     ```

4. **Definindo Jobs:**
   - Adicione jobs ao workflow:

```yaml
name: CI/CD Pipeline

on: push

jobs:
  build_dev:
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: 'dev'
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up environment
      run: echo "Setting up $ENVIRONMENT environment"

    - name: Install dependencies
      run: echo "Installing dependencies for $ENVIRONMENT"

    - name: Build App
      run: echo "Building app for $ENVIRONMENT environment"

    - name: Test App
      run: echo "Testing app for $ENVIRONMENT environment"

    - name: Deploy App
      run: echo "Deploying app to $ENVIRONMENT environment"

  build_qa:
    needs: build_dev
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: 'qa'
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up environment
      run: echo "Setting up $ENVIRONMENT environment"

    - name: Install dependencies
      run: echo "Installing dependencies for $ENVIRONMENT"

    - name: Build App
      run: echo "Building app for $ENVIRONMENT environment"

    - name: Test App
      run: echo "Testing app for $ENVIRONMENT environment"

    - name: Deploy App
      run: echo "Deploying app to $ENVIRONMENT environment"

  build_hml:
    needs: build_qa
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: 'hml'
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up environment
      run: echo "Setting up $ENVIRONMENT environment"

    - name: Install dependencies
      run: echo "Installing dependencies for $ENVIRONMENT"

    - name: Build App
      run: echo "Building app for $ENVIRONMENT environment"

    - name: Test App
      run: echo "Testing app for $ENVIRONMENT environment"

    - name: Deploy App
      run: echo "Deploying app to $ENVIRONMENT environment"

  build_prd:
    needs: build_hml
    runs-on: ubuntu-latest
    env:
      ENVIRONMENT: 'prd'
    steps:
    - name: Checkout code
      uses: actions/checkout@v2

    - name: Set up environment
      run: echo "Setting up $ENVIRONMENT environment"

    - name: Install dependencies
      run: echo "Installing dependencies for $ENVIRONMENT"

    - name: Build App
      run: echo "Building app for $ENVIRONMENT environment"

    - name: Deploy App
      run: echo "Deploying app to $ENVIRONMENT environment"

```

## Executando o Workflow

Após configurar e commitar o arquivo `ci.yml`, o GitHub Actions executará o workflow definido sempre que houver um push na branch `main`. Você pode acompanhar a execução na aba "Actions" do repositório.

## Conclusão

Este tutorial apresentou uma introdução ao GitHub Actions, demonstrando como configurar um workflow básico. Para aprofundar seus conhecimentos, consulte a [documentação oficial do GitHub Actions](https://docs.github.com/pt/actions).

*Referência: [Primeiros passos com o GitHub Actions - Parte 1](https://www.iesodias.com/post/primeiros-passos-com-o-github-actions-parte-1)*
