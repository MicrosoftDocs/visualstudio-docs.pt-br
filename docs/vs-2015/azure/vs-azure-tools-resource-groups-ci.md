---
title: Integração contínua nos serviços de DevOps do Azure usando os projetos de grupo de recursos do Azure | Microsoft Docs
description: Descreve como configurar a integração contínua nos serviços de DevOps do Azure usando os projetos de implantação de grupo de recursos do Azure no Visual Studio.
author: mlearned
manager: douge
ms.assetid: b81c172a-be87-4adc-861e-d20b94be9e38
ms.service: azure-resource-manager
ms.topic: article
ms.workload: azure-vs
ms.date: 08/01/2016
ms.author: mlearned
ms.openlocfilehash: b20a43181ad4d36377e61434b880b491543a6c47
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791599"
---
# <a name="continuous-integration-in-azure-devops-services-using-azure-resource-group-deployment-projects"></a>Integração contínua nos serviços de DevOps do Azure usando os projetos de implantação do grupo de recursos do Azure
Para implantar um modelo do Azure, você deve executar tarefas em vários estágios: compilar, testar, copiar para o Azure (também chamado de "Preparo") e implantar o modelo. Há duas maneiras diferentes para implantar modelos em serviços de DevOps do Azure. Ambos os métodos oferecem os mesmos resultados, então escolha aquele que melhor se adapta a seu fluxo de trabalho.

1. Adicione uma etapa única ao seu pipeline de compilação que executa o script do PowerShell que está incluído no projeto de implantação de grupo de recursos do Azure (Deploy-AzureResourceGroup.ps1). O script copia artefatos e, em seguida, implanta o modelo.
2. Adicione que vários serviços do Azure DevOps compilar as etapas, cada uma executando uma tarefa do estágio.

Este artigo demonstra ambas as opções. A primeira opção tem a vantagem de usar o mesmo script usado por desenvolvedores no Visual Studio e fornecer consistência em todo o ciclo de vida. A segunda opção oferece uma alternativa conveniente para o script interno. Ambos os procedimentos supõem que você já tiver um projeto de implantação do Visual Studio check-in em serviços de DevOps do Azure.

## <a name="copy-artifacts-to-azure"></a>Copiar artefatos para o Azure
Independentemente do cenário, se você tiver quaisquer artefatos necessários para a implantação de modelo, você deve atribuir acesso do Azure Resource Manager para eles. Esses artefatos podem incluir arquivos, como:

* Modelos aninhados
* Scripts de configuração e scripts DSC
* Binários do aplicativo

