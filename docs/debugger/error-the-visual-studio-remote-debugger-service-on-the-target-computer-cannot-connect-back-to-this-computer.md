---
title: 'Erro: O serviço do Depurador Remoto do Visual Studio no computador de destino não pode se conectar novamente a esse computador'
titleSuffix: ''
ms.custom: seodec18
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: troubleshooting
f1_keywords:
- vs.debug.error.service_access_denied_oncallback
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
ms.openlocfilehash: 37caaea1f70771145f318d892025d566a99f4ea6
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53062616"
---
# <a name="error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer"></a>Erro: O serviço do Depurador Remoto do Visual Studio no computador de destino não pode se conectar novamente a esse computador
Esse erro significa que o serviço de depurador remoto do Visual Studio está em execução em uma conta de usuário que não pode autenticar ao tentar se conectar ao computador do qual você está depurando.  
  
 A tabela a seguir mostra quais contas podem acessar o computador:  
  
|||||  
|-|-|-|-|  
||Conta de LocalSystem|Conta de domínio|Contas locais que têm o mesmo nome de usuário e senha nos dois computadores|  
|Ambos os computadores no mesmo domínio|Sim|Sim|Sim|  
|Ambos os computadores em domínios que tenham a confiança bidirecional|Não|Não|Sim|  
|Um ou ambos os computadores em um grupo de trabalho|Não|Não|Sim|  
|Computadores em domínios diferentes|Não|Não|Sim|  
  
 Além disso:  
  
-   A conta na qual você executa o serviço de depurador remoto do Visual Studio deve ser administrador no computador remoto de modo que possa depurar qualquer processo.  
  
-   a conta também precisa receber o privilégio de `Log on as a service` no computador remoto que está usando a ferramenta administrativa **Política de Segurança Local**.  
  
-   Se você estiver usando um acesso de conta local no computador, deverá executar o serviço de depurador remoto do Visual Studio em uma conta local.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Verifique se o serviço de depurador remoto do Visual Studio está configurado corretamente no computador remoto. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md).  
  
2.  Execute o serviço de depurador remoto com uma conta que possa acessar o computador host do depurador, conforme mostrado na tabela anterior.  
  
### <a name="to-add-log-on-as-a-service-privilege"></a>Para adicionar o privilégio “Fazer logon como um serviço”  
  
1.  No menu **Iniciar**, escolha **Painel de Controle**.  
  
2.  No Painel de Controle, escolha o **Modo de Exibição Clássico**, se necessário.  
  
3.  Clique duas vezes em **Ferramentas Administrativas**.  
  
4.  Na janela Ferramentas Administrativas, clique duas vezes em **Política de Segurança Local**.  
  
5.  Na janela **Configurações de Segurança Local**, expanda a pasta **Políticas Locais**.  
  
6.  Clique em **Atribuição de Direitos do Usuário**.  
  
7.  Na coluna **Política**, clique duas vezes em **Fazer logon como um serviço** para exibir as atribuições locais atuais da Política de Grupo na caixa de diálogo **Fazer logon como um serviço**.  
  
8.  Para adicionar novos usuários, clique no botão **Adicionar Usuário ou Grupo**.  
  
9. Quando você terminar de adicionar usuários, clique em **OK**.  
  
### <a name="to-work-around-this-error"></a>Para resolver esse erro  
  
-   Execute o Monitor de Depuração Remota como um aplicativo em vez de um serviço.  
  
## <a name="see-also"></a>Consulte também  
 [Solução de problemas e erros de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)