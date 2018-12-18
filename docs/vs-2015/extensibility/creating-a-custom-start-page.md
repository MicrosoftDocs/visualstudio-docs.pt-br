---
title: Página inicial de criação personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 87f653a6ac745253ae86eb6bf8dfab92169ac4db
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806055"
---
# <a name="creating-a-custom-start-page"></a>Criando uma página inicial personalizada
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você não pode criar uma página inicial personalizada usando o modelo de projeto de página inicial, conforme descrito em [páginas de inicialização](../misc/creating-your-own-start-page.md), você pode criar manualmente um seguindo as etapas neste documento.  
  
## <a name="creating-a-blank-start-page"></a>Criando uma página inicial em branco  
 Primeiro, verifique uma página em branco Iniciar criando um arquivo. XAML que tem uma estrutura de marca que reconhecerá o Visual Studio. Em seguida, adicione a marcação e code-behind para produzir a aparência e funcionalidade desejada.  
  
#### <a name="to-create-a-blank-start-page"></a>Para criar uma página em branco do início  
  
1.  Criar um novo projeto do tipo **aplicativo WPF** (**Visual c# / área de trabalho do Windows**.  
  
2.  Adicione uma referência ao `Microsoft.VisualStudio.Shell.14.0`.  
  
3.  Abra o arquivo XAML no editor de XML e altere o nível superior \<Janela > elemento para um \<UserControl > elemento sem a remoção de qualquer uma das declarações de namespace.  
  
4.  Remover o `x:Class` declaração do elemento de nível superior. Isso torna o conteúdo XAML compatível com a janela de ferramentas do Visual Studio que hospeda a página inicial.  
  
5.  Adicione as seguintes declarações de namespace para o nível superior \<UserControl > elemento.  
  
    ```  
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
    ```  
  
     Esses namespaces permite que você acesse as configurações de interface do usuário, controles e comandos do Visual Studio. Para obter mais informações, consulte [adicionando comandos do Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).  
  
     O exemplo a seguir mostra a marcação no arquivo. XAML para uma página em branco do início. Qualquer conteúdo personalizado deve ficar no interno <xref:System.Windows.Controls.Grid> elemento.  
  
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
  
6.  Adicionar controles ao vazio \<UserControl > elemento para preencher sua página inicial personalizada. Para obter informações sobre como adicionar funcionalidade específica para o Visual Studio, consulte [adicionando comandos do Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md).  
  
## <a name="testing-and-applying-the-custom-start-page"></a>Página iniciam do teste e aplicando personalizado  
 Não defina a instância primária do Visual Studio para executar a página inicial personalizada até que você verificar que ele não falhe Visual Studio. Em vez disso, testá-lo na instância experimental.  
  
#### <a name="to-test-a-manually-created-custom-start-page"></a>Para testar uma página de início personalizados criados manualmente  
  
1.  Copie seu arquivo XAML e quaisquer arquivos de texto de suporte ou marcação arquivos, como o **%USERPROFILE%\My Documents\Visual Studio 2015\StartPages\\**  pasta.  
  
2.  Se sua página inicial faz referência a quaisquer controles ou tipos em assemblies que não estão instalados pelo Visual Studio, copie os assemblies e, em seguida, cole-os nas _pasta de instalação do Visual Studio_**\Common7\IDE\ PrivateAssemblies\\**.  
  
3.  Em um prompt de comando do Visual Studio, digite **devenv /rootsuffix Exp** para abrir uma instância experimental do Visual Studio.  
  
4.  Na instância experimental, vá para o **Ferramentas / opções / ambiente / inicialização** da página e selecione o arquivo XAML da **Personalizar página inicial** lista suspensa.  
  
5.  Sobre o **modo de exibição** menu, clique em **Start Page**.  
  
     Sua página inicial personalizada deve ser exibida. Se você deseja alterar todos os arquivos, você deve fechar a instância experimental, faça as alterações, copie e cole os arquivos alterados e, em seguida, reabra a instância experimental para exibir as alterações.  
  
#### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Para aplicar a personalizar página inicial na instância primária do Visual Studio  
  
-   Depois de testar sua página inicial e determinou que ele seja estável, use o **Personalizar página inicial** opção a **opções** caixa de diálogo, selecioná-la como a página inicial na instância primária do Visual Studio  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Adicionar XAML personalizado à página inicial](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)   
 [Adicionando o controle de usuário para a página inicial](../extensibility/adding-user-control-to-the-start-page.md)   
 [Adicionando comandos do Visual Studio para uma página inicial](../extensibility/adding-visual-studio-commands-to-a-start-page.md)   
 [Passo a passo: Salvando as configurações do usuário em uma página inicial](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)   
 [Implantar páginas iniciais personalizadas](../extensibility/deploying-custom-start-pages.md)

