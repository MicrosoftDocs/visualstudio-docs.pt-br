---
title: Prioridade do projeto | Microsoft Docs
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
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1d052658cc6f61027def4fdae89c2981581b7e27
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51742318"
---
# <a name="project-priority"></a>Prioridade do projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um item de projeto geralmente é um membro de apenas um projeto na solução. Portanto, o IDE pode facilmente determinar qual projeto é usado para abrir o item. No entanto, se um item for um membro de mais de um projeto, o IDE usa um esquema de prioridade para determinar o melhor projeto para abrir o item.  
  
 A lista a seguir mostra o esquema de prioridade do projeto:  
  
-   As chamadas IDE a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> método para cada projeto na solução para determinar se o documento é um membro desse projeto.  
  
-   Se o documento é um membro do projeto, o projeto responde com uma prioridade que o projeto atribui acordo com seu tratamento desse documento. Por exemplo, um projeto de linguagem responde com uma prioridade alta para seus arquivos de origem do idioma, mas responde com uma prioridade mais baixa para um tipo de arquivo não reconhecido que não é usado como parte do processo de compilação.  
  
-   Projetos que oferecem designers ou editores personalizados, específicos do projeto para um documento também recebem uma prioridade alta.  
  
-   O <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração fornece o documento de valores de prioridade.  
  
-   O projeto que especifica a prioridade mais alta é considerando o contexto para abrir o documento. Se dois projetos retornam valores de prioridade igual, o projeto ativo é preferencial. Se nenhum projeto na solução responde que ele pode abrir o documento, o IDE coloca o documento no projeto arquivos diversos. Para obter mais informações, consulte [projeto arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md).  
  
## <a name="see-also"></a>Consulte também  
 [Projeto arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md)   
 [Como: abrir editores para documentos abertos](../../extensibility/how-to-open-editors-for-open-documents.md)   
 [Adicionar modelos projeto e de item de projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)

