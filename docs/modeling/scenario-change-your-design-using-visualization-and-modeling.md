---
title: 'Cenário: alterar o design usando visualização e modelagem'
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- code visualization [Visual Studio ALM]
- modeling software [Visual Studio ALM]
- software modeling [Visual Studio ALM]
- walkthroughs [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], modeling software
- walkthroughs [Visual Studio ALM], modeling software
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c0e971a2a38013ae75287467404e3321e3c4d37
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544190"
---
# <a name="scenario-change-your-design-using-visualization-and-modeling"></a>Cenário: alterar o design usando visualização e modelagem

Verifique se o sistema de software atende às necessidades dos usuários usando as ferramentas de visualização e modelagem no Visual Studio.
Use ferramentas como mapas de código, diagramas de dependência e diagramas de classe para:

Para ver quais versões do Visual Studio oferecem suporte a cada ferramenta, consulte [suporte de versão para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

- Esclareça os requisitos dos usuários e os processos de negócios.

- Visualize e explore o código existente.

- Descreva as alterações em um sistema existente.

- Verifique se o sistema atende aos seus requisitos.

- Mantenha o código consistente com o design.

Este passo a passos:

- Descreve como essas ferramentas podem beneficiar seu projeto de software.

- Mostra como você pode usar essas ferramentas, independentemente de sua abordagem de desenvolvimento, com um cenário de exemplo.

Para saber mais sobre essas ferramentas e os cenários que eles dão suporte, consulte:

- [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)

- [Visualizar código](../modeling/visualize-code.md)

## <a name="scenario-overview"></a>Visão geral do cenário

Este cenário descreve os episódios dos ciclos de vida de desenvolvimento de software de duas empresas fictícias: jantar agora e editora Zuzu. O jantar agora fornece um serviço de entrega de refeição baseado na Web em Seattle. Os clientes podem pedir refeições e pagar por eles no site do jantar agora. Em seguida, os pedidos são enviados para o restaurante local apropriado para entrega. A editora Zuzu, uma empresa em Nova York, executa várias empresas e na Web. Por exemplo, eles executam um site onde os clientes podem postar revisões de restaurante.

A editora recentemente adquiriu o jantar agora e deseja fazer as seguintes alterações:

- Integre seus sites adicionando recursos de revisão de restaurante ao jantar agora.

- Substitua o sistema de pagamento do jantar agora pelo sistema da Lucerne.

- Expanda o serviço de jantar agora na região.

O jantar agora usa o SCRUM e a programação extrema. Eles têm cobertura de teste muito alta e muito pouco código sem suporte. Eles minimizam riscos criando versões pequenas, mas em funcionamento, de um sistema e, em seguida, adicionando funcionalidade incrementalmente. Eles desenvolvem seu código em iterações curtas e frequentes. Isso permite que eles adotem alterações com confiança, com frequência o código de refatoração e evite "Big design up inicial".

A Lucerne mantém uma coleção imensamente maior e complexa de sistemas, alguns dos quais têm mais de 40 anos de idade. Eles têm muito cuidado ao fazer alterações devido à complexidade e ao escopo do código herdado. Eles seguem um processo de desenvolvimento mais rigoroso, preferindo criar soluções detalhadas e documentar o design e as alterações que ocorrem durante o desenvolvimento.

Ambas as equipes usam diagramas de modelagem no Visual Studio para ajudá-los a desenvolver sistemas que atendam às necessidades dos usuários. Eles usam Team Foundation Server junto com outras ferramentas para ajudá-los a planejar, organizar e gerenciar seu trabalho.

Para obter mais informações sobre Team Foundation Server, consulte:

- [Planejar e acompanhar o trabalho](#plan-and-track-work)

- [Testando, validando e verificando o código atualizado](#TestValidateCheckInCode)

## <a name="roles-of-architecture-and-modeling-diagrams-in-software-development"></a><a name="ModelingDiagramsTools"></a>Funções de diagramas de arquitetura e modelagem no desenvolvimento de software

A tabela a seguir descreve as funções que essas ferramentas podem reproduzir durante vários e vários estágios do ciclo de vida do desenvolvimento de software:

||**Modelagem de requisitos de usuário**|**Modelagem de processos de negócios**|**Arquitetura do sistema & design**|**Visualização de código & exploração**|**Verificação**|
|------|-|-|-|-|-|
|Diagrama de DSL (linguagem específica do domínio)|Sim|Sim|Sim|||
|Diagrama de dependência, validação de camada|||Sim|Sim|Sim|
|Mapa de códigos|||Sim|Sim|Sim|
|Designer de Classe (baseado em código)||||Sim||

Para desenhar diagramas de dependência, você deve criar um projeto de modelagem como parte de uma solução existente ou um novo. Esses diagramas devem ser criados no projeto de modelagem.
Os itens em diagramas de dependência estão localizados no projeto de modelagem, mas não são armazenados no modelo comum. Mapas de código e diagramas de classe .NET criados a partir do código existem fora do projeto de modelagem.

Consulte:

- [Criar diagramas de dependência do código](../modeling/create-layer-diagrams-from-your-code.md)

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)

- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)

- [SDK de Modelagem para Visual Studio - linguagens específicas ao domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Ambas as equipes também usam validação de dependência para garantir que o código em desenvolvimento permaneça consistente com o design. Consulte:

- [Mantendo o código consistente com o design](#ValidatingCode)

- [Descrever a arquitetura lógica: diagramas de dependência](#DescribeLayers)

- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

> [!NOTE]
> Algumas versões do Visual Studio dão suporte à validação de dependência e versões somente leitura de mapas de código para visualização e modelagem. Para ver quais edições do Visual Studio oferecem suporte a esse recurso, consulte [suporte de edição para ferramentas de arquitetura e modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="understand-and-communicate-information-about-the-system"></a>Entender e comunicar informações sobre o sistema

Não há nenhuma ordem recomendada para usar os diagramas de modelagem do Visual Studio, para que você possa usá-los conforme eles se ajustarem às suas necessidades ou abordagem. Normalmente, as equipes revisitam seus modelos iterativamente e frequentemente em um projeto. Cada diagrama oferece forças específicas para ajudá-lo a entender, descrever e comunicar diferentes aspectos do sistema em desenvolvimento.

O jantar agora e a Zulu se comunicam entre si e com os participantes do projeto usando diagramas como linguagem comum. Por exemplo, o jantar agora usa diagramas para executar estas tarefas:

- Visualizar o código existente.

- Comunique-se com a Lucerne sobre histórias de usuários novas ou atualizadas.

- Identifique as alterações necessárias para dar suporte a histórias de usuário novas ou atualizadas.

A Lucerne usa diagramas para executar estas tarefas:

- Saiba mais sobre o processo de negócios do jantar agora.

- Entenda o design do sistema.

- Comunique-se com o jantar agora sobre os requisitos de usuário novos ou atualizados.

- Documentar atualizações no sistema.

Os diagramas são integrados com o Team Foundation Server para que as equipes possam planejar, gerenciar e controlar seu trabalho com mais facilidade. Por exemplo, eles usam modelos para identificar casos de teste e tarefas de desenvolvimento e para estimar seu trabalho. A Lucerne links Team Foundation Server itens de trabalho a elementos de modelo para que eles possam monitorar o progresso e garantir que o sistema atenda aos requisitos dos usuários. Por exemplo, eles vinculam casos de uso a itens de trabalho de caso de teste para que possam ver se os casos de uso são atendidos quando todos os testes são aprovados.

Antes que as equipes verifiquem suas alterações, elas validam o código em relação aos testes e ao design executando compilações que incluem validação de dependência e testes automatizados. Isso ajuda a garantir que o código atualizado não entre em conflito com o design e interromper a funcionalidade de trabalho anterior.

### <a name="identify-changes-to-the-existing-system"></a>Identificar alterações no sistema existente

Agora, o jantar deve estimar o custo da reunião do novo requisito. Isso depende, em parte, de quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos jantares, agora, os desenvolvedores criam esses mapas e diagramas a partir do código existente:

|**Mapa ou diagrama**|**programas**|
|-|-|
|*Mapa de códigos*<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)<br />- [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)|Dependências e outras relações no código.<br /><br /> Por exemplo, o jantar agora pode começar examinando mapas de código assembly para obter uma visão geral dos assemblies e suas dependências. Eles podem analisar os mapas para explorar os namespaces e as classes nesses assemblies.<br /><br /> Agora, o jantar também pode criar mapas para explorar áreas específicas e outros tipos de relações no código. Eles usam Gerenciador de Soluções para localizar e selecionar as áreas e relações que os interessam.|
|*Diagrama de classe baseado em código*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md).|Classes existentes no código|

 Por exemplo, o desenvolvedor cria um mapa de código. Ela ajusta seu escopo para se concentrar nas áreas que serão afetadas pelo novo cenário. Essas áreas são selecionadas e realçadas no mapa:

 ![Grafo de dependência de namespace](../modeling/media/namespace_reviewsystem.png)

 **Mapa de código do namespace**

 O desenvolvedor expande os namespaces selecionados para ver suas classes, métodos e relações:

 ![Grafo de dependência de namespace expandido](../modeling/media/dep_reviewsystem.png)

 **Mapa de código de namespace expandido com links entre grupos visíveis**

 O desenvolvedor examina o código para localizar as classes e os métodos afetados. Para ver os efeitos de cada alteração ao fazê-las, gere novamente os mapas de código após cada alteração. Consulte [Visualizar código](../modeling/visualize-code.md).

 Para descrever as alterações em outras partes do sistema, como componentes ou interações, a equipe pode desenhar esses elementos em quadros de comunicações. Eles também podem desenhar os seguintes diagramas no Visual Studio para que os detalhes possam ser capturados, gerenciados e compreendidos por ambas as equipes:

|**Diagramas**|**Descrita**|
|-|-|
|*Diagrama de classe baseado em código*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md).|Classes existentes no código.|

### <a name="keep-code-consistent-with-the-design"></a><a name="ValidatingCode"></a>Manter o código consistente com o design
 Agora, o jantar deve garantir que o código atualizado permaneça consistente com o design. Eles criam diagramas de dependência que descrevem as camadas de funcionalidade no sistema, especificam as dependências permitidas entre elas e associam os artefatos de solução a essas camadas.

|**Diagrama**|**Descrita**|
|-|-|
|*Diagrama de dependência*<br /><br /> Consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)|A arquitetura lógica do código.<br /><br /> Um diagrama de dependência organiza e mapeia os artefatos em uma solução do Visual Studio para abstrair grupos chamados *camadas*. Essas camadas identificam as funções, as tarefas ou as funções que esses artefatos executam no sistema.<br /><br /> Os diagramas de dependência são úteis para descrever o design pretendido do sistema e validar o código em evolução nesse design.<br /><br /> Para criar camadas, arraste itens de Gerenciador de Soluções, mapas de código, Modo de Exibição de Classe e pesquisador de objetos. Para desenhar novas camadas, use a caixa de ferramentas ou clique com o botão direito do mouse na superfície do diagrama.<br /><br /> Para exibir as dependências existentes, clique com o botão direito do mouse na superfície do diagrama de dependência e clique em **gerar dependências**. Para especificar as dependências pretendidas, desenhe novas dependências.|

Por exemplo, o diagrama de dependência a seguir descreve as dependências entre as camadas e o número de artefatos associados a cada camada:

![Diagrama de dependência do sistema de pagamento integrado](../modeling/media/layer_integrated_dnlucerne.png)

 **Diagrama de dependência**

Para garantir que conflitos com o design não ocorram durante o desenvolvimento de código, as equipes usam a validação de dependência em compilações que são executadas no Azure DevOps. Eles também criam uma tarefa personalizada do MSBuild para exigir a validação de dependência em suas operações de check-in. Eles usam relatórios de compilação para coletar erros de validação.

Consulte:

- [Usar o designer visual](/azure/devops/pipelines/get-started-designer)

- [Check-in restrito do TFVC](/azure/devops/pipelines/build/triggers)

- [Tarefas de Build e versão](/azure/devops/pipelines/tasks/index)

### <a name="general-tips-for-creating-and-using-models"></a>Dicas gerais para criar e usar modelos

- A maioria dos diagramas consiste em nós que estão conectados por linhas. Para cada tipo de diagrama, a caixa de ferramentas fornece diferentes tipos de nós e linhas.

   Para abrir a caixa de ferramentas, no menu **Exibir** , clique em **caixa de ferramentas**.

- Para criar um nó, arraste-o da caixa de ferramentas para o diagrama. Determinados tipos de nós devem ser arrastados para nós existentes. Por exemplo, em um diagrama de componente, uma nova porta deve ser adicionada a um componente existente.

- Para criar uma linha ou uma conexão, clique na ferramenta apropriada na caixa de ferramentas, clique no nó de origem e, em seguida, clique no nó de destino. Algumas linhas podem ser criadas somente entre determinados tipos de nós. Quando você move o ponteiro sobre uma possível origem ou destino, o ponteiro indica se você pode criar uma conexão.

### <a name="plan-and-track-work"></a>Planejar e acompanhar o trabalho

Os diagramas de modelagem do Visual Studio são integrados com Team Foundation Server para que você possa planejar, gerenciar e acompanhar o trabalho com mais facilidade. As duas equipes usam modelos para identificar casos de teste e tarefas de desenvolvimento e para estimar seu trabalho. A Lucerne cria e vincula Team Foundation Server itens de trabalho a elementos de modelo, como casos de uso ou componentes. Isso ajuda a monitorar seu progresso e rastrear seu trabalho de volta aos requisitos dos usuários. Isso ajuda a garantir que suas alterações continuem a atender a esses requisitos.

À medida que seu trabalho progride, as equipes atualizam seus itens de trabalho para refletir o tempo gasto em suas tarefas. Eles também monitoram e relatam o status em seu trabalho usando os seguintes recursos de Team Foundation Server:

- *Relatórios de gravação* diária que mostram se eles vão concluir o trabalho planejado no tempo esperado. Eles geram outros relatórios semelhantes de Team Foundation Server para acompanhar o progresso dos bugs.

- Uma *planilha de iteração* que usa o Microsoft Excel para ajudar a equipe a monitorar e balancear a carga de trabalho entre seus membros. Esta planilha está vinculada a Team Foundation Server e fornece o foco para discussão durante suas reuniões de progresso regulares.

- Um *painel de desenvolvimento* que usa o Office Project para manter a equipe informada sobre informações importantes do projeto.

Consulte:

- [Sobre as ferramentas Agile e o gerenciamento ágil de projetos](/azure/devops/boards/backlogs/backlogs-overview?view=vsts)

- [Gráficos, painéis e widgets (Azure DevOps Services)](/azure/devops/report/dashboards/overview?view=vsts)

- [Criar sua lista de pendências e tarefas usando o Project](/azure/devops/boards/backlogs/office/create-your-backlog-tasks-using-project)

### <a name="test-validate-and-check-in-code"></a><a name="TestValidateCheckInCode"></a>Testar, validar e fazer check-in de código

Conforme as equipes concluem cada tarefa, elas verificam seu código no controle do código-fonte e recebem lembretes de Team Foundation Server, caso se esqueçam. Antes que Team Foundation Server aceite seus check-ins, as equipes executam testes de unidade e validação de dependência para verificar o código em relação aos seus casos de teste e ao design. Eles usam Team Foundation Server para executar compilações, testes de unidade automatizados e validação de dependência regularmente. Isso ajuda a garantir que o código atenda aos seguintes critérios:

- Funciona.

- Ele não interrompe o código que estava funcionando anteriormente.

- Ele não entra em conflito com o design.

Agora, o jantar tem uma grande coleção de testes automatizados, que a Lucerne pode reutilizar porque quase todos ainda se aplicam. A Lucerne também pode criar esses testes e adicionar novos para abranger novas funcionalidades. Ambos também usam o Visual Studio para executar testes manuais.

Para garantir que o código esteja de acordo com o design, as equipes configuram suas compilações no Azure DevOps para incluir a validação de dependência. Se ocorrer algum conflito, um relatório será gerado com os detalhes.

Consulte:

- [Testando o aplicativo](/azure/devops/test/overview?view=vsts)

- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)

