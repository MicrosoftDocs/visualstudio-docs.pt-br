---
title: Não é possível anexar ao processo | Microsoft Docs
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
manager: ghogen
ms.openlocfilehash: f0075050b6d24b63ed8380644ad9ec50dd4aa8ec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737664"
---
# <a name="unable-to-attach-to-the-process"></a>Não é possível anexar ao processo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Não é possível anexar ao processo. O componente do depurador no servidor recebeu acesso negado ao se conectar a esse computador.  
  
 Há dois cenários comuns que causam esse erro:  
  
 **Cenário 1:** um computador está executando o Windows XP. O computador B executa o Windows Server 2003. O registro no computador B contém o seguinte valor DWORD:  
  
 `HKLM\Software\Microsoft\MachineDebugManager\AllowLaunchAsOtherUser=1`  
  
 O usuário 1 inicia uma sessão do Terminal Server (sessão 1) no computador B e inicia um aplicativo gerenciado a partir dessa sessão.  
  
 Usuário 2, que é o administrador em ambos os computadores, é registrado no computador A. A partir daí, ele tenta se anexar a um aplicativo em execução na sessão 1 no computador B.  
  
 **Cenário 2:** um usuário estiver conectado em dois computadores, A e B, no mesmo grupo de trabalho, usando a mesma senha em ambos os computadores. O depurador está em execução na máquina e tentando se conectar a um aplicativo gerenciado em execução no computador do computador B. A tem **acesso à rede: modelo de compartilhamento e segurança para contas locais** definido como **convidado**.  
  
### <a name="to-solve-scenario-1"></a>Para solucionar o cenário 1  
  
-   Execute o depurador e o aplicativo gerenciado no mesmo nome e senha da conta do usuário.  
  
### <a name="to-solve-scenario-2"></a>Para resolver o cenário 2  
  
1.  Dos **inicie** menu, escolha **painel de controle**.  
  
2.  No painel de controle, clique duas vezes **ferramentas administrativas**.  
  
3.  Na janela Ferramentas administrativas, clique duas vezes em **política de segurança Local**.  
  
4.  Na janela de política de segurança Local, selecione **diretivas locais**.  
  
5.  No **diretivas** coluna, clique duas vezes em **acesso à rede: modelo de compartilhamento e segurança para contas locais**.  
  
6.  No **acesso à rede: modelo de compartilhamento e segurança para contas locais** diálogo caixa, altere a configuração de segurança local para **clássico**e clique em **Okey**.  
  
    > [!CAUTION]
    >  A alteração do modelo de segurança para Clássico pode resultar em acesso inesperado a arquivos e componentes DCOM compartilhados. Se você fizer essa alteração, um usuário remoto poderá ser autenticado com sua conta de usuário local em vez como Convidado. Se um usuário remoto corresponder ao seu nome de usuário e sua senha, esse usuário terá acesso a qualquer pasta ou objeto DCOM você compartilhar. Se você usar esse modelo de segurança, verifique se todas as contas de usuário no computador têm senhas fortes ou configure uma ilha isolada de rede para os computadores de depuração e depurados para impedir o acesso não autorizado.  
  
7.  Feche todas as janelas.  
  
## <a name="see-also"></a>Consulte também  
 [Preparação e configurações do depurador](../debugger/debugger-settings-and-preparation.md)



