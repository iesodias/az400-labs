# Laboratório Prático: Visão Geral do Azure DevOps

## Introdução

O **Azure DevOps** é um conjunto de ferramentas da Microsoft que permite às equipes planejar, desenvolver, entregar e gerenciar software de forma eficiente. Este laboratório oferece uma visão geral dos principais serviços do Azure DevOps e orienta na criação e configuração de um projeto básico.

## Objetivos

- Compreender os principais serviços do Azure DevOps.
- Criar e configurar um projeto no Azure DevOps.
- Navegar e utilizar os serviços fundamentais: Boards, Repos, Pipelines, Test Plans e Artifacts.

## Pré-requisitos

- Conta ativa no [Azure DevOps](https://dev.azure.com/).
- Permissões para criar novos projetos e recursos dentro do Azure DevOps.

## Passo 1: Criar um Novo Projeto

1. **Acessar o Portal do Azure DevOps**:
   - Navegue até [https://dev.azure.com/](https://dev.azure.com/) e faça login com sua conta Microsoft.

2. **Criar um Projeto**:
   - Clique em **"New Project"**.
   - Insira um nome para o projeto, por exemplo, `Projeto-Lab`.
   - Opcionalmente, adicione uma descrição.
   - Selecione a visibilidade do projeto: **Pública** ou **Privada**.
   - Clique em **"Create"**.

## Passo 2: Explorar os Serviços Principais

### 2.1 Azure Boards

- **Descrição**: Ferramenta de planejamento e rastreamento de trabalho que suporta metodologias ágeis, como Scrum e Kanban.&#8203;:contentReference[oaicite:0]{index=0}

- **Ações**:
  - Navegue até **Boards** no menu lateral.
  - Crie um **Work Item**:
    - Clique em **"New Work Item"** e selecione **"Task"**.
    - Insira um título e uma descrição.
    - Atribua a tarefa a um membro da equipe.
    - Defina a prioridade e o estado.
    - Clique em **"Save & Close"**.

### 2.2 Azure Repos

- **Descrição**: :contentReference[oaicite:1]{index=1}&#8203;:contentReference[oaicite:2]{index=2}

- **Ações**:
  - Acesse **Repos** no menu lateral.
  - Clone o repositório:
    - Clique em **"Clone"** e copie a URL.
    - No terminal, execute: `git clone <URL-do-repositório>`
  - Adicione e faça commit de um arquivo:
    - Crie um novo arquivo no diretório clonado.
    - Execute `git add <nome-do-arquivo>` e `git commit -m "Mensagem de commit"`.
    - Envie as alterações: `git push origin main`.

### 2.3 Azure Pipelines

- **Descrição**: :contentReference[oaicite:3]{index=3}&#8203;:contentReference[oaicite:4]{index=4}

- **Ações**:
  - Vá para **Pipelines** no menu lateral.
  - Clique em **"Create Pipeline"**.
  - Selecione a fonte do código (por exemplo, Azure Repos Git).
  - Escolha o repositório e a configuração de pipeline (por exemplo, YAML).
  - Defina as etapas do pipeline:
    - Build: Compile o código.
    - Test: Execute testes automatizados.
    - Deploy: Implemente a aplicação em um ambiente específico.
  - Salve e execute o pipeline.

### 2.4 Azure Test Plans

- **Descrição**: :contentReference[oaicite:5]{index=5}&#8203;:contentReference[oaicite:6]{index=6}

- **Ações**:
  - Acesse **Test Plans** no menu lateral.
  - Crie um plano de teste:
    - Clique em **"New Test Plan"**.
    - Insira um nome e selecione uma área e iteração.
    - Adicione **Test Suites** e **Test Cases** conforme necessário.

### 2.5 Azure Artifacts

- **Descrição**: :contentReference[oaicite:7]{index=7}&#8203;:contentReference[oaicite:8]{index=8}

- **Ações**:
  - Navegue até **Artifacts** no menu lateral.
  - Crie um feed:
    - Clique em **"New Feed"**.
    - Insira um nome e defina permissões.
    - Publique e consuma pacotes utilizando o feed criado.

## Conclusão

Este laboratório proporcionou uma visão geral dos principais serviços do Azure DevOps e orientou na criação e configuração de um projeto básico. Para aprofundar seus conhecimentos, explore a [documentação oficial do Azure DevOps](https://learn.microsoft.com/pt-br/azure/devops/user-guide/services?view=azure-devops) e pratique com cenários reais.

**Referências**:

- [Visão geral dos serviços - Azure DevOps](https://learn.microsoft.com/pt-br/azure/devops/user-guide/services?view=azure-devops)
- [Visão geral das ferramentas de DevOps para Azure DevOps](https://learn.microsoft.com/pt-br/azure/devops/user-guide/devops-alm-overview?view=azure-devops)
