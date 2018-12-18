---
title: 'Aviso de segurança: Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou se você não tiver certeza, não anexe a esse processo | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.attachsecuritywarning
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 52246c1e-a371-40a0-b756-a435cc51876f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 68d88e01dde07789467272db830cae45ca5d60c4
ms.sourcegitcommit: eefffa7ebe339d1297cdc12f51a813e7849d7e95
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2018
ms.locfileid: "34178002"
---
# <a name="security-warning-attaching-to-a-process-owned-by-an-untrusted-user-can-be-dangerous-if-the-following-information-looks-suspicious-or-you-are-unsure-do-not-attach-to-this-process"></a>Aviso de segurança: Anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou se você não tiver certeza, não anexe a esse processo
Essa caixa de diálogo de aviso é exibida quando você anexa a um processo que contém o código parcialmente confiável ou seja de propriedade de um usuário não confiável imediatamente antes de ocorrer a anexação. Um processo não confiável que contém o código mal-intencionado tem o potencial de danificar o computador que faz a depuração. Se você tiver motivo desconfiar o processo, você deve clicar em **Cancelar** para evitar a depuração.  
  
 Para suprimir este aviso durante a depuração de um cenário legítimo, feche o Visual Studio e defina o valor dessa chave do registro como 1: `HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\<version>\Debugger\DisableAttachSecurityWarning`e, em seguida, reinicie o Visual Studio. Depois de concluir a depurar do cenário, redefina o valor como 0 e reinicie o Visual Studio.  
  
 Os “Usuários confiáveis” incluem você, mais um conjunto de usuários padrão que são definidos normalmente em computadores que têm o .NET Framework instalado, por exemplo, `aspnet`, `localsystem`, `networkservice` e `localservice`.  
  
## <a name="uielement-list"></a>Lista UIElement  
 Nome  
 Nome do assembly solicitado para depurar  
  
 User  
 Usuário atual  
  
 Attach  
 Pressione para continuar a depurar anexando  
  
 Não anexar  
 Não anexar ao processo  
  
## <a name="see-also"></a>Consulte também  
 [Anexar a processos em execução](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)   
 [Segurança do depurador](../debugger/debugger-security.md)