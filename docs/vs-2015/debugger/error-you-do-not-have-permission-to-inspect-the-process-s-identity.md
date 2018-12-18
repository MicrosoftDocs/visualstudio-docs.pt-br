---
title: 'Erro: Você não tem permissão para inspecionar o processo de&#39;identidade de s | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 6233d060-85b8-42be-ae5f-bde7e1d0f241
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0974e38f9a0a901c97ca5dc3c9473d027095d67c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809374"
---
# <a name="error-you-do-not-have-permission-to-inspect-the-process39s-identity"></a>Erro: Você não tem permissão para inspecionar o processo de&#39;identidade de s
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você não tem permissão para inspecionar a identidade do processo. Isto pode ocorrer devido à configuração do sistema.  
  
 O depurador não pôde inspecionar a identidade do processo, que são informações necessárias para depuração. A causa mais provável é que os Serviços de Terminal estão sendo desabilitados. O serviço dos Serviços de Terminal é habilitado por padrão. Siga estas etapas para habilitá-lo novamente.  
  
### <a name="to-enable-terminal-services"></a>Para habilitar Serviços de Terminal  
  
1.  Clique em **inicie** e, em seguida, escolha **painel de controle**.  
  
2.  No painel de controle, escolha **alternar para modo de exibição clássico**, se necessário e, em seguida, clique duas vezes em **ferramentas administrativas**.  
  
3.  No **ferramentas administrativas** janela, clique duas vezes em **gerenciamento de computador**.  
  
4.  Na janela de gerenciamento do computador, expanda o **serviços e aplicativos** nó.  
  
5.  Sob o **aplicativos e serviços**, clique em **serviços**.  
  
     Uma lista de serviços aparece no painel direito.  
  
6.  No **Services** lista, clique com botão direito **serviços de Terminal** e, em seguida, escolha **propriedades**.  
  
7.  No **propriedades de serviços de Terminal** janela, vá para o **gerais** guia e defina **tipo de inicialização** para **Manual**.  
  
8.  Clique em **OK**.  
  
9. Reinicie o computador.  
  
     Esse procedimento não habilita automaticamente a Área de Trabalho Remota. Se quiser habilitar a Área de Trabalho Remota no computador, execute o seguinte procedimento adicional.  
  
### <a name="to-enable-remote-desktop"></a>Para habilitar a Área de Trabalho Remota  
  
1.  Clique em **inicie** e, em seguida, clique com botão direito **meu computador**.  
  
2.  Escolha **Propriedades**.  
  
     O **propriedades do sistema** janela é exibida.  
  
3.  Clique em **remoto**.  
  
4.  Sob **área de trabalho remota**, selecione **permitem que os usuários se conectem remotamente a este computador**.  
  
5.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)



