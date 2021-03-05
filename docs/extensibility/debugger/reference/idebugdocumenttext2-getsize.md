---
description: Recupera o tamanho do texto nesta posição no documento.
title: 'IDebugDocumentText2:: GetSize | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 91dd1b2a510589ab048bd1bd290b0ab4aabe571b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167302"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
Recupera o tamanho do texto nesta posição no documento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetSize( 
   ULONG* pcNumLines,
   ULONG* pcNumChars
);
```

```csharp
int GetSize( 
   ref uint pcNumLines,
   ref uint pcNumChars
);
```

## <a name="parameters"></a>Parâmetros
`pcNumLines`\
fora Retorna o número de linhas de texto.

`pcNumChars`\
fora Retorna o número de caracteres de texto.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários

 [Somente C++] Se um valor específico não for desejado, passe um NULL para o parâmetro.

 [Somente C#] Ambos os parâmetros devem ser especificados.

## <a name="see-also"></a>Confira também
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
