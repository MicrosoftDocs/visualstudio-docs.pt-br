---
title: 'Erro: o processo de trabalho do site da Web foi encerrado pelo IIS | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.web_server_process_terminated
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 582cf1b5faf0cc62d85e17544aa03c4ede4ab0a8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49852837"
---
# <a name="error-web-site-worker-process-has-been-terminated-by-iis"></a>Erro: o processo de trabalho do site foi encerrado pelo IIS
O depurador interrompeu a execução de código no site. Isso fez o IIS (Serviços de Informações da Internet) supor que o processo de trabalho parou de responder. Consequentemente, o IIS terminou o processo de trabalho.  
  
 Para retomar a depuração, será necessário configurar o IIS para permitir que o processo de trabalho continue. Essa mensagem de erro não aparece em versões do IIS que são anteriores ao IIS 7.  
  
### <a name="to-configure-iis-7-to-allow-the-worker-process-to-continue"></a>Para configurar o IIS 7 para permitir que o processo de trabalho continue  
  
1. Abra o **ferramentas administrativas** janela.  
  
   1.  Clique em **inicie**e, em seguida, escolha **painel de controle**.  
  
   2.  Na **painel de controle**, escolha **alterne para modo de exibição clássico**, se necessário e, em seguida, clique duas vezes em **ferramentas administrativas**.  
  
2. No **ferramentas administrativas** janela, clique duas vezes em **serviços de informações da Internet (IIS) Manager**.  
  
    O Gerenciador do IIS é aberto.  
  
3. No **conexões** painel, expanda o \<nome do computador > nó se necessário.  
  
4. Sob o \<nome do computador > nó, clique em **Pools de aplicativos**.  
  
5. No **Pools de aplicativos** lista, clique no nome do seu aplicativo é executado no pool e, em seguida, clique em **configurações avançadas**.  
  
6. No **configurações avançadas** diálogo caixa, localize a **modelo de processo** seção e execute uma das seguintes ações:  
  
   - Definir **Ping habilitado** à **falso**.  
  
   - Definir **tempo de resposta máximo de Ping** para um valor maior que 90 segundos.  
  
     Definindo **Ping habilitado** à **falso** impede que o IIS verificando se o processo de trabalho ainda está em execução e mantém o processo de trabalho ativo até que você interrompa o processo depurado. Definindo **tempo de resposta máximo de Ping** com um valor grande permite que o IIS continue monitorando o processo de trabalho.  
  
7. Clique em **Okey** para fechar o **configurações avançadas** caixa de diálogo.  
  
8. Feche o Gerenciador do IIS e o **ferramentas administrativas** janela.  
  
## <a name="see-also"></a>Consulte também  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)