### <a name="nested-templates-and-configuration-scripts"></a>Modelos aninhados e Scripts de configuração
Quando você usa os modelos fornecidos pelo Visual Studio (ou compilados com trechos de código do Visual Studio), o script do PowerShell não apenas prepara os artefatos, ele também parametriza o URI de recursos para diferentes implantações. O script e em seguida, copia os artefatos para um contêiner seguro no Azure, cria um token de SaS do contêiner e, em seguida, passa essas informações para a implantação de modelo. Ver [criar uma implantação de modelo](https://msdn.microsoft.com/library/azure/dn790564.aspx) para saber mais sobre modelos aninhados.  Ao usar tarefas nos serviços de DevOps do Azure, você deve selecionar as tarefas apropriadas para a implantação de modelo e se necessário, passar valores de parâmetro da etapa de preparo para a implantação de modelo.

## <a name="set-up-continuous-deployment-in-azure-pipelines"></a>Configurar implantação contínua em Pipelines do Azure
Para chamar o script do PowerShell em Pipelines do Azure, você precisará atualizar seu pipeline de compilação. Em resumo, as etapas são: 

1. Edite o pipeline de compilação.
2. Configure a autorização do Azure em Pipelines do Azure.
3. Adicione uma etapa de compilação do Azure PowerShell que referencia o script do PowerShell no projeto de implantação de grupo de recursos do Azure.
4. Definir o valor de *- ArtifactsStagingDirectory* parâmetro para trabalhar com um projeto criado em Pipelines do Azure.

### <a name="detailed-walkthrough-for-option-1"></a>Passo a passo detalhado para a opção 1
Os procedimentos a seguir orientam você pelas etapas necessárias para configurar a implantação contínua nos serviços de DevOps do Azure usando uma única tarefa que executa o script do PowerShell em seu projeto. 

1. Edite seu pipeline de compilação de serviços de DevOps do Azure e adicione uma etapa de compilação do Azure PowerShell. Escolha o pipeline de compilação sob o **compilar pipelines** categoria e, em seguida, escolha o **editar** link.
   
   ![Editar o pipeline de build][0]
2. Adicione um novo **Azure PowerShell** etapa no pipeline de compilação de build e, em seguida, escolha o **Adicionar etapa de compilação...** .
   
   ![Adicionar etapa de build][1]
3. Escolha o **tarefa de implantação** categoria, selecione o **do Azure PowerShell** da tarefa e, em seguida, escolha seu **adicionar** botão.
   
   ![Adicionar tarefas][2]
4. Escolha o **Azure PowerShell** etapa de compilação e, em seguida, preencha seus valores.
   
   1. Se você já tiver um ponto de extremidade de serviço do Azure adicionado aos serviços de DevOps do Azure, escolha a assinatura na **assinatura do Azure** caixa de listagem suspensa e, em seguida, pule para a próxima seção. 
      
      Se você não tiver um ponto de extremidade de serviço do Azure nos serviços de DevOps do Azure, você precisará adicioná-lo. Esta subseção o guiará durante o processo. Se sua conta do Azure usa uma conta da Microsoft (como Hotmail), você deve executar as etapas a seguir para obter uma autenticação de entidade de serviço.

   2. Escolha o **gerenciar** link ao lado de **assinatura do Azure** caixa de listagem suspensa.
      
      ![Gerenciar assinaturas do Azure][3]
   3. Escolher **Azure** na **novo ponto de extremidade de serviço** caixa de listagem suspensa.
      
      ![Novo ponto de extremidade de serviço][4]
   4. No **Adicionar assinatura do Azure** caixa de diálogo, selecione o **entidade de serviço** opção.
      
      ![Opção de entidade de serviço][5]
   5. Adicione suas informações de assinatura do Azure para o **Adicionar assinatura do Azure** caixa de diálogo. Você precisa fornecer os seguintes itens:
      
      * Id da assinatura
      * Nome da assinatura
      * Id da entidade de serviço
      * Chave da entidade de serviço
      * Id do locatário
   6. Adicionar um nome de sua escolha para o **assinatura** caixa nome. Esse valor aparece mais adiante na **assinatura do Azure** lista suspensa nos serviços de DevOps do Azure. 

   7. Se você não souber sua ID de assinatura do Azure, você pode usar um dos comandos a seguir para recuperá-la.
      
      Para scripts do PowerShell, use:
      
      `Get-AzureRmSubscription`
      
      CLI do Azure, use:
      
      `azure account show`
   8. Para obter uma ID de entidade de serviço, chave de entidade de serviço e ID de locatário, siga o procedimento em [entidade de serviço usando o portal e de aplicativo do Active Directory crie](/azure/azure-resource-manager/resource-group-create-service-principal-portal) ou [autenticando uma entidade de serviço com o Azure O Gerenciador de recursos](/azure/azure-resource-manager/resource-group-authenticate-service-principal).
   9. Adicione os valores de ID de entidade de serviço, chave de entidade de serviço e ID de locatário para o **Adicionar assinatura do Azure** diálogo caixa e, em seguida, escolha o **Okey** botão.
      
      Agora você tem uma entidade de serviço válida para usar para executar o script do PowerShell do Azure.
5. Edite o pipeline de compilação e escolha o **Azure PowerShell** etapa de compilação. Selecione a assinatura na **assinatura do Azure** caixa de listagem suspensa. (Se a assinatura não aparecer, escolha o **Refresh** botão próximo a **gerenciar** link.) 
   
   ![Configurar a tarefa de build do Azure PowerShell][8]
6. Forneça um caminho para o script do PowerShell Deploy-AzureResourceGroup.ps1. Para fazer isso, escolha o botão de reticências (...) ao lado de **caminho do Script** , navegue até o script Deploy-AzureResourceGroup.ps1 do PowerShell na **Scripts** pasta do seu projeto, selecioná-la e, em seguida, Escolha o **Okey** botão.    
   
   ![Selecione o caminho para script][9]
7. Depois de selecionar o script, atualize o caminho para o script para que ele é executado em stagingdirectory (o mesmo diretório que *ArtifactsLocation* é definido como). Você pode fazer isso adicionando "$(Build.StagingDirectory)/"para o início do caminho do script.
   
    ![Editar caminho para script][10]
8. No **argumentos de Script** , digite os seguintes parâmetros (em uma única linha). Quando você executar o script no Visual Studio, você pode ver como o VS usa os parâmetros na **saída** janela. Você pode usar isso como um ponto de partida para definir os valores de parâmetro na etapa de compilação.
   
   | Parâmetro | Descrição |
   | --- | --- |
   | -ResourceGroupLocation |O valor de localização geográfica em que o grupo de recursos está localizado, como **eastus** ou **'Leste dos Estados Unidos'**. (Adicione aspas se houver um espaço no nome). Ver [regiões do Azure](https://azure.microsoft.com/regions/) para obter mais informações. |
   | -ResourceGroupName |O nome do grupo de recursos usado para essa implantação. |
   | -UploadArtifacts |Esse parâmetro, quando presente, especifica que artefatos que precisam ser carregados no Azure do sistema local. Você só precisará definir essa opção se sua implantação de modelo exigir artefatos adicionais que você deseja testar usando o script do PowerShell (como scripts de configuração ou modelos aninhados). |
   | -StorageAccountName |O nome da conta de armazenamento usada para artefatos de preparação para essa implantação. Esse parâmetro é usado somente se você estiver preparando artefatos para implantação. Se esse parâmetro for fornecido, uma nova conta de armazenamento é criada se o script não tenha criado uma durante a implantação anterior. Se o parâmetro for especificado, a conta de armazenamento já deve existir. |
   | -StorageAccountResourceGroupName |O nome do grupo de recursos associado à conta de armazenamento. Esse parâmetro é necessário apenas se você fornecer um valor para o parâmetro StorageAccountName. |
   | -TemplateFile |O caminho para o arquivo de modelo no projeto de implantação de grupo de recursos do Azure. Para aumentar a flexibilidade, use um caminho para esse parâmetro que é relativo ao local do script do PowerShell em vez de um caminho absoluto. |
   | -TemplateParametersFile |O caminho para o arquivo de parâmetros no projeto de implantação de grupo de recursos do Azure. Para aumentar a flexibilidade, use um caminho para esse parâmetro que é relativo ao local do script do PowerShell em vez de um caminho absoluto. |
   | -ArtifactStagingDirectory |Esse parâmetro permite que o script do PowerShell conheça a pasta de onde os arquivos binários do projeto devem ser copiados. Esse valor substitui o valor padrão usado pelo script do PowerShell. Para usar os serviços de DevOps do Azure, defina o valor como: - ArtifactStagingDirectory stagingdirectory |
   
   Aqui está um exemplo de argumentos de script (linha quebrada para facilitar a leitura):
   
   ```    
   -ResourceGroupName 'MyGroup' -ResourceGroupLocation 'eastus' -TemplateFile '..\templates\azuredeploy.json' 
   -TemplateParametersFile '..\templates\azuredeploy.parameters.json' -UploadArtifacts -StorageAccountName 'mystorageacct' 
   –StorageAccountResourceGroupName 'Default-Storage-EastUS' -ArtifactStagingDirectory '$(Build.StagingDirectory)'    
   ```
   
   Quando tiver terminado, o **argumentos de Script** caixa deve se parecer com a lista a seguir:
   
   ![Argumentos de script][11]
9. Depois de adicionar todos os itens necessários para a etapa de compilação do PowerShell do Azure, escolha o **fila** botão para criar um projeto de compilação. O **Build** tela mostra a saída do script do PowerShell.

### <a name="detailed-walkthrough-for-option-2"></a>Passo a passo detalhado para a opção 2
Os procedimentos a seguir orientam você pelas etapas necessárias para configurar a implantação contínua nos serviços de DevOps do Azure usando as tarefas infernas.

1. Edite seu pipeline de compilação de serviços de DevOps do Azure para adicionar que duas novas etapas de compilação. Escolha o pipeline de compilação sob o **definições de compilação** categoria e, em seguida, escolha o **editar** link.
   
   ![Editar definição de compilação][12]
2. Adicionar novas etapas de compilação ao pipeline de build usando o **Adicionar etapa de compilação...** .
   
   ![Adicionar etapa de build][13]
3. Escolha o **Deploy** categoria de tarefa, selecione a **a cópia de arquivos do Azure** de tarefas e, em seguida, escolha seu **adicionar** botão.
   
   ![Adicionar tarefa de cópia de arquivos do Azure][14]
4. Escolha o **implantação de grupo de recursos do Azure** da tarefa e, em seguida, escolha seu **Add** botão e, em seguida, **fechar** o **catálogo de tarefas**.
   
   ![Adicionar tarefa de implantação do grupo de recursos do Azure][15]
5. Escolha o **do Azure File Copy** de tarefa e preencha seus valores.
   
   Se você já tiver um ponto de extremidade de serviço do Azure adicionado aos serviços de DevOps do Azure, escolha a assinatura na **assinatura do Azure** caixa de listagem suspensa. Se você não tiver uma assinatura, consulte [opção 1](#detailed-walkthrough-for-option-1) para obter instruções sobre como configurar uma nos serviços de DevOps do Azure.
   
   * Origem: insira **stagingdirectory**
   * Tipo de Conexão do Azure – selecione **do Azure Resource Manager**
   * Assinatura do Azure RM: escolha a assinatura para a conta de armazenamento que você deseja usar na **assinatura do Azure** caixa de listagem suspensa. Se a assinatura não aparecer, escolha o **Refresh** botão próximo a **gerenciar** link.
   * Tipo de destino: escolha **BLOBs do Azure**
   * Conta de armazenamento RM - selecione a conta de armazenamento você gostaria de usar para a preparação de artefatos
   * Nome do contêiner – insira o nome do contêiner que você deseja usar para a preparação; ele pode ser qualquer nome de contêiner válido, mas seja dedicado a esse pipeline de compilação
   
   Para obter os valores de saída:
   
   * Insira o contêiner de armazenamento URI - **artifactsLocation**
   * Token SAS do contêiner de armazenamento - insira **artifactsLocationSasToken**
   
   ![Configurar a tarefa de cópia de arquivos do Azure][16]
6. Escolha o **implantação de grupo de recursos do Azure** etapa de compilação e, em seguida, preencha seus valores.
   
   * Tipo de Conexão do Azure – selecione **do Azure Resource Manager**
   * Assinatura do Azure RM: escolha a assinatura para implantação na **assinatura do Azure** caixa de listagem suspensa. Isso geralmente será a mesma assinatura usada na etapa anterior
   * Ação – escolha **criar ou atualizar grupo de recursos**
   * Grupo de recursos - Selecione um grupo de recursos ou insira o nome de um novo grupo de recursos para a implantação
   * Local – selecione o local para o grupo de recursos
   * Modelo – insira o caminho e o nome do modelo a ser implantado acrescentando **stagingdirectory**, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.json)**
   * Parâmetros do modelo – insira o caminho e o nome dos parâmetros a ser usado, acrescentando **stagingdirectory**, por exemplo: **$(Build.StagingDirectory/DSC-CI/azuredeploy.parameters.json)**
   * Substituir parâmetros de modelo – Insira ou copie e cole o código a seguir:
     
     ```    
     -_artifactsLocation $(artifactsLocation) -_artifactsLocationSasToken (ConvertTo-SecureString -String "$(artifactsLocationSasToken)" -AsPlainText -Force)
     ```
     ![Configurar a tarefa de implantação do grupo de recursos do Azure][17]
7. Depois de adicionar todos os itens necessários, salve o pipeline de compilação e escolha **enfileirar nova compilação** na parte superior.

## <a name="next-steps"></a>Próximas etapas
Leia [visão geral do Azure Resource Manager](/azure-resource-manager/resource-group-overview.md) para saber mais sobre o Azure Resource Manager e grupos de recursos do Azure.

[0]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough1.png
[1]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough2.png
[2]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough3.png
[3]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough4.png
[4]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough5.png
[5]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough6.png
[8]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough9.png
[9]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough10.png
[10]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough11b.png
[11]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough12.png
[12]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough13.png
[13]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough14.png
[14]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough15.png
[15]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough16.png
[16]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough17.png
[17]: media/vs-azure-tools-resource-groups-ci-in-vsts/walkthrough18.png
