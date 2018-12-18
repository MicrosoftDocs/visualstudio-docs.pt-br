---
title: 'Erro: Falha de autenticação Kerberos | Microsoft Docs'
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
- vs.debug.error.callback_kerberos_auth_failed
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c18053f9-9074-4bc3-a8bf-13e4acbea921
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2ec03ae3d3b64435877b51996cb84a1768cc4a42
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51732342"
---
# <a name="error-kerberos-authentication-failed"></a>Erro: falha na autenticação Kerberos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao tentar fazer a depuração remota, você poderá receber a seguinte mensagem de erro:  
  
```  
Error: The Visual Studio Remote Debugger on the target computer cannot connect back to this computer. Kerberos auythentication failed.  
```  
  
 Esse erro ocorre quando o Monitor de Depuração Remota do Visual Studio está sendo executado sob a conta Serviço de Rede ou Sistema Local. Em uma dessas contas, o depurador remoto deve estabelecer uma conexão de autenticação de Kerberos para se comunicar de volta com o computador host do depurador do Visual Studio.  
  
 A autenticação Kerberos não está disponível nestas condições:  
  
- O computador de destino ou o computador host do depurador está em um grupo de trabalho, em vez de em um domínio  
  
   \- ou -  
  
- Kerberos foi desabilitado no controlador de domínio.  
  
  Se a autenticação Kerberos não estiver disponível, alterar a conta usada para executar o Monitor de Depuração Remota do Visual Studio. Para o procedimento, consulte [erro: serviço de depurador remoto a do Visual Studio no computador de destino não pode se reconectar a este computador](../debugger/error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer.md).  
  
  Se ambos os computadores estiverem conectados ao mesmo domínio e você ainda receber essa mensagem, verifique se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador. Consulte o procedimento a seguir.  
  
### <a name="to-verify-that-dns-on-the-target-computer-is-correctly-resolving-the-debugger-host-computer-name"></a>Para verificar se o DNS no computador de destino está resolvendo corretamente o nome do computador host do depurador  
  
1.  No computador de destino, abra o **inicie** , aponte para **Acessórios** e, em seguida, clique em **Prompt de comando**.  
  
2.  No **Prompt de comando** , digite:  
  
    ```  
    ping <debugger_host_computer_name>  
    ```  
  
3.  A primeira linha da resposta `ping` mostra o nome completo do computador e o endereço IP retornados pelo DNS para o computador especificado.  
  
4.  No computador de host do depurador, abra uma **Prompt de comando** e execute `ipconfig`.  
  
5.  Compare os valores de endereço IP.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)



