---
title: Enviar os eventos necessários | Microsoft Docs
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
- debugging [Debugging SDK], required events
ms.assetid: 08319157-43fb-44a9-9a63-50b919fe1377
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 758f60b5bea17943eae9e55c98db420df2404d5a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51758283"
---
# <a name="sending-the-required-events"></a>Enviando os eventos necessários
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Use este procedimento para o envio de eventos necessários.  
  
## <a name="process-for-sending-required-events"></a>Processo de envio de eventos necessários  
 Os eventos a seguir são necessários, em ordem, quando a criação de uma depuração (DES) do mecanismo e anexá-lo a um programa:  
  
1.  Enviar um [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) o objeto de evento para o Gerenciador de sessão de depuração (SDM) quando o DE é inicializado para um ou mais programas em um processo de depuração.  
  
2.  Quando o programa a ser depurado é anexado ao, envie uma [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) o objeto de evento para o SDM. Esse evento pode ser um evento de interrupção, dependendo do seu design de mecanismo.  
  
3.  Se o programa estiver anexado a quando o processo é iniciado, envie uma [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) o objeto de evento para o SDM para notificar o IDE do novo thread. Esse evento pode ser um evento de interrupção, dependendo do seu design de mecanismo.  
  
4.  Enviar um [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) o objeto de evento para o SDM quando o programa que está sendo depurado está concluído o carregamento ou quando a anexar ao programa seja concluído. Esse evento deve ser um evento de interrupção.  
  
5.  Se o aplicativo a ser depurado é iniciado, envie uma [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) o objeto de evento para o SDM quando a primeira instrução de código na arquitetura de tempo de execução está prestes a ser executada. Esse evento é sempre um evento de interrupção. Quando passo a passo para a sessão de depuração, o IDE para esse evento.  
  
> [!NOTE]
>  Muitas linguagens usam inicializadores globais ou funções externas pré-compilado (da biblioteca CRT ou Main) no início do seu código. Se o idioma do programa que você está depurando contém qualquer um desses tipos de elementos antes do ponto de entrada inicial, em seguida, esse código é executado e o evento de ponto de entrada é enviado quando o usuário ponto de entrada, como **principal** ou `WinMain`, é atingido.  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar um programa para depuração](../../extensibility/debugger/enabling-a-program-to-be-debugged.md)

