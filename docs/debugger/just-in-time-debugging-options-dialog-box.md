---
title: Caixa de diálogo de Just-In-Time, depuração, opções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Debugger.JIT
- vs.debug.options.JIT
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- Just-In-Time debugging, setting options
- Options dialog box, debugging
ms.assetid: 7f11b2e3-3fb5-449d-b07c-6ecf1d6a487d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a6736e0646193754dbd932e5501a6473ee18c7e6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49936323"
---
# <a name="just-in-time-debugging-options-dialog-box"></a>Caixa de diálogo Just-In-Time, Depuração, Opções
Para acessar o **Just-In-Time** página, vá para o **ferramentas** menu e clique em **opções**. No **opções** diálogo caixa, expanda o **depuração** nó e selecione **Just-In-Time**. Essa página permite habilitar a depuração Just-In-Time para o código gerenciado, o código nativo e o script. Para obter mais informações, consulte [depuração Just-in-](../debugger/just-in-time-debugging-in-visual-studio.md).  
  
 Você pode habilitar a depuração Just-In-Time para estes tipos de programa:  
  
- Gerenciado  
  
- Nativo  
  
- script  
  
  A depuração Just-In-Time é uma técnica para depurar um programa que é iniciado fora do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Você pode executar um programa criado no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] fora do ambiente do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]. Se você tiver habilitado a depuração Just-In-Time, uma falha exibirá uma caixa de diálogo que perguntará se você quer depurar.  
  
## <a name="associated-warnings"></a>Avisos associados  
 Quando você visita esta página do **opções** caixa de diálogo, você poderá ver uma mensagem de aviso como esta:  
  
 **Outro depurador se registrou como Just-In-Time depurador. Para reparar, habilite Just-In-Time depurar ou executar o reparo do Visual Studio.**  
  
 Essa mensagem ocorrerá se você tiver outro depurador, possivelmente uma versão anterior do depurador do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], definida como o depurador Just-In-Time.  
  
 Outra mensagem que você pode ver é o seguinte:  
  
 **Just-In-Time depuração detectados erros de registro. Para reparar, habilite Just-In-Time depurar ou executar o reparo do Visual Studio.**  
  
 Se você vir qualquer um desses avisos, depuração com Just-In-Time [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)] requer privilégios de administrador até que você tiver corrigido o problema. Se você tentar habilitar como um não administrador nessas condições, verá a seguinte mensagem de erro:  
  
 **O acesso é negado. Têm um administrador habilitar Just-In-Time de depuração ou repare a instalação do Visual Studio.**  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo depuração, opções](../debugger/debugging-options-dialog-box.md)   
 [Como especificar configurações do depurador](../debugger/how-to-specify-debugger-settings.md)