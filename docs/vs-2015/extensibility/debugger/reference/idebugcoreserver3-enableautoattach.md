---
title: IDebugCoreServer3::EnableAutoAttach | Microsoft Docs
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
- IDebugCoreServer3::EnableAutoAttach
helpviewer_keywords:
- IDebugCoreServer3::EnableAutoAttach
ms.assetid: 06aa633b-263b-4e08-8844-9a52d5120b94
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0823c64e150d306d4613a8df797f11c0785ba762
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774491"
---
# <a name="idebugcoreserver3enableautoattach"></a>IDebugCoreServer3::EnableAutoAttach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Permite que a anexação automática para os mecanismos de depuração especificada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT EnableAutoAttach(  
   GUID*     rgguidSpecificEngines,  
   DWORD     celtSpecificEngines,  
   LPCOLESTR pszStartPageUrl,  
   BSTR*     pbstrSessionId  
);  
```  
  
```csharp  
int EnableAutoAttach(  
   Guid[]     rgguidSpecificEngines,  
   uint       celtSpecificEngines,  
   string     pszStartPageUrl,  
   out string pbstrSessionId  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `rgguidSpecificEngines`  
 [in] Matriz de GUIDs para cada mecanismo de depuração para marcar como anexação automática.  
  
 `celtSpecificEngines`  
 [in] O número de mecanismos especificado em `rgguidSpecificEngines`.  
  
 `pszStartPageUrl`  
 [in] A URL inicial para usar ao anexar a automática.  
  
 `pbstrSessionID`  
 [out] ID da sessão que foi anexado automaticamente.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará o código de erro. Um código de erro é `E_AUTO_ATTACH_NOT_REGISTERED`, que indica se a fábrica de classes auto-attach não foi registrada.  
  
## <a name="remarks"></a>Comentários  
 Quando um programa associado com a URL especificada é iniciado, os mecanismos de depuração especificada são iniciados automaticamente e anexados.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)

