# Laboratório Prático: Criando e Gerenciando Pull Requests no Azure DevOps

## Visão Geral

Este laboratório orienta você na criação e gestão de Pull Requests (PRs) no Azure DevOps, facilitando a revisão e a integração de alterações de código no repositório Git.

## Pré-requisitos

- **Conta no Azure DevOps**: Acesse [Azure DevOps](https://dev.azure.com/) e faça login ou crie uma conta.
- **Projeto no Azure DevOps**: Tenha um projeto existente ou crie um novo.
- **Repositório Git**: Utilize um repositório Git dentro do seu projeto no Azure DevOps.

## Passo 1: Criar uma Nova Branch

1. **Navegue até o Repositório**:
   - No seu projeto do Azure DevOps, vá para **Repos** > **Files**.

2. **Criar uma Branch**:
   - Clique em **"New Branch"**.
   - Nomeie a branch, por exemplo, `feature/nova-funcionalidade`.
   - Selecione a branch de origem (por exemplo, `main`).
   - Clique em **"Create"**.

## Passo 2: Fazer Alterações na Nova Branch

1. **Selecione a Nova Branch**:
   - No menu suspenso de branches, escolha `feature/nova-funcionalidade`.

2. **Edite ou Adicione Arquivos**:
   - Selecione o arquivo a ser modificado ou adicione um novo.
   - Faça as alterações necessárias.
   - Adicione uma mensagem de commit descritiva.
   - Clique em **"Commit"**.

## Passo 3: Criar um Pull Request (PR)

1. **Inicie o PR**:
   - Após o commit, clique em **"Create a pull request"** ou vá para **Repos** > **Pull Requests** e clique em **"New Pull Request"**.

2. **Configure o PR**:
   - **Source branch**: `feature/nova-funcionalidade`.
   - **Target branch**: `main`.
   - Adicione um **título** e uma **descrição** detalhados.
   - **Adicione revisores**: Selecione membros da equipe para revisar o PR.
   - **Adicione work items**: Vincule itens de trabalho relacionados, se aplicável.

3. **Crie o PR**:
   - Revise as configurações e clique em **"Create"**.

## Passo 4: Revisão do Pull Request

1. **Notificação aos Revisores**:
   - Os revisores receberão uma notificação para revisar o PR.

2. **Processo de Revisão**:
   - Os revisores podem adicionar comentários, sugerir alterações ou aprovar o PR.
   - O autor do PR deve responder aos comentários e fazer ajustes conforme necessário.

## Passo 5: Completar o Pull Request

1. **Aprovação**:
   - Após a aprovação de todos os revisores e a resolução de todos os comentários, o PR está pronto para ser concluído.

2. **Completar o PR**:
   - Clique em **"Complete"**.
   - Opcionalmente, selecione:
     - **"Delete source branch"**: Exclui a branch `feature/nova-funcionalidade` após a conclusão.
     - **"Squash changes"**: Combina todos os commits em um único commit na branch de destino.
   - Clique em **"Complete merge"**.

3. **Confirmação**:
   - A branch `feature/nova-funcionalidade` é mesclada na `main`.
   - As alterações estão agora integradas ao código principal.

## Conclusão

Você aprendeu a:

- Criar e gerenciar branches no Azure DevOps.
- Fazer alterações e commits em uma branch.
- Configurar e criar um Pull Request.
- Conduzir o processo de revisão e completar o PR.

Para aprofundar seus conhecimentos, consulte a [documentação oficial do Azure DevOps sobre Pull Requests](https://learn.microsoft.com/en-us/azure/devops/repos/git/pull-requests?view=azure-devops).

**Referências Adicionais**:

- [Conceitos de Pull Request - LinkedIn Learning](https://br.linkedin.com/learning/descubra-o-azure-devops/conceitos-de-pull-request)
- [Como criar um Pull Request no Azure DevOps - YouTube](https://www.youtube.com/watch?v=RXQ9jZmKzfE)
