---
title: 'Erro: A depuração não é&#39;t possível porque um depurador de Kernel está habilitado no sistema | Microsoft Docs'
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
- vs.debug.error.kernel_dbg_enabled
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
- CSharp
- C++
helpviewer_keywords:
- kernel debugger
ms.assetid: 630a7abd-3303-4aaa-888a-6de3de14bc01
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: eea2e7d8277bc67df75be3d05d907a8bd13c29c5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725281"
---
# <a name="error-debugging-isn39t-possible-because-a-kernel-debugger-is-enabled-on-the-system"></a>Erro: A depuração não é&#39;t possível porque um depurador de Kernel está habilitado no sistema
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você depura o código gerenciado, talvez receba a seguinte mensagem de erro:  
  
```  
Debugging isn't possible because a kernel debugger is enabled on the system  
```  
  
 Essa mensagem ocorre quando você tenta depurar o código gerenciado:  
  
-   em um sistema do [!INCLUDE[win7](../includes/win7-md.md)] ou [!INCLUDE[wiprlhext](../includes/wiprlhext-md.md)]que foi iniciado em modo de depuração.  
  
-   o aplicativo usa o CLR versão 2.0, 3.0 ou 3.5.  
  
## <a name="solution"></a>Solução  
  
#### <a name="to-fix-this-problem"></a>Para corrigir esse problema  
  
-   Atualizar seu aplicativo para usar a versão 4.0 ou 4.5 do CLR  
  
     —ou—  
  
-   Desabilite a depuração de kernel e depure-a no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
     —ou—  
  
-   Depure usando o depurador de kernel em vez do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
     —ou—  
  
-   No depurador de kernel, desabilite as exceções em modo de usuário.  
  
#### <a name="to-disable-kernel-debugging-in-the-current-session"></a>Para desabilitar a depuração de kernel na sessão atual  
  
-   No prompt de comando, digite:  
  
    ```  
    Kdbgctrl.exe -d  
    ```  
  
#### <a name="to-disable-kernel-debugging-for-all-sessions-windows-vista-and-windows-7"></a>Para desabilitar a depuração de kernel para todas as sessões (Windows Vista e Windows 7)  
  
1.  No prompt de comando, digite:  
  
    ```  
    bcdedit /debug off   
    ```  
  
2.  Reinicie o computador.  
  
#### <a name="to-disable-kernel-debugging-for-all-sessions-other-windows-operating-systems"></a>Para desabilitar a depuração de kernel para todas as sessões (outros sistemas operacionais Windows)  
  
1.  Localize Boot. ini na unidade do sistema (normalmente c:\\). O arquivo boot.ini pode ser ocultado e somente leitura. Portanto, você deve usar o seguinte comando para vê-lo:  
  
    ```  
    dir /ASH  
    ```  
  
2.  Abra o boot.ini usando o Bloco de Notas e remova as seguintes opções:  
  
    ```  
    /debug  
    /debugport  
    /baudrate  
    ```  
  
3.  Reinicie o computador.  
  
#### <a name="to-debug-with-the-kernel-debugger"></a>Para depurar com o depurador de kernel  
  
1.  Se o depurador de kernel estiver associado, você verá uma mensagem que pergunta se quer continuar a depuração. Clique no botão para continuar.  
  
2.  Você poderá obter um `User break exception(Int 3).` Se isso ocorrer, digite o seguinte comando do depurador de kernel para continuar a depuração:  
  
     `gn`  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)



