---
title: Depurando um serviço de nuvem do Azure ou a máquina virtual no Visual Studio | Microsoft Docs
description: Depurando um serviço de nuvem ou máquina Virtual no Visual Studio
author: mikejo5000
manager: douge
ms.assetid: 945e06e0-2100-41af-b218-72347367ddab
ms.topic: conceptual
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 11/11/2016
ms.author: mikejo
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.openlocfilehash: b2c67ce81a42df4a17761fcee2dcd2f8a67c4941
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51001313"
---
# <a name="debugging-an-azure-cloud-service-or-virtual-machine-in-visual-studio"></a>Depurando um serviço de nuvem do Azure ou a máquina virtual no Visual Studio

Visual Studio oferece diferentes opções para depurar serviços de nuvem do Azure e máquinas virtuais.

## <a name="debug-your-cloud-service-on-your-local-computer"></a>Depurar seu serviço de nuvem em seu computador local

Você pode economizar tempo e dinheiro usando o Azure compute emulator para depurar seu serviço de nuvem em um computador local. Ao depurar um serviço localmente antes de implantá-lo, você pode melhorar a confiabilidade e desempenho sem pagar pelo tempo de computação. No entanto, alguns erros podem ocorrer somente quando você executa um serviço de nuvem no Azure em si. Se você habilitar a depuração remota ao publicar seu serviço e, em seguida, anexar o depurador a uma instância de função, você pode depurar esses erros.

O emulador simula o serviço de computação do Azure e é executado no ambiente local para que você possa testar e depurar seu serviço de nuvem antes de implantá-lo. O emulador trata o ciclo de vida das instâncias de função e fornece acesso a recursos simulados, como armazenamento local. Quando você depura ou executa seu serviço no Visual Studio, ele inicia automaticamente o emulador como um aplicativo em segundo plano e, em seguida, implanta seu serviço no emulador. Você pode usar o emulador para exibir seu serviço quando ele é executado no ambiente local. Você pode executar a versão completa ou a versão expressa do emulador. (A partir do Azure 2.3, a versão expressa do emulador é o padrão.) Ver [usando o Emulator Express para executar e depurar um serviço de nuvem localmente](vs-azure-tools-emulator-express-debug-run.md).

### <a name="to-debug-your-cloud-service-on-your-local-computer"></a>Para depurar seu serviço de nuvem em seu computador local

1. Na barra de menus, escolha **Debug**, **iniciar depuração** para executar o projeto de serviço de nuvem do Azure. Como alternativa, você pode pressionar F5. Você verá uma mensagem que o emulador de computação está sendo iniciado. Quando o emulador é iniciado, o ícone de bandeja do sistema o confirma.

    ![Emulador do Azure na bandeja do sistema](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC783828.png)

2. Exibir a interface do usuário para o emulador de computação abrindo o menu de atalho do ícone do Azure na área de notificação e, em seguida, selecione **mostrar IU do emulador de computação**.

    O painel esquerdo da interface do usuário mostra os serviços que estão implantados atualmente para o emulador de computação e as instâncias de função que cada serviço está em execução. Você pode escolher o serviço ou funções para exibir o ciclo de vida, registro em log e informações de diagnóstico no painel direito. Se você colocar o foco na margem superior de uma janela incluída, ela se expande para preencher o painel direito.

3. Percorra o aplicativo selecionando os comandos na **depurar** menu e definindo pontos de interrupção no seu código. Conforme você percorre o aplicativo no depurador, os painéis são atualizados com o status atual do aplicativo. Quando você interrompe a depuração, a implantação do aplicativo é excluída. Se seu aplicativo inclui uma função web e você tiver definido a propriedade de ação de inicialização para iniciar o navegador da web, o Visual Studio inicia o aplicativo web no navegador. Se você alterar o número de instâncias de uma função na configuração do serviço, você deve parar o serviço de nuvem e, em seguida, reinicie a depuração para que você possa depurar essas novas instâncias da função.

    **Observação:** quando você interrompe a execução ou depuração do serviço, o emulador de computação local e o emulador de armazenamento não são interrompidos. Você deve interrompê-los explicitamente da área de notificação.