- [Usar controle de versão](/azure/devops/repos/tfvc/overview?view=azure-devops)

- [Azure Pipelines](/azure/devops/pipelines/index?view=vsts)

## <a name="update-the-system-using-visualization-and-modeling"></a>Atualizar o sistema usando a visualização e a modelagem

A Lucerne e o jantar agora devem integrar seus sistemas de pagamento. As seções a seguir mostram os diagramas de modelagem no Visual Studio que os ajudam a executar esta tarefa:

- [Visualizar código existente: mapas de código](#VisualizeCode)

- [Definir um glossário de tipos: diagramas de classe](#DefineClasses)

- [Descrever a arquitetura lógica: diagramas de dependência](#DescribeLayers)

Consulte:

- [Visualizar código](../modeling/visualize-code.md)

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)

- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)

### <a name="visualize-existing-code-code-maps"></a><a name="VisualizeCode"></a>Visualizar código existente: mapas de código

Os mapas de código mostram a organização atual e as relações no código. Os itens são representados por *nós* no mapa e as relações são representadas por *links*. Os mapas de código podem ajudá-lo a executar os seguintes tipos de tarefas:

- Explore um código desconhecido.

- Entenda onde e como uma alteração proposta pode afetar o código existente.

- Encontre áreas de complexidade, dependências naturais ou padrões ou outras áreas que possam se beneficiar do aprimoramento.

Por exemplo, o jantar agora deve estimar o custo da atualização do componente PaymentProcessing. Isso depende, em parte, de quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos jantares, agora, os desenvolvedores geram mapas de código do código e ajusta o foco do escopo nas áreas que podem ser afetadas pela alteração.

O mapa a seguir mostra as dependências entre a classe PaymentProcessing e outras partes do sistema do jantar agora, que aparecem selecionadas:

![Grafo de dependência para o sistema de pagamento do jantar agora](../modeling/media/dep_dnpayment.png)

**Mapa de códigos para o sistema de pagamento do jantar agora**

O desenvolvedor explora o mapa expandindo a classe PaymentProcessing e selecionando seus membros para ver as áreas potencialmente afetadas:

![Métodos dentro de PaymentProcessing e dependências](../modeling/media/depgraph_expandeddn.png)

**Métodos dentro da classe PaymentProcessing e suas dependências**

Eles geram o mapa a seguir para o sistema de pagamento Zulu para inspecionar suas classes, métodos e dependências. A equipe vê que o sistema da Lucerne também pode exigir trabalho para interagir com as outras partes do jantar agora:

![Grafo de dependência para o sistema de pagamento Zulu](../modeling/media/depgraph_lucernepay.png)

**Mapa de códigos para o sistema de pagamento da Lucerne**

Ambas as equipes trabalham juntas para determinar as alterações necessárias para integrar os dois sistemas. Eles decidem refatorar parte do código para que seja mais fácil de atualizar. A classe PaymentApprover será movida para o namespace DinnerNow. Business e exigirá alguns novos métodos. As classes do jantar agora que lidam com as transações terão seu próprio namespace. As equipes criam e usam itens de trabalho para planejar, organizar e acompanhar seu trabalho. Eles vinculam os itens de trabalho a elementos de modelo onde são úteis.

Depois de reorganizar o código, as equipes geram um novo mapa de código para ver a estrutura e as relações atualizadas:

![Grafo de dependência com código reorganizado](../modeling/media/depgraph_integrated.png)

**Mapa de código com código reorganizado**

Esse mapa mostra que a classe PaymentApprover agora está no namespace DinnerNow. Business e tem alguns métodos novos. Agora, as classes Transaction do jantar agora têm seu próprio namespace PaymentSystem, o que torna mais fácil lidar com esse código posteriormente.

#### <a name="creating-a-code-map"></a>Criando um mapa de código

- Para obter uma visão geral rápida do código-fonte, siga estas etapas para gerar um mapa de código:

     No menu **arquitetura** , clique em **gerar mapa de código para solução**.

     Para obter uma visão geral rápida do código compilado, crie um mapa de código em branco e arraste arquivos de assembly ou arquivos binários para a superfície do mapa.

- Para explorar um código específico ou itens de solução, use Gerenciador de Soluções para selecionar itens e relações que você deseja visualizar. Em seguida, você pode gerar um novo mapa ou adicionar itens selecionados a um mapa existente. Consulte [mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md).

- Para ajudá-lo a explorar o mapa, reorganize o layout para que ele se adapte aos tipos de tarefas que você deseja executar.

     Por exemplo, para visualizar a disposição em camadas no código, selecione um layout de árvore. Consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

#### <a name="summary-strengths-of-code-maps"></a>Resumo: pontos fortes dos mapas de código
 Os mapas de código ajudam você a:

- Saiba mais sobre a organização e as relações no código existente.

- Identifique áreas que podem ser afetadas por uma alteração proposta.

- Encontre áreas de complexidade, padrões, camadas ou outras áreas que você pode melhorar para tornar o código mais fácil de manter, alterar e reutilizar.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descrita**|
|-|-|
|Diagrama de dependência|A arquitetura lógica do sistema. Use a validação de dependência para garantir que o código permaneça consistente com o design.<br /><br /> Para ajudá-lo a identificar dependências ou dependências pretendidas existentes, crie um mapa de código e itens relacionados ao grupo. Para criar um diagrama de dependência, consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)|
|Diagrama de classe (baseado em código)|Classes existentes no código para um projeto específico.<br /><br /> Para visualizar e modificar uma classe existente no código, use Designer de Classe.<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md).|

