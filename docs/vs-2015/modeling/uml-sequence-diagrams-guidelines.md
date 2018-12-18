---
title: 'Diagramas de sequência UML: Diretrizes | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.sequencediagram.linktosequencediagram
- vs.teamarch.logicalclassdiagram.createlifeline
- vs.teamarch.componentdiagram.createlifeline
helpviewer_keywords:
- diagrams - modeling, sequence
- sequence diagrams
- UML diagrams, sequence
- interactions, UML
- diagrams - modeling, UML sequence
- UML interactions
- UML, sequence diagrams
- UML sequence diagrams
- behaviors, UML
ms.assetid: 5990ef7c-ba60-4e20-a36d-e29c1fa6c8bb
caps.latest.revision: 55
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 56ecc5c54611f94cdbfb0f08ec54a4e0722f0cbd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51803624"
---
# <a name="uml-sequence-diagrams-guidelines"></a>Diagramas de sequência UML: diretrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode desenhar um *diagrama de sequência* para mostrar uma interação. Uma interação é uma sequência de mensagens entre as instâncias de classes, componentes, subsistemas ou atores típicas.  
  
 Diagramas de sequência UML fazem parte de um modelo UML e existem somente dentro de projetos de modelagem UML. Para criar um diagrama de sequência UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**. Saiba mais sobre [elementos de diagrama de sequência UML](../modeling/uml-sequence-diagrams-reference.md) ou [diagramas de modelagem UML](../modeling/edit-uml-models-and-diagrams.md) em geral. Para uma demonstração em vídeo, consulte [fazer um rascunho de interações com o uso de diagramas de sequência (2010)](http://channel9.msdn.com/Blogs/clinted/UML-with-VS-2010-Part-7-Sketching-Interactions-with-Sequence-Diagrams).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="in-this-topic"></a>Neste tópico  
 [Usando diagramas de sequência UML](#Using)  
  
 [Etapas básicas para desenhar diagramas de sequência](#BasicSteps)  
  
 [Criando e usando diagramas de sequência simples](#Simple)  
  
 [Classes e as linhas de vida](#ClassesAndLifelines)  
  
 [Criar sequências de interação reutilizáveis](#Multiple)  
  
 [Recolhendo grupos de linhas da vida](#Collapse)  
  
 [Descrever estruturas de controle com fragmentos](#Fragments)  
  
##  <a name="Using"></a> Usando diagramas de sequência UML  
 Você pode usar diagramas de sequência para uma variedade de finalidades em diferentes níveis de detalhes do programa. Ocasiões típicos para desenhar um diagrama de sequência são da seguinte maneira:  
  
- Se você tiver um diagrama de caso de uso que resume os usuários do seu sistema e suas metas, você pode desenhar diagramas de sequência para descrever como os principais componentes do sistema interagem para cumprir o objetivo de cada caso de uso. Para obter mais informações, consulte [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md).  
  
- Se você tiver identificado as mensagens que chegam em uma interface de um componente, você pode desenhar diagramas de sequência para descrever como as partes internas do componente interagem para alcançar o resultado necessário para cada mensagem recebida. Para obter mais informações, consulte [diagramas de componente UML: diretrizes](../modeling/uml-component-diagrams-guidelines.md).  
  
  Desenhar diagramas de sequência tem vários benefícios:  
  
- Você pode ver facilmente como as tarefas são distribuídas entre os componentes.  
  
- Você pode identificar padrões de interação que dificultam a atualizar o software.  
  
## <a name="relationship-to-other-diagrams"></a>Relação com outros diagramas  
 Você pode usar diagramas de sequência UML junto com outros diagramas de várias maneiras.  
  
#### <a name="lifelines-and-types"></a>Linhas da vida e tipos  
 As linhas da vida que você desenhar em um diagrama de sequência podem representar típicas instâncias dos componentes ou classes de em seu sistema. Você pode criar linhas de vida de tipos e tipos de linhas da vida e mostram os tipos em diagramas de classe UML e diagramas de componente UML. Para obter mais informações, consulte [Classes e as linhas de vida](#ClassesAndLifelines).  
  
#### <a name="parameter-types"></a>Tipos de parâmetro  
 Você também pode descrever em um diagrama de classe UML os tipos de parâmetros e retornar valores que foram usados nas mensagens enviadas entre as linhas da vida.  
  
#### <a name="use-case-details"></a>Detalhes do caso de uso  
 Um caso de uso representa o objetivo de um usuário, junto com uma sequência de etapas para atingir a meta. A sequência de etapas pode ser descrita de várias maneiras. Uma opção é desenhar um diagrama de sequência que mostra as interações entre usuários e os componentes principais do sistema. Para obter mais informações, consulte [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md).  
  
##  <a name="BasicSteps"></a> Etapas básicas para desenhar diagramas de sequência  
 Para obter uma lista completa de elementos em diagramas de sequência, consulte [diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md).  
  
> [!NOTE]
>  Etapas detalhadas para criar qualquer um dos diagramas de modelagem são descritas em [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
#### <a name="to-create-a-sequence-diagram"></a>Para criar um diagrama de sequência  
  
1. Sobre o **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
2. Sob **modelos**, clique em **diagrama de sequência UML**.  
  
3. Nomeie o diagrama.  
  
4. Na **adicionar ao projeto de modelagem**, selecione um projeto de modelagem existente na sua solução, ou **criar um novo projeto de modelagem**e, em seguida, clique em **Okey**.  
  
    Um novo diagrama de sequência é exibido com o **diagrama de sequência** caixa de ferramentas. A caixa de ferramentas contém os elementos necessários e conectores.  
  
   ![Partes de um diagrama de sequência](../modeling/media/uml-sequence.png "UML_Sequence")  
  
#### <a name="to-draw-a-sequence-diagram"></a>Para desenhar um diagrama de sequência  
  
1.  Arraste **linhas de vida** (1) da **caixa de ferramentas** para o diagrama para representar as instâncias de classes, componentes, os atores ou dispositivos.  
  
    > [!NOTE]
    >  Você também pode criar uma linha da vida, arrastando uma classe existente, a interface, o ator ou o componente a partir **Gerenciador de modelos UML** para o diagrama. Isso cria uma linha da vida que representa uma instância do tipo escolhido.  
  
2.  Desenhe mensagens para mostrar como as linhas da vida colaboram para atingir um objetivo específico.  
  
     Para criar uma mensagem (3, 4, 6, 7), clique em uma ferramenta de mensagem. Em seguida, clique na linha de vida de envio no ponto onde você deseja que a mensagem para iniciar e, em seguida, clique na linha de vida de recebimento.  
  
     Uma ocorrência de execução (5) é exibido na linha de vida de recebimento. A ocorrência de execução representa um período de tempo durante o qual a instância está executando um método. Você pode criar outras mensagens que iniciam com uma ocorrência de execução.  
  
3.  Para mostrar uma mensagem que vem de uma fonte de evento desconhecido (9), ou transmite para destinatários desconhecidos (10), desenhe uma mensagem assíncrona de ou para o espaço em branco no diagrama. Essas mensagens são chamadas *encontrou mensagens* (9) e *perdeu mensagens* (10).  
  
    > [!NOTE]
    >  Para mover um grupo de linhas da vida que perdeu ou encontrou mensagens, siga estas etapas para selecionar as linhas da vida antes de movê-los: desenhar um retângulo em torno dessas linhas de vida, ou pressione e mantenha o **CTRL** enquanto você clica em cada linha da vida da chave. Se você usar **Selecionar tudo** ou **CTRL**+**um** para selecionar todas as linhas da vida e, em seguida, movê-los, qualquer perdida ou localizada anexadas a essas linhas da vida de mensagens não será movido. Se esse cenário ocorrer, será possível mover essas mensagens separadamente.  
  
4.  Desenhe diagramas de sequência para cada mensagem principal no mesmo componente ou sistema.  
  
#### <a name="to-change-the-order-of-messages"></a>Para alterar a ordem das mensagens  
  
-   Arraste uma mensagem para cima ou para baixo em sua linha de vida. Você pode arrastá-lo ao longo de outras mensagens, ou para dentro ou fora um bloco de execução.  
  
     \- ou -  
  
-   Clique na mensagem e usar o **seta para cima** e **seta para baixo** chaves para ajustar as posições de mensagem. Use **SHIFT + seta para cima** e **SHIFT + seta para baixo** para alterar a ordem das mensagens.  
  
#### <a name="to-move-or-copy-message-sequences-on-the-sequence-diagram"></a>Para mover ou copiar as sequências de mensagem no diagrama de sequência  
  
1.  Uma mensagem (3, 4) com o botão direito e, em seguida, clique em **cópia**.  
  
2.  Clique com botão direito a ocorrência de execução (5) ou uma linha de vida (1) do qual você deseja que a nova mensagem a ser enviado e, em seguida, clique em **colar**. Novo remetente pode ser em um diagrama de diferente se desejar.  
  
     Uma cópia da mensagem e todas as suas mensagens subsidiárias é adicionada ao final da ocorrência de execução, ou até o final da linha de vida.  
  
    > [!NOTE]
    >  A mensagem colada sempre aparece no final da linha da vida ou ocorrência de execução. Depois que você colou-lo, você poderá arrastá-lo até uma posição anterior.  
  
#### <a name="to-display-and-edit-the-signature-text-for-a-message"></a>Para exibir e editar o texto da assinatura para uma mensagem  
  
- Na linha de vida de destino deve ser associada ou mapeada para tipos para o texto da assinatura para ser visível. Para realizar essa tarefa, execute uma das seguintes etapas:  
  
  - Clique com botão direito na linha de vida e, em seguida, escolha **criar classe**.  
  
     -ou-  
  
  - Selecione a linha da vida, pressione **F4**e, em seguida, no **propriedades** janela, defina a **tipo** propriedade a um existente, digite ou especifique o nome para um novo tipo. O rótulo da mensagem com o botão direito e, em seguida, escolha **operação criar**.  
  
    O texto da assinatura é exibida abaixo do rótulo de mensagem. Agora você pode editar o texto da assinatura. Para obter mais informações, consulte [Classes e as linhas de vida](#ClassesAndLifelines).  
  
#### <a name="to-improve-the-layout-of-a-sequence-diagram"></a>Para melhorar o layout de um diagrama de sequência  
  
-   Uma parte em branco do diagrama com o botão direito e, em seguida, clique em **reorganizar Layout**.  
  
-   Para desfazer a operação, clique em **edite**e, em seguida, clique em **desfazer**.  
  
#### <a name="to-change-the-package-that-owns-the-interaction"></a>Para alterar o pacote que possui a interação  
  
1.  Na **Gerenciador de modelos UML**, encontre a interação que exibe o diagrama de sequência.  
  
    > [!NOTE]
    >  A interação não aparecerão nos **Gerenciador de modelos UML** até que você adicione a primeira linha da vida para o diagrama de sequência.  
  
2.  Arraste a interação no pacote.  
  
     \- ou -  
  
     A interação com o botão direito e, em seguida, clique em **Recortar**. O pacote com o botão direito e, em seguida, clique em **colar**.  
  
##  <a name="Simple"></a> Criando e usando diagramas de sequência simples  
 A forma mais simples e mais amplamente usado de diagrama de sequência contém apenas linhas da vida e mensagens. Um diagrama desse tipo lhe permite mostrar claramente uma sequência típica de interações entre objetos em seu design, ou entre seu sistema e seus usuários. Isso é com frequência suficiente para ajudá-lo a debater e transmitir seu design.  
  
 Aqui estão algumas coisas a considerar quando você desenhar um diagrama de sequência simples.  
  
### <a name="types-of-message"></a>Tipos de mensagem  
 Há três ferramentas que você pode usar para criar as mensagens.  
  
-   Use o **Synchronous** ferramenta para descrever uma interação na qual o remetente aguarda o receptor retornar uma resposta (3).  
  
     Um  **< \<retornar >>** seta será mostrada no final da ocorrência de execução. Ele indica o retorno do controle para o remetente.  
  
-   Use o **Asynchronous** ferramenta para descrever uma interação na qual o remetente pode continuar imediatamente sem esperar que o receptor (4).  
  
-   Use o **criar** ferramenta para descrever uma interação na qual o remetente cria o receptor (8).  
  
     Uma ação Criar mensagem deve ser a primeira mensagem que o receptor recebe.  
  
### <a name="annotating-the-interactions"></a>Anotando as interações  
 Para descrever mais detalhes sobre a sequência, você pode colocar uma **comentário** em qualquer lugar no diagrama.  
  
 Usando o **Links de comentário**, você pode vincular um comentário para as linhas de vida, execuções, usos de interação e fragmentos.  
  
> [!CAUTION]
>  Quando você deseja anexar um comentário para um ponto específico na sequência, vinculá-lo a uma ocorrência de execução, o uso de interação, ou do fragmento. Não vinculá-lo a uma linha da vida, porque nesse caso, ele não permaneça conectado no ponto na sequência correto.  
  
 Use um comentário para:  
  
-   Observe o que foi obtido em pontos-chave na sequência. Isso ajuda os leitores para ver os objetivos das interações.  
  
-   Descreva a finalidade geral de toda a sequência. Anexar o comentário para a ocorrência de execução inicial ou deixá-lo desconectados. Por exemplo, "cliente tiver escolhido a itens de menu e tem um preço."  
  
-   Descreva as responsabilidades de cada linha da vida. Anexe o comentário para a linha da vida. Por exemplo, "Ordering Manager coleta opções de menu do cliente."  
  
-   Observe as exceções ou alternativas que podem ser executadas como uma alternativa para a sequência típica mostrada. Por exemplo "cliente poderá optar por ignorar o restante dessa sequência."  
  
    -   Considere o uso de fragmentos como uma alternativa mais formal para esse tipo de anotação. Consulte [descrevendo as estruturas de controle com fragmentos](#Fragments)  
  
## <a name="deciding-the-scope-of-the-diagram"></a>Decidindo o escopo do diagrama  
 É importante saber claramente que o diagrama destina-se a mostrar.  
  
#### <a name="initiating-event"></a>Iniciando o evento  
 Cada diagrama deve mostrar a sequência de interações que resulta de um evento inicial. Isso pode ser, por exemplo:  
  
-   Um usuário iniciar um caso de uso, por exemplo, abrindo a página da Web para comprar uma refeição.  
  
-   Uma mensagem de componente de um sistema para outro, por exemplo, consultando a disponibilidade de itens que um cliente deseja comprar.  
  
-   Um evento disparado por uma alteração de estado, por exemplo, ações de um item cair abaixo do limite.  
  
#### <a name="level-of-detail"></a>Nível de detalhe  
 Diagramas de sequência podem mostrar diferentes níveis de detalhe. Você pode decidir o nível de detalhes em duas dimensões separadas de forma praticamente independente:  
  
 Linhas de vida podem representar um desses níveis de detalhe:  
  
- Objetos no código do programa, que existe ou você está desenvolvendo.  
  
- Componentes ou seus subcomponentes, geralmente a omissão fachadas proxies e outros mecanismos de connective.  
  
- Seu sistema e atores externos  
  
  As mensagens podem representar um desses níveis de detalhe:  
  
- Mensagens de software no código do programa, em uma API, ou interface da Web.  
  
- As transações ou subpropriedades de transações, por exemplo, entre os usuários e o sistema, ou entre o código e o banco de dados.  
  
- Casos de uso - principais interações entre usuários e o sistema.  
  
  Se você estiver Explorando o código existente ou que descreve um novo design, geralmente é útil desenhar e discutir o menor detalhadas modos de exibição.  
  
## <a name="describing-variations"></a>Descrevendo variações  
 O diagrama mostra uma única sequência de eventos típica. Se você quiser mostrar as possibilidades alternativas, como cenários de falha, você pode usar qualquer uma dessas opções:  
  
-   Desenhar diagramas de sequência separado para descrever esses cenários  
  
-   Use [que descreve estruturas de controle com fragmentos](#Fragments) para mostrar os loops, alternativas e assim por diante.  
  
## <a name="assessing-the-design"></a>Avaliando o Design  
 Você pode usar o diagrama para avaliar a distribuição de tarefas entre seus objetos ou componentes. Considere a refatoração se você vir esses padrões:  
  
-   Uma linha da vida parece fazer tudo, fazendo chamadas para todo o resto, enquanto as outras linhas da vida apenas respondem passivamente.  
  
-   Muitas mensagens cruzam linhas da vida. Cada linha da vida deve enviar mensagens para apenas alguns vizinhos e não deve se comunicar com vizinhos dos seus vizinhos. Geralmente deve ser possível organizar as linhas da vida para que haja apenas alguns lugares onde as mensagens entre as linhas de vida; e onde há cruzamentos, na linha de vida de destino deve não também trocar mensagens com as linhas da vida transversais.  
  
-   Parecem que algumas linhas de vida lidar com mais de um tipo de tarefa. Ele deve fácil encontrar uma sentença sucinta que descreve as responsabilidades de cada linha da vida, resumindo o trabalho em resposta a cada mensagem que ele recebe.  
  
##  <a name="ClassesAndLifelines"></a> Classes e as linhas de vida  
 As linhas da vida em seus diagramas de sequência mostram as instâncias de classes ou interfaces de componentes. Você pode nomear uma linha da vida de duas maneiras:  
  
|**Para essa finalidade**|**Use este formato**|  
|--------------------------|-------------------------|  
|Instância anônima de um tipo.<br /><br /> Use essa opção se você tiver apenas uma linha da vida de cada tipo.|*typeName*|  
|Instância nomeada de um tipo.<br /><br /> Use essa opção se você deseja mostrar uma sequência que envolve mais de uma instância do mesmo tipo.|*objectName*:*typeName*|  
  
### <a name="creating-lifelines-from-types"></a>Criar linhas de vida de tipos  
 Você pode criar novas linhas da vida de classes que você já definiu, por exemplo em um diagrama de classe.  
  
> [!NOTE]
>  Verifique se que você tem um diagrama de sequência existente antes de executar essa tarefa.  
  
##### <a name="to-create-a-lifeline-from-an-existing-type"></a>Para criar uma linha da vida de um tipo existente  
  
- Arraste uma classe, componente ou interface do Gerenciador de modelos UML para um diagrama de sequência.  
  
   \- ou -  
  
  1. Clique com botão direito a classe, componente ou interface em seu respectivo diagrama e, em seguida, clique em **criar linha de vida**.  
  
  2. No **criar linha de vida** caixa de diálogo, selecione um diagrama de sequência e, em seguida, clique em **Okey**.  
  
     Uma nova linha de vida de instância nomeada é exibida, cujo tipo é o tipo que você arrastou.  
  
  > [!NOTE]
  >  Você pode repetir essa ação quantas vezes desejar. Isso criará as linhas de vida com nomes de instância diferente.  
  
##### <a name="to-change-the-type-of-a-lifeline"></a>Para alterar o tipo de uma linha da vida  
  
1.  Uma linha da vida com o botão direito e, em seguida, clique em **propriedades**.  
  
2.  No **propriedades** janela, defina as **tipo** propriedade. Você pode selecionar um tipo no menu suspenso ou digite um novo nome.  
  
### <a name="creating-classes-from-lifelines"></a>Criando Classes de linhas de vida  
 Quando você tiver criado um ou mais diagramas de sequência, você pode resumir as linhas da vida com a criação de interfaces ou classes deles.  
  
##### <a name="to-create-a-class-or-interface-from-a-lifeline"></a>Para criar uma classe ou interface de uma linha da vida  
  
1.  Clique com botão direito na linha de vida e, em seguida, clique em **criar classe** ou **criar Interface**.  
  
     Uma nova classe ou interface é exibida no Gerenciador de modelos UML.  
  
2.  Crie operações na classe ou interface para cada mensagem recebida na linha de vida:  
  
    1.  Selecione todas as mensagens que você deseja incluir.  
  
    2.  Clique em um das mensagens e, em seguida, clique em **criar método**.  
  
         A nova classe ou interface oferece operações para cada mensagem selecionada.  
  
         O nome da operação é exibida abaixo de cada seta de mensagem e, na **operação** propriedade da mensagem.  
  
         Se sua mensagem incluídos parâmetros no formulário "(parameter: type)", eles aparecerão na lista de parâmetros da operação de novo.  
  
        > [!NOTE]
        >  Você deve repetir esta etapa se você adicionar novas mensagens no diagrama de sequência.  
  
3.  Para exibir a nova classe ou interface em detalhes, adicione-a um diagrama de classe ou componente.  
  
    1.  Abra ou crie um diagrama de classe ou componente.  
  
    2.  Arraste a nova classe ou interface de **Gerenciador de modelos UML** para um diagrama de classe.  
  
         A classe ou interface é exibida no diagrama de classe.  
  
         \- ou -  
  
    3.  Arraste a nova interface da **Gerenciador de modelos UML** em um componente ou uma porta em um diagrama de componente.  
  
         A interface aparece no componente como um pirulito.  
  
### <a name="creating-classes-for-parameters"></a>Criação de classes para parâmetros  
 Você pode incluir parâmetros nas mensagens em um diagrama de sequência. Você pode usar um diagrama de classe UML para descrever os tipos de parâmetro.  
  
##  <a name="Multiple"></a> Criar sequências de interação reutilizáveis  
 Você pode usar um diagrama separado para descrever uma sequência que contém detalhes que você deseja separar ou que seja comum entre vários diagramas.  
  
 Você pode criar um retângulo de uso da interação (12) em um diagrama que aponta para os detalhes em outro diagrama.  
  
 Clique duas vezes em um uso de interação para abrir o diagrama de sequência que esteja vinculado a ele.  
  
#### <a name="to-create-a-reusable-interaction-sequence-from-existing-lifelines"></a>Para criar uma sequência de interação reutilizável de linhas de vida existentes  
  
1.  No **caixa de ferramentas**, clique em **uso da interação**.  
  
2.  No diagrama de sequência, mantenha o botão do mouse pressionada enquanto arrasta entre as linhas da vida que você deseja incluir na sequência de reutilizáveis. Inicie a posição vertical em que você deseja inserir o uso de interação.  
  
     Um uso da interação aparece entre as linhas da vida selecionadas no diagrama de sequência.  
  
3.  Duas vezes no nome sobre o uso de interação e renomeá-lo para descrever o efeito da sequência reutilizável neste diagrama.  
  
     \- ou -  
  
     Grave o nome como uma chamada de função com parâmetros.  
  
4.  Vincule o uso de interação para outro diagrama de sequência. Clique com botão direito o uso de interação e, em seguida, qualquer um:  
  
     Clique em **criar nova sequência** para criar um novo diagrama de sequência  
  
     \- ou -  
  
     Clique em **Link para a sequência** para vincular a um diagrama existente.  
  
     Visual Studio cria um vínculo entre o uso de interação e a nova sequência de interação.  
  
     Um novo diagrama de sequência é exibido em sua solução. Ele contém as linhas da vida que você usou para criar o uso de interação.  
  
    > [!NOTE]
    >  Somente as linhas de vida que você usou para criar o uso da interação serão incluídas. O novo diagrama não incluirá as linhas da vida que você criou depois da interação utilizada, mesmo se o uso de interação abrange-los agora.  
  
#### <a name="to-create-a-reusable-sequence-from-existing-messages"></a>Para criar uma sequência reutilizável de mensagens existentes  
  
-   A mensagem que você deseja mover e, em seguida, clique com o botão direito **mover para diagrama**.  
  
     Visual Studio:  
  
    -   Substitui com uma interação usa a mensagem selecionada e quaisquer mensagens subsidiárias.  
  
    -   Move as substituído mensagens para um novo diagrama de sequência.  
  
    -   Cria um vínculo entre o uso de interação e o novo diagrama de sequência.  
  
#### <a name="to-navigate-to-the-sequence-referenced-by-an-interaction-use"></a>Para navegar para a sequência referenciada por um uso de interação  
  
-   Clique duas vezes o uso de interação.  
  
     \- ou -  
  
     O uso de interação com o botão direito do mouse e, em seguida, clique em **ir para a sequência**.  
  
### <a name="creating-a-placeholder-with-an-interaction-use"></a>Criar um espaço reservado com um uso de interação  
 Você pode criar um interação com o uso sem vinculá-lo até outro diagrama. Você pode usar isso como um espaço reservado para uma parte da sequência de cujos detalhes ainda serão serão solucionados. Use o nome da interação usada para indicar o resultado desejado.  
  
##  <a name="Collapse"></a> Recolhendo grupos de linhas da vida  
 Você pode recolher um conjunto de linhas da vida juntos, para que o grupo é exibido como uma linha da vida. Isso ajuda você a visualizar um grupo de objetos como um único componente. Usos de interação entre linhas de vida em um grupo recolhido e de mensagens estão ocultos. Mensagens e as sequências de interação que incluem outras linhas de vida são mostradas.  
  
#### <a name="to-collapse-a-group-of-lifelines-together"></a>Para recolher um grupo de linhas da vida juntos  
  
1.  Selecione dois ou mais linhas de vida.  
  
2.  Clique em um deles e, em seguida, clique em **recolher**.  
  
     As linhas de vida separadas são substituídas por uma única linha da vida.  
  
     Mensagens e usos de interação que envolvem somente os membros do grupo estão ocultos.  
  
3.  Para renomear o grupo, clique no nome.  
  
    > [!NOTE]
    >  O nome do grupo serão perdido quando você expande o grupo.  
  
#### <a name="to-expand-a-collapsed-group"></a>Para expandir um grupo recolhido  
  
-   Clique com botão direito na linha de vida recolhida e, em seguida, clique em **expandir**.  
  
    > [!NOTE]
    >  O nome do grupo serão perdidos, juntamente com todos os links a partir do grupo para comentários ou itens de trabalho.  
  
##  <a name="Fragments"></a> Descrever estruturas de controle com fragmentos  
 Você pode usar os fragmentos combinados (13) para definir o processamento simultâneo, ramificações e loops em um diagrama de sequência. Como alternativa, considere usar um diagrama de atividade. O diagrama de atividade não é tão útil mostrar mensagens entre os atores na, mas em alguns casos, é melhor para mostrando a simultaneidade, ramificações e loops.  
  
 Para obter uma lista completa dos tipos de fragmento, consulte [descrever o fluxo de controle com fragmentos em diagramas de sequência UML](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md).  
  
#### <a name="to-create-a-combined-fragment"></a>Para criar um fragmento combinado  
  
1.  Selecione uma mensagem ou uma sequência de mensagens inicial tudo na mesma linha da vida ou ocorrência de execução.  
  
    > [!NOTE]
    >  Selecione as setas de mensagem, não as ocorrências de execução que as mensagens apontam para.  
  
2.  Clique em uma das mensagens, aponte para **envolver com**e, em seguida, clique no tipo de fragmento que você precisa.  
  
     Um novo fragmento é exibida. Ele contém as mensagens que você selecionou.  
  
     Se o tipo de fragmento combinado permite que vários fragmentos, um fragmento vazio também será exibida.  
  
3.  Para definir o protetor de um fragmento, a borda de fragmento com o botão direito e, em seguida, clique em **propriedades**. Defina as **Guard** propriedade.  
  
     O protetor é usado para definir a condição para uma ramificação ou um loop.  
  
4.  Para adicionar um novo fragmento para um tipo que permite que vários fragmentos, o limite de um fragmento com o botão direito e aponte para **adicionar**. Clique em **operando de interação antes** ou **interação operando após**.  
  
5.  Para adicionar novas mensagens para um fragmento, use as ferramentas de mensagem, ou copiar e colar.  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Vídeo: Fazer um rascunho de interações com o uso de diagramas de sequência](http://go.microsoft.com/fwlink/?LinkId=201113)



