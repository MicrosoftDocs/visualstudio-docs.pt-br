---
title: Salvar um documento personalizado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5425a1c35816fd85847915029e3b6f2da1ed75a6
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132542"
---
# <a name="saving-a-custom-document"></a>Salvar um documento personalizado
Os identificadores de ambiente a **salvar**, **Salvar como**, e **Salvar tudo** comandos. Quando um usuário clica **salvar**, **Salvar como**, **ou salvar tudo** no **arquivo** menu ou fecha a solução, resultando em um Salvar tudo, o seguinte processo ocorre.  
  
 ![Editor de cliente salvar](../../extensibility/internals/media/private.gif "privada")  
Salvar, salvar como e tratamento de um editor personalizado de comando Salvar tudo  
  
 Esse processo é detalhado nas etapas a seguir:  
  
1.  Para o **salvar** e **Salvar como** comandos, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> de serviço para determinar a janela do documento ativo e, portanto, os itens devem ser salvos. Depois que a janela do documento ativo é conhecida, o ambiente localiza o ponteiro de hierarquia e o identificador de item (itemID) para o documento na tabela de documento em execução. Para obter mais informações, consulte [tabela de documento executando](../../extensibility/internals/running-document-table.md).  
  
     Para o comando Salvar tudo, o ambiente usa as informações na tabela de documento em execução para compilar a lista de todos os itens para salvar.  
  
2.  Quando a solução recebe um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> chamada, itera por meio do conjunto de itens selecionados (ou seja, as várias seleções expostas pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> serviço).  
  
3.  Em cada item na seleção, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> método para determinar se o comando de menu Salvar deve ser habilitado. Se um ou mais itens estiverem sujos, o comando Salvar está habilitado. Se a hierarquia usa um editor padrão, em seguida, os representantes de hierarquia consultando sujas status para o editor chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> método.  
  
4.  Em cada item selecionado que foi alterado, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> método nas hierarquias apropriados.  
  
     No caso de um editor personalizado, a comunicação entre o objeto de dados de documento e o projeto é privada. Portanto, quaisquer dúvidas de persistência especiais são tratadas entre esses dois objetos.  
  
    > [!NOTE]
    >  Se você implementar sua própria persistência, certifique-se de chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> método para economizar tempo. Este método verifica para ter certeza de que é seguro salvar o arquivo (por exemplo, o arquivo não é somente leitura).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)