### <a name="define-a-glossary-of-types-class-diagrams"></a><a name="DefineClasses"></a>Definir um glossário de tipos: diagramas de classe
 Os diagramas de classe definem as entidades, os termos ou os conceitos que participam do sistema e suas relações entre si. Por exemplo, você pode usar esses diagramas durante o desenvolvimento para descrever os atributos e as operações de cada classe, independentemente de seu idioma ou estilo de implementação.

 Para ajudar a Lucerne a descrever e discutir as entidades que participam do caso de uso de pagamento do processo, elas desenham o seguinte diagrama de classe:

 ![Processar entidades de pagamento no diagrama de classes](../modeling/media/uml_payentities.png)

 **Processar entidades de pagamento em um diagrama de classe**

 Este diagrama mostra que um cliente pode ter muitos pedidos e diferentes maneiras de pagar por pedidos. O BankAccount e o CreditCard herdam de pagamento.

 Durante o desenvolvimento, a Lucerne usa o seguinte diagrama de classe para descrever e discutir os detalhes de cada classe:

 ![Processar detalhes da entidade de pagamento em um diagrama de classe](../modeling/media/uml_payment.png)

 **Processar detalhes de pagamento no diagrama de classe**

#### <a name="drawing-a-class-diagram"></a>Desenhando um diagrama de classe

