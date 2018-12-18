---
title: 'Como: diagnosticar o desempenho da extensão | Microsoft Docs'
ms.custom: ''
ms.date: 11/08/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 46b0a1e3-7e69-47c9-9d8d-a1815d6c3896
author: BertanAygun
ms.author: bertaygu
manager: douge
ms.workload:
- bertaygu
ms.openlocfilehash: d1f2942c9f5987a686226c94e9764b8ab6300050
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49934919"
---
# <a name="measuring-extension-impact-in-startup"></a>Medindo o impacto de extensão na inicialização

## <a name="focus-on-extension-performance-in-visual-studio-2017"></a>O foco no desempenho de extensão no Visual Studio 2017

Com base nos comentários dos clientes, um das áreas de foco para a versão do Visual Studio 2017 tem sido o desempenho de carga de solução e de inicialização. Como a equipe da plataforma Visual Studio, temos trabalhado como melhorar o desempenho de carga de solução e de inicialização. Em geral, nossa medidas sugerem extensões instaladas também podem ter um impacto considerável sobre esses cenários.

Para ajudar os usuários a compreender esse impacto, adicionamos um novo recurso no Visual Studio para notificar os usuários de extensões lentas. Às vezes, o Visual Studio detecta uma nova extensão lentidão na inicialização ou a carga de solução. Quando uma lentidão é detectada, os usuários verão uma notificação no IDE que aponta para a nova caixa de diálogo "Gerenciar desempenho do Visual Studio". Essa caixa de diálogo também sempre pode ser acessada pelo menu de ajuda para procurar extensões detectadas anteriormente.

![gerenciar o desempenho do Visual Studio](media/manage-performance.png)

Este documento tem como objetivo ajudar os desenvolvedores de extensão, descrevendo como o impacto de extensão é calculado. Este documento também descreve como o impacto de extensão pode ser analisado localmente. Localmente análise do impacto da extensão determinará se uma extensão pode ser mostrada como um desempenho afetando a extensão.

> [!NOTE]
> Este documento se concentra no impacto de extensões no carregamento da solução e de inicialização. As extensões também afetam o desempenho do Visual Studio quando eles fazem com que a interface do usuário pare de responder. Para obter mais informações sobre esse tópico, consulte [como: atrasos de diagnóstico da interface do usuário causados pelas extensões](how-to-diagnose-ui-delays-caused-by-extensions.md).

## <a name="how-extensions-can-impact-startup"></a>Como as extensões podem afetar a inicialização

Uma das maneiras mais comuns para as extensões de impacto no desempenho de inicialização é escolhendo a carga automaticamente em um dos contextos de interface do usuário de inicialização conhecidas como NoSolutionExists ou ShellInitialized. Esses contextos de interface do usuário obterem ativados durante a inicialização. Todos os pacotes que incluem o `ProvideAutoLoad` atributo em sua definição nesses contextos será carregado e inicializado nesse momento.

Quando medimos o impacto de uma extensão, vamos nos concentrar principalmente no tempo gasto por essas extensões que optar por carregamento automático nos contextos acima. Medido tempos seriam incluem, mas não se limitam a:

* Carregamento de assemblies de extensão para pacotes síncronos
* Tempo gasto no construtor da classe de pacote para pacotes síncronos
* Tempo gasto no método de inicialização (ou SetSite) de pacote para pacotes síncronos
* Para pacotes assíncronos, as operações acima é executado no thread em segundo plano.  Dessa forma, as operações são excluídas do monitoramento.
* Tempo gasto em qualquer trabalho assíncrono agendado durante a inicialização do pacote para ser executado no thread principal
* Tempo gasto em manipuladores de eventos, especificamente o ativação de contexto de shell inicializado ou a alteração de estado de zumbi shell
* A partir da atualização 3 do Visual Studio 2017, podemos também iniciará monitorando o tempo gasto em chamadas ociosas antes que o shell é inicializado. Operações longas nos manipuladores ociosos também fazer com que o IDE não responder e contribuir com o tempo de inicialização percebido pelo usuário.

