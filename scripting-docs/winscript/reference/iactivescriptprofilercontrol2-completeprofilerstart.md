---
title: IActiveScriptProfilerControl2::CompleteProfilerStart | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::CompleteProfilerStart
ms.assetid: e14d94a2-39d3-40a1-84d9-6300fbe2b339
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 5abd4ee4237991714bfe3d8ba21b083f1a1920cd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724496"
---
# <a name="iactivescriptprofilercontrol2completeprofilerstart"></a>IActiveScriptProfilerControl2::CompleteProfilerStart
Notifica o criador de perfil que você tiver começado a criação de perfil em todos os mecanismos de script aplicável. Usando esse método, você pode obter a pilha de chamadas completa se [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] estiver em execução quando você inicia a criação de perfil.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CompleteProfilerStart();  
```  
  
#### <a name="parameters"></a>Parâmetros  
 O método não usa nenhum parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um HRESULT. Os valores possíveis são:  
  
|Valor retornado|Significado|  
|------------------|-------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_FAIL`|Criação de perfil não pode ser iniciada.|  
|`S_FALSE`|Criação de perfil foi iniciada quando um script não estava em execução.|  
|`ACTIVPROF_E_PROFILER_ABSENT`|Criação de perfil não está habilitada. Nenhum retorno de chamada já foi definido.|  
|`E_OUTOFMEMORY`|Não é possível obter a pilha de chamadas devido à falta de memória.|  
  
## <a name="remarks"></a>Comentários  
 Chamando `IActiveScriptProfilerControl2::CompleteProfilerStart` garante que os eventos para funções já na pilha de chamadas são enviados. Esse método deve ser chamado após a criação de perfil iniciado em qualquer mecanismo de script na guia atual. O método pode ser chamado de qualquer mecanismo de script.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)   
 [Interface IActiveScriptProfilerControl2](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)