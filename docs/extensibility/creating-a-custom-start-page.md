---
title: Criando uma página inicial personalizada | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: ed35948158866b7d0bbb2e458c8f8bc2f7b3f844
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85903666"
---
# <a name="creating-a-custom-start-page"></a>Criando uma página inicial personalizada

Você pode criar uma página inicial personalizada seguindo as etapas neste documento.

## <a name="create-a-blank-start-page"></a>Criar uma página inicial em branco

Primeiro, crie uma página inicial em branco criando um arquivo *. XAML* que tenha uma estrutura de marca que o Visual Studio reconhecerá. Em seguida, adicione marcação e code-behind para produzir a aparência e a funcionalidade que você deseja.

1. Crie um novo projeto do tipo **aplicativo WPF** (**Visual C#**  >  **Windows Desktop**).

2. Adicione uma referência a `Microsoft.VisualStudio.Shell.14.0` .

3. Abra o arquivo XAML no editor de XML e altere o elemento de nível superior \<Window> para um \<UserControl> elemento sem remover nenhuma das declarações de namespace.

4. Remova a `x:Class` declaração do elemento de nível superior. Isso torna o conteúdo XAML compatível com a janela de ferramentas do Visual Studio que hospeda a página inicial.

5. Adicione as seguintes declarações de namespace ao elemento de nível superior \<UserControl> .

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     Esses namespaces permitem que você acesse comandos, controles e configurações de interface do usuário do Visual Studio. Para obter mais informações, consulte [adicionar comandos do Visual Studio a uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).

     O exemplo a seguir mostra a marcação no arquivo *. XAML* para uma página inicial em branco. Qualquer conteúdo personalizado deve ir para o <xref:System.Windows.Controls.Grid> elemento interno.

    ```vb
    <UserControl
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:MyNamespace="clr-namespace:ManualStartPage;assembly=ManualStartPage"
        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        xmlns:local="clr-namespace:StartPageHost"
        mc:Ignorable="d"
         Height="350" Width="525">
        <Grid>
        <!--Add content here.-->
        </Grid>
    </UserControl>
    ```

6. Adicione controles ao elemento vazio \<UserControl> para preencher sua página inicial personalizada. Para obter informações sobre como adicionar funcionalidade específica ao Visual Studio, consulte [adicionar comandos do Visual Studio a uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).

## <a name="test-and-apply-the-custom-start-page"></a>Testar e aplicar a página inicial personalizada

Não defina a instância primária do Visual Studio para executar a página inicial personalizada até verificar se ela não falha no Visual Studio. Em vez disso, teste-o na instância experimental.

### <a name="to-test-a-manually-created-custom-start-page"></a>Para testar uma página inicial personalizada criada manualmente

1. Copie o arquivo XAML e todos os arquivos de texto de suporte ou arquivos de marcação para a pasta *%USERPROFILE%\My Documentos\visual Studio 2015 \\ \ StartPages* .

2. Se a página inicial fizer referência a qualquer controle ou tipo em assemblies que não são instalados pelo Visual Studio, copie os assemblies e cole-os na *{pasta de instalação do \\ Visual Studio} \Common7\IDE\PrivateAssemblies*.

3. Em um prompt de comando do Visual Studio, digite **devenv/Rootsuffix exp** para abrir uma instância experimental do Visual Studio.

4. Na instância experimental, vá para a **Tools**  >  página de inicialização do ambiente**Opções**de ferramentas  >  **Environment**  >  **Startup** e selecione o arquivo XAML na lista suspensa **Personalizar página inicial** .

5. No menu **Exibir** , clique em **página inicial**.

     Sua página inicial personalizada deve ser exibida. Se você quiser alterar todos os arquivos, deverá fechar a instância experimental, fazer as alterações, copiar e colar os arquivos alterados e, em seguida, abrir novamente a instância experimental para exibir as alterações.

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Para aplicar a página inicial personalizada na instância primária do Visual Studio

- Depois de testar a página inicial e encontrá-la estável, use a opção **Personalizar página inicial** na caixa de diálogo **Opções** para selecioná-la como a página inicial na instância primária do Visual Studio

## <a name="see-also"></a>Confira também

- [Walkthrough: Adicionar XAML personalizado à página inicial](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [Adicionar controle de usuário à página inicial](../extensibility/adding-user-control-to-the-start-page.md)
- [Adicionar comandos do Visual Studio a uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [Walkthrough: salvar as configurações do usuário em uma página inicial](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [Implantar páginas iniciais personalizadas](../extensibility/deploying-custom-start-pages.md)
