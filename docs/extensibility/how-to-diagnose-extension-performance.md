---
title: 'Como: diagnosticar o desempenho da extensão | Microsoft Docs'
ms.date: 11/08/2016
ms.topic: how-to
ms.assetid: 46b0a1e3-7e69-47c9-9d8d-a1815d6c3896
author: BertanAygun
ms.author: bertaygu
manager: jillfra
ms.workload:
- bertaygu
ms.openlocfilehash: 542d8a6d6d90091aa7a800ef18f847fea6b1a81c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905911"
---
# <a name="measuring-extension-impact-in-startup"></a>Medindo o impacto da extensão na inicialização

## <a name="focus-on-extension-performance-in-visual-studio-2017"></a>Concentre-se no desempenho da extensão no Visual Studio 2017

Com base nos comentários dos clientes, uma das áreas de enfoque da versão 2017 do Visual Studio foi a inicialização e o desempenho de carregamento da solução. Como equipe da plataforma do Visual Studio, trabalhamos para melhorar o desempenho de inicialização e de carregamento da solução. Em geral, nossas medidas sugerem que as extensões instaladas também podem ter um impacto considerável nesses cenários.

Para ajudar os usuários a entender esse impacto, adicionamos um novo recurso no Visual Studio para notificar os usuários sobre extensões lentas. Às vezes, o Visual Studio detecta uma nova extensão que reduz a carga ou a inicialização da solução. Quando um retardamento for detectado, os usuários verão uma notificação no IDE apontando-os para a nova caixa de diálogo "gerenciar o desempenho do Visual Studio". Essa caixa de diálogo também pode ser acessada pelo menu ajuda para procurar extensões detectadas anteriormente.

![gerenciar o desempenho do Visual Studio](media/manage-performance.png)

Este documento tem como objetivo ajudar os desenvolvedores de extensão a descrever como o impacto da extensão é calculado. Este documento também descreve como o impacto da extensão pode ser analisado localmente. A análise local do impacto da extensão determinará se uma extensão pode ser mostrada como uma extensão de impacto no desempenho.

> [!NOTE]
> Este documento se concentra no impacto das extensões na inicialização e no carregamento da solução. As extensões também afetam o desempenho do Visual Studio quando fazem com que a interface do usuário fique sem resposta. Para obter mais informações sobre este tópico, consulte [como diagnosticar atrasos de interface do usuário causados por extensões](how-to-diagnose-ui-delays-caused-by-extensions.md).

## <a name="how-extensions-can-impact-startup"></a>Como as extensões podem afetar a inicialização

Uma das maneiras mais comuns de extensões de afetar o desempenho da inicialização é escolher a carga automática em um dos contextos de interface do usuário de inicialização conhecidos, como NoSolutionExists ou ShellInitialized. Esses contextos de interface do usuário são ativados durante a inicialização. Todos os pacotes que incluem o `ProvideAutoLoad` atributo em sua definição com esses contextos serão carregados e inicializados nesse momento.

Quando medimos o impacto de uma extensão, nos concentramos principalmente no tempo gasto por essas extensões que optam por carregar automaticamente os contextos acima. Os tempos medidos incluem, mas não se limitando a:

* Carregamento de assemblies de extensão para pacotes síncronos
* Tempo gasto no construtor de classe de pacote para pacotes síncronos
* Tempo gasto no método de inicialização de pacote (ou SetSite) para pacotes síncronos
* Para pacotes assíncronos, as operações acima são executadas no thread em segundo plano.  Como tal, as operações são excluídas do monitoramento.
* Tempo gasto em qualquer trabalho assíncrono agendado durante a inicialização do pacote para execução no thread principal
* Tempo gasto em manipuladores de eventos, especificamente a ativação de contexto inicializada por shell ou a alteração de estado zumbi do Shell
* A partir do Visual Studio 2017 atualização 3, também iniciaremos o tempo de monitoramento gasto em chamadas ociosas antes do Shell ser inicializado. Operações longas em manipuladores ociosos também causam IDE sem resposta e contribuem para o tempo de inicialização percebido pelo usuário.

