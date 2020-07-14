---
title: Erro-o processo de trabalho do site da Web foi encerrado pelo IIS | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.web_server_process_terminated
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
ms.openlocfilehash: 6d61f124d906137557b17b81122eba34e471a1a4
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85459994"
---
# <a name="error-web-site-worker-process-has-been-terminated-by-iis"></a>Erro: o processo de trabalho do site foi encerrado pelo IIS
O depurador interrompeu a execução de código no site. Isso fez o IIS (Serviços de Informações da Internet) supor que o processo de trabalho parou de responder. Consequentemente, o IIS terminou o processo de trabalho.

 Para retomar a depuração, será necessário configurar o IIS para permitir que o processo de trabalho continue. Essa mensagem de erro não aparece em versões do IIS que são anteriores ao IIS 7.

### <a name="to-configure-iis-7-to-allow-the-worker-process-to-continue"></a>Para configurar o IIS 7 para permitir que o processo de trabalho continue

1. Abra a janela **Ferramentas Administrativas**.

   1. Clique em **Iniciar**e escolha **painel de controle**.

   2. No **painel de controle**, escolha **alternar para exibição clássica**, se necessário, e clique duas vezes em **Ferramentas administrativas**.

2. Na janela **Ferramentas Administrativas**, clique duas vezes em **Serviços de Informações da Internet (IIS)**.

    O Gerenciador do IIS é aberto.

3. No painel **conexões** , expanda o \<computer name> nó, se necessário.

4. No \<computer name> nó, clique em **pools de aplicativos**.

5. Na lista **Pools de Aplicativos**, clique com o botão direito do mouse no nome do pool no qual seu aplicativo está sendo executado e clique em **Configurações Avançadas**.

6. Na caixa de diálogo **Configurações Avançadas**, localize a seção **Modelo de Processo** e execute uma das seguintes ações:

   - Defina **Ping Habilitado** como **False**.

   - Defina **Tempo de Resposta Máximo de Ping** com um valor maior do que 90 segundos.

     Configurar **Ping Habilitado** como **False** impede que o IIS verifique se o processo de trabalho ainda está em execução e mantém o processo de trabalho ativo até que você pare o processo depurado. Configurar **Tempo de Resposta Máximo de Ping** com um valor grande permite que o IIS continue monitorando o processo de trabalho.

7. Clique em **OK** para fechar a caixa de diálogo **Configurações Avançadas** .

8. Feche o Gerenciador do IIS e a janela **Ferramentas Administrativas**.

## <a name="see-also"></a>Veja também
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)