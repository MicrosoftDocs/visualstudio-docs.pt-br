---
title: Anexo com base em Iniciar | Microsoft Docs
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
- debug engines, launching
- debug engines, attaching to programs
ms.assetid: 362f00ac-1909-4a3a-bacb-c0ceb5549816
caps.latest.revision: 9
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 1c3d361d9e8b99467e0a8a131e9d30be5db30b9d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792444"
---
# <a name="launch-based-attachment"></a>Anexo baseado em inicialização
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Com base em inicialização anexo a um programa é automático. Quando o processo que hospeda o programa é iniciado pelo SDM, anexo com base em inicialização segue um caminho semelhante do método manual de anexo. Para obter informações, consulte [anexar ao programa](../../extensibility/debugger/attaching-to-the-program.md).  
  
## <a name="the-attaching-process"></a>O processo de anexar  
 A principal diferença é a sequência de eventos a seguir a **Attach** chamar, da seguinte maneira:  
  
1.  Enviar um **IDebugEngineCreateEvent2** o objeto de evento para o SDM. Para obter detalhes, consulte [enviando eventos](../../extensibility/debugger/sending-events.md).  
  
2.  Chame o `IDebugProgram2::GetProgramId` método na **IDebugProgram2** interface é passada para o **Attach** método.  
  
3.  Enviar um **IDebugProgramCreateEvent2** objeto de evento para notificar o SDM que local **IDebugProgram2** objeto foi criado para representar o programa para a Alemanha.  
  
4.  Enviar um [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) o objeto de evento para notificar o SDM que um novo thread é criado para o processo que o iniciou.  
  
## <a name="see-also"></a>Consulte também  
 [Enviar os eventos necessários](../../extensibility/debugger/sending-the-required-events.md)   
 [Habilitar um programa para depuração](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)

