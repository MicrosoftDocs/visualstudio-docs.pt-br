---
title: IDebugMemoryContext2::Subtract | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugMemoryContext2::Subtract
helpviewer_keywords:
- Subtract method
- IDebugMemoryContext2::Subtract method
ms.assetid: 63df14c7-8d7e-47c1-afa7-5a1ab5d8eaba
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 70ed92b6098a736baf3bfa927a368f38a9ba01a7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721611"
---
# <a name="idebugmemorycontext2subtract"></a>IDebugMemoryContext2::Subtract
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Subtrai o valor especificado do contexto atual e retorna um novo contexto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT Subtract(   
   UINT64                 dwCount,  
   IDebugMemoryContext2** ppMemCxt  
);  
```  
  
```csharp  
int Subtract(  
   ulong                    dwCount,   
   out IDebugMemoryContext2 ppMemCxt  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwCount`  
 [in] O número de bytes de memória para diminuir.  
  
 `ppMemCxt`  
 [out] Retorna um novo [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Um contexto de memória é um endereço, portanto, subtrair um valor de um endereço produz um novo endereço que requer uma nova interface de contexto.  
  
 Esse método sempre deve produzir um novo contexto, mesmo se o endereço resultante está fora do espaço de memória associado a este contexto. A única exceção a isso é se nenhuma memória pode ser alocada para o novo contexto ou se `ppMemCxt` é um valor nulo (que é um erro).  
  
## <a name="see-also"></a>Consulte também  
 [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)

