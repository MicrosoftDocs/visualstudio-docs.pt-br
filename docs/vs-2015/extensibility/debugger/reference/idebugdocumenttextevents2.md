---
title: IDebugDocumentTextEvents2 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dca9d3c8de956faf2dab5c9090c9963a7c9fbea0
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58926397"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Essa interface é usada para notificar o Visual Studio sobre as alterações no documento de origem que são fornecidas pelo mecanismo de depuração.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugDocumentTextEvents2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 O DE implementa essa interface para dar suporte a fazer as alterações no código-fonte. Normalmente, essa interface é implementada no mesmo objeto que implementa o [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) interface.  
  
## <a name="notes-for-callers"></a>Observações para chamadores  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Obtém a essa interface por meio de uma chamada para o <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A> método. O <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> interface é obtido de uma chamada para o <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A> método. O <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> interface é obtida chamando o [QueryInterface](http://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3) método em um [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) interface.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable  
 A tabela a seguir mostra os métodos de `IDebugDocumentTextEvents2`.  
  
|Método|Descrição|  
|------------|-----------------|  
|[onDestroy](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|Indica que todo o documento foi destruído.|  
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|Notifica o pacote de depuração que o texto foi inserido no documento.|  
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|Notifica o pacote de depuração que o texto foi removido do documento.|  
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|Notifica o pacote de depuração que o texto foi substituído no documento.|  
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|Notifica o pacote de depuração que foram atualizados os atributos de texto no documento.|  
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|Notifica o receptor do evento que os atributos do documento foram atualizados.|  
  
## <a name="remarks"></a>Comentários  
 Somente os mecanismos de depuração que fornecem seus próprios documentos seriam aproveitar o `IDebugDocumentTextEvent2` interface. Um exemplo disso seria um mecanismo de depuração de script. No processo de interpretar os scripts, novo código-fonte pode ser gerado que não está presente em qualquer arquivo de disco e é conhecido apenas DE.  
  
## <a name="requirements"></a>Requisitos  
 Header: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)   
 [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
