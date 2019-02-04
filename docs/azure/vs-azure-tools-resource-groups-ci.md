---
title: Integração contínua no Azure DevOps Services usando projetos do Grupo de Recursos do Azure | Microsoft Docs
description: Descreve como configurar a integração contínua no Azure DevOps Services usando projetos de implantação do Grupo de Recursos do Azure no Visual Studio.
author: mlearned
manager: jillfra
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.topic: conceptual
ms.workload: azure-vs
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: bbe4fc4f59527b73b46d95f70541202f87ffab4e
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55139038"
---
# <a name="continuous-integration-in-azure-devops-services-using-azure-resource-group-deployment-projects"></a>Integração contínua no Azure DevOps Services usando projetos de implantação do Grupo de Recursos do Azure
Para implantar um modelo do Azure, você pode executar tarefas em vários estágios: compilar, testar, copiar para o Azure (também chamado de "preparar") e implantar modelo. Há duas maneiras diferentes de implantar modelos no Azure DevOps Services. Os dois métodos oferecem os mesmos resultados, então escolha aquele que melhor se adapta ao seu fluxo de trabalho.

1. Adicione uma única etapa ao seu pipeline de build que executa o script do PowerShell incluído no projeto de implantação do Grupo de Recursos do Azure (Deploy-AzureResourceGroup.ps1). O script copia artefatos e implanta o modelo.
2. Adicione várias etapas de build do Azure DevOps Services, cada uma executando uma tarefa do estágio.

Este artigo demonstra ambas as opções. A primeira opção tem a vantagem de usar o mesmo script usado pelos desenvolvedores no Visual Studio e fornecer consistência em todo o ciclo de vida. A segunda opção oferece uma alternativa conveniente para o script interno. Ambos os procedimentos supõem que você já tenha um projeto de implantação do Visual Studio no Azure DevOps Services.

## <a name="copy-artifacts-to-azure"></a>Copiar artefatos para o Azure
Independentemente do cenário, se você tiver quaisquer artefatos necessários para a implantação de modelo, será preciso conceder a eles acesso ao Azure Resource Manager. Esses artefatos podem incluir arquivos como:

* Modelos aninhados
* Scripts de configuração e scripts DSC
* Binários do aplicativo

