---
title: ALM (Gerenciamento do Ciclo de Vida do Aplicativo) com aplicativos do Unity | Microsoft Docs
ms.date: 08/21/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: 2dc61e63-9ba2-4c16-b1ad-f46249e576b6
author: conceptdev
ms.author: crdun
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: 41e27d2d7a3fc79695fa1d476a76e199348c5320
ms.sourcegitcommit: 28909340cd0a0d7cb5e1fd29cbd37e726d832631
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44320885"
---
# <a name="devops-with-unity-apps"></a>DevOps com aplicativos do Unity

Desenvolver aplicativos para plataformas modernas envolve muito mais atividades do que apenas escrever código. Essas atividades, conhecidas como DevOps (desenvolvimento + operações), abrangem o ciclo de vida completo do aplicativo e incluem trabalhos de planejamento e acompanhando, elaboração e implementação de código, gerenciamento de um repositório de código-fonte, execução de builds, gerenciamento de integrações e implantações contínuas, testes (incluindo testes de unidade e testes de IU), execução de várias formas de diagnóstico em ambientes de desenvolvimento e produção e monitoramento de desempenho do aplicativo e dos comportamentos do usuário em tempo real por meio de telemetria e análise.

O Visual Studio, com o Azure DevOps Services e o Team Foundation Server, oferece uma variedade de funcionalidades de DevOps. Muitas delas são aplicáveis a projetos multiplataforma, incluindo jogos e aplicativos gráficos de imersão criados com o Unity, principalmente ao usar C# como linguagem de script. No entanto, como o Unity tem seus próprios ambiente de desenvolvimento e mecanismo de tempo de execução, uma série de recursos de DevOps não se aplicam como se aplicariam a outros tipos de projetos criados no Visual Studio.

As tabelas a seguir identificam como os recursos de DevOps no Visual Studio aplicam-se ou não se aplicam ao trabalhar com o Unity. Consulte a documentação vinculada para obter detalhes sobre os recursos em si.

## <a name="agile-tools"></a>Ferramentas agile

Link de referência: [About Agile tools and Agile project management](/azure/devops/boards/backlogs/overview?view=vsts) (Sobre as ferramentas Agile e o gerenciamento de projetos Agile) (usando o Azure Boards ou o TFS, incluindo o Team Explorer Everywhere)

Comentário Geral: todos os recursos de planejamento e acompanhamento são independentes do tipo de projeto e de linguagens de codificação.

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|Gerenciar listas de pendências e sprints|Sim||
|Acompanhamento de trabalho|Sim||
|Colaboração da sala da equipe|Sim||
|Quadros kanban|Sim||
|Relatar e visualizar o progresso|Sim||

## <a name="modeling"></a>Modelagem

Link de referência: **[Analisar e modelar a arquitetura](../modeling/analyze-and-model-your-architecture.md)**

Comentário geral: embora esses recursos de design sejam independentes da linguagem de codificação ou funcionem com linguagens .NET como C#, eles operam em um paradigma de aplicativo tradicional com hierarquias de objeto e relações de classe. Projetar um jogo no Unity envolve um paradigma totalmente diferente, ou seja, as relações de objetos gráficos, sons, sombreadores, scripts e assim por diante. Por esse motivo, as ferramentas do diagrama de modelagem do Visual Studio não são particularmente relevantes para a totalidade de um projeto do Unity. Eles poderiam ser usados para gerenciar relações em scripts C#, mas essa é apenas uma parte do todo.

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|Diagramas de sequência|Não||
|Grafos de dependência|Não||
|Hierarquia de chamadas|Não||
|Designer de Classe|Não||
|Gerenciador de arquitetura|Não||
|Diagramas UML (caso de uso, atividade, classe, componente, sequência e DSL)|Não||
|Diagramas de camada|Não||
|Validação da camada|Não||

