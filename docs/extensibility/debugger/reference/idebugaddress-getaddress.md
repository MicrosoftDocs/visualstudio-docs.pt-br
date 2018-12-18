---
title: IDebugAddress::GetAddress | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 869094fabca44eca352a9610ac59a6627df74dd7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873351"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
Retorna uma estrutura que descreve um objeto e sua localização em seu escopo ou contêiner.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetAddress (  
   DEBUG_ADDRESS * pAddress  
);  
```  
  
```csharp  
int GetAddress(  
   DEBUG_ADDRESS[] pAddress  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pAddress`  
 [no, out] Um [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) estrutura que é preenchida por este método.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 O [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) estrutura é passada para esse método, que, em seguida, preenche-o com as informações apropriadas. Como essas informações são interpretadas depende do tipo de informações retornadas e o manipulador de símbolo em si. Ver [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md) para obter mais detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)