### <a name="nested-templates-and-configuration-scripts"></a>Modelos aninhados e scripts de configuração
Quando você usa os modelos fornecidos pelo Visual Studio (ou compilados com snippets de código do Visual Studio), o script do PowerShell não apenas prepara os artefatos como também parametriza o URI dos recursos para implantações distintas. Em seguida, o script copia os artefatos para um contêiner seguro no Azure, cria um token SaS para esse contêiner e passa essas informações para a implantação de modelo. Confira [Criar uma implantação de modelo](https://msdn.microsoft.com/library/azure/dn790564.aspx) para saber mais sobre modelos aninhados.  Ao usar tarefas no Azure DevOps Services, você deve selecionar as tarefas apropriadas para sua implantação de modelo e, se necessário, passar valores de parâmetro da etapa de preparo para a implantação de modelo.

## <a name="set-up-continuous-deployment-in-azure-pipelines"></a>Configurar a implantação contínua no Azure Pipelines
Para chamar o script do PowerShell no Azure Pipelines, você precisa atualizar seu pipeline de build. Resumindo, as etapas são:

1. Editar o pipeline de build.
2. Configurar a autorização do Azure Pipelines.
3. Adicione uma etapa de compilação do Azure PowerShell que faz referência ao script do PowerShell no projeto de implantação do Grupo de recursos do Azure.
4. Defina o valor do parâmetro *- ArtifactsStagingDirectory* para trabalhar com um projeto compilado no Azure Pipelines.

### <a name="detailed-walkthrough-for-option-1"></a>Passo a passo detalhado da Opção 1
Os procedimentos a seguir percorrer as etapas necessárias para configurar implantação contínua no Azure DevOps Services usando uma única tarefa que executa o script do PowerShell em seu projeto.

1. Edite seu pipeline de build do Azure DevOps Services e adicione uma etapa de build do Azure PowerShell. Escolha o pipeline de build na categoria **Pipelines de build** e escolha o link **Editar**.

   ![Editar o pipeline de build](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png)
2. Adicione uma nova etapa de build do **Azure PowerShell** para o pipeline de build e escolha o botão **Adicionar etapa de compilação…** .

   ![Adicionar etapa de build](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png)
3. Escolha a categoria **Tarefa de implantação**, escolha a tarefa do **Azure PowerShell** e escolha o botão **Adicionar**.

   ![Adicionar tarefas](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png)
4. Escolha a etapa de compilação do **Azure PowerShell** e, em seguida, preencha seus valores.

   1. Se um ponto de extremidade de serviço do Azure já tiver sido adicionado ao Azure DevOps Services, escolha a assinatura na caixa de listagem suspensa **Assinatura do Azure** e vá para a próxima seção.

      Se você não tiver um ponto de extremidade de serviço do Azure no Azure DevOps Services, será necessário adicionar um. Esta subseção o guiará pelo processo. Se sua conta do Azure usa uma conta da Microsoft (como Hotmail), você deve executar as seguintes etapas para obter uma autenticação da Entidade de Serviço.

   2. Escolha o link **Gerenciar** próximo à caixa de listagem suspensa **Assinatura do Azure**.

      ![Gerenciar assinaturas do Azure](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png)
   3. Escolha **Azure** na caixa de listagem suspensa **Novo Ponto de Extremidade de Serviço**.

      ![Novo ponto de extremidade de serviço](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png)
   4. Na caixa de diálogo **Adicionar Assinatura do Azure**, selecione a opção **Entidade de Serviço**.

      ![Opção da entidade de serviço](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png)
   5. Adicione as informações de assinatura do Azure à caixa de diálogo **Adicionar Assinatura do Azure** . Você precisa fornecer os seguintes itens:

      * ID da assinatura
      * Nome da assinatura
      * Id da Entidade de serviço
      * Chave da Entidade de serviço
      * ID do locatário
   6. Adicione um nome de sua escolha à caixa de nome da **Assinatura** . Esse valor será exibido mais tarde na lista suspensa **Assinatura do Azure** no Azure DevOps Services.

   7. Se você não souber sua ID de assinatura do Azure, use um dos comandos a seguir para obtê-la.

      Para scripts do PowerShell, use:

      `Get-AzureRmSubscription`

      Para a CLI do Azure, use:

      `azure account show`
   8. Para obter uma ID da Entidade de Serviço, Chave da Entidade de Serviço e ID do Locatário, siga o procedimento em [Criar aplicativo do Active Directory e entidade de serviço usando o portal](/azure/azure-resource-manager/resource-group-create-service-principal-portal) ou [Autenticar uma entidade de serviço com o Azure Resource Manager](/azure/azure-resource-manager/resource-group-authenticate-service-principal).
   9. Adicione os valores de ID de Entidade de Serviço, Chave de Entidade de Serviço e ID de Locatário à caixa de diálogo **Adicionar Assinatura do Azure** e, em seguida, escolha o botão **OK**.

      Agora você tem uma Entidade de Serviço válida para executar o script do Azure PowerShell.
5. Edite o pipeline de build e escolha a etapa de compilação do **Azure PowerShell**. Selecione a assinatura na caixa de listagem suspensa **Assinatura do Azure**. (Se a assinatura não aparecer, escolha o botão **Atualizar** ao lado do link **Gerenciar**.)

   ![Configurar tarefa de build do Azure PowerShell](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png)
6. Forneça um caminho para o script do PowerShell Deploy-AzureResourceGroup.ps1. Para fazer isso, escolha o botão de reticências (...) ao lado da caixa **Caminho do Script**, navegue até o script Deploy-AzureResourceGroup.ps1 do PowerShell na pasta **Scripts** de seu projeto, selecione-o e escolha o botão **OK**.

   ![Selecionar caminho para script](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png)
7. Depois de selecionar o script, atualize o caminho até ele para que seja executado a partir de Build.StagingDirectory (o mesmo diretório para o qual *ArtifactsLocation* está configurado). Você pode fazer isso adicionando "$(Build.StagingDirectory)/" ao início do caminho do script.

    ![Editar caminho para script](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png)
8. Na caixa **Argumentos do Script** , digite os parâmetros a seguir (em uma única linha). Ao executar o script no Visual Studio, você pode ver como o VS usa os parâmetros na janela **Saída** . Você pode usar isso como um ponto de partida para definir os valores do parâmetro na etapa de compilação.

   | Parâmetro | DESCRIÇÃO |
   | --- | --- |
   | -ResourceGroupLocation |O valor da localização geográfica na qual o grupo de recursos está localizado, por exemplo, **eastus** ou **'Leste dos EUA'**. (Adicione aspas se houver um espaço no nome). Veja [Regiões do Azure](https://azure.microsoft.com/regions/) para saber mais. |
   | -ResourceGroupName |O nome do grupo de recursos usado para essa implantação. |
   | -UploadArtifacts |Esse parâmetro, quando presente, especifica que artefatos do sistema local precisam ser carregados no Azure. Você só precisa definir essa opção se a implantação de seu modelo exigir artefatos adicionais que você deseja testar usando o script do PowerShell (como scripts de configuração ou modelos aninhados). |
   | -StorageAccountName |O nome da conta de armazenamento usada para artefatos de preparação para essa implantação. Esse parâmetro será usado somente se você estiver preparando artefatos para implantação. Se esse parâmetro for fornecido, uma nova conta de armazenamento será criada caso o script não tenha criado uma durante a implantação anterior. Se o parâmetro for especificado, a conta de armazenamento já deverá existir. |
   | -StorageAccountResourceGroupName |O nome do grupo de recursos associado à conta de armazenamento. Esse parâmetro será necessário apenas se você fornecer um valor para o parâmetro StorageAccountName. |
   | -TemplateFile |O caminho para o arquivo de modelo no projeto de implantação do Grupo de recursos do Azure. Para aumentar a flexibilidade, use um caminho para esse parâmetro que seja relativo ao local do script do PowerShell em vez de um caminho absoluto. |
   | -TemplateParametersFile |O caminho para o arquivo de parâmetros no projeto de implantação do Grupo de recursos do Azure. Para aumentar a flexibilidade, use um caminho para esse parâmetro que seja relativo ao local do script do PowerShell em vez de um caminho absoluto. |
   | -ArtifactStagingDirectory |Esse parâmetro permite que o script do PowerShell conheça a pasta de onde os arquivos binários do projeto devem ser copiados. Esse valor substitui o valor padrão usado pelo script do PowerShell. Para usar o Azure DevOps Services, defina o valor como: – ArtifactStagingDirectory $(Build.StagingDirectory) |

   Veja a seguir um exemplo de argumentos de script (linha quebrada para facilitar a leitura):

   ```
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json'
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct'
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'
   ```

   Quando tiver terminado, a caixa **Argumentos de Script** deverá ser semelhante à seguinte lista:

   ![Argumentos de script](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png)
9. Depois de adicionar todos os itens necessários para a etapa de compilação do Azure PowerShell, escolha o botão de compilação **Fila** para compilar o projeto. A tela **Compilação** mostra a saída do script do PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Passo a passo detalhado da Opção 2
Os procedimentos a seguir percorrem as etapas necessárias para configurar a implantação contínua no Azure DevOps Services usando as tarefas infernas.

1. Edite seu pipeline de build do Azure DevOps Services para adicionar duas novas etapas de build. Escolha o pipeline de build na categoria **Definições de build** e escolha o link **Editar**.

   ![Editar definição de compilação](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png)
2. Adicione as novas etapas de build ao pipeline de build usando o botão **Adicionar etapa de build…** .

   ![Adicionar etapa de build](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png)
3. Escolha a categoria de tarefa **Implantar**, escolha a tarefa do **Cópia de Arquivos do Azure** e escolha o botão **Adicionar**.

   ![tarefa Adicionar Cópias de Arquivos do Azure](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png)
4. Escolha a tarefa **Implantação do Grupo de Recursos do Azure**, escolha o botão **Adicionar** e, em seguida, **Fechar** o **Catálogo de Tarefas**.

   ![tarefa Adicionar Implantação do Grupo de Recursos do Azure](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png)
5. Escolha a tarefa **Cópia de Arquivos do Azure** e preencha seus valores.

   Se um ponto de extremidade de serviço do Azure já tiver sido adicionado ao Azure DevOps Services, escolha a assinatura na caixa de listagem suspensa **Assinatura do Azure**. Se você não tiver uma assinatura, veja a [Opção 1](#detailed-walkthrough-for-option-1) para obter instruções de como configurar uma no Azure DevOps Services.

   * Origem: insira **$(Build.StagingDirectory)**
   * Tipo de Conexão do Azure: escolha **Azure Resource Manager**
   * Assinatura do RM do Azure: selecione a assinatura para a conta de armazenamento que você quer usar na caixa de listagem suspensa **Assinatura do Azure**. Se a assinatura não aparecer, escolha o botão **Atualizar** ao lado do link **Gerenciar**.
   * Tipo de Destino: escolha **Blob do Azure**
   * Conta de Armazenamento do RM: escolha a conta de armazenamento que você quer usar para a preparação de artefatos
   * Nome do Contêiner – insira o nome do contêiner que deseja usar de preparo. Pode ser qualquer nome de contêiner válido, mas que seja dedicado a esse pipeline de build

   Para obter os valores de saída:

   * URI do Contêiner de Armazenamento: insira **artifactsLocation**
   * Token SAS do Contêiner de Armazenamento: insira **artifactsLocationSasToken**

   ![tarefa Configurar Cópias de Arquivos do Azure](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png)
6. Escolha a etapa de build **Implantação do Grupo de Recursos do Azure** e preencha seus valores.

   * Tipo de Conexão do Azure: escolha **Azure Resource Manager**
   * Assinatura do RM do Azure – selecione a assinatura para implantação na caixa de listagem suspensa **Assinatura do Azure**. Normalmente, será a mesma assinatura usada na etapa anterior
   * Ação – escolha **Criar ou Atualizar Grupo de Recursos**
   * Grupo de Recursos – escolha um grupo de recursos ou insira o nome de um novo grupo de recursos para a implantação
   * Local – escolha o local para o grupo de recursos
   * Modelo – insira o caminho e o nome do modelo a ser implantado acrescentando **$(Build.StagingDirectory)** no início, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parâmetros do Modelo – insira o caminho e o nome dos parâmetros a serem usado acrescentando **$(Build.StagingDirectory)** no início, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Substitua Parâmetros do Modelo: insira ou copie e cole o seguinte código:

     ```
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Tarefa Configurar Implantação do Grupo de Recursos do Azure](media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png)
7. Após adição de todos os itens necessários, salve o pipeline de build e escolha **Enfileirar novo build** na parte superior.

## <a name="next-steps"></a>Próximas etapas

Leia [Visão geral do Gerenciador de Recursos do Azure](/azure/azure-resource-manager/resource-group-overview) para saber mais sobre o Gerenciador de Recursos do Azure e os grupos de recursos do Azure.