Um diagrama de classe tem os seguintes recursos principais:

- Tipos como classes, interfaces e enumerações:

  - Uma *classe* é a definição de objetos que compartilham características estruturais ou comportamentais específicas.

  - Uma *interface* define uma parte do comportamento visível externamente de um objeto.

  - Uma *Enumeração* é um classificador que contém uma lista de valores literais.

- *Atributos* são valores de um determinado tipo que descrevem cada instância de um *classificador*. Um classificador é um nome geral para tipos, componentes, casos de uso e até mesmo atores.

- *Operações* são métodos ou funções que as instâncias de um classificador podem executar.

- Uma *Associação* indica algum tipo de relação entre dois classificadores.

  - Uma *agregação* é uma associação que indica uma propriedade compartilhada entre classificadores.

  - Uma *composição* é uma associação que indica uma relação de parte inteira entre classificadores.

    Para mostrar agregações ou composições, defina a propriedade de **agregação** em uma associação. **Compartilhado** mostra as agregações **e as composições mostra** as composições.

- Uma *dependência* indica que a alteração da definição de um classificador pode alterar a definição de outro classificador.

- Uma *generalização* indica que um classificador específico herda parte de sua definição de um classificador geral. Uma *realização* indica que uma classe implementa as operações e os atributos oferecidos por uma interface.

     Para criar essas relações, use a ferramenta de **herança** . Como alternativa, uma realização pode ser representada como uma *pirulito*.

