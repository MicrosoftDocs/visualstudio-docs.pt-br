---
title: 'Cenário: Alterar o design usando visualização e modelagem | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-techdebt
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- code visualization [Visual Studio ALM]
- modeling software [Visual Studio ALM]
- software modeling [Visual Studio ALM]
- walkthroughs [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], visualizing code
- walkthrough [Visual Studio ALM], modeling software
- walkthroughs [Visual Studio ALM], modeling software
ms.assetid: ccc80825-a4a0-44fa-a0bb-f95254785a3b
caps.latest.revision: 63
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4dface8e157e44aa09b271446dba68b2779d0a6b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51745765"
---
# <a name="scenario-change-your-design-using-visualization-and-modeling"></a>Cenário: alterar o design usando visualização e modelagem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Certifique-se de que seu sistema de software atende às necessidades dos usuários usando a visualização e modelagem de ferramentas no Visual Studio. Use ferramentas como diagramas de modelagem UML (Unified Language), mapas de código, diagramas de camada e diagramas de classe para:  
  
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
  
- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)  
  
##  <a name="ScenarioOverview"></a> Visão geral do cenário  
 Este cenário descreve episódios de ciclos de vida de desenvolvimento do software de duas empresas fictícias: Dinner Now e Lucerne Publishing. O dinner Now fornece um serviço de entrega de refeições baseado na Web em Seattle. Os clientes podem pedir refeições e pagá-las no site da Web agora do jantar. Os pedidos são então enviados para o restaurante local apropriado para entrega. A Lucerne Publishing, uma empresa de Nova York, tem vários negócios dentro e fora da Web. Por exemplo, eles executarem um site da Web em que os clientes podem postar resenhas de restaurantes.  
  
 A Lucerne recentemente adquirida Dinner Now e deseja fazer as seguintes alterações:  
  
- Integre seus sites da Web, adicionando recursos de critica de restaurante ao Dinner Now.  
  
- Substitua o sistema de pagamento da Dinner Now pelo sistema de Lucerne.  
  
- Expanda o serviço Dinner Now em toda a região.  
  
  O dinner Now usa programação extrema e SCRUM. Eles têm cobertura de teste muito alta e pouco código não suportado. Minimizam os riscos criando pequenas, mas as versões de trabalho de um sistema e, em seguida, adicionando a funcionalidade incrementalmente. Desenvolvem seu código em iterações curtas e frequentes. Isso permite que eles adotar a alteração, refatorar o código com frequência e evitar "big design frontal sobrecarregado".  
  
  A Lucerne mantém uma coleção muito maior e complexa de sistemas, alguns dos quais são os mais de 40 anos de idade. Eles são muito cautelosos ao fazer alterações devido à complexidade e ao escopo do código herdado. Eles seguem um processo de desenvolvimento mais rigoroso, preferindo criar soluções detalhadas e documentar as alterações que ocorrem durante o desenvolvimento e design.  
  
  Ambas as equipes usam diagramas de modelagem no Visual Studio para ajudá-los a desenvolver sistemas que atendem às necessidades dos usuários. Eles usam o Team Foundation Server junto com outras ferramentas para ajudá-los a planejar, organizar e gerenciar seu trabalho.  
  
  Para obter mais informações sobre o Team Foundation Server, consulte:  
  
- [Planejamento e acompanhamento de trabalho](#PlanningTracking)  
  
- [Testando, validando e fazendo check-in de código atualizado](#TestValidateCheckInCode)  
  
##  <a name="ModelingDiagramsTools"></a> Funções de arquitetura e diagramas de modelagem no desenvolvimento de Software  
 A tabela a seguir descreve as funções que essas ferramentas podem executar durante vários e vários estágios do ciclo de vida de desenvolvimento de software:  
  
||**Modelagem dos requisitos de usuário**|**Modelagem de processo empresarial**|**Design e arquitetura do sistema**|**Visualização de código e a exploração**|**Verificação**|  
|------|------------------------------------|-----------------------------------|--------------------------------------|------------------------------------------|----------------------|  
|Diagrama de caso de uso (UML)|√|√|||√|  
|Diagrama de atividade (UML)|√|√|√||√|  
|Diagrama de classes (UML)|√|√|√||√|  
|Diagrama de componente (UML)|√|√|√||√|  
|Diagrama de sequência (UML)|√|√|√||√|  
|Diagrama de linguagem específica do domínio (DSL)|√|√|√|||  
|Diagrama de camada, validação de camada|||√|√|√|  
|Mapa de código|||√|√|√|  
|Designer de classe (baseado em código)||||√||  
  
 Para desenhar diagramas de UML e diagramas de camada, você deve criar um projeto de modelagem como parte de uma solução existente ou um novo. Esses diagramas devem ser criados no projeto de modelagem. Os itens em diagramas UML fazem parte de um modelo comum, e os diagramas UML são exibições desse modelo. Os itens em diagramas de camada estão localizados no projeto de modelagem, mas elas não são armazenadas no modelo comum. Mapas de código e diagramas de classe .NET criados pelo código existem fora do projeto de modelagem.  
  
 Consulte:  
  
- [Criar projetos e diagramas de modelagem UML](../modeling/create-uml-modeling-projects-and-diagrams.md)  
  
- [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)  
  
- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)  
  
- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)  
  
