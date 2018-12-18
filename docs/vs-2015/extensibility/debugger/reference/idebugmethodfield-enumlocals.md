---
title: IDebugMethodField::EnumLocals | Microsoft Docs
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
- IDebugMethodField::EnumLocals
helpviewer_keywords:
- IDebugMethodField::EnumLocals method
ms.assetid: b0456a6d-2b96-49e2-a871-516571b4f6a5
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d54ae7fbf8c8a16cb62b7c21a7b52fc52d6d8d08
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741841"
---
# <a name="idebugmethodfieldenumlocals"></a>IDebugMethodField::EnumLocals
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Cria um enumerador para variáveis locais selecionados do método.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT EnumLocals(   
   IDebugAddress*     pAddress,  
   IEnumDebugFields** ppLocals  
);  
```  
  
```csharp  
int EnumLocals(  
   IDebugAddress        pAddress,   
   out IEnumDebugFields ppLocals  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pAddress`  
 [in] Uma [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) objeto que representa o endereço de depuração que seleciona o contexto ou escopo do qual obter os locais.  
  
 `ppLocals`  
 [out] Retorna um [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) objeto que representa uma lista de locais; caso contrário, retornará um valor nulo se não houver nenhum locais.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, Retorna S_OK ou retornará S_FALSE se não houver nenhum locais. Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Somente as variáveis definidas dentro do bloco que contém o endereço de depuração determinado são enumeradas. Se todos os locais, incluindo qualquer locais gerados pelo compilador são necessários, chame o [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md) método.  
  
 Um método pode conter vários contextos ou blocos de escopo. Por exemplo, o seguinte método artificial contém três escopos, os dois blocos internos e o corpo do método em si.  
  
```csharp  
public void func(int index)  
{  
    // Method body scope  
    int a = 0;  
    if (index == 1)  
    {  
        // Inner scope 1  
        int temp1 = a;  
    }  
    else  
    {  
        // Inner scope 2  
        int temp2 = a;  
    }  
}  
```  
  
 O [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) objeto representa o `func` método em si. Chamar o `EnumLocals` método com um [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) definido como o `Inner Scope 1` endereço retorna uma enumeração que contém o `temp1` variável, por exemplo.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)   
 [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)   
 [EnumAllLocals](../../../extensibility/debugger/reference/idebugmethodfield-enumalllocals.md)

