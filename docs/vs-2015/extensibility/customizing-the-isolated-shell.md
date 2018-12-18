---
title: Personalizar o Shell isolado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio shell, isolated mode
ms.assetid: e0b7c3ae-210f-4f48-ac49-6a59e6034f5f
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 097186ba43202c537bf8acbe0b47893151055c19
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733780"
---
# <a name="customizing-the-isolated-shell"></a>Personalizar o Shell isolado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode personalizar seu aplicativo de shell isolado do Visual Studio, alterando os diferentes aspectos da interface do usuário do Visual Studio e restringindo os comandos e os recursos incluídos em seu aplicativo especializado.  
  
## <a name="using-the-applicationpkgdef-file"></a>Usando o arquivo Application.pkgdef  
 A solução de modelo de shell isolado inclui um *SolutionName*. Arquivo Application.pkgdef que permite que você modifique os seguintes recursos:  
  
##### <a name="the-application-title"></a>O título do aplicativo  
 Você pode personalizar o título do aplicativo, que é o nome que é exibido na barra de título do aplicativo, alterando o valor da linha "AppName" a *SolutionName*. Arquivo Application.pkgdef. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
 Se você não quiser que o título do aplicativo para exibir o projeto que está carregado no momento, altere o valor da linha "ShowHierarchyRootInTitle" no *SolutionName*. Arquivo de Application.pkgdef de DWORD: 00000001 para DWORD: 00000000.  
  
##### <a name="the-application-icon"></a>O ícone do aplicativo  
 Você pode personalizar o ícone do aplicativo, que é o ícone que é exibido pelo nome do aplicativo na barra de título do aplicativo. Copie um ícone diferente para o diretório de ícone. Na **Gerenciador de soluções**, adicionar o ícone para a pasta de arquivos de recurso. Em seguida, abra o arquivo VSShellStub.rc e substitua o valor de IDI_STUBPROGRAM com o nome do novo ícone. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
