---
title: IDebugAddress::GetAddress | Microsoft Docs
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
- IDebugAddress::GetAddress
helpviewer_keywords:
- IDebugAddress:GetAddress method
ms.assetid: 2590387b-5d36-4116-9a75-737957b8898e
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: cf2888a476c631fd17b8f97971deecfc699bfd57
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734345"
---
# <a name="idebugaddressgetaddress"></a>IDebugAddress::GetAddress
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

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

