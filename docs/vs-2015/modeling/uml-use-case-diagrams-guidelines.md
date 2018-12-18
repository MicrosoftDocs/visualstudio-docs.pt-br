---
title: 'Diagramas de caso de uso UML: Diretrizes | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: b1ae8ed0-d00b-4f9b-8e23-733e09e81e9b
caps.latest.revision: 38
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b4a4bc02202f8ec1f41052dcdea63d97bbcb9671
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51793081"
---
# <a name="uml-use-case-diagrams-guidelines"></a>Diagramas de caso de uso UML: diretrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode desenhar um *diagrama de caso de uso* para resumir a quem usa o aplicativo ou sistema e o que podem fazer com ele. Para criar um diagrama de caso de uso UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
 Para uma demonstração em vídeo, consulte [organizar recursos em casos de uso](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-2-Organizing-Features-Into-Use-Cases/).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Com a Ajuda de um diagrama de caso de uso, você pode discutir e comunicar-se:  
  
- Os cenários em que seu aplicativo ou sistema interage com sistemas externos, organizações ou pessoas.  
  
- As metas que ele ajuda a esses atores alcançar.  
  
- O escopo do seu sistema.  
  
  Um diagrama de caso de uso não mostra os detalhes dos casos de uso: apenas resume algumas das relações entre casos de uso, atores e sistemas. Em particular, o diagrama não mostra a ordem na qual as etapas são executadas para atingir as metas de cada caso de uso. Você pode descrever os detalhes em outros diagramas e documentos, que você pode vincular a cada caso de uso. Para obter mais informações, consulte [casos de uso que descrevem detalhadamente](#Details) neste tópico.  
  
  As descrições que você fornecer para casos de uso usará vários termos relacionados ao domínio em que o sistema funciona, como a venda, o Menu, o cliente e assim por diante. É importante definir claramente esses termos e suas relações, e você pode fazer isso com a Ajuda de um diagrama de classe UML. Para obter mais informações, consulte [diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md).  
  
  Casos de uso lidam apenas em requisitos funcionais de um sistema. Outros requisitos, como regras de negócio, qualidade de serviço requisitos e restrições de implementação devem ser representados separadamente. Arquitetura e os detalhes internos também devem ser descritos separadamente. Para obter mais informações sobre como definir os requisitos de usuário, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
  Os exemplos usados neste tópico estão relacionadas a um site da Web no qual os clientes podem pedir refeições de restaurantes locais.  
  
  ![Elementos em um diagrama de caso de uso](../modeling/media/uml-ucovactor.png "UML_UCOvActor")  
  
- Uma *ator* (1) é uma classe de pessoa, organização, dispositivo ou componente de software externo que interage com seu sistema. Exemplo de atores é **Customer**, **restaurante**, **Sensor de temperatura**, **autorizador de cartão de crédito.**  
  
- Um *caso de uso* (2) representa as ações executadas por um ou mais atores na busca de uma meta específica. São exemplos de casos de uso **Meal Order**, **Menu de atualização**, **processamento de pagamento**.  
  
   Em um diagrama de caso de uso, casos de uso estão associados (3) com os atores que realizá-las.  
  
- Sua *sistema (4)* é tudo o que você está desenvolvendo. Pode ser um pequeno componente de software, cujos atores são apenas para outros componentes de software; ou pode ser um aplicativo completo; ou pode ser um conjunto distribuído grande dos aplicativos implantados em vários computadores e dispositivos. Subsistemas de exemplo estão **site de ordenação refeição**, **refeição entrega Business**, **versão 2 do site**.  
  
   Um diagrama de caso de uso pode mostrar quais casos de uso são compatíveis com seu sistema ou seus subsistemas.  
  
##  <a name="BasicSteps"></a> Etapas básicas para desenhar diagramas de caso de uso  
  
> [!NOTE]
>  Etapas detalhadas para a criação de qualquer um dos diagramas de modelagem são descritas em [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
#### <a name="to-create-a-new-use-case-diagram"></a>Para criar um novo diagrama de caso de uso  
  
1.  Sobre o **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
2.  Sob **modelos**, clique em **diagrama de caso de UMLUse**.  
  
3.  Nomeie o diagrama.  
  
4.  Na **adicionar ao projeto de modelagem**, selecione um projeto de modelagem existente na sua solução, ou **criar um novo projeto de modelagem**e, em seguida, clique em **Okey**.  
  
#### <a name="to-draw-a-use-case-diagram"></a>Para desenhar um diagrama de caso de uso  
  
1.  Arraste **subsistema** os limites da caixa de ferramentas para o diagrama, para representar seu sistema inteiro ou seus componentes principais.  
  
    -   Você pode desenhar um diagrama de caso de uso sem limites, se você deseja descrever quais casos de uso não têm suporte do sistema pelo seu sistema ou seus componentes.  
  
    -   Arraste o canto de um sistema para aumentá-lo, se for necessário.  
  
    -   Renomeie-a adequadamente.  
  
2.  Arraste **atores** da caixa de ferramentas para o diagrama (colocando-os fora do limite de qualquer sistema).  
  
    -   Os atores representam classes de usuários, as organizações e sistemas externos que interagem com o seu sistema.  
  
    -   Renomeie-os. Por exemplo: **agência do cliente, restaurante, cartão de crédito.**  
  
3.  Arraste **casos de uso** Toolbox para os sistemas apropriados.  
  
    -   Casos de uso representam as atividades que os atores executam com a Ajuda do seu sistema.  
  
    -   Renomeie-os usando títulos que entende os atores em si. Não use títulos que estão relacionados ao seu código. Por exemplo: **Meal Order, pague refeição, entregar refeição**.  
  
    -   Começar com transações principais, como **Meal Order**, deixando até posteriores interações menores, como **selecione o Item de Menu**.  
  
    -   Coloque cada caso de uso no sistema ou subsistema principal que dá suporte a ele (ignorando qualquer fachada ou o componente envolvido somente na conexão com o usuário).  
  
    -   Você pode desenhar um caso de uso fora dos limites do sistema para mostrar que ele não é suportado pelo seu sistema, talvez em uma versão específica ou versão.  
  
4.  Clique em **associação** na caixa de ferramentas, um caso de uso e, em seguida, um ator que participa no caso de uso. Vincule cada ator para seus casos de uso dessa maneira.  
  
5.  Casos de estrutura, o uso com o **Include**, **estender** e **generalização** relações. Para criar cada um desses links, clique na ferramenta, em seguida, a fonte de caso de uso, em seguida, o destino. Consulte a seção intitulada [estruturação de casos de uso](#Structuring).  
  
6.  Descreva os casos de uso em mais detalhes. Consulte a seção intitulada [casos de uso que descrevem detalhadamente](#Details).  
  
7.  Desenhe diagramas separados para se concentrar em subsistemas diferentes ou em diferentes grupos de casos de uso relacionados. Todos os diagramas em um projeto de modelagem são exibições do mesmo modelo.  
  
##  <a name="Actors"></a> Desenho de atores e casos de uso  
 O objetivo principal de um diagrama de caso de uso é mostrar que interage com seu sistema e as principais metas que eles atingem com ele.  
  
-   Crie **atores** para representar as classes de pessoas, as organizações, outros sistemas, software ou dispositivos que interagem com seu sistema ou subsistema.  
  
    -   Para saber como desenhar atores e outros elementos, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
    -   Para cada conjunto distinto de metas, identifique os atores por seu tipo ou função, mesmo que as pessoas físicas ou entidades podem ser o mesmo. Por exemplo, o restaurante e clientes são atores separados, mesmo que um funcionário do restaurante, às vezes, pode ser um cliente.  
  
-   Crie **casos de uso** para cada um dos objetivos de cada ator procura obter com o sistema.  
  
    -   Nomear e descrever os casos de uso em palavras que o ator entenderia, em vez de termos de implementação.  
  
-   Use **associações** vincular atores a casos de uso.  
  
### <a name="inheritance-between-actors"></a>Herança entre atores  
 ![Diagrama de caso de uso mostrando herança](../modeling/media/uml-ucguideinherit.png "UML_UCGuideInherit")  
  
 Você pode desenhar um **generalização** link entre atores. O ator especializado, como o cliente Club no exemplo, herda os casos de uso do ator generalizado, como o cliente. Ponta de seta deve apontar para o ator mais geral, como o cliente. Quando você cria o link, aponte primeiro o ator mais especializado.  
  
 O ator especializado pode ter seus próprio casos de uso adicionais que não estão disponíveis para os outros atores.  
  
> [!CAUTION]
>  Você não deve fazer loops de relações de generalização que resultam em um ator generalizar em si. Loops podem gerar erros.  
  
### <a name="alternative-actor-icons"></a>Ícones de ator alternativo  
 Você pode usar ícones personalizados para representar um ator, em vez da figura de pilha padrão. Por exemplo, você pode alterá-lo para se parecer com um dispositivo, restaurante, bancário e assim por diante.  
  
##### <a name="to-change-the-appearance-of-an-actor"></a>Para alterar a aparência de um ator  
  
1.  O ator com o botão direito e, em seguida, clique em **propriedades**.  
  
     O **propriedades** janela é exibida.  
  
2.  Defina as **caminho da imagem** propriedade para o local de um arquivo de imagem.  
  
    -   Você pode usar qualquer um dos vários formatos de imagem, incluindo. bmp,. jpg e. gif.  
  
    -   Use um arquivo que está incluído no controle de fonte de solução ou projeto para que ele ainda está disponível quando a solução é movida ou copiada.  
  
3.  Para replicar essa aparência em outros diagramas de caso de uso, copie o ator e cole-o em outro diagrama.  
  
    -   A alteração da imagem se aplica somente ao modo de exibição em um diagrama específico. Ele não se aplica ao elemento de modelo subjacente. Se você arrastar o ator do Gerenciador de modelos UML para outro diagrama, ele será exibido como a figura de pilha padrão.  
  
### <a name="multiplicities-between-actors-and-use-cases"></a>Multiplicidades entre os atores e casos de uso  
 A associação entre um ator e um caso de uso pode mostrar uma *multiplicidade* em cada extremidade.  
  
 ![Use o caso de um-para-um com ator](../modeling/media/uml-ucguidemulti1.png "UML_UCGuideMulti1")  
  
> [!NOTE]
>  As multiplicidades de uma associação em um diagrama de caso de uso estão ocultos se eles estiverem **1**.  
  
 Por padrão, é cada multiplicidade **1**. Em uma interpretação estrita do modelo, uma multiplicidade de 1 significa que, por exemplo, apenas um cliente está envolvido na ordem de cada uma delas e que cada cliente solicita uma só refeição por vez.  
  
 Você pode alterar esses multiplicidades.  
  
 Por exemplo:  
  
 ![Caso de uso mostrando muitos para muitos multiplicidade](../modeling/media/uml-ucguidemulti2.png "UML_UCGuideMulti2")  
  
- Para que vários atores da mesma classe podem fazer parte de uma única ocorrência de um caso de uso de estado, configure a multiplicidade do final de ator da associação para * * 1... \\***.  
  
   Na ilustração, um ou mais restaurantes podem levar parte do atendimento a mesma ordem refeição.  
  
- Para mostrar que cada ator pode participar ao mesmo tempo em várias ocorrências de um caso de uso, configure a multiplicidade no final da associação para caso use * *\\* * *.  
  
   Na ilustração, cada restaurante pode trabalhar em suprir mais de uma ordem por vez.  
  
##### <a name="to-set-multiplicities-on-an-association"></a>Para definir as multiplicidades em uma associação  
  
1. A associação com o botão direito e, em seguida, clique em **propriedades**.  
  
2. Expanda o **função primeiro** ou **segunda função**.  
  
    *Função* significa que o elemento em uma extremidade da associação.  
  
3. Defina a propriedade de multiplicidade, escolhendo na lista:  
  
   - **1** afirmar que exatamente uma instância dessa função participa de cada link.  
  
   - **1...\\*** para o estado que participam de uma ou mais instâncias dessa função em cada link.  
  
   - **entre 0 e 1** declarar que a participação é opcional.  
  
   - **\\*** para o estado que participam de zero ou mais instâncias dessa função no link.  
  
> [!NOTE]
>  Muitas equipes não coloque informações de multiplicidade em diagramas de caso de uso, deixando as multiplicidades no valor padrão de 1. Em vez disso, eles fornecem as informações nas descrições separadas dos casos de uso. Nesse caso, todas as multiplicidades nos diagramas de caso de uso serão ocultadas.  
  
### <a name="using-an-actor-or-use-case-on-multiple-diagrams"></a>Usando um ator ou caso de uso em vários diagramas  
 Você pode mostrar os mesmos atores e casos de uso em vários diagramas. Por exemplo:  
  
-   Você pode descrever em diagramas diferentes os diferentes casos de uso em que um ator é envolvido.  
  
-   Você pode usar um diagrama para mostrar os atores e os subsistemas ao qual um caso de uso está associado e usar outro diagrama para mostrar como o caso de uso é estruturado em casos de uso incluídos e estendido.  
  
##### <a name="to-show-the-same-actor-or-use-case-on-different-diagrams"></a>Para mostrar o mesmo ator ou caso de uso em diagramas diferentes  
  
1.  Crie o ator ou caso de uso em um diagrama.  
  
2.  Crie outro diagrama de caso de uso.  
  
3.  Arraste um ator ou caso de uso **Gerenciador de modelos** para o novo diagrama.  
  
    > [!NOTE]
    >  Se você colocar no novo diagrama, um ator e um caso de uso que já estão associados, a associação entre elas aparecerão automaticamente no novo diagrama.  
  
##  <a name="Details"></a> Casos de uso que descreve em detalhes  
 Representa um caso de uso:  
  
- Uma meta de um ator usando o sistema, como **comprar uma refeição**; e  
  
- Um ou mais *cenários*, ou seja, sequências de etapas executadas em saber a meta, tais como: {**Meal Order, pagamento, distribua**}. Além dos cenários de êxito, pode haver várias exceções ou cenários de falha, como **rejeitadas de cartão de crédito**.  
  
  Um caso de uso pode ser descrito em diferentes níveis de detalhes. Em um estágio inicial de design, apenas o nome no diagrama de caso de uso é suficiente.  Posteriormente, descrições mais detalhadas dos cenários podem ser gravadas.  
  
  No Visual Studio Ultimate, você pode descrever um caso de uso de várias maneiras, que pode ser usado separadamente ou em conjunto:  
  
- Vincule o caso de uso para outro diagrama ou diagramas no projeto.  
  
  -   Um diagrama de atividade o ajuda a explicar um processo mais complexo em que há loops, ramificações e threads paralelos. Ele também pode mostrar o fluxo de dados entre partes do processo. Para obter mais informações, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
  -   Um diagrama de sequência ajuda a explicar uma série complexa de interações entre diferentes atores. Você também pode usá-lo para mostrar o que acontece dentro do sistema em resposta a cada caso de uso. Para obter mais informações, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
- Vincule o caso de uso para uma página do OneNote, seção ou parágrafo que descreve o caso de uso em detalhes.  
  
- Vincule o caso de uso para um documento do Word, em que você usar texto, capturas de tela, e assim por diante para descrever os cenários de caso de uso. Para obter mais informações, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
#### <a name="to-link-a-use-case-to-a-diagram-or-file-in-the-same-solution"></a>Para vincular um caso de uso em um diagrama ou um arquivo na mesma solução  
  
1.  Desenhe um diagrama como um diagrama de sequência ou um diagrama de atividade para ilustrar um cenário de caso de uso.  
  
2.  Volte para o diagrama de caso de uso.  
  
3.  Arraste o arquivo ou o diagrama no Gerenciador de soluções em uma parte em branco do diagrama de caso.  
  
4.  Conectar-se de que o artefato para o caso de uso usando um **dependência**.  
  
#### <a name="to-link-to-a-solution-file-such-as-a-word-document-or-powerpoint-presentation"></a>Para vincular a um arquivo de solução como um documento do Word ou apresentação do PowerPoint  
  
1.  Escreva um documento que usa o texto, capturas de tela, e assim por diante para descrever o cenário de caso de uso.  
  
2.  Adicione o documento à solução.  
  
    1.  Mova o documento do Word na mesma pasta do Windows como a solução.  
  
    2.  No Gerenciador de soluções, clique com botão direito a solução, aponte para **Add**e, em seguida, clique em **Item existente**.  
  
    3.  Navegue até o documento do Word e clique em **adicionar**.  
  
         O documento do Word é exibido em uma pasta de solução no Gerenciador de soluções.  
  
3.  Arraste o documento do Word no Gerenciador de soluções em uma parte em branco do diagrama de caso.  
  
     Um novo artefato é exibida.  
  
4.  Conectar-se de que o artefato para o caso de uso usando um **dependência**.  
  
#### <a name="to-link-to-a-shared-document-onenote-element-or-web-page"></a>Para vincular a um documento compartilhado, o OneNote elemento ou página da web  
  
1.  Obter a URL do elemento de dados compartilhado. Isso pode ser, por exemplo, um início de caminho do arquivo de rede '\\\\', ou uma página da web ou URL do Sharepoint início 'http://' ou um link para uma seção do OneNote, página ou início de parágrafo ' onenote:'.  
  
2.  Na caixa de ferramentas, clique em **artefato** e, em seguida, clique no diagrama de caso.  
  
3.  Com o novo artefato selecionado, digite ou cole a URL para o **hiperlink** propriedade.  
  
> [!NOTE]
>  Clique duas vezes em um artefato para abrir o diagrama ou de documento para que ele é vinculado.  
  
### <a name="linking-use-cases-to-work-items"></a>Vincular casos de uso a itens de trabalho  
 Se seu projeto usa [!INCLUDE[vstsTfsRosarioLong](../includes/vststfsrosariolong-md.md)] e você tiver [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], você pode vincular um item de trabalho em cada caso de uso [!INCLUDE[esprfound](../includes/esprfound-md.md)]. Para saber como fazer com que esses links, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).  
  
 Isso permite que você:  
  
-   Descreva o caso de uso do item de trabalho vinculado. Em particular, se seu projeto usa o Visual Studio Formal modelo de processo, você pode vincular a um Item de trabalho de caso de uso. Esse tipo de item de trabalho fornece campos para descrever as metas e os cenários de caso de uso.  
  
-   Vincular casos de teste para o caso de uso, para que você pode obter relatórios sobre quanto o código que está sendo desenvolvido implementa o caso de uso.  
  
-   Vincular tarefas para o caso de uso para que você possa acompanhar o andamento do trabalho de desenvolvimento.  
  
##  <a name="Structuring"></a> Estruturar os casos de uso  
 Você deve tentar descrevem o comportamento do seu sistema com apenas alguns casos de uso importantes. Cada caso de uso de grandes define uma grande meta um ator alcança, como comprar um produto ou, do ponto de vista do fornecedor, oferecendo produtos para venda.  
  
 Quando você tiver feito essas metas limpar, você pode ir em mais detalhes sobre como o cada objetivo é alcançado e variações nos objetivos básicos.  
  
 Evite a decomposição de casos de uso em muitos detalhes. Casos de uso são sobre a experiência dos usuários do seu sistema, em vez de seu funcionamento interno. Além disso, você normalmente achará mais produtivo para criar versões de trabalho iniciais do código, em vez de gastar tempo estruturação de casos de uso em muitos detalhes.  
  
 Você pode resumir em um diagrama de caso de uso as relações entre casos de uso principal e mais detalhadas. As seções a seguir descrevem isso:  
  
-   [Mostrando os detalhes de um caso de uso com Include](#Include)  
  
-   [Metas de compartilhamento com a generalização](#Inheritance)  
  
-   [Separar casos de variante com Extend](#Extend)  
  
###  <a name="Include"></a> Mostrando os detalhes de um caso de uso com Include  
 Usar um **Include** relação para mostrar que um caso de uso descreve alguns dos detalhes de outro. Na ilustração, a **ordenar uma refeição** inclui **pagar**, **escolha Menu**, e **escolha o Item de Menu**. Cada um dos casos de uso mais detalhado, incluído é uma etapa que o ator ou atores talvez precise executar para alcançar a meta geral de caso de uso incluindo. A seta deve apontar o caso de uso mais detalhado, incluído.  
  
> [!CAUTION]
>  Você não deve fazer loops de incluir relações que resultam em um caso de uso, incluindo ele próprio. Loops podem gerar erros.  
  
 Você pode compartilhar os casos de uso incluídos. No exemplo, o **ordenar uma refeição** e **inscrever-se às análises** incluem de casos de uso **pagar**.  
  
 ![Casos de uso decompostos com incluem](../modeling/media/uml-ucguideinclude.png "UML_UCGuideInclude")  
  
 A meta e cenários de um caso de uso incluídos devem fazer sentido independentemente para que ele pode ser incluído nos casos de uso que são criados posteriormente.  
  
 Separar casos de uso na inclusão e incluídas partes é útil para atingir as metas a seguir:  
  
-   As descrições de caso de uso em diferentes camadas de detalhes da estrutura.  
  
-   Evite repetir cenários compartilhados nos casos de uso diferentes.  
  
####  <a name="Steps"></a> Definir a ordem das etapas detalhadas  
 O diagrama de caso de uso não diz nada sobre a ordem na qual as etapas mais detalhadas devem ser executadas, nem sobre como se cada um deles é sempre necessário.  
  
 Para tornar a ordem de limpar as etapas, você pode usar um **artefato** para anexar um documento separado para o, incluindo caso de uso. No exemplo a seguir, um diagrama de atividade anexado à ordem de um caso de uso refeição. Como alternativa, você pode usar um documento de texto que tem uma lista de etapas ou uma sequência de capturas de tela. Para obter mais informações, consulte [casos de uso que descrevem detalhadamente](#Details).  
  
 Quando você usa um diagrama de atividade, observe estas convenções de nomenclatura:  
  
- O nome da atividade inteira é o mesmo que o caso de uso incluindo.  
  
- As ações no diagrama de atividade têm os mesmos nomes que o incluído casos de uso.  
  
  Para obter mais informações, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
  ![Use as etapas casos mostradas no diagrama de atividade vinculada](../modeling/media/uml-ucguidesteps.png "UML_UCGuideSteps")  
  
###  <a name="Inheritance"></a> Metas de compartilhamento com a generalização  
 Usar uma relação de generalização para mostrar que um *especializado* caso de uso é uma maneira específica para atingir as metas expressadas por outra *geral* caso de uso. Abra ponta da seta deve apontar em caso de uso mais geral.  
  
 ![Mostrando a relação de generalização de casos de uso](../modeling/media/uml-ucguidegeneral.png "UML_UCGuideGeneral")  
  
 Por exemplo, **pagar** generaliza **pagar com cartão de crédito** e **pagar por dinheiro**.  
  
> [!CAUTION]
>  Você não deve fazer loops de relações de generalização, que resultam em um ator generalizar em si. Loops podem gerar erros.  
  
 Casos de uso especializado podem ajudar você a mostram diferentes maneiras de que seu sistema pode atingir o mesmo objetivo.  
  
 Os casos de uso especializado são considerados para herdar as metas e os atores de geral de caso de uso. O caso de uso geral não precisa ter cenários da própria; suas especializações descrevem as diferentes maneiras de atingir as metas.  
  
##### <a name="to-refactor-common-goals-from-two-or-more-use-cases"></a>Para refatorar comuns metas de dois ou mais casos de uso  
  
1.  Crie e nome do novo geral de caso de uso.  
  
2.  Criar uma **generalização** relação com a grande seta apontando para o novo caso de uso geral.  
  
    1.  Clique em **generalização** na caixa de ferramentas.  
  
    2.  Clique em um caso de uso especializado (**pagar com cartão de crédito** no exemplo).  
  
    3.  Clique no caso de uso geral (**pagar** no exemplo).  
  
3.  Se você descreveu as metas para os casos de uso especializado, mova que as partes comuns na descrição dos geral de caso de uso.  
  
4.  Atores que são compartilhados entre os casos de uso especializado podem ser movidos para o caso de uso geral.  
  
###  <a name="Extend"></a> Separando os casos de variante com Extend  
 Use um link de estender para mostrar que um caso de uso pode adicionar funcionalidade ao outro caso de uso em determinadas circunstâncias. A seta deve apontar o caso de uso principal, estendida.  
  
 ![Um caso de uso estendendo outro](../modeling/media/uml-ucguideextend.png "UML_UCGuideExtend")  
  
> [!CAUTION]
>  Você não deve fazer loops de estender relações, que resultam em um ator generalizar em si. Loops podem gerar erros.  
  
 Por exemplo, o **Login** caso de uso de um site típico pode incluir **registrar de novo usuário** - mas somente quando o usuário ainda não tiver uma conta.  
  
##### <a name="to-separate-a-use-case-into-main-and-extending-parts"></a>Para separar um caso de uso em partes principais e extensão  
  
1. Criar e a nova extensão de nome de caso de uso.  
  
2. Criar uma **estender** relação com a seta apontando para o caso de uso estendido.  
  
   1.  Clique em **estender** na caixa de ferramentas.  
  
   2.  Clique em caso de uso estendendo (**registrar um novo usuário** no exemplo).  
  
   3.  Clique no caso de uso estendido (**Login** no exemplo).  
  
       > [!NOTE]
       >  Evite a criação de um loop de estender relações no diagrama. Ele está incorreto para um caso de uso ser uma extensão de si mesmo.  
  
3. Se você já tiver criado os cenários para o caso de uso estendido, mova as etapas relevantes para o cenário da extensão.  
  
4. A descrição da extensão (**registrar um novo usuário** no exemplo) deve incluir detalhes de onde nos cenários de caso de uso principal que ele ocorrerá e sob quais circunstâncias. Pense nele como modificar a descrição do caso principal.  
  
   O caso de uso de extensão representa as etapas do cenário que seriam parte dos cenários de caso de uso principal. O cenário e a meta da extensão serão sempre lida no contexto do caso de uso principal, portanto que eles não precisarão ser útil independentemente.  
  
   Separando as extensões pode ser úteis para descrever essas situações:  
  
-   Há atores adicionais que estejam envolvidos apenas no caso de uso de extensão. Por exemplo, um administrador deve aprovar o registro do cliente no site da Web.  
  
-   Um subsistema separado lidará com o caso de uso da extensão.  
  
-   Essa extensão estarão disponível apenas em versões específicas do sistema. Você pode mostrar cada versão como um subsistema separado no diagrama de caso.  
  
##  <a name="Subsystems"></a> Usando limites de subsistema  
 Use um limite de subsistema para mostrar quais casos de uso estão dentro do escopo do seu sistema.  
  
#### <a name="to-draw-a-subsystem-boundary"></a>Para desenhar um limite de subsistema  
  
1. Na caixa de ferramentas, clique em **subsistema**, em seguida, clique no diagrama.  
  
    Um subsistema é exibido no diagrama.  
  
2. Arraste os cantos do subsistema para ajustar seu tamanho.  
  
3. Arraste casos de uso existentes para dentro ou fora do subsistema para ajustar seu conteúdo.  
  
   \- ou -  
  
   Para criar um novo caso de uso diretamente em um subsistema, clique em **caso de uso** na caixa de ferramentas, em seguida, clique dentro do subsistema.  
  
> [!NOTE]
>  O **assuntos** propriedade de um caso de uso indica quais subsistema que ele está contido.  
  
### <a name="use-cases-outside-the-system-scope"></a>Casos de uso fora do escopo do sistema  
 Geralmente é útil incluir os casos de uso do diagrama que fazem parte dos negócios, mas não foram tratadas pelo sistema que você está desenvolvendo. Isso ajuda os desenvolvedores a compreender o contexto de seu trabalho. Por exemplo, entregar refeição pôde ser exibida como um caso de uso que envolvem os atores restaurante e clientes, mas fora de responsabilidade do refeição ordenação de Site da Web.  
  
### <a name="multiple-subsystems"></a>Vários subsistemas  
 Você pode criar vários limites de subsistema para mostrar como diferentes use casos são tratados por diferentes componentes do sistema. Por exemplo, **adicionar avaliação de restaurante** podem ser tratados em um site separado do Fórum. Lembre-se de que um diagrama de caso de uso deve lidar com o que é visível para o usuário. Se você deseja descrever a divisão interna de trabalho no sistema, considere usar um diagrama de componente.  
  
### <a name="system-versions"></a>Versões do sistema  
 Você pode usar os limites de subsistema diferente para ilustrar as diferentes versões do sistema. Por exemplo, o caso de uso do pagamento pode ser incluído em um site versão 2, mas não em 1. a versão isso implica que o sistema de ajuda os clientes a fazer seus pedidos. No entanto, eles precisam pagar restaurante diretamente.  
  
 Use **dependência** relações para vincular os subsistemas que representam diferentes versões ou variantes.  
  
 ![Subsistemas mostram diferentes versões de um sistema](../modeling/media/uml-ucguidesystem.png "UML_UCGuideSystem")  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos de usuário do modelo](../modeling/model-user-requirements.md)   
 [Diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md)   
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)   
 [Vídeo: Organizar recursos em casos de uso](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-2-Organizing-Features-Into-Use-Cases/)



