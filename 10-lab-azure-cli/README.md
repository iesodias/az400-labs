# Laboratório Prático: Explorando a Azure CLI na VM Criada com Bicep

## Visão Geral

Neste laboratório vamos usar a Azure CLI para interagir com os recursos do Azure diretamente da máquina virtual Ubuntu que criamos anteriormente com Bicep

A Azure CLI é uma ferramenta de linha de comando poderosa para gerenciar recursos do Azure

Vamos executar diversos comandos para explorar o ambiente

## Pré-requisitos

- VM Ubuntu criada via Bicep (como no lab anterior)
- Acesso SSH funcional
- Azure CLI já instalada na VM (se não estiver instale com `curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash`)
- Login com `az login --use-device-code` (ideal para aulas e gravações)

---

## Comandos Azure CLI (seguros para gravação)

### 1. Listar os grupos de recursos existentes (sem detalhes sensíveis)
```bash
az group list --query "[].name" --output table
```

### 2. Verificar se um grupo de recursos existe
```bash
az group exists --name MeuGrupoBicep
```

### 3. Criar um novo grupo de recursos (se necessário)
```bash
az group create --name MeuGrupoTeste --location eastus
```

### 4. Listar as VMs de um grupo
```bash
az vm list --resource-group MeuGrupoBicep --query "[].name" --output table
```

### 5. Obter status da VM
```bash
az vm get-instance-view \
  --name mac-lab-bicep \
  --resource-group MeuGrupoBicep \
  --query "instanceView.statuses[?starts_with(code, 'PowerState/')].displayStatus" \
  --output tsv
```

### 6. Parar a VM
```bash
az vm stop --name mac-lab-bicep --resource-group MeuGrupoBicep
```

### 7. Iniciar a VM
```bash
az vm start --name mac-lab-bicep --resource-group MeuGrupoBicep
```

### 8. Reiniciar a VM
```bash
az vm restart --name mac-lab-bicep --resource-group MeuGrupoBicep
```

### 9. Atualizar o tamanho da VM (exemplo para Standard_B2s)
```bash
az vm resize \
  --resource-group MeuGrupoBicep \
  --name mac-lab-bicep \
  --size Standard_B2s
```

### 10. Listar tamanhos disponíveis para VMs
```bash
az vm list-sizes --location eastus --output table
```

### 11. Listar IPs públicos sem mostrar o IP diretamente
```bash
az network public-ip list \
  --resource-group MeuGrupoBicep \
  --query "[].name" \
  --output table
```

### 12. Listar todas as interfaces de rede do grupo
```bash
az network nic list --resource-group MeuGrupoBicep --query "[].name" --output table
```

### 13. Mostrar os NSGs (Network Security Groups) do grupo
```bash
az network nsg list --resource-group MeuGrupoBicep --query "[].name" --output table
```

### 14. Listar os discos de VMs
```bash
az disk list --resource-group MeuGrupoBicep --query "[].name" --output table
```

### 15. Deletar uma VM (confirmando com --yes)
```bash
az vm delete --name mac-lab-bicep --resource-group MeuGrupoBicep --yes
```

---

## Extra: Instalar a Azure CLI na VM (caso ainda não esteja instalada)

```bash
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

---

Com isso você tem um conjunto prático de comandos para explorar recursos Azure direto da linha de comando

Todos os comandos acima foram selecionados para evitar a exibição de dados sensíveis durante gravações ou demonstrações públicas ✅