Nós adicionamos muitos recursos a partir do Visual Studio 2015. Esses recursos ajudam a remover a necessidade de pacotes para carregar automaticamente. Os recursos também adiam a necessidade de que os pacotes sejam carregados em casos mais específicos. Esses casos incluem exemplos em que os usuários teriam mais certeza de usar a extensão ou reduzir um impacto de extensão ao carregar automaticamente.

Você pode encontrar mais detalhes sobre esses recursos nos seguintes documentos:

[Contextos de IU baseados em regras](how-to-use-rule-based-ui-context-for-visual-studio-extensions.md): um mecanismo mais rico baseado em regras criado com base em contextos de interface do usuário permite que você crie contextos personalizados com base em tipos de projeto, tipos e atributos. Contextos personalizados podem ser usados para carregar um pacote durante cenários mais específicos. Esses cenários específicos incluem a presença de um projeto com um recurso específico em vez da inicialização. Os contextos personalizados também permitem que [a visibilidade do comando seja vinculada a um contexto personalizado](visibilityconstraints-element.md) com base nos componentes do projeto ou em outros termos disponíveis. Esse recurso elimina a necessidade de carregar um pacote para registrar um manipulador de consulta de status de comando.

[Suporte a pacotes assíncronos](how-to-use-asyncpackage-to-load-vspackages-in-the-background.md): a nova classe base AsyncPackage no Visual Studio 2015 permite que pacotes do Visual Studio sejam carregados em segundo plano de forma assíncrona se a carga do pacote foi solicitada por um atributo de carregamento automático ou uma consulta de serviço assíncrono. Esse carregamento em segundo plano permite que o IDE permaneça responsivo. O IDE é responsivo mesmo enquanto a extensão é inicializada em cenários de plano de fundo e críticos, como a inicialização e o carregamento da solução não seriam afetados.

[Serviços assíncronos](how-to-provide-an-asynchronous-visual-studio-service.md): com suporte a pacotes assíncronos, também Adicionamos suporte para consultar serviços de forma assíncrona e ser capaz de registrar serviços assíncronos. Mais importante, estamos trabalhando na conversão dos principais serviços do Visual Studio para dar suporte à consulta assíncrona para que a maior parte do trabalho em uma consulta assíncrona ocorra em threads em segundo plano. SComponentModel (host do MEF do Visual Studio) é um dos principais serviços que agora dá suporte à consulta assíncrona para permitir que as extensões ofereçam suporte completamente ao carregamento assíncrono.

## <a name="reducing-impact-of-auto-loaded-extensions"></a>Reduzindo o impacto das extensões carregadas automaticamente

Se um pacote ainda precisar ser carregado automaticamente na inicialização, é importante minimizar o trabalho feito durante a inicialização do pacote. Minimizar o trabalho de inicialização do pacote reduz as chances de a extensão afetar a inicialização.

Alguns exemplos que poderiam fazer com que a inicialização do pacote sejam caros são:

### <a name="use-of-synchronous-package-load-instead-of-asynchronous-package-load"></a>Uso da carga de pacote síncrona em vez da carga de pacote assíncrona

Como os pacotes síncronos são carregados no thread principal por padrão, incentivamos os proprietários de extensão que têm pacotes carregados automaticamente para usar a classe base de pacote assíncrono, como mencionado anteriormente. A alteração de um pacote carregado automaticamente para dar suporte ao carregamento assíncrono também facilitará a resolução dos outros problemas abaixo.

### <a name="synchronous-filenetwork-io-requests"></a>Solicitações de e/s de arquivo/rede síncronas

Idealmente, qualquer solicitação de e/s de arquivo ou rede síncrona deve ser evitada no thread principal. Seu impacto dependerá do estado da máquina e poderá bloquear por longos períodos de tempo em alguns casos.

Usar o carregamento de pacote assíncrono e APIs de e/s assíncronas deve garantir que a inicialização do pacote não bloqueie o thread principal nesses casos. Os usuários também podem continuar a interagir com o Visual Studio enquanto as solicitações de e/s ocorrem em segundo plano.

### <a name="early-initialization-of-services-components"></a>Inicialização antecipada de serviços, componentes

