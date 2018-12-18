---
title: IDebugCoreServer2::GetMachineUtilities_V7 | Microsoft Docs
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
- IDebugCoreServer2::GetMachineUtilities_V7
helpviewer_keywords:
- IDebugCoreServer2::GetMachineUtilities_V7
ms.assetid: 64c1f08f-853b-4498-9810-29791581ef2f
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 2e9c35354a9325854a3b30fbb0fc64a59989796d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779379"
---
# <a name="idebugcoreserver2getmachineutilitiesv7"></a>IDebugCoreServer2::GetMachineUtilities_V7
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método obtém os utilitários de máquina para um servidor.  
  
> [!NOTE]
>  Este método é obsoleto: não use ([!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] sempre retorna `E_NOTIMPL` se esse método é chamado). Ele é retido por razões históricas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetMachineUtilities_V7(  
   IDebugMDMUtil2_V7** ppUtil  
);  
```  
  
```csharp  
int GetMachineUtilities_V7(  
   out IDebugMDMUtil2_V7 ppUtil  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppUtil`  
 [out] Retorna um `IDebugMDMUtil2_V7` interface que representa as informações de utilitários do computador.  
  
## <a name="return-value"></a>Valor de retorno  
 Sempre retorna `E_NOTIMPL`, indicando que o método não está implementado.  
  
## <a name="remarks"></a>Comentários  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] sempre retorna `E_NOTIMPL` se esse método é chamado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCoreServer2](../../../extensibility/debugger/reference/idebugcoreserver2.md)

