---
title: Obter informações de serviço do armazenamento de configurações | Microsoft Docs
description: Saiba como usar o armazenamento de configurações para encontrar todos os serviços disponíveis ou determinar se um serviço específico está instalado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: cb014803945ea88cd6c2c27eee8c120059014a18
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900636"
---
# <a name="get-service-information-from-the-settings-store"></a>Obter informações de serviço do armazenamento de configurações
Você pode usar o armazenamento de configurações para encontrar todos os serviços disponíveis ou determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.

## <a name="to-list-the-available-services"></a>Para listar os serviços disponíveis

1. Crie um projeto VSIX chamado `FindServicesExtension` e adicione um comando personalizado chamado `FindServicesCommand` . Para obter mais informações sobre como criar um comando personalizado, consulte [Criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

2. Em *FindServicesCommand.cs,* adicione as seguintes diretivas using:

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. Obter o armazenamento de definições de configuração e, em seguida, encontrar a subcoleção chamada Serviços. Essa coleção inclui todos os serviços disponíveis. No método `MenuItemCommand` , remova o código existente e substitua-o pelo seguinte:

    ```csharp
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

4. Compile o projeto e comece a depuração. A instância experimental é exibida.

5. Na instância experimental, no menu **Ferramentas,** clique em **Invocar FindServicesCommand**.

     Você deverá ver uma caixa de mensagem listando todos os serviços.

     Para verificar essas configurações, você pode usar o editor do Registro.

## <a name="find-a-specific-service"></a>Encontrar um serviço específico
 Você também pode usar o <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> método para determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.

1. No MenuItemCallback do projeto que você criou no procedimento anterior, pesquise o armazenamento de definições de configuração para a coleção que tem a subcoleção nomeada pelo GUID do `Services` serviço. Nesse caso, procuraremos o serviço de Ajuda.

    ```csharp
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

2. Compile o projeto e comece a depuração.

3. Na instância experimental, no menu **Ferramentas,** clique em **Invocar FindServicesCommand**.

     Você deverá ver uma mensagem com o texto **Serviço de Ajuda Disponível: seguido** por **True** ou **False.** Para verificar essa configuração, você pode usar um editor do Registro, conforme mostrado nas etapas anteriores.
