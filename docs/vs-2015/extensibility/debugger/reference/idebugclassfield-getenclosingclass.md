---
title: IDebugClassField::GetEnclosingClass | Microsoft Docs
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
- IDebugClassField::GetEnclosingClass
helpviewer_keywords:
- IDebugClassField::GetEnclosingClass method
ms.assetid: a0c12e3c-9ea0-4dfb-9e45-8cea18725022
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3b348fddc3dbd49c4ea74a3ab69eb1d6e774fb9a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809890"
---
# <a name="idebugclassfieldgetenclosingclass"></a>IDebugClassField::GetEnclosingClass
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Obtém a classe que engloba essa classe.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetEnclosingClass(   
   IDebugClassField** ppClassField  
);  
```  
  
```csharp  
int GetEnclosingClass(  
   out IDebugClassField ppClassField  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppClassField`  
 [out] Retorna um [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) a classe de objeto que representa o delimitador. Retorna um valor nulo se não houver nenhuma classe delimitadora.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará S_OK; Caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Se a classe representada por este [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) objeto é uma classe aninhada, em seguida, a `ppClassField` parâmetro retorna um `IDebugClassField` a classe de objeto que representa o delimitador. Por exemplo, dada esta definição de classe:  
  
```  
class RootClass {  
   class NestedClass { }  
};  
```  
  
 Chamando o `GetEnclosingClass` método em de `IDebugClassField` objeto que representa o `NestedClass` classe retorna um `IDebugClassField` que representa a classe de objeto `RootClass`.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)

