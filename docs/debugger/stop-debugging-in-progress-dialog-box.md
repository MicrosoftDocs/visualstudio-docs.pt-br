---
title: Parar a depuração na caixa de diálogo de progresso | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.stopnow
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- Stop Debugging in Progress dialog box
ms.assetid: ed7ef49d-e25f-4a4d-9396-9bc7b4143117
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3a6e13967cc18fae8d837cc71ea8a91c60f2b1bb
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44281189"
---
# <a name="stop-debugging-in-progress-dialog-box"></a>Caixa de diálogo Parar Depuração em Andamento
Essa caixa de diálogo aparece quando o depurador está tentando interromper uma sessão de depuração, mas parar a sessão deve demorar um pouco. Parar uma sessão de depuração normalmente é muito rápido e essa caixa de diálogo não é exibida. Entretanto, às vezes, leva mais tempo para desanexar de todos os processos que estão sendo depurados. Se parar a sessão levar mais do que alguns segundos (ou se ocorrer um erro de desanexação), essa caixa de diálogo será exibida. Se isso ocorrer com frequência, poderá ser devido a um problema interno e você deverá entrar em contato com o Product Support Services.  
  
 Você pode esperar os processos desanexarem e essa caixa de diálogo desaparecer ou usar o **parar agora** botão para forçar o encerramento imediato.  
  
 **Parar agora**  
 Clique neste botão para encerrar imediatamente a sessão de depuração. Usando o **parar agora** encerrará em vez de desanexar os processos que estão sendo depurados. Se você estiver depurando processos do sistema, encerrar os processos com **parar agora** pode ter efeitos inesperados e indesejados.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Desanexação de programas](/previous-versions/visualstudio/visual-studio-2010/x1thkxez(v=vs.100))