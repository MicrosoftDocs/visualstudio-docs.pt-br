---
title: IDebugExpressionEvaluator2::GetService | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IDebugExpressionEvaluator2::GetService
- GetService
ms.assetid: f8988a9e-9d18-42af-84a7-55f41e9adf63
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 3c79663e8c274020f7e997bd638c3ae5b16ca874
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844803"
---
# <a name="idebugexpressionevaluator2getservice"></a>IDebugExpressionEvaluator2::GetService
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Recupera um objeto de serviço recebe seu identificador exclusivo.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT GetService (  
   GUID        uid,  
   IUnknown ** ppService  
);  
```  
  
```csharp  
int GetService (  
   Guid       uid,  
   out object ppService  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `uid`  
 [in] Identificador exclusivo do serviço a ser recuperado.  
  
 `ppService`  
 [out] Retorna um objeto que representa o serviço.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Isso pode ser consumido por um avaliador de expressão de terceiros para obter serviços de outro avaliador de expressão. Por exemplo, esse método pode ser usado para obter a interface para o serviço de visualização simultânea do avaliador de expressão padrão. Avaliadores de expressão de terceiros provavelmente não precisará implementar essa interface.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugExpressionEvaluator2](../../../extensibility/debugger/reference/idebugexpressionevaluator2.md)

