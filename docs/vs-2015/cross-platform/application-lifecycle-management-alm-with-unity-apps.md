---
title: ALM (Gerenciamento do Ciclo de Vida do Aplicativo) com aplicativos do Unity | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2dc61e63-9ba2-4c16-b1ad-f46249e576b6
caps.latest.revision: 14
author: conceptdev
ms.author: crdun
manager: ghogen
ms.openlocfilehash: 0a39bee5517f0a4311613af336a5b8bc6e6fa00e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51760700"
---
# <a name="application-lifecycle-management-alm-with-unity-apps"></a>ALM (Gerenciamento do Ciclo de Vida do Aplicativo) com aplicativos do Unity
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Desenvolver aplicativos para plataformas modernas envolve muito mais atividades do que apenas escrever código. Essas atividades, conhecidas como DevOps (desenvolvimento + operações), abrangem o ciclo de vida completo do aplicativo e incluem trabalhos de planejando e acompanhando, elaboração e implementação de código, gerenciamento de um repositório de código-fonte, execução de compilações, gerenciamento de integrações contínuas e implantações, teste (incluindo testes de unidade e testes de interface do usuário), execução de várias formas de diagnóstico em ambientes de desenvolvimento e produção e monitoramento do desempenho do aplicativo e dos comportamentos do usuário em tempo real por meio de telemetria e análise.  
  
 O Visual Studio, junto com o Visual Studio Team Services e o Team Foundation Server, proporciona uma variedade de recursos de DevOps, também conhecidos como ALM ou Gerenciamento do Ciclo de Vida do Aplicativo. Muitos são aplicáveis aos projetos de plataforma cruzada, incluindo jogos e aplicativos gráficos de imersão criados com o Unity, especialmente ao usar C# como linguagem de script. No entanto, uma vez que o Unity tem seu próprio ambiente de desenvolvimento e o mecanismo de tempo de execução, vários recursos ALM não se aplicam como se aplicariam a outros tipos de projetos criados no Visual Studio.  
  
 As tabelas a seguir identifica como os recursos do Visual Studio ALM se aplicam ou não se aplicam ao trabalhar com o Unity. Consulte a documentação vinculada para obter detalhes sobre os recursos em si.  
  
