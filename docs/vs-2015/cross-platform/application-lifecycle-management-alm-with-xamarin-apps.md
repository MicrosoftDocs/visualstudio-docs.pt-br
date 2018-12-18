---
title: ALM (Gerenciamento do Ciclo de Vida do Aplicativo) com aplicativos Xamarin | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ff978cc2-5a25-46d6-921b-e51adaa65992
caps.latest.revision: 16
ms.author: crdun
manager: crdun
ms.openlocfilehash: f2e7af8227e11d554a4f953593dad396d5543aca
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745212"
---
# <a name="application-lifecycle-management-alm-with-xamarin-apps"></a>ALM (Gerenciamento do Ciclo de Vida do Aplicativo) com aplicativos Xamarin
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O Xamarin permite criar aplicativos móveis de plataforma cruzada direcionados para Android, iOS e Windows usando C#, .NET e Visual Studio. O Xamarin permite que uma grande parte do código seja compartilhada entre plataformas, com apenas um pequeno percentual precisando ser específico da plataforma. Para obter mais informações sobre o Xamarin em si, consulte [Visual Studio e Xamarin](../cross-platform/visual-studio-and-xamarin.md).  
  
 Desenvolver aplicativos para plataformas modernas envolve muito mais atividades do que apenas escrever código. Essas atividades, conhecidas como DevOps (desenvolvimento + operações), abrangem o ciclo de vida completo do aplicativo e incluem trabalhos de planejando e acompanhando, elaboração e implementação de código, gerenciamento de um repositório de código-fonte, execução de compilações, gerenciamento de integrações contínuas e implantações, teste (incluindo testes de unidade e testes de interface do usuário), execução de várias formas de diagnóstico em ambientes de desenvolvimento e produção e monitoramento do desempenho do aplicativo e dos comportamentos do usuário em tempo real por meio de telemetria e análise.  
  
 O Visual Studio, junto com o Visual Studio Team Services e o Team Foundation Server, proporciona uma variedade de recursos de DevOps, também conhecidos como ALM ou Gerenciamento do Ciclo de Vida do Aplicativo. Muitos deles são totalmente aplicáveis a projetos de plataforma cruzada.  
  
 Isso é especialmente verdadeiro com aplicativos Xamarin, pois eles são criados com C# e .NET, em torno dos quais algumas ferramentas ALM são criadas. Outras ferramentas exigem integração com ambientes de build e tempo de execução. Uma vez que os aplicativos Xamarin são executados em plataformas não Windows e usam a implementação Mono do .NET, o Xamarin fornece ferramentas especializadas para determinadas necessidades.  
  
 As tabelas a seguir identificam os recursos do Visual Studio ALM que você pode esperar que funcionem bem com um projeto do Xamarin e quais delas têm limitações. Consulte a documentação vinculada para obter detalhes sobre os recursos em si.  
  
