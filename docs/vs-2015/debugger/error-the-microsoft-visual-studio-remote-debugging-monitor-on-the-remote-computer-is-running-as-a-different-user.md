---
title: 'Erro: O Monitor de depuração remota do Microsoft Visual Studio no computador remoto está sendo executado como um usuário diferente | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- -anyuser option
- anyuser option
- Remote Debugging Monitor
- remote debugging, Remote Debugging Monitor
- msvsmon.exe
ms.assetid: e5b18734-2daf-4c58-b5de-24ae1295703e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2961aed55df241bce3c67eaa4c8630bac1e65f65
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722126"
---
# <a name="error-the-microsoft-visual-studio-remote-debugging-monitor-on-the-remote-computer-is-running-as-a-different-user"></a>Erro: o Monitor de Depuração Remota do Microsoft Visual Studio no computador remoto está sendo executado como um usuário diferente
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao tentar fazer a depuração remota, você pode receber a seguinte mensagem de erro:  
  
 O Monitor de Depuração Remota do Microsoft Visual Studio no computador está sendo executado como um usuário diferente.  
  
## <a name="cause"></a>Causa  
 Essa mensagem ocorre quando você está depurando no modo Sem Autenticação e o usuário que iniciou o msvsmon não é o usuário que está executando o Visual Studio.  
  
## <a name="solution"></a>Solução  
 A solução melhor e mais segura é executar o Monitor de Depuração Remota (msvsmon.exe) na mesma conta de usuário que o Visual Studio. Se você não pode fazer isso, você pode executar o Monitor de depuração remota em outra conta com o **permitir que qualquer usuário depure** opção selecionada no Monitor de depuração remota **opções** caixa de diálogo.  
  
> [!CAUTION]
>  Conceder permissões a outros usuários para se conectar permite a possibilidade de acidentalmente conectar à sessão de depuração remota incorreta. Depuração no **sem autenticação** modo nunca é seguro e deve ser usado com cuidado.  
  
 Para obter mais informações, consulte [iniciar o Monitor de depuração remota](http://msdn.microsoft.com/library/55b60ce7-834b-4e83-a10e-fe4248260a4c).  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)