- [SDK de Modelagem para Visual Studio – linguagens específicas de domínio](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)  
  
  Para mostrar exibições alternativas da arquitetura, você pode reutilizar determinados elementos do mesmo modelo em vários diagramas diferentes ou. Por exemplo, você pode arrastar um componente até outro diagrama de componente ou para um diagrama de sequência para que ele pode funcionar como um ator. Ver [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
  Ambas as equipes também usam validação de camada para certificar-se de que o código em desenvolvimento permanece consistente com o design.  
  
  Consulte:  
  
- [Mantendo código consistente com o Design](#ValidatingCode)  
  
- [Descreve a arquitetura lógica: diagramas de camada](#DescribeLayers)  
  
- [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)  
  
  > [!NOTE]
  >  Algumas versões do Visual Studio dão suporte a validação de camada e versões de somente leitura de mapas de código e diagramas UML para visualização e modelagem. Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
##  <a name="UnderstandingCommunicating"></a> Compreender e comunicar informações sobre o sistema  
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
  
  Antes das equipes de check-in de suas alterações, elas validam o código contra os testes e o design executando as compilações que incluem validação de camada e testes automatizados. Isso ajuda a garantir que o código atualizado não entram em conflito com o design e interromper a funcionalidade de trabalho anteriormente.  
  
  Consulte:  
  
- [Noções básicas sobre a função do sistema do processo de negócios](#UnderstandingBPMandSystemDesign)  
  
- [Descrevendo requisitos de usuário novos ou atualizados](#DescribingURM)  
  
- [Criando testes de modelos](#CreatingTests)  
  
- [Identificação de alterações no sistema existente](#DeterminingChanges)  
  
- [Mantendo código consistente com o design](#ValidatingCode)  
  
- [Dicas gerais para criar e usar modelos](#GeneralTips)  
  
- [Planejamento e acompanhamento de trabalho](#PlanningTracking)  
  
- [Testando, validando e fazendo check-in de código atualizado](#TestValidateCheckInCode)  
  
###  <a name="UnderstandingBPMandSystemDesign"></a> Noções básicas sobre a função do sistema do processo de negócios  
 A Lucerne deseja saber mais sobre o processo de negócios Dinner Now. Eles criam os seguintes diagramas para esclarecer seu entendimento com a Dinner Now com mais facilidade:  
  
|**Diagrama**|**Descreve**|  
|-----------------|-------------------|  
|*Diagrama de caso de uso (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)<br />-   [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|-As atividades que o sistema Dinner Now suporta<br />-As pessoas e sistemas externos que executam as atividades<br />-Os principais componentes do sistema que suportam cada atividade<br />-As partes do processo de negócios que estão fora do escopo do sistema atual, por exemplo, entrega de alimento|  
|*Diagrama de atividade (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|O fluxo das etapas que ocorrem quando um cliente cria um pedido|  
|*Diagrama de classes (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|As entidades de negócios e termos usados na discussão e as relações entre essas entidades. Por exemplo, a ordem e o Item de Menu são parte do vocabulário nesse cenário.|  
  
 Por exemplo, a Lucerne cria o seguinte diagrama de caso de uso para entender as tarefas que são executadas no site da Web agora do jantar e quem as executa:  
  
 ![Diagrama de casos de uso UML](../modeling/media/uml-usecase.png "UML_UseCase")  
  
 **Diagrama de Casos de Uso UML**  
  
 O diagrama de atividade a seguir descreve o fluxo das etapas quando um cliente cria um pedido no site da Web agora do jantar. Nesta versão, elementos de comentário identificam as funções e linhas criam *raias*, que organizam as etapas por função:  
  
 ![Diagrama de atividade UML](../modeling/media/uml-dinnernowprocess.png "UML_DinnerNowProcess")  
  
 **Diagrama de Atividade UML**  
  
 O diagrama de classe a seguir descreve as entidades que participam do processo de pedido:  
  
 ![Diagrama de classe UML](../modeling/media/uml-dinnerorders.png "UML_DinnerOrders")  
  
 **Diagrama de Classe UML**  
  
###  <a name="DescribingURM"></a> Descrevendo requisitos de usuário novos ou atualizados  
 A Lucerne deseja adicionar funcionalidade ao sistema do Dinner Now para que os clientes podem ler e contribuir com revisões de restaurante. Eles atualizar os diagramas a seguir para que eles possam descrever e abordar esse novo requisito com a Dinner Now:  
  
|**Diagrama**|**Descreve**|  
|-----------------|-------------------|  
|*Diagrama de caso de uso (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)<br />-   [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|Um novo caso de uso para "Escrever uma revisão de um restaurante"|  
|*Diagrama de atividade (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|As etapas que ocorrem quando um cliente deseja escrever uma resenha de restaurante|  
|*Diagrama de classes (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|Os dados que é necessário para armazenar uma revisão|  
  
 Por exemplo, o seguinte diagrama de caso de uso inclui um novo caso de uso "Gravar revisão" para representar o novo requisito. Ele é realçado em laranja no diagrama para facilitar sua identificação:  
  
 ![Diagrama de casos de uso UML](../modeling/media/uml-writerev.png "UML_WriteRev")  
  
 **Diagrama de casos de uso UML**  
  
 O seguinte diagrama de atividade inclui novos elementos em laranja para descrever o fluxo das etapas no novo caso de uso:  
  
 ![Diagrama de atividade UML](../modeling/media/uml-writereview.png "UML_WriteReview")  
  
 **Diagrama de atividade UML**  
  
 O seguinte diagrama de classe inclui uma nova classe de revisão e suas relações com outras classes, de modo que as equipes possam discutir seus detalhes. Observe que um cliente e um restaurante podem ter várias revisões:  
  
 ![Diagrama de classe UML](../modeling/media/uml-dinnerreviews.png "UML_DinnerReviews")  
  
 **Diagrama de classe UML**  
  
###  <a name="CreatingTests"></a> Criando testes de modelos  
 Ambas as equipes concordam que precisam um conjunto completo de testes para o sistema e seus componentes antes de quaisquer alterações. A Lucerne tem uma equipe especializada que executa o sistema e testes de nível de componente. Eles reutilizam os testes criados pela Dinner Now e estruturam os testes usando diagramas de UML:  
  
- Cada caso de uso é representado por um ou vários testes. Os elementos no link de diagrama de caso de uso para o caso de teste de itens de trabalho no Team Foundation Server.  
  
- Cada fluxo em um diagrama de atividade ou um diagrama de sequência de nível de sistema é associado a um teste na pior das hipóteses. A equipe de teste certifica-se de que testa cada caminho possível pelo diagrama de atividade sistematicamente.  
  
- Os termos usados para descrever os testes são baseados em termos definidos por diagramas de caso, a classe e a atividade de uso.  
  
  Como alterarem de requisitos e os diagramas são atualizados para refletir essas alterações, os testes também são atualizados. Um requisito é considerado preenchido somente quando os testes são aprovados. Quando for possível ou prático, os testes são definidos e com base em diagramas de UML antes do início da implementação.  
  
  Consulte:  
  
- [Desenvolver testes por meio de um modelo](../modeling/develop-tests-from-a-model.md)  
  
- [Validar o modelo UML](../modeling/validate-your-uml-model.md)  
  
###  <a name="DeterminingChanges"></a> Identificação de alterações no sistema existente  
 O dinner Now deve estimar o custo de atender o requisito de novo. Isso depende em parte quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos desenvolvedores da Dinner Now cria esses mapas e diagramas de código existente:  
  
|**Mapa ou diagrama**|**programas**|  
|------------------------|---------------|  
|*Mapa de código*<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)<br />-   [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)|As dependências e outros relacionamentos no código.<br /><br /> Por exemplo, Dinner Now pode começar revisando os mapas de código de assembly para uma visão geral dos assemblies e suas dependências. Eles podem detalhar os mapas para explorar namespaces e classes nesses assemblies.<br /><br /> O dinner Now também pode criar mapas para explorar areas particulares e outros tipos de relações no código. Eles usam o Gerenciador de soluções para localizar e selecionar as áreas e relacionamentos de seu interesse.|  
|*Diagrama de classe base*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|Classes existentes no código|  
  
 Por exemplo, o desenvolvedor cria um mapa de código. Ela ajusta seu escopo para focalizar nas áreas que serão afetadas pelo novo cenário. Essas áreas são selecionadas e realçadas no mapa:  
  
 ![Gráfico de dependência de Namespace](../modeling/media/namespace-reviewsystem.png "Namespace_ReviewSystem")  
  
 **Mapa de código do Namespace**  
  
 O desenvolvedor expande namespaces selecionadas para ver suas classes, métodos e relações:  
  
 ![Gráfico de dependência de namespace expandido](../modeling/media/dep-reviewsystem.png "Dep_ReviewSystem")  
  
 **Mapa de código do namespace expandido com links de grupo cruzado visíveis**  
  
 O desenvolvedor examina o código para localizar as classes e métodos afetados. Para ver os efeitos de cada alteração conforme você faz a eles, gerar mapas de código após cada alteração. Ver [Visualizar código](../modeling/visualize-code.md).  
  
 Para descrever alterações em outras partes do sistema, como componentes ou interações, a equipe pode desenhar esses elementos em quadros de comunicações. Eles também podem desenhar os diagramas a seguir no Visual Studio para que os detalhes podem ser capturados, gerenciados e compreendidos por ambas equipes:  
  
|**Diagramas**|**Descreve**|  
|------------------|-------------------|  
|*Diagrama de atividade (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|O fluxo das etapas que ocorrem quando o sistema observa que um cliente faz um pedido de um restaurante novamente, solicitando que o cliente para escrever uma resenha.|  
|*Diagrama de classes (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|Classes lógicas e suas relações. Por exemplo, uma nova classe é adicionada para descrever uma **revisão** e suas relações com outras entidades, como **restaurante**, **Menu**, e **cliente**.<br /><br /> Para associar revisões com um cliente, o sistema deve armazenar detalhes do cliente. Um diagrama de classe UML pode ajudar a esclarecer esses detalhes.|  
|*Diagrama de classe base*<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|Classes existentes no código.|  
|*Diagrama de componente (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|As partes de alto nível do sistema, como o site da Web agora do jantar e suas interfaces. Essas interfaces definem como os componentes interagem com cada outro através dos métodos ou serviços que eles fornecem e consomem.|  
|*Diagrama de sequência (UML)*<br /><br /> Consulte:<br /><br /> -   [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)<br />-   [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)|A sequência de interações entre as instâncias.|  
  
 Por exemplo, o diagrama de componente a seguir mostra o novo componente, que é uma parte do componente de Site da Dinner Now. O componente ReviewProcessing trata a funcionalidade de criar revisões e é realçado em laranja:  
  
 ![Diagrama de componente UML](../modeling/media/uml-internal.png "UML_Internal")  
  
 **Diagrama de componente UML**  
  
 O diagrama a seguir mostra a sequência de interações que ocorrem quando o Site da Dinner Now verifica se o cliente fez pedido em um restaurante antes. Se isso for verdadeiro, será solicitado que o cliente para criar uma revisão, que é enviada para o restaurante e publicada pelo site da Web:  
  
 ![Diagrama de sequência UML](../modeling/media/uml-revsystem.png "UML_RevSystem")  
  
 **Diagrama de sequência UML**  
  
###  <a name="ValidatingCode"></a> Mantendo código consistente com o Design  
 O dinner Now deve se certificar de que os códigos atualizados ficaram consistentes com o design. Eles criam diagramas de camada que descrevem as camadas de funcionalidade no sistema, especifique as dependências permitidas entre os artefatos de solução deles e associam para essas camadas.  
  
|**Diagrama**|**Descreve**|  
|-----------------|-------------------|  
|*Diagrama de camada*<br /><br /> Consulte:<br /><br /> -   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)<br />-   [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|A arquitetura lógica do código.<br /><br /> Um diagrama de camada organiza e mapeia os artefatos em um [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução para grupos abstratos chamados *camadas*. Essas camadas identificam as funções, tarefas ou funções que esses artefatos executam no sistema.<br /><br /> Diagramas de camada são úteis para descrever o design pretendido do sistema e validação de código em evolução em relação a esse design.<br /><br /> Para criar camadas, arraste itens do Gerenciador de soluções, mapas de código, modo de exibição de classe e Pesquisador de objetos. Para desenhar novas camadas, use a caixa de ferramentas ou clique com botão direito na superfície do diagrama.<br /><br /> Para exibir as dependências existentes, clique com botão direito na superfície do diagrama de camada e, em seguida, clique em **gerar dependências**. Para especificar dependências destinadas, desenhe novas dependências.|  
  
 Por exemplo, o diagrama de camada a seguir descreve as dependências entre camadas e o número de artefatos que estão associados a cada camada:  
  
 ![Diagrama de camada do sistema de pagamento integrada](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")  
  
 **Diagrama de Camada**  
  
 Para certificar-se de que está em conflito com o design não ocorra durante o desenvolvimento de código, a equipe usa a validação de camada nas compilações que é executada no Team Foundation Build. Eles também pode criar uma tarefa MSBuild personalizada para exigir validação de camada em suas operações de check-in. Eles usam relatórios de compilação para coletar erros de validação.  
  
 Consulte:  
  
-   [Definir o processo de compilação](http://msdn.microsoft.com/library/61593e10-d24b-492f-b19a-af4d85abea6b)  
  
-   [Usar um processo de compilação de check-in para validar alterações](http://msdn.microsoft.com/library/9cfc8b9c-1023-40fd-8ab5-1b1bd9c172ec)  
  
-   [Personalizar o modelo de processo de compilação](http://msdn.microsoft.com/library/b94c58f2-ae6f-4245-bedb-82cd114f6039)  
  
###  <a name="GeneralTips"></a> Dicas gerais para criar e usar modelos  
  
- A maioria de diagramas consistem em nós que são conectados por linhas. Para cada tipo de diagrama, a caixa de ferramentas fornece tipos diferentes de nós e linhas.  
  
   Para abrir a caixa de ferramentas, nos **modo de exibição** menu, clique em **caixa de ferramentas**.  
  
- Para criar um nó, arraste-o na caixa de ferramentas para o diagrama. Determinados tipos de nós devem ser arrastados para nós existentes. Por exemplo, em um diagrama de componente, uma nova porta deve ser adicionada a um componente existente.  
  
- Para criar uma linha ou uma conexão, clique na ferramenta apropriado na caixa de ferramentas, clique no nó de origem e, em seguida, clique no nó de destino. Algumas linhas podem ser criadas somente entre determinados tipos de nós. Quando você move o ponteiro sobre uma possível fonte ou destino, o ponteiro indica se é possível criar uma conexão.  
  
- Quando você cria itens em diagramas de UML, você está adicionando-os a um modelo comum. Os diagramas UML em um projeto de modelagem são exibições desse modelo. Itens em um diagrama de camada fazem parte do projeto de modelagem, mesmo que eles não são armazenados no modelo comum.  
  
   Para ver o modelo sobre o **arquitetura** , aponte para **Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
- Em alguns casos, você pode arrastar determinados itens da **Gerenciador de modelos UML** para um diagrama UML. Alguns elementos dentro do mesmo modelo podem ser usados em vários ou alternam diagramas diferentes para mostrar modos de exibição da arquitetura. Por exemplo, você pode arrastar um componente até outro diagrama de componente ou para um diagrama de sequência a ser usado como um ator.  
  
- O Visual Studio suporta UML 2.1.2. Esta visão geral descreve os principais recursos dos diagramas UML nesta versão, mas há muitos livros que abordam o UML e seu uso em detalhes.  
  
  Ver [criar modelos para o aplicativo](../modeling/create-models-for-your-app.md).  
  
###  <a name="PlanningTracking"></a> Planejamento e acompanhamento de trabalho  
 Diagramas de modelagem do Visual Studio são integrados com o Team Foundation Server para que você pode planejar, gerenciar e acompanhar o trabalho com mais facilidade. Ambas as equipes usam modelos para identificar casos de teste e tarefas de desenvolvimento e estimar seu trabalho. A Lucerne cria e vincula o Team Foundation Server itens para modelar elementos, como casos de uso ou componentes de trabalho. Isso os ajuda a monitorar o andamento e rastrear seu trabalho de volta para os requisitos de usuários. Isso os ajuda a garantir que as alterações continuam atendendo aos requisitos.  
  
 Como seu trabalho progride, as equipes atualizam seus itens de trabalho para refletir a hora em que eles passam em suas tarefas. Também monitoram e relatam o status em seu trabalho usando os seguintes recursos do Team Foundation Server:  
  
- Diário *relatórios de burndown* que mostram se eles concluirá o trabalho planejado no tempo esperado. Geram outros relatórios semelhantes do Team Foundation Server para acompanhar o andamento de bugs.  
  
- Uma *planilha de iteração* que usa o Microsoft Excel para ajudar a equipe a monitorar e equilibrar a carga de trabalho entre seus membros. Esta planilha é vinculada ao Team Foundation Server e fornece o foco para discussão durante suas reuniões regulares de progresso.  
  
- Um *painel de desenvolvimento* que usa o Office Project para manter a equipe informada sobre informações importantes do projeto.  
  
  Consulte:  
  
- [Acompanhar o trabalho usando o Visual Studio Team Services ou Team Foundation Server](http://msdn.microsoft.com/library/52aa8bc9-fc7e-4fae-9946-2ab255ca7503)  
  
- [Vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md)  
  
- [Gráficos, painéis e relatórios para o Visual Studio ALM](http://msdn.microsoft.com/library/1f28ba6c-c5e5-46d3-9209-ede24ae78e48)  
  
- [Criar sua lista de pendências e tarefas usando o Project](http://msdn.microsoft.com/library/be5cef4f-755f-4ffe-8dd7-876d1e02c330)  
  
###  <a name="TestValidateCheckInCode"></a> Testando, validando e fazendo check-In de código  
 Conforme as equipes concluem cada tarefa, eles verificam o código no controle de versão do Team Foundation e recebem lembretes do Team Foundation Server, caso eles esqueçam. Antes que o Team Foundation Server aceite seus check-ins, as equipes de executar testes de unidade e validação de camada para verificar o código em relação a seus casos de teste e o design. Usar o Team Foundation Server para executar compilações, testes de unidade automatizados e validação de camada regularmente. Isso ajuda a garantir que o código atenda aos seguintes critérios:  
  
- Ele funciona.  
  
- Não dividir previamente código de trabalho.  
  
- Ele não entra em conflito com o design.  
  
  O dinner Now tem uma grande coleção de testes automatizados, que a Lucerne pode reutilizar porque quase todos ainda se aplicam. A Lucerne também pode criar esses testes e adicionar novos para cobrir a nova funcionalidade. Ambos também usam o Visual Studio para executar testes manuais.  
  
  Para certificar-se de que o código está de acordo com o design, as equipes configuram suas compilações no Team Foundation Build para incluir a validação de camada. Se qualquer conflito ocorrer, um relatório é gerado com os detalhes.  
  
  Consulte:  
  
- [Testando o aplicativo](http://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac)  
  
- [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)  
  
- [Usar controle de versão](http://go.microsoft.com/fwlink/?LinkID=525605)  
  
- [Compilar o aplicativo](http://msdn.microsoft.com/library/a971b0f9-7c28-479d-a37b-8fd7e27ef692)  
  
##  <a name="UpdatingSystem"></a> Atualizando a sistema usando a visualização e modelagem  
 A Lucerne e Dinner Now devem integrar seus sistemas de pagamento. As seções a seguir mostram que os diagramas de modelagem no Visual Studio o ajudam a realizar essa tarefa:  
  
- [Entender os requisitos de usuário: usar diagramas de caso](#UnderstandUseCases)  
  
- [Entender o processo comercial: diagramas de atividade](#UnderstandActivities)  
  
- [Descrever a estrutura do sistema: diagramas de componente](#DescribeComponents)  
  
- [Descreve as interações: diagramas de sequência](#DescribeSequence)  
  
- [Visualizar o código existente: Mapas de código](#VisualizeCode)  
  
- [Defina um glossário de tipos: diagramas de classe](#DefineClasses)  
  
- [Descreve a arquitetura lógica: diagramas de camada](#DescribeLayers)  
  
  Consulte:  
  
- [Criar modelos para o aplicativo](../modeling/create-models-for-your-app.md)  
  
- [Visualizar código](../modeling/visualize-code.md)  
  
- [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)  
  
- [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)  
  
- [Modelar a arquitetura do aplicativo](../modeling/model-your-app-s-architecture.md)  
  
###  <a name="UnderstandUseCases"></a> Entender os requisitos de usuário: usar diagramas de caso  
 Diagramas de caso de uso resumem as atividades que um sistema suporta e quem executa essas atividades. A Lucerne usa um diagrama de caso de uso para aprender o seguinte sobre o sistema Dinner Now:  
  
- Os clientes criam pedidos.  
  
- Os restaurantes recebem pedidos.  
  
- O Gateway externo do processador de pagamento, que o sistema Dinner Now pagamento usa para validar pagamentos, está fora do escopo para o site da Web.  
  
  O diagrama também mostra como alguns dos principais casos de divisão de usar em casos de uso menores. A Lucerne deseja usar seu próprio sistema de pagamento. Realçam o caso de uso de processamento de pagamento em uma cor diferente para indicar que ela requer alterações:  
  
  ![Realce o processamento de pagamento em um diagrama de caso de uso](../modeling/media/uml-processpay.png "UML_ProcessPay")  
  
  **Realce o pagamento do processo no diagrama de caso**  
  
  Se o tempo de desenvolvimento foi curto, a equipe pode discutir se deseja permitir que os clientes diretamente os restaurantes de pagamento. Para mostrar isso, substituiriam o caso de uso de processamento de pagamento por uma que está fora dos limites do sistema Dinner Now. Vinculariam o cliente diretamente ao restaurante, indicando que o Dinner Now processaria somente pedidos:  
  
  ![Compor escopo de pagar restaurante no diagrama de caso](../modeling/media/uml-payrestaurant.png "UML_PayRestaurant")  
  
  **Compor escopo de pagar restaurante no diagrama de caso**  
  
  Consulte:  
  
- [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)  
  
- [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)  
  
#### <a name="drawing-a-use-case-diagram"></a>Desenhando um diagrama de caso de uso  
 Um diagrama de caso de uso tem os seguintes recursos principais:  
  
- *Os atores* representam as funções executadas por pessoas, as organizações, as máquinas ou sistemas de software. Por exemplo, o cliente, o restaurante e o sistema Dinner Now pagamento são atores.  
  
- *Casos de uso* representam interações entre os atores e o sistema em desenvolvimento.  Eles podem representar qualquer escala de interação de um único clique de mouse ou a mensagem a uma transação estendida por muitos dias.  
  
- *Associações* vinculam atores a casos de uso.  
  
- Um caso de uso maior pode *incluem* menores, por exemplo, criar pedido inclui selecionar restaurante. Você pode *estender* um caso de uso, que adiciona metas e etapas para o caso de uso estendido, para indicar que o caso de uso ocorre apenas sob determinadas condições. Casos de uso também podem herdar de cada outro.  
  
- Um *subsistema* representa o sistema de software que está em desenvolvimento ou um de seus componentes. É uma grande caixa que contém os casos de uso. Um diagrama de casos esclarece o que está dentro ou fora dos limites do subsistema. Para indicar que o usuário deve cumprir determinadas metas de outras maneiras, desenhe esses casos de uso fora dos limites do subsistema.  
  
- *Artefatos* vincular elementos no diagrama a outros diagramas ou documentos.  
  
  Consulte:  
  
- [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)  
  
- [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)  
  
#### <a name="summary-strengths-of-use-case-diagrams"></a>Resumo: Pontos fortes de diagramas de caso de uso  
 Diagramas de caso de uso ajudam a visualizar:  
  
-   As atividades que um sistema suporta ou não oferece suporte a  
  
-   As pessoas e sistemas externos que executam as atividades  
  
-   Os principais componentes do sistema que suportam cada atividade, o que você pode representar como subsistemas aninhados dentro do sistema pai  
  
-   Como um caso de uso pode se dividir em menores ou em variações  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descreve**|  
|-----------------|-------------------|  
|Diagrama de atividade|O fluxo das etapas em um caso de uso e aqueles que executam essas etapas em que o caso de uso.<br /><br /> Os nomes dos casos de uso frequentemente espelham as etapas em um diagrama de atividade. Diagramas de atividade suportam elementos como decisões, mesclagens, entradas e saídas, fluxos simultâneos e assim por diante.<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|  
|Diagrama de sequência|A sequência de interações entre os participantes em um caso de uso.<br /><br /> Consulte:<br /><br /> -   [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)<br />-   [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)|  
|Diagrama de classes (UML)|As entidades ou tipos que participam do caso de uso.<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
  
###  <a name="UnderstandActivities"></a> Entender o processo comercial: diagramas de atividade  
 Diagramas de atividade descrevem o fluxo das etapas em um processo comercial e fornecem uma maneira simples de se comunicar de fluxo de trabalho. Um projeto de desenvolvimento pode ter vários diagramas de atividade. Normalmente, uma atividade aborda todas as ações que resultam de uma ação externa, como ordenar uma refeição, atualizar um menu ou adicionar um novo restaurante ao negócio. Uma atividade também pode descrever os detalhes de uma ação complexa.  
  
 A Lucerne atualiza o seguinte diagrama de atividade para mostrar que a Lucerne processa o pagamento e paga o restaurante. Elas substituem o sistema Dinner Now pagamento com o sistema de pagamento de Lucerne conforme realçado:  
  
 ![Sistema de pagamento de Lucerna no diagrama de atividade](../modeling/media/uml-lucerne.png "UML_Lucerne")  
  
 **Substituindo o sistema Dinner Now pagamento no diagrama de atividade**  
  
 A diagrama atualizado ajuda a Lucerna e Dinner Now a visualizar onde o sistema de pagamento de Lucerna se encaixa no processo de negócios. Nesta versão, os comentários são usados para identificar as funções que executam as etapas. Linhas são usadas para criar *raias*, que organizam as etapas por função.  
  
 As equipes também podem considerar discutir um artigo alternativo onde o cliente paga o restaurante após o pedido é entregue. Isso criaria requisitos diferentes para o sistema de software.  
  
 Anteriormente, o Dinner Now desenhou esses diagramas em um quadro de comunicações ou no PowerPoint. Eles agora também usarem o Visual Studio para desenhar esses diagramas para que ambas as equipes podem capturar, entender e gerenciar os detalhes.  
  
 Consulte:  
  
-   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)  
  
-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)  
  
#### <a name="drawing-an-activity-diagram"></a>Desenhando um diagrama de atividade  
 Um diagrama de atividade tem os seguintes recursos principais:  
  
- Uma *inicial do nó* que indica a primeira ação de atividade.  
  
   O diagrama deve sempre ter um de nós.  
  
- *Ações* que descrevem as etapas em que o usuário ou o software executa uma tarefa.  
  
- *Fluxos de controle* que mostram o fluxo entre ações.  
  
- *Nós de decisão* que representam ramificações condicionais no fluxo.  
  
- *Nós de bifurcação* que dividem fluxos únicos em fluxos simultâneos.  
  
- *Nós de final de atividade* que mostram fins da atividade.  
  
   Embora esses nós sejam opcionais, é útil para incluí-los no diagrama para mostrar onde a atividade termina.  
  
  Consulte:  
  
- [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)  
  
- [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)  
  
#### <a name="summary-strengths-of-activity-diagrams"></a>Resumo: Pontos fortes de diagramas de atividade  
 Diagramas de atividade ajudarão-lo a visualizar e descrever o fluxo de controle e informações entre as ações de negócios, sistema ou programa. Essa é uma maneira simple e útil para descrever o fluxo de trabalho ao se comunicar com outras pessoas.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descrição**|  
|-----------------|---------------------|  
|Diagrama de caso de uso|Resume as atividades que cada ator executa.<br /><br /> Consulte:<br /><br /> -   [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)<br />-   [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|  
|Diagrama de componente|Visualize o sistema como uma coleção de partes reutilizáveis que fornecem ou consomem o comportamento por meio de um conjunto bem definido de interfaces.<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|  
  
###  <a name="DescribeComponents"></a> Descrever a estrutura do sistema: diagramas de componente  
 Diagramas de componente descrevem o sistema como uma coleção de partes separáveis que fornecem ou consomem o comportamento por meio de um conjunto bem definido de interfaces. As partes podem estar em qualquer escala e podem se conectar de qualquer maneira.  
  
 Para ajudar Lucerne e Dinner Now a visualizar e discutir os componentes do sistema e suas interfaces, eles criam diagramas de componente a seguir:  
  
 ![Componentes externos no sistema de pagamento](../modeling/media/uml-extdnpayment.png "UML_ExtDNPayment")  
  
 **Componentes do sistema de pagamento Dinner Now**  
  
 Este diagrama mostra tipos diferentes de componentes e suas *dependências*. Por exemplo, o Site da Dinner Now e o sistema de pagamento de Lucerne exigem o Gateway externo do processador de pagamentos validar pagamentos. As setas entre componentes representam as dependências que indicam quais componentes requerem funcionalidade de outros componentes.  
  
 Para usar o sistema de pagamento de Lucerne, o Site da Dinner Now deve ser atualizado para usar as interfaces de inserção e no sistema de pagamento de Lucerne.  
  
 O diagrama a seguir mostra uma configuração específica de componentes para o Site da Dinner Now. Essa configuração indica que qualquer instância do site da Web consiste em quatro *partes*:  
  
- CustomerProcessing  
  
- OrderProcessing  
  
- ReviewProcessing  
  
- PaymentProcessing  
  
  Essas partes são instâncias dos tipos de componente especificado e estão conectados da seguinte maneira:  
  
  ![Componentes de site da Web agora jantar](../modeling/media/uml-dinnernow.png "UML_DinnerNow")  
  
  **Componentes dentro do Dinner Now Web Site**  
  
  O Site da Dinner Now delega seu comportamento para essas partes, que manipulam as funções do site da Web. As setas entre o componente pai e seus componentes do membro mostram *delegações* que indicam quais partes manipulam as mensagens que o pai recebe ou envia através das interfaces.  
  
  Nessa configuração, o componente PaymentProcessing processa pagamentos de cliente. Portanto, ele deve ser atualizado para integrar com o sistema de pagamento de Lucerne. Em outros cenários, várias instâncias de um tipo de componente podem existir no mesmo componente pai.  
  
  Consulte:  
  
- [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)  
  
- [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)  
  
#### <a name="drawing-a-component-diagram"></a>Desenhando um diagrama de componente  
 Um diagrama de componente tem os seguintes recursos principais:  
  
- *Componentes* que representam partes separáveis da funcionalidade do sistema.  
  
- *Portas da interface fornecidas* que representam grupos de mensagens ou chamadas de quais componentes implementam são usadas por outros componentes ou sistemas externos.  
  
- *Portas da interface* que representam grupos de mensagens ou chamadas que os componentes enviam para outros componentes ou sistemas externos. Esse tipo de porta descreve as operações que um componente de pelo menos espera de outros componentes ou sistemas externos.  
  
- *Partes* são membros de componentes e normalmente são instâncias de outros componentes. Uma parte é uma parte do design interno do componente pai.  
  
- *Dependências* que indicam componentes requerem a funcionalidade de outros componentes.  
  
- *As delegações* que indica as partes de um componente de manipulam as mensagens enviadas de ou recebidas pelo componente pai.  
  
  Consulte:  
  
- [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)  
  
- [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)  
  
#### <a name="summary-strengths-of-component-diagrams"></a>Resumo: Pontos fortes de diagramas de componente  
 Diagramas de componente ajudam a visualizar:  
  
-   O sistema como uma coleção de partes separáveis independentemente da linguagem de implementação ou estilo.  
  
-   Componentes com interfaces bem definidas, tornando o design mais fácil de entender e atualizar quando os requisitos mudam.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descrição**|  
|-----------------|---------------------|  
|Mapa de código|Visualize a organização e os relacionamentos no código existente.<br /><br /> Para identificar os candidatos a componentes, crie um código de mapa e agrupe os itens por sua função no sistema.<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)|  
|Diagrama de sequência|Visualize a sequência de interações entre componentes ou as partes dentro de um componente.<br /><br /> Para criar uma linha da vida em um diagrama de sequência de um componente, o componente com o botão direito e, em seguida, clique em **criar linha de vida**.<br /><br /> Consulte:<br /><br /> -   [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)<br />-   [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)|  
|Diagrama de classes (UML)|Defina as interfaces nas portas necessárias ou fornecidas e as classes que implementam a funcionalidade dos componentes.<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
|Diagrama de camada|Descreve a arquitetura lógica do sistema no que diz respeito aos componentes. Use a validação de camada para certificar-se de que o código permaneça consistente com o design.<br /><br /> Consulte:<br /><br /> -   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)<br />-   [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|  
|Diagrama de atividade|Visualize processamento interno que os componentes executam em resposta às mensagens de entrada.<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|  
  
###  <a name="VisualizeCode"></a> Visualizar o código existente: Mapas de código  
 Mapas de código mostram a organização atual e os relacionamentos no código. Itens são representados por *nós* no mapa, e as relações são representadas por *links*. Mapas de código podem ajudá-lo a realizar os seguintes tipos de tarefas:  
  
- Explore o código não familiar.  
  
- Compreenda onde e como uma alteração proposta pode afetar o código existente.  
  
- Localize áreas de complexidade, camadas ou padrões naturais, ou outras áreas que podem se beneficiar de melhoria.  
  
  Por exemplo, Dinner Now deve estimar o custo de atualização do componente PaymentProcessing. Isso depende em parte quanto essa alteração afetará outras partes do sistema. Para ajudá-los a entender isso, um dos desenvolvedores da Dinner Now gera mapas de código do código e ajusta o foco do escopo nas áreas que possam ser afetados pela alteração.  
  
  O mapa a seguir mostra as dependências entre a classe de PaymentProcessing e outras partes do sistema do Dinner Now, que aparecem selecionadas:  
  
  ![Grafo de dependência para o sistema de pagamento do Dinner Now](../modeling/media/dep-dnpayment.png "Dep_DNPayment")  
  
  **Mapa de códigos para o sistema de pagamento do Dinner Now**  
  
  O desenvolvedor explora o mapa, expandindo a classe de PaymentProcessing e selecionando seus membros para ver as áreas que são potencialmente afetadas:  
  
  ![Métodos dentro de PaymentProcessing e dependências](../modeling/media/depgraph-expandeddn.png "DepGraph_ExpandedDN")  
  
  **Métodos dentro da classe PaymentProcessing e suas dependências**  
  
  Elas geram o mapa a seguir para o sistema de pagamento de Lucerne inspecionar suas classes, métodos e as dependências. A equipe vê que o sistema Lucerne também pode exigir para interagir com as outras partes da Dinner Now:  
  
  ![Gráfico de dependência para o sistema de pagamento de Lucerne](../modeling/media/depgraph-lucernepay.png "DepGraph_LucernePay")  
  
  **Mapa de códigos para o sistema de pagamento de Lucerne**  
  
  Ambas as equipes trabalham juntos para determinar as alterações que são necessárias para integrar os dois sistemas. Decidem refatorar algum código para que ela será mais fácil de atualizar. A classe PaymentApprover se moverá para o espaço DinnerNow Business e exigirá alguns novos métodos. As classes de Dinner Now que tratam transações terão seu próprio namespace. As equipes criam e usam os itens de trabalho para planejar, organizar e acompanhar seu trabalho. Vinculam os itens de trabalho para modelar elementos onde é útil.  
  
  Após reorganizar o código, as equipes de geram um novo mapa de código para ver a estrutura atualizada e relações:  
  
  ![Gráfico de dependência com código reorganizado](../modeling/media/depgraph-integrated.png "DepGraph_Integrated")  
  
  **Mapa de códigos com código reorganizado**  
  
  Este mapa mostra que a classe PaymentApprover agora está no espaço DinnerNow Business e tem alguns novos métodos. As classes de transação Dinner Now agora têm seu próprio namespace de PaymentSystem, que torna mais fácil lidar com esse código mais tarde.  
  
#### <a name="creating-a-code-map"></a>Criar um mapa de código  
  
-   Para obter uma visão geral rápida do código-fonte, siga estas etapas para gerar um mapa de código:  
  
     Sobre o **arquitetura** menu, clique em **gerar mapa de código para solução**.  
  
     Para obter uma visão geral rápida do código compilado, crie um mapa de código em branco e, em seguida, arraste os arquivos de assembly ou arquivos binários para a superfície do mapa.  
  
-   Para explorar o código específico ou itens de solução, use o Gerenciador de soluções para selecionar itens e relações que você deseja visualizar. Você pode gerar um novo mapa ou adicionar itens selecionados a um mapa existente. Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md).  
  
-   Para ajudá-lo a explorar o mapa, reorganize o layout para que ele atenda aos tipos de tarefas que você deseja executar.  
  
     Por exemplo, para visualizar em camadas no código, selecione um layout de árvore. Ver [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).  
  
#### <a name="summary-strengths-of-code-maps"></a>Resumo: Pontos fortes dos mapas de código  
 Mapas de código ajudam a:  
  
-   Saiba mais sobre a organização e os relacionamentos no código existente.  
  
-   Identificar áreas que podem ser afetadas por uma alteração proposta.  
  
-   Localize áreas de complexidade, padrões, camadas ou outras áreas que você pode melhorar de modo a facilitar a manutenção, alterar e reutilizar o código.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descreve**|  
|-----------------|-------------------|  
|Diagrama de camada|A arquitetura lógica do sistema. Use a validação de camada para certificar-se de que o código permaneça consistente com o design.<br /><br /> Para ajudá-lo a identificar as camadas existentes ou camadas pretendidas, crie um mapa de código e agrupar itens relacionados. Para criar um diagrama de camada, consulte:<br /><br /> -   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)|  
|Diagrama de componente|Componentes, suas interfaces e suas relações.<br /><br /> Para ajudá-lo a identificar os componentes, crie um código de mapa e agrupe os itens por sua função no sistema.<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|  
|Diagrama de classes (UML)|Classes, seus atributos e operações e suas relações.<br /><br /> Para ajudar a identificar esses elementos, criar um diagrama de classe UML que mostre esses elementos.<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
|Diagrama de classe (baseado em código)|Classes existentes no código para um projeto específico.<br /><br /> Para visualizar e modificar uma classe existente no código, use o Designer de classe.<br /><br /> Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).|  
  
###  <a name="DescribeSequence"></a> Descreve as interações: diagramas de sequência  
 Diagramas de sequência descrevem uma série de interações entre as partes de um sistema. As partes podem ser de qualquer escala. Por exemplo, eles podem variar de objetos individuais em um programa para grandes subsistemas ou a atores externos. As interações podem ser de qualquer escala e tipo. Por exemplo, eles podem variar de mensagens individuais para transações estendidas e podem ser chamadas de função ou mensagens de serviço Web.  
  
 Para ajudar Lucerne e Dinner Now a descrever e discutir as etapas no caso de uso de processamento de pagamento, eles criam o diagrama a seguir o diagrama de componente. As linhas da vida espelham o componente de Site da Dinner Now e suas partes. As mensagens que aparecem entre as linhas de vida seguem as conexões nos diagramas componentes:  
  
 ![Caso de uso do diagrama de sequência para processamento de pagamento](../modeling/media/umlsequence-processpayment.png "UMLSequence_ProcessPayment")  
  
 **Caso de uso do diagrama de sequência para o processamento de pagamento**  
  
 O diagrama de sequência mostra que, quando o cliente cria um pedido, o Site da Dinner Now chama ProcessOrder em uma instância de OrderProcessing. Em seguida, OrderProcessing chama ProcessPayment em PaymentProcessing. Isso continua até que o Gateway externo do processador de pagamentos valide o pagamento. Somente então o controle retorne para o Site da Dinner Now.  
  
 A Lucerne deve estimar o custo de atualização de seus sistemas de pagamento para integrar com o sistema Dinner Now. Para ajudá-los a entender isso, eles também podem criar mapas de código para visualizar o código afetado.  
  
 Consulte:  
  
-   [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)  
  
-   [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)  
  
-   [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)  
  
#### <a name="drawing-a-sequence-diagram"></a>Desenhando um diagrama de sequência  
 Um diagrama de sequência tem os seguintes recursos principais:  
  
- Vertical *linhas da vida* representam atores ou instâncias dos objetos de software.  
  
   Para adicionar um símbolo de ator, que indica que um participante está fora do sistema em desenvolvimento, clique na linha de vida. No **propriedades** janela, defina **ator** para **verdadeiro**. Se o **propriedades** janela não estiver aberta, pressione **F4**.  
  
- Horizontal *mensagens* representam chamadas de método, mensagens de serviço Web ou alguma outra comunicação. *As ocorrências de execução* são retângulos verticais sombreados que aparecem nas linhas de vida e representam os períodos durante o qual receber chamadas de processo de objetos.  
  
- Durante um *síncrono* mensagem, o objeto do remetente aguarda o controle para <\<retornar >> como em uma chamada de função normal. Durante um *assíncrona* mensagem, o remetente pode continuar imediatamente.  
  
- Use <\<criar >> mensagens para indicar a construção de objetos por outros objetos. Ele deve ser a primeira mensagem enviada para o objeto.  
  
  Consulte:  
  
- [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)  
  
- [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)  
  
#### <a name="summary-strengths-of-sequence-diagrams"></a>Resumo: Pontos fortes de diagramas de sequência  
 Diagramas de sequência ajudam a visualizar:  
  
-   O fluxo de controle que transferido entre atores ou objetos durante a execução de um caso de uso.  
  
-   A implementação de uma chamada de método ou uma mensagem.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descrição**|  
|-----------------|---------------------|  
|Diagrama de classes (UML)|Definir as classes que representam as linhas de vida e os parâmetros e retornam valores que são usados em mensagens enviadas entre linhas de vida.<br /><br /> Para criar uma classe de uma linha da vida, clique com botão direito na linha de vida e, em seguida, clique em **criar classe** ou **criar Interface**. Para criar uma linha da vida de um tipo em um diagrama de classe, o tipo com o botão direito e, em seguida, clique em **criar linha de vida**.<br /><br /> Consulte:<br /><br /> -   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)<br />-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)|  
|Diagrama de componente|Descreva os componentes que representam as linhas de vida e as interfaces que fornecem e dissipam o comportamento representado por mensagens.<br /><br /> Para criar uma linha da vida de um diagrama de componente, o componente com o botão direito e, em seguida, clique em **criar linha de vida**.<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|  
|Diagrama de caso de uso|Resume as interações entre usuários e componentes em um diagrama de sequência como um caso de uso, que representa o objetivo de um usuário.<br /><br /> Consulte:<br /><br /> -   [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)<br />-   [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|  
  
###  <a name="DefineClasses"></a> Defina um glossário de tipos: diagramas de classe  
 Diagramas de classe definem as entidades, os termos ou os conceitos que participam do sistema e suas relações uns com os outros. Por exemplo, você pode usar esses diagramas durante o desenvolvimento para descrever os atributos e operações para cada classe, independentemente da linguagem de implementação ou estilo.  
  
 Para ajudar Lucerne a descrever e discutir as entidades que participam no caso de uso de processamento de pagamento, eles desenham o diagrama de classe a seguir:  
  
 ![Processar as entidades de pagamento no diagrama de classe](../modeling/media/uml-payentities.png "UML_PayEntities")  
  
 **Entidades de pagamento do processo em um diagrama de classe**  
  
 Este diagrama mostra que um cliente pode ter muitos pedidos e maneiras diferentes de pagar os pedidos. BankAccount e CreditCard herdam de pagamento.  
  
 Durante o desenvolvimento, Lucerne usa o seguinte diagrama de classe para descrever e discutir os detalhes de cada classe:  
  
 ![Processar os detalhes da entidade de pagamento em um diagrama de classe](../modeling/media/uml-payment.png "UML_Payment")  
  
 **Detalhes de pagamento do processo no diagrama de classe**  
  
 Consulte:  
  
-   [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)  
  
-   [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)  
  
#### <a name="drawing-a-class-diagram"></a>Desenhando um diagrama de classe  
 Um diagrama de classe tem os seguintes recursos principais:  
  
- Tipos como classes, interfaces e enumerações:  
  
  -   Um *classe* é a definição de objetos que compartilham características estruturais ou comportamentais específicas.  
  
  -   Uma *interface* define uma parte do comportamento externamente visível de um objeto.  
  
  -   Uma *enumeração* é um classificador que contém uma lista de valores literais.  
  
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
  
  Consulte:  
  
- [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)  
  
- [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)  
  
- [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)  
  
#### <a name="summary-strengths-of-class-diagrams"></a>Resumo: Pontos fortes de diagramas de classe  
 Diagramas de classe ajudam você a definir:  
  
-   Um glossário de termos para usar ao abordar as necessidades de usuários e as entidades que participam do sistema comuns. Ver [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
-   Tipos que são usados por partes do sistema, como componentes, independentemente da sua implementação. Ver [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).  
  
-   Relações, como dependências entre tipos. Por exemplo, você pode mostrar que um tipo pode ser associado a várias instâncias de outro tipo.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descrição**|  
|-----------------|---------------------|  
|Diagrama de caso de uso|Definir os tipos que são usados para descrever metas e etapas em casos de uso.<br /><br /> Consulte:<br /><br /> -   [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)<br />-   [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)|  
|Diagrama de atividade|Defina os tipos de dados que passam por nós de objeto, pinos de entrada, pinos de saída e nós de parâmetro de atividade.<br /><br /> Consulte:<br /><br /> -   [Diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md)<br />-   [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)|  
|Diagrama de componente|Descreva componentes, suas interfaces e suas relações. Uma classe também pode descrever um componente completo.<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|  
|Diagrama de camada|Defina a arquitetura lógica do sistema no que diz respeito às classes.<br /><br /> Use a validação de camada para certificar-se de que o código permaneça consistente com o design.<br /><br /> Consulte:<br /><br /> -   [Criar diagramas de camada do seu código](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)<br />-   [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)<br />-   [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)|  
|Diagrama de sequência|Definir os tipos de linhas de vida e as operações, parâmetros e retornar valores para todas as mensagens que a linha da vida pode receber.<br /><br /> Para criar uma linha da vida de um tipo em um diagrama de classe, o tipo com o botão direito e, em seguida, clique em **criar linha de vida**.<br /><br /> Consulte:<br /><br /> -   [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)<br />-   [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)|  
|Mapa de código|Visualize a organização e os relacionamentos no código existente.<br /><br /> Para identificar classes, seus relacionamentos e seus métodos, crie um mapa de códigos que mostre esses elementos.<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)|  
  
###  <a name="DescribeLayers"></a> Descreve a arquitetura lógica: diagramas de camada  
 Diagramas de camadas descrevem a arquitetura lógica de um sistema organizando os artefatos em sua solução em grupos abstratos ou *camadas*. Os artefatos podem ser muitas coisas, como namespaces, projetos, classes, métodos e assim por diante. As camadas representam e descrevem as funções ou tarefas realizadas pelos artefatos no sistema. Você também pode incluir validação de camada na compilação e operações de check-in para certificar-se de que o código permaneça consistente com seu design.  
  
 Para manter o código consistente com o design, o Dinner Now e Lucerne usam o seguinte diagrama de camada para validar seu código, à medida que ele evolui:  
  
 ![Diagrama de camada do sistema de pagamento integrada](../modeling/media/layer-integrated-dnlucerne.png "Layer_Integrated_DNLucerne")  
  
 **Diagrama de camada para o Dinner Now integrado à Lucerne**  
  
 As camadas neste diagrama vincular os artefatos de solução Dinner Now e Lucerne correspondentes. Por exemplo, a camada negócios está vinculada ao espaço DinnerNow Business e seus membros, que agora incluem a classe PaymentApprover. Os links da camada de acesso a recursos ao namespace DinnerNow. As setas, ou *dependências*, especificar que somente a camada comercial pode usar a funcionalidade na camada de acesso aos recursos. Conforme as equipes atualizam o código, validação de camada é executada regularmente para capturar conflitos à medida que eles ocorrem e para ajudar as equipes a resolvê-los rapidamente.  
  
 As equipes trabalham juntas para integrar e testar os dois sistemas de forma incremental. Primeiro certifique-se de que PaymentApprover e o restante da Dinner Now trabalham uns com êxito antes de lidar com o PaymentProcessing.  
  
 O mapa de código a seguir mostra as novas chamadas entre o Dinner Now e o PaymentApprover:  
  
 ![Gráfico de dependência atualizado com o sistema integrado](../modeling/media/depgraph-intsystem.png "DepGraph_IntSystem")  
  
 **Mapa de código com chamadas de método atualizado**  
  
 Após a confirmação de que o sistema funciona conforme o esperado, comentários o código de PaymentProcessing Dinner Now. Os relatórios de validação de camada estão vazios, e o mapa de código resultante mostra que não há mais nenhuma dependência de PaymentProcessing existe:  
  
 ![Gráfico de dependência sem PaymentProcessing](../modeling/media/depgraph-nomore.png "DepGraph_NoMore")  
  
 **Mapa de código sem PaymentProcessing**  
  
#### <a name="drawing-a-layer-diagram"></a>Desenhando um diagrama de camada  
 Um diagrama de camada tem os seguintes recursos principais:  
  
- *Camadas* descrevem grupos lógicos de artefatos.  
  
- Um *link* é uma associação entre uma camada e um artefato.  
  
   Para criar camadas de artefatos, arraste itens do Gerenciador de soluções, mapas de código, modo de exibição de classe ou Pesquisador de objetos. Para desenhar novas camadas e, em seguida, vinculá-las aos artefatos, use a caixa de ferramentas ou clique com botão direito na superfície de diagrama para criar as camadas e, em seguida, arraste itens para essas camadas.  
  
   O número em uma camada mostra o número de artefatos que estão associados à camada. Esses artefatos podem ser namespaces, projetos, classes, métodos e assim por diante. Ao interpretar o número de artefatos em uma camada, lembre-se de:  
  
  - Se uma camada estiver vinculada a um artefato que contenha outros artefatos, mas não estiver vinculada diretamente a outros artefatos, o número incluirá apenas o artefato vinculado. No entanto, os outros artefatos estão incluídos para análise durante a validação da camada.  
  
     Por exemplo, se uma camada estiver vinculada a um único namespace, o número de artefatos vinculados será 1, mesmo se o namespace contiver classes. Se a camada também tiver links para cada classe no namespace, o número incluirá as classes vinculadas.  
  
  - Se uma camada contiver outras camadas vinculadas a artefatos, a camada de contêiner também estará vinculada a esses artefatos, mesmo que o número na camada de contêiner não inclua esses artefatos.  
  
    Para ver os artefatos que estão vinculados a uma camada, a camada com o botão direito e, em seguida, clique em **Exibir Links** para abrir **Gerenciador de camadas**.  
  
- Um *dependência* indica que uma camada pode usar a funcionalidade em outra camada, mas não vice-versa. Um *dependência bidirecional* indica que uma camada pode usar a funcionalidade em outra camada e vice-versa.  
  
   Para exibir as dependências existentes no diagrama de camada, clique com botão direito na superfície do diagrama e, em seguida, clique em **gerar dependências**. Para descrever dependências pretendidas, desenhe novas dependências.  
  
  Consulte:  
  
- [Criar diagramas de camada por meio de código](../modeling/create-layer-diagrams-from-your-code.md)  
  
- [Diagramas de camada: referência](../modeling/layer-diagrams-reference.md)  
  
- [Diagramas de camada: diretrizes](../modeling/layer-diagrams-guidelines.md)  
  
- [Validar o código com diagramas de camada](../modeling/validate-code-with-layer-diagrams.md)  
  
#### <a name="summary-strengths-of-layer-diagrams"></a>Resumo: Pontos fortes de diagramas de camada  
 Diagramas de camada ajudarão-lo:  
  
-   Descreve a arquitetura lógica de um sistema de acordo com a funcionalidade de seus artefatos.  
  
-   Certifique-se de que o código em desenvolvimento está de acordo com o design especificado.  
  
#### <a name="relationship-to-other-diagrams"></a>Relação com Outros Diagramas  
  
|**Diagrama**|**Descrição**|  
|-----------------|---------------------|  
|Mapa de código|Visualize a organização e os relacionamentos no código existente.<br /><br /> Para criar camadas, gere um mapa de código e, em seguida, agrupar itens no mapa como camadas potenciais. Arraste os grupos do mapa para o diagrama de camada.<br /><br /> Consulte:<br /><br /> -   [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)<br />-   [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)|  
|Diagrama de componente|Descreva componentes, suas interfaces e suas relações.<br /><br /> Para visualizar camadas, crie um diagrama de componente que descreve a funcionalidade dos diferentes componentes no sistema.<br /><br /> Consulte:<br /><br /> -   [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)<br />-   [Diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md)|  
  
## <a name="external-resources"></a>Recursos externos  
  
|**Categoria**|**Links**|  
|------------------|---------------|  
|**Fóruns**|-   [Visualização do Visual Studio e ferramentas de modelagem](http://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visualização do Visual Studio e modelagem (ferramentas DSL) do SDK](http://go.microsoft.com/fwlink/?LinkId=184721)|  
  
## <a name="see-also"></a>Consulte também  
 [Visualizar código](../modeling/visualize-code.md)   
 [Criar modelos para seu aplicativo](../modeling/create-models-for-your-app.md)   
 [Usar modelos no processo de desenvolvimento](../modeling/use-models-in-your-development-process.md)   
 [Usar modelos no desenvolvimento Agile](http://msdn.microsoft.com/en-us/592ac27c-3d3e-454a-9c38-b76658ed137f)   
 [Validar o sistema durante o desenvolvimento](../modeling/validate-your-system-during-development.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)



