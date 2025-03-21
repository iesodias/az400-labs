# Laboratório Prático: Introdução ao Azure Automation

## Visão Geral

Neste laboratório vamos aprender a usar o Azure Automation para automatizar tarefas de gerenciamento no Azure usando runbooks

Vamos criar uma conta de Automation um runbook em PowerShell e executar esse runbook para gerenciar uma VM

## Pré-requisitos

- Conta no Azure
- Azure CLI instalada ou acesso ao portal Azure
- Uma VM existente (como a criada nos labs anteriores)

---

## Passo 1: Criar o Resource Group (caso ainda não exista)

```bash
az group create --name MeuGrupoAutomation --location eastus
```

---

## Passo 2: Criar uma conta de Azure Automation

```bash
az automation account create \
  --name MinhaContaAutomation \
  --resource-group MeuGrupoAutomation \
  --location eastus \
  --sku Free
```

---

## Passo 3: Criar um Runbook em branco

```bash
az automation runbook create \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --name IniciarVMRunbook \
  --type PowerShell
```

---

## Passo 4: Editar o Runbook com script para iniciar uma VM

Crie um arquivo chamado `iniciar-vm.ps1` com o seguinte conteúdo:

```powershell
param(
  [string] $resourceGroup = "MeuGrupoBicep",
  [string] $vmName = "mac-lab-bicep"
)

Start-AzVM -ResourceGroupName $resourceGroup -Name $vmName
```

Envie o script para o runbook:

```bash
az automation runbook replace-content \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --name IniciarVMRunbook \
  --content @iniciar-vm.ps1
```

---

## Passo 5: Publicar o Runbook

```bash
az automation runbook publish \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --name IniciarVMRunbook
```

---

## Passo 6: Executar o Runbook Manualmente

```bash
az automation runbook start \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --name IniciarVMRunbook
```

---

## Passo 7: Monitorar a Execução via CLI

```bash
az automation job list \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --output table
```

---

## Passo 8: Monitorar e Gerenciar no Portal Azure

1. Acesse o [Portal do Azure](https://portal.azure.com)
2. Pesquise por **"Contas de Automação"** e clique na conta **MinhaContaAutomation**
3. No menu lateral, clique em **Runbooks** e selecione o runbook **IniciarVMRunbook**
4. Clique em **Jobs** para visualizar as execuções e logs
5. Clique em um Job para ver detalhes, status e logs de saída

Essa visualização é útil para verificar resultados, logs de erro e rastrear execuções programadas

---

## Passo 9: Agendar o Runbook (opcional)

Crie um agendamento:

```bash
az automation schedule create \
  --resource-group MeuGrupoAutomation \
  --automation-account-name MinhaContaAutomation \
  --name AgendarVM \
  --start-time "2025-03-22T09:00:00Z" \
  --frequency Day \
  --interval 1
```

Link o agendamento ao runbook:

⚠️ **Importante:** Atualmente a Azure CLI **não possui** um comando nativo para vincular diretamente um runbook a um agendamento. Esse vínculo deve ser feito manualmente pelo **Portal do Azure**.

### Alternativa via Portal:

1. Acesse a conta de automação no [Portal do Azure](https://portal.azure.com)
2. Clique em **Runbooks** > selecione o runbook **IniciarVMRunbook**
3. Vá em **Agendamentos (Schedules)** > clique em **Adicionar um agendamento existente**
4. Selecione o agendamento **AgendarVM** criado anteriormente
5. Clique em **OK** para salvar

### Limpar o ambiente

```bash
az group delete --name MeuGrupoAutomation --yes --no-wait
```