---
title: Usando o repositório de configurações | Microsoft Docs
description: Saiba como ler dados do repositório de definições de configuração, que são configurações somente leitura do Visual Studio e do VSPackage.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Settings Store, using
ms.assetid: 447ec08a-eca5-40b8-89b0-f98fdf3d39a4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4d7fff5bc3eeeb3b4515e2e47027f5b88fb7807d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898377"
---
# <a name="using-the-settings-store"></a>Usar o repositório de configurações
Há dois tipos de armazenamentos de configurações:

- Definições de configuração, que são configurações somente leitura do Visual Studio e do VSPackage. O Visual Studio mescla as configurações de todos os arquivos. pkgdef conhecidos nesse armazenamento.

- Configurações de usuário, que são configurações graváveis, como as que são exibidas em páginas na caixa de diálogo **Opções** , páginas de propriedades e algumas outras caixas de diálogo. As extensões do Visual Studio podem usá-las para armazenamento local de pequenas quantidades de dados.

  Este tutorial mostra como ler dados do repositório de definições de configuração. Consulte [gravando no repositório de configurações do usuário](../extensibility/writing-to-the-user-settings-store.md) para obter uma explicação de como gravar no armazenamento de configurações do usuário.

## <a name="creating-the-example-project"></a>Criando o projeto de exemplo
 Esta seção mostra como criar um projeto de extensão simples com um comando de menu para demonstração.

1. Cada extensão do Visual Studio começa com um projeto de implantação VSIX que conterá os ativos de extensão. Crie um [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] projeto VSIX denominado `SettingsStoreExtension` . Você pode encontrar o modelo de projeto VSIX na caixa de diálogo **novo projeto** em **Visual C#/extensibilidade**.

2. Agora, adicione um modelo de item de comando personalizado chamado **SettingsStoreCommand**. Na caixa de diálogo **Adicionar novo item** , vá para **Visual C#/extensibilidade** e selecione **comando personalizado**. No campo **nome** na parte inferior da janela, altere o nome do arquivo de comando para **SettingsStoreCommand. cs**. Para obter mais informações sobre como criar um comando personalizado, consulte [criando uma extensão com um comando de menu](../extensibility/creating-an-extension-with-a-menu-command.md)

## <a name="using-the-configuration-settings-store"></a>Usando o repositório de definições de configuração
 Esta seção mostra como detectar e exibir definições de configuração.

1. No arquivo SettingsStorageCommand. cs, adicione as seguintes diretivas using:

   ```
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Settings;
   using Microsoft.VisualStudio.Shell.Settings;
   using System.Windows.Forms;
   ```

2. No `MenuItemCallback` , remova o corpo do método e adicione essas linhas para obter o repositório de definições de configuração:

   ```
   SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
   SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
   ```

    O <xref:Microsoft.VisualStudio.Shell.Settings.ShellSettingsManager> é uma classe auxiliar gerenciada sobre o <xref:Microsoft.VisualStudio.Shell.Interop.IVsSettingsManager> serviço.

3. Agora descubra se as ferramentas do Windows Phone estão instaladas. Seu código deve ficar assim:

   ```
   private void MenuItemCallback(object sender, EventArgs e)
   {
       SettingsManager settingsManager = new ShellSettingsManager(ServiceProvider);
       SettingsStore configurationSettingsStore = settingsManager.GetReadOnlySettingsStore(SettingsScope.Configuration);
       bool arePhoneToolsInstalled = configurationSettingsStore.CollectionExists(@"InstalledProducts\Microsoft Windows Phone Developer Tools");
       string message = "Microsoft Windows Phone Developer Tools: " + arePhoneToolsInstalled;
       MessageBox.Show(message);
   }
   ```

4. Testa o código. Compile o projeto e comece a depuração.

5. Na instância experimental, no menu **ferramentas** , clique em **invocar SettingsStoreCommand**.

    Você deverá ver uma caixa de mensagem dizendo que **o Microsoft Windows Phone ferramentas para desenvolvedores:**  seguido por **true** ou **false**.

   O Visual Studio mantém o repositório de configurações no registro do sistema.

#### <a name="to-use-a-registry-editor-to-verify-configuration-settings"></a>Para usar um editor de registro para verificar as definições de configuração

1. Abra Regedit.exe.

2. Navegue até HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0Exp_Config\InstalledProducts\\ .

    > [!NOTE]
    > Verifique se você está olhando a chave que contém \ 14.0Exp_Config \ e não 14.0_Config \\ . Quando você executa a instância experimental do Visual Studio, as definições de configuração estão no hive do registro "14.0Exp_Config".

3. Expanda o nó \Installed Products \. Se a mensagem nas etapas anteriores for **Microsoft Windows Phone ferramentas para desenvolvedores instalada: true**, os produtos \Installed \ deverão conter um nó de ferramentas para desenvolvedores do Microsoft Windows Phone. Se a mensagem for **Microsoft Windows Phone ferramentas para desenvolvedores instalada: false**, \Installed Products \ não deverá conter um nó Microsoft Windows Phone ferramentas para desenvolvedores.
