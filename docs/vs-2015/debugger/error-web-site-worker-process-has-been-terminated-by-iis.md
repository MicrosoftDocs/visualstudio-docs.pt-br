---
title: 'Erro: o processo de trabalho do site da Web foi encerrado pelo IIS | Microsoft Docs'
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
- vs.debug.error.web_server_process_terminated
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 5707b972-71a6-4cc6-ab99-c7c00ca8628c
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 93271bcba524054a2289b078b0e92fde115eaf23
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789051"
---
# <a name="error-web-site-worker-process-has-been-terminated-by-iis"></a>Erro: o processo de trabalho do site foi encerrado pelo IIS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

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



