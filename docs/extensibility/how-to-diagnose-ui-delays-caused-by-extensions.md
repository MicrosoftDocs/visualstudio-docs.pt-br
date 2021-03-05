---
title: Diagnosticando atrasos da interface do usuário da extensão no Visual Studio | Microsoft Docs
description: O Visual Studio o notificará se os atrasos da interface do usuário puderem ser causados por uma extensão. Saiba como diagnosticar o que em seu código de extensão está causando atrasos na interface do usuário.
ms.custom: SEO-VS-2020
ms.date: 01/26/2018
ms.topic: conceptual
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload: multiple
ms.openlocfilehash: 7bc43d806595c7653421daec6efabb087cc1071c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102171351"
---
# <a name="how-to-diagnose-ui-delays-caused-by-extensions"></a>Como diagnosticar atrasos na interface do usuário causados pelas extensões

Quando a interface do usuário não responde, o Visual Studio examina a pilha de chamadas do thread da interface do usuário, começando pela folha e trabalhando em direção à base. Se o Visual Studio determinar que um quadro de pilha de chamadas pertence a um módulo que faz parte de uma extensão instalada e habilitada, ele mostrará uma notificação.

![Notificação de atraso da interface do usuário (sem resposta)](media/ui-delay-notification-in-vs.png)

A notificação informa ao usuário que o atraso da interface de usuário (ou seja, a falta de resposta na interface do usuário) pode ter sido o resultado do código de uma extensão. Ele também fornece ao usuário opções para desabilitar a extensão ou notificações futuras para essa extensão.

Este documento descreve como você pode diagnosticar o que em seu código de extensão está causando notificações de atraso da interface do usuário.

> [!NOTE]
> Não use a instância experimental do Visual Studio para diagnosticar atrasos da interface do usuário. Algumas partes da análise de pilha de chamadas necessárias para notificações de atraso da interface do usuário são desativadas ao usar a instância experimental, o que significa que as notificações de atraso da interface do usuário não podem ser mostradas.

Uma visão geral do processo de diagnóstico é a seguinte:
1. Identifique o cenário do gatilho.
2. Reinicie o VS com o log de atividades ativado.
3. Inicie o rastreamento ETW.
4. Dispare a notificação para que ela apareça novamente.
5. Interrompa o rastreamento ETW.
6. Examine o log de atividades para obter a ID de atraso.
7. Analise o rastreamento ETW usando a ID de atraso da etapa 6.

Nas seções a seguir, veremos essas etapas mais detalhadamente.

## <a name="identify-the-trigger-scenario"></a>Identificar o cenário do gatilho

Para diagnosticar um atraso na interface do usuário, primeiro você precisa identificar o que (sequência de ações) faz com que o Visual Studio mostre a notificação. Isso é para que você possa disparar a notificação posteriormente com o registro em log ativado.

## <a name="restart-vs-with-activity-logging-on"></a>Reiniciar VS com o log de atividades ativado

O Visual Studio pode gerar um "log de atividades" que fornece informações úteis ao depurar um problema. Para ativar o log de atividades no Visual Studio, abra o Visual Studio com a `/log` opção de linha de comando. Depois que o Visual Studio é iniciado, o log de atividades é armazenado no seguinte local:

```DOS
%APPDATA%\Microsoft\VisualStudio\<vs_instance_id>\ActivityLog.xml
```

Para saber mais sobre como você pode encontrar sua ID de instância do VS, consulte [ferramentas para detectar e gerenciar instâncias do Visual Studio](../install/tools-for-managing-visual-studio-instances.md). Usaremos esse log de atividades posteriormente para saber mais sobre atrasos da interface do usuário e notificações relacionadas.

## <a name="starting-etw-tracing"></a>Iniciando o rastreamento ETW

