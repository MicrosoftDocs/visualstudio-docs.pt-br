---
title: Atrasa a diagnosticar a extensão de interface do usuário no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 01/26/2018
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
author: PooyaZv
ms.author: pozandev
manager: douge
ms.workload: multiple
ms.openlocfilehash: 1bf5dba23622c5dc3d964bdac19fec210aa60b1e
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639189"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>Como: interface do usuário de diagnosticar atrasos causados pelas extensões

Quando a interface do usuário se torna sem resposta, o Visual Studio examina a pilha de chamadas do thread da interface do usuário, começando com a folha e funcionando em direção à base. Se o Visual Studio determinar que um quadro de pilha de chamadas pertence a um módulo que é parte de uma extensão instalada e habilitada, ele mostrará uma notificação.

![(Falta de resposta) notificação de atraso de interface do usuário](media/ui-delay-notification-in-vs.png)

A notificação informa ao usuário que o atraso de interface do usuário (ou seja, a falta de resposta na interface do usuário) pode ter sido o resultado do código de uma extensão. Ele também fornece o usuário com opções para desabilitar a extensão ou notificações futuras para essa extensão.

Este documento descreve como diagnosticar o que em seu código de extensão está causando as notificações de atraso de interface do usuário. 

> [!NOTE]
> Não use a instância experimental do Visual Studio para diagnosticar atrasos de interface do usuário. Algumas partes da análise de pilha de chamadas necessárias para notificações de atraso de interface do usuário são desativadas ao usar a instância experimental, que significa que as notificações de atraso de interface do usuário não podem ser mostradas.

Uma visão geral do processo de diagnóstico é da seguinte maneira:
1. Identifique o cenário de gatilho.
2. Reinicie o VS com atividade de logon.
3. Inicie o rastreamento ETW.
4. Dispare a notificação seja exibida novamente.
5. Pare o rastreamento ETW.
6. Examine o log de atividade para obter a ID de atraso.
7. Analise o rastreamento ETW usando a ID de atraso da etapa 6.

Nas seções a seguir, vamos percorrer essas etapas mais detalhadamente.

## <a name="identify-the-trigger-scenario"></a>Identificar o cenário de gatilho

Para diagnosticar um atraso de interface do usuário, primeiro você precisa identificar quais (sequência de ações) faz com que o Visual Studio mostrar a notificação. Isso está na ordem para que você pode disparar a notificação mais tarde com o log ativado.

## <a name="restart-vs-with-activity-logging-on"></a>Reinicie o VS com atividade de logon

O Visual Studio pode gerar um log de atividades"" que fornece informações úteis ao depurar um problema. Para ativar a atividade de registro em log no Visual Studio, inicie o Visual Studio com o `/log` opção de linha de comando. Depois que o Visual Studio é iniciado, o log de atividades é armazenado no seguinte local:

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

Para saber mais sobre como você pode encontrar seu VS ID da instância, consulte [ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md). Posteriormente, usaremos o log de atividades para obter mais informações sobre atrasos de interface do usuário e as notificações relacionadas.

## <a name="starting-etw-tracing"></a>Iniciar o rastreamento ETW