Adicionamos vários recursos, a partir do Visual Studio 2015. Esses recursos ajudam com removendo a necessidade de pacotes para carregar automaticamente. Os recursos também adiar a necessidade de pacotes para carregar a casos mais específicos. Esses casos incluem exemplos em que os usuários eram mais certos de usar a extensão ou reduzir o impacto de uma extensão ao carregar automaticamente.

Você pode encontrar mais detalhes sobre esses recursos nos seguintes documentos:

[Contextos de interface do usuário baseada em regras](how-to-use-rule-based-ui-context-for-visual-studio-extensions.md): um mecanismo mais avançado baseado em regras criado em torno de contextos de interface do usuário permite que você crie os contextos personalizados com base em tipos de projeto, tipos e atributos. Contextos personalizados podem ser usados para carregar um pacote durante a cenários mais específicos. Nesses cenários específicos incluem a presença de um projeto com uma funcionalidade específica, em vez de inicialização. Contextos personalizados também permitem [visibilidade estar vinculado a um contexto personalizado de comando](visibilityconstraints-element.md) com base em componentes do projeto ou outros termos disponíveis. Este recurso elimina a necessidade de carregar um pacote para registrar um manipulador de consulta de status do comando.

[Suporte de pacote assíncrono](how-to-use-asyncpackage-to-load-vspackages-in-the-background.md): A nova classe de base AsyncPackage no Visual Studio 2015 permite que os pacotes do Visual Studio a ser carregado em segundo plano assincronamente se carregar o pacote foi solicitado por um atributo de carga automático ou uma consulta de serviço assíncrona . Esse carregamento em segundo plano permite que o IDE permaneça responsivo. O IDE está respondendo, mesmo enquanto a extensão é inicializada em segundo plano e cenários críticos como carga de solução e de inicialização não serão afetados.

[Serviços assíncronos](how-to-provide-an-asynchronous-visual-studio-service.md): com suporte de pacote assíncrono, também adicionamos suporte para consultar serviços de forma assíncrona e ser capaz de registrar os serviços assíncronos. Mais importante é que estamos trabalhando na conversão de serviços do Visual Studio core para dar suporte à consulta assíncrona para que a maior parte do trabalho em uma consulta assíncrona ocorre em threads em segundo plano. SComponentModel (host do MEF do Visual Studio) é um dos principais serviços que agora dá suporte à consulta assíncrona para permitir extensões dar suporte a carregamento assíncrono completamente.

## <a name="reducing-impact-of-auto-loaded-extensions"></a>Reduzir o impacto de auto carregado extensões

Se um pacote precisar ser automaticamente carregado na inicialização, é importante minimizar o trabalho realizado durante a inicialização do pacote. Minimizar o trabalho de inicialização do pacote reduz as chances de extensão que afetam a inicialização.

Alguns exemplos que podem causar a inicialização do pacote a ser caro são:

### <a name="use-of-synchronous-package-load-instead-of-asynchronous-package-load"></a>Uso de carregamento do pacote síncrona em vez de carregar o pacote assíncrono

Porque síncronos pacotes são carregados no thread principal, por padrão, é recomendável que os proprietários de extensão que têm pacotes automaticamente carregado para usar a classe base do pacote assíncrono em vez disso, como mencionado anteriormente. Alterar um pacote carregado de automática para dar suporte a carregamento assíncrono também tornará mais fácil de resolver os problemas abaixo.

### <a name="synchronous-filenetwork-io-requests"></a>Solicitações de e/s de arquivo síncrono/rede

O ideal é que qualquer solicitação síncrona de e/s de arquivo ou de rede deve ser evitada no thread principal. O impacto dependerá o estado da máquina e pode bloquear por longos períodos de tempo, em alguns casos.

