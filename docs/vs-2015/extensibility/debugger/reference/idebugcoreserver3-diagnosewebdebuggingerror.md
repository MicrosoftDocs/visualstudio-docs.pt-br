---
title: IDebugCoreServer3::DiagnoseWebDebuggingError | Microsoft Docs
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
- IDebugCoreServer3::DiagnoseWebDebuggingError
helpviewer_keywords:
- IDebugCoreServer3::DiagnoseWebDebuggingError
ms.assetid: 8c4570ca-ae55-42f2-bbaa-8d8e75d2fa19
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 67f1d4580d2722c1043c9287cd1eae4c6084dd7f
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51736324"
---
# <a name="idebugcoreserver3diagnosewebdebuggingerror"></a>IDebugCoreServer3::DiagnoseWebDebuggingError
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Falha nas tentativas de determinar o motivo pelo qual um auto-attach.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT DiagnoseWebDebuggingError(  
   LPCWSTR pszUrl  
);  
```  
  
```csharp  
int DiagnoseWebDebuggingError(  
   string pszUrl  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pszUrl`  
 [in] Não usado no momento; sempre deve ser definido como um valor nulo.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. Estes são os outros códigos de retorno típicos:  
  
|Código|Descrição|  
|----------|-----------------|  
|`S_WEBDBG_UNABLE_TO_DIAGNOSE`|Não é possível determinar o motivo de falha de servidor remoto iniciar a depuração.|  
|`S_WEBDBG_DEBUG_VERB_BLOCKED`|Não é possível depurar em um servidor remoto, possivelmente devido a permissões insuficientes ou porque o verbo DEBUG não está habilitado.|  
|`E_WEBDBG_DEBUG_VERB_BLOCKED`|O servidor web foi bloqueado e está bloqueando o verbo DEBUG, que é necessário para habilitar a depuração.|  
  
## <a name="see-also"></a>Consulte também  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)

