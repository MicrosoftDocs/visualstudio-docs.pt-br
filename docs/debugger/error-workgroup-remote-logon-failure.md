---
title: Erro-falha de logon remoto do grupo de trabalho | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 97045215098b1f59d5f76a928e9e0a1ab8362756
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460086"
---
# <a name="error-workgroup-remote-logon-failure"></a>Erro: falha no logon remoto do grupo de trabalho
Este erro é:

 Falha de logon: usuário desconhecido ou senha inválida

 **Causa**

 Esse erro pode ocorrer quando você está depurando de um computador em um grupo de trabalho e tentar se conectar ao computador remoto. As possíveis causas incluem:

- Não há nenhuma conta com o nome e a senha correspondentes no computador remoto.

- Se o computador do Visual Studio e o computador remoto estiverem em grupos de trabalho, esse erro poderá ocorrer devido à configuração padrão de **Política de Segurança Local** no computador remoto. A configuração padrão de **Política de Segurança Local** é **Convidado somente – os usuários locais são autenticados como Convidado**. Para depurar nessa configuração, você deverá alterar a configuração no computador remoto para **Clássico – os usuários locais são autenticados como eles próprios**.

> [!NOTE]
> Você deve ser administrador para realizar as seguintes tarefas.

### <a name="to-open-the-local-security-policy-window"></a>Para abrir a janela Política de Segurança Local

1. Inicie o snap-in **secpol.msc** do snap-in Console de Gerenciamento Microsoft. Digite secpol.msc na pesquisa do Windows, na caixa de execução do Windows ou em um prompt de comando.

### <a name="to-add-user-rights-assignments"></a>Para adicionar atribuições de direitos de usuário

1. Abra a janela **Política de Segurança Local**.

2. Expanda a pasta **Políticas Locais**.

3. Clique em **Atribuição de Direitos do Usuário**.

4. Na coluna **Política**, clique duas vezes em **Depurar programas** para exibir as atribuições locais atual da política de grupo na caixa de diálogo **Configuração de Política de Segurança Local**.

     ![Direitos de usuário da política de segurança local](../debugger/media/dbg_err_localsecuritypolicy_userrightsdebugprograms.png "DBG_ERR_LocalSecurityPolicy_UserRightsDebugPrograms")

5. Para adicionar novos usuários, clique no botão **Adicionar Usuário ou Grupo**.

### <a name="to-change-the-sharing-and-security-model"></a>Para alterar o Modelo de Compartilhamento e Segurança

1. Abra a janela **Política de Segurança Local**.

2. Expanda a pasta **Políticas Locais**.

3. Clique em **Opções de Segurança**.

4. Na coluna **Política**, clique duas vezes em **Acesso à rede: modelo de compartilhamento e segurança para contas locais**.

5. Na caixa de diálogo **Acesso à rede: modelo de compartilhamento e segurança para contas locais**, altere o valor para **Clássico – os usuários locais são autenticados como eles próprios** e clique no botão **Aplicar**.

     ![Opções de segurança da política de segurança local](../debugger/media/dbg_err_localsecuritypolicy_securityoptions_networkaccess.png "DBG_ERR_LocalSecurityPolicy_SecurityOptions_NetworkAccess")

## <a name="see-also"></a>Veja também
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)
- [Depuração remota](../debugger/remote-debugging.md)