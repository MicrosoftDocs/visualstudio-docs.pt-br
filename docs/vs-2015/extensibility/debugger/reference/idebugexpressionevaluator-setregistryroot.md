---
title: IDebugExpressionEvaluator::SetRegistryRoot | Microsoft Docs
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
- IDebugExpressionEvaluator::SetRegistryRoot
helpviewer_keywords:
- IDebugExpressionEvaluator::SetRegistryRoot method
ms.assetid: 790886d8-1975-4d3c-9a75-cd86c1faf4ca
caps.latest.revision: 12
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5d91ab4e3a4b46e9eb44346a91b88055cc6a4175
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49890460"
---
# <a name="idebugexpressionevaluatorsetregistryroot"></a>IDebugExpressionEvaluator::SetRegistryRoot
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método define a raiz do registro. Usado para a depuração lado a lado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT SetRegistryRoot (   
   LPCOLESTR ustrRegistryRoot  
);  
```  
  
```csharp  
int SetRegistryRoot(  
   string ustrRegistryRoot  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ustrRegistryRoot`  
 [in] A nova raiz do registro.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 A raiz do Registro especificada é normalmente definida quando o avaliador de expressão é instanciado pela primeira vez e aponta para a chave do registro para uma versão específica do Visual Studio (HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\\*x. y* , onde *x. y* é um número de versão).  
  
## <a name="see-also"></a>Consulte também  
 [IDebugExpressionEvaluator](../../../extensibility/debugger/reference/idebugexpressionevaluator.md)

