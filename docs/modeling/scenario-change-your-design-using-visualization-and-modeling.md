---
title: 'Cenário: alterar o design usando visualização e modelagem'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- code visualization [Visual Studio ALM]
- modeling software [Visual Studio ALM]
- software modeling [Visual Studio ALM]
- walkthroughs [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], modeling software
- walkthroughs [Visual Studio ALM], modeling software
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bc8066148b2c8612b3a07922e15422022b8c9c4d
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967500"
---
# <a name="scenario-change-your-design-using-visualization-and-modeling"></a>Cenário: alterar o design usando visualização e modelagem

Certifique-se de que seu sistema de software atende às necessidades dos usuários usando a visualização e modelagem de ferramentas no Visual Studio.
Use ferramentas como mapas de código, diagramas de dependência e diagramas de classe para:

Para ver quais versões do Visual Studio oferecem suporte a cada ferramenta, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

- Esclareça os requisitos e processos de negócios dos usuários.

- Visualize e explore o código existente.

- Descreva as alterações para um sistema existente.

- Verifique se que o sistema atende aos seus requisitos.

- Manter o código consistente com o design.

Este passo a passo:

- Descreve como essas ferramentas podem se beneficiar seu projeto de software.

- Mostra como você pode usar essas ferramentas, independentemente sua abordagem de desenvolvimento, com um cenário de exemplo.

Para obter mais informações sobre essas ferramentas e os cenários que dão suporte a eles, consulte:

- [Análise e modelagem de arquitetura](../modeling/analyze-and-model-your-architecture.md)

- [Visualizar código](../modeling/visualize-code.md)

## <a name="scenario-overview"></a>Visão geral do cenário

Este cenário descreve episódios de ciclos de vida de desenvolvimento do software de duas empresas fictícias: Dinner Now e Lucerne Publishing. O dinner Now fornece um serviço de entrega de refeições baseado na Web em Seattle. Os clientes podem pedir refeições e pagá-las no site da Dinner Now. Os pedidos são então enviados para o restaurante local apropriado para entrega. A Lucerne Publishing, uma empresa de Nova York, tem vários negócios dentro e fora da Web. Por exemplo, eles executarem um site em que os clientes podem postar resenhas de restaurantes.

A Lucerne recentemente adquirida Dinner Now e deseja fazer as seguintes alterações:

- Integre seus sites, adicionando recursos de critica de restaurante ao Dinner Now.

- Substitua o sistema de pagamento da Dinner Now pelo sistema de Lucerne.

- Expanda o serviço Dinner Now em toda a região.

O dinner Now usa programação extrema e SCRUM. Eles têm cobertura de teste muito alta e pouco código não suportado. Minimizam os riscos criando pequenas, mas as versões de trabalho de um sistema e, em seguida, adicionando a funcionalidade incrementalmente. Desenvolvem seu código em iterações curtas e frequentes. Isso permite que eles adotar a alteração, refatorar o código com frequência e evitar "big design frontal sobrecarregado".

A Lucerne mantém uma coleção muito maior e complexa de sistemas, alguns dos quais são os mais de 40 anos de idade. Eles são muito cautelosos ao fazer alterações devido à complexidade e ao escopo do código herdado. Eles seguem um processo de desenvolvimento mais rigoroso, preferindo criar soluções detalhadas e documentar as alterações que ocorrem durante o desenvolvimento e design.

Ambas as equipes usam diagramas de modelagem no Visual Studio para ajudá-los a desenvolver sistemas que atendem às necessidades dos usuários. Eles usam o Team Foundation Server junto com outras ferramentas para ajudá-los a planejar, organizar e gerenciar seu trabalho.

Para obter mais informações sobre o Team Foundation Server, consulte:

