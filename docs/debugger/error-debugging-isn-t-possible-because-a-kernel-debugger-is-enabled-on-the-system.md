---
title: Erro-a depuração não&#39;t possível porque um depurador de kernel está habilitado no sistema | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.kernel_dbg_enabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- kernel debugger
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 80c27ef642697a8514a0809095b980d8c38a47d8
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460859"
---
# <a name="error-debugging-isn39t-possible-because-a-kernel-debugger-is-enabled-on-the-system"></a>Erro: a depuração não&#39;o t possível porque um depurador de kernel está habilitado no sistema
Quando você depura o código gerenciado, talvez receba a seguinte mensagem de erro:

```cmd
Debugging isn't possible because a kernel debugger is enabled on the system
```

 Essa mensagem ocorre quando você tenta depurar o código gerenciado:

- em um sistema do [!INCLUDE[win7](../debugger/includes/win7_md.md)] ou [!INCLUDE[wiprlhext](../debugger/includes/wiprlhext_md.md)]que foi iniciado em modo de depuração.

- o aplicativo usa o CLR versão 2.0, 3.0 ou 3.5.

## <a name="solution"></a>Solução

#### <a name="to-fix-this-problem"></a>Para corrigir esse problema

- Atualizar seu aplicativo para usar a versão 4.0 ou 4.5 do CLR

   — ou —

- Desabilite a depuração de kernel e depure-a no [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

   — ou —

- Depure usando o depurador de kernel em vez do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)].

   — ou —

- No depurador de kernel, desabilite as exceções em modo de usuário.

#### <a name="to-disable-kernel-debugging-in-the-current-session"></a>Para desabilitar a depuração de kernel na sessão atual

- No prompt de comando, digite:

    ```cmd
    Kdbgctrl.exe -d
    ```

#### <a name="to-disable-kernel-debugging-for-all-sessions-windows-vista-and-windows-7"></a>Para desabilitar a depuração de kernel para todas as sessões (Windows Vista e Windows 7)

1. No prompt de comando, digite:

    ```cmd
    bcdedit /debug off
    ```

2. Reinicie o computador.

#### <a name="to-disable-kernel-debugging-for-all-sessions-other-windows-operating-systems"></a>Para desabilitar a depuração de kernel para todas as sessões (outros sistemas operacionais Windows)

1. Localize boot.ini na unidade do sistema (normalmente C:\\). O arquivo boot.ini pode ser ocultado e somente leitura. Portanto, você deve usar o seguinte comando para vê-lo:

    ```cmd
    dir /ASH
    ```

2. Abra o boot.ini usando o Bloco de Notas e remova as seguintes opções:

    ```cmd
    /debug
    /debugport
    /baudrate
    ```

3. Reinicie o computador.

#### <a name="to-debug-with-the-kernel-debugger"></a>Para depurar com o depurador de kernel

1. Se o depurador de kernel estiver associado, você verá uma mensagem que pergunta se quer continuar a depuração. Clique no botão para continuar.

2. Você poderá obter um `User break exception(Int 3).` Se isso ocorrer, digite o seguinte comando do depurador de kernel para continuar a depuração:

     `gn`

## <a name="see-also"></a>Veja também
- [Segurança do depurador](../debugger/debugger-security.md)
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