## <a name="code"></a>Código

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|[Usar o TFVC (Controle de Versão do Team Foundation)](/azure/devops/repos/tfvc/overview?view=vsts) ou o Azure Repos|Sim|Projetos do Unity são simplesmente uma coleção de arquivos que podem ser colocados em sistemas de controle de versão como qualquer outro projeto, mas há algumas considerações especiais descritas após esta tabela.|
|[Introdução ao GIT no Azure Repos](/azure/devops/repos/git/gitquickstart?view=vsts&tabs=visual-studio)|Sim|Consulte as observações após a tabela.|
|[Melhorar a qualidade do código](../test/improve-code-quality.md)|Sim||
|[Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md)|Sim||
|[Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)|Sim||

Considerações especiais para controle de versão com o Unity:

1. O Unity acompanha metadados sobre ativos de jogos em uma única biblioteca opaca que está oculta por padrão. Para manter arquivos e metadados em sincronia, é necessário tornar os metadados visíveis e armazená-lo em partes mais gerenciáveis. Para obter detalhes, consulte [Uso de sistemas de controle de versão externo com o Unity](http://docs.unity3d.com/Manual/ExternalVersionControlSystemSupport.html) (documentação do Unity).

2. Nem todos os arquivos e pastas em um projeto do Unity são apropriados para controle do código-fonte, como também é descrito no link acima. As pastas Ativos e ProjectSettings devem ser adicionadas, mas as pastas Biblioteca e Temp, não. Para obter uma lista adicional de arquivos gerados não entrariam no controle do código-fonte, consulte a discussão [Como usar Git para controle do código-fonte Unity3D?](http://stackoverflow.com/questions/18225126/how-to-use-git-for-unity3d-source-control) em StackOverflow. Muitos desenvolvedores têm publicaram sobre assunto independentemente em seus blogs.

3. Ativos binários em um projeto do Unity, como texturas ou arquivos de áudio, podem ocupar uma grande quantidade de armazenamento. Vários sistemas de controle do código-fonte, como Git, armazenam uma cópia única de um arquivo para cada alteração feita, mesmo que a alteração afete apenas uma pequena parte do arquivo. Isso pode fazer o repositório Git ficar inflado. Para resolver isso, os desenvolvedores do Unity geralmente optam por adicionar somente ativos finais ao repositório e usar uma maneira diferente de manter um histórico de trabalho de seus ativos, como OneDrive, DropBox ou git-annex. Essa abordagem funciona porque esses ativos geralmente não precisam ter controle de versão ao longo das alterações do código-fonte. Os desenvolvedores normalmente também definem o Modo de Serialização de Ativo como Forçar Texto no editor do projeto para armazenar arquivos de cena no texto e não no formato binário, o que permite mesclagens no controle do código-fonte. Para obter detalhes, consulte [Configurações do Editor](http://docs.unity3d.com/Manual/class-EditorManager.html) (documentação do Unity).

## <a name="build"></a>Build

Link de referência: **[Azure Pipelines](/azure/devops/pipelines/index?view=vsts)**

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|TFS (Team Foundation Server) local|Possível|Projetos do Unity são criados por meio do ambiente do Unity e não por meio do sistema de build do Visual Studio (compilar dentro de Ferramentas do Visual Studio para Unity compilará os scripts, mas não produzirá um executável). É possível [compilar projetos do Unity da linha de comando](http://docs.unity3d.com/Manual/CommandLineArguments.html) (documentação do Unity), de modo que seja possível configurar um processo MSBuild em um servidor TFS para executar os comandos do Unity apropriados, desde que o Unity em si esteja instalado no computador.<br /><br /> O Unity também oferece o [Build de Nuvem Unity](https://build.cloud.unity3d.com/landing/), que monitora um repositório Git ou SVN e executa compilações periódicas. No momento, ele não funciona com o TFVC nem o Azure DevOps Services.|
|Servidor de build local vinculado ao Azure DevOps Services|Possível|Dadas as mesmas condições acima, ainda é possível direcionar builds disparados por meio do Azure DevOps Services para uso em um computador com TFS local. Consulte [Build and release agents](/azure/devops/pipelines/agents/agents?view=vsts) (Agentes de build e de versão) para obter instruções.|
|Serviço de controlador hospedado do Azure DevOps Services|Não|Atualmente, não há suporte para compilações do Unity.|
|Compilar definições com pré e pós-scripts|Sim|Uma definição de build personalizada que usa a linha de comando do Unity para executar um build também pode ser configurada para scripts de pré e pós-build.|
|Integração contínua incluindo check-ins restritos|Sim|Check-ins restritos somente para TFVC, uma vez que Git funciona em um modelo de solicitação pull, em vez de check-ins.|

## <a name="test"></a>Teste

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|Planejando testes, criando casos de teste e organizando conjuntos de testes|Sim||
|Teste manual|Sim||
|Gerenciador de Teste (testes de gravação e reprodução)|Somente dispositivos Windows e emuladores Android||
|Cobertura de código|N/D|Não se aplica, uma vez que o teste de unidade acontece dentro do Unity e não no Visual Studio, consulte abaixo.|
|[Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)|No Unity, mas não no Visual Studio|O Unity fornece a própria estrutura de teste de unidade como parte das [Ferramentas de Teste do Unity](https://www.assetstore.unity3d.com/en/#!/content/13802) (Unity Asset Store). Resultados de teste de unidade são relatados dentro do Unity e não aparecerão no Visual Studio.|
|[Usar a automação de interface do usuário para testar seu código](../test/use-ui-automation-to-test-your-code.md)|Não|Os testes de IU codificados dependem de controles legíveis na interface do usuário do aplicativo. Os aplicativos Unity são gráficos por natureza e, assim, o conteúdo não é legível para ferramentas de teste de IU codificado.|

## <a name="improve-code-quality"></a>Melhorar a qualidade do código

Link de referência: **[Melhorar a qualidade do código](../test/improve-code-quality.md)**

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|[Analisar a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|Sim|Pode analisar o código de script C# no Visual Studio.|
|[Localizar código duplicado usando detecção de clone de código](https://msdn.microsoft.com/library/hh205279.aspx)|Sim|Pode analisar o código de script C# no Visual Studio.|
|[Medir complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|Sim|Pode analisar o código de script C# no Visual Studio.|
|[Gerenciador de Desempenho](../profiling/performance-explorer.md)|Não|Use o [Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) (site do Unity).|
|[Analisar problemas de memória do .NET Framework](https://msdn.microsoft.com/library/dn342825.aspx)|Não|Ferramentas do Visual Studio não têm ganchos na estrutura Mono (como usado pelo Unity) para a criação de perfil. Use o [Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) (documentação do Unity).|

## <a name="release-management"></a>Gerenciamento de liberações

Link de referência: [Build e versão no Azure Pipelines e no TFS](/azure/devops/pipelines/overview?view=vsts)

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|Gerenciar processos de versão|Sim||
|Implantação para servidores para carregamento lateral por meio de scripts|Sim||
|Carregar para a loja de aplicativos|Parcial|Estão disponíveis extensões que podem automatizar esse processo para algumas lojas de aplicativos. Consulte [Extensões para o Azure DevOps Services](https://marketplace.visualstudio.com/VSTS); por exemplo, a [extensão para Google Play](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play).|

## <a name="monitor-with-hockeyapp"></a>Monitorar com HockeyApp

Link de referência: **[Monitorar com HockeyApp](https://www.hockeyapp.net/features/)**

|Recurso|Tem suporte com o Unity|Comentários Adicionais|
|-------------|--------------------------|-------------------------|
|Análise de falhas, telemetria e distribuição beta|Sim|HockeyApp é útil principalmente para tratar a distribuição beta e obter relatórios de falha.<br /><br /> Para telemetria de scripts do C#, é possível usar qualquer estrutura de análise, desde que ela seja executada na versão do .NET que é usada pelo Unity. No entanto, isso permite análise somente dentro de scripts de jogos e não mais profundamente dentro do mecanismo do Unity. No momento, não há nenhum plug-in do Application Insights, mas plug-ins estão disponíveis para outras soluções de análise, como [Unity Analytics](https://www.assetstore.unity3d.com/en/#!/content/28120) e [Google Analytics](https://github.com/googleanalytics/google-analytics-plugin-for-unity). Serviços como Unity Analytics que entendem a natureza de um projeto Unity obviamente fornecerão análise muito mais significativa do que estruturas genéricas.|
