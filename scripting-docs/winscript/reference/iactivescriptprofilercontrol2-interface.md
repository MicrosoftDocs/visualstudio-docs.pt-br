---
title: Interface IActiveScriptProfilerControl2 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptProfilerControl2 interface
ms.assetid: 89455276-5c23-420b-a7e0-804a32635291
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 9bc0dfa31b37a6bf99427c8eddfe2bd038da9b9d
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24724746"
---
# <a name="iactivescriptprofilercontrol2-interface"></a>Interface IActiveScriptProfilerControl2
Fornece métodos que adiciona a capacidade de iniciar ou interromper a criação de perfil quando um script é executado.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptProfilerControl2::CompleteProfilerStart](../../winscript/reference/iactivescriptprofilercontrol2-completeprofilerstart.md)|Notifica o criador de perfil que você tiver começado a criação de perfil em todos os mecanismos de script aplicável. Isso permite que você obtenha a pilha de chamadas completa se [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] estiver em execução quando você inicia a criação de perfil.|  
|[IActiveScriptProfilerControl2::PrepareProfilerStop](../../winscript/reference/iactivescriptprofilercontrol2-prepareprofilerstop.md)|Notifica o criador de perfil que você pretende parar criação de perfil em todos os mecanismos de script aplicável. Isso permite que você obtenha a pilha de chamadas completa se [!INCLUDE[javascript](../../javascript/includes/javascript-md.md)] está em execução quando você interromper a criação de perfil.|  
  
## <a name="see-also"></a>Consulte também  
 [Interface IActiveScriptProfilerControl](../../winscript/reference/iactivescriptprofilercontrol-interface.md)   
 [Interfaces do criador de perfil de script ativo](../../winscript/reference/active-script-profiler-interfaces.md)