---
title: Implementar manipulação de comando para projetos de aninhados | Microsoft Docs
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
- nested projects, implementing command handling
ms.assetid: 48a9d66e-d51c-4376-a95a-15796643a9f2
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 113cc2c061b008892921aac348f3eb56a7bef0d3
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742567"
---
# <a name="implementing-command-handling-for-nested-projects"></a>Implementando a manipulação de comando para projetos aninhados
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O IDE pode passar comandos que são passados para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> e o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> interfaces para projetos aninhados ou projetos pai podem filtrar ou substituir os comandos.  
  
> [!NOTE]
>  Somente os comandos que normalmente é tratados pelo projeto pai podem ser filtrados. Comandos como **construir** e **implantar** que são manipulados pelo IDE não pode ser filtrado.  
  
 As etapas a seguir descrevem o processo para implementar o tratamento do comando.  
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-implement-command-handling"></a>Implementar manipulação de comando  
  
1. Quando o usuário seleciona um projeto aninhado ou um nó em um projeto aninhado:  
  
   1. As chamadas IDE a <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> método.  
  
      – ou —  
  
   2. Se o comando foi originado em uma janela de hierarquia, como um comando de menu de atalho no Gerenciador de soluções, o IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy.QueryStatusCommand%2A> método no pai do projeto.  
  
2. O projeto pai pode examinar os parâmetros a serem passados para `QueryStatus`, como `pguidCmdGroup` e `prgCmds`, para determinar se o projeto pai deve filtrar os comandos. Se o projeto pai é implementado para comandos de filtragem, ela deverá definir:  
  
   ```  
   prgCmds[0].cmdf = OLECMDF_SUPPORTED;  
   // make sure it is disabled  
   prgCmds[0].cmdf &= ~MSOCMDF_ENABLED;  
   ```  
  
    Em seguida, o projeto pai deve retornar `S_OK`.  
  
    Se o projeto pai não filtra o comando, ele deverá apenas retornar `S_OK`. Nesse caso, o IDE roteia automaticamente o comando para o projeto filho.  
  
    O projeto pai não tem que rotear o comando para o projeto filho. O IDE executa essa tarefa...  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>   
 [Comandos, Menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)   
 [Aninhar projetos](../../extensibility/internals/nesting-projects.md)

