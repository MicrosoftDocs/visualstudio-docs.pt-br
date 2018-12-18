---
title: Modificar o Shell isolado usando o. Arquivo VSCT | Microsoft Docs
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
- Visual Studio shell, isolated mode%2C .vsct file
ms.assetid: 6d147c2d-10e9-400e-b8ce-5566287b41ba
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0eb5b110386f4a696c228e746223d745df6b18f7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817601"
---
# <a name="modifying-the-isolated-shell-by-using-the-vsct-file"></a>Modificar o Shell isolado usando o. Arquivo VSCT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O projeto de interface do usuário para um projeto de shell isolado do Visual Studio contém um arquivo. VSCT que permite que você especifique quais grupos de aplicativos e os comandos individuais estão disponíveis no aplicativo. A seguir está um trecho de um arquivo. VSCT não modificado.  
  
```  
<!-- <Define name="No_WindowListCommand"/> -->  
<!-- <Define name="No_MoreWindowsCommand"/> -->  
<!-- <Define name="No_PaneNextPaneCommand"/> -->  
<!-- <Define name="No_PanePrevPaneCommand"/> -->  
```  
  
 Por padrão, a maioria dos comandos e grupos de comando são incluídos. Para excluir um comando ou um grupo de comandos, simplesmente remova esse comando ou grupo.  
  
 Por exemplo, para remover o próximo painel e os comandos anteriores do painel, remova os `No_PaneNextPaneCommand` e `No_PanePrevPaneCommand` entradas:  
  
```  
  
<Define name="No_PaneNextPaneCommand"/> <Define name="No_PanePrevPaneCommand"/>  
  
```  
  
 Para uma mais detalhadas exemplo essas personalizações, consulte [instruções passo a passo: Criando um aplicativo básico de Shell isolado](../extensibility/walkthrough-creating-a-basic-isolated-shell-application.md).  
  
## <a name="referenced-files"></a>Arquivos referenciados  
 O arquivo. VSCT de padrão para um aplicativo faz referência a arquivos a seguir. Esses arquivos estão localizados no subdiretório \VisualStudioIntegration\Common\Inc\ do diretório de instalação do SDK do Visual Studio.  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|wbids.h|Identidades de interface do usuário para o pacote Web procurar.|  
|AppIDCmdUsed.vsct|Tabela de comando para elementos de interface de usuário do Visual Studio principais.|  
|EmulatorCmdUsed.vsct|Tabela de comando para elementos de interface do usuário de emulação editor Emacs e Brief.|  
|Vsdebugguids.h|Define os GUIDs dos comandos, página de opções e outros recursos do depurador do Visual Studio.|  
|VsDbgCmdUsed.vsct|Tabela de comando para o depurador.|  
  
 O arquivo de AppIDCmdUsed.vsct inclui elementos de interface de usuário do Visual Studio com base nos símbolos definidos no arquivo. VSCT aplicativo.  
  
 Para obter mais informações, consulte [criar tabela de comando de XML (. VSCT) arquivos](../extensibility/internals/designing-xml-command-table-dot-vsct-files.md) e o [referência de esquema XML do VSCT](../extensibility/vsct-xml-schema-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Shell isolado do Visual Studio](../extensibility/visual-studio-isolated-shell.md)

