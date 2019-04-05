---
title: Tratamento de comandos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - command handling
ms.assetid: 78f67d92-77f7-45cb-ad75-6e3346379cc3
caps.latest.revision: 21
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 563f38cd2dc3854918fe637fdc11afe1d1a49b64
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58928439"
---
# <a name="command-handling"></a>Manipulação de comando
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O editor pode definir novos comandos. Normalmente, os comandos são exibidos em um menu, em uma barra de ferramentas ou em um menu de contexto.  
  
 Para obter mais informações sobre como definir os menus e comandos, consulte [comandos, Menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).  
  
 Um serviço de linguagem pode controlar quais menus de contexto são mostrados no editor, interceptando o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> enumeração. Como alternativa, você pode controlar o menu de contexto em uma base por marcador. Para obter mais informações, consulte [comandos importantes para filtros do serviço de linguagem](../extensibility/internals/important-commands-for-language-service-filters.md).  
  
## <a name="adding-commands-to-the-editor-context-menu"></a>Adicionar comandos ao Menu de contexto do Editor  
 Para adicionar um comando ao menu de contexto, você deve primeiro definir um conjunto de comandos de menu que pertencem a um grupo específico. O exemplo a seguir é retirado do arquivo. VSCT gerado como parte do passo a passo [passo a passo: Adicionar recursos a um Editor personalizado](../extensibility/walkthrough-adding-features-to-a-custom-editor.md):  
  
 \<Guid de menu = "guidCustomEditorCmdSet" id = "IDMX_RTF" prioridade = "0x0000" type = "Contexto" >  
  
 \<Parent guid="guidCustomEditorCmdSet" id="0"/>  
  
 \<Cadeias de caracteres >  
  
 \<ButtonText > Menu de contexto CustomEditor\</ButtonText >  
  
 \<CommandName>CustomEditorContextMenu\</CommandName>  
  
 \</Strings>  
  
 \</Menu>  
  
 \</Menus>  
  
 O texto acima adiciona um comando de menu de contexto com o texto **Menu de contexto CustomEditor**. O GUID de Menu é que o do conjunto de comando que é criado com este editor e o tipo é "Contexto".  
  
 Você também pode usar comandos predefinidos que não precisam ser definidos no arquivo. VSCT. Por exemplo, se você examinar o arquivo EditorPane.cs gerado pelo modelo do pacote do Visual Studio, você encontra que um conjunto de comandos predefinidos, como <xref:Microsoft.VisualStudio.VSConstants.VSStd97CmdID> definido pelo <xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>, são tratados em manipuladores de comandos, como o método onSelectAll.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)
