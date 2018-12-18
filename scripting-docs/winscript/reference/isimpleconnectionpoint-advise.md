---
title: ISimpleConnectionPoint::Advise | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.Advise
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::Advise
ms.assetid: 59ded60d-b938-4110-aca3-e69ba234ca9a
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 7ec43d135401386a3f54f2c047040897f038ba19
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24733786"
---
# <a name="isimpleconnectionpointadvise"></a>ISimpleConnectionPoint::Advise
Estabelece uma conexão entre o objeto de ponto de conexão simples e coletor do cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Advise(  
   IDispatch*  pdisp,  
   DWORD*      pdwCookie  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pdisp`  
 [in] Ponteiro para o `IDispatch` interface no cliente do coletor de aviso. Coletor do cliente recebe as chamadas de saída do ponto de conexão simples.  
  
 `pdwCookie`  
 [out] Ponteiro para um token retornado que identifica exclusivamente essa conexão. O chamador usa esse token posteriormente para excluir a conexão, passando-o para o `ISimpleConnectionPoint::Unadvise` método. Se a conexão não foi estabelecida com êxito, esse valor é zero.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método estabelece uma conexão entre o objeto de ponto de conexão simples e coletor do cliente.  
  
## <a name="see-also"></a>Consulte também  
 [Interface ISimpleConnectionPoint](../../winscript/reference/isimpleconnectionpoint-interface.md)   
 [ISimpleConnectionPoint::Unadvise](../../winscript/reference/isimpleconnectionpoint-unadvise.md)