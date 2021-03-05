---
description: Obtém uma interface especificada entre limites de processo.
title: 'IDebugProviderProgramNode2:: UnmarshalDebuggeeInterface | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0f51484ae1e9acbb9b94fe546f8157145673e22f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167861"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
Obtém uma interface especificada entre limites de processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>Parâmetros
`riid`\
no GUID da interface a ser obtida.

`ppvObject`\
fora Retorna o objeto que implementa a interface desejada. [C++] isso pode ser convertido diretamente no tipo de interface desejado. [C#] use o <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> método para obter a interface desejada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é usado quando o mecanismo de depuração está em execução no [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] espaço de processo e o programa que está sendo depurado está em execução em seu próprio espaço de processo.

## <a name="see-also"></a>Confira também
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