## <a name="agile-tools"></a>Ferramentas agile  
 Link de referência: **[Trabalho](http://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** (usando o Visual Studio Team Services ou TFS, incluindo o Team Explorer Everywhere)  
  
 Comentário Geral: todos os recursos de planejamento e acompanhamento são independentes do tipo de projeto e de linguagens de codificação.  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|Gerenciar listas de pendências e sprints|Sim||  
|Acompanhamento de trabalho|Sim||  
|Colaboração da sala da equipe|Sim||  
|Quadros kanban|Sim||  
|Relatar e visualizar o progresso|Sim||  
  
## <a name="modeling"></a>Modelagem  
 Link de referência: **[Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)**  
  
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
|[Use o Controle de Versão do Team Foundation](http://msdn.microsoft.com/library/1d629052-c65d-4c5d-81eb-eaa4413fe285) ou Visual Studio Team Services|Sim|Projetos do Unity são simplesmente uma coleção de arquivos que podem ser colocados em sistemas de controle de versão como qualquer outro projeto, mas há algumas considerações especiais descritas após esta tabela.|  
|[Introdução ao Git no Team Services](http://msdn.microsoft.com/library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|Sim|Consulte as observações após a tabela.|  
|[Análise de código/melhorar a qualidade do código (referências, alterações sugeridas, etc.)](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|Sim||  
|[Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md)|Sim||  
|[Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)|Sim||  
  
 Considerações especiais para controle de versão com o Unity:  
  
1.  O Unity acompanha metadados sobre ativos de jogos em uma única biblioteca opaca que está oculta por padrão. Para manter arquivos e metadados em sincronia, é necessário tornar os metadados visíveis e armazená-lo em partes mais gerenciáveis. Para obter detalhes, consulte [Uso de sistemas de controle de versão externo com o Unity](http://docs.unity3d.com/Manual/ExternalVersionControlSystemSupport.html) (documentação do Unity).  
  
2.  Nem todos os arquivos e pastas em um projeto do Unity são apropriados para controle do código-fonte, como também é descrito no link acima. As pastas Ativos e ProjectSettings devem ser adicionadas, mas as pastas Biblioteca e Temp, não. Para obter uma lista adicional de arquivos gerados não entrariam no controle do código-fonte, consulte a discussão [Como usar Git para controle do código-fonte Unity3D?](http://stackoverflow.com/questions/18225126/how-to-use-git-for-unity3d-source-control) em StackOverflow. Muitos desenvolvedores têm publicaram sobre assunto independentemente em seus blogs.  
  
3.  Ativos binários em um projeto do Unity, como texturas ou arquivos de áudio, podem ocupar uma grande quantidade de armazenamento. Vários sistemas de controle do código-fonte, como Git, armazenam uma cópia única de um arquivo para cada alteração feita, mesmo que a alteração afete apenas uma pequena parte do arquivo. Isso pode fazer o repositório Git ficar inflado. Para resolver isso, os desenvolvedores do Unity geralmente optam por adicionar somente ativos finais ao repositório e usar uma maneira diferente de manter um histórico de trabalho de seus ativos, como OneDrive, DropBox ou git-annex. Essa abordagem funciona porque esses ativos geralmente não precisam ter controle de versão junto com as alterações do código-fonte. Os desenvolvedores normalmente também definem o Modo de Serialização de Ativo para Forçar Texto do editor do projeto para armazenar arquivos de cena no texto, em vez de no formato binário, o que permite mesclagens no controle do código-fonte. Para obter detalhes, consulte [Configurações do Editor](http://docs.unity3d.com/Manual/class-EditorManager.html) (documentação do Unity).  
  
## <a name="build"></a>Build  
 Link de referência: **[Build](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)**  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|Servidor TFS local|Possível|Projetos do Unity são criados por meio do ambiente do Unity e não por meio do sistema de build do Visual Studio (compilar dentro de Ferramentas do Visual Studio para Unity compilará os scripts, mas não produzirá um executável). É possível [compilar projetos do Unity da linha de comando](http://docs.unity3d.com/Manual/CommandLineArguments.html) (documentação do Unity), de modo que seja possível configurar um processo MSBuild em um servidor TFS para executar os comandos do Unity apropriados, desde que o Unity em si esteja instalado no computador.<br /><br /> O Unity também oferece o [Build de Nuvem Unity](https://build.cloud.unity3d.com/landing/), que monitora um repositório Git ou SVN e executa compilações periódicas. No momento, não funciona com o Controle de Versão do Team Foundation nem Visual Studio Team Services.|  
|Servidor de build local vinculado ao Visual Studio Team Services|Possível|Dadas as mesmas condições acima, mais possível, ainda, direcionar compilações disparadas por meio do Visual Studio Team Services para uso em um computador TFS local.  Consulte [Servidor de build](http://msdn.microsoft.com/library/2d258a0a-f178-4e93-9da1-eba61151af3c) para obter instruções.|  
|Serviço de controlador hospedado do Visual Studio Team Services|Não|Atualmente, não há suporte para compilações do Unity.|  
|Compilar definições com pré e pós-scripts|Sim|Uma definição de build personalizada que usa a linha de comando do Unity para executar um build também pode ser configurada para scripts de pré e pós-build.|  
|Integração contínua incluindo check-ins restritos|Sim|Check-ins restritos somente para TFVC, uma vez que Git funciona em um modelo de solicitação pull, em vez de check-ins.|  
  
## <a name="testing"></a>Testes  
 Link de referência: **[Testando o aplicativo](http://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)**  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|Planejando testes, criando casos de teste e organizando conjuntos de testes|Sim||  
|Teste manual|Sim||  
|Gerenciador de Teste (testes de gravação e reprodução)|Somente dispositivos Windows e emuladores Android||  
|Cobertura de código|N/D|Não se aplica, uma vez que o teste de unidade acontece dentro do Unity e não no Visual Studio, consulte abaixo.|  
|[Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)|No Unity, mas não no Visual Studio|O Unity fornece a própria estrutura de teste de unidade como parte das [Ferramentas de Teste do Unity](https://www.assetstore.unity3d.com/en/#!/content/13802) (Unity Asset Store). Resultados de teste de unidade são relatados dentro do Unity e não aparecerão no Visual Studio.|  
|[Usar automação de interface do usuário para testar código](../test/use-ui-automation-to-test-your-code.md)|Não|Testes de UI codificados dependem de controles legíveis na interface do usuário do aplicativo; aplicativos Unity são gráficos por natureza e, assim, o conteúdo não é legível pelas ferramentas de teste de IU codificado.|  
  
## <a name="improve-code-quality"></a>Melhorar a qualidade do código  
 Link de referência: **[Melhorar a qualidade do código](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)**  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|[Analisando a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|Sim|Pode analisar o código de script C# no Visual Studio.|  
|[Localizando código duplicado usando detecção de clone de código](http://msdn.microsoft.com/library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|Sim|Pode analisar o código de script C# no Visual Studio.|  
|[Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|Sim|Pode analisar o código de script C# no Visual Studio.|  
|[Gerenciador de Desempenho](../profiling/performance-explorer.md)|Não|Use o [Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) (site do Unity).|  
|[Analisar problemas de memória do .NET Framework](../misc/analyze-dotnet-framework-memory-issues.md)|Não|Ferramentas do Visual Studio não têm ganchos na estrutura Mono (como usado pelo Unity) para a criação de perfil. Use o [Unity Profiler](http://docs.unity3d.com/Manual/Profiler.html) (documentação do Unity).|  
  
## <a name="release-management"></a>Gerenciamento de liberações  
 Link de referência: **[Implantações automatizadas com Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview)**  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|Gerenciar processos de versão|Sim||  
|Implantação para servidores para carregamento lateral por meio de scripts|Sim||  
|Carregar para a loja de aplicativos|Parcial|Estão disponíveis extensões que podem automatizar esse processo para algumas lojas de aplicativos.  Consulte [Extensões para Visual Studio Team Services](https://marketplace.visualstudio.com/VSTS); por exemplo, a [extensão para Google Play](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play).|  
  
## <a name="monitor-with-hockeyapp"></a>Monitorar com HockeyApp  
 Link de referência: **[Monitorar com HockeyApp](https://www.hockeyapp.net/features/)**  
  
|Recurso|Tem suporte com o Unity|Comentários Adicionais|  
|-------------|--------------------------|-------------------------|  
|Análise de falhas, telemetria e distribuição beta|Sim|HockeyApp é útil principalmente para tratar a distribuição beta e obter relatórios de falha.<br /><br /> Para telemetria de scripts do C#, é possível usar qualquer estrutura de análise, desde que ela seja executada na versão do .NET que é usada pelo Unity. No entanto, isso permite análise somente dentro de scripts de jogos e não mais profundamente dentro do mecanismo do Unity. No momento, não há nenhum plug-in do Application Insights, mas plug-ins estão disponíveis para outras soluções de análise, como [Unity Analytics](https://www.assetstore.unity3d.com/en/#!/content/28120) e [Google Analytics](https://github.com/googleanalytics/google-analytics-plugin-for-unity). Serviços como Unity Analytics que entendem a natureza de um projeto Unity obviamente fornecerão análise muito mais significativa do que estruturas genéricas.|



