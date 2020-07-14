---
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.openlocfilehash: 2e5782c49f26925d9eda81f04653b1a20666c6b1
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149166"
---
1. No computador remoto, localize e inicie o **depurador remoto** no menu **Iniciar** . 
   
   Se você não tiver permissões administrativas no computador remoto, clique com o botão direito do mouse no aplicativo do **depurador remoto** e selecione **Executar como administrador**. Caso contrário, basta iniciá-lo normalmente.

   Se você estiver planejando anexar a um processo que está sendo executado como administrador ou que está sendo executado em uma conta de usuário diferente (como o IIS), clique com o botão direito do mouse no aplicativo do **depurador remoto** e selecione **Executar como administrador**. Para obter mais informações, consulte [executar o depurador remoto como administrador](../remote-debugging-errors-and-troubleshooting.md#run-the-remote-debugger-as-an-administrator).
   
1. Na primeira vez que você iniciar o depurador remoto (ou antes de configurá-lo), a caixa de diálogo **configuração de depuração remota** será exibida.  
  
    Configuração do depurador(../media/remotedebuggerconfwizardpage.png "remoto") de ![configuração do depurador]remoto  
  
1. Se a API dos serviços Web do Windows não estiver instalada, o que acontece apenas no Windows Server 2008 R2, selecione o botão **instalar** .  
  
1. Selecione pelo menos um tipo de rede no qual você deseja usar as ferramentas remotas. Se os computadores estiverem conectados por meio de um domínio, você deverá escolher o primeiro item. Se os computadores estiverem conectados por meio de um grupo de trabalho ou grupos domésticos, escolha o segundo ou terceiro item, conforme apropriado.  
  
1. Selecione **Configurar depuração remota** para configurar o firewall e iniciar o depurador remoto.  
  
1. Quando a configuração estiver concluída, a janela do **depurador remoto** será exibida.
  
    Janela de depurador(../media/remotedebuggerwindow.png "remoto") da ![janela do depurador remoto]
  
    O depurador remoto agora está aguardando uma conexão. Use o nome do servidor e o número da porta mostrada para definir a configuração de conexão remota no Visual Studio.  
  
Para interromper o depurador remoto, selecione **arquivo**  >  **sair**. Você pode reiniciá-lo no menu **Iniciar** ou na linha de comando:  
  
```cmd
<Remote debugger installation directory>\msvsmon.exe
```
