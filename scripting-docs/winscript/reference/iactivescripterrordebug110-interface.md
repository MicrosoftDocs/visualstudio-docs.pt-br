---
title: Interface IActiveScriptErrorDebug110 | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptErrorDebug110 Interface
ms.assetid: 5c1a4993-4cad-4ccf-89c2-53abfddfe1f2
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 152f12154acc59b88fc8b1c9a176ac87a5da847d
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24645756"
---
# <a name="iactivescripterrordebug110-interface"></a>Interface IActiveScriptErrorDebug110
Adiciona a funcionalidade para o [IActiveScriptDebug Interface](../../winscript/reference/iactivescriptdebug-interface.md). Esta interface é implementada pelo mecanismo JavaScript para determinar o porquê de um evento BREAKREASON_ERROR ter ocorrido.  
  
> [!IMPORTANT]
>  Esta interface é implementada pelo PDM v11.0 e superiores. Localizado em. activdbg100.h.  
  
## <a name="methods"></a>Métodos  
 A interface `IActiveScriptErrorDebug110` expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptErrorDebug110::GetExceptionThrownKind](../../winscript/reference/iactivescripterrordebug110-getexceptionthrownkind.md)|Retorna o tipo de exceção para uma exceção gerada.|