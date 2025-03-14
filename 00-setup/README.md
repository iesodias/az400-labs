# Validar o Ambiente do Laboratório

Para a realização dos laboratórios, é essencial que seu ambiente esteja configurado corretamente. Esta página guiará você pelo processo de configuração, garantindo que todos os pré-requisitos sejam atendidos.

## Pré-requisitos

Os laboratórios requerem o **Microsoft Edge** ou um **navegador compatível com o Azure DevOps**.

### Configuração das Ferramentas Necessárias

- **Assinatura do Azure**: Se você ainda não possui uma assinatura do Azure, crie uma seguindo as instruções nesta página ou acesse [Azure Free Tier](https://azure.microsoft.com/free).
- **Organização no Azure DevOps**: Se ainda não tem uma organização no Azure DevOps para os laboratórios, crie uma seguindo as instruções [nesta página](https://learn.microsoft.com/pt-br/azure/devops/organizations/accounts/create-organization).
- **Git para Windows**: Faça o download e instale a partir da [página oficial](https://git-scm.com/download/win).
- **Visual Studio Code**: Instale a partir do site oficial [VS Code](https://code.visualstudio.com/).
- **Azure CLI**: Instale o Azure CLI nas máquinas de agente auto-hospedado seguindo as [instruções oficiais](https://learn.microsoft.com/pt-br/cli/azure/install-azure-cli).
- **.NET SDK (versão mais recente)**: Instale o SDK do .NET nas máquinas de agente auto-hospedado.

---

## Criando uma Organização no Azure DevOps (Necessário Apenas uma Vez)

> **Nota**: Comece no passo 3 se você já tiver uma conta Microsoft pessoal e uma assinatura ativa do Azure vinculada a essa conta.

1. Abra uma **janela anônima** no navegador e crie uma nova **Conta Microsoft (MSA)** em [Microsoft Account](https://account.microsoft.com).
2. Com a mesma sessão do navegador, inscreva-se para uma assinatura gratuita do **Azure** em [Azure Free Tier](https://azure.microsoft.com/free).
3. Acesse o [Portal do Azure](https://portal.azure.com) e pesquise por **Azure DevOps** na barra de pesquisa.
4. Clique em **Azure DevOps Organizations**.
5. Clique em **My Azure DevOps Organizations** ou acesse diretamente [Azure DevOps Organizations](https://aex.dev.azure.com).
6. Na página **"Precisamos de mais alguns detalhes"**, clique em **Continuar**.
7. No menu suspenso à esquerda, escolha **Default Directory** em vez de **Microsoft Account**.
8. Se solicitado, forneça seu nome, e-mail e localização e clique em **Continuar**.
9. De volta à [Azure DevOps Organizations](https://aex.dev.azure.com), com **Default Directory** selecionado, clique em **Create New Organization**.
10. Aceite os Termos de Serviço clicando em **Continuar**.
11. Caso solicitado, mantenha o nome padrão da organização do Azure DevOps (ele deve ser único globalmente) e escolha um local de hospedagem próximo a você.
12. Após a criação da organização no **Azure DevOps**, vá para **Organization Settings** (canto inferior esquerdo).
13. Em **Organization Settings**, vá para **Billing**.
14. Clique em **Setup Billing**, selecione sua **Assinatura do Azure** e clique em **Salvar**.
15. Quando a tela exibir o **ID da Assinatura do Azure** vinculado, altere **Paid parallel jobs for MS Hosted CI/CD** de **0 para 1** e clique em **Salvar**.

> **Nota**: Aguarde alguns minutos para que as novas configurações sejam aplicadas antes de usar os recursos de CI/CD.

16. Em **Organization Settings**, vá para **Pipelines > Settings**.
17. Desative as opções:
    - **Disable creation of classic build pipelines**
    - **Disable creation of classic release pipelines**
18. Em **Organization Settings**, vá para **Security > Policies**.
19. Ative a opção **Allow public projects**.

> **Nota**: Alguns laboratórios exigem projetos públicos para uso da versão gratuita.

---

## Criando e Configurando um Projeto no Azure DevOps (Necessário Apenas uma Vez)

> **Nota**: Certifique-se de ter criado sua **Organização no Azure DevOps** antes de prosseguir.

Para seguir todas as instruções do laboratório, você precisará:

- Criar um novo **projeto no Azure DevOps**.
- Criar um **repositório** baseado no **eShopOnWeb**.
- Criar uma **conexão de serviço** com sua **assinatura do Azure**.

### Criar o Projeto

1. Acesse seu navegador e vá até sua **Organização no Azure DevOps**.
2. Selecione **New Project** e utilize as seguintes configurações:
   - **Nome**: `eShopOnWeb`
   - **Visibilidade**: `Privado`
   - **Configurações Avançadas > Controle de Versão**: `Git`
   - **Configurações Avançadas > Processo de Itens de Trabalho**: `Scrum`
3. Clique em **Criar**.

---

### Importar o Repositório eShopOnWeb

1. No navegador, acesse sua **Organização no Azure DevOps**.
2. Abra o projeto **eShopOnWeb** recém-criado.
3. Vá para **Repos > Files**, clique em **Import a Repository** e selecione **Import**.
4. Na janela **Import a Git Repository**, cole a seguinte URL:
5. Clique em **Importar**.

#### Estrutura do Repositório:

- `.ado/` - Contém os pipelines YAML do Azure DevOps.
- `.devcontainer/` - Configuração para desenvolvimento com contêineres (VS Code ou GitHub Codespaces).
- `.azure/` - Contém templates de infraestrutura como código (Bicep e ARM).
- `.github/` - Contém workflows YAML do GitHub Actions.
- `src/` - Contém a aplicação .NET 8 usada nos laboratórios.

6. Vá para **Repos > Branches**.
7. Passe o mouse sobre a branch `main` e clique no **menu de opções** (`...`).
8. Selecione **Set as default branch**.

---

## Criar uma Conexão de Serviço para Acessar Recursos do Azure

1. Acesse o portal [Azure DevOps](https://aex.dev.azure.com).
2. Faça login na **Organização do Azure DevOps**.

> **Nota**: Se for seu primeiro login, pode ser necessário criar um perfil, aceitar os Termos de Serviço e clicar em **Continuar**.

3. No projeto **eShopOnWeb**, vá para **Project Settings** (canto inferior esquerdo).
4. Em **Pipelines**, selecione **Service Connections** e clique em **Create Service Connection**.

5. Na tela **New Service Connection**:
- Selecione **Azure Resource Manager** e clique em **Next**.
- Escolha **App registration (automatic)** como **Identity type**.
- Em **Scope level**, selecione **Workload Identity Federation** e **Subscription**.

> **Nota**: Você também pode configurar manualmente via **App registration (manual)** ou **Managed Identity (manual)** seguindo a [documentação oficial do Azure DevOps](https://learn.microsoft.com/en-us/azure/devops/pipelines/library/service-endpoints).

6. Preencha os campos:
- **Subscription**: Selecione sua **assinatura do Azure**.
- **Resource Group**: Escolha o grupo de recursos onde deseja implantar serviços. *(Se necessário, crie um novo no [Portal do Azure](https://portal.azure.com))*
- **Service Connection Name**: Digite `azure-subs`.

7. **Desmarque** a opção **Grant access permission to all pipelines** e clique em **Salvar**.

> **Importante**: Para ambientes de produção, não é recomendado conceder acesso a todos os pipelines. Isso é usado apenas para simplificar o laboratório.

---

## ✅ Agora Você Está Pronto Para os Laboratórios!

Parabéns! Você concluiu todas as etapas de configuração e está pronto para iniciar os laboratórios. 🚀🎉
