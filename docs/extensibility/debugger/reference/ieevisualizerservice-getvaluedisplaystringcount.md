---
title: IEEVisualizerService::GetValueDisplayStringCount | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IEEVisualizerService::GetValueDisplayStringCount
- GetValueDisplayStringCount
ms.assetid: d683a833-fbfb-4042-84df-6905124a268a
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 5ef642e48ee4389e48c1141c18a70f9ad5d0b793
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49949663"
---
# <a name="ieevisualizerservicegetvaluedisplaystringcount"></a>IEEVisualizerService::GetValueDisplayStringCount
Recupera o número de cadeias de caracteres a ser exibida para a propriedade especificada ou o campo de valor.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetValueDisplayStringCount (  
   DWORD         displayKind,   
   IDebugField * propertyOrField,   
   ULONG *       pcelt  
);  
```  
  
```csharp  
int GetValueDisplayStringCount (  
   uint        displayKind,   
   IDebugField propertyOrField,   
   out ulong   pcelt  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `displayKind`  
 [in] O valor dos [DisplayKind](../../../extensibility/debugger/reference/displaykind.md) enumeração.  
  
 `propertyOrField`  
 [in] Uma [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) interface que representa uma propriedade ou campo.  
  
 `pcelt`  
 [out] Retorna o número de cadeias de caracteres de valor para exibir.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="see-also"></a>Consulte também  
 [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)