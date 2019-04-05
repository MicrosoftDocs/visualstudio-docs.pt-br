---
title: Não é possível anexar ao processo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.unable2attach
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 0468de6c-3ff1-4979-a8c6-8afb53f37547
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 473afbdbbeb510434d45bf28dc02a3ff636d2b9c
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58927682"
---
# <a name="unable-to-attach-to-the-process"></a>Não é possível anexar ao processo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Não é possível anexar ao processo. O componente do depurador no servidor recebeu acesso negado ao se conectar a esse computador.  
  
 Há dois cenários comuns que causam esse erro:  
  
 **Cenário 1:** A máquina está executando o Windows XP. O computador B executa o Windows Server 2003. O registro no computador B contém o seguinte valor DWORD:  
  
 `HKLM\Software\Microsoft\MachineDebugManager\AllowLaunchAsOtherUser=1`  
  
 O usuário 1 inicia uma sessão do Terminal Server (sessão 1) no computador B e inicia um aplicativo gerenciado a partir dessa sessão.  
  
 Usuário 2, que é o administrador em ambos os computadores, é registrado no computador A. A partir daí, ele tenta se anexar a um aplicativo em execução na sessão 1 no computador B.  
  
 **Cenário 2:** Um usuário estiver conectado em dois computadores, A e B, no mesmo grupo de trabalho, usando a mesma senha em ambos os computadores. O depurador está em execução na máquina e tentando se conectar a um aplicativo gerenciado em execução no computador do computador B. A tem **acesso à rede: Modelo de compartilhamento e segurança para contas locais** definido como **convidado**.  
  
### <a name="to-solve-scenario-1"></a>Para solucionar o cenário 1  
  
-   Execute o depurador e o aplicativo gerenciado no mesmo nome e senha da conta do usuário.  
  
### <a name="to-solve-scenario-2"></a>Para solucionar o cenário 2  
  
1.  No menu **Iniciar**, selecione **Painel de Controle**.  
  
2.  No Painel de Controle, clique duas vezes em **Ferramentas administrativas**.  
  
3.  Na janela Ferramentas administrativas, clique duas vezes em **Política de Segurança Local**.  
  
4.  Na janela Política de Segurança Local, selecione **Políticas Locais**.  
  
5.  No **diretivas** coluna, clique duas vezes em **acesso à rede: Modelo de compartilhamento e segurança para contas locais**.  
  
6.  No **acesso à rede: Modelo de compartilhamento e segurança para contas locais** caixa de diálogo, altere a configuração de segurança local para **clássico**e clique em **Okey**.  
  
    > [!CAUTION]
    >  A alteração do modelo de segurança para Clássico pode resultar em acesso inesperado a arquivos e componentes DCOM compartilhados. Se você fizer essa alteração, um usuário remoto poderá ser autenticado com sua conta de usuário local em vez como Convidado. Se um usuário remoto corresponder ao seu nome de usuário e sua senha, esse usuário terá acesso a qualquer pasta ou objeto DCOM você compartilhar. Se você usar esse modelo de segurança, verifique se todas as contas de usuário no computador têm senhas fortes ou configure uma ilha isolada de rede para os computadores de depuração e depurados para impedir o acesso não autorizado.  
  
7.  Feche todas as janelas.  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)
