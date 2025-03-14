# Laboratório: Planejamento Ágil e Gerenciamento de Portfólio com Azure Boards

## Visão Geral

Este laboratório orienta você na utilização das ferramentas de planejamento ágil e gerenciamento de portfólio fornecidas pelo Azure Boards. Você aprenderá a planejar, gerenciar e acompanhar o trabalho de sua equipe de forma eficaz, explorando backlog de produtos, sprints e quadros de tarefas.

## Objetivos

Após concluir este laboratório, você será capaz de:

- Gerenciar equipes, áreas e iterações.
- Gerenciar itens de trabalho.
- Gerenciar sprints e capacidade.
- Personalizar quadros Kanban.
- Definir dashboards.
- Personalizar processos da equipe.

## Pré-requisitos

- **Navegador Compatível**: Microsoft Edge ou outro navegador suportado pelo Azure DevOps.
- **Organização no Azure DevOps**: Caso ainda não tenha uma, crie seguindo as instruções em [Criar uma organização ou coleção de projetos](https://learn.microsoft.com/pt-br/azure/devops/organizations/accounts/create-organization).

## Tempo Estimado

Aproximadamente 60 minutos.

## Instruções

### Exercício 0: Configurar os Pré-requisitos do Laboratório

Neste exercício, você configurará um novo projeto no Azure DevOps com um repositório baseado no eShopOnWeb.

#### Tarefa 1: Criar e Configurar o Projeto da Equipe

1. **Acessar o Azure DevOps**: Abra seu navegador e navegue até sua organização no Azure DevOps.
2. **Criar Novo Projeto**: Clique em **Novo Projeto**.
   - **Nome do Projeto**: `mdc-project`
   - **Visibilidade**: `Privado`
   - **Processo de Itens de Trabalho**: Selecione `Scrum` nas opções avançadas.
3. **Confirmar Criação**: Clique em **Criar**.

### Exercício 1: Gerenciar Projeto Ágil

Neste exercício, você utilizará o Azure Boards para realizar tarefas comuns de planejamento ágil e gerenciamento de portfólio.

#### Tarefa 1: Gerenciar Equipes, Áreas e Iterações

1. **Acessar Configurações do Projeto**: No canto inferior esquerdo, clique em **Configurações do Projeto**.
2. **Criar Nova Equipe**:
   - Vá até a seção **Equipes**.
   - Clique em **Nova Equipe**.
   - **Nome da Equipe**: `mdc-team`
   - Clique em **Criar**.
3. **Configurar Iterações**:
   - Selecione a equipe `mdc-team`.
   - Clique em **Iterações e Caminhos de Área**.
   - Na aba **Iterações**, clique em **+ Selecionar iteração(s)**.
   - Selecione `mdc-project\Sprint 1` e clique em **Salvar e fechar**.
   - Repita o processo para adicionar `Sprint 2` e `Sprint 3` (Clicar em NEW).

#### Tarefa 2: Gerenciar Itens de Trabalho

1. **Acessar Itens de Trabalho**:
   - No menu lateral, clique em **Boards** e selecione **Itens de Trabalho**.
2. **Criar Novo Item**:
   - Clique em **Novo Item de Trabalho** e selecione **História de Usuário**.
   - **Título**: `Implementar funcionalidade de pesquisa`
   - **Atribuído a**: Selecione um membro da equipe.
   - **Área**: `mdc-project\mdc-team`
   - **Iteração**: `mdc-project\Sprint 2`
   - Clique em **Salvar**.

#### Tarefa 3: Gerenciar Sprints e Capacidade

1. **Configurar Sprints**:
   - No menu **Boards**, selecione **Sprints**.
   - Na aba **Configurações**, defina as datas de início e término para `Sprint 2` e `Sprint 3`.
2. **Definir Capacidade**:
   - Na aba **Capacidade**, adicione membros da equipe e defina suas capacidades (horas/dia).

#### Tarefa 4: Personalizar Quadros Kanban

1. **Acessar Quadro Kanban**:
   - No menu **Boards**, selecione **Quadros**.
2. **Personalizar Colunas**:
   - Clique em **Configurações** (ícone de engrenagem).
   - Adicione, remova ou renomeie colunas conforme necessário.
3. **Adicionar Cartões Personalizados**:
   - Na seção **Estilos de Cartão**, defina regras para destacar itens específicos.

#### Tarefa 5: Definir Dashboards

1. **Acessar Dashboards**:
   - No menu **Visão Geral**, selecione **Dashboards**.
2. **Criar Novo Dashboard**:
   - Clique em **Novo Dashboard**.
   - **Nome**: `mdc-team`
   - Selecione a equipe `mdc-team`.
   - Clique em **Criar**.
3. **Adicionar Widgets**:
   - No dashboard, clique em **Adicionar Widget**.
   - Adicione widgets como **Gráfico de Burndown**, **Consulta de Itens de Trabalho**, entre outros.

#### Tarefa 6: Personalizar Processo da Equipe

1. **Acessar Processos**:
   - No menu **Organização**, selecione **Configurações** e depois **Processos**.
2. **Clonar Processo**:
   - Selecione o processo `Scrum` e clique em **Clonar**.
   - **Nome**: `Processo Personalizado mdc-team`
   - Clique em **Criar Processo**.
3. **Personalizar Tipos de Itens**:
   - No novo processo, adicione ou modifique tipos de itens de trabalho conforme necessário.
4. **Associar Processo ao Projeto**:
   - Volte às configurações do projeto `mdc-project`.
   - Em **Configurações do Projeto**, altere o processo para `Processo Personalizado mdc-team`.

## Revisão

Neste laboratório, você aprendeu a utilizar o Azure Boards para realizar diversas tarefas de planejamento ágil e gerenciamento de portfólio, incluindo a gestão de equipes, áreas, iterações, itens de trabalho, sprints, capacidade, personalização de quadros Kanban, definição de dashboards e personalização de processos da equipe.

Para aprofundar seu conhecimento, confira o módulo [Abordagem ágil para desenvolvimento de software](https://learn.microsoft.com/pt-br/training/modules/agile-software-development/) no Microsoft Learn.