Um dos padrões comuns na inicialização do pacote é inicializar os serviços usados pelo ou fornecidos pelo pacote no pacote `constructor` ou `initialize` método. Embora isso garanta que os serviços estejam prontos para serem usados, ele também pode adicionar custo desnecessário ao carregamento do pacote se esses serviços não forem usados imediatamente. Em vez disso, esses serviços devem ser inicializados sob demanda para minimizar o trabalho feito na inicialização do pacote.

Para serviços globais fornecidos por um pacote, você pode usar `AddService` métodos que usam uma função para inicializar o serviço lentamente somente quando ele é solicitado por um componente. Para serviços usados no pacote, você pode usar lazy \<T> ou AsyncLazy \<T> para garantir que os serviços sejam inicializados/consultados no primeiro uso.

## <a name="measuring-impact-of-auto-loaded-extensions-using-activity-log"></a>Medindo o impacto de extensões carregadas automaticamente usando o log de atividades

A partir do Visual Studio 2017 atualização 3, o log de atividades do Visual Studio agora conterá entradas para o impacto de desempenho dos pacotes durante a inicialização e a carga da solução. Para ver essas medições, você precisa abrir o Visual Studio com a opção/log e abrir o arquivo *ActivityLog.xml* .

No log de atividades, as entradas estarão na origem "gerenciar o desempenho do Visual Studio" e serão parecidas com o exemplo a seguir:

```Component: 3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c, Inclusive Cost: 2008.9381, Exclusive Cost: 2008.9381, Top Level Inclusive Cost: 2008.9381```

Este exemplo mostra que um pacote com o GUID "3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c" gastou 2008 MS na inicialização do Visual Studio. Observe que o Visual Studio considera o custo de nível superior como o número principal ao calcular o impacto de um pacote, pois essa seria a economia que os usuários veem quando desabilitam a extensão para esse pacote.

## <a name="measuring-impact-of-auto-loaded-extensions-using-perfview"></a>Medindo o impacto de extensões carregadas automaticamente usando PerfView

Embora a análise de código possa ajudar a identificar os caminhos de código que podem retardar a inicialização do pacote, você também pode utilizar o rastreamento usando aplicativos como o PerfView para entender o impacto de uma carga de pacote na inicialização do Visual Studio.

PerfView é uma ferramenta de rastreamento de todo o sistema. Essa ferramenta o ajudará a entender os caminhos ativos em um aplicativo devido ao uso da CPU ou ao bloqueio de chamadas do sistema. Veja abaixo um exemplo rápido de como analisar uma extensão de exemplo usando o PerfView disponível no [centro de download da Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=28567).

**Código de exemplo:**

Este exemplo é baseado no código de exemplo abaixo, que é projetado para mostrar algumas causas de atraso comuns:

```csharp
protected override void Initialize()
{
    // Initialize a class from another assembly as an example
    MakeVsSlowServiceImpl service = new MakeVsSlowServiceImpl();

    // Costly work in main thread involving file IO
    string systemPath = Environment.GetFolderPath(Environment.SpecialFolder.Windows);
    foreach (string file in Directory.GetFiles(systemPath))
    {
        DateTime creationDate = File.GetCreationTime(file);
    }

    // Costly work after shell is initialized. This callback executes on main thread
    KnownUIContexts.ShellInitializedContext.WhenActivated(() =>
    {
        DoMoreWork();
    });

    // Start async work on background thread
    DoAsyncWork().Forget();
}

private async Task DoAsyncWork()
{
    // Switch to background thread to do expensive work
    await TaskScheduler.Default;
    System.Threading.Thread.Sleep(500);
}

private void DoMoreWork()
{
    // Costly work
    System.Threading.Thread.Sleep(500);
    // Blocking call to an asynchronous work.
    ThreadHelper.JoinableTaskFactory.Run(async () => { await DoAsyncWork(); });
}
```

**Gravando um rastreamento com PerfView:**

Depois de configurar seu ambiente do Visual Studio com sua extensão instalada, você pode registrar um rastreamento de inicialização abrindo PerfView e abrindo a caixa de diálogo **Collect** no menu **coletar** .

