---
description: Obtém as informações de atributo como um blob de bytes.
title: 'IDebugCustomAttribute:: GetAttributeBytes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeBytes
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeBytes
ms.assetid: cf34583b-6530-4dcc-89f8-eb27e4e8d594
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d7cfc3ba650ff8277bb6cb85f5d1530d202bd426
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163077"
---
# <a name="idebugcustomattributegetattributebytes"></a>IDebugCustomAttribute::GetAttributeBytes
Obtém as informações de atributo como um blob de bytes.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAttributeBytes( 
   BYTE*  ppBlob,
   DWORD* pdwLen
);
```

```csharp
int GetAttributeBytes(
   ref byte[] ppBlob,
   ref uint   pdwLen
);
```

## <a name="parameters"></a>Parâmetros
`ppBlob`\
[entrada, saída] Uma matriz que é preenchida com os bytes de atributo.

`pdwLen`\
[entrada, saída] Especifica o número máximo de bytes a serem retornados na `ppBlob` matriz e retorna o número de bytes gravados na matriz.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Defina o `ppBlob` parâmetro como um valor nulo para retornar o número de bytes de atributos disponíveis. Em seguida, aloque uma matriz e passe essa matriz no para o `ppBlob` parâmetro.

 Os bytes de atributo representam os dados brutos do atributo personalizado.

## <a name="see-also"></a>Confira também
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
