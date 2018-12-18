---
title: Interface IDebugThreadCall | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugThreadCall interface
ms.assetid: 9a9a9892-f310-4ef3-8db2-4f868be52d7e
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8b2b1b500aec08520166d9092edfa6a58c1df0fa
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726936"
---
# <a name="idebugthreadcall-interface"></a>Interface IDebugThreadCall
O `IDebugThreadCall` interface costuma ser implementada por um componente que faz chamadas entre threads com a `IDebugThread` marshalling de implementação fornecida pelo Gerenciador de depuração do processo (PDM).  
  
 As chamadas PDM o `IDebugThreadCall` interface no thread desejado e o `IDebugThreadCall` interface envia a chamada para a implementação desejada. O `IDebugThreadCall` interface converte as informações do parâmetro passadas nos parâmetros para a parte superior apropriada.  
  
 O `IDebugThreadCall` interface é um objeto free-thread.  
  
## <a name="methods"></a>Métodos  
 Além dos métodos herdados de `IUnknown`, o `IDebugThreadCall` interface expõe os métodos a seguir.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugThreadCall::ThreadCallHandler](../../winscript/reference/idebugthreadcall-threadcallhandler.md)|Lida com chamadas para executar código em outro thread.|