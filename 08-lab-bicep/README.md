# Laboratório Prático: Criando uma Infraestrutura com Bicep no Azure

## Visão Geral

Neste laboratório vamos criar uma máquina virtual Ubuntu no Azure usando Bicep que é uma linguagem declarativa para infraestrutura como código

Recursos que serão provisionados:

- **Rede Virtual e Sub-rede**
- **Endereço IP Público**
- **Grupo de Segurança de Rede (NSG)**
- **Interface de Rede (NIC)**
- **Máquina Virtual Ubuntu**

## Pré-requisitos

- **Conta no Azure:** Acesse https://portal.azure.com e faça login ou crie uma conta
- **Azure CLI instalada:** https://learn.microsoft.com/cli/azure/install-azure-cli
- **VS Code com extensão Bicep (opcional)**

## Passo 1: Criar o Grupo de Recursos

```bash
az group create --name MeuGrupoBicep --location eastus
```

Esse comando cria um grupo para organizar todos os recursos do seu ambiente

## Passo 2: Criar o Arquivo Bicep

Crie um arquivo chamado `main.bicep` com o seguinte conteúdo:

```bicep
@description('Nome da máquina virtual.')
param vmName string = 'mac-lab-bicep'

@description('Nome de usuário para a máquina virtual.')
param adminUsername string = 'azureuser'

@description('Senha para o usuário administrador.')
@secure()
param adminPassword string

@description('Localização para todos os recursos.')
param location string = resourceGroup().location

@description('Tamanho da máquina virtual.')
param vmSize string = 'Standard_B1s'

// Rede Virtual
resource virtualNetwork 'Microsoft.Network/virtualNetworks@2023-05-01' = {
  name: '${vmName}-vnet'
  location: location
  properties: {
    addressSpace: {
      addressPrefixes: ['10.0.0.0/16']
    }
    subnets: [
      {
        name: 'default'
        properties: {
          addressPrefix: '10.0.0.0/24'
        }
      }
    ]
  }
}

// Endereço IP Público
resource publicIp 'Microsoft.Network/publicIPAddresses@2023-05-01' = {
  name: '${vmName}-pip'
  location: location
  properties: {
    publicIPAllocationMethod: 'Dynamic'
  }
}

// Grupo de Segurança de Rede
resource networkSecurityGroup 'Microsoft.Network/networkSecurityGroups@2023-05-01' = {
  name: '${vmName}-nsg'
  location: location
  properties: {
    securityRules: [
      {
        name: 'Allow-SSH'
        properties: {
          priority: 1000
          direction: 'Inbound'
          access: 'Allow'
          protocol: 'Tcp'
          sourcePortRange: '*'
          destinationPortRange: '22'
          sourceAddressPrefix: '*'
          destinationAddressPrefix: '*'
        }
      }
    ]
  }
}

// Interface de Rede
resource networkInterface 'Microsoft.Network/networkInterfaces@2023-05-01' = {
  name: '${vmName}-nic'
  location: location
  properties: {
    ipConfigurations: [
      {
        name: 'ipconfig1'
        properties: {
          subnet: {
            id: virtualNetwork.properties.subnets[0].id
          }
          privateIPAllocationMethod: 'Dynamic'
          publicIPAddress: {
            id: publicIp.id
          }
        }
      }
    ]
    networkSecurityGroup: {
      id: networkSecurityGroup.id
    }
  }
}

// Máquina Virtual
resource virtualMachine 'Microsoft.Compute/virtualMachines@2023-03-01' = {
  name: vmName
  location: location
  properties: {
    hardwareProfile: {
      vmSize: vmSize
    }
    storageProfile: {
      imageReference: {
        publisher: 'Canonical'
        offer: '0001-com-ubuntu-server-jammy'
        sku: '22_04-lts-gen2'
        version: 'latest'
      }
    }
    osProfile: {
      computerName: vmName
      adminUsername: adminUsername
      adminPassword: adminPassword
      linuxConfiguration: {
        disablePasswordAuthentication: false
      }
    }
    networkProfile: {
      networkInterfaces: [
        {
          id: networkInterface.id
        }
      ]
    }
  }
}
```

## Passo 3: Fazer o Deploy com Azure CLI

```bash
az deployment group create \
  --resource-group MeuGrupoBicep \
  --template-file main.bicep \
  --parameters adminPassword='A!9f#2Lq@8s&7Gz'
```

Esse comando lê o arquivo Bicep e cria todos os recursos descritos com a senha fornecida

## Passo 4: Obter o IP Público da Máquina Virtual

```bash
az network public-ip show \
  --resource-group MeuGrupoBicep \
  --name mac-lab-bicep-pip \
  --query ipAddress \
  --output tsv
```

O resultado será algo como:

```bash
172.203.153.149
```

## Passo 5: Conectar via SSH na Máquina Virtual

```bash
ssh azureuser@172.203.153.149
```

Quando solicitado digite a senha:

```text
A!9f#2Lq@8s&7Gz
```

## Passo 6: (Opcional) Limpar os Recursos

```bash
az group delete --name MeuGrupoBicep --yes --no-wait
```

Esse comando remove todos os recursos criados no grupo para evitar cobranças