- Os *pacotes* são grupos de classificadores, associações, linhas de vida, componentes e outros pacotes. As relações de *importação* indicam que um pacote inclui todas as definições de outro pacote.

Como ponto de partida para explorar e discutir as classes existentes, você pode usar Designer de Classe para criar diagramas de classe a partir do código.

- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)

#### <a name="summary-strengths-of-class-diagrams"></a>Resumo: forças dos diagramas de classe
 Os diagramas de classe ajudam a definir:

- Um glossário comum de termos a serem usados ao discutir as necessidades dos usuários e as entidades que participam do sistema. Consulte [requisitos de usuário de modelo](../modeling/model-user-requirements.md).

- Tipos que são usados por partes do sistema, como componentes, independentemente de sua implementação. Consulte [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).

- Relações, como dependências, entre tipos. Por exemplo, você pode mostrar que um tipo pode ser associado a várias instâncias de outro tipo.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descrição**|
|-|-|
|Diagrama de dependência|Defina a arquitetura lógica do sistema como está relacionada às classes.<br /><br /> Use a validação de dependência para garantir que o código permaneça consistente com o design.<br /><br /> Consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)|
|Mapa de códigos|Visualize a organização e as relações no código existente.<br /><br /> Para identificar classes, suas relações e seus métodos, crie um mapa de código que mostre esses elementos.<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)|

