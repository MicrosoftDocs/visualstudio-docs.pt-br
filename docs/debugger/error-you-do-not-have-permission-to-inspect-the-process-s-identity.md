---
title: 'Erro: Você não tem permissão para inspecionar o processo de&#39;identidade de s | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: troubleshooting
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
ms.openlocfilehash: 25d0a0be957cc06be75e48432a96357146671926
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56688076"
---
# <a name="error-you-do-not-have-permission-to-inspect-the-process39s-identity"></a>Erro: Você não tem permissão para inspecionar o processo de&#39;identidade de s
Você não tem permissão para inspecionar a identidade do processo. Isto pode ocorrer devido à configuração do sistema.

 O depurador não pôde inspecionar a identidade do processo, que são informações necessárias para depuração. A causa mais provável é que os Serviços de Terminal estão sendo desabilitados. O serviço dos Serviços de Terminal é habilitado por padrão. Siga estas etapas para habilitá-lo novamente.

### <a name="to-enable-terminal-services"></a>Para habilitar Serviços de Terminal

1.  Clique em **Iniciar** e escolha **Painel de Controle**.

2.  No Painel de Controle, escolha **Alternar para o Modo de Exibição Clássico** se necessário e clique duas vezes em **Ferramentas Administrativas**.

3.  Na janela **Ferramentas Administrativas**, clique duas vezes em **Gerenciamento de Computador**.

4.  Na janela Gerenciamento de Computador, expanda o nó **Serviços e Aplicativos**.

5.  Em **Serviços e Aplicativos**, clique em **Serviços**.

     Uma lista de serviços aparece no painel direito.

6.  Na lista **Serviços**, clique com o botão direito do mouse em **Serviços de Terminal** e escolha **Propriedades**.

7.  No **propriedades de serviços de Terminal** janela, vá para o **gerais** guia e defina **tipo de inicialização** para **Manual**.

8.  Clique em **OK**.

9. Reinicie o computador.

     Esse procedimento não habilita automaticamente a Área de Trabalho Remota. Se quiser habilitar a Área de Trabalho Remota no computador, execute o seguinte procedimento adicional.

### <a name="to-enable-remote-desktop"></a>Para habilitar a Área de Trabalho Remota

1.  Clique em **Iniciar** e clique com o botão direito do mouse em **Meu Computador**.

2.  Escolha **Propriedades**.

     A janela **Propriedades do Sistema** é exibida.

3.  Clique em **Remoto**.

4.  Em **Área de Trabalho Remota**, selecione **Permitir que usuários se conectem remotamente a este computador**.

5.  Clique em **OK**.

## <a name="see-also"></a>Consulte também
- [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)