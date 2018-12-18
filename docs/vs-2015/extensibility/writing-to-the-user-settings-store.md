---
title: Gravando o Store de configurações do usuário | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: efd27f00-7fe5-45f8-9b97-371af732be97
caps.latest.revision: 4
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 70522d8a291cad559a042dab7f4eeb3c3c4684ac
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779717"
---
# <a name="writing-to-the-user-settings-store"></a>Gravando no repositório de configurações do usuário
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Configurações de usuário são graváveis como aquelas na **Ferramentas / opções** caixa de diálogo, janelas Propriedades e determinadas outras caixas de diálogo. Extensões do Visual Studio podem usar estes para armazenar pequenas quantidades de dados. Este passo a passo mostra como adicionar o bloco de notas para o Visual Studio como uma ferramenta externa, leitura e gravação para o repositório de configurações do usuário.  
  
### <a name="backing-up-your-user-settings"></a>Fazendo backup de suas configurações de usuário  
  
1.  Você deve ser capaz de redefinir as configurações de ferramentas externas para que você possa depurar e repita o procedimento. Para fazer isso, você deve salvar as configurações originais para que você pode restaurá-los conforme necessário.  
  
2.  Abra Regedit.exe.  
  
3.  Navegue até ferramentas HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp\External\\.  
  
    > [!NOTE]
    >  Certifique-se de que você está vendo a chave que contém \14.0Exp\ e não \14.0\\. Quando você executa a instância experimental do Visual Studio, as configurações de usuário estão no hive do Registro "14.0Exp".  
  
4.  Clique com botão direito na subchave \External Tools\ e, em seguida, clique em **exportar**. Certifique-se de que **ramificação selecionada** está selecionado.  
  
5.  Salve o arquivo externo Tools.reg resultante.  
  
6.  Posteriormente, quando você deseja redefinir as configurações de ferramentas externas, selecione a chave do registro Tools HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp\External \ e clique em **excluir** no menu de contexto.  
  
7.  Quando o **Confirmar exclusão da chave** caixa de diálogo for exibida, clique em **Sim**.  
  
8.  O arquivo Tools.reg externo que você salvou anteriormente com o botão direito, clique em **abrir com**e, em seguida, clique em **Editor do registro**.  
  
## <a name="writing-to-the-user-settings-store"></a>Gravando no repositório de configurações do usuário  
  
1.  Crie um projeto VSIX chamado UserSettingsStoreExtension e, em seguida, adicione um comando personalizado chamado UserSettingsStoreCommand. Para obter mais informações sobre como criar um comando personalizado, consulte [criando uma extensão com um comando de Menu](../extensibility/creating-an-extension-with-a-menu-command.md)  
  
2.  No UserSettingsStoreCommand.cs, adicione as seguintes instruções using:  
  
    ```csharp  
    using System.Collections.Generic;  
    using Microsoft.VisualStudio.Settings;  
    using Microsoft.VisualStudio.Shell.Settings;  
    ```  
  
3.  No MenuItemCallback, exclua o corpo do método e obter o usuário armazenam as configurações, da seguinte maneira:  
  
    ```csharp  
    private void MenuItemCallback(object sender, EventArgs e)  
    {  
        SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);  
        WritableSettingsStore userSettingsStore = settingsManager.GetWritableSettingsStore(SettingsScope.UserSettings);  
    }  
    ```  
  
4.  Agora, descubra se o bloco de notas já está definido como uma ferramenta externa. Você precisa iterar por todas as ferramentas externas para determinar se a configuração ToolCmd é "Notepad", da seguinte maneira:  
  
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
  
5.  Se o bloco de notas não foi definido como uma ferramenta externa, defina-o da seguinte maneira:  
  
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
  
6.  Teste o código. Lembre-se de que ele adiciona o bloco de notas como uma ferramenta externa, portanto, você deve reverter o registro antes de executá-lo uma segunda vez.  
  
7.  Compilar o código e iniciar a depuração.  
  
8.  Sobre o **ferramentas** menu, clique em **UserSettingsStoreCommand invocar**. Isso adicionará o bloco de notas para o **ferramentas** menu.  
  
9. Agora você deve ver o bloco de notas no menu Ferramentas / opções de menu e clicando em **bloco de notas** deve abrir uma instância do bloco de notas.

