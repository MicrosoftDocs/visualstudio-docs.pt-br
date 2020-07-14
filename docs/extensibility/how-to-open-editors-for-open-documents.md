---
title: 'Como: abrir editores para documentos abertos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- editors [Visual Studio SDK], opening for open documents
ms.assetid: 1a0fa49c-efa4-4dcc-bdc0-299b7052acdc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0f67a7fad5944e82087f520508ef9f4a66b7109d
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905815"
---
# <a name="how-to-open-editors-for-open-documents"></a>Como abrir editores para documentos abertos
Antes que um projeto abra uma janela de documento, primeiro o projeto deve determinar se o arquivo já está aberto na janela do documento para outro editor. O arquivo pode ser aberto em um editor específico do projeto ou um dos editores padrão registrados com o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] .

## <a name="open-a-project-specific-editor"></a>Abrir um editor específico do projeto
 Use o procedimento a seguir para abrir um editor específico do projeto para um arquivo que já está aberto.

### <a name="to-open-a-project-specific-editor-for-an-open-file"></a>Para abrir um editor específico do projeto para um arquivo aberto

1. Chame o método <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> .

    Essa chamada retorna ponteiros para a hierarquia do documento, item de hierarquia e quadro de janela, se apropriado.

2. Se o documento estiver aberto, o projeto deverá verificar se apenas um objeto de dados de documento existe ou se um objeto de exibição de documento também está presente.

   - Se um objeto de exibição de documento existir e essa exibição for para um item de hierarquia ou hierarquia diferente, o projeto usará o ponteiro para o quadro de janela da exibição para retonar a janela existente.

   - Se um objeto de exibição de documento existir e essa exibição for para a mesma hierarquia e item de hierarquia, o projeto poderá abrir uma segunda exibição se puder anexar ao objeto de dados de documento subjacente. Caso contrário, o projeto deve usar o ponteiro para o quadro de janela da exibição para retonar a janela existente.

   - Se apenas o objeto de dados do documento existir, o projeto deverá determinar se ele pode usar o objeto de dados do documento para sua exibição. Se o objeto de dados do documento for compatível, conclua as etapas discutidas em [abrir um editor específico do projeto](../extensibility/how-to-open-project-specific-editors.md).

     Se o objeto de dados do documento não for compatível, um erro deverá ser exibido para o usuário indicando que o arquivo está em uso no momento. Esse erro só deve ser exibido em casos transitórios, como quando um arquivo está sendo compilado ao mesmo tempo em que o usuário está tentando abrir o arquivo usando um editor diferente do editor de [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] texto principal. O editor de texto principal pode compartilhar o objeto de dados de documento com o compilador.

3. Se o documento não estiver aberto porque não há objeto de dados de documento ou objeto de exibição de documento, conclua as etapas em [abrir um editor específico do projeto](../extensibility/how-to-open-project-specific-editors.md).

## <a name="open-a-standard-editor"></a>Abrir um editor padrão
 Use o procedimento a seguir para abrir um editor padrão para um arquivo que já está aberto.

### <a name="to-open-a-standard-editor-for-an-open-file"></a>Para abrir um editor padrão para um arquivo aberto

1. Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>.

     Esse método primeiro verifica se o documento ainda não está aberto chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.IsDocumentOpen%2A> . Se o documento já estiver aberto, sua janela do editor será retonada.

2. Se o documento não estiver aberto, conclua as etapas em [como: abrir editores padrão](../extensibility/how-to-open-standard-editors.md).

## <a name="see-also"></a>Confira também
- [Abrir e salvar itens de projeto](../extensibility/internals/opening-and-saving-project-items.md)
- [Como: abrir editores específicos do projeto](../extensibility/how-to-open-project-specific-editors.md)
- [Como: abrir editores padrão](../extensibility/how-to-open-standard-editors.md)
