---
title: IDebugBinder3::GetEEService | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 982802d1e89434322aba4f5078ceb6dd5a850034
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68193038"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Esse método retorna um serviço solicitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetEEService(  
   [in] GUID        vendor,  
   [in] GUID        language,  
   [in] GUID        iid,  
   [out] IUnknown** ppService  
);  
```  
  
```csharp  
Int GetEEService(  
   Guid       vendor,  
   Guid       language,  
   Guid       iid,  
   out object ppService  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `vendor`  
 [in] `GUID` de um fornecedor (um valor nulo é aceitável).  
  
 `language`  
 [in] `GUID` de uma linguagem (um valor nulo é aceitável).  
  
 `iid`  
 [in] `IID` do serviço a obter.  
  
 `ppService`  
 [out] Uma interface para o serviço solicitado.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Passe o `IID` para o [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md) interface (`IID_IEEVisualizerServiceProvider`) para ver se o serviço Visualizador de tipo está disponível. Se assim, o avaliador de expressão pode obter o [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md) interface para oferecer suporte a visualizadores de tipo. Ver [visualização e exibindo os dados](../../../extensibility/debugger/visualizing-and-viewing-data.md) para obter detalhes.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)   
 [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)   
 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)   
 [Visualizar e exibir dados](../../../extensibility/debugger/visualizing-and-viewing-data.md)
