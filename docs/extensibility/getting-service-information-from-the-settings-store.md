---
title: Obtendo informações de serviço do repositório de configurações | Microsoft Docs
description: Saiba como usar o repositório de configurações para localizar todos os serviços disponíveis ou para determinar se um serviço específico está instalado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 7028d440-d16d-4b08-9b94-eb8cc93b25fc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1a39987e13ed3af4bc19c3a80baf0049467daf3a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057644"
---
# <a name="get-service-information-from-the-settings-store"></a>Obter informações de serviço do repositório de configurações
Você pode usar o repositório de configurações para localizar todos os serviços disponíveis ou para determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.

## <a name="to-list-the-available-services"></a>Para listar os serviços disponíveis

1. Crie um projeto VSIX chamado `FindServicesExtension` e, em seguida, adicione um comando personalizado chamado `FindServicesCommand` . Para obter mais informações sobre como criar um comando personalizado, consulte [criar uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

2. No *FindServicesCommand. cs*, adicione as seguintes diretivas using:

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    using System.Windows.Forms;
    ```

3. Obtenha o repositório de definições de configuração e, em seguida, localize a subcoleção denominada serviços. Essa coleção inclui todos os serviços disponíveis. No `MenuItemCommand` método, remova o código existente e substitua-o pelo seguinte:

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

5. Na instância experimental, no menu **ferramentas** , clique em **invocar FindServicesCommand**.

     Você deverá ver uma caixa de mensagem listando todos os serviços.

     Para verificar essas configurações, você pode usar o editor do registro.

## <a name="find-a-specific-service"></a>Localizar um serviço específico
 Você também pode usar o <xref:Microsoft.VisualStudio.Settings.SettingsStore.CollectionExists%2A> método para determinar se um serviço específico está instalado. Você deve saber o tipo da classe de serviço.

1. No MenuItemCallback do projeto que você criou no procedimento anterior, pesquise o repositório de definições de configuração para a `Services` coleção que tem a subcoleção denominada pelo GUID do serviço. Nesse caso, procuraremos o serviço de ajuda.

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

3. Na instância experimental, no menu **ferramentas** , clique em **invocar FindServicesCommand**.

     Você verá uma mensagem com o serviço de **ajuda de texto disponível:**  seguido por **true** ou **false**. Para verificar essa configuração, você pode usar um editor do registro, conforme mostrado nas etapas anteriores.