##### <a name="the-command-line-logo"></a>O logotipo de linha de comando  
 Você pode personalizar o logotipo de linha de comando, que é o texto que aparece quando o aplicativo é iniciado na linha de comando, alterando o valor da linha "CommandLineLogo" a *SolutionName*. Arquivo Application.pkgdef. Para obter mais detalhes, consulte [passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="the-name-of-the-user-files-subfolder"></a>O nome da subpasta de arquivos do usuário  
 Você pode alterar o nome da pasta do seu aplicativo mantém para arquivos do usuário, alterando o valor da linha "UserFilesSubFolderName" na *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-title-of-the-solution-tree-node-in-the-new-project-dialog"></a>O título do nó de árvore da solução na caixa de diálogo Novo projeto  
 Você pode personalizar o título do nó da solução na caixa de diálogo Novo projeto, alterando o valor da linha "NewProjDlgSlnTreeNodeTitle" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-installed-templates-header-in-the-new-project-dialog"></a>O cabeçalho de modelos instalados na caixa de diálogo Novo projeto  
 Você pode alterar o cabeçalho de modelos instalados na caixa de diálogo Novo projeto, alterando o valor da linha "NewProjDlgInstalledTemplatesHdr" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="whether-or-not-to-hide-miscellaneous-files-by-default"></a>Se deseja ou não ocultar arquivos diversos por padrão  
 Você pode especificar se deseja ou não ocultar arquivos diversos por padrão, alterando o valor da linha "HideMiscellaneousFilesByDefault" a *SolutionName*. Arquivo Application.pkgdef. Para ocultar arquivos diversos, defina o valor `dword:00000001`e para mostrar os arquivos, defina o valor `dword:00000000`.  
  
##### <a name="whether-or-not-to-disable-the-output-window"></a>Se deseja ou não desabilitar a janela de saída  
 Você pode especificar se deseja ou não desabilitar a janela de saída em seu aplicativo, alterando o valor da linha "DisableOutputWindow" a *SolutionName*. Arquivo Application.pkgdef. Para desabilitar a janela de saída, defina o valor `dword:00000001`e para mostrar a janela de saída, defina o valor `dword:00000000`.  
  
##### <a name="whether-or-not-to-allow-dropped-files-on-the-main-window"></a>Se deseja ou não permitir que arquivos ignorados na janela principal  
 Você pode especificar se deseja ou não permitir que arquivos ignorados na janela principal em seu aplicativo, alterando o valor da linha "AllowsDroppedFilesOnMainWindow" a *SolutionName*. Arquivo Application.pkgdef. Para permitir que arquivos ignorados, defina o valor `dword:00000001`e para impedir que arquivos ignorados, defina o valor `dword:00000000`.  
  
##### <a name="the-default-search-page"></a>A página de pesquisa padrão  
 Você pode personalizar a página do navegador da web, que é exibido quando a janela do navegador da web é aberta, alterando o valor da linha "DefaultSearchPage" na página de *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-default-home-page"></a>A home page padrão  
 Você pode personalizar a home page, alterando o valor da linha "DefaultHomePage" a *SolutionName*. Arquivo Application.pkgdef. Para obter mais detalhes, consulte [passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md)  
  
##### <a name="whether-or-not-to-hide-the-solution-concept"></a>Se deseja ou não ocultam o conceito de solução  
 Você pode especificar se deseja ou não ocultar a solução em seu aplicativo, alterando o valor da linha "HideSolutionConcept" a *SolutionName*. Arquivo Application.pkgdef. Para ocultar a solução, defina o valor `dword:00000001`e para mostrar a solução, defina o valor `dword:00000000`.  
  
##### <a name="the-default-debug-engine"></a>O mecanismo de depuração padrão  
 Você pode alterar o mecanismo de depuração de seu aplicativo usa alterando o valor da linha "DefaultDebugEngine" no *SolutionName*. Arquivo Application.pkgdef para o GUID do seu mecanismo de depuração.  
  
##### <a name="the-file-extension-of-the-user-options-file"></a>A extensão de arquivo do arquivo de opções do usuário  
 Você pode alterar o nome da pasta do seu aplicativo mantém para arquivos do usuário, alterando o valor da linha "UserOptsFileExt" na *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-solution-file-extension"></a>A extensão de arquivo de solução  
 Você pode alterar a extensão usada para os arquivos de solução, alterando o valor da linha "SolutionFileExt" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-default-user-files-folder-root"></a>A pasta raiz de arquivos de usuário padrão  
 Você pode alterar o nome da pasta raiz dos arquivos de usuário para seu aplicativo, alterando o valor da linha "UserFilesSubFolderName" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-solution-file-creator-identifier"></a>O identificador de criador do arquivo de solução  
 Você pode alterar o identificador usado para arquivos de solução, alterando o valor da linha "SolutionFileCreatorIdentifier" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-default-projects-location"></a>O local padrão dos projetos  
 Você pode alterar o nome do local padrão de projetos, alterando o valor da linha "DefaultProjectsLocation" a *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="the-application-localization-package"></a>O pacote de localização do aplicativo  
 Você pode alterar o pacote de localização usado para o seu aplicativo, alterando o valor da linha "AppLocalizationPackage" no *SolutionName*. Arquivo Application.pkgdef.  
  
##### <a name="whether-or-not-to-show-the-hierarchy-root-in-the-title"></a>Se deseja ou não mostrar a raiz da hierarquia no título  
 Você pode especificar se deseja ou não mostrar a raiz da hierarquia na barra de título em seu aplicativo, alterando o valor da linha "ShowHierarchyRootInTitle" a *SolutionName*. Arquivo Application.pkgdef. Para mostrar a raiz da hierarquia, defina o valor `dword:00000001`e para ocultar a raiz da hierarquia, defina o valor `dword:00000000`.  
  
##### <a name="specifying-a-start-page"></a>Especificar uma página inicial  
 Para especificar uma página inicial para seu aplicativo personalizado, na *SolutionName*. Arquivo Application.pkgdef, defina o valor de "DisableStartPage" para `dword:00000000`e, em `[$RootKey$\StartPage\Default]` defina o URI para o local do arquivo. XAML:  
  
```  
DisableStartPage=dword:00000000  
[$RootKey$\StartPage\Default]  
"Uri"="$RootFolder$\<name of XAML file>"  
```  
  
 No arquivo Applicationcommands.vsct na *SolutionName*da interface do usuário do projeto, comente a entrada "No_ShellPkg_startPageCommand":  
  
```  
<!--<Define name="No_ShellPkg_StartPageCommand"/>-->  
```  
  
 Você deve adicionar o arquivo. XAML e quaisquer arquivos de gráficos que você precisa de, o *SolutionName* projeto. Esses arquivos, na verdade, devem ser copiados para o *SolutionName* diretório do projeto, não são adicionado de algum outro diretório.  
  
 Em todos os arquivos, defina a **tipo de Item** propriedade a ser **arquivos de Shell isolado** para que os arquivos a serem copiados para o *$RootFolder$* directory. (Para definir a **tipo de Item** propriedade, o arquivo com o botão direito e selecione **propriedades**. Essa propriedade é encontrada em **propriedades de configuração**, **geral**.)  
  
 Para obter mais informações sobre como personalizar as páginas iniciais, consulte [Personalizando a página inicial](../ide/customizing-the-start-page-for-visual-studio.md).  
  
## <a name="using-other-elements-of-the-isolated-shell"></a>Usando outros elementos do shell isolado  
 Você pode usar outros arquivos e projetos que estão incluídos no modelo de solução de shell isolado para personalizar ainda mais seu aplicativo.  
  
##### <a name="enabledisable-visual-studio-packages"></a>Habilitar/desabilitar pacotes do Visual Studio  
 O *SolutionName*arquivo. pkgundef permite que você desabilite determinados tipos de funcionalidade do Visual Studio, excluindo certos pacotes. Por exemplo, a seguinte linha:  
  
```  
[$RootKey$\Projects\{A2FE74E1-B743-11d0-AE1A-00A0C90FFFC3}\AddItemTemplates\TemplateDirs\{39c9c826-8ef8-4079-8c95-428f5b1c323f}]  
```  
  
 Remove o projeto arquivos diversos do conjunto de modelos de projeto exibido na **novo projeto** caixa de diálogo. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
##### <a name="enabledisable-menu-commands"></a>Habilitar/desabilitar comandos de menu  
 O *SolutionName*UI.vsct arquivo inclui uma lista de comentada de todos os comandos de menu disponíveis para o shell isolado. Para desabilitar um determinado comando, remova a linha correspondente. Por exemplo, para desabilitar o comentário/divisão da janela, descomente o `<Define name="No_SplitCommand"/>` linha. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
##### <a name="the-bitmap-used-on-the-splash-screen"></a>O bitmap usado na tela inicial  
 Você pode personalizar o bitmap usado na tela inicial, que é a janela que é exibida quando o aplicativo é iniciado, alterando o valor da linha "SplashScreenBitmap" a *SolutionName*. Arquivo Application.pkgdef. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
##### <a name="the-helpabout-window"></a>A Ajuda/sobre a janela  
 No modelo de shell isolado, há um projeto separado, você pode usar para personalizar a Ajuda/sobre a caixa para seu aplicativo. Para obter mais detalhes, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).

