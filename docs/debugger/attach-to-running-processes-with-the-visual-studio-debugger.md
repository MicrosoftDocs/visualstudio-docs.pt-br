---
title: Anexar a processos em execução com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 09/27/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.processes.attach
- vs.debug.process
- vs.debug.programs
- vs.debug.detaching
- vs.debug.processes
- vs.debug.error.attach
- vs.debug.remotemachine
dev_langs:
- CSharp
- FSharp
- C++
- VB
helpviewer_keywords:
- remote debugging, attaching to programs
- processes, attaching to running processes
- Attach to Process dialog box
- debugging [Visual Studio], attaching to processes
- debugger, processes
ms.assetid: 27900e58-090c-4211-a309-b3e1496d5824
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 07ed9670795e11b0d98b3703445450b468a93aa8
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53068455"
---
# <a name="attach-to-running-processes-with-the-visual-studio-debugger"></a>Anexar a processos em execução com o depurador do Visual Studio
Você pode anexar o depurador do Visual Studio para um processo em execução em um computador local ou remoto. Depois que o processo está em execução, selecione **Debug** > **anexar ao processo** ou pressione **Ctrl**+**Alt** + **P** no Visual Studio e usar o **anexar ao processo** caixa de diálogo para anexar o depurador ao processo.

Você pode usar **anexar ao processo** para depurar aplicativos em execução em computadores locais ou remotos, depurar vários processos simultaneamente, depurar os aplicativos que não foram criados no Visual Studio ou depurar qualquer aplicativo que não tenha iniciado a partir do Visual Studio com o depurador anexado. Por exemplo, se você estiver executando um aplicativo sem o depurador e atingir uma exceção, você pode, em seguida, anexar o depurador ao processo executando o aplicativo e iniciar a depuração.

Para obter informações sobre depuração básica no Visual Studio, consulte [Introdução ao depurador](../debugger/getting-started-with-the-debugger.md).

