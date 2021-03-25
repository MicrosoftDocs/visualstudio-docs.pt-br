---
title: Gravando no repositório de configurações do usuário | Microsoft Docs
description: Saiba como adicionar o bloco de notas ao Visual Studio como uma ferramenta externa lendo e gravando no armazenamento de configurações do usuário usando este passo a passos.
ms.custom: SEO-VS-2020
ms.date: 05/23/2019
ms.topic: how-to
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8ff3fa6f061f894abce17d2e6c58bfb791740a90
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061765"
---
# <a name="writing-to-the-user-settings-store"></a>Gravando no repositório de configurações do usuário
As configurações de usuário são configurações graváveis, como aquelas na caixa de diálogo **ferramentas/opções** , janelas de propriedades e algumas outras caixas de diálogo. As extensões do Visual Studio podem usá-las para armazenar pequenas quantidades de dados. Este tutorial mostra como adicionar o bloco de notas ao Visual Studio como uma ferramenta externa, lendo e gravando no repositório de configurações do usuário.

## <a name="writing-to-the-user-settings-store"></a>Gravando no repositório de configurações do usuário

1. Crie um projeto VSIX chamado UserSettingsStoreExtension e, em seguida, adicione um comando personalizado chamado UserSettingsStoreCommand. Para obter mais informações sobre como criar um comando personalizado, consulte [criando uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

2. No UserSettingsStoreCommand. cs, adicione as seguintes diretivas using:

    ```csharp
    using System.Collections.Generic;
    using Microsoft.VisualStudio.Settings;
    using Microsoft.VisualStudio.Shell.Settings;
    ```

3. No MenuItemCallback, exclua o corpo do método e obtenha o armazenamento de configurações do usuário, da seguinte maneira:

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);
    }
    ```

4. Agora descubra se o bloco de notas já está definido como uma ferramenta externa. Você precisa iterar em todas as ferramentas externas para determinar se a configuração ToolCmd é "notepad", da seguinte maneira:

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already an External Tool.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }
    }

    ```

5. Se o bloco de notas não tiver sido definido como uma ferramenta externa, defina-o da seguinte maneira:

    ```vb
    private void MenuItemCallback(object sender, EventArgs e)
    {
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);

        // Find out whether Notepad is already installed.
        int toolCount = userSettingsStore.GetInt32("External Tools", "ToolNumKeys");
        bool hasNotepad = false;
        CompareInfo Compare = CultureInfo.InvariantCulture.CompareInfo;
        for (int i = 0; i < toolCount; i++)
        {
            if (Compare.IndexOf(userSettingsStore.GetString("External Tools", "ToolCmd" + i), "Notepad", CompareOptions.IgnoreCase) >= 0)
            {
                hasNotepad = true;
                break;
            }
        }

        string message = (hasNotepad) ? "Notepad already installed" : "Installing Notepad";
         if (!hasNotepad)
        {
            userSettingsStore.SetString("External Tools", "ToolTitle" + toolCount, "&Notepad");
            userSettingsStore.SetString("External Tools", "ToolCmd" + toolCount, "C:\\Windows\\notepad.exe");
            userSettingsStore.SetString("External Tools", "ToolArg" + toolCount, "");
            userSettingsStore.SetString("External Tools", "ToolDir" + toolCount, "$(ProjectDir)");
            userSettingsStore.SetString("External Tools", "ToolSourceKey" + toolCount, "");
            userSettingsStore.SetUInt32("External Tools", "ToolOpt" + toolCount, 0x00000011);

            userSettingsStore.SetInt32("External Tools", "ToolNumKeys", toolCount + 1);
        }
    }
    ```

6. Teste o código. Lembre-se de que ele adiciona o bloco de notas como uma ferramenta externa, portanto, você deve reverter o registro antes de executá-lo uma segunda vez.

7. Compile o código e inicie a depuração.

8. No menu **ferramentas** , clique em **invocar UserSettingsStoreCommand**. Isso adicionará o bloco de notas ao menu **ferramentas** .

9. Agora você deve ver o bloco de notas no menu ferramentas/opções e clicar em **bloco** de notas deve exibir uma instância do bloco de notas.
