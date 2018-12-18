---
title: IDebugStopCompleteEvent2 | Microsoft Docs
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
- IDebugStopCompleteEvent2 interface
ms.assetid: ff3e89f4-61bb-489d-901c-447260100218
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: b64c9719c6d2975829451dbf11cf584f98805c1b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780471"
---
# <a name="idebugstopcompleteevent2"></a>IDebugStopCompleteEvent2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

O mecanismo de depuração (DES) pode enviar esse evento opcional para o Gerenciador de sessão de depuração (SDM) quando um programa foi interrompido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
IDebugStopCompleteEvent2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>Observações para implementadores  
 Isso é uma nova interface para [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)]. Versões anteriores não dava suporte assíncrono parando.  
  
 [Parar](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) é chamado pelo SDM em vários processos ou um programas com vários cenários. Quando um programa envia um evento de interrupção para o SDM, o SDM solicita parar, muito de outros programas.  
  
 Ele é usado para informar assincronamente o SDM que um programa foi interrompido. Isso é útil para um mecanismo de depuração do interpretador, às vezes, em que nenhum código é executado dentro do programa depurado, portanto [parar](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) não pode ser concluída de forma síncrona. Se um mecanismo de depuração deseja empregar essa notificação assíncrona, ela deve retornar `S_ASYNC_STOP` partir [parar](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

