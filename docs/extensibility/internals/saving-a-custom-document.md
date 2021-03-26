---
title: Salvando um documento personalizado | Microsoft Docs
description: Saiba mais sobre o processo que ocorre para um documento personalizado para um tipo de projeto que você adiciona ao IDE do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a536a5f0f2b1cac09c65079974c661e09e9139ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080912"
---
# <a name="saving-a-custom-document"></a>Salvando um documento personalizado
O ambiente manipula os comandos **salvar**, **salvar como** e **salvar todos** . Quando um usuário clica em **salvar**, **salvar como** **ou salvar tudo** no menu **arquivo** ou fecha a solução, resultando em um salvamento de tudo, o processo a seguir ocorre.

 ![Salvar do editor do cliente](../../extensibility/internals/media/private.gif "Privados") Salvar, salvar como e salvar todo o tratamento de comandos para um editor personalizado

 Esse processo é detalhado nas seguintes etapas:

1. Para os comandos **salvar** e **salvar como** , o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> serviço para determinar a janela do documento ativo e, portanto, quais itens devem ser salvos. Depois que a janela do documento ativo é conhecida, o ambiente localiza o ponteiro de hierarquia e o identificador de item (itemID) do documento na tabela de documentos em execução. Para obter mais informações, consulte [executando a tabela de documentos](../../extensibility/internals/running-document-table.md).

     Para o comando salvar tudo, o ambiente usa as informações na tabela de documentos em execução para compilar a lista de todos os itens a serem salvos.

2. Quando a solução recebe uma <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> chamada, ela itera no conjunto de itens selecionados (ou seja, as várias seleções expostas pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> serviço).

3. Em cada item na seleção, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> método para determinar se o comando de menu salvar deve ser habilitado. Se um ou mais itens estiverem sujos, o comando salvar será habilitado. Se a hierarquia usar um editor padrão, a hierarquia delegará a consulta de status sujo para o editor chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> método.

4. Em cada item selecionado que está sujo, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> método nas hierarquias apropriadas.

     No caso de um editor personalizado, a comunicação entre o objeto de dados do documento e o projeto é particular. Portanto, qualquer preocupação especial de persistência é tratada entre esses dois objetos.

    > [!NOTE]
    > Se você implementar sua própria persistência, certifique-se de chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> método para economizar tempo. Esse método verifica se é seguro salvar o arquivo (por exemplo, o arquivo não é somente leitura).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>
- [Abrindo e salvando itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)
