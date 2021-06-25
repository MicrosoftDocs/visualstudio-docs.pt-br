---
title: Prioridade do projeto | Microsoft Docs
description: Saiba mais sobre o esquema de prioridade que o Visual Studio IDE usa para determinar o melhor projeto para abrir um item se o item for membro de mais de um projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ac0556e63b25f0f2a0df399cb23d5e2e9473008
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899635"
---
# <a name="project-priority"></a>Prioridade do projeto
Um item de projeto geralmente é membro de apenas um projeto na solução. Portanto, o IDE pode determinar facilmente qual projeto é usado para abrir o item. No entanto, se um item for membro de mais de um projeto, o IDE usará um esquema de prioridade para determinar o melhor projeto para abrir o item.

 A lista a seguir mostra o esquema de prioridade do projeto:

- O IDE chama o método para cada projeto na solução para determinar se <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> o documento é membro desse projeto.

- Se o documento for um membro do projeto, o projeto responderá com uma prioridade que o projeto atribuirá de acordo com sua manipulação desse documento. Por exemplo, um projeto de linguagem responde com uma alta prioridade para seus arquivos de origem de idioma, mas responde com uma prioridade mais baixa para um tipo de arquivo não reconhecedo que não é usado como parte de seu processo de build.

- Projetos que fornecem editores ou designers personalizados específicos do projeto para um documento também recebem uma alta prioridade.

- A <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração fornece os valores de prioridade do documento.

- O projeto que especifica a prioridade mais alta recebe o contexto para abrir o documento. Se dois projetos retornarem valores de prioridade iguais, o projeto ativo será preferencial. Se nenhum projeto na solução responder que ele pode abrir o documento, o IDE colocará o documento no projeto Arquivos Diversos. Para obter mais informações, consulte [Projeto de arquivos diversos.](../../extensibility/internals/miscellaneous-files-project.md)

## <a name="see-also"></a>Confira também
- [Projeto arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md)
- [Como abrir editores para documentos abertos](../../extensibility/how-to-open-editors-for-open-documents.md)
- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
