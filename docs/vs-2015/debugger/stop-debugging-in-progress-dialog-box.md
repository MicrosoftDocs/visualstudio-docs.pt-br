---
title: Parar a depuração na caixa de diálogo de progresso | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.stopnow
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- Stop Debugging in Progress dialog box
ms.assetid: ed7ef49d-e25f-4a4d-9396-9bc7b4143117
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2dba046c57e7b3990b3bf31994da699bed1e6442
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51792275"
---
# <a name="stop-debugging-in-progress-dialog-box"></a>Caixa de diálogo Parar Depuração em Andamento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Essa caixa de diálogo aparece quando o depurador está tentando interromper uma sessão de depuração, mas parar a sessão deve demorar um pouco. Parar uma sessão de depuração normalmente é muito rápido e essa caixa de diálogo não é exibida. Entretanto, às vezes, leva mais tempo para desanexar de todos os processos que estão sendo depurados. Se parar a sessão levar mais do que alguns segundos (ou se ocorrer um erro de desanexação), essa caixa de diálogo será exibida. Se isso ocorrer com frequência, poderá ser devido a um problema interno e você deverá entrar em contato com o Product Support Services.  
  
 Você pode esperar os processos desanexarem e essa caixa de diálogo desaparecer ou usar o **parar agora** botão para forçar o encerramento imediato.  
  
 **Parar agora**  
 Clique neste botão para encerrar imediatamente a sessão de depuração. Usando o **parar agora**encerrará em vez de desanexar os processos que estão sendo depurados. Se você estiver depurando processos do sistema, encerrar os processos com **parar agora** pode ter efeitos inesperados e indesejados.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Desanexação de programas](http://msdn.microsoft.com/en-us/f2c756c2-8079-474b-94c2-01c19a141a01)



