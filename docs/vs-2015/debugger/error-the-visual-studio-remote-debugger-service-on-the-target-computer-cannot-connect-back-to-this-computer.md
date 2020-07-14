---
title: 'Erro: o serviço de Depurador Remoto do Visual Studio no computador de destino não pode se conectar novamente a este computador | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.error.service_access_denied_oncallback
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 89ecf99d-66bf-4da0-a840-aa95b0be1702
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 80a7de83f118b38d9a3c71f1c7e7febf48e0f5bc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85520504"
---
# <a name="error-the-visual-studio-remote-debugger-service-on-the-target-computer-cannot-connect-back-to-this-computer"></a>Erro: o serviço Depurador Remoto do Visual Studio no computador de destino não pode se reconectar a este computador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Esse erro significa que o serviço de depurador remoto do Visual Studio está em execução em uma conta de usuário que não pode autenticar ao tentar se conectar ao computador do qual você está depurando.  
  
 A tabela a seguir mostra quais contas podem acessar o computador:  
  
|Cenário|Conta de LocalSystem|Conta do domínio|Contas locais que têm o mesmo nome de usuário e senha nos dois computadores|  
|-|-|-|-|-|  
|Ambos os computadores no mesmo domínio|Sim|Sim|Sim|  
|Ambos os computadores em domínios que tenham a confiança bidirecional|Não|Não|Sim|  
|Um ou ambos os computadores em um grupo de trabalho|Não|Não|Sim|  
|Computadores em domínios diferentes|Não|Não|Sim|  
  
 Além disso:  
  
- A conta na qual você executa o serviço de depurador remoto do Visual Studio deve ser administrador no computador remoto de modo que possa depurar qualquer processo.  
  
- a conta também precisa receber o privilégio de `Log on as a service` no computador remoto que está usando a ferramenta administrativa **Política de Segurança Local**.  
  
- Se você estiver usando um acesso de conta local no computador, deverá executar o serviço de depurador remoto do Visual Studio em uma conta local.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1. Verifique se o serviço de depurador remoto do Visual Studio está configurado corretamente no computador remoto. Para obter mais informações, consulte [Configurar o ferramentas remotas no dispositivo](https://msdn.microsoft.com/library/90f45630-0d26-4698-8c1f-63f85a12db9c).  
  
2. Execute o serviço de depurador remoto com uma conta que possa acessar o computador host do depurador, conforme mostrado na tabela anterior.  
  
### <a name="to-add-log-on-as-a-service-privilege"></a>Para adicionar o privilégio “Fazer logon como um serviço”  
  
1. No menu **Iniciar**, escolha **Painel de Controle**.  
  
2. No Painel de Controle, escolha o **Modo de Exibição Clássico**, se necessário.  
  
3. Clique duas vezes em **Ferramentas Administrativas**.  
  
4. Na janela Ferramentas Administrativas, clique duas vezes em **Política de Segurança Local**.  
  
5. Na janela **Configurações de Segurança Local**, expanda a pasta **Políticas Locais**.  
  
6. Clique em **Atribuição de Direitos do Usuário**.  
  
7. Na coluna **Política**, clique duas vezes em **Fazer logon como um serviço** para exibir as atribuições locais atuais da Política de Grupo na caixa de diálogo **Fazer logon como um serviço**.  
  
8. Para adicionar novos usuários, clique no botão **Adicionar Usuário ou Grupo**.  
  
9. Quando você terminar de adicionar usuários, clique em **OK**.  
  
### <a name="to-work-around-this-error"></a>Para resolver esse erro  
  
- Execute o Monitor de Depuração Remota como um aplicativo em vez de um serviço.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)   
 [Depuração remota](../debugger/remote-debugging.md)