- [Planejamento e acompanhamento de trabalho](#planning-and-tracking-work)

- [Testando, validando e fazendo check-in de código atualizado](#TestValidateCheckInCode)

## <a name="ModelingDiagramsTools"></a> Funções de arquitetura e diagramas de modelagem no desenvolvimento de Software

A tabela a seguir descreve as funções que essas ferramentas podem executar durante vários e vários estágios do ciclo de vida de desenvolvimento de software:

||**Modelagem dos requisitos de usuário**|**Modelagem de processo empresarial**|**Design e arquitetura do sistema**|**Visualização de código e a exploração**|**Verificação**|
|------|-|-|-|-|-|
|Diagrama de linguagem específica do domínio (DSL)|Sim|Sim|Sim|||
|Diagrama de dependência e validação de camada|||Sim|Sim|Sim|
|Mapa de código|||Sim|Sim|Sim|
|Designer de classe (baseado em código)||||Sim||

Para desenhar diagramas de dependência, você deve criar um projeto de modelagem como parte de uma solução existente ou um novo. Esses diagramas devem ser criados no projeto de modelagem.
Os itens em diagramas de dependência estão localizados no projeto de modelagem, mas elas não são armazenadas no modelo comum. Mapas de código e diagramas de classe .NET criados pelo código existem fora do projeto de modelagem.

Consulte:

- [Criar diagramas de dependência usando seu código](../modeling/create-layer-diagrams-from-your-code.md)

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)

- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

- [SDK de Modelagem para Visual Studio – linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

Ambas as equipes também usam validação de dependência para certificar-se de que o código em desenvolvimento permanece consistente com o design. Consulte:

- [Mantendo código consistente com o Design](#ValidatingCode)

- [Descreve a arquitetura lógica: diagramas de dependência](#DescribeLayers)

- [Validar código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

> [!NOTE]
> Algumas versões do Visual Studio dão suporte a versões somente leitura dos mapas de código e validação de dependência para visualização e modelagem. Para ver quais edições do Visual Studio dão suporte a esse recurso, consulte [suporte de edição para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

## <a name="understand-and-communicate-information-about-the-system"></a>Entender e comunicar informações sobre o sistema

Não há nenhuma ordem prescrita para usando o Visual Studio, diagramas, de modelagem, portanto, você pode usá-los de acordo com suas necessidades ou abordagem. Geralmente, as equipes revisitam seus modelos e de forma iterativa com frequência em todo o projeto. Cada diagrama oferece pontos específicos para ajudá-lo a entender, descrever e comunicar os diferentes aspectos do sistema em desenvolvimento.

O dinner Now e Lucerne se comuniquem entre si e com participantes do projeto usando diagramas como sua linguagem comum. Por exemplo, Dinner Now usa diagramas para executar estas tarefas:

- Visualize o código existente.

- Comunicar-se com Lucerne sobre histórias de usuário novos ou atualizados.

- Identifique alterações que são necessárias para dar suporte a histórias de usuários novos ou atualizados.

A Lucerne usa diagramas para executar estas tarefas:

- Saiba mais sobre o processo de negócios Dinner Now.

- Entenda o design do sistema.

- Se comunicar com a Dinner Now sobre requisitos de usuário novos ou atualizados.

- Atualizações de documento para o sistema.

Os diagramas são integrados com o Team Foundation Server para que as equipes podem planejar, gerenciar e acompanhar seu trabalho mais facilmente. Por exemplo, usar modelos para identificar casos de teste e tarefas de desenvolvimento e estimar seu trabalho. A Lucerne vincula Team Foundation Server itens de trabalho a elementos de modelo para que eles podem monitorar o progresso e certifique-se de que o sistema atende aos requisitos dos usuários. Por exemplo, vinculam casos de uso para itens de trabalho de caso de teste para que possam ver que os casos de uso são atendidos quando todos os testes aprovados.

Antes das equipes de check-in de suas alterações, elas validam o código contra os testes e o design executando as compilações que incluem validação de dependência e os testes automatizados. Isso ajuda a garantir que o código atualizado não entram em conflito com o design e interromper a funcionalidade de trabalho anteriormente.

### <a name="identify-changes-to-the-existing-system"></a>Identificar as alterações no sistema existente

O dinner Now deve estimar o custo de atender o requisito de novo. Isso depende em parte quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos desenvolvedores da Dinner Now cria esses mapas e diagramas de código existente:

|**Mapa ou diagrama**|**programas**|
|-|-|
|*Mapa de código*<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)<br />- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)|As dependências e outros relacionamentos no código.<br /><br /> Por exemplo, Dinner Now pode começar revisando os mapas de código de assembly para uma visão geral dos assemblies e suas dependências. Eles podem detalhar os mapas para explorar namespaces e classes nesses assemblies.<br /><br /> O dinner Now também pode criar mapas para explorar areas particulares e outros tipos de relações no código. Eles usam o Gerenciador de soluções para localizar e selecionar as áreas e relacionamentos de seu interesse.|
|*Diagrama de classe base*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|Classes existentes no código|

 Por exemplo, o desenvolvedor cria um mapa de código. Ela ajusta seu escopo para focalizar nas áreas que serão afetadas pelo novo cenário. Essas áreas são selecionadas e realçadas no mapa:

 ![Gráfico de dependência de Namespace](../modeling/media/namespace_reviewsystem.png)

 **Mapa de código do Namespace**

 O desenvolvedor expande namespaces selecionadas para ver suas classes, métodos e relações:

 ![Gráfico de dependência de namespace expandido](../modeling/media/dep_reviewsystem.png)

 **Mapa de código do namespace expandido com links de grupo cruzado visíveis**

 O desenvolvedor examina o código para localizar as classes e métodos afetados. Para ver os efeitos de cada alteração conforme você faz a eles, gerar mapas de código após cada alteração. Ver [Visualizar código](../modeling/visualize-code.md).

 Para descrever alterações em outras partes do sistema, como componentes ou interações, a equipe pode desenhar esses elementos em quadros de comunicações. Eles também podem desenhar os diagramas a seguir no Visual Studio para que os detalhes podem ser capturados, gerenciados e compreendidos por ambas equipes:

|**Diagramas**|**Descreve**|
|-|-|
|*Diagrama de classe base*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|Classes existentes no código.|

### <a name="ValidatingCode"></a> Manter o código consistente com o Design
 O dinner Now deve se certificar de que os códigos atualizados ficaram consistentes com o design. Eles criam diagramas de dependência que descrevem as camadas de funcionalidade no sistema, especifique as dependências permitidas entre os artefatos de solução deles e associam para essas camadas.

|**Diagrama**|**Descreve**|
|-|-|
|*Diagrama de dependência*<br /><br /> Consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)|A arquitetura lógica do código.<br /><br /> Um diagrama de dependência organiza e mapeia os artefatos em uma solução do Visual Studio para grupos abstratos chamados *camadas*. Essas camadas identificam as funções, tarefas ou funções que esses artefatos executam no sistema.<br /><br /> Diagramas de camada são úteis para descrever o design pretendido do sistema e validação de código em evolução em relação a esse design.<br /><br /> Para criar camadas, arraste itens do Gerenciador de soluções, mapas de código, modo de exibição de classe e Pesquisador de objetos. Para desenhar novas camadas, use a caixa de ferramentas ou clique com botão direito na superfície do diagrama.<br /><br /> Para exibir as dependências existentes, clique com botão direito na superfície do diagrama de camada e, em seguida, clique em **gerar dependências**. Para especificar dependências destinadas, desenhe novas dependências.|

 Por exemplo, o diagrama de dependência a seguir descreve as dependências entre camadas e o número de artefatos que estão associados a cada camada:

 ![Diagrama de dependência do sistema de pagamento integrado](../modeling/media/layer_integrated_dnlucerne.png)

 **Diagrama de dependência**

Para certificar-se de que está em conflito com o design não ocorra durante o desenvolvimento de código, a equipe usa a validação de dependência em compilações que é executada em DevOps do Azure. Eles também pode criar uma tarefa MSBuild personalizada para exigir validação de dependência em suas operações de check-in. Eles usam relatórios de compilação para coletar erros de validação.

Consulte:

- [Usar o designer visual](/azure/devops/pipelines/get-started-designer)

- [Check-in restringido TFVC](/azure/devops/pipelines/build/triggers#gated)

- [Compilar e tarefas de liberação](/azure/devops/pipelines/tasks/index)

### <a name="general-tips-for-creating-and-using-models"></a>Dicas gerais para criar e usar modelos

- A maioria de diagramas consistem em nós que são conectados por linhas. Para cada tipo de diagrama, a caixa de ferramentas fornece tipos diferentes de nós e linhas.

     Para abrir a caixa de ferramentas, nos **modo de exibição** menu, clique em **caixa de ferramentas**.

- Para criar um nó, arraste-o na caixa de ferramentas para o diagrama. Determinados tipos de nós devem ser arrastados para nós existentes. Por exemplo, em um diagrama de componente, uma nova porta deve ser adicionada a um componente existente.

- Para criar uma linha ou uma conexão, clique na ferramenta apropriado na caixa de ferramentas, clique no nó de origem e, em seguida, clique no nó de destino. Algumas linhas podem ser criadas somente entre determinados tipos de nós. Quando você move o ponteiro sobre uma possível fonte ou destino, o ponteiro indica se é possível criar uma conexão.

### <a name="plan-and-track-work"></a>Planejar e acompanhar o trabalho

Diagramas de modelagem do Visual Studio são integrados com o Team Foundation Server para que você pode planejar, gerenciar e acompanhar o trabalho com mais facilidade. Ambas as equipes usam modelos para identificar casos de teste e tarefas de desenvolvimento e estimar seu trabalho. A Lucerne cria e vincula o Team Foundation Server itens para modelar elementos, como casos de uso ou componentes de trabalho. Isso os ajuda a monitorar o andamento e rastrear seu trabalho de volta para os requisitos de usuários. Isso os ajuda a garantir que as alterações continuam atendendo aos requisitos.

Como seu trabalho progride, as equipes atualizam seus itens de trabalho para refletir a hora em que eles passam em suas tarefas. Também monitoram e relatam o status em seu trabalho usando os seguintes recursos do Team Foundation Server:

- Diário *relatórios de burndown* que mostram se eles concluirá o trabalho planejado no tempo esperado. Geram outros relatórios semelhantes do Team Foundation Server para acompanhar o andamento de bugs.

- Uma *planilha de iteração* que usa o Microsoft Excel para ajudar a equipe a monitorar e equilibrar a carga de trabalho entre seus membros. Esta planilha é vinculada ao Team Foundation Server e fornece o foco para discussão durante suas reuniões regulares de progresso.

- Um *painel de desenvolvimento* que usa o Office Project para manter a equipe informada sobre informações importantes do projeto.

Consulte:

- [Sobre as ferramentas do Agile e gerenciamento de projeto Agile](/azure/devops/boards/backlogs/overview?view=vsts)

- [Gráficos, painéis e widgets (serviços de DevOps do Azure)](/azure/devops/report/dashboards/overview?view=vsts)

- [Criar sua lista de pendências e tarefas usando o Project](/azure/devops/boards/backlogs/office/create-your-backlog-tasks-using-project)

### <a name="TestValidateCheckInCode"></a> Testar, validar e verificar o código

Conforme as equipes concluem cada tarefa, eles verificam o código no controle do código-fonte e recebem lembretes do Team Foundation Server, caso eles esqueçam. Antes que o Team Foundation Server aceite seus check-ins, as equipes de executar testes de unidade e validação de dependência para verificar o código em relação a seus casos de teste e o design. Usar o Team Foundation Server para executar compilações, testes de unidade automatizados e validação de dependência regularmente. Isso ajuda a garantir que o código atenda aos seguintes critérios:

- Ele funciona.

- Não dividir previamente código de trabalho.

- Ele não entra em conflito com o design.

O dinner Now tem uma grande coleção de testes automatizados, que a Lucerne pode reutilizar porque quase todos ainda se aplicam. A Lucerne também pode criar esses testes e adicionar novos para cobrir a nova funcionalidade. Ambos também usam o Visual Studio para executar testes manuais.

Para certificar-se de que o código está de acordo com o design, as equipes configuram suas compilações no DevOps do Azure para incluir a validação de dependência. Se qualquer conflito ocorrer, um relatório é gerado com os detalhes.

Consulte:

- [Testando o aplicativo](/azure/devops/test/overview?view=vsts)

- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)

- [Usar controle de versão](http://go.microsoft.com/fwlink/?LinkID=525605)

- [Pipelines do Azure](/azure/devops/pipelines/index?view=vsts)

## <a name="update-the-system-using-visualization-and-modeling"></a>Atualizar o sistema usando a visualização e modelagem

A Lucerne e Dinner Now devem integrar seus sistemas de pagamento. As seções a seguir mostram que os diagramas de modelagem no Visual Studio o ajudam a realizar essa tarefa:

- [Visualizar o código existente: Mapas de código](#VisualizeCode)

- [Defina um glossário de tipos: diagramas de classe](#DefineClasses)

- [Descreve a arquitetura lógica: diagramas de dependência](#DescribeLayers)

Consulte:

- [Visualizar código](../modeling/visualize-code.md)

- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)

- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)

### <a name="VisualizeCode"></a> Visualizar o código existente: Mapas de código

Mapas de código mostram a organização atual e os relacionamentos no código. Itens são representados por *nós* no mapa, e as relações são representadas por *links*. Mapas de código podem ajudá-lo a realizar os seguintes tipos de tarefas:

- Explore o código não familiar.

- Compreenda onde e como uma alteração proposta pode afetar o código existente.

- Localize áreas de complexidade, dependências naturais ou padrões ou outras áreas que podem se beneficiar de melhoria.

Por exemplo, Dinner Now deve estimar o custo de atualização do componente PaymentProcessing. Isso depende em parte quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos desenvolvedores da Dinner Now gera mapas de código do código e ajusta o foco do escopo nas áreas que possam ser afetados pela alteração.

O mapa a seguir mostra as dependências entre a classe de PaymentProcessing e outras partes do sistema do Dinner Now, que aparecem selecionadas:

![Grafo de dependência para o sistema de pagamento do Dinner Now](../modeling/media/dep_dnpayment.png)

**Mapa de códigos para o sistema de pagamento do Dinner Now**

O desenvolvedor explora o mapa, expandindo a classe de PaymentProcessing e selecionando seus membros para ver as áreas que são potencialmente afetadas:

![Métodos dentro de PaymentProcessing e dependências](../modeling/media/depgraph_expandeddn.png)

**Métodos dentro da classe PaymentProcessing e suas dependências**

Elas geram o mapa a seguir para o sistema de pagamento de Lucerne inspecionar suas classes, métodos e as dependências. A equipe vê que o sistema Lucerne também pode exigir para interagir com as outras partes da Dinner Now:

![Gráfico de dependência para o sistema de pagamento de Lucerne](../modeling/media/depgraph_lucernepay.png)

**Mapa de códigos para o sistema de pagamento de Lucerne**

Ambas as equipes trabalham juntos para determinar as alterações que são necessárias para integrar os dois sistemas. Decidem refatorar algum código para que ela será mais fácil de atualizar. A classe PaymentApprover se moverá para o espaço DinnerNow Business e exigirá alguns novos métodos. As classes de Dinner Now que tratam transações terão seu próprio namespace. As equipes criam e usam os itens de trabalho para planejar, organizar e acompanhar seu trabalho. Vinculam os itens de trabalho para modelar elementos onde é útil.

Após reorganizar o código, as equipes de geram um novo mapa de código para ver a estrutura atualizada e relações:

![Gráfico de dependência com código reorganizado](../modeling/media/depgraph_integrated.png)

**Mapa de códigos com código reorganizado**

Este mapa mostra que a classe PaymentApprover agora está no espaço DinnerNow Business e tem alguns novos métodos. As classes de transação Dinner Now agora têm seu próprio namespace de PaymentSystem, que torna mais fácil lidar com esse código mais tarde.

#### <a name="creating-a-code-map"></a>Criar um mapa de código

- Para obter uma visão geral rápida do código-fonte, siga estas etapas para gerar um mapa de código:

     Sobre o **arquitetura** menu, clique em **gerar mapa de código para solução**.

     Para obter uma visão geral rápida do código compilado, crie um mapa de código em branco e, em seguida, arraste os arquivos de assembly ou arquivos binários para a superfície do mapa.

- Para explorar o código específico ou itens de solução, use o Gerenciador de soluções para selecionar itens e relações que você deseja visualizar. Você pode gerar um novo mapa ou adicionar itens selecionados a um mapa existente. Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).

- Para ajudá-lo a explorar o mapa, reorganize o layout para que ele atenda aos tipos de tarefas que você deseja executar.

     Por exemplo, para visualizar em camadas no código, selecione um layout de árvore. Ver [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

#### <a name="summary-strengths-of-code-maps"></a>Resumo: Pontos fortes dos mapas de código
 Mapas de código ajudam a:

- Saiba mais sobre a organização e os relacionamentos no código existente.

- Identificar áreas que podem ser afetadas por uma alteração proposta.

- Localize áreas de complexidade, padrões, camadas ou outras áreas que você pode melhorar de modo a facilitar a manutenção, alterar e reutilizar o código.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descreve**|
|-|-|
|Diagrama de dependência|A arquitetura lógica do sistema. Use a validação de dependência para certificar-se de que o código permaneça consistente com o design.<br /><br /> Para ajudá-lo a identificar dependencys existentes ou dependencys pretendidos, crie um mapa de código e agrupar itens relacionados. Para criar um diagrama de dependência, consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)|
|Diagrama de classe (baseado em código)|Classes existentes no código para um projeto específico.<br /><br /> Para visualizar e modificar uma classe existente no código, use o Designer de classe.<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|

### <a name="DefineClasses"></a> Defina um glossário de tipos: diagramas de classe
 Diagramas de classe definem as entidades, os termos ou os conceitos que participam do sistema e suas relações uns com os outros. Por exemplo, você pode usar esses diagramas durante o desenvolvimento para descrever os atributos e operações para cada classe, independentemente da linguagem de implementação ou estilo.

 Para ajudar Lucerne a descrever e discutir as entidades que participam no caso de uso de processamento de pagamento, eles desenham o diagrama de classe a seguir:

 ![Entidades de pagamento do processo no diagrama de classe](../modeling/media/uml_payentities.png)

 **Entidades de pagamento do processo em um diagrama de classe**

 Este diagrama mostra que um cliente pode ter muitos pedidos e maneiras diferentes de pagar os pedidos. BankAccount e CreditCard herdam de pagamento.

 Durante o desenvolvimento, Lucerne usa o seguinte diagrama de classe para descrever e discutir os detalhes de cada classe:

 ![Processar os detalhes da entidade de pagamento em um diagrama de classe](../modeling/media/uml_payment.png)

 **Detalhes de pagamento do processo no diagrama de classe**

#### <a name="drawing-a-class-diagram"></a>Desenhando um diagrama de classe

Um diagrama de classe tem os seguintes recursos principais:

- Tipos como classes, interfaces e enumerações:

    - Um *classe* é a definição de objetos que compartilham características estruturais ou comportamentais específicas.

    - Uma *interface* define uma parte do comportamento externamente visível de um objeto.

    - Uma *enumeração* é um classificador que contém uma lista de valores literais.

- *Atributos* são valores de um determinado tipo que descrevem cada instância de um *classificador*. Um classificador é um nome geral para tipos, componentes, casos de uso e até atores.

- *Operações* métodos ou funções que instâncias de um classificador podem executar.

- Uma *associação* indica algum tipo de relação entre os dois classificadores.

  - Uma *agregação* é uma associação que indica uma propriedade compartilhada entre classificadores.

  - Um *composição* é uma associação que indica uma relação de inteiro-parte entre classificadores.

    Para mostrar agregações ou composições, defina as **agregação** propriedade em uma associação. **Compartilhado** mostra agregações e **composto** mostra composições.

- Um *dependência* indica que a alterar a definição de um classificador pode alterar a definição de outro classificador.

- Um *generalização* indica que um classificador específico herda parte de sua definição de um classificador geral. Um *realização* indica que uma classe implementa as operações e atributos oferecidos por uma interface.

     Para criar essas relações, use o **herança** ferramenta. Como alternativa, uma realização pode ser representada como uma *pirulito*.

- *Pacotes* são grupos de classificadores, associações, linhas da vida, componentes e outros pacotes. *Importação* relações indicam que um pacote inclui todas as definições de outro pacote.

Como ponto de partida para explorar e discutir as classes existentes, você pode usar o Designer de classe para criar diagramas de classe do código.

- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)

#### <a name="summary-strengths-of-class-diagrams"></a>Resumo: Pontos fortes de diagramas de classe
 Diagramas de classe ajudam você a definir:

- Um glossário de termos para usar ao abordar as necessidades de usuários e as entidades que participam do sistema comuns. Ver [requisitos de usuário do modelo](../modeling/model-user-requirements.md).

- Tipos que são usados por partes do sistema, como componentes, independentemente da sua implementação. Ver [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).

- Relações, como dependências entre tipos. Por exemplo, você pode mostrar que um tipo pode ser associado a várias instâncias de outro tipo.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descrição**|
|-|-|
|Diagrama de dependência|Defina a arquitetura lógica do sistema no que diz respeito às classes.<br /><br /> Use a validação de dependência para certificar-se de que o código permaneça consistente com o design.<br /><br /> Consulte:<br /><br /> - [Criar diagramas de dependência do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)<br />- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />- [Validar o código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)|
|Mapa de código|Visualize a organização e os relacionamentos no código existente.<br /><br /> Para identificar classes, seus relacionamentos e seus métodos, crie um mapa de códigos que mostre esses elementos.<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)|

### <a name="DescribeLayers"></a> Descreve a arquitetura lógica: diagramas de dependência
 Diagramas de dependência descrevem a arquitetura lógica de um sistema organizando os artefatos em sua solução em grupos abstratos ou *camadas*. Os artefatos podem ser muitas coisas, como namespaces, projetos, classes, métodos e assim por diante. As camadas representam e descrevem as funções ou tarefas realizadas pelos artefatos no sistema. Você também pode incluir validação de camada na compilação e operações de check-in para certificar-se de que o código permaneça consistente com seu design.

 Para manter o código consistente com o design, o Dinner Now e Lucerne usam o seguinte diagrama de dependência para validar seu código, à medida que ele evolui:

 ![Diagrama de dependência do sistema de pagamento integrado](../modeling/media/layer_integrated_dnlucerne.png)

 **Diagrama de dependência para o Dinner Now integrado à Lucerne**

 As camadas neste diagrama vincular os artefatos de solução Dinner Now e Lucerne correspondentes. Por exemplo, a camada negócios está vinculada ao espaço DinnerNow Business e seus membros, que agora incluem a classe PaymentApprover. Os links da camada de acesso a recursos ao namespace DinnerNow. As setas, ou *dependências*, especificar que somente a camada comercial pode usar a funcionalidade na camada de acesso aos recursos. Conforme as equipes atualizam o código, validação de camada é executada regularmente para capturar conflitos à medida que eles ocorrem e para ajudar as equipes a resolvê-los rapidamente.

 As equipes trabalham juntas para integrar e testar os dois sistemas de forma incremental. Primeiro certifique-se de que PaymentApprover e o restante da Dinner Now trabalham uns com êxito antes de lidar com o PaymentProcessing.

 O mapa de código a seguir mostra as novas chamadas entre o Dinner Now e o PaymentApprover:

 ![Gráfico de dependência atualizado com o sistema integrado](../modeling/media/depgraph_intsystem.png)

 **Mapa de código com chamadas de método atualizado**

 Após a confirmação de que o sistema funciona conforme o esperado, comentários o código de PaymentProcessing Dinner Now. Os relatórios de validação de camada estão vazios, e o mapa de código resultante mostra que não há mais nenhuma dependência de PaymentProcessing existe:

 ![Gráfico de dependência sem PaymentProcessing](../modeling/media/depgraph_nomore.png)

 **Mapa de código sem PaymentProcessing**

#### <a name="drawing-a-dependency-diagram"></a>Desenhando um diagrama de dependência

Um diagrama de dependência tem os seguintes recursos principais:

- *Camadas* descrevem grupos lógicos de artefatos.

- Um *link* é uma associação entre uma camada e um artefato.

     Para criar camadas de artefatos, arraste itens do Gerenciador de soluções, mapas de código, modo de exibição de classe ou Pesquisador de objetos. Para desenhar novas camadas e, em seguida, vinculá-las aos artefatos, use a caixa de ferramentas ou clique com botão direito na superfície de diagrama para criar as camadas e, em seguida, arraste itens para essas camadas.

     O número em uma camada mostra o número de artefatos que estão associados à camada. Esses artefatos podem ser namespaces, projetos, classes, métodos e assim por diante. Ao interpretar o número de artefatos em uma camada, lembre-se de:

  - Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.

       Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.

  - Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.

    Para ver os artefatos que estão vinculados a uma camada, a dependência com o botão direito e, em seguida, clique em **Exibir Links** para abrir **Gerenciador de camadas**.

- Um *dependência* indica que uma camada pode usar a funcionalidade em outra camada, mas não vice-versa. Um *dependência bidirecional* indica que uma camada pode usar a funcionalidade em outra camada e vice-versa.

     Para exibir as dependências existentes no diagrama de dependência, clique com botão direito na superfície do diagrama e, em seguida, clique em **gerar dependências**. Para descrever dependências pretendidas, desenhe novas dependências.

Consulte:

- [Criar diagramas de dependência usando seu código](../modeling/create-layer-diagrams-from-your-code.md)

- [Diagramas de dependência: referência](../modeling/layer-diagrams-reference.md)

- [Diagramas de dependência: diretrizes](../modeling/layer-diagrams-guidelines.md)

- [Validar código com diagramas de dependência](../modeling/validate-code-with-layer-diagrams.md)

#### <a name="summary-strengths-of-dependency-diagrams"></a>Resumo: Pontos fortes de diagramas de dependência

Diagramas de dependência ajudam a:

- Descreve a arquitetura lógica de um sistema de acordo com a funcionalidade de seus artefatos.

- Certifique-se de que o código em desenvolvimento está de acordo com o design especificado.

#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas

|**Diagrama**|**Descrição**|
|-|-|
|Mapa de código|Visualize a organização e os relacionamentos no código existente.<br /><br /> Para criar camadas, gere um mapa de código e, em seguida, agrupar itens no mapa como camadas potenciais. Arraste os grupos do mapa para o diagrama de dependência.<br /><br /> Consulte:<br /><br /> - [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)|

## <a name="external-resources"></a>Recursos externos

|**Categoria**|**Links**|
|-|-|
|**Fóruns**|- [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />- [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|

## <a name="see-also"></a>Consulte também

- [Visualizar código](../modeling/visualize-code.md)
- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)
- [Usar modelos no desenvolvimento Agile](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)
- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)
