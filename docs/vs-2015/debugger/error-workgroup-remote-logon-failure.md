---
title: 'Erro: Falha no Logon remoto do grupo de trabalho | Microsoft Docs'
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
- vs.debug.error.workgroup_remote_logon_failure
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
- logon failure, remote debugging
- remote debugging, logon failure
ms.assetid: 7be2c5bb-40fe-48d6-8cfc-c231fbd3d64e
caps.latest.revision: 22
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b13531d3a9dd5249b0c96ddc4e8f736c20696303
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51723655"
---
# <a name="error-workgroup-remote-logon-failure"></a>Erro: falha no logon remoto do grupo de trabalho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este erro é:  
  
 Falha de logon: usuário desconhecido ou senha inválida  
  
 **Causa**  
  
 Esse erro pode ocorrer quando você está depurando de um computador em um grupo de trabalho e tentar se conectar ao computador remoto. Possíveis causas incluem:  
  
-   Não há nenhuma conta com o nome e a senha correspondentes no computador remoto.  
  
-   Se o computador do Visual Studio e o computador remoto estiverem em grupos de trabalho, esse erro pode ocorrer devido ao padrão **política de segurança Local** configuração no computador remoto. A configuração padrão para o **política de segurança Local** configuração é **somente convidados - usuários locais são autenticados como convidado**. Para depurar nessa configuração, você deve alterar a configuração no computador remoto para **Clássico - os usuários locais são autenticados como eles próprios**.  
  
> [!NOTE]
>  Você deve ser administrador para realizar as seguintes tarefas.  
  
### <a name="to-open-the-local-security-policy-window"></a>Para abrir a janela Política de Segurança Local  
  
1.  Iniciar o **secpol. msc** snap-in do Console de gerenciamento Microsoft. Digite secpol.msc na pesquisa do Windows, na caixa de execução do Windows ou em um prompt de comando.  
  
### <a name="to-add-user-rights-assignments"></a>Para adicionar atribuições de direitos de usuário  
  
1.  Abra o local  
  
2.  Abra o **política de segurança Local** janela.  
  
3.  Expanda o **diretivas locais** pasta.  
  
4.  Clique em **atribuição de direitos do usuário**.  
  
5.  No **diretiva** coluna, clique duas vezes em **depurar programas** para exibir as atribuições de política de grupo local atual no **configuração de política de segurança Local** caixa de diálogo.  
  
     ![Direitos de usuário de política de segurança local](../debugger/media/dbg-err-localsecuritypolicy-userrightsdebugprograms.png "DBG_ERR_LocalSecurityPolicy_UserRightsDebugPrograms")  
  
6.  Para adicionar novos usuários, clique o **adicionar usuário ou grupo** botão.  
  
### <a name="to-change-the-sharing-and-security-model"></a>Para alterar o Modelo de Compartilhamento e Segurança  
  
1.  Abra o **política de segurança Local** janela.  
  
2.  Expanda o **diretivas locais** pasta.  
  
3.  Clique em **opções de segurança**.  
  
4.  No **diretiva** coluna, clique duas vezes em **acesso à rede: modelo de compartilhamento e segurança para contas locais**.  
  
5.  No **acesso à rede: modelo de compartilhamento e segurança para contas locais** caixa de diálogo, altere o valor a ser **Clássico - os usuários locais são autenticados como eles próprios** e clique no **aplicar**botão.  
  
     ![Opções de segurança da política de segurança local](../debugger/media/dbg-err-localsecuritypolicy-securityoptions-networkaccess.png "DBG_ERR_LocalSecurityPolicy_SecurityOptions_NetworkAccess")  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)



