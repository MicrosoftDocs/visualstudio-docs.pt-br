---
title: 'Erro: Falha no Logon remoto de grupo de trabalho | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.workgroup_remote_logon_failure
dev_langs:
- CSharp
- VB
- FSharp
- JScript
- C++
helpviewer_keywords:
- logon failure, remote debugging
- remote debugging, logon failure
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 60cee4e6bdb4ebab925325695eb9ad6813929879
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31481990"
---
# <a name="error-workgroup-remote-logon-failure"></a>Erro: falha no logon remoto do grupo de trabalho
Este erro é:  
  
 Falha de logon: usuário desconhecido ou senha inválida  
  
 **Causa**  
  
 Esse erro pode ocorrer quando você está depurando de um computador em um grupo de trabalho e tentar se conectar ao computador remoto. Possíveis causas incluem:  
  
-   Não há nenhuma conta com o nome e a senha correspondentes no computador remoto.  
  
-   Se o computador do Visual Studio e o computador remoto estão em grupos de trabalho, esse erro pode ocorrer devido à padrão **política de segurança Local** configuração no computador remoto. A configuração padrão para o **política de segurança Local** configuração é **somente convidados - usuários locais autenticam como convidado**. Para depurar nesta configuração, você deve alterar a configuração no computador remoto para **Clássico - os usuários locais se autentiquem como si mesmos**.  
  
> [!NOTE]
>  Você deve ser administrador para realizar as seguintes tarefas.  
  
### <a name="to-open-the-local-security-policy-window"></a>Para abrir a janela Política de Segurança Local  
  
1.  Iniciar o **secpol. msc** snap-in do Console de gerenciamento Microsoft. Digite secpol.msc na pesquisa do Windows, na caixa de execução do Windows ou em um prompt de comando.  
  
### <a name="to-add-user-rights-assignments"></a>Para adicionar atribuições de direitos de usuário  
  
1.  Abra o **política de segurança Local** janela.  
  
2.  Expanda o **políticas locais** pasta.  
  
3.  Clique em **atribuição de direitos do usuário**.  
  
4.  No **política** coluna, clique duas vezes em **depurar programas** para exibir as atribuições de política de grupo local atual no **configuração de política de segurança Local** caixa de diálogo.  
  
     ![Direitos de usuário de diretiva de segurança local](../debugger/media/dbg_err_localsecuritypolicy_userrightsdebugprograms.png "DBG_ERR_LocalSecurityPolicy_UserRightsDebugPrograms")  
  
5.  Para adicionar novos usuários, clique o **adicionar usuário ou grupo** botão.  
  
### <a name="to-change-the-sharing-and-security-model"></a>Para alterar o Modelo de Compartilhamento e Segurança  
  
1.  Abra o **política de segurança Local** janela.  
  
2.  Expanda o **políticas locais** pasta.  
  
3.  Clique em **opções de segurança**.  
  
4.  No **política** coluna, clique duas vezes em **acesso à rede: modelo de compartilhamento e segurança para contas locais**.  
  
5.  No **acesso à rede: modelo de compartilhamento e segurança para contas locais** caixa de diálogo, altere o valor para **clássico - usuários locais autenticados como eles mesmos** e clique no **aplicar**botão.  
  
     ![Opções de segurança da política de segurança local](../debugger/media/dbg_err_localsecuritypolicy_securityoptions_networkaccess.png "DBG_ERR_LocalSecurityPolicy_SecurityOptions_NetworkAccess")  
  
## <a name="see-also"></a>Consulte também  
 [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)