## <a name="agile-tools"></a>Ferramentas agile  
 Link de referência: **[Trabalho](http://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)** (usando o Visual Studio Team Services ou TFS, incluindo o Team Explorer Everywhere)  
  
 Comentário Geral: todos os recursos de planejamento e acompanhamento são independentes do tipo de projeto e de linguagens de codificação.  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Gerenciar listas de pendências e sprints|Sim||  
|Acompanhamento de trabalho|Sim||  
|Colaboração da sala da equipe|Sim||  
|Quadros kanban|Sim||  
|Relatar e visualizar o progresso|Sim||  
  
## <a name="modeling"></a>Modelagem  
 Link de referência: **[Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)**  
  
 Recursos de design são independentes da linguagem de codificação ou funcionam com linguagens .NET como C#. Consulte [Funções de arquitetura e diagramas de modelagem no desenvolvimento de software](../modeling/scenario-change-your-design-using-visualization-and-modeling.md#ModelingDiagramsTools) para aspectos relacionados a código.  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Diagramas de sequência|Sim||  
|Grafos de dependência|Sim||  
|Hierarquia de chamadas|Sim||  
|Designer de Classe|Sim||  
|Gerenciador de arquitetura|Sim||  
|Diagramas UML (caso de uso, atividade, classe, componente, sequência e DSL)|Sim||  
|Diagramas de camada|Sim||  
|Validação da camada|Sim||  
  
## <a name="code"></a>Código  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|[Use o Controle de Versão do Team Foundation](http://msdn.microsoft.com/library/1d629052-c65d-4c5d-81eb-eaa4413fe285) ou Visual Studio Team Services|Sim||  
|[Introdução ao Git no Team Services](http://msdn.microsoft.com/library/32f46ecd-1b03-4ef0-a9c4-8a120da2b03f)|Sim||  
|[Análise de código/melhorar a qualidade do código (referências, alterações sugeridas, etc.)](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)|Sim||  
|[Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md)|Sim|Exceto através de limites específicos da plataforma em que a implementação não seja resolvida até o tempo de execução.|  
|[Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)|Sim||  
  
## <a name="build"></a>Build  
 Link de referência: **[Build](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)**  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Servidor TFS local|Sim|Computadores de build devem ter Xamarin instalado e podem ser vinculados a um computador OSX para compilar para iOS. Consulte [Configurando TFS para Xamarin](http://developer.xamarin.com/guides/cross-platform/ci/configuring_tfs/) (site do Xamarin)|  
|Servidor de build local vinculado ao Visual Studio Team Services|Sim|Consulte [Servidor de build](http://msdn.microsoft.com/library/2d258a0a-f178-4e93-9da1-eba61151af3c) para obter instruções.|  
|Serviço de controlador hospedado do Visual Studio Team Services|Sim|Consulte [Compilar seu aplicativo Xamarin](https://www.visualstudio.com/en-us/docs/build/apps/mobile/xamarin).|  
|Compilar definições com pré e pós-scripts|Sim||  
|Integração contínua incluindo check-ins restritos|Sim|Check-ins restritos somente para TFVC, uma vez que Git funciona em um modelo de solicitação pull, em vez de check-ins.|  
  
## <a name="testing"></a>Testes  
 Link de referência: **[Testando o aplicativo](http://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)**  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Planejando testes, criando casos de teste e organizando conjuntos de testes|Sim||  
|Teste manual|Sim||  
|Gerenciador de Teste (testes de gravação e reprodução)|Sim|Somente dispositivos Windows e emuladores Android do Visual Studio. Gravação para todos os dispositivos é possível com o [Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder).|  
|Cobertura de código|N/D||  
|[Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)|Sim|Para os destinos Android e Windows, as ferramentas internas do MSTest podem ser usadas. Para executar testes de unidade em Windows, Android e iOS, o Xamarin recomenda NUnit. Consulte [Configurando TFS para Xamarin](http://developer.xamarin.com/guides/cross-platform/ci/configuring_tfs/) (site do Xamarin).|  
|[Usar automação de interface do usuário para testar código](../test/use-ui-automation-to-test-your-code.md)|Somente Windows|O gravador de teste da interface do usuário do Visual Studio é somente Windows. Para todas as plataformas, consulte [Xamarin Test Recorder](https://www.xamarin.com/test-cloud/recorder).|  
  
## <a name="improve-code-quality"></a>Melhorar a qualidade do código  
 Link de referência: **[Melhorar a qualidade do código](http://msdn.microsoft.com/library/73baa961-c21f-43fe-bb92-3f59ae9b5945)**  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|[Analisando a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)|Sim||  
|[Localizando código duplicado usando detecção de clone de código](http://msdn.microsoft.com/library/a97cd5a6-5ffa-4104-9627-8e59e513654d)|Sim||  
|[Medindo complexidade e facilidade de manutenção do código gerenciado](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)|Sim||  
|[Gerenciador de Desempenho](../profiling/performance-explorer.md)|Não|Use o [Xamarin Profiler](http://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/) por meio do Xamarin Studio em vez disso. Observe que o Xamarin Profiler está atualmente em visualização e ainda não funciona para destinos do Windows.|  
|[Analisar problemas de memória do .NET Framework](../misc/analyze-dotnet-framework-memory-issues.md)|Não|Ferramentas do Visual Studio não têm ganchos na estrutura Mono para a criação de perfil.|  
  
## <a name="release-management"></a>Gerenciamento de liberações  
 Link de referência: **[Implantações automatizadas com Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview)**  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Gerenciar processos de versão|Sim||  
|Implantação para servidores para carregamento lateral por meio de scripts|Sim||  
|Carregar para a loja de aplicativos|Parcial|Estão disponíveis extensões que podem automatizar esse processo para algumas lojas de aplicativos.  Consulte [Extensões para Visual Studio Team Services](https://marketplace.visualstudio.com/VSTS); por exemplo, a [extensão para Google Play](https://marketplace.visualstudio.com/items?itemName=ms-vsclient.google-play).|  
  
## <a name="monitor-with-hockeyapp"></a>Monitorar com HockeyApp  
 Link de referência: **[Monitorar com HockeyApp](https://www.hockeyapp.net/features/)**  
  
|Recurso|Tem suporte com o Xamarin|Comentários Adicionais|  
|-------------|----------------------------|-------------------------|  
|Análise de falhas, telemetria e distribuição beta|Sim||