## <a name="debug-a-cloud-service-in-azure"></a>Depure um serviço de nuvem no Azure

Para depurar um serviço de nuvem de um computador remoto, você deve habilitar essa funcionalidade explicitamente quando você implanta seu serviço de nuvem para que os serviços (por exemplo, msvsmon.exe) são instalados nas máquinas virtuais que executam suas instâncias de função. Se você não habilitar a depuração remota quando publicou o serviço, você precisará publicar novamente o serviço com a depuração remota habilitada.

Se você habilitar a depuração remota para um serviço de nuvem, ele não mostrará degradação de desempenho ou incorrer em encargos adicionais. Não use a depuração remota em um serviço de produção, pois os clientes que usam o serviço podem ser afetados negativamente.

> [!NOTE]
> Quando você publica um serviço de nuvem do Visual Studio, você pode habilitar **IntelliTrace** para quaisquer funções nesse serviço destinados ao .NET Framework 4 ou o .NET Framework 4.5. Usando **IntelliTrace**, você pode examinar os eventos que ocorreram em uma instância de função no passado e reproduzir o contexto no momento. Ver [depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016) e [usando o IntelliTrace](https://msdn.microsoft.com/library/dd264915.aspx).

### <a name="to-enable-remote-debugging-for-a-cloud-service"></a>Para habilitar a depuração remota para um serviço de nuvem

1. Abra o menu de atalho do projeto do Azure e, em seguida, selecione **publicar**.

2. Selecione o **preparo** ambiente e o **depurar** configuração.

    Isso é apenas uma diretriz. Você pode optar por executar ambientes de teste em um ambiente de produção. No entanto, você poderá afetar negativamente os usuários se você habilitar a depuração remota no ambiente de produção. Você pode escolher a configuração de versão, mas a configuração de depuração facilita a depuração.

    ![Escolha a configuração de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746717.gif)

3. Siga as etapas normais, mas selecione a **habilitar depurador remoto para todas as funções** caixa de seleção a **configurações avançadas** guia.

    ![Configuração de depuração](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746718.gif)

### <a name="to-attach-the-debugger-to-a-cloud-service-in-azure"></a>Para anexar o depurador a um serviço de nuvem no Azure

1. No Gerenciador de servidores, expanda o nó para o serviço de nuvem.

2. Abra o menu de atalho para a função ou instância de função à qual você deseja anexar e, em seguida, selecione **Anexar depurador**.

    Se você depurar uma função, o depurador do Visual Studio anexará a cada instância dessa função. O depurador interromperá no ponto de interrupção para a primeira instância de função que executa essa linha de código e atende a quaisquer condições de ponto de interrupção. Se você depura uma instância, o depurador será anexado apenas essa instância e interrompido em um ponto de interrupção somente quando essa instância específica executa essa linha de código e atende às condições do ponto de interrupção.

    ![Anexar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746719.gif)

3. Depois que o depurador é anexado a uma instância, depure como de costume. O depurador é anexado automaticamente ao processo de host apropriado para sua função. Dependendo de qual é a função, o depurador é anexado a w3wp.exe, WaWorkerHost.exe ou WaIISHost.exe. Para verificar se o processo ao qual o depurador é anexado, expanda o nó da instância no Gerenciador de servidores. Ver [arquitetura de funções do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações sobre os processos do Azure.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

4. Para identificar os processos aos quais o depurador é anexado, abra a caixa de diálogo de processos, na barra de menus, escolha Depurar, Windows, processos. (Teclado: Ctrl + Alt + Z) Para desanexar um processo específico, abra o menu de atalho e, em seguida, selecione **desanexar processo**. Ou, localize o nó da instância no Gerenciador de servidores, localize o processo, abra o menu de atalho e, em seguida, selecione **desanexar processo**.

    ![Depurar processos](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC690787.gif)

> [!WARNING]
> Evite paradas longas em pontos de interrupção quando a depuração. O Azure trata um processo que é interrompido por mais de alguns minutos como sem resposta e interromperá o envio de tráfego para essa instância. Se você parar por muito tempo, msvsmon.exe dispara do processo.

Para desanexar o depurador de todos os processos em sua instância ou função, abra o menu de atalho para a função ou instância que você está depurando e, em seguida, selecione **desanexar depurador**.

## <a name="limitations-of-remote-debugging-in-azure"></a>Limitações da depuração remota no Azure

No SDK 2.3 do Azure, a depuração remota tem as seguintes limitações:

* Com a depuração remota habilitada, você não pode publicar um serviço de nuvem na qual qualquer função tenha mais de 25 instâncias.
* O depurador usa as portas 30400 a 30424, 31400 a 31424 e 32400 a 32424. Se você tentar usar qualquer uma dessas portas, você não poderá publicar seu serviço e uma das seguintes mensagens de erro será exibida no log de atividades do Azure:

  * Erro ao validar o arquivo. cscfg em relação ao arquivo. csdef.
    O intervalo' intervalo de portas reservado' para o ponto de extremidade remotedebugger da função 'role' se sobrepõe com uma porta já definida ou um intervalo.
  * Falha na alocação. Tente novamente mais tarde, tente reduzir o tamanho da VM ou o número de instâncias de função ou tente implantar em uma região diferente.

## <a name="debugging-azure-virtual-machines"></a>Depuração de máquinas virtuais do Azure

Você pode depurar programas que são executados em máquinas virtuais do Azure usando o Gerenciador de servidores no Visual Studio. Quando você habilita a depuração remota em uma máquina virtual do Azure, o Azure instala o extensão de depuração remota na máquina virtual. Em seguida, você pode anexar a processos na máquina virtual e depurar como faria normalmente.

> [!NOTE]
> As máquinas virtuais criadas por meio da pilha do Gerenciador de recursos do Azure pode ser depuradas remotamente usando o Gerenciador de nuvem no Visual Studio 2015. Para obter mais informações, consulte [Gerenciando recursos do Azure com o Cloud Explorer](http://go.microsoft.com/fwlink/?LinkId=623031).

### <a name="to-debug-an-azure-virtual-machine"></a>Para depurar uma máquina virtual do Azure

1. No Gerenciador de servidores, expanda o nó de máquinas virtuais e selecione o nó da máquina virtual que você deseja depurar.

2. Abra o menu de contexto e selecione **Ativar depuração**. Quando for perguntado se você tiver certeza se você quiser habilitar a depuração na máquina virtual, selecione **Sim**.

    O Azure instala o extensão de depuração remota na máquina virtual para habilitar a depuração.

    ![Comando depuração habilitada para máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Log de atividades do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)

3. Depois que a extensão de depuração remota concluir a instalação, abra o menu de contexto da máquina virtual e selecione **Anexar depurador...**

    O Azure obtém uma lista dos processos na máquina virtual e os mostra na anexar à caixa de diálogo de processo.

    ![Comando Anexar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)

4. No **anexar ao processo** caixa de diálogo, selecione **selecione** para limitar a lista de resultados para mostrar apenas os tipos de código que você deseja depurar. Você pode depurar código gerenciado de 32 bits ou 64 bits, o código nativo ou ambos.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

5. Selecione os processos que você deseja depurar na máquina virtual e, em seguida, selecione **Attach**. Por exemplo, você pode escolher o processo w3wp.exe se quiser depurar um aplicativo web na máquina virtual. Ver [depurar um ou mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) e [arquitetura de funções do Azure](http://blogs.msdn.com/b/kwill/archive/2011/05/05/windows-azure-role-architecture.aspx) para obter mais informações.

## <a name="create-a-web-project-and-a-virtual-machine-for-debugging"></a>Criar um projeto da web e uma máquina virtual para depuração

Antes de publicar seu projeto do Azure, talvez seja útil testá-lo em um ambiente independente que dá suporte a cenários de teste e depuração, e onde você pode instalar testes e programas de monitoramento. Uma maneira de executar esses testes é depurar remotamente seu aplicativo em uma máquina virtual.

Projetos do Visual Studio ASP.NET oferecem uma opção para criar uma máquina virtual útil que você pode usar para teste de aplicativos. A máquina virtual inclui pontos de extremidade geralmente são necessários, como o PowerShell, a área de trabalho remota e WebDeploy.

### <a name="to-create-a-web-project-and-a-virtual-machine-for-debugging"></a>Para criar um projeto da web e uma máquina virtual para depuração

1. No Visual Studio, crie um novo aplicativo Web ASP.NET.

2. Na caixa de diálogo Novo projeto ASP.NET, na seção do Azure, escolha **Máquina Virtual** na caixa de listagem suspensa. Deixe o **criar recursos remotos** caixa de seleção marcada. Selecione **Okey** para continuar.

    O **criar a máquina virtual no Azure** caixa de diálogo é exibida.

    ![Criar caixa de diálogo do projeto de web do ASP.NET](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746723.png)

    **Observação:** você será solicitado a entrar sua conta do Azure se você ainda não entrou no.

3. Selecione as várias configurações para a máquina virtual e, em seguida, selecione **Okey**. Ver [máquinas virtuais](http://go.microsoft.com/fwlink/?LinkId=623033) para obter mais informações.

    O nome inserido para o nome DNS será o nome da máquina virtual.

    ![Criar a máquina virtual na caixa de diálogo do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746724.png)

    O Azure cria a máquina virtual e provisiona e configura os pontos de extremidade, como área de trabalho remota e implantação da Web

4. Depois que a máquina virtual está totalmente configurada, selecione o nó da máquina virtual no Gerenciador de servidores.

5. Abra o menu de contexto e selecione **Ativar depuração**. Quando for perguntado se você tiver certeza se você quiser habilitar a depuração na máquina virtual, selecione **Sim**.

    O Azure instala o extensão de depuração remota para a máquina virtual para habilitar a depuração.

    ![Comando depuração habilitada para máquina virtual](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746720.png)

    ![Log de atividades do Azure](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746721.png)

6. Publicar seu projeto, conforme descrito na [como: implantar um projeto Web usando um único clique publicação no Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx). Como você deseja depurar na máquina virtual, na **configurações** página do **publicar na Web** assistente, selecione **depurar** como a configuração. Isso garante que os símbolos de código estão disponíveis durante a depuração.

    ![Configurações de publicação](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718349.png)

7. No **opções de publicação do arquivo**, selecione **remover arquivos adicionais no destino** se o projeto já tiver sido implantado em um momento anterior.

8. Depois de publicar o projeto, no menu de contexto da máquina virtual no Gerenciador de servidores, selecione **Anexar depurador...**

    O Azure obtém uma lista dos processos na máquina virtual e os mostra na anexar à caixa de diálogo de processo.

    ![Comando Anexar depurador](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC746722.png)

9. No **anexar ao processo** caixa de diálogo, selecione **selecione** para limitar a lista de resultados para mostrar apenas os tipos de código que você deseja depurar. Você pode depurar código gerenciado de 32 bits ou 64 bits, o código nativo ou ambos.

    ![Selecione a caixa de diálogo de tipo de código](./media/vs-azure-tools-debug-cloud-services-virtual-machines/IC718346.png)

10. Selecione os processos que você deseja depurar na máquina virtual e, em seguida, selecione **Attach**. Por exemplo, você pode escolher o processo w3wp.exe se quiser depurar um aplicativo web na máquina virtual. Ver [depurar um ou mais processos no Visual Studio](https://msdn.microsoft.com/library/jj919165.aspx) para obter mais informações.

## <a name="next-steps"></a>Próximas etapas

* Use **Intellitrace** para coletar um log de chamadas e eventos de um servidor de versão. Ver [depurando um serviço de nuvem publicado com o IntelliTrace e o Visual Studio](http://go.microsoft.com/fwlink/?LinkID=623016).

* Use **diagnóstico do Azure** para registrar as informações detalhadas do código em execução nas funções, se as funções estão em execução no ambiente de desenvolvimento ou no Azure. Ver [coletando dados de log usando o diagnóstico do Azure](http://go.microsoft.com/fwlink/p/?LinkId=400450).