Você pode usar [Perfview](https://github.com/Microsoft/perfview/) para coletar um rastreamento de ETW. O PerfView fornece uma interface fácil de usar para coletar um rastreamento ETW e analisá-lo. Use o seguinte comando para coletar um rastreamento:

```DOS
Perfview.exe collect C:\trace.etl /BufferSizeMB=1024 -CircularMB:2048 -Merge:true -Providers:*Microsoft-VisualStudio:@StacksEnabled=true -NoV2Rundown /kernelEvents=default+FileIOInit+ContextSwitch+Dispatcher
```

Isso habilita o provedor "Microsoft-VisualStudio", que é o provedor que o Visual Studio usa para eventos relacionados a notificações de atraso da interface do usuário. Ele também especifica a palavra-chave para o provedor de kernel que o PerfView pode usar para gerar a exibição de **pilhas de tempo de thread** .

## <a name="trigger-the-notification-to-appear-again"></a>Disparar a notificação para aparecer novamente

Depois que o PerfView tiver iniciado a coleta de rastreamento, você poderá usar a sequência de ação do gatilho (da etapa 1) para que a notificação apareça novamente. Depois que a notificação é mostrada, você pode interromper a coleta de rastreamento para PerfView para processar e gerar o arquivo de rastreamento de saída.

## <a name="stop-etw-tracing"></a>Parar rastreamento ETW

Para interromper a coleta de rastreamento, basta usar o botão **parar coleção** na janela Perfview. Depois de parar a coleta de rastreamento, o PerfView processará automaticamente os eventos ETW e gerará um arquivo de rastreamento de saída.

## <a name="examine-the-activity-log-to-get-the-delay-id"></a>Examine o log de atividades para obter a ID de atraso

Conforme mencionado anteriormente, você pode encontrar o log de atividades em *%APPDATA%\Microsoft\VisualStudio \<vs_instance_id>\ActivityLog.xml*. Toda vez que o Visual Studio detecta um atraso da interface do usuário da extensão, ele grava um nó no log de atividades com `UIDelayNotifications` como a origem. Esse nó contém quatro partes de informações sobre o atraso da interface do usuário:

- A ID de atraso da interface do usuário, um número sequencial que identifica exclusivamente um atraso da interface do usuário em uma sessão do VS
- A ID da sessão, que identifica exclusivamente sua sessão do Visual Studio do início ao fim
- Se uma notificação foi ou não mostrada para o atraso da interface do usuário
- A extensão que provavelmente causou o atraso da interface do usuário

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
> Nem todos os atrasos da interface do usuário resultam em uma notificação. Portanto, você sempre deve verificar a **notificação mostrada?** valor para identificar corretamente o atraso correto da interface do usuário.

Depois de encontrar o atraso de interface do usuário correto no log de atividades, anote a ID de atraso da interface do usuário especificada no nó. Você usará a ID para procurar o evento ETW correspondente na próxima etapa.

## <a name="analyze-the-etw-trace"></a>Analisar o rastreamento ETW

Em seguida, abra o arquivo de rastreamento. Você pode fazer isso usando a mesma instância de PerfView ou iniciando uma nova instância e definindo o caminho da pasta atual no canto superior esquerdo da janela para o local do arquivo de rastreamento.

![Configurando o caminho da pasta em Perfview](media/perfview-set-path.png)

Em seguida, selecione o arquivo de rastreamento no painel esquerdo e abra-o escolhendo **abrir** no menu de contexto ou clique com o botão direito do mouse.

> [!NOTE]
> Por padrão, o PerfView gera um arquivo zip. Quando você abre o *trace.zip*, ele descompacta automaticamente o arquivo morto e abre o rastreamento. Você pode ignorar isso desmarcando a caixa **zip** durante a coleta de rastreamento. No entanto, se você estiver planejando transferir e usar rastreamentos em diferentes máquinas, é altamente recomendável desmarcar a caixa **zip** . Sem essa opção, o PDBs necessário para assemblies NGen não acompanhará o rastreamento e, portanto, os símbolos de assemblies NGen não serão resolvidos no computador de destino. (Consulte [esta postagem de blog](https://devblogs.microsoft.com/devops/creating-ngen-pdbs-for-profiling-reports/) para obter mais informações sobre PDBs para assemblies NGen.)

Pode levar vários minutos para que o PerfView processe e abra o rastreamento. Quando o rastreamento está aberto, uma lista de vários "modos de exibição" aparece sob ele.

![Exibição de Resumo de rastreamento de PerfView](media/perfview-summary-view-events-selected.png)

Primeiro, usaremos a exibição de **eventos** para obter o intervalo de tempo do atraso da interface do usuário:

1. Abra o modo de exibição **eventos** selecionando `Events` nó sob o rastreamento e escolhendo **abrir** no menu de contexto ou clique com o botão direito do mouse.
2. Selecione " `Microsoft-VisualStudio/ExtensionUIUnresponsiveness` " no painel esquerdo.
3. Pressione Enter

A seleção é aplicada e todos os `ExtensionUIUnresponsiveness` eventos são exibidos no painel direito.

![Selecionando eventos na exibição de eventos](media/perfview-event-selection.png)

Cada linha no painel direito corresponde a um atraso da interface do usuário. O evento inclui um valor de "ID de atraso" que deve corresponder à ID de atraso no log de atividades da etapa 6. Como `ExtensionUIUnresponsiveness` é acionado no final do atraso da interface do usuário, o carimbo de data/hora do evento (aproximadamente) marca a hora de término do atraso da interface do usuário. O evento também contém a duração do atraso. Podemos subtrair a duração do carimbo de data/hora final para obter o carimbo de data/hora de quando o atraso da interface do usuário começou.

![Calculando o intervalo de tempo de atraso da interface do usuário](media/ui-delay-time-range.png)

Na captura de tela anterior, por exemplo, o carimbo de data/hora do evento é 12125,679 e a duração do atraso é de 6143, 85 (MS). Assim,
* O atraso início é 12125,679-6143, 85 = 5982,594.
* O intervalo de tempo de atraso da interface do usuário é de 5982,594 a 12125,679.

Assim que tivermos o intervalo de tempo, podemos fechar o modo de exibição de **eventos** e abrir a exibição de **pilhas de tempo de thread (com atividades de StartStop)** . Essa exibição é especialmente útil porque muitas vezes as extensões que estão bloqueando o thread da interface do usuário estão apenas aguardando outros threads ou uma operação associada à e/s. Assim, a exibição da **pilha de CPU** , que é a opção go-to para a maioria dos casos, pode não capturar o tempo que o thread passa bloqueando, uma vez que ele não está usando a CPU durante esse tempo. As **pilhas de tempo de thread** resolvem esse problema mostrando corretamente o tempo bloqueado.

![Nó de pilhas de tempo (com atividades de StartStop) no modo de exibição de resumo PerfView](media/perfview-thread-time-with-startstop-activities-stacks.png)

Ao abrir a exibição **pilhas de tempo de thread** , escolha o processo **devenv** para iniciar a análise.

![Exibição de pilhas de tempo de thread para análise de atraso da interface do usuário](media/ui-delay-thread-time-stacks.png)

Na exibição **pilhas de tempo de thread** , no canto superior esquerdo da página, você pode definir o intervalo de tempo para os valores que calculamos na etapa anterior e pressionar **Enter** para que as pilhas sejam ajustadas para esse intervalo de tempo.

> [!NOTE]
> Determinar qual thread é o thread da interface do usuário (inicialização) pode ser muito intuitivo se a coleta de rastreamento for iniciada depois que o Visual Studio já estiver aberto. No entanto, os primeiros elementos na pilha do thread da interface do usuário (inicialização) são sempre prováveis DLLs do sistema operacional (*ntdll.dll* e *kernel32.dll*) seguidos por `devenv!?` e depois `msenv!?` . Essa sequência pode ajudar a identificar o thread da interface do usuário.

 ![Identificando o thread de inicialização](media/ui-delay-startup-thread.png)

Você também pode filtrar ainda mais essa exibição apenas incluindo pilhas que contêm módulos do seu pacote.

* Defina **GroupPats** como vazio texto para remover qualquer agrupamento adicionado por padrão.
* Defina **IncPats** para incluir parte do nome do assembly, além do filtro de processo existente. Nesse caso, deve ser **devenv; UIDelayR2**.

![Configurando GroupPath e IncPath na exibição de pilhas de tempo de thread](media/perfview-tts-group-path-inc-path.png)

O PerfView tem orientação detalhada no menu **ajuda** que você pode usar para identificar gargalos de desempenho em seu código. Além disso, os links a seguir fornecem mais informações sobre como utilizar as APIs de Threading do Visual Studio para otimizar seu código:

* [https://github.com/Microsoft/vs-threading/blob/master/doc/index.md](https://github.com/Microsoft/vs-threading/blob/master/doc/index.md)
* [https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md](https://github.com/Microsoft/vs-threading/blob/master/doc/cookbook_vs.md)

Você também pode usar os novos analisadores estáticos do Visual Studio para extensões (pacote NuGet [aqui](https://www.nuget.org/packages/microsoft.visualstudio.sdk.analyzers)), que fornecem orientação sobre as práticas recomendadas para escrever extensões eficientes. Consulte uma lista de analisadores do [SDK do vs](https://github.com/Microsoft/VSSDK-Analyzers/blob/master/doc/index.md) e [analisadores de Threading](https://github.com/Microsoft/vs-threading/blob/master/doc/analyzers/index.md).

> [!NOTE]
> Se não for possível resolver a falta de resposta devido a dependências das quais você não tem controle (por exemplo, se sua extensão tiver que chamar serviços síncronos VS no thread da interface do usuário), gostaríamos de saber isso. Se você for membro de nosso programa de parceiros do Visual Studio, poderá entrar em contato conosco enviando uma solicitação de suporte do desenvolvedor. Caso contrário, use a ferramenta ' relatar um problema ' para enviar seus comentários e incluir `"Extension UI Delay Notifications"` no título. Inclua também uma descrição detalhada da sua análise.
