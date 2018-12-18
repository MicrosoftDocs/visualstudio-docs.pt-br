---
title: Interface IDebugSyncOperation | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugSyncOperation interface
ms.assetid: 8d714492-1836-462c-980a-c99e91a2c81b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6705c2aa990aef3cf551a94546bf78a64026cecc
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727006"
---
# <a name="idebugsyncoperation-interface"></a>Interface IDebugSyncOperation
Permite que um mecanismo de script extrair uma operação (por exemplo, a avaliação de expressão) que precisa ser executada enquanto aninhado em um determinado thread bloqueado. A interface também fornece um mecanismo para cancelar operações não responder.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugSyncOperation` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugSyncOperation::GetTargetThread](../../winscript/reference/idebugsyncoperation-gettargetthread.md)|Retorna o thread de aplicativo de destino para esta operação síncrona.|  
|[IDebugSyncOperation::Execute](../../winscript/reference/idebugsyncoperation-execute.md)|Modo síncrono executa a operação e retorna.|  
|[IDebugSyncOperation::InProgressAbort](../../winscript/reference/idebugsyncoperation-inprogressabort.md)|Cancela uma operação em andamento em outro thread.|