Usando o carregamento do pacote assíncrono e APIs de e/s assíncronas deve ter certeza de que a inicialização do pacote não bloqueia o thread principal em tais casos. Os usuários também podem continuar a interagir com o Visual Studio, enquanto as solicitações de e/s acontecem em segundo plano.

### <a name="early-initialization-of-services-components"></a>Inicialização inicial dos serviços, componentes

Um dos padrões comuns na inicialização do pacote é inicializar serviços usados pelo ou fornecido por esse pacote no pacote `constructor` ou `initialize` método. Enquanto isso garante que serviços estão prontos para serem usados, também é possível adicionar um custo desnecessário para empacotar o carregamento se esses serviços não são usados imediatamente. Em vez disso, esses serviços devem ser inicializados sob demanda para minimizar o trabalho feito na inicialização do pacote.

Para serviços globais fornecidos por um pacote, você pode usar `AddService` métodos que usam uma função lentamente inicializar o serviço apenas quando ele é solicitado por um componente. Para serviços usados dentro do pacote, você pode usar Lazy<T> ou AsyncLazy<T> para certificar-se de que os serviços são inicializados/consultada no primeiro uso.

## <a name="measuring-impact-of-auto-loaded-extensions-using-activity-log"></a>Medir o impacto de auto carregado extensões usando o log de atividades

A partir do Visual Studio 2017 atualização 3, log de atividades do Visual Studio agora contém entradas para o impacto no desempenho de pacotes durante o carregamento de solução e de inicialização. Para ver essas medidas, você precisa iniciar o Visual Studio com o parâmetro /log e abra *activitylog. XML* arquivo.

No log de atividades, as entradas estarão em fonte "Gerenciar desempenho do Visual Studio" em se parecerá com o exemplo a seguir:

```Component: 3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c, Inclusive Cost: 2008.9381, Exclusive Cost: 2008.9381, Top Level Inclusive Cost: 2008.9381```

Este exemplo mostra que um pacote com GUID "3cd7f5bf-6662-4ff0-ade8-97b5ff12f39c" gastou ms 2008 na inicialização do Visual Studio. Observe que o Visual Studio considera o custo de nível superior como o número principal ao calcular o impacto de um pacote, já que isso seria que os usuários de economia veem quando eles desabilitarem a extensão para esse pacote.

## <a name="measuring-impact-of-auto-loaded-extensions-using-perfview"></a>Medir o impacto de auto carregado extensões usando PerfView

Enquanto a análise de código pode ajudar a identificar os caminhos de código que podem reduzir a velocidade de inicialização do pacote, você também pode utilizar o rastreamento usando aplicativos como o PerfView para entender o impacto de um pacote de carga na inicialização do Visual Studio.

