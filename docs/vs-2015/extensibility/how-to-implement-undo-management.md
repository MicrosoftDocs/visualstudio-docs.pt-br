---
title: 'Como: implementar o gerenciamento de desfazer | Microsoft Docs'
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
- editors [Visual Studio SDK], legacy - undo management
ms.assetid: 1942245d-7a1d-4a11-b5e7-a3fe29f11c0b
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: f7eb3e3a1bbda905b2f5c5819835b10513d444fb
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806094"
---
# <a name="how-to-implement-undo-management"></a>Como: implementar o gerenciamento de desfazer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A principal interface usada para o gerenciamento de desfazer é <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>, que é implementado pelo ambiente. Para dar suporte ao gerenciamento de desfazer, implemente a unidades de desfazer separado (ou seja, <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoUnit>, que pode conter várias etapas individuais.  
  
 Como implementar o gerenciamento de desfazer varia dependendo se o editor oferece suporte a vários modos de exibição ou não. Os procedimentos para cada implementação são detalhados nas seções a seguir.  
  
## <a name="cases-where-an-editor-supports-a-single-view"></a>Casos em que um editor dá suporte a uma única exibição  
 Nesse cenário, o editor não oferece suporte a vários modos de exibição. Há apenas um editor e um documento, e eles dão suporte a desfazer. Use o procedimento a seguir para implementar o gerenciamento de desfazer.  
  
#### <a name="to-support-undo-management-for-a-single-view-editor"></a>Para dar suporte ao gerenciamento de desfazer para um editor de modo de exibição único  
  
1.  Chame `QueryInterface` sobre o `IServiceProvider` interface no quadro de janela para `IOleUndoManager`, do objeto de visualização de documento para acessar o Gerenciador de desfazer (`IID_IOLEUndoManager`).  
  
2.  Quando um modo de exibição está localizado em um quadro de janela, ela recebe um ponteiro de site, o que ele pode usar para chamar `QueryInterface` para `IServiceProvider`.  
  
## <a name="cases-where-an-editor-supports-multiple-views"></a>Casos em que um editor dá suporte a vários modos de exibição  
 Se você tiver a separação de documento e exibição, há o Gerenciador de desfazer normalmente um associado ao documento em si. Todas as unidades de desfazer são colocadas no Gerenciador de um Desfazer associado ao objeto de dados do documento.  
  
 Em vez da consulta de modo de exibição para o Gerenciador de desfazer, o que há um para cada modo de exibição, os dados do documento de objeto chamadas <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> para instanciar o Gerenciador de desfazer, especificando um identificador de classe de CLSID_OLEUndoManager. O identificador de classe é definido no arquivo OCUNDOID.h.  
  
 Ao usar <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2.CreateInstance%2A> para criar sua própria instância do Gerenciador de desfazer, use o procedimento a seguir para conectar seu Gerenciador de desfazer no ambiente.  
  
#### <a name="to-hook-your-undo-manager-into-the-environment"></a>Para conectar o Gerenciador de desfazer para o ambiente  
  
1. Chame `QueryInterface` no objeto retornado de <xref:Microsoft.VisualStudio.Shell.Interop.ILocalRegistry2> para `IID_IOleUndoManager`. Store o ponteiro para <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager>.  
  
2. Chame `QueryInterface` na `IOleUndoManager` para `IID_IOleCommandTarget`. Store o ponteiro para <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>.  
  
3. Retransmissão sua <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.QueryStatus%2A> e <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget.Exec%2A> chamadas em armazenado `IOleCommandTarget` interface para os seguintes comandos StandardCommandSet97:  
  
   -   cmdidUndo  
  
   -   cmdidMultiLevelUndo  
  
   -   cmdidRedo  
  
   -   cmdidMultiLevelRedo  
  
   -   cmdidMultiLevelUndoList  
  
   -   cmdidMultiLevelRedoList  
  
4. Chame `QueryInterface` na `IOleUndoManager` para `IID_IVsChangeTrackingUndoManager`. Store o ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>.  
  
    Use o ponteiro para <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager> para chamar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.MarkCleanState%2A>, o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.AdviseTrackingClient%2A>e o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager.UnadviseTrackingClient%2A> métodos.  
  
5. Chame `QueryInterface` na `IOleUndoManager` para `IID_IVsLinkCapableUndoManager`.  
  
6. Chame <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkCapableUndoManager.AdviseLinkedUndoClient%2A> com seu documento, que também deve implementar o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLinkedUndoClient> interface. Quando o documento é fechado, chame `IVsLinkCapableUndoManager::UnadviseLinkedUndoClient`.  
  
7. Quando o documento é fechado, chame `QueryInterface` em seu Gerenciador de desfazer para `IID_IVsLifetimeControlledObject`.  
  
8. Chamar <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject.SeverReferencesToOwner%2A>.  
  
9. Quando forem feitas alterações no documento, chame <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> no Gerenciador de com um `OleUndoUnit` classe. O <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A> método mantém uma referência ao objeto, geralmente você liberá-lo logo após o <xref:Microsoft.VisualStudio.OLE.Interop.IOleUndoManager.Add%2A>.  
  
   O `OleUndoManager` classe representa uma instância da pilha de desfazer. Portanto, há um objeto de Gerenciador de desfazer por entidade de dados que estão sendo controlada para desfazer ou refazer.  
  
> [!NOTE]
>  Enquanto o objeto do Gerenciador de desfazer é usado pelo editor de texto, ele é um componente geral que tem suporte específico para o editor de texto. Se você quiser dar suporte a vários nível desfazer ou refazer, você pode usar esse objeto para fazer isso.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsChangeTrackingUndoManager>   
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLifetimeControlledObject>   
 [Como limpar a pilha de desfazer](../extensibility/how-to-clear-the-undo-stack.md)

