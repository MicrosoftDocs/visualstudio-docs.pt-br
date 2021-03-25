---
description: Obtém o documento de origem associado a este fluxo de entrada.
title: 'IDebugDisassemblyStream2:: GetDocument | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetDocument
helpviewer_keywords:
- IDebugDisassemblyStream2::GetDocument
ms.assetid: 3d039a44-ebaa-4413-ac18-7cfd92c408bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1d214cf9be09dea4a4bf244224a5ae1bd6d882ef
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066991"
---
# <a name="idebugdisassemblystream2getdocument"></a>IDebugDisassemblyStream2::GetDocument
Obtém o documento de origem associado a este fluxo de entrada.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDocument( 
   BSTR              bstrDocumentUrl,
   IDebugDocument2** ppDocument
);
```

```csharp
int GetDocument( 
   string              bstrDocumentUrl,
   out IDebugDocument2 ppDocument
);
```

## <a name="parameters"></a>Parâmetros
`bstrDocumentUrl`\
no A URL do documento.

`ppDocument`\
fora Retorna um objeto [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) que representa o documento.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é implementado por mecanismos de depuração que têm documentos de texto que não são armazenados em um arquivo real.

## <a name="see-also"></a>Confira também
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
