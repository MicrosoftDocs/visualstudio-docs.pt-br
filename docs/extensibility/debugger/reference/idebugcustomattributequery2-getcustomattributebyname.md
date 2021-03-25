---
description: Obtém os bytes de atributos personalizados, dado o nome do atributo personalizado.
title: 'IDebugCustomAttributeQuery2:: GetCustomAttributeByName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dd8b1793bad585dd808ebd812b610cd68aabc129
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077597"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
Obtém os bytes de atributos personalizados, dado o nome do atributo personalizado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCustomAttributeByName( 
   LPCOLESTR pszCustomAttributeName,
   BYTE*     ppBlob,
   DWORD*    pdwLen
);
```

```csharp
int GetCustomAttributeByName(
   [In] string        pszCustomAttributeName,
   [In, Out] byte[]   ppBlob,
   [In, Out] ref uint pdwLen
);
```

## <a name="parameters"></a>Parâmetros
`pszCustomAttributeName`\
no Uma cadeia de caracteres que contém o nome do atributo personalizado a ser pesquisado.

`ppBlob`\
[entrada, saída] Uma matriz que é preenchida com os bytes do atributo personalizado.

`pdwLen`\
[entrada, saída] Especifica o número máximo de bytes a serem retornados na `ppBlob` matriz e retorna o número de bytes gravados na matriz.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK ou retornará S_FALSE se o atributo personalizado não existir. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Defina o `ppBlob` parâmetro como um valor nulo para retornar o número de bytes de atributos disponíveis. Em seguida, aloque uma matriz e passe essa matriz no para o `ppBlob` parâmetro.

 Os bytes de atributo representam os dados brutos do atributo personalizado.

 Se os `ppBlob` `pdwLen` parâmetros e forem definidos como um valor nulo, esse método poderá ser usado para determinar se o atributo personalizado simplesmente existe. No entanto, uma alternativa mais fácil é chamar o método [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md) .

## <a name="see-also"></a>Confira também
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