![menu de coleta de Perfview](media/perfview-collect-menu.png)

As opções padrão fornecerão pilhas de chamadas para o consumo de CPU, mas como estamos interessados no tempo de bloqueio também, você deve habilitar pilhas de **tempo de thread** . Quando as configurações estiverem prontas, você poderá clicar em **Iniciar coleta** e abrir o Visual Studio após a gravação ser iniciada.

Antes de parar a coleta, você deseja verificar se o Visual Studio está totalmente inicializado, se a janela principal está totalmente visível e se sua extensão tem alguma peça da interface do usuário que mostra automaticamente, elas também estão visíveis. Quando o Visual Studio é totalmente carregado e sua extensão é inicializada, você pode interromper a gravação para analisar o rastreamento.

**Analisando um rastreamento com PerfView:**

Após a conclusão da gravação, o PerfView abrirá automaticamente o rastreamento e expandirá as opções.

Para os fins deste exemplo, estamos interessados principalmente na exibição de **pilhas de tempo do thread** , que pode ser encontrada em **grupo avançado**. Essa exibição mostrará o tempo total gasto em um thread por um método, incluindo tempo de CPU e tempo bloqueado, como e/s de disco ou aguardando identificadores.

 ![pilhas de tempo de thread](media/perfview-thread-time-stacks.png)

 Ao abrir a exibição **pilhas de tempo de thread** , você deve escolher o processo **devenv** para iniciar a análise.

O PerfView tem orientações detalhadas sobre como ler pilhas de tempo de thread em seu próprio menu de ajuda para uma análise mais detalhada. Para fins deste exemplo, queremos filtrar essa exibição mais detalhadamente apenas incluindo pilhas com nosso nome de módulo de pacotes e thread de inicialização.

1. Defina **GroupPats** como vazio texto para remover qualquer agrupamento adicionado por padrão.
2. Defina **IncPats** para incluir parte do seu nome de assembly e do thread de inicialização, além do filtro de processo existente. Nesse caso, deve ser **devenv; Thread de inicialização; MakeVsSlowExtension**.

Agora, a exibição mostrará apenas o custo associado aos assemblies relacionados à extensão. Nessa exibição, qualquer hora listada na coluna **Inc (custo inclusivo)** do thread de inicialização está relacionada à nossa extensão filtrada e afetará a inicialização.

Para o exemplo acima, algumas pilhas de chamadas interessantes seriam:

1. E/s usando `System.IO` classe: embora o custo inclusivo desses quadros possa não ser muito caro no rastreamento, eles são uma causa potencial de um problema, uma vez que a velocidade de e/s de arquivo varia de máquina para máquina.

   ![quadros de e/s do sistema](media/perfview-system-io-frames.png)

2. Bloqueio de chamadas aguardando outro trabalho assíncrono: nesse caso, o tempo inclusivo representaria a hora em que o thread principal é bloqueado na conclusão do trabalho assíncrono.

   ![bloqueio de quadros de chamada](media/perfview-blocking-call-frames.png)

Uma das outras exibições no rastreamento que será útil para determinar o impacto será as pilhas de **carregamento de imagem**. Você pode aplicar os mesmos filtros aplicados à exibição de **pilhas de tempo de thread** e descobrir todos os assemblies carregados por causa do código executado pelo seu pacote carregado automaticamente.

É importante minimizar o número de assemblies carregados dentro de uma rotina de inicialização de pacote, pois cada assembly adicional envolverá e/s de disco extra, o que pode retardar a inicialização consideravelmente em máquinas mais lentas.

## <a name="summary"></a>Resumo

A inicialização do Visual Studio tem sido uma das áreas com as quais continuamente obtemos comentários. Nosso objetivo, como mencionado anteriormente, é que todos os usuários tenham uma experiência de inicialização consistente, independentemente dos componentes e extensões instalados. Gostaríamos de trabalhar com proprietários de extensão para ajudá-los a atingir essa meta. As diretrizes acima devem ser úteis para entender o impacto de extensões na inicialização e evitar a necessidade de carregá-la ou carregá-la de forma assíncrona para minimizar o impacto na produtividade do usuário.
