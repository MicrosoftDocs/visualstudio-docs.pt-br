---
title: IActiveScriptProfilerControl2::PrepareProfilerStop | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2::PrepareProfilerStop
ms.assetid: e43a63bc-c44f-44a8-9db4-29062b9e6a16
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 78078cd874be1d7d3d169be2d3d70e65866be3fd
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724516"
---
# <a name="iactivescriptprofilercontrol2prepareprofilerstop"></a>IActiveScriptProfilerControl2::PrepareProfilerStop
Notifica o criador de perfil que você pretende parar criação de perfil em todos os mecanismos de script aplicável. Usando esse método, você pode obter a pilha de chamadas completa se [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] está em execução quando você interromper a criação de perfil.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT PrepareProfilerStop();  
```  
  
#### <a name="parameters"></a>Parâmetros  
 O método não usa nenhum parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um HRESULT. Os valores possíveis são:  
  
|Valor retornado|Significado|  
|------------------|-------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_FAIL`|Não foi possível iniciar a criação de perfil.|  
|`S_FALSE`|Criação de perfil foi interrompida quando um script não estava em execução.|  
|`ACTIVPROF_E_PROFILER_ABSENT`|Criação de perfil não está habilitada.|  
  
## <a name="remarks"></a>Comentários  
 Chamando `IActiveScriptProfilerControl2::PrepareProfilerStop` garante que os eventos para funções na pilha de chamadas são enviados. Esse método deve ser chamado antes de interromper a criação de perfil em qualquer mecanismo de script na guia atual. O método pode ser chamado de qualquer mecanismo de script.  
  
## <a name="see-also"></a>Consulte também  
 [IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)   
 [Interface IActiveScriptProfilerControl2](../../winscript/reference/iactivescriptprofilercontrol2-interface.md)