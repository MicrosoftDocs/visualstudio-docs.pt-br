---
title: 'Diagramas de componente UML: Diretrizes | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML diagrams, component
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML, component diagrams
- component diagrams
ms.assetid: 6c1bdd60-369e-477e-83ed-7f6fe75c9f0b
caps.latest.revision: 37
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7400bac1fa6dcbf086718e54d18288b8ab80f1b0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51801454"
---
# <a name="uml-component-diagrams-guidelines"></a>Diagramas de componente UML: diretrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode desenhar um *diagrama de componente* para mostrar a estrutura de um sistema de software. Para uma demonstração em vídeo, consulte [criando a estrutura física usando diagramas de componente](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-6-Designing-a-Projects-Physical-Structure/).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Para criar um diagrama de componente UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
 Um componente é uma unidade modular substituível dentro de seu ambiente. Seus internos permanecem ocultos, mas ele tem uma ou mais bem definidos *interfaces fornecidas* por meio do qual suas funções podem ser acessadas. Um componente também pode ter *as interfaces necessárias*. Uma interface obrigatória define quais funções ou serviços ela exige de outros componentes. Conectando-se as interfaces fornecidas e obrigatórias de vários componentes, um componente maior pode ser construído. Um sistema de software completo pode ser considerado um componente.  
  
 O desenho de diagramas de componente tem vários benefícios:  
  
- O pensamento do design em relação aos blocos principais ajuda a equipe de desenvolvimento a compreender um design existente e a criar um novo.  
  
- Pensando no sistema como uma coleção de componentes com interfaces fornecidas bem definidas e obrigatórias, você melhora a separação entre os componentes. Isso, por sua vez, facilita a compreensão e a alteração do design quando os requisitos são alterados.  
  
  É possível usar um diagrama de componente para representar o design, independentemente da linguagem ou da plataforma que o design usa ou usará.  
  
##  <a name="OtherDiagrams"></a> Relação com outros diagramas  
 É possível usar um diagrama de componente com outros diagramas.  
  
|Outro diagrama|Ajuda a debater e transmitir esses aspectos do design|  
|-------------------|--------------------------------------------------------------------|  
|Diagrama de Sequência UML|-As interações entre componentes de um sistema<br />-As interações entre as partes dentro de um componente.<br /><br /> Para obter mais informações, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).|  
|Diagrama de Classes UML|-As interfaces de um componente. O diagrama de classe permite detalhar os métodos da interface.<br />-Os dados enviados em parâmetros nas interfaces dos componentes.<br /><br /> Para obter mais informações, consulte [diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md).|  
|Diagramas de Atividade|-O processamento interno realizado por um componente em resposta às mensagens de entrada.<br /><br /> Para obter mais informações, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).|  
|Diagramas de Camada|-Camadas arquitetônicas lógicas para os componentes.<br /><br /> Para obter mais informações, consulte [diagramas de camada: referência](../modeling/layer-diagrams-reference.md).|  
  
##  <a name="Basics"></a> Etapas básicas para desenhar diagramas de componente  
 Para informações de referência sobre os elementos em diagramas de componente, consulte [diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md).  
  
 Para obter mais informações sobre como usar diagramas de componente no processo de design, consulte [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).  
  
