---
title: Criar a sua própria página inicial | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Create start page
- custom start page
- customize start page
ms.assetid: a0df5b9c-0932-4e54-86f0-28530ad9d684
caps.latest.revision: 22
manager: douge
ms.openlocfilehash: 005f9597abd1ce688724af9fcb167a626e4cd885
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49815033"
---
# <a name="creating-your-own-start-page"></a>Criando sua própria página inicial
Você pode criar uma página inicial personalizada usando o modelo de projeto de página Iniciar ou criando uma página em branco do início.  
  
 O designer XAML pode não fornecer representações visuais totalmente precisas das páginas personalizadas de iniciar devido a dependências no modelo de aplicativo do Visual Studio.  
  
## <a name="using-the-project-template"></a>Usando o modelo de projeto  
 O modelo de página inicial do projeto cria um projeto de página inicial que é uma cópia completa da página do Visual Studio iniciar. Em seguida, você pode editar a página de início às suas especificações.  
  
#### <a name="to-create-a-custom-start-page-by-using-the-start-page-project-template"></a>Para criar uma página inicial personalizada usando o modelo de projeto de página inicial  
  
1.  Baixe e instale o [modelo de projeto de página de início](http://go.microsoft.com/fwlink/?LinkId=186204) da Galeria do Visual Studio.  
  
    > [!WARNING]
    >  No momento o modelo de projeto do Visual Studio 2010 iniciar página não foi atualizado. Para obter informações sobre como atualizar esse modelo, consulte [como: atualizar um Visual Studio iniciar página personalizada](../misc/how-to-upgrade-a-visual-studio-custom-start-page.md).  
  
2.  Depois de ter instalado o modelo, crie um novo projeto de página de início com ele.  
  
3.  No painel esquerdo da caixa de diálogo Novo projeto, sob **modelos instalados**, expanda o **Other Project Types** nó e, em seguida, clique **extensibilidade**.  
  
4.  No painel central, clique em **página de início personalizada**e, em seguida, nomeie o projeto e clique em **Okey**.  
  
     Visual Studio cria um projeto de página inicial que é uma cópia completa da página do Visual Studio iniciar.  
  
5.  Partir **Gerenciador de soluções**, abra **StartPage**.  
  
6.  Edite StartPage.  
  
     Você pode exibir seu trabalho pressionando F5 para abrir uma instância experimental do Visual Studio com a página de início personalizados instalados.  
  
## <a name="creating-a-blank-start-page"></a>Criando uma página inicial em branco  
 A maneira mais fácil para criar uma página em branco de começar é usar o modelo de projeto de página inicial e, em seguida, remover o conteúdo.  
  
#### <a name="to-create-a-blank-start-page-by-using-the-start-page-project-template"></a>Para criar uma página de início em branco usando o modelo de projeto de página inicial  
  
1. Crie um projeto de página inicial usando o modelo de projeto de página inicial, conforme descrito no procedimento anterior.  
  
2. Abra StartPage.  
  
3. Remova todo o conteúdo da página, deixando apenas os elementos xml externo e a grade de contenção <xref:System.Windows.Controls.Grid> elemento, para que seu arquivo. XAML é semelhante ao exemplo a seguir.  
  
   ```xaml
      <Grid xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
                xmlns:sp="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.StartPage"
                xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.10.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.10.0"
            mc:Ignorable="d" 
                d:DesignHeight="600" d:DesignWidth="800">
       <Grid>
           <!--Add content here.-->
       </Grid>
   </Grid>
   ```
      
4. Remova os arquivos de suporte que você não pretende usar.  
  
    Você deve manter os arquivos. VSIX e. pkgdef para fins de implantação.  
  
   Como alternativa, você pode criar uma página em branco Iniciar criando um arquivo XAML com a estrutura de marca correto seja reconhecida pelo Visual Studio. Em seguida, você pode adicionar a marcação e code-behind para obter a aparência desejada e a funcionalidade. Para obter mais informações, consulte [criando uma página de início personalizado](../extensibility/creating-a-custom-start-page.md).  
  
## <a name="testing-and-applying-the-custom-start-page"></a>Página iniciam do teste e aplicando personalizado  
 Não defina a instância primária para executar a página inicial personalizada até que você verificar que ele não falhe. Quando você testou sua página inicial personalizada, pode aplicá-lo ao seu sistema, repetindo as três últimas etapas deste procedimento na instância primária do Visual Studio.  
  
#### <a name="to-test-a-custom-start-page"></a>Para testar uma página inicial personalizada  
  
1. Pressione F5.  
  
    A instância experimental do Visual Studio é aberto com a nova página inicial instalado, mas não selecionada.  
  
2. Na instância experimental do Visual Studio, sobre o **ferramentas** menu, clique em **opções**.  
  
3. No **opções** caixa de diálogo **ambiente**, selecione **inicialização**. Em seguida, na **Personalizar página inicial** lista, selecione o arquivo. XAML e clique em **Okey**.  
  
4. Sobre o **modo de exibição** menu, clique em **Start Page**.  
  
    O página de início do trabalho é exibido. Feche a instância experimental, copiar novamente todos os arquivos alterados e, em seguida, reabra a instância experimental para ver as novas alterações.  
  
   Você pode compartilhar sua página inicial personalizada, carregando o arquivo. VSIX do seu diretório bin\debug para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web ou para outro site da Web ou intranet compartilhar. Para obter mais informações, consulte [implantação de páginas de inicialização personalizada](../extensibility/deploying-custom-start-pages.md).  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando a página inicial](../ide/customizing-the-start-page-for-visual-studio.md)   
 [Adicionar XAML personalizado à página inicial](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)