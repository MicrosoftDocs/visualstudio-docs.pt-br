---
title: IPropertyProxyEESide::ResolveAssemblyRef | Microsoft Docs
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
- IPropertyProxyEESide::ResolveAssemblyRef
helpviewer_keywords:
- IPropertyProxyEESide::ResolveAssemblyRef
ms.assetid: 662ca0a6-dad0-4c00-a718-bb3bbc5bd9da
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 228c19b596cb8b9069cba5f36ec980f1f86d69aa
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913280"
---
# <a name="ipropertyproxyeesideresolveassemblyref"></a>IPropertyProxyEESide::ResolveAssemblyRef
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Determina o local da referência de assembly gerenciado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT ResolveAssemblyRef(  
   BSTR*                  assemName,  
   IEEDataStorage**       assemBytes,  
   IEEDataStorage**       assemPdb,  
   BSTR*                  assemLocation,  
   ASSEMBLYLOCRESOLUTION* alr  
);  
```  
  
```csharp  
int ResolveAssemblyRef(  
   ref string                     assemName,  
   out IEEDataStorage             assemBytes,  
   out IEEDataStorage             assemPdb,  
   out string                     assemLocation,  
   out enum_ASSEMBLYLOCRESOLUTION alr  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `assemName`  
 [in] Nome do assembly para resolver.  
  
 `assemBytes`  
 [out] Retorna um [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) contendo os bytes de assembly associados à referência de objeto.  
  
 `assemPdb`  
 [out] Retorna um `IEEDataStorage` objeto que contém o símbolo de armazena os dados associados a esta referência.  
  
 `assemLocation`  
 [out] Retorna o local do caminho dessa referência.  
  
 `alr`  
 [out] Retorna um valor da [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md) enumeração que indica o local do assembly dessa referência.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, esse método não é implementado por um avaliador de expressão personalizada.  
  
## <a name="see-also"></a>Consulte também  
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)   
 [ASSEMBLYLOCRESOLUTION](../../../extensibility/debugger/reference/assemblylocresolution.md)

