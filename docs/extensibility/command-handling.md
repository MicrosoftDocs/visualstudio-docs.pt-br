---
title: Tratamento de comandos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - command handling
ms.assetid: 78f67d92-77f7-45cb-ad75-6e3346379cc3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a155927bb69c55c15a06cb058692038c8b309a30
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39230859"
---
# <a name="command-handling"></a>Manipulação de comando
O editor pode definir novos comandos. Normalmente, os comandos são exibidos em um menu, em uma barra de ferramentas ou em um menu de contexto.  
  
 Para obter mais informações sobre como definir os menus e comandos, consulte [comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md).  
  
 Um serviço de linguagem pode controlar quais menus de contexto são mostrados no editor, interceptando o <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> enumeração. Como alternativa, você pode controlar o menu de contexto em uma base por marcador. Para obter mais informações, consulte [comandos importantes para filtros do serviço de linguagem](../extensibility/internals/important-commands-for-language-service-filters.md).  
  
## <a name="add-commands-to-the-editor-context-menu"></a>Adicionar comandos ao menu de contexto do editor  
 Para adicionar um comando ao menu de contexto, você deve primeiro definir um conjunto de comandos de menu que pertencem a um grupo específico. O exemplo a seguir é obtido dos *VSCT* arquivo gerado como parte do passo a passo [passo a passo: adicionar recursos a um editor personalizado](../extensibility/walkthrough-adding-features-to-a-custom-editor.md):  
  
 \<Guid de menu = "guidCustomEditorCmdSet" id = "IDMX_RTF" prioridade = "0x0000" type = "Contexto" >  
  
 \<Guid pai = "guidCustomEditorCmdSet" id = "0" / >  
  
 \<Cadeias de caracteres >  
  
 \<ButtonText > Menu de contexto CustomEditor\</ButtonText >  
  
 \<CommandName > CustomEditorContextMenu\</CommandName >  
  
 \</ Cadeias de caracteres >  
  
 \</ Menu >  
  
 \</ Menus >  
  
 O texto acima adiciona um comando de menu de contexto com o texto **Menu de contexto CustomEditor**. O GUID de Menu é parte do conjunto de comando que é criado com este editor. O tipo é "Contexto".  
  
 Você também pode usar comandos predefinidos que não precisam ser definidos na *VSCT* arquivo. Por exemplo, examine os *EditorPane.cs* arquivo gerado pelo modelo de pacote do Visual Studio. Você verá que um conjunto de comandos predefinidos, como <xref:Microsoft.VisualStudio.VSConstants.VSStd97CmdID> definido por <xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>, são tratados em manipuladores de comandos, como o `onSelectAll` método.  
  
## <a name="see-also"></a>Consulte também  
 [Comandos, menus e barras de ferramentas](../extensibility/internals/commands-menus-and-toolbars.md)