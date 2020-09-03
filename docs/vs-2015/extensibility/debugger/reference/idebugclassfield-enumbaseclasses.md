---
title: 'IDebugClassField:: EnumBaseClasses | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumBaseClasses
helpviewer_keywords:
- IDebugClassField::EnumBaseClasses method
ms.assetid: 78749674-ef75-46d3-a1f4-ff33afd90e32
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: acfdc872ba5f7cf1989ea1d9ec67f82f1c0419b0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191053"
---
# <a name="idebugclassfieldenumbaseclasses"></a>IDebugClassField::EnumBaseClasses
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Cria um enumerador para as classes base dessa classe.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT EnumBaseClasses(   
   IEnumDebugFields** ppEnum  
);  
```  
  
```csharp  
int EnumBaseClasses(  
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppEnum`  
 fora Retorna um objeto [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) que representa a lista de classes base. Retorna um valor nulo se não houver nenhuma classe base.  
  
## <a name="return-value"></a>Valor Retornado  
 Se for bem-sucedido, retornará S_OK, retornará S_SH_NO_BASE_CLASSES se não houver nenhuma classe base (e o `ppEnum` parâmetro for definido como um valor nulo); caso contrário, retornará um código de erro.  
  
## <a name="remarks"></a>Comentários  
 As classes base no objeto enumerador são especificadas na ordem da classe base mais imediata (ou mais derivada) para a classe base mais remota. Por exemplo, considerando as classes C++:  
  
```  
class Root { }  
class Level1 : Root { }  
class Level2 : Level1 { }  
class MyClass : Level2 { }  
```  
  
 A enumeração retornaria as classes base na ordem `Level2` , `Level1` , `Root` .  
  
## <a name="see-also"></a>Consulte Também  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
