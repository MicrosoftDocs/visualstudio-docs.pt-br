---
title: Página inicial de criação personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 30c161478bb04dcf964cb2054e714689c13b6538
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39497632"
---
# <a name="creating-a-custom-start-page"></a>Criando uma página inicial personalizada
Você pode criar uma página inicial personalizada, seguindo as etapas neste documento.  
  
## <a name="create-a-blank-start-page"></a>Criar uma página em branco do início  
 Primeiro, verifique uma página em branco iniciar com a criação de um *. XAML* arquivo que tem uma estrutura de marca que o Visual Studio reconheça. Em seguida, adicione a marcação e code-behind para produzir a aparência e funcionalidade desejada.  
  
### <a name="to-create-a-blank-start-page"></a>Para criar uma página em branco do início  
  
1.  Criar um novo projeto do tipo **aplicativo WPF** (**Visual c#** > **área de trabalho do Windows**).  
  
2.  Adicione uma referência ao `Microsoft.VisualStudio.Shell.14.0`.  
  
3.  Abra o arquivo XAML no editor de XML e altere o nível superior \<Janela > elemento para um \<UserControl > elemento sem a remoção de qualquer uma das declarações de namespace.  
  
4.  Remover o `x:Class` declaração do elemento de nível superior. Isso torna o conteúdo XAML compatível com a janela de ferramentas do Visual Studio que hospeda a página de início.  
  
5.  Adicione as seguintes declarações de namespace para o nível superior \<UserControl > elemento.  
  
    ```vb  
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
    ```  
  
     Esses namespaces permite que você acesse as configurações de interface do usuário, controles e comandos do Visual Studio. Para obter mais informações, consulte [comandos de adicionar o Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).  
  
     O exemplo a seguir mostra a marcação na *. XAML* arquivo para uma página em branco do início. Qualquer conteúdo personalizado deve ficar no interno <xref:System.Windows.Controls.Grid> elemento.  
  
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
  
6.  Adicionar controles ao vazio \<UserControl > elemento para preencher sua página inicial personalizada. Para obter informações sobre como adicionar funcionalidade específica para o Visual Studio, consulte [comandos de adicionar o Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).  
  
## <a name="test-and-apply-the-custom-start-page"></a>Testar e aplicar a página inicial personalizada  
 Não defina a instância primária do Visual Studio para executar a página inicial personalizada até que você verificar que ele não falhe Visual Studio. Em vez disso, testá-lo na instância experimental.  
  
### <a name="to-test-a-manually-created-custom-start-page"></a>Para testar uma criados manualmente página inicial personalizada  
  
1.  Copie seu arquivo XAML e quaisquer arquivos de texto de suporte ou marcação arquivos, como o *%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\*  pasta.  
  
2.  Se sua página inicial faz referência a quaisquer controles ou tipos em assemblies que não estão instalados pelo Visual Studio, copie os assemblies e, em seguida, cole-os nas *{pasta de instalação do Visual Studio} \Common7\IDE\PrivateAssemblies\\* .  
  
3.  Em um prompt de comando do Visual Studio, digite **devenv /rootsuffix Exp** para abrir uma instância experimental do Visual Studio.  
  
4.  Na instância experimental, vá para o **ferramentas** > **opções** > **ambiente** > **deinicialização** página e selecione seu arquivo XAML a partir de **Personalizar página inicial** lista suspensa.  
  
5.  Sobre o **modo de exibição** menu, clique em **Start Page**.  
  
     Sua página inicial personalizada deve ser exibida. Se você deseja alterar todos os arquivos, você deve fechar a instância experimental, faça as alterações, copie e cole os arquivos alterados e, em seguida, reabra a instância experimental para exibir as alterações.  
  
### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Para aplicar a personalizar página inicial na instância primária do Visual Studio  
  
-   Depois de testar sua página inicial e determinou que ele seja estável, use o **Personalizar página inicial** opção a **opções** caixa de diálogo, selecioná-la como a página inicial na instância primária do Visual Studio  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Adicionar XAML personalizado para a página de início](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)   
 [Adicionar controle de usuário para a página de início](../extensibility/adding-user-control-to-the-start-page.md)   
 [Adicionar comandos do Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md)   
 [Passo a passo: Salvar configurações do usuário em uma página inicial](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)   
 [Implantar páginas de inicialização personalizada](../extensibility/deploying-custom-start-pages.md)