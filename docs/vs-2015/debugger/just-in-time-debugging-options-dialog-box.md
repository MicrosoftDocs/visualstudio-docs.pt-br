---
title: Caixa de diálogo de Just-In-Time, depuração, opções | Microsoft Docs
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
- VS.ToolsOptionsPages.Debugger.JIT
- vs.debug.options.JIT
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
- Just-In-Time debugging, setting options
- Options dialog box, debugging
ms.assetid: 7f11b2e3-3fb5-449d-b07c-6ecf1d6a487d
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 06fdd9d12003053ea6d992aa1d7d0fe9ed7144d9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788128"
---
# <a name="just-in-time-debugging-options-dialog-box"></a>Caixa de diálogo Just-In-Time, Depuração, Opções
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para acessar o **Just-In-Time** página, vá para o **ferramentas** menu e clique em **opções**. No **opções** diálogo caixa, expanda o **depuração** nó e selecione **Just-In-Time**. Essa página permite habilitar a depuração Just-In-Time para o código gerenciado, o código nativo e o script. Para obter mais informações, consulte [depuração Just-in-](../debugger/just-in-time-debugging-in-visual-studio.md).  
  
 Você pode habilitar a depuração Just-In-Time para estes tipos de programa:  
  
- Gerenciado  
  
- Nativo  
  
- script  
  
  A depuração Just-In-Time é uma técnica para depurar um programa que é iniciado fora do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Você pode executar um programa criado no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fora do ambiente do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Se você tiver habilitado a depuração Just-In-Time, uma falha exibirá uma caixa de diálogo que perguntará se você quer depurar.  
  
## <a name="associated-warnings"></a>Avisos associados  
 Quando você visita esta página do **opções** caixa de diálogo, você poderá ver uma mensagem de aviso como esta:  
  
 **Outro depurador se registrou como Just-In-Time depurador. Para reparar, habilite Just-In-Time depurar ou executar o reparo do Visual Studio.**  
  
 Essa mensagem ocorrerá se você tiver outro depurador, possivelmente uma versão anterior do depurador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], definida como o depurador Just-In-Time.  
  
 Outra mensagem que você pode ver é o seguinte:  
  
 **Just-In-Time depuração detectados erros de registro. Para reparar, habilite Just-In-Time depurar ou executar o reparo do Visual Studio.**  
  
 Se você vir qualquer um desses avisos, depuração com Just-In-Time [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] requer privilégios de administrador até que você tiver corrigido o problema. Se você tentar habilitar como um não administrador nessas condições, verá a seguinte mensagem de erro:  
  
 **O acesso é negado. Têm um administrador habilitar Just-In-Time de depuração ou repare a instalação do Visual Studio.**  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo depuração, opções](../debugger/debugging-options-dialog-box.md)   
 [Como especificar configurações do depurador](../debugger/how-to-specify-debugger-settings.md)



