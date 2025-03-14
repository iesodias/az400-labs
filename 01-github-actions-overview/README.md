# 📌 Visão Geral do GitHub Actions

O **GitHub Actions** é uma plataforma de **CI/CD (Integração e Entrega Contínua)** que permite automatizar fluxos de trabalho diretamente dentro do **GitHub**. Com ele, é possível configurar pipelines que realizam **builds, testes e deploys** automatizados, respondendo a eventos específicos, como **push, pull requests ou agendamentos**.

---

## 🔹 **Componentes Principais do GitHub Actions**
### 📌 **Workflows**
- São processos automatizados definidos por arquivos dentro do diretório `.github/workflows`.
- Cada workflow pode ser acionado por eventos e conter múltiplos jobs.

### 📌 **Eventos**
- São gatilhos que **iniciam a execução** de um workflow.
- Exemplos: push, pull_request, schedule, workflow_dispatch.

### 📌 **Jobs**
- Conjunto de tarefas que são executadas em **runners** (máquinas virtuais hospedadas pelo GitHub ou auto-hospedadas).
- Os jobs podem rodar em **paralelo** ou **sequencialmente**.

### 📌 **Steps**
- São as **etapas individuais** dentro de um **job**.
- Podem incluir **scripts personalizados** ou chamadas para **ações reutilizáveis**.

### 📌 **Ações**
- São **componentes reutilizáveis** que realizam tarefas específicas.
- Podem ser utilizadas dentro dos **steps** para evitar código repetitivo.

---

## 🔹 **Navegando pelo GitHub Actions no Portal**
Para explorar e gerenciar workflows no **GitHub Actions** pelo portal web:

### ✅ **1. Acessar a Aba "Actions"**
- Dentro do **repositório**, clique na aba **"Actions"** no menu superior.

### ✅ **2. Visualizar Workflows Existentes**
- A página **Actions** exibe uma **lista de workflows** configurados no repositório.
- Cada workflow contém o **histórico de execuções** e seus status.

### ✅ **3. Acompanhar Logs de Execução**
- Clique em uma **execução específica** para visualizar:
  - **Logs detalhados** de cada etapa.
  - Status de **sucesso ou falha** dos jobs.
  - **Erros ou saídas do terminal**.

### ✅ **4. Criar um Novo Workflow**
- Clique em **"New Workflow"** dentro da aba **Actions**.
- Escolha um **modelo pronto** ou crie um **workflow customizado**.
- Para workflows customizados, crie manualmente um **arquivo** no diretório `.github/workflows/`.

---

## 🔹 **Criando um Workflow Básico**
Agora vamos criar um **workflow simples** que roda **build e testes** para uma aplicação.

### ✅ **1. Criar o Arquivo de Workflow**
- No repositório, navegue até `.github/workflows/` e crie um novo arquivo.

### ✅ **2. Configurar o Workflow**
- Edite o arquivo e defina um fluxo de trabalho que será acionado em eventos específicos, como push na branch principal.

### ✅ **3. Commitar e Push do Workflow**
- Salve as alterações e faça o **commit e push** do arquivo para o repositório.

### ✅ **4. Monitorar a Execução**
- Acesse a aba **"Actions"** no GitHub para visualizar a **execução do workflow**.
- Se houver falhas, clique nos **logs** para depurar e corrigir os problemas.

---

## 🔹 **Personalizando Workflows**
Além do básico, o GitHub Actions permite **personalizações avançadas**, como:

✅ **Execução em Diferentes Ambientes**  
✅ **Workflows Condicionais**  
✅ **Aprovações Manuais**  
✅ **Agendamento de Jobs**  
✅ **Uso de Secrets e Variáveis**  

Para aprender mais, consulte a **[Documentação Oficial do GitHub Actions](https://docs.github.com/pt/actions)**.

🚀 **Agora você está pronto para criar e gerenciar pipelines automatizados no GitHub Actions!** 🚀