Você pode usar [PerfView](https://github.com/Microsoft/perfview/) para coletar um rastreamento ETW. O PerfView fornece uma interface fácil de usar para coletar um rastreamento ETW e analisá-los. Use o comando a seguir para coletar um rastreamento:

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

Isso permite que o provedor "Microsoft-VisualStudio", que é o provedor que usa o Visual Studio para eventos relacionados a notificações de atraso de interface do usuário. Ela também especifica a palavra-chave para o provedor de kernel que pode usar o PerfView para gerar o **pilhas de tempo do Thread** modo de exibição.

## <a name="trigger-the-notification-to-appear-again"></a>Disparar a notificação seja exibida novamente

Depois que o PerfView iniciou a coleta de rastreamento, você pode usar a sequência de ação de gatilho (da etapa 1) para a notificação seja exibido novamente. Quando a notificação é exibida, você pode parar a coleta de rastreamento de PerfView processar e gerar o arquivo de rastreamento de saída.

## <a name="stop-etw-tracing"></a>Parar o rastreamento ETW

Para interromper a coleta de rastreamento, basta usar o **parar a coleta** botão na janela PerfView. Depois de parar a coleta de rastreamento, o PerfView automaticamente processará os eventos ETW e gera um arquivo de rastreamento de saída.

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>Examine o log de atividades para obter a ID de atraso

Como mencionado anteriormente, você pode encontrar o log de atividades em *%APPDATA%\Microsoft\VisualStudio\<vs_instance_id > \ActivityLog.xml*. Sempre que o Visual Studio detectar uma atraso de interface do usuário de extensão, ele grava um nó para o log de atividades com `UIDelayNotifications` como a origem. Esse nó contém quatro tipos de informações sobre o atraso de interface do usuário:

- A ID de atraso de interface do usuário, um número sequencial que identifica exclusivamente um atraso de interface do usuário em uma sessão do VS
- A ID de sessão, que identifica exclusivamente a sessão do Visual Studio, do início ao fechar
- Ou não uma notificação foi exibida para o atraso de interface do usuário
- A extensão que provavelmente causado o atraso de interface do usuário

```xml
<entry>
  <record>271</record>
  <time>2018/02/03 12:02:52.867</time>
  <type>Information</type>
  <source>UIDelayNotifications</source>
  <description>A UI delay (Delay ID = 0) has been detected. (Session ID=16e49d4b-26c2-4247-ad1c-488edeb185e0; Blamed extension="UIDelayR2"; Notification shown? Yes.)</description>
</entry>
```

> [!NOTE]
> Nem todos os atrasos de interface do usuário resultam em uma notificação. Portanto, você sempre deve verificar a **notificação mostrada?** valor para identificar corretamente o atraso de interface do usuário à direita.

Depois de localizar o atraso de interface do usuário correto no log de atividades, anote a ID de atraso de interface do usuário especificada no nó. Você usará a ID para procurar o evento ETW correspondente na próxima etapa.

## <a name="analyze-the-etw-trace"></a>Analisar o rastreamento ETW

Em seguida, abra o arquivo de rastreamento. Você pode fazer isso usando a mesma instância do PerfView ou iniciar uma nova instância e definindo o caminho da pasta atual no canto superior esquerdo da janela para o local do arquivo de rastreamento.

![Definir o caminho da pasta no Perfview](media/perfview-set-path.png)

Em seguida, selecione o arquivo de rastreamento no painel esquerdo e abra-o, escolhendo **abrir** no menu de contexto ou o botão direito do mouse.

> [!NOTE]
> Por padrão o PerfView gera um arquivo Zip. Quando você abre *trace.zip*, ele descompacta o arquivo morto automaticamente e abre o rastreamento. Você pode ignorar isso desmarcando os **Zip** caixa durante a coleta de rastreamento. No entanto, se você estiver planejando transferir e usar rastreamentos em máquinas diferentes, convém desmarcando os **Zip** caixa. Sem essa opção, os PDBs necessárias para assemblies Ngen não acompanharão o rastreamento e, portanto, símbolos de assemblies Ngen não serão resolvidos no computador de destino. (Consulte [esta postagem de blog](https://blogs.msdn.microsoft.com/devops/2012/12/10/creating-ngen-pdbs-for-profiling-reports/) para obter mais informações sobre PDBs para assemblies Ngen.) 

Pode levar vários minutos para que o PerfView processar e abrir o rastreamento. Quando o rastreamento é aberto, uma lista de vários "exibições" aparecem sob ele.

![Exibição de resumo de rastreamento de PerfView](media/perfview-summary-view-events-selected.png)

Vamos primeiro usar o **eventos** modo de exibição para obter o intervalo de tempo do atraso da interface do usuário:

1. Abra o **eventos** exibição selecionando `Events` nó sob o rastreamento e escolhendo **abrir** no menu de contexto ou o botão direito do mouse.
2. Selecione "`Microsoft-VisualStudio/ExtensionUIUnresponsiveness`" no painel esquerdo.
3. Pressione Enter

A seleção é aplicada e todos os `ExtensionUIUnresponsiveness` eventos são exibidos no painel direito.

![Seleção de eventos no modo de exibição de eventos](media/perfview-event-selection.png)

Cada linha no painel direito corresponde a um atraso de interface do usuário. O evento inclui um valor de "ID do atraso" que deve corresponder a ID de atraso no log de atividades da etapa 6. Uma vez que `ExtensionUIUnresponsiveness` é acionado no final do atraso da interface do usuário, o carimbo de hora do evento (aproximadamente) as marcas a hora de término do atraso da interface do usuário. O evento também contém a duração do atraso. Podemos pode subtrair a duração do carimbo de hora de término para obter o carimbo de hora de quando o atraso de interface do usuário é iniciada.

![Calcular o intervalo de tempo do atraso da interface do usuário](media/ui-delay-time-range.png)

Na captura de tela anterior, por exemplo, o carimbo de hora do evento é 12,125.679 e a duração do atraso é 6,143.085 (ms). Assim,
* O início de atraso é 12,125.679 6,143.085 = 5,982.594.
* O intervalo de tempo de atraso de interface do usuário é 5,982.594 para 12,125.679.

Assim que tivermos o intervalo de tempo, podemos fechar do **eventos** exiba e abra o **pilhas de tempo do Thread (com atividades StartStop)** modo de exibição. Este modo de exibição é especialmente útil porque geralmente as extensões que estão bloqueando o thread de interface do usuário são simplesmente aguardando outros threads ou uma operação vinculada à e/S. Portanto, o **pilha de CPU** exibição, que é a opção ideal para a maioria dos casos, não pode capturar o tempo gasto pelo thread, pois ele não está usando a CPU durante esse período de bloqueio. O **pilhas de tempo do Thread** resolve esse problema, o tempo de mostrando bloqueado corretamente.

![Nó de pilhas de tempo (com atividades StartStop) do thread na exibição de resumo de PerfView](media/perfview-thread-time-with-startstop-activities-stacks.png)

Durante a abertura **pilhas de tempo do Thread** exibir, escolha o **devenv** processo para iniciar a análise.

![Exibição de pilhas de tempo para análise de atraso de interface do usuário do thread](media/ui-delay-thread-time-stacks.png)

No **pilhas de tempo do Thread** exibir, no canto superior esquerdo da página, você pode definir o intervalo de tempo para os valores que calculamos na etapa anterior e pressione **Enter** para que as pilhas são ajustadas para esse intervalo de tempo.

> [!NOTE]
> Determinar qual thread é a interface do usuário thread (inicialização) pode ser confuso se a coleta de rastreamento é iniciada depois que o Visual Studio já está aberto. No entanto, os primeiros elementos na pilha do thread da interface do usuário (inicialização) são mais provável sempre DLLs do sistema operacional (*Ntdll. dll* e *kernel32.dll*) seguido por `devenv!?` e, em seguida, `msenv!?` . Essa sequência pode ajudar a identificar o thread de interface do usuário.

 ![Identificando o thread de inicialização](media/ui-delay-startup-thread.png)

Você também pode filtrar essa exibição, incluindo somente as pilhas que contêm módulos do seu pacote.

* Definir **GroupPats** para texto vazio para remover qualquer agrupamento adicionado por padrão.
* Definir **IncPats** para incluir a parte do nome do assembly, além de filtro de processo existente. Nesse caso, ele deve ser **devenv; UIDelayR2**.

![Definindo GroupPath e IncPath no modo de exibição de pilhas de tempo do Thread](media/perfview-tts-group-path-inc-path.png)

PerfView tem detalhadas orientações sob o **ajudar** menu que você pode usar para identificar gargalos de desempenho em seu código. Além disso, os links a seguir fornecem mais informações sobre como utilizar o Visual Studio de threading de APIs para otimizar o código:

* [https://aka.ms/vsthreading](https://aka.ms/vsthreading)
* [https://aka.ms/vsthreadingcookbook](https://aka.ms/vsthreadingcookbook)

Você também pode usar os novo analisadores estáticos do Visual Studio para extensões (pacote do NuGet [aqui](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)), que fornecem orientação sobre as práticas recomendadas para escrever extensões eficientes. Ver uma lista dos [analisadores de SDK do VS](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md) e [threading analisadores](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md).

> [!NOTE]
> Se não for possível resolver a falta de resposta devido a dependências, você não tem controle sobre (por exemplo, se sua extensão tem que chamar VS services síncronas no thread da interface do usuário), gostaríamos de saber sobre isso. Se você for um membro do nosso programa de parceiro do Visual Studio, você pode contatar-nos enviando uma solicitação de suporte do desenvolvedor. Caso contrário, use a ferramenta de um problema de relatório para enviar seus comentários e incluir `"Extension UI Delay Notifications"` no título. Também inclua uma descrição detalhada da sua análise.
