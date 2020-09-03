---
title: IDebugDocumentContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentContext2
helpviewer_keywords:
- IDebugDocumentContext2
ms.assetid: 2a446c71-8100-4c09-a1cc-fd446bd74030
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d31a78412a1a6b20518b6f38ba76b7964cbdbe3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80731736"
---
# <a name="idebugdocumentcontext2"></a>IDebugDocumentContext2
Essa interface representa uma posição em um documento de arquivo de origem.

## <a name="syntax"></a>Syntax

```
IDebugDocumentContext2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para depuração de nível de código-fonte. Além de uma posição no código-fonte, essa interface fornece métodos para comparar contextos e navegar por um documento de código-fonte.

## <a name="notes-for-callers"></a>Observações para chamadores
 Os métodos em várias interfaces, geralmente as interfaces [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md) e [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md) , retornam essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugDocumentContext2` .

|Método|Descrição|
|------------|-----------------|
|[GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)|Obtém o documento que contém este contexto de documento.|
|[GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)|Obtém o nome de exibição do documento que contém este contexto de documento.|
|[EnumCodeContexts](../../../extensibility/debugger/reference/idebugdocumentcontext2-enumcodecontexts.md)|Recupera uma lista de todos os contextos de código associados a este contexto de documento.|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugdocumentcontext2-getlanguageinfo.md)|Obtém o idioma associado a este contexto de documento.|
|[GetStatementRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getstatementrange.md)|Obtém o intervalo de instruções do arquivo deste contexto de documento.|
|[GetSourceRange](../../../extensibility/debugger/reference/idebugdocumentcontext2-getsourcerange.md)|Obtém o intervalo de origem do arquivo deste contexto de documento.|
|[Comparar](../../../extensibility/debugger/reference/idebugdocumentcontext2-compare.md)|Compara este contexto de documento com uma determinada matriz de contextos de documento.|
|[Seek](../../../extensibility/debugger/reference/idebugdocumentcontext2-seek.md)|Move o contexto do documento por um determinado número de instruções ou linhas.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)
