---
title: Interface IDebugAsyncOperation | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugAsyncOperation interface
ms.assetid: ebb2ea75-1443-4d8a-812d-171a166f5f9d
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 157ed1248535855fcb53ca2eb6f49427fea94149
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726096"
---
# <a name="idebugasyncoperation-interface"></a>Interface IDebugAsyncOperation
O processo de depuração Manager implementa o `IDebugAsyncOperation` interface. Um mecanismo de linguagem chama o `IDebugApplication::CreateAsyncDebugOperation` método para obter uma referência a esta interface. O mecanismo de linguagem pode usar o `IDebugAsyncOperation` interface para fornecer acesso assíncrono a uma operação síncrona de depuração.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugAsyncOperation` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugAsyncOperation::GetSyncDebugOperation](../../winscript/reference/idebugasyncoperation-getsyncdebugoperation.md)|Retorna a operação síncrona depuração associada a este objeto.|  
|[IDebugAsyncOperation::Start](../../winscript/reference/idebugasyncoperation-start.md)|Faz com que a operação assíncrona começar.|  
|[IDebugAsyncOperation::Abort](../../winscript/reference/idebugasyncoperation-abort.md)|Cancela uma operação.|  
|[IDebugAsyncOperation::QueryIsComplete](../../winscript/reference/idebugasyncoperation-queryiscomplete.md)|Determina se a operação de depuração foi concluída.|  
|[IDebugAsyncOperation::GetResult](../../winscript/reference/idebugasyncoperation-getresult.md)|Fornece o valor de retorno e parâmetro de objeto de retorno da operação síncrona de depuração.|