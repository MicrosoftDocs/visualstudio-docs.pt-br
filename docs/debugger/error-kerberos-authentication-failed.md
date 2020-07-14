---
title: Erro-falha na autenticação Kerberos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.callback_kerberos_auth_failed
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 07afa4aca82a83f5b7ba64ad0e9958710582a6a0
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460671"
---
# <a name="error-kerberos-authentication-failed"></a>Erro: falha na autenticação Kerberos
Ao tentar fazer a depuração remota, você poderá receber a seguinte mensagem de erro:

```cmd
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos authentication failed.
```

 Esse erro ocorre quando o Monitor de Depuração Remota do Visual Studio está sendo executado sob a conta Serviço de Rede ou Sistema Local. Em uma dessas contas, o depurador remoto deve estabelecer uma conexão de autenticação de Kerberos para se comunicar de volta com o computador host do depurador do Visual Studio.

 A autenticação Kerberos não está disponível nestas condições:

- O computador de destino ou o computador host do depurador está em um grupo de trabalho, em vez de em um domínio

   \- ou –

- Kerberos foi desabilitado no controlador de domínio.

  Se a autenticação Kerberos não estiver disponível, alterar a conta usada para executar o Monitor de Depuração Remota do Visual Studio. Para o procedimento, consulte [erro: o serviço de depurador remoto do Visual Studio no computador de destino não pode se conectar de volta a este computador](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md).

  Se ambos os computadores estiverem conectados ao mesmo domínio e você ainda receber essa mensagem, verifique se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador. Consulte o procedimento a seguir.

### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>Para verificar se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador

1. No computador de destino, abra o menu **Iniciar**, aponte para **Acessórios** e clique em **Prompt de Comando**.

2. Na janela do **prompt de comando** , digite:

    ```cmd
    ping <debugger_host_computer_name>
    ```

3. A primeira linha da resposta `ping` mostra o nome completo do computador e o endereço IP retornados pelo DNS para o computador especificado.

4. No computador host do depurador, abra uma janela de **Prompt de Comando** e execute `ipconfig`.

5. Compare os valores de endereço IP.

## <a name="see-also"></a>Veja também
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Depuração remota](../debugger/remote-debugging.md)