> [!TIP]
> Não tenho certeza se deve ser usado **anexar ao processo** para seu cenário de depuração? Ver [comum de cenários de depuração](#BKMK_Scenarios). 

##  <a name="BKMK_Attach_to_a_running_process"></a> Anexar a um processo em execução no computador local  

Para reanexar rapidamente a um processo anexado ao anteriormente, consulte [anexar novamente a um processo](#BKMK_reattach). 

Para depurar um processo em um computador remoto, consulte [anexar a um processo em um computador remoto](#BKMK_Attach_to_a_process_on_a_remote_computer).

**Para anexar a um processo no computador local:**  

1. No Visual Studio, selecione **Debug** > **anexar ao processo** (ou pressione **Ctrl**+**Alt** + **P**) para abrir o **anexar ao processo** caixa de diálogo.
  
   **Tipo de Conexão** deve ser definido como **padrão**. **Destino de Conexão** deve ser o nome do computador local. 
  
   ![DBG_Basics_Attach_To_Process](../debugger/media/DBG_Basics_Attach_To_Process.png "DBG_Basics_Attach_To_Process") 
  
2. No **processos disponíveis** lista, localize e selecione o processo ou processos que você deseja anexar.  

   - Para selecionar rapidamente um processo, digite seu nome ou a primeira letra na **processos de filtro** caixa. 
  
   - Se você não souber o nome do processo, percorra a lista, ou consulte [comum de cenários de depuração](#BKMK_Scenarios) para alguns nomes comuns do processo. 
  
   >[!TIP]
   >Processos podem iniciar e parar em segundo plano enquanto o **anexar ao processo** caixa de diálogo é aberta, portanto, a lista de processos em execução pode não estar atualizada. Você pode selecionar **Refresh** a qualquer momento para ver a lista atual. 
  
3. No **anexar a** campo, verifique se o tipo de código que você pretende depurar está listado. O padrão **automática** definindo funciona para a maioria dos tipos de aplicativo. 
  
   Para selecionar manualmente os tipos de código:
   1. Clique em **Selecionar**. 
   1. No **Selecionar tipo de código** caixa de diálogo, selecione **depurar esses tipos de código**.
   1. Selecione os tipos de código que você deseja depurar.
   1. Selecione **OK**.
  
4. Selecione **anexar**.
  
>[!NOTE]
>Você também pode ser associada a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador em um momento. Você pode definir o aplicativo ativo no Visual Studio **local de depuração** barra de ferramentas ou **processos** janela.  

##  <a name="BKMK_Attach_to_a_process_on_a_remote_computer"></a> Anexar a um processo em um computador remoto  

Você também pode selecionar um computador remoto a **anexar ao processo** caixa de diálogo, exibir uma lista de processos disponíveis em execução nesse computador e anexar a um ou mais processos para depuração. O depurador remoto (*msvsmon.exe*) deve estar em execução no computador remoto. Para obter mais informações, consulte [depuração remota](../debugger/remote-debugging.md). 

Para obter instruções mais completas para depuração de aplicativos do ASP.NET que foi implantados no IIS, consulte [depuração ASP.NET em um computador remoto de IIS remota](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).

**Para anexar a um processo em execução em um computador remoto:**  

1. No Visual Studio, selecione **Debug** > **anexar ao processo** (ou pressione **Ctrl**+**Alt** + **P**) para abrir o **anexar ao processo** caixa de diálogo.
  
2. **Tipo de Conexão** deve ser **padrão** na maioria dos casos. No **destino de Conexão** , selecione o computador remoto, usando um dos seguintes métodos:

   - Selecione a seta suspensa ao lado **destino de Conexão**e selecione o nome do computador na lista suspensa.  
   - Digite o nome do computador na **destino de Conexão** caixa.
      
     > [!NOTE]
     > Se você não pode se conectar usando o nome do computador remoto, tente usar o IP e endereço da porta (por exemplo, `123.45.678.9:4022`). 4022 é a porta padrão para o depurador remoto do Visual Studio 2017 x64. Para outras atribuições de porta do depurador remoto, consulte [atribuições de porta do depurador remoto](remote-debugger-port-assignments.md).  
      
   - Selecione o **encontrar** lado a **destino de Conexão** caixa para abrir o **conexões remotas** caixa de diálogo. O **conexões remotas** caixa de diálogo lista todos os dispositivos que estão na sua sub-rede local ou diretamente conectado ao seu computador. Talvez você precise [abra a porta UDP 3702](../debugger/remote-debugger-port-assignments.md) no servidor para descobrir dispositivos remotos. Selecione o computador ou dispositivo que você deseja e, em seguida, clique em **selecionar**. 
  
   > [!NOTE]
   > O **tipo de Conexão** configuração persiste entre as sessões de depuração. O **destino de Conexão** configuração persiste entre as sessões de depuração somente se uma conexão de depuração bem-sucedida ocorreu com o destino.

3. Clique em **Refresh** para popular o **processos disponíveis** lista.
     
    >[!TIP]
    >Processos podem iniciar e parar em segundo plano enquanto o **anexar ao processo** caixa de diálogo é aberta, portanto, a lista de processos em execução pode não estar atualizada. Você pode selecionar **Refresh** a qualquer momento para ver a lista atual. 
     
4. No **processos disponíveis** lista, localize e selecione o processo ou processos que você deseja anexar.  

   - Para selecionar rapidamente um processo, digite seu nome ou a primeira letra na **processos de filtro** caixa. 
  
   - Se você não souber o nome do processo, percorra a lista, ou consulte [comum de cenários de depuração](#BKMK_Scenarios) para alguns nomes comuns do processo. 
  
   - Para localizar os processos em execução em todas as contas de usuário, selecione o **Mostrar processos de todos os usuários** caixa de seleção.
      
     >[!NOTE]
     >Se você tentar anexar a um processo de propriedade de uma conta de usuário não confiável, aparecerá uma confirmação da caixa de diálogo de aviso de segurança. Para obter mais informações, consulte [aviso de segurança: anexar a um processo pertencente a um usuário não confiável pode ser perigoso. Se as informações a seguir parecerem suspeitas ou você não tiver certeza, não anexe a esse processo](../debugger/security-warning-attaching-to-a-process-owned-by-an-untrusted-user.md).  
      
5. No **anexar a** campo, verifique se o tipo de código que você pretende depurar está listado. O padrão **automática** definindo funciona para a maioria dos tipos de aplicativo. 
  
   Para selecionar manualmente os tipos de código:
   1. Clique em **Selecionar**. 
   1. No **Selecionar tipo de código** caixa de diálogo, selecione **depurar esses tipos de código**.
   1. Selecione os tipos de código que você deseja depurar.
   1. Selecione **OK**.
  
6. Selecione **anexar**.
  
>[!NOTE]
>Você também pode ser associada a vários aplicativos para depuração, mas apenas um aplicativo está ativo no depurador em um momento. Você pode definir o aplicativo ativo no Visual Studio **local de depuração** barra de ferramentas ou **processos** janela.  

Em alguns casos, quando você depura em uma sessão de área de trabalho remota (serviços de Terminal), o **processos disponíveis** lista não exibirá todos os processos disponíveis. Se você estiver executando o Visual Studio como um usuário que tenha uma conta de usuário limitado, o **processos disponíveis** lista não mostrará os processos em execução na sessão 0. A sessão 0 é usada para serviços e outros processos do servidor, incluindo *w3wp.exe*. Você pode resolver o problema executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] em uma conta de administrador ou executando o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] no console do servidor em vez de uma sessão de Serviços de Terminal. 

Se nenhuma dessas soluções alternativas é possível, uma terceira opção é anexar ao processo executando `vsjitdebugger.exe -p <ProcessId>` na linha de comando do Windows. Você pode determinar a ID do processo usando *tlist.exe*. Para obter *tlist.exe*, baixe e instale a depuração de ferramentas para Windows, disponível em [downloads do WDK e WinDbg](/windows-hardware/drivers/download-the-wdk).

## <a name="BKMK_reattach"></a> Reconecte-se a um processo

Você poderá reanexar rapidamente a processos que estavam anteriormente conectados a, escolhendo **Debug** > **reanexar ao processo** (**Shift** + **Alt**+**P**). Quando você escolhe este comando, o depurador tentará imediatamente anexar até o último processo anexado ao primeiro tentando corresponder à ID do processo anterior e se isso falhar, correspondendo ao anterior nome do processo. Se nenhuma correspondência for encontrada, ou se vários processos têm o mesmo nome, o **anexar ao processo** caixa de diálogo será aberta para que você possa selecionar o processo correto.

> [!NOTE]
> O **reanexar ao processo** command é novo no Visual Studio 2017.

## <a name="BKMK_Scenarios"></a> Cenários comuns de depuração

Para ajudá-lo a determinar se deve ser usado **anexar ao processo** e qual processo para anexar a tabela a seguir mostra alguns cenários comuns de depuração, com links para obter mais instruções onde estiver disponível. (A lista não é exaustiva.) 

Para alguns tipos de aplicativo, como os aplicativos do aplicativo Universal do Windows (UWP), não anexe diretamente a um nome de processo, mas usar o **depurar pacote do aplicativo instalado** a opção de menu no Visual Studio em vez disso (veja a tabela).

Para que o depurador se anexe ao código escrito em C++, o código precisa emitir `DebuggableAttribute`. Você pode adicionar isso ao seu código automaticamente vinculando à opção do vinculador [/ASSEMBLYDEBUG](/cpp/build/reference/assemblydebug-add-debuggableattribute).

Para depuração de script do lado do cliente, a depuração de script deve ser habilitada no navegador. Para depurar o script do lado do cliente no Chrome, escolha **Webkit** como o tipo de código e, dependendo de seu tipo de aplicativo, talvez seja necessário fechar todas as instâncias do Chrome e iniciar o navegador no modo de depuração (tipo `chrome.exe --remote-debugging-port=9222` de uma linha de comando).

Para selecionar rapidamente um processo em execução para anexar a, no Visual Studio, digite **Ctrl**+**Alt**+**P**e, em seguida, digite a primeira letra das nome do processo.

|Cenário|Depurar o método|Nome do processo|Observações e links|
|-|-|-|-|
|Depuração remota ASP.NET 4 ou 4.5 em um servidor IIS|Usar as ferramentas remotas e **anexar ao processo**|*w3wp.exe*|Consulte [remota de depuração do ASP.NET em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)|
|Depuração remota do ASP.NET Core em um servidor IIS|Usar as ferramentas remotas e **anexar ao processo**|*dotnet.exe*|Para implantação de aplicativo, consulte [publicar no IIS](https://docs.asp.net/en/latest/publishing/iis.html). Para depuração, consulte [depuração remota do ASP.NET Core em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md)|
|Depurar o script do lado do cliente em um servidor IIS local, para tipos de aplicativos com suporte |Use **anexar ao processo**|*Chrome.exe*, *MicrosoftEdgeCP.exe*, ou *iexplore.exe*|Depuração de script deve ser habilitada. Para o Chrome, você também deve executar Chrome no modo de depuração e selecione **código Webkit** na **anexar a** campo.|
|Depurar um aplicativo c#, Visual Basic ou C++ no computador local|Use um [depuração padrão](../debugger/getting-started-with-the-debugger.md) ou **anexar ao processo**|*\<appname > .exe*|Na maioria dos cenários, usar a depuração padrão e não **anexar ao processo**.|
|Depuração remota de um aplicativo de desktop do Windows|Ferramentas remotas|N/D| Ver [remoto depurar um aplicativo c# ou Visual Basic](../debugger/remote-debugging-csharp.md) ou [remoto depurar um aplicativo C++](../debugger/remote-debugging-cpp.md)|
|Depurar um aplicativo ASP.NET no computador local depois de iniciar o aplicativo sem o depurador|Use **anexar ao processo**|*iiexpress.exe*|Isso pode ser útil para fazer com que seu aplicativo carregar mais rápido, como (por exemplo) ao criar o perfil. |
|Depurar outros tipos de aplicativos com suporte em um processo do servidor|Se o servidor remoto, use as ferramentas remotas, e **anexar ao processo**|*Chrome.exe*, *iexplore.exe*, ou outros processos|Se necessário, use o Monitor de recursos para ajudar a identificar o processo. Confira [Depuração remota](../debugger/remote-debugging.md).|
|Remoto depurar um aplicativo de IoT, OneCore, HoloLens ou aplicativo Universal do Windows (UWP)|Depurar pacote do aplicativo instalado|N/D|Ver [depurar pacote de aplicativo instalado](debug-installed-app-package.md) em vez de usar **anexar ao processo**|
|Depurar um aplicativo de IoT, OneCore, HoloLens ou aplicativo Universal do Windows (UWP) que não tenha iniciado a partir do Visual Studio|Depurar pacote do aplicativo instalado|N/D|Ver [depurar pacote de aplicativo instalado](debug-installed-app-package.md) em vez de usar **anexar ao processo**|  
  
## <a name="use-debugger-features"></a>Usar recursos do depurador

Para usar os recursos completos do depurador do Visual Studio (como usar pontos de interrupção) ao anexar a um processo, o aplicativo deve corresponder exatamente ao seu local de origem e símbolos. Ou seja, o depurador deve ser capaz de carregar o correto [(. PDB) arquivos de símbolo](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md). Por padrão, isso requer uma compilação de depuração.

Para cenários de depuração remota, você deve ter o código-fonte (ou uma cópia do código-fonte) estiver aberto no Visual Studio. Os binários do aplicativo compilado no computador remoto devem vir da mesma compilação, como no computador local.

Em alguns cenários de depuração locais, você pode depurar no Visual Studio sem acesso à fonte de se os arquivos de símbolos corretos estão presentes com o aplicativo. Por padrão, isso requer uma compilação de depuração. Para obter mais informações, consulte [especificar arquivos de origem e símbolo](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).
  
##  <a name="BKMK_Troubleshoot_attach_errors"></a> Solucionar problemas de anexo  
 Quando o depurador se anexa a um processo em execução, o processo pode conter um ou mais tipos de código. Os tipos de código aos quais o depurador pode se anexar são exibidos e selecionados na caixa de diálogo **Selecionar Tipo de Código**.  
  
 Às vezes, o depurador pode ser anexado com êxito a um tipo de código, mas não a outro tipo de código. Isso pode ocorrer se você estiver tentando anexar a um processo que esteja sendo executado em um computador remoto. O computador remoto pode ter componentes de depuração remota instalados para alguns tipos de código mas não para outros. Isso também pode ocorrer se você tentar anexar a dois ou mais processos para depuração direta de banco de dados. A depuração de SQL dá suporte à anexação de apenas um único processo.  
  
 Se o depurador é consegue se conectar a alguns, mas nem todos os tipos de código, você verá uma mensagem identificando quais tipos de falha ao anexar.  
  
 Se o depurador for anexado com êxito a pelo menos um tipo de código, você poderá depurar o processo. Você poderá depurar apenas os tipos de código que foram anexados com êxito. O código desanexado no processo ainda será executado, mas você não poderá definir pontos de interrupção, exibir dados ou executar outras operações em que o código de depuração.  
  
 Se você quiser obter informações mais específicas sobre por que o depurador não conseguiu anexar a um tipo de código, tente reanexar somente àquele tipo de código.  
  
 **Para obter informações específicas sobre o motivo de um tipo de código ter falhado na anexação:**  
  
1.  Desanexe do processo. Sobre o **Debug** menu, selecione **desanexar tudo**.  
  
1.  Reanexe ao processo, selecionando apenas o tipo de código que não foi anexado.  
  
    1.  Na caixa de diálogo **Anexar ao Processo**, selecione o processo na lista **Processos Disponíveis**.  
  
    2.  Selecione **selecionar**.  
  
    3.  Na caixa de diálogo **Tipo de Código Selecionado**, selecione **Depurar esses tipos de código** e o tipo de código que falhou em ser anexado. Desmarque os outros tipos de código.  
  
    4.  Selecione **OK**.  
  
    5.  No **anexar ao processo** caixa de diálogo, selecione **Attach**.  
  
    Desta vez, o anexo falhará completamente e você receberá uma mensagem de erro específica.  
  
## <a name="see-also"></a>Consulte também  
 [Depurar vários processos](../debugger/debug-multiple-processes.md)   
 [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md)   
 [Depuração remota](../debugger/remote-debugging.md)
 