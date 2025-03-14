# Laboratório Prático: Criando uma Pipeline no Azure DevOps

## Visão Geral

Este laboratório orienta você na criação de uma pipeline no Azure DevOps utilizando um arquivo YAML. A pipeline será composta por múltiplos estágios, incluindo:

- **Build:** Compilação da aplicação.
- **Análise de Código Estático:** Verificação da qualidade e segurança do código.
- **Testes Unitários:** Execução de testes para validar funcionalidades.
- **Teste de Carga:** Avaliação do desempenho sob carga.
- **Deploy para DEV, HML e PRD:** Implantação em diferentes ambientes.

## Pré-requisitos

- **Conta no Azure DevOps:** Acesse [Azure DevOps](https://dev.azure.com/) e faça login ou crie uma conta.
- **Projeto no Azure DevOps:** Tenha um projeto existente ou crie um novo.
- **Repositório Git:** Utilize um repositório Git dentro do seu projeto no Azure DevOps.

## Passo 1: Criar o Arquivo de Pipeline YAML

1. **Acesse o Repositório:**
   - No seu projeto do Azure DevOps, vá para **Repos** > **Files**.

2. **Criar o Arquivo YAML:**
   - Dentro do diretório raiz do repositório, crie uma pasta chamada `.azure-pipelines`.
   - Dentro dessa pasta, crie um arquivo chamado `pipeline.yml`.

3. **Definir o Conteúdo do Arquivo YAML:**
   - Insira o seguinte conteúdo no arquivo `pipeline.yml`:

```yaml
trigger:
- main

pool:
vmImage: 'ubuntu-latest'

stages:
- stage: Build
displayName: 'Build Stage'
jobs:
- job: Build
    displayName: 'Build Job'
    steps:
    - script: echo "Building the application..."
    displayName: 'Run Build'

- stage: Static_Code_Analysis
displayName: 'Static Code Analysis'
dependsOn: Build
jobs:
- job: Analysis
    displayName: 'Run Static Analysis'
    steps:
    - script: echo "Running static code analysis with SonarQube..."
    displayName: 'Run SonarQube Analysis'
    - script: echo "Running ESLint for JavaScript code..."
    displayName: 'Run ESLint'

- stage: Unit_Tests
displayName: 'Run Unit Tests'
dependsOn: Static_Code_Analysis
jobs:
- job: Test
    displayName: 'Run Tests'
    steps:
    - script: echo "Running unit tests..."
    displayName: 'Run Unit Tests'

- stage: Load_Test
displayName: 'Run Load Test'
dependsOn: Unit_Tests
jobs:
- job: LoadTest
    displayName: 'Run Load Test'
    steps:
    - script: echo "Running load test with Apache JMeter..."
    displayName: 'Run JMeter Load Test'
    - script: echo "Generating load test report..."
    displayName: 'Generate Load Test Report'

- stage: Deploy_DEV
displayName: 'Deploy to DEV'
dependsOn: Load_Test
jobs:
- job: Deploy
    displayName: 'Deploy Job'
    steps:
    - script: echo "Deploying to DEV environment..."
    displayName: 'Deploy to DEV'

- stage: Deploy_HML
displayName: 'Deploy to HML'
dependsOn: Deploy_DEV
jobs:
- job: Deploy
    displayName: 'Deploy Job'
    steps:
    - script: echo "Deploying to HML environment..."
    displayName: 'Deploy to HML'

- stage: Deploy_PRD
displayName: 'Deploy to PRD'
dependsOn: Deploy_HML
jobs:
- job: Deploy
    displayName: 'Deploy Job'
    steps:
    - script: echo "Deploying to PRD environment..."
    displayName: 'Deploy to PRD'
    - script: echo "Approval required for PRD deployment..."
    displayName: 'Wait for approval'
```

## Passo 2: Configurar a Pipeline no Azure DevOps

1. **Acesse Pipelines:**
   - No seu projeto do Azure DevOps, vá para **Pipelines** > **Pipelines**.

2. **Criar uma Nova Pipeline:**
   - Clique em **"New Pipeline"**.
   - Selecione **"Azure Repos Git"** como fonte de código.
   - Escolha o repositório onde o arquivo `pipeline.yml` foi adicionado.
   - Na etapa de configuração, selecione **"Existing Azure Pipelines YAML file"**.
   - Navegue até o arquivo `.azure-pipelines/pipeline.yml`.
   - Clique em **"Continue"**.

3. **Salvar e Executar:**
   - Revise as configurações da pipeline.
   - Clique em **"Save and run"**.
   - Insira uma mensagem de commit, se necessário, e confirme.

## Passo 3: Monitorar a Execução da Pipeline

1. **Acompanhar a Execução:**
   - Após iniciar a pipeline, você será redirecionado para a página de execução.
   - Acompanhe cada estágio e job conforme são executados.

2. **Verificar Resultados:**
   - Clique em cada estágio para visualizar logs e resultados detalhados.
   - Em caso de falhas, os logs fornecerão informações para diagnóstico.

## Passo 4: Configurar Aprovação Manual para Deploy em Produção

1. **Adicionar Aprovação Manual:**
   - No arquivo `pipeline.yml`, localize o estágio `Deploy_PRD`.
   - Adicione a propriedade `approval` para requerer aprovação manual:

     ```yaml
     - stage: Deploy_PRD
       displayName: 'Deploy to PRD'
       dependsOn: Deploy_HML
       jobs:
       - job: Deploy
         displayName: 'Deploy Job'
         steps:
         - script: echo "Deploying to PRD environment..."
           displayName: 'Deploy to PRD'
         - script: echo "Approval required for PRD deployment..."
           displayName: 'Wait for approval'
       approval:
         steps:
         - script: echo "Awaiting manual approval..."
           displayName: 'Manual Approval'
     ```

2. **Salvar Alterações:**
   - Commit e push das alterações no arquivo `pipeline.yml`.

3. **Executar Pipeline:**
   - Inicie a pipeline novamente e observe que o estágio de deploy em produção agora requer aprovação manual.

## Conclusão

Você configurou uma pipeline no Azure DevOps com múltiplos estágios, desde a compilação até a implantação em produção, incluindo aprovações manuais. Essa estrutura modulariza o processo de CI/CD, garantindo maior controle e qualidade nas entregas.

**Referências Adicionais:**

- [Criar um pipeline com estágios - Azure Pipelines](https://learn.microsoft.com/pt-br/azure/devops/pipelines/process/run-stages?view=azure-devops)
- [Tutorial: Criar um pipeline de vários estágios com o Azure DevOps](https://learn.microsoft.com/
::contentReference[oaicite:0]{index=0}
 
