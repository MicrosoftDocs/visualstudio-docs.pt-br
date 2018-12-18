---
title: Isolado parâmetros de ponto de entrada do Shell (C++) | Microsoft Docs
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
- Shell [Visual Studio], isolated mode%2C Start entry point
- Visual Studio shell, isolated mode%2C Start entry point
ms.assetid: 18f4b18b-2173-4afa-ba0a-42fe33e61118
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 270a5c932429a518447d0029b05d3c9522db7387
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749160"
---
# <a name="isolated-shell-entry-point-parameters-c"></a>Parâmetros de ponto de entrada do Shell isolado (C++)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando um aplicativo baseado no shell do Visual Studio é iniciado, ele chama o ponto de entrada do início do shell do Visual Studio. As configurações a seguir podem ser substituídas na chamada para o ponto de entrada do início do shell. Para obter uma descrição de cada configuração, consulte [. Arquivos de Pkgdef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md).  
  
- AddinsAllowed  
  
- AllowsDroppedFilesOnMainWindow  
  
- AppName  
  
- CommandLineLogo  
  
- DefaultHomePage  
  
- DefaultProjectsLocation  
  
- DefaultSearchPage  
  
- DefaultUserFilesFolderRoot  
  
- DisableOutputWindow  
  
- HideMiscellaneousFilesByDefault  
  
- HideSolutionConcept  
  
- NewProjDlgInstalledTemplatesHdr  
  
- NewProjDlgSlnTreeNodeTitle  
  
- SolutionFileCreatorIdentifier  
  
- SolutionFileExt  
  
- UserFilesSubFolderName  
  
- UserOptsFileExt  
  
  O Visual Studio Shell isolado modelo cria um arquivo de origem *solutionName*. cpp, onde *solutionName* é o nome da solução para o aplicativo. Esse arquivo define o ponto de entrada principal para o aplicativo, a função _tWinMain. Essa função invocará o ponto de entrada do início do shell.  
  
  Você pode alterar o comportamento do aplicativo ao alterar essas configurações quando o aplicativo é iniciado.  
  
## <a name="parameters"></a>Parâmetros  
 O ponto de entrada do início do shell do Visual Studio define cinco parâmetros. Não altere os primeiros quatro parâmetros. O quinto parâmetro usa uma lista de substituição de configurações. O ponto de entrada do início do shell é chamado de ponto de entrada principal de um aplicativo.  
  
 O ponto de entrada do início do shell tem a seguinte assinatura.  
  
```  
typedef int (__cdecl *STARTFCN)(LPSTR, LPWSTR, int, GUID *, WCHAR *pszSettings);  
```  
  
 Se você não quiser substituir as configurações de aplicativo, deixe o valor das configurações substituem o parâmetro como um ponteiro nulo.  
  
 Para substituir um ou mais configurações, passe uma cadeia de caracteres Unicode que contém as configurações a ser substituído. A cadeia de caracteres é uma lista separada por ponto e vírgula de pares nome-valor. Cada par contém o nome da configuração a ser substituída, seguido por um sinal de igual (=), seguido pelo valor a ser aplicado à configuração.  
  
> [!NOTE]
>  Não inclua espaços em branco nas cadeias de caracteres Unicode.  
  
 Para configurações de Boolianas, as cadeias de caracteres a seguir representam o valor true; todas as outras cadeias de caracteres representam o valor false. Essas cadeias de caracteres diferenciam maiusculas de minúsculas.  
  
-   \+  
  
-   1  
  
-   -1  
  
-   em  
  
-   true  
  
-   sim  
  
## <a name="example"></a>Exemplo  
 Para desabilitar complementos e alterar o local padrão dos projetos para seu aplicativo, você pode definir o último parâmetro para "AddinsAllowed=false;DefaultProjectsLocation=%USERPROFILE%\temp".  
  
## <a name="see-also"></a>Consulte também  
 [Personalizar o Shell isolado](../extensibility/customizing-the-isolated-shell.md)   
 [Arquivos .Pkgdef](../extensibility/modifying-the-isolated-shell-by-using-the-dot-pkgdef-file.md)

