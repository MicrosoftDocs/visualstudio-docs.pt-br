---
title: IDebugMemoryBytes2::WriteAt | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a2d164f0ef816285e2df4a9e49b09d55feb90d25
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49864264"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
Grava o número especificado de bytes de memória, iniciando no endereço especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT WriteAt(   
   IDebugMemoryContext2* pStartContext,  
   DWORD                 dwCount,  
   BYTE*                 rgbMemory  
);  
```  
  
```csharp  
int WriteAt(  
   IDebugMemoryContext2 pStartContext,  
   uint                 dwCount,  
   byte[]               rgbMemory  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pStartContext`  
 [in] O [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) objeto que especifica o local iniciar a gravação de bytes.  
  
 `dwCount`  
 [in] O número de bytes a serem gravados.  
  
 `rgbMemory`  
 [in] Bytes a serem gravados. Essa matriz deve para ter pelo menos `dwCount` bytes de tamanho.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` se nem todos os bytes poderia ser escritos ou retorna um código de erro (normalmente `E_FAIL`).  
  
## <a name="remarks"></a>Comentários  
 Se o endereço inicial não está dentro da janela de memória, representada por este [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) do objeto, nenhuma gravação ocorrerá e um código de erro `E_FAIL` é retornado — mesmo que se sobreponha a quantidade para gravar no espaço de memória.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)   
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)