### <a name="describe-the-logical-architecture-dependency-diagrams"></a><a name="DescribeLayers"></a>Descrever a arquitetura lógica: diagramas de dependência
 Os diagramas de dependência descrevem a arquitetura lógica de um sistema organizando os artefatos em sua solução em grupos abstratos ou *camadas*. Os artefatos podem ser muitas coisas, como namespaces, projetos, classes, métodos e assim por diante. As camadas representam e descrevem as funções ou tarefas que os artefatos executam no sistema. Você também pode incluir a validação de camada em suas operações de criação e check-in para garantir que o código permaneça consistente com seu design.

 Para manter o código consistente com o design, o jantar agora e a Lucerne usam o diagrama de dependência a seguir para validar seu código à medida que ele evolui:

 ![Diagrama de dependência do sistema de pagamento integrado](../modeling/media/layer_integrated_dnlucerne.png)

 **Diagrama de dependência para jantar agora integrado à Lucerne**

 As camadas neste diagrama vinculam-se ao jantar correspondente agora e aos artefatos da solução Zulu. Por exemplo, a camada de negócios vincula-se ao namespace DinnerNow. Business e a seus membros, que agora incluem a classe PaymentApprover. A camada de acesso a recursos vincula-se ao namespace DinnerNow. Data. As setas, ou *dependências*, especificam que apenas a camada de negócios pode usar a funcionalidade na camada de acesso ao recurso. À medida que as equipes atualizam seu código, a validação de camada é executada regularmente para detectar conflitos à medida que ocorrem e para ajudar as equipes a solucioná-los imediatamente.

 As equipes trabalham em conjunto para integrar e testar incrementalmente os dois sistemas. Primeiro, eles garantem que o PaymentApprover e o restante do jantar agora trabalhem com os outros com êxito antes de lidarem com o PaymentProcessing.

 O mapa de código a seguir mostra as novas chamadas entre o jantar agora e PaymentApprover:

 ![Grafo de dependência atualizado com sistema integrado](../modeling/media/depgraph_intsystem.png)

 **Mapa de código com chamadas de método atualizadas**

 Depois de confirmar que o sistema funciona conforme o esperado, o jantar agora comenta o código PaymentProcessing. Os relatórios de validação de camada são limpos e o mapa de código resultante mostra que não existem mais dependências de PaymentProcessing:

 ![Grafo de dependência sem PaymentProcessing](../modeling/media/depgraph_nomore.png)

 **Mapa de código sem PaymentProcessing**

