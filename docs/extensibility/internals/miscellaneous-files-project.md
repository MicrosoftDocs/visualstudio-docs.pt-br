---
title: Projeto de arquivos diversos | Microsoft Docs
description: Saiba mais sobre os dois tipos de editores que podem ser usados para abrir arquivos em um projeto do Visual Studio e a função do projeto para determinar qual editor deve ser usado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- files, adding existing files to solutions
- Miscellaneous Files project
- Solution Items folder
- files, opening with Miscellaneous Files project
ms.assetid: 93a278a8-d4f4-400b-8945-4f1b0a2b5bac
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b79eaaeaf94954e2d3dc1bd855b56bee5b8bdae4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105063273"
---
# <a name="miscellaneous-files-project"></a>Projeto arquivos diversos
Quando um usuário abre itens de projeto, o IDE é atribuído ao projeto de arquivos diversos quaisquer itens que não sejam membros de nenhum projeto em uma solução.

 Os projetos desempenham uma função significativa para determinar qual editor é usado quando um usuário abre um item de projeto. Um projeto pode ser criado para abrir determinados arquivos usando um editor específico do projeto ou um editor padrão.

 Um editor específico de projeto normalmente requer que o usuário tenha conhecimento especial ou use interfaces especiais do projeto. Para obter mais informações, consulte [como: abrir editores de Project-Specific](../../extensibility/how-to-open-project-specific-editors.md).

 Um editor padrão pode abrir qualquer arquivo de uma extensão específica em qualquer projeto. O usuário pode personalizar alguns editores padrão, como o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Editor de texto, para projetos, mas ainda manter seu caractere público. Os editores padrão são criados usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> método.

 Se nenhum projeto na solução responder que pode abrir um item de projeto, o IDE fornece um projeto especial chamado projeto de arquivos diversos que abre qualquer arquivo.

 Esse projeto especial fornece a abertura de um arquivo fora do contexto de um projeto. Durante o processamento do <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> método, o projeto de arquivos diversos sempre responde com uma prioridade muito baixa. Portanto, o projeto de arquivos diversos sempre gera qualquer projeto de prioridade mais alta que pode abrir arquivos.

 O projeto de arquivos diversos não exige que o usuário o crie explicitamente com a caixa de diálogo **novo projeto** . Além disso, o projeto de arquivos diversos não gerencia permanentemente uma lista de membros do projeto. Ele usa um recurso opcional para registrar uma lista de arquivos usados mais recentemente para cada usuário.

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument>
- <xref:Microsoft.VisualStudio.Shell.Interop.VSDOCUMENTPRIORITY>
- [Como abrir editores específicos a um projeto](../../extensibility/how-to-open-project-specific-editors.md)
- [Como abrir editores padrão](../../extensibility/how-to-open-standard-editors.md)
- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
- [Adicionando o projeto e os modelos de item do projeto](../../extensibility/internals/adding-project-and-project-item-templates.md)
