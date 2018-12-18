---
title: Configure as funções para um serviço de nuvem do Azure com o Visual Studio | Microsoft Docs
description: Saiba como instalar e configurar funções para serviços de nuvem do Azure usando o Visual Studio.
author: ghogen
manager: douge
assetId: d397ef87-64e5-401a-aad5-7f83f1022e16
ms.prod: visual-studio-dev14
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/21/2017
ms.author: ghogen
ms.openlocfilehash: ce2259debb55c4792c2998f0e67df69dbc8cb7f9
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001340"
---
# <a name="configure-azure-cloud-service-roles-with-visual-studio"></a>Configurar funções de serviço de nuvem do Azure com o Visual Studio
Um serviço de nuvem do Azure pode ter um ou mais trabalho ou funções da web. Para cada função, você precisa definir como essa função é configurada e também configurar como essa função é executada. Para saber mais sobre as funções nos serviços de nuvem, assista ao vídeo [Introdução aos serviços de nuvem do Azure](https://channel9.msdn.com/Series/Windows-Azure-Cloud-Services-Tutorials/Introduction-to-Windows-Azure-Cloud-Services). 

As informações para seu serviço de nuvem são armazenadas nos seguintes arquivos:

- **Servicedefinition. Csdef** -arquivo de definição de serviço define as configurações de tempo de execução para seu serviço de nuvem, incluindo as funções que são necessárias, pontos de extremidade e tamanho da máquina virtual. Nenhum dos dados armazenados em `ServiceDefinition.csdef` pode ser alterado quando a função está sendo executada.
- **ServiceConfiguration. cscfg** – o arquivo de configuração de serviço define quantas instâncias de uma função são executadas e os valores das configurações definidas para uma função. Os dados armazenados em `ServiceConfiguration.cscfg` podem ser alterados enquanto a função está sendo executada.

Para armazenar valores diferentes para as configurações que controlam como uma função é executada, você pode definir várias configurações de serviço. Você pode usar uma configuração de serviço diferentes para cada ambiente de implantação. Por exemplo, você pode definir sua cadeia de conexão de conta de armazenamento para usar o emulador de armazenamento local do Azure em uma configuração de serviço local e criar outra configuração de serviço para usar o armazenamento do Azure na nuvem.

Quando você cria um serviço de nuvem do Azure no Visual Studio, duas configurações de serviço são automaticamente criadas e adicionadas ao seu projeto do Azure:

- `ServiceConfiguration.Cloud.cscfg`
- `ServiceConfiguration.Local.cscfg`

## <a name="configure-an-azure-cloud-service"></a>Configurar um serviço de nuvem do Azure
Você pode configurar um serviço de nuvem do Azure no Gerenciador de soluções no Visual Studio, conforme mostrado nas etapas a seguir:

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, no menu de contexto, selecione **propriedades**.
   
    ![Menu de contexto do projeto de Gerenciador de soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-project-context-menu.png)

1. Na página de propriedades do projeto, selecione a **desenvolvimento** guia. 

    ![Página de propriedades do projeto - guia de desenvolvimento](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-development-tab.png)

1. No **configuração do serviço** , selecione o nome da configuração do serviço que você deseja editar. (Se você quiser fazer alterações em todas as configurações de serviço para essa função, selecione **todas as configurações de**.)
   
    > [!IMPORTANT]
    > Se você escolher uma configuração de serviço específica, algumas propriedades ficarão desabilitadas porque elas só podem ser definidas para todas as configurações. Para editar essas propriedades, você deve selecionar **todas as configurações de**.
    > 
    > 
   
    ![Lista de configuração de serviço para um serviço de nuvem do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/cloud-service-service-configuration-property.png)

## <a name="change-the-number-of-role-instances"></a>Alterar o número de instâncias de função
Para melhorar o desempenho do serviço de nuvem, você pode alterar o número de instâncias de uma função em execução, com base no número de usuários ou a carga esperada para uma função específica. Uma máquina virtual separada é criada para cada instância de uma função quando o serviço de nuvem é executado no Azure. Isso afeta a cobrança pela implantação desse serviço de nuvem. Para obter mais informações sobre a cobrança, consulte [entenda sua fatura do Microsoft Azure](/azure/billing/billing-understand-your-bill).

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto. Sob o **funções** nó, a função que você deseja atualizar e, no menu de contexto, selecione o botão direito do mouse **propriedades**.

    ![Menu de contexto de função do Azure no Gerenciador de soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione o **configuração** guia.

    ![Guia de configuração](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page.png)

1. No **configuração do serviço** , selecione a configuração do serviço que você deseja atualizar.
   
    ![Lista configuração de serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-select-configuration.png)

1. No **contagem de instâncias** texto, digite o número de instâncias que você deseja iniciar para essa função. Cada instância é executada em uma máquina virtual separada quando você publicar o serviço de nuvem do Azure.

    ![Atualizando a contagem de instâncias](./media/vs-azure-tools-configure-roles-for-cloud-service/role-configuration-properties-page-instance-count.png)

1. No Visual Studio, ferramentas, selecione **salvar**.

## <a name="manage-connection-strings-for-storage-accounts"></a>Gerenciar cadeias de conexão para contas de armazenamento
Você pode adicionar, remover ou modificar cadeias de caracteres de conexão para suas configurações de serviço. Por exemplo, você pode querer uma cadeia de caracteres de conexão local para uma configuração de serviço local que tem um valor de `UseDevelopmentStorage=true`. Você também poderá definir uma configuração de serviço de nuvem que usa uma conta de armazenamento no Azure.

> [!WARNING]
> Quando você insere as informações de chave de conta de armazenamento do Azure para uma cadeia de conexão da conta de armazenamento, essas informações são armazenadas localmente no arquivo de configuração de serviço. No entanto, essas informações no momento não é armazenadas como texto criptografado.
> 
> 

Usando um valor diferente para cada configuração de serviço, você não precisa usar cadeias de conexão diferentes em seu serviço de nuvem ou modificar seu código quando você publica seu serviço de nuvem no Azure. Você pode usar o mesmo nome para a cadeia de caracteres de conexão no seu código e o valor é diferente, com base na configuração de serviço que você selecionar quando criar seu serviço de nuvem ou quando publicá-lo.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto. Sob o **funções** nó, a função que você deseja atualizar e, no menu de contexto, selecione o botão direito do mouse **propriedades**.

    ![Menu de contexto de função do Azure no Gerenciador de soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione o **configurações** guia.

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. No **configuração do serviço** , selecione a configuração do serviço que você deseja atualizar.

    ![Configuração de serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Para adicionar uma cadeia de caracteres de conexão, selecione **Adicionar configuração**.

    ![Adicionar a cadeia de caracteres de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Depois que a nova configuração foi adicionada à lista, atualize a linha na lista com as informações necessárias.

    ![Nova cadeia de caracteres de conexão](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -insira o nome que você deseja usar para a cadeia de conexão.
    - **Tipo de** - marque **cadeia de caracteres de Conexão** na lista suspensa.
    - **Valor** -você pode inserir a cadeia de caracteres de conexão diretamente para o **valor** de célula ou selecione as reticências (...) para funcionar no **criar cadeia de Conexão de armazenamento** caixa de diálogo.  

1. No **criar cadeia de Conexão de armazenamento** caixa de diálogo, selecione uma opção para **conectar-se usando**. Em seguida, siga as instruções para a opção selecionada:

    - **Emulador de armazenamento do Microsoft Azure** -se você selecionar essa opção, as configurações restantes na caixa de diálogo serão desabilitadas como eles se aplicam apenas ao Azure. Selecione **OK**.
    - **Sua assinatura** – se você selecionar essa opção, use a lista suspensa para selecionar e entrar em uma conta da Microsoft, ou adicionar uma conta da Microsoft. Selecione uma conta de armazenamento e a assinatura do Azure. Selecione **OK**.
    - **Credenciais inseridas manualmente** -insira o nome da conta de armazenamento e a chave primária ou secundária. Selecione uma opção para **Conexão** (HTTPS é recomendado na maioria dos cenários). Selecione **OK**.

1. Para excluir uma cadeia de caracteres de conexão, selecione a cadeia de caracteres de conexão e, em seguida, selecione **remover configuração**.

1. No Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-access-a-connection-string"></a>Acessar programaticamente uma cadeia de caracteres de conexão

As etapas a seguir mostram como acessar programaticamente uma cadeia de caracteres de conexão usando C#.

1. Adicione o seguinte usando diretivas para um C# em que você pretende usar a configuração de arquivo:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. O código a seguir ilustra um exemplo de como acessar uma cadeia de caracteres de conexão. Substitua o &lt;ConnectionStringName > espaço reservado com o valor apropriado. 

    ```csharp
    // Setup the connection to Azure Storage
    var storageAccount = CloudStorageAccount.Parse(RoleEnvironment.GetConfigurationSettingValue("<ConnectionStringName>"));
    ```

## <a name="add-custom-settings-to-use-in-your-azure-cloud-service"></a>Adicionar configurações personalizadas para usar em seu serviço de nuvem do Azure
Configurações personalizadas no arquivo de configuração de serviço permitem que você adicione um nome e valor para uma cadeia de caracteres para uma configuração de serviço específico. Você pode optar por usar essa configuração para configurar um recurso em seu serviço de nuvem lendo o valor da configuração e usando esse valor para controlar a lógica em seu código. Você pode alterar esses valores de configuração de serviço sem precisar recompilar o pacote de serviço ou quando seu serviço de nuvem está em execução. Seu código pode verificar se há notificações de quando uma configuração é alterada. Ver [RoleEnvironment. Changing Event](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx).

Você pode adicionar, remover ou modificar configurações personalizadas para suas configurações de serviço. Talvez você queira valores diferentes para essas cadeias de caracteres para diferentes configurações de serviço.

Usando um valor diferente para cada configuração de serviço, você não precisa usar cadeias de caracteres diferentes em seu serviço de nuvem ou modificar seu código quando você publica seu serviço de nuvem no Azure. Você pode usar o mesmo nome para a cadeia de caracteres em seu código e o valor é diferente, com base na configuração de serviço que você selecionar quando criar seu serviço de nuvem ou quando publicá-lo.

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto. Sob o **funções** nó, a função que você deseja atualizar e, no menu de contexto, selecione o botão direito do mouse **propriedades**.

    ![Menu de contexto de função do Azure no Gerenciador de soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione o **configurações** guia.

    ![Guia Configurações](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab.png)

1. No **configuração do serviço** , selecione a configuração do serviço que você deseja atualizar.

    ![Lista configuração de serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-select-configuration.png)

1. Para adicionar uma configuração personalizada, selecione **Adicionar configuração**.

    ![Adicionar configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting.png)

1. Depois que a nova configuração foi adicionada à lista, atualize a linha na lista com as informações necessárias.

    ![Nova configuração personalizada](./media/vs-azure-tools-configure-roles-for-cloud-service/project-properties-settings-tab-add-setting-new-setting.png)

    - **Nome** -insira o nome da configuração.
    - **Tipo de** - marque **cadeia de caracteres** na lista suspensa.
    - **Valor** -insira o valor da configuração. Você pode inserir o valor diretamente para o **valor** de célula ou selecione as reticências (...) para inserir o valor na **Editar cadeia de caracteres** caixa de diálogo.  

1. Para excluir uma configuração personalizada, selecione a configuração e, em seguida, selecione **remover configuração**.

1. No Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-access-a-custom-settings-value"></a>Acessar programaticamente o valor de uma configuração personalizada
 
As etapas a seguir mostram como acessar de forma programática usando uma configuração personalizada C#.

1. Adicione o seguinte usando diretivas para um C# em que você pretende usar a configuração de arquivo:

    ```csharp
    using Microsoft.WindowsAzure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.ServiceRuntime;
    ```

1. O código a seguir ilustra um exemplo de como acessar uma configuração personalizada. Substitua o &lt;SettingName > espaço reservado com o valor apropriado. 
    
    ```csharp
    var settingValue = RoleEnvironment.GetConfigurationSettingValue("<SettingName>");
    ```

## <a name="manage-local-storage-for-each-role-instance"></a>Gerenciar o armazenamento local para cada instância de função
Você pode adicionar o armazenamento do sistema de arquivos local para cada instância de uma função. Os dados armazenados nesse armazenamento não é acessível por outras instâncias da função para que os dados são armazenados ou por outras funções.  

1. Crie ou abra um projeto de serviço de nuvem do Azure no Visual Studio.

1. Na **Gerenciador de soluções**, expanda o nó do projeto. Sob o **funções** nó, a função que você deseja atualizar e, no menu de contexto, selecione o botão direito do mouse **propriedades**.

    ![Menu de contexto de função do Azure no Gerenciador de soluções](./media/vs-azure-tools-configure-roles-for-cloud-service/solution-explorer-azure-role-context-menu.png)

1. Selecione o **armazenamento Local** guia.

    ![Guia armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab.png)

1. No **configuração de serviço** lista, verifique **todas as configurações de** está selecionada como as configurações de local de armazenamento se aplicam a todas as configurações de serviço. Qualquer outro valor resulta em todos os campos de entrada na página que está sendo desativado. 

    ![Lista configuração de serviço](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-service-configuration.png)

1. Para adicionar uma entrada de armazenamento local, selecione **adicionar armazenamento Local**.

    ![Adicionar armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-add-local-storage.png)

1. Depois que a nova entrada de armazenamento local foi adicionada à lista, atualize a linha na lista com as informações necessárias.

    ![Nova entrada de armazenamento local](./media/vs-azure-tools-configure-roles-for-cloud-service/role-local-storage-tab-new-local-storage.png)

    - **Nome** -insira o nome que você deseja usar para o novo armazenamento local.
    - **Tamanho (MB)** -insira o tamanho em MB que você precisa para o novo armazenamento local.
    - **Limpar na reciclagem de função** -Selecione esta opção para remover os dados no novo armazenamento local quando a máquina virtual para a função é reciclada.

1. Para excluir uma entrada de armazenamento local, selecione a entrada e, em seguida, selecione **remover armazenamento Local**.

1. No Visual Studio, ferramentas, selecione **salvar**.

## <a name="programmatically-accessing-local-storage"></a>Acessar programaticamente o armazenamento local

Esta seção ilustra como acessar programaticamente o armazenamento local usando C# escrevendo um arquivo de texto de teste `MyLocalStorageTest.txt`.  

### <a name="write-a-text-file-to-local-storage"></a>Gravar um arquivo de texto no armazenamento local

O código a seguir mostra um exemplo de como gravar um arquivo de texto para o armazenamento local. Substitua o &lt;LocalStorageName > espaço reservado com o valor apropriado. 

    ```csharp
    // Retrieve an object that points to the local storage resource
    LocalResource localResource = RoleEnvironment.GetLocalResource("<LocalStorageName>");
    
    //Define the file name and path
    string[] paths = { localResource.RootPath, "MyLocalStorageTest.txt" };
    String filePath = Path.Combine(paths);
    
    using (FileStream writeStream = File.Create(filePath))
    {
        Byte[] textToWrite = new UTF8Encoding(true).GetBytes("Testing Web role storage");
        writeStream.Write(textToWrite, 0, textToWrite.Length);
    }

    ```

### <a name="find-a-file-written-to-local-storage"></a>Localizar um arquivo gravado no armazenamento local

Para exibir o arquivo criado pelo código na seção anterior, siga estas etapas:
    
1.  Na área de notificação do Windows, clique com botão direito no ícone do Azure e, no menu de contexto, selecione **mostrar IU do emulador de computação**. 

    ![Mostrar emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/show-compute-emulator.png)

1. Selecione a função da web.

    ![Emulador de computação do Azure](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator.png)

1. Sobre o **emulador de computação do Microsoft Azure** menu, selecione **ferramentas** > **abrir repositório local**.

    ![Item de menu abrir repositório local](./media/vs-azure-tools-configure-roles-for-cloud-service/compute-emulator-open-local-store-menu.png)

1. Quando a janela do Windows Explorer é aberta, insira ' Mylocalstoragetest ' para o **pesquisa** caixa de texto e selecione **Enter** para iniciar a pesquisa. 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre projetos do Azure no Visual Studio, lendo [Configurando um projeto do Azure](vs-azure-tools-configuring-an-azure-project.md). Saiba mais sobre o esquema do serviço de nuvem lendo [referência de esquema](https://msdn.microsoft.com/library/azure/dd179398).