> [!NOTE]
>  Etapas detalhadas para a criação de qualquer um dos diagramas de modelagem são descritas em [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
#### <a name="to-create-a-component-diagram"></a>Para criar um diagrama de componente  
  
1.  Sobre o **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
2.  Sob **modelos**, clique em **diagrama de componente UML**.  
  
3.  Nomeie o diagrama.  
  
4.  Na **adicionar ao projeto de modelagem**, selecione um projeto de modelagem existente na sua solução, ou **criar um novo projeto de modelagem**e, em seguida, clique em **Okey**...  
  
     Um novo diagrama de componente é exibida com a UML **diagrama de componente** caixa de ferramentas. A caixa de ferramentas contém os elementos e as relações obrigatórios.  
  
### <a name="drawing-components"></a>Desenhando Componentes  
 ![Componentes com interfaces](../modeling/media/uml-compdrawing.png "UML_CompDrawing")  
  
 Criar uma *componente* (1) para cada unidade funcional principal no sistema ou aplicativo.  
  
 Entre os exemplos estão um aplicativo, um dispositivo de hardware, um serviço Web, um assembly .NET., uma classe de programa ou um grupo de classes, ou qualquer segmento separável de um programa.  
  
##### <a name="to-create-components"></a>Para criar componentes  
  
1.  Clique em **componente** na caixa de ferramentas e, em seguida, clique em uma parte em branco do diagrama.  
  
     \- ou -  
  
     Copie e cole um componente existente.  
  
    1.  Localizar um componente existente em um diagrama ou no **Gerenciador de modelos UML**.  
  
    2.  O componente com o botão direito e, em seguida, clique em **cópia**.  
  
    3.  Abra o diagrama onde você deseja que o componente copiado seja exibido.  
  
    4.  Uma parte em branco do diagrama com o botão direito e, em seguida, clique em **colar**.  
  
         Uma cópia do componente é exibida com um novo nome.  
  
2.  Clique no nome do componente para alterá-lo.  
  
3.  Clique na divisa (5) caso você queira ver apenas o cabeçalho do componente.  
  
### <a name="showing-the-ports-of-a-component"></a>Mostrando as Portas de um Componente  
 Um *porta* (2, 3) representa um grupo de mensagens ou chamadas de operação passam dentro ou fora de um componente. O grupo é descrito por uma interface, que define o tipo da porta. Uma porta pode fornecer uma interface ou exigir uma interface.  
  
 Uma porta com um *interface fornecida* (2) indica operações implementadas pelo componente e que pode ser usado por outros componentes.  
  
 Entre os exemplos estão uma interface do usuário, um serviço Web, uma interface do .NET ou uma coleção de funções em qualquer linguagem de programação.  
  
 Uma porta com um *interface necessária* (3) representa o requisito de um componente para um grupo de operações ou serviços ser fornecido por outros componentes ou sistemas externos.  
  
 Por exemplo, um navegador da Web exige servidores Web, ou um suplemento de aplicativo exige serviços do aplicativo.  
  
 Um componente pode ter um número de portas qualquer.  
  
##### <a name="to-add-ports-to-a-component"></a>Para adicionar portas a um componente  
  
1. Na caixa de ferramentas, clique em **Interface fornecida** ou **Interface obrigatória**.  
  
2. Clique no componente ao qual você deseja adicioná-la.  
  
    Uma porta é exibida no limite do componente.  
  
    Uma interface nova é criada como o tipo da porta. Essa interface é exibida no **Gerenciador de modelos UML**.  
  
3. Arraste a porta em torno do limite do componente para colocá-la onde você deseja.  
  
4. Arraste o rótulo da porta para ajustar sua posição.  
  
5. Clique no rótulo para alterá-lo. O rótulo mostra o nome da interface. Se alterá-lo, você mudará o nome da interface.  
  
   Se quiser listar os atributos e as operações da interface, você poderá fazer isso adicionando-os à interface no Gerenciador de Modelos UML. Como alternativa, é possível arrastar a interface do Gerenciador de Modelos UML para um diagrama de classe e adicionar as operações e os atributos para lá.  
  
### <a name="linking-between-components"></a>Vinculando entre componentes  
 Use uma dependência (4) para mostrar que o requisito de um componente pode ser atendido pelas operações ou pelos serviços fornecidos por outro componente.  
  
##### <a name="to-show-that-a-provided-interface-can-satisfy-a-required-interface"></a>Para mostrar que uma interface fornecida pode atender a uma interface obrigatória  
  
1. Na caixa de ferramentas, clique em **dependência**.  
  
2. Clique na porta com a interface obrigatória em um componente e, em seguida, clique na porta com a interface fornecida em outro componente.  
  
   Você deve tentar evitar a criação de loops de dependência nos quais cada componente em um grupo depende de todos os outros componentes.  
  
##### <a name="to-add-a-port-for-an-existing-interface-to-a-component"></a>Para adicionar uma porta para uma interface existente a um componente  
  
-   Encontre a interface no **Gerenciador de modelos UML** e, em seguida, arraste-o a partir daí para o componente.  
  
     -ou-  
  
-   Copie e cole uma referência para uma interface de um diagrama.  
  
    1.  Em um diagrama de classe ou um diagrama de componente, a interface com o botão direito e, em seguida, clique em **cópia**.  
  
    2.  No diagrama de componente, o componente com o botão direito e, em seguida, clique em **Colar referência**.  
  
         Uma interface fornecida é exibida no componente. Uma marca Action é exibida próxima.  
  
        > [!NOTE]
        >  Se você usar **colar** em vez de **Colar referência**, uma nova interface que tem um novo nome será criada.  
  
    3.  Se você quisesse criar uma interface obrigatória, clique na marca de ação e, em seguida, clique em **converter a Interface necessária**.  
  
##  <a name="Parts"></a> Mostrando as partes internas de um componente  
 ![Diagrama de componente mostrando partes internas](../modeling/media/uml-compshowing.png "UML_CompShowing")  
  
 É possível colocar partes (3) em um componente (1) para mostrar como ele é feito de componentes menores que interagem entre si.  
  
 O diagrama na ilustração indica que cada instância do tipo Dinner Now Web Service contém uma instância de Customer Server e uma instância de Kitchen Server.  
  
 Uma parte é uma propriedade do componente pai, da mesma forma como um atributo pertence a uma classe comum. Uma parte tem seu próprio tipo, que normalmente também é um componente. O rótulo da parte tem a mesma forma de um atributo comum:  
  
 `+ partName : TypeName`  
  
 Dentro do componente pai, cada parte mostra as interfaces fornecida e obrigatória definidas para seu tipo (4, 5). As operações ou os serviços exigidos por uma parte podem ser fornecidos por outros. Você pode usar **Assembly Part** conectores para mostrar como as partes são conectadas entre si (6).  
  
 Também é possível mostrar que uma interface do componente pai é efetivamente fornecida ou obrigatória por uma de suas partes. Você pode se conectar a uma porta do pai para uma porta de uma parte interna usando uma **delegação** relação (9). As duas portas devem ser do mesmo tipo (fornecida ou obrigatória), e seus tipos de interface devem ser compatíveis.  
  
 É possível criar uma nova parte com um novo tipo, ou com base em um tipo existente.  
  
#### <a name="to-add-parts-to-a-component"></a>Para adicionar partes a um componente  
  
1.  Crie uma parte para cada unidade funcional principal que você considera ser uma parte do componente pai.  
  
    1.  Clique em **componente** na caixa de ferramentas e, em seguida, clique no componente pai (1).  
  
         Uma nova parte (3) é exibida no componente pai.  
  
         Um novo componente é criado no **Gerenciador de modelos UML**. Este é o novo tipo da parte.  
  
         \- ou -  
  
         Arraste um componente existente do Gerenciador de Modelos UML para o componente pai.  
  
         Uma nova parte (3) é exibida no componente pai. O tipo é o componente arrastado do Gerenciador de Modelos UML.  
  
         \- ou -  
  
         Um componente em um diagrama ou no Gerenciador de modelos UML, com o botão direito e, em seguida, clique em **cópia**.  
  
         Clique com botão direito no componente pai e, em seguida, clique em **Colar referência**.  
  
         Uma nova parte (3) é exibida no componente pai. O tipo é o componente que você copiou.  
  
    2.  Clique no nome da nova parte para alterá-lo. Não é possível alterar seu tipo.  
  
    3.  É possível adicionar interfaces fornecidas e obrigatórias (4, 5) à nova parte. Clique o **Interface fornecida** ou **Interface obrigatória** ferramenta e, em seguida, clique na parte.  
  
         \- ou -  
  
         Arraste uma interface existente do **Gerenciador de modelos UML** até a parte.  
  
         As interfaces são adicionadas ao tipo da parte e são exibidas na própria parte. O componente pai ajustará seu tamanho, se necessário.  
  
2.  Conecte as partes.  
  
    -   Use o **dependência** ferramenta para conectar as portas de partes diferentes (6).  
  
3.  Conecte as partes às portas do componente pai:  
  
    1.  Crie uma ou várias portas (7) no componente pai. Clique em **Interface obrigatória** ou **Interface fornecida** na caixa de ferramentas e, em seguida, clique no componente pai.  
  
    2.  Delegue (9) a porta a uma ou várias partes. Clique o **delegação** ferramenta, uma porta no componente pai e, em seguida, uma porta em uma parte. É possível conectar portas que forneçam ou exijam interfaces da mesma maneira.  
  
### <a name="showing-the-parts-of-a-part"></a>Mostrando as Partes de uma Parte  
 Depois de decompor um componente em partes, você poderá decompor cada um dos tipos de parte em partes internas próprias.  
  
 É mais fácil fazer cada camada de decomposição em um diagrama de componente separado. Você deve primeiro localizar o tipo da parte. Por exemplo, na ilustração, uma das partes é chamada `DNCustomerServer`, e seu tipo é um componente chamado `CustomerServer`. É possível encontrar esse tipo no Gerenciador de Modelos UML e colocá-lo em outro diagrama. Em seguida, é possível criar suas próprias partes internas.  
  
##### <a name="to-place-a-parts-type-on-a-diagram"></a>Para colocar o tipo de uma parte em um diagrama  
  
1.  Determine o nome totalmente qualificado do tipo da parte.  
  
     A parte com o botão direito e, em seguida, clique em **propriedades**.  
  
     O nome do tipo aparece na **tipo** campo da janela Propriedades.  
  
2.  Localize o tipo da parte na **Gerenciador de modelos UML**.  
  
     Clique em **modo de exibição**, aponte para **Other Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
     Expanda o projeto e, se necessário, qualquer pacote a que o tipo pertença.  
  
     O tipo será listado como um **componente**.  
  
     Será possível alterar o nome aqui se você quiser.  
  
3.  Abra ou crie outro diagrama de componente.  
  
4.  Arraste do tipo no Gerenciador de Modelos UML para o diagrama.  
  
     Uma exibição do tipo é exibida como um componente no diagrama.  
  
     Ela tem as mesmas interfaces definidas para a parte.  
  
     Agora é possível adicionar partes a ela.  
  
##  <a name="Designing"></a> Criando o componente  
  
### <a name="describing-how-the-parts-collaborate"></a>Descrevendo Como as Partes Colaboram  
 É possível desenham um diagrama de sequência para mostrar como as partes trabalham juntas em resposta a uma mensagem que chega ao componente pai.  
  
 É possível usar esses diagramas tanto para explicar um componente existente quanto para criar um novo componente.  
  
 Se ainda estiver criando o componente, você poderá desenhar diagramas de sequência antes de decidir quais partes ele terá. É possível usar os diagramas de sequência para testar partes diferentes, interfaces obrigatórias e sequências de mensagem. Desenhe diagramas de sequência para as mensagens recebidas mais frequentes e mais importantes. Em seguida, é possível criar partes no componente que correspondem às linhas da vida decididas.  
  
 Use os diagramas de sequência para avaliar como o trabalho do sistema é distribuído entre os diferentes componentes.  
  
- Se for muito empilhado em uma parte, provavelmente será mais difícil atualizar o aplicativo do que se o trabalho estiver distribuído por igual.  
  
- Se o trabalho estiver muito distribuído com muitas interações, o desempenho do sistema poderá ser ruim e ser difícil de compreender.  
  
  ![Partes de colaboração de exibição de diagrama de sequência](../modeling/media/uml-compdescparts.png "UML_CompDescParts")  
  
##### <a name="to-draw-a-sequence-diagram-that-shows-collaboration-between-parts"></a>Para desenhar um diagrama de sequência que mostre a colaboração entre as partes  
  
1.  Criar um novo diagrama de sequência.  
  
     Para obter mais informações, consulte [diagramas de sequência UML: diretrizes](../modeling/uml-sequence-diagrams-guidelines.md).  
  
2.  Crie uma linha da vida para um componente externo, usuário, dispositivo ou outro ator (1) que envia mensagens para esse componente.  
  
     Você pode definir as **ator** propriedade dessa linha da vida como true para indicar que ela é externa ao componente em consideração. Uma figura de pilha é exibida acima da linha da vida.  
  
3.  Crie uma linha da vida para a interface fornecida (2) desse componente para o qual o ator escolhido envia mensagens.  
  
4.  Crie uma linha da vida para cada parte (3) do componente.  
  
5.  Crie uma linha da vida para cada interface obrigatória (4) do componente.  
  
6.  Desenhe mensagens com base no ator externo (5). Mostre como a mensagem é passada para as partes e como elas colaboram para responder à mensagem.  
  
7.  Quando necessário, mostre mensagens enviadas para uma interface obrigatória (6). Não mostre detalhes dentro da execução da mensagem.  
  
### <a name="is-the-component-more-than-its-parts"></a>O Componente é Maior do que suas Partes?  
 Em alguns casos, um componente não é nada mais do que um nome dado a uma coleção de partes. Todo o trabalho é feito pela partes e, no tempo de execução, não há código ou outro artefato que represente o componente.  
  
 É possível indicar isso no modelo definindo o **Is Indirectly Instantiated** propriedade do componente. Nesse caso, todas as interfaces do componente devem estar nas portas, com delegações para partes internas.  
  
### <a name="describing-the-process-inside-each-part"></a>Descrevendo o Processo Dentro de Cada Parte  
 É possível usar diagramas de atividade para mostrar como um componente processa cada mensagem recebida. Para obter mais informações, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
 ![Diagrama de atividade com o buffer de dados](../modeling/media/uml-compdescribingproc.png "UML_CompDescribingProc")  
  
 Use uma Ação de Evento de Aceitação (1) para mostrar que uma mensagem recebida inicia um novo thread.  
  
 Use nós de objeto e pinos de entrada/saída para mostrar o fluxo de informações, além de mostrar onde as informações são armazenadas. No exemplo, um nó de objeto (2) é usado para mostrar itens que estão sendo armazenados em buffer entre um thread e outro.  
  
### <a name="defining-data-and-classes"></a>Definindo Dados e Classes  
 É possível usar um diagrama de classes UML para descrever o conteúdo detalhado de:  
  
-   As interfaces dos componentes. Quando você adiciona uma porta obrigatória ou fornecida a um componente, uma interface é exibida no Gerenciador de Modelos UML. É possível arrastar ou copiá-la para um Diagrama de Classes UML para mostrar seus atributos e operações, além de relações com outras interfaces.  
  
-   Dados passados em parâmetros de operações nas interfaces.  
  
-   Os dados armazenados nos componentes, por exemplo, conforme mostrado no objeto fluem em diagramas de atividade.  
  
### <a name="general-dependencies-between-components"></a>Dependências Gerais Entre Componentes  
 É possível usar um diagrama de componente para apenas mostrar as partes principais do design e suas interdependências.  
  
 ![Uma dependência entre os componentes](../modeling/media/uml-compdepend.png "UML_CompDepend")  
  
 Use o **dependência** ferramenta para desenhar uma dependência. Isso indica que o design de um componente confia em outro.  
  
 Entre os tipos comuns de dependência estão os seguintes:  
  
- Um componente chama o código dentro do outro.  
  
- Um componente cria uma instância de uma classe definida dentro de outra classe.  
  
- Um componente usa informações criadas por outro componente.  
  
  É possível usar o nome da seta de dependência para denotar um tipo específico de uso. Para definir o nome, clique com botão direito na seta e clique em **propriedades**e defina as **nome** campo na janela Propriedades.  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Vídeo: Criando a estrutura física usando diagramas de componente](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-6-Designing-a-Projects-Physical-Structure/)



