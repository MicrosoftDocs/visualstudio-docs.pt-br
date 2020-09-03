---
title: Prioridade do projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], opening items
ms.assetid: 9f707592-2fb6-4f75-9269-f6d4700a998e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a75c1c333d88e1bf5524281bee8b2a683ca6c98e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706416"
---
# <a name="project-priority"></a>Prioridade do projeto
Um item de projeto geralmente é um membro de apenas um projeto na solução. Portanto, o IDE pode determinar facilmente qual projeto é usado para abrir o item. No entanto, se um item for membro de mais de um projeto, o IDE usará um esquema de prioridade para determinar o melhor projeto para abrir o item.

 A lista a seguir mostra o esquema de prioridade do projeto:

- O IDE chama o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject2.IsDocumentInProject%2A> método para cada projeto na solução para determinar se o documento é membro desse projeto.

- Se o documento for um membro do projeto, o projeto responderá com uma prioridade que o projeto atribui de acordo com seu manuseio desse documento. Por exemplo, um projeto de linguagem responde com uma prioridade alta para seus arquivos de origem de idioma, mas responde com uma prioridade mais baixa para um tipo de arquivo não reconhecido que não é usado como parte de seu processo de compilação.

- Os projetos que fornecem editores ou designers personalizados e específicos do projeto para um documento também recebem uma prioridade alta.

- A <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY> enumeração fornece os valores de prioridade do documento.

- O projeto que especifica a prioridade mais alta recebe o contexto para abrir o documento. Se dois projetos retornarem valores de prioridade iguais, o projeto ativo é preferencial. Se nenhum projeto na solução responder que pode abrir o documento, o IDE colocará o documento no projeto de arquivos diversos. Para obter mais informações, consulte [Miscellaneous Files Project](../../extensibility/internals/miscellaneous-files-project.md).

## <a name="see-also"></a>Confira também
- [Projeto arquivos diversos](../../extensibility/internals/miscellaneous-files-project.md)
- [Como abrir editores para documentos abertos](../../extensibility/how-to-open-editors-for-open-documents.md)
- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
