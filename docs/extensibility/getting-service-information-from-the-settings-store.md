---
title: Obtendo informações do serviço de Store de configurações | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 947eb0fd25e57e00f355afac8dc993071859189c
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39500482"
---
# <a name="get-service-information-from-the-settings-store"></a>Obter informações de serviço do armazenamento de configurações
Você pode usar o repositório de configurações para encontrar todos os serviços disponíveis ou para determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.  
  
## <a name="to-list-the-available-services"></a>Para listar os serviços disponíveis  
  
1.  Crie um projeto do VSIX chamado `FindServicesExtension` e, em seguida, adicione um comando personalizado chamado `FindServicesCommand`. Para obter mais informações sobre como criar um comando personalizado, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
2.  Na *FindServicesCommand.cs*, adicione as seguintes instruções using:  
  
    ```vb  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    using System.Windows.Forms;  
    ```  
  
3.  Obter o repositório de configurações de configuração, em seguida, localizar a subcoleção serviços nomeada. Esta coleção inclui todos os serviços disponíveis. No `MenuItemCommand` método, remova o código existente e substitua-o pelo seguinte:  
  
    ```  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);  
        string message = "Available services:\n";  
        IEnumerable<string> collection = configurationSettingsStore.GetSubCollectionNames("Services");  
        int n = 0;  
        foreach (string service in collection)  
        {  
            message += configurationSettingsStore.GetString("Services\\" + service, "Name", "Unknown") + "\n";  
        }  
  
        MessageBox.Show(message);  
    }  
    ```  
  
4.  Compile o projeto e comece a depuração. A instância experimental é exibida.  
  
5.  Na instância experimental, sobre o **ferramentas** menu, clique em **FindServicesCommand invocar**.  
  
     Você deve ver uma caixa de mensagem listando todos os serviços.  
  
     Para verificar essas configurações, você pode usar o editor do registro.  
  
## <a name="find-a-specific-service"></a>Localizar um serviço específico  
 Você também pode usar o <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> método para determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.  
  
1.  A eNom menuitemcallback do projeto que você criou no procedimento anterior, pesquisar o repositório de configurações de configuração para o `Services` coleção que tem a subcoleção chamada pelo GUID do serviço. Nesse caso, vamos para o serviço de Ajuda.  
  
    ```  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);  
        string helpServiceGUID = typeof(SVsHelpService).GUID.ToString("B").ToUpper();  
        bool hasHelpService = configurationSettingsStore.CollectionExists("Services\\" + helpServiceGUID);  
        string message = "Help Service Available: " + hasHelpService;  
  
        MessageBox.Show(message);  
    }  
    ```  
  
2.  Compile o projeto e comece a depuração.  
  
3.  Na instância experimental, sobre o **ferramentas** menu, clique em **FindServicesCommand invocar**.  
  
     Você verá uma mensagem com o texto **ajuda disponível do serviço:** seguido **verdadeiro** ou **False**. Para verificar essa configuração, você pode usar um editor do registro, conforme mostrado nas etapas anteriores.