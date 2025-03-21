# Laboratório Prático: Deploy de Infraestrutura com Bicep via GitHub Actions

## Visão Geral

Neste laboratório vamos configurar um workflow no GitHub Actions para realizar o deploy automatizado de uma infraestrutura no Azure usando arquivos Bicep

Esse pipeline vai:

- Fazer login no Azure usando um Service Principal
- Criar o resource group caso ele não exista
- Executar o deploy do template Bicep
- Exibir o IP público da VM criada

## Pré-requisitos

- **Conta no GitHub:** https://github.com
- **Conta no Azure:** https://portal.azure.com
- **Azure CLI instalada localmente** (para criar o service principal): https://learn.microsoft.com/cli/azure/install-azure-cli
- **Repositório com o arquivo `main.bicep` pronto**

## Passo 1: Criar um Service Principal para o GitHub

No seu terminal local execute o seguinte comando:

```bash
az ad sp create-for-rbac \
  --name "mdcgithubactions" \
  --role contributor \
  --scopes /subscriptions/b4afae6b-342d-47f7-82b5-FAKE-sub \
  --sdk-auth
```

Esse comando vai retornar um JSON como esse:

```json
{
  "clientId": "...",
  "clientSecret": "...",
  "subscriptionId": "...",
  "tenantId": "...",
  "activeDirectoryEndpointUrl": "...",
  "resourceManagerEndpointUrl": "...",
  "...": "..."
}
```

Copie **todo o JSON** pois usaremos no GitHub como segredo

## Passo 2: Adicionar Secrets no GitHub

Acesse seu repositório no GitHub > **Settings** > **Secrets and variables** > **Actions** > **New repository secret**

### 1. `AZURE_CREDENTIALS`

Cole o JSON completo gerado pelo comando do passo anterior

### 2. `ADMIN_PASSWORD`

Coloque a senha da VM que será usada no parâmetro `adminPassword` do Bicep

Exemplo:
```
A!9f#2Lq@8s&7Gz
```

## Passo 3: Criar o Workflow do GitHub Actions

Crie o arquivo `.github/workflows/deploy-bicep.yml` com o seguinte conteúdo:

```yaml
name: Deploy Bicep to Azure

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout do código
        uses: actions/checkout@v3

      - name: Login no Azure
        uses: azure/login@v1
        with:
          creds: ${{ secrets.AZURE_CREDENTIALS }}

      - name: Criar o resource group (caso não exista)
        run: |
          az group create \
            --name MeuGrupoBicep \
            --location eastus

      - name: Deploy do Bicep
        run: |
          az deployment group create \
            --resource-group MeuGrupoBicep \
            --template-file main.bicep \
            --parameters adminPassword='${{ secrets.ADMIN_PASSWORD }}'

      - name: Obter IP público da VM
        run: |
          az network public-ip show \
            --resource-group MeuGrupoBicep \
            --name mac-lab-bicep-pip \
            --query ipAddress \
            --output tsv
```

## Passo 4: Fazer o Push do Código

Envie o código para o repositório no branch `main`:

```bash
git add .
git commit -m "adiciona pipeline de deploy bicep"
git push origin main
```

## Passo 5: Verificar a Execução

Vá para o repositório no GitHub > **Actions** > clique no workflow em execução e acompanhe os logs

No final ele vai mostrar o IP público da VM criada no terminal da execução

## Passo 6: Conectar na VM via SSH (opcional)

Se quiser testar o acesso à VM criada:

```bash
ssh azureuser@<ip-publico>
```

Digite a senha definida em `ADMIN_PASSWORD`


