---
title: Salvando um documento personalizado | Microsoft Docs
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
- persistence, saving custom documents
- projects [Visual Studio SDK], saving custom documents
- editors [Visual Studio SDK], saving custom documents
ms.assetid: 040b36d6-1f0a-4579-971c-40fbb46ade1d
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5d292cc60b782f8036367c72bf0e59e8b83d5191
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764248"
---
# <a name="saving-a-custom-document"></a>Salvando um documento personalizado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Os identificadores de ambiente do **salve**, **Salvar como**, e **Salvar tudo** comandos. Quando um usuário clica **salvar**, **Salvar como**, **ou salvar tudo** sobre a **arquivo** menu ou fecha a solução, resultando em um Salvar tudo, o seguinte processo ocorre.  
  
 ![Cliente Editor Save](../../extensibility/internals/media/private.gif "privada")  
Salvar, salvar como e salvar tudo manipulação de comando para um editor personalizado  
  
 Esse processo é detalhado nas etapas a seguir:  
  
1.  Para o **salve** e **Salvar como** comandos, o ambiente usa o <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> de serviço para determinar a janela do documento ativo e, portanto, quais itens devem ser salvas. Depois que a janela de documento ativa é conhecida, o ambiente localiza o ponteiro de hierarquia e o identificador do item (itemID) para o documento na tabela de documento em execução. Para obter mais informações, consulte [tabela de documento em execução](../../extensibility/internals/running-document-table.md).  
  
     Para o comando Salvar tudo, o ambiente usa as informações na tabela de documento em execução para compilar a lista de todos os itens para salvar.  
  
2.  Quando a solução recebe um <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> chamada, ele itera no conjunto de itens selecionados (ou seja, as várias seleções expostas pelo <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> service).  
  
3.  Em cada item na seleção, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IsItemDirty%2A> método para determinar se o comando de menu Salvar deve ser habilitado. Se um ou mais itens estiverem sujos, o comando Save está habilitado. Se a hierarquia usa um editor padrão, em seguida, os delegados de hierarquia consultando sujos status para o editor chamando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2.IsDocDataDirty%2A> método.  
  
4.  Em cada item selecionado está sujo, a solução usa o ponteiro de hierarquia para chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.SaveItem%2A> método nas hierarquias apropriados.  
  
     No caso de um editor personalizado, a comunicação entre o objeto de dados de documento e o projeto é privada. Assim, preocupações relacionadas à persistência especiais são tratadas entre esses dois objetos.  
  
    > [!NOTE]
    >  Se você implementar sua própria persistência, certifique-se de chamar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2.QuerySaveFiles%2A> método para economizar tempo. Esse método verifica para ter certeza de que é seguro salvar o arquivo (por exemplo, o arquivo não é somente leitura).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>   
 [Abrir e salvar itens de projeto](../../extensibility/internals/opening-and-saving-project-items.md)

