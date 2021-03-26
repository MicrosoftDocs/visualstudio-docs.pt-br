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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 84d6e807e3be6d0fbdaa94834fbc8cad37f8e4d2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088075"
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