#### <a name="drawing-a-dependency-diagram"></a>Desenhando um diagrama de dependência

Um diagrama de dependência tem os seguintes recursos principais:

- *Camadas* descrevem grupos lógicos de artefatos.

- Um *link* é uma associação entre uma camada e um artefato.

     Para criar camadas de artefatos, arraste itens de Gerenciador de Soluções, mapas de código, Modo de Exibição de Classe ou pesquisador de objetos. Para desenhar novas camadas e vinculá-las a artefatos, use a caixa de ferramentas ou clique com o botão direito do mouse na superfície do diagrama para criar as camadas e, em seguida, arraste os itens para essas camadas.

     O número em uma camada mostra o número de artefatos vinculados à camada. Esses artefatos podem ser namespaces, projetos, classes, métodos e assim por diante. Ao interpretar o número de artefatos em uma camada, lembre-se do seguinte:

  - Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.

       Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.

  - Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.

    Para ver os artefatos que estão vinculados a uma camada, clique com o botão direito do mouse na dependência e clique em **exibir links** para abrir o **Gerenciador de camadas**.

- Uma *dependência* indica que uma camada pode usar a funcionalidade em outra camada, mas não vice-versa. Uma *dependência bidirecional* indica que uma camada pode usar a funcionalidade em outra camada, e vice-versa.

     Para exibir as dependências existentes no diagrama de dependência, clique com o botão direito do mouse na superfície do diagrama e clique em **gerar dependências**. Para descrever as dependências pretendidas, desenhe novas.

Consulte:

- [Criar diagramas de dependência do código](../modeling/create-layer-diagrams-from-your-code.md)

- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)

- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)

- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

#### <a name="summary-strengths-of-dependency-diagrams"></a>Resumo: pontos fortes de diagramas de dependência

Os diagramas de dependência ajudam você a:

- Descreva a arquitetura lógica de um sistema de acordo com a funcionalidade de seus artefatos.

- Verifique se o código em desenvolvimento está em conformidade com o design especificado.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descrição**|
|-|-|
|Mapa de códigos|Visualize a organização e as relações no código existente.<br /><br /> Para criar camadas, gere um mapa de código e agrupe itens no mapa como camadas potenciais. Arraste os grupos do mapa para o diagrama de dependência.<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)|

## <a name="external-resources"></a>Recursos externos

|**Categoria**|**Links**|
|-|-|
|**Fóruns**|- [Ferramentas de modelagem & de visualização do Visual Studio](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />- [SDK de modelagem de & de visualização do Visual Studio (ferramentas DSL)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|

## <a name="see-also"></a>Confira também

- [Visualizar código](../modeling/visualize-code.md)
- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Usar modelos no desenvolvimento ágil](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)
- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)
