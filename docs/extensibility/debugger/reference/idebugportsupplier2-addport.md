---
title: IDebugPortSupplier2::AddPort | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 09303ac64d042df0d563f113e3c181d523719554
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49820611"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
Adiciona uma porta.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT AddPort(   
   IDebugPortRequest2* pRequest,  
   IDebugPort2**       ppPort  
);  
```  
  
```csharp  
int AddPort(   
   IDebugPortRequest2 pRequest,  
   out IDebugPort2    ppPort  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRequest`  
 [in] Uma [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) objeto que descreve a porta a ser adicionado.  
  
 `ppPort`  
 [out] Retorna um [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) objeto que representa a porta.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Esse método cria, na verdade, a porta solicitada, bem como adicioná-lo à lista interna do fornecedor de porta de portas ativas. O [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) método pode ser chamado primeiro para evitar possíveis atrasos demorados.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)   
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)   
 [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)   
 [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)