PerfView é uma ferramenta de rastreamento de todo o sistema. Essa ferramenta ajudará você a entender os caminhos de acesso em um aplicativo por causa de uso da CPU ou bloqueando chamadas do sistema. Abaixo está um exemplo rápido sobre como analisar uma extensão de exemplo usando PerfView disponível na [Microsoft Download Center](https://www.microsoft.com/en-us/download/details.aspx?id=28567).

**Código de exemplo:**

Este exemplo se baseia o exemplo de código a seguir, que foi projetado para mostrar algumas causas comuns de atraso de caso:

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

**Gravação de um rastreamento com PerfView:**

Depois que você configurar seu ambiente do Visual Studio com a sua extensão instalada, você pode gravar um rastreamento de inicialização abrindo o PerfView e abrindo o **coletar** caixa de diálogo da **coletar** menu.

![menu de coletar do perfview](media/perfview-collect-menu.png)

As opções padrão fornecerá as pilhas de chamadas para o consumo de CPU, mas já que estamos interessados em tempo de bloqueio, bem, você também deve habilitar **tempo de Thread** pilhas. Depois que as configurações estiverem prontas que você pode clicar em **iniciar coleta** e inicie o Visual Studio depois que a gravação é iniciada.

Antes de parar a coleta, convém certificar-se de que o Visual Studio está totalmente inicializado, a janela principal está completamente visível e se sua extensão tem alguma interface do usuário que mostram automaticamente, eles também são visíveis. Depois que o Visual Studio é completamente carregado e sua extensão é inicializada, você pode interromper a gravação para analisar o rastreamento.

**Analisando um rastreamento com PerfView:**

Concluída a gravação o PerfView automaticamente abrir o rastreamento e expanda as opções.

Para os fins deste exemplo, estamos interessados principalmente na **pilhas de tempo do Thread** modo de exibição que pode ser encontrado sob **grupo avançado**. Essa exibição mostrará o tempo total gasto em um thread por um método, incluindo o tempo de CPU e o tempo bloqueado, como e/s de disco ou aguardando identificadores.

 ![pilhas de tempo do thread](media/perfview-thread-time-stacks.png)

 Durante a abertura **pilhas de tempo do Thread** exibir, você deve escolher o **devenv** processo para iniciar a análise.

O PerfView tem orientação detalhada sobre como ler as pilhas de tempo em seu próprio menu de ajuda para uma análise mais detalhada de thread. Para fins deste exemplo, queremos filtrar essa exibição, incluindo somente as pilhas de nosso thread de inicialização e o nome de módulo pacotes.

1. Definir **GroupPats** para texto vazio para remover qualquer agrupamento adicionado por padrão.
2. Definir **IncPats** para incluir a parte de seu nome de assembly e a inicialização de Thread, além de filtro de processo existente. Nesse caso, ele deve ser **devenv; Thread de inicialização. MakeVsSlowExtension**.

Agora a exibição mostrará apenas custo que está associado com os assemblies relacionados à extensão. Nessa exibição, a qualquer momento listados na **Inc (Inclusive custo)** coluna do thread de inicialização está relacionada à nossa extensão filtrado e irá afetar a inicialização.

No exemplo acima alguns chamada interessante pilhas seria:

1. E/s usando `System.IO` classe: ao custo inclusivo desses quadros pode não ser muito caro no rastreamento, eles são uma causa potencial de um problema, pois a velocidade de e/s de arquivo irá variar de máquina para máquina.

   ![quadros de e/s do sistema](media/perfview-system-io-frames.png)

2. Bloqueando chamadas aguardando outro trabalho assíncrono: nesse caso, o tempo inclusivo representaria a hora em que o thread principal é bloqueado após a conclusão de trabalho assíncrono.

   ![quadros de chamada de bloqueio](media/perfview-blocking-call-frames.png)

Um dos outros modos de exibição no rastreamento que serão úteis para determinar o impacto será o **pilhas de carregamento de imagem**. Você pode aplicar os mesmo filtros conforme aplicado a **pilhas de tempo do Thread** visualizar e descobrir todos os assemblies carregados por causa do código executado por seu pacote de carregado automaticamente.

É importante minimizar o número de assemblies carregados dentro de uma rotina de inicialização do pacote conforme cada assembly adicional envolve a e/s de disco extra que pode reduzir a velocidade de inicialização consideravelmente em computadores mais lentos.

## <a name="summary"></a>Resumo

Inicialização do Visual Studio tem sido uma das áreas que estamos continuamente obter comentários sobre. Nosso objetivo, conforme mencionado anteriormente é para todos os usuários tenham uma inicialização consistente experiência, independentemente de componentes e extensões que eles instalaram. Gostaríamos de trabalhar com os proprietários de extensão para ajudá-los nos ajudar a alcançar essa meta. As diretrizes acima devem ser úteis em compreender um impacto de extensões na inicialização e ou evitar a necessidade de automático de carga ou carregá-lo de forma assíncrona para minimizar o impacto na produtividade do usuário.
