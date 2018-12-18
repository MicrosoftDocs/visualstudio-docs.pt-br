---
title: 'Diagramas de atividade UML: Diretrizes | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML diagrams, activity
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- activity diagrams
- UML, activity diagrams
ms.assetid: fe5dbe96-79ab-483a-b9bc-44d0d1d3efc2
caps.latest.revision: 50
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: a13db375305e96c4657e007f9cd8bfffbf34f990
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722687"
---
# <a name="uml-activity-diagrams-guidelines"></a>Diagramas de atividade UML: diretrizes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, você pode desenhar um diagrama de atividade para descrever um processo de negócios ou um algoritmo de software como um fluxo de trabalho por meio de uma série de ações. As pessoas, os componentes de software ou dispositivos podem executar essas ações. Para uma demonstração em vídeo, consulte: [captura de fluxos de trabalho comerciais por meio de diagramas de atividade](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-4-Capture-Business-Workflows/).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Para criar um diagrama de atividade UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
 Você pode usar um diagrama de atividade para muitas finalidades:  
  
- Para descrever um processo de negócios ou um fluxo de trabalho entre usuários e seu sistema. Para obter mais informações, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
- Para descrever as etapas realizadas em um caso de uso. Para obter mais informações, consulte [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md).  
  
- Para descrever um método, função ou operação no software. Para obter mais informações, consulte [modelar a arquitetura do seu aplicativo](../modeling/model-your-app-s-architecture.md).  
  
  Desenhar um diagrama de atividade pode ajudar a aperfeiçoar o processo. Se o diagrama de um processo existente for muito complexa, você pode considerar como o processo pode ser simplificado.  
  
  Para informações de referência sobre os elementos em diagramas de atividade, consulte [diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md).  
  
##  <a name="Relationships"></a> Relação com outros diagramas  
 Se você desenhar um diagrama de atividade para descrever um processo comercial ou uma forma em que os usuários usam o seu sistema, você pode desenhar um diagrama de caso de uso para mostrar uma exibição diferente das mesmas informações. No diagrama de caso, você desenhar as ações que os casos de uso. Dê os casos de uso com os mesmos nomes que as ações correspondentes. As vantagens da exibição de casos de uso são o que você pode:  
  
- Mostrar em um diagrama como maior ações/casos de uso são compostos de partes menores, usando a relação de inclusões.  
  
- Conecte-se cada caso de uso/ação explicitamente para os usuários ou sistemas externos envolvidas na sua execução.  
  
- Desenhe os limites em torno de ações/casos de uso com suporte pelo seu sistema, ou cada componente principal dele.  
  
  Você também pode desenhar um diagrama de atividade para descrever o design detalhado de uma operação de software.  
  
  Em um diagrama de atividade, você pode mostrar o fluxo de dados passados entre ações. Consulte a seção sobre [que descreve o fluxo de dados](#DataFlows). Mas um diagrama de atividade não descreve a estrutura dos dados. Para essa finalidade, você pode desenhar um diagrama de classe UML. Para obter informações, consulte [diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md).  
  
##  <a name="BasicSteps"></a> Etapas básicas para desenhar diagramas de atividade  
 Etapas detalhadas para a criação de qualquer um dos diagramas de modelagem são descritas em [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
#### <a name="to-draw-an-activity-diagram"></a>Para desenhar um diagrama de atividade  
  
1.  Sobre o **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
2.  Sob **modelos**, clique em **diagrama de atividade UML**.  
  
3.  Nomeie o diagrama.  
  
4.  Na **adicionar ao projeto de modelagem**, selecione um projeto de modelagem existente na sua solução, ou **criar um novo projeto de modelagem**.  
  
#### <a name="to-draw-elements-on-an-activity-diagram"></a>Para desenhar os elementos em um diagrama de atividade  
  
1.  Arraste os elementos da caixa de ferramentas para o diagrama.  
  
     Comece colocando as atividades principais no diagrama, conectando-os e, em seguida, adicionar os toques finais como nós iniciais e finais.  
  
    > [!NOTE]
    >  É possível arrastar os elementos existentes para o diagrama do Gerenciador de modelos UML.  
  
2.  Para conectar os elementos, siga estas etapas:  
  
    1.  No **diagrama de atividade** caixa de ferramentas, clique em **conector**.  
  
    2.  No diagrama, clique no elemento de origem.  
  
    3.  Clique no elemento de destino.  
  
        > [!NOTE]
        >  Para usar uma ferramenta várias vezes, clique duas vezes na ferramenta na caixa de ferramentas.  
  
#### <a name="to-move-an-activity-to-another-package"></a>Para mover uma atividade para outro pacote  
  
-   Na **Gerenciador de modelos UML**, arraste a atividade em um pacote.  
  
     \- ou -  
  
-   Na **Gerenciador de modelos UML**, a atividade com o botão direito e clique em **Recortar**. Em seguida, o pacote com o botão direito e clique em **colar**.  
  
    > [!NOTE]
    >  A atividade será exibida no Gerenciador de modelos UML somente quando você adiciona o primeiro elemento no diagrama.  
  
##  <a name="SimpleControlFlow"></a> Descrevendo o fluxo de controle  
 Um diagrama de atividade descreve um algoritmo de processo ou software de negócios como uma série de ações. Setas de conector mostram como controle é passado em sequência de uma ação para a próxima. Normalmente, uma ação pode iniciar somente depois que a ação anterior foi concluída.  
  
 A figura a seguir é um exemplo de como você pode mostrar uma sequência de ações com ações, conectores, branches e loops. Cada elemento é explicado mais detalhadamente nas seções a seguir.  
  
 ![Um diagrama de atividade simples](../modeling/media/uml-actguidectrl.png "UML_ActGuideCtrl")  
  
 Use os diagramas de atividade **ações** e **conectores** para descrever seu aplicativo como uma série de ações ou um sistema com o controle que fluem em sequência de uma ação para a próxima.  
  
- Criar uma **ação** (1) para cada tarefa principal que é executada por um usuário, o sistema ou ambos em colaboração.  
  
  > [!NOTE]
  >  Tente descrever seu processo ou o algoritmo com apenas algumas ações. Você pode usar **chame ações de comportamento** para definir cada ação em mais detalhes em um diagrama separado, conforme descrito em [descrevendo subpropriedades atividades com ações de comportamento chamar](#Subactivities).  
  
- Certifique-se de que o título de cada ação indica claramente o que ele normalmente alcança.  
  
- Vincular as ações na sequência com **conectores** (2).  
  
- Cada ação termina antes de começa a próxima ação no fluxo de controle. Se você quiser descrevem ações que se sobrepõem, use uma **nó de bifurcação** conforme descrito na seção [fluxos simultâneos](#Concurrent).  
  
  Embora o diagrama descreve a sequência de ações, ele não descreve como as ações são executadas ou como o controle é passado de uma ação para a próxima. Se você usar o diagrama para representar um processo comercial, controle pode ser passado, por exemplo, quando uma pessoa envia uma mensagem de email para outro. Se você usar o diagrama para representar um design de software, controle pode ser passado pelo fluxo normal de execução de uma instrução para o próximo.  
  
### <a name="describing-decisions-and-loops"></a>Descrevendo as decisões e Loops  
  
-   Use uma **nó de decisão** (3) para indicar um ponto em que o resultado de uma decisão determina a próxima etapa. Você pode desenhar quantos caminhos de saída, como você deseja.  
  
-   Se você usar o diagrama de atividade para definir a parte de um aplicativo, você deve definir as proteções (4) para que fique claro quando cada caminho deve ser tomado. O conector com o botão direito, clique em **propriedades**e, nas **propriedades** janela, digite um valor para o **Guard** campo.  
  
-   Nem sempre é necessário definir as proteções. Por exemplo, se você usar o diagrama de atividade para descrever um processo de negócios ou um protocolo de interação, uma ramificação define a gama de opções abertas para o usuário ou para os componentes de interação.  
  
-   Use uma **nó mesclar** (5) para reunir-se de que dois ou mais fluxos alternativos ramificam em uma **nó de decisão**.  
  
    > [!NOTE]
    >  Você deve usar um **mesclar nó** reunir todos os fluxos alternativos, em vez de reunir os fluxos em uma ação. No exemplo, não seria correto para se conectar a partir do nó de decisão diretamente de volta para **escolha o Item de Menu**. Isso ocorre porque uma ação não é iniciado até que os threads de controle tem chegado em todos os seus conectores de entrada. Portanto, você deve reunir apenas fluxos simultâneos em uma ação. Para obter mais informações, consulte [fluxos simultâneos](#Concurrent).  
  
-   Use ramificações para descrever loops, conforme mostrado no exemplo.  
  
    > [!NOTE]
    >  Experimente aninhar loops de forma bem estruturada, como você faria no código do programa. Se você descrevendo um processo de negócios existente, isso poderia revelar algumas oportunidades para melhorá-lo.  
  
### <a name="starting-the-activity"></a>Iniciar a atividade  
 Há duas maneiras de indicar pontos de entrada em uma atividade:  
  
-   **Nó inicial**  
  
     Criar uma **inicial do nó** (6) para indicar a primeira ação de atividade.  
  
     Esse método é mais útil quando você descrevendo uma atividade de subpropriedades, ou em que você não precisa declarar explicitamente o que inicia a atividade. Por exemplo, a atividade de ordem uma refeição claramente começa quando um cliente obtém faminto.  
  
-   **Aceitar o nó de evento**  
  
     Crie **aceitar eventos nós**, conforme descrito na seção [fluxos simultâneos](#Concurrent), para indicar o início de um thread que responde a um evento específico, como um entrada do usuário. Não fornecem um fluxo de entrada para o nó. A omissão de um fluxo de entrada indica que um thread será iniciado sempre que o evento ocorre.  
  
     Esse método é mais útil quando você descreve uma resposta a um evento externo específico.  
  
### <a name="ending-the-activity"></a>Encerrando a atividade  
 Use uma **nó Final da atividade** (7) para indicar o final de uma atividade.  
  
-   Quando um thread de controle atinge uma **nó Final da atividade**, ações simultâneas e atividades de subpropriedades de toda a atividade encerrar.  
  
-   Você pode usar mais de um nó Final da atividade de reduzir a confusão dos conectores adicionais.  
  
### <a name="interrupting-the-activity"></a>Interromper a atividade  
 Para descrever como o fluxo comum de uma atividade pode ser interrompido, por exemplo, se o usuário decidir cancelar o processo, você pode criar um nó de evento aceitar que escuta esse evento. Para obter mais informações, consulte a seção [fluxos simultâneos](#Concurrent). Crie um fluxo de controle do que para um nó Final da atividade (7).  
  
### <a name="swimlanes"></a>Raias  
 Às vezes é útil organizar as ações de uma atividade em áreas correspondentes às funções de negócios que executam as ações ou objetos diferentes. Essas áreas convencionalmente são organizadas em colunas e são chamadas *raias*.  
  
- Use linhas ou retângulos do **formas simples** seção da caixa de ferramentas para desenhar as raias ou outras áreas.  
  
- Para rotular cada Raia, crie um comentário e defina suas **Transparent** propriedade **verdadeiro**.  
  
  Formas simples não fazem parte do modelo de UML e não aparecem no Gerenciador de modelos UML.  
  
##  <a name="DataFlows"></a> Descrevendo o fluxo de dados  
 Você pode descrever os dados que passam para dentro e fora de uma atividade em qualquer uma das duas maneiras:  
  
-   Use uma **nó do objeto**. Esse é o método mais simples de descrever as informações que passam entre atividades. Um nó de objeto é como uma variável em um programa. Ele representa algo que armazena um ou mais valores que estão passando de uma ação para outro.  
  
-   Use uma **pino de saída** e uma **entrada de Pin**. Esse método permite descrever separadamente as saídas de uma ação e as entradas para outra. PINs são como parâmetros em um programa. PINs representam portas em que os objetos podem entram e saem de uma ação.  
  
    > [!NOTE]
    >  Para obter uma visão geral dos elementos usados nesta seção, consulte a seção de fluxos de dados do tópico ver [diagramas de atividade UML: referência](../modeling/uml-activity-diagrams-reference.md).  
  
### <a name="describing-data-flow-with-object-nodes"></a>Descrevendo o fluxo de dados conosco de objeto  
 A maioria dos fluxos de controle carregam dados. Por exemplo, o fluxo de saída da ação de "Cliente fornece detalhes" transmite uma referência para o endereço de envio.  
  
 Se você deseja descrever esses dados no seu diagrama, você pode substituir um conector com um nó de objeto e dois conectores, como mostrado na figura a seguir.  
  
 ![Nós de objeto podem mostrar dados passados entre ações](../modeling/media/uml-actguidedata.png "UML_ActGuideData")  
  
 Observe que os retângulos com cantos arredondados, como o despacho de mercadorias, representam ações, em que o processamento ocorre. Os retângulos com cantos quadrados, como endereço de remessa, representam um fluxo de objetos de uma ação para outro.  
  
 Nomeie o nó do objeto que reflete a função do nó como um condutor ou buffer dos objetos que fluem entre as ações.  
  
 Você pode definir as **tipo** do nó de objeto na janela Propriedades. O tipo pode ser um tipo primitivo como inteiro, ou uma classe, interface ou enumeração que você tenha definido em um diagrama de classe. Por exemplo, você poderia criar um endereço de remessa de classe com atributos de endereço de rua, cidade e assim por diante, junto com uma associação a uma outra classe é chamada Customer. Para obter mais informações, consulte [diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md).  
  
> [!NOTE]
>  Se você digitar o nome de um tipo que não tenha sido definido, um item será adicionado sob **tipos não especificados** no Gerenciador de modelos UML. Se você definir um tipo de nome em um diagrama de classe depois, você deve redefinir o tipo de nó de objeto, de modo que ele se refere ao novo tipo.  
  
#### <a name="buffering-data-in-object-nodes"></a>Buffer de dados em nós de objeto  
 Um nó de objeto pode agir como um buffer para vários objetos. Na ilustração a seguir, o fluxo de controle mostra que o usuário pode ir em torno de [escolha mais] (1) muitas vezes, um loop enquanto o nó do objeto de itens de Menu escolhida (2) acumula as opções do usuário. Por fim, quando o usuário tiver concluído sua seleção, o controle passa para a ação de confirmar a ordem (3), que aceita a lista completa de opções do buffer de itens de Menu escolhido.  
  
 ![Buffer de dados em nós de objeto](../modeling/media/uml-actguidebuffer.png "UML_ActGuideBuffer")  
  
 Você pode especificar como os itens em um buffer são armazenados, definindo as propriedades do nó de objeto:  
  
-   Defina as **ordenação** propriedade:  
  
    -   **Não ordenada** para especificar uma ordem aleatória ou não especificada. (Padrão.)  
  
    -   **Ordenado** para especificar uma ordem de acordo com uma chave específica.  
  
    -   **PEPS** para especificar uma ordem do primeiro a entrar, primeiro a sair.  
  
    -   **UEPS** para especificar uma ordem de último a entrar, primeiro a sair.  
  
-   Defina as **limite superior** propriedade para especificar o número máximo de objetos que podem ser contidos no buffer. O padrão é *. Isso significa que não há nenhum limite.  
  
### <a name="describing-data-flow-with-input-and-output-pins"></a>Descrevendo o fluxo de dados com entrada e os pinos de saída  
 Use uma **pino de saída** e uma **entrada de Pin** separadamente descrever as saídas de uma ação e as entradas para outra.  
  
 ![Pinos de entrada e saídos são parâmetros de ação](../modeling/media/uml-actguidepins.png "UML_ActGuidePins")  
  
 Para criar um pin, clique em **entrada de Pin** ou **pino de saída** na caixa de ferramentas e, em seguida, clique em uma ação. Em seguida, você pode mover o pin em torno do perímetro da ação e altere seu nome. Você pode criar entrada e saída pinos em qualquer tipo de ação, incluindo **chame ações de comportamento**, **chame ações de operação**, **enviar ações de sinal**, e  **Aceite as ações de evento**.  
  
 Um conector entre dois pinos representa um fluxo de objeto, como os fluxos de e para um nó de objeto.  
  
 Nomeie cada pino que indica a função dos objetos ele produz ou aceita, como um nome de parâmetro.  
  
 Você pode definir o tipo de objetos transmitidos na **tipo** propriedade. Isso deve ser um tipo que você criou em um diagrama de classe UML.  
  
 Os objetos que fluem entre os pinos conectados devem ser compatíveis de alguma forma. Isso pode ocorrer porque os objetos gerados pelo pino de saída pertencem a um tipo derivado do tipo do pino de entrada.  
  
 Como alternativa, você pode especificar que o fluxo do objeto inclui uma transformação que converte dados entre o tipo do pino de saída e o tipo do pino de entrada. A transformação mais comuns desse tipo apenas extrai a parte apropriada de um tipo maior. O exemplo na Figura implica a existência de uma transformação que extrai o endereço de envio de OrderDetail.  
  
##  <a name="Details"></a> Definindo uma ação em mais detalhes  
 Além de usar o nome da ação para se certificar de que o resultado que normalmente, ela deve atingir, aqui estão algumas maneiras de adicionar mais detalhes a uma ação:  
  
-   Escrever uma descrição mais detalhada na **corpo** propriedade. Por exemplo, você poderia escrever um fragmento de código do programa ou pseudocódigo ou uma descrição completa dos resultados obtidos.  
  
-   Substituir a ação com uma ação de chamar de comportamento e descrever seu comportamento detalhado dentro de um diagrama de atividade separado. Ver [descrevendo subpropriedades atividades com ações de comportamento de chamadas](#Subactivities).  
  
-   Defina a ação **Local pós-condições** e **pré-condições Local** propriedades para descrever seu resultado em detalhes mais específicos. Para obter mais informações, consulte [definindo pós-condições e pré-condições](#Postcondition).  
  
###  <a name="Subactivities"></a> Descrevendo o subdiretório atividades com ações de comportamento de chamadas  
 Você pode descrever o comportamento detalhado de uma ação usando um diagrama de atividade separado. Um comportamento chamado é um diagrama de atividade que é representado no seu diagrama de atividade principal por uma ação de chamar de comportamento. Você também pode usar a ação de chamar de comportamento para descrever o comportamento que é compartilhado entre diferentes atividades para que você não precise desenhar a atividade de subpropriedades várias vezes.  
  
 Na figura a seguir, diagrama 1 mostra uma atividade que tem uma ação de chamar de comportamento e 2 do diagrama mostra o diagrama de atividade subpropriedades que mostra o comportamento de chamada.  
  
 ![Um diagrama de atividade separado mostra ações detalhadas](../modeling/media/uml-actguidedetail.png "UML_ActGuideDetail")  
  
##### <a name="to-describe-a-sub-activity-with-a-call-behavior-action"></a>Para descrever uma atividade de subpropriedades com uma ação de chamar de comportamento  
  
1.  Para criar o diagrama para a atividade de subpropriedades, no **Gerenciador de soluções**, clique em seu projeto de modelagem, aponte para **Add**e, em seguida, clique em **Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo **modelos** clique em **diagrama de atividade** e, no **nome** caixa, digite o nome que você planeja dar sua **chame a ação de comportamento**.  
  
3.  Desenhe o fluxo de trabalho detalhados para a atividade de subpropriedades. Esse é o comportamento de chamada.  
  
    -   No diagrama de atividade de subpropriedades chamado, o **inicial do nó** indica onde o controle é iniciado quando o comportamento de chamada é invocado. O **nó Final da atividade** mostra onde o controle deve retornar para a atividade pai.  
  
4.  Definir a **comportamento** propriedade do **plano de ação de comportamento** para se referir ao diagrama de comportamento de chamada.  
  
    > [!NOTE]
    >  O diagrama de atividade de subpropriedades deve ter alguns elementos nele ou o diagrama não estará disponível na lista suspensa para o **comportamento** propriedade. Além disso, o ícone trident não aparecerão no seu **plano de ação de comportamento** forma até que você defina seu **comportamento** propriedade.  
  
5.  Defina as **é síncrona** propriedade da ação para indicar se sua atividade aguarda para concluir a atividade de chamada.  
  
    -   Se você definir **síncrona é** como false, você está indicando que o fluxo pode continuar para a próxima ação antes que a atividade de chamada é concluída. Você não deve definir a saída de fluem de pins ou dados de saída da ação.  
  
### <a name="describing-data-flow-in-and-out-of-sub-activities"></a>Descrevendo o fluxo de dados dentro e fora de subpropriedades de atividades  
 Você pode descrever os dados que fluem para dentro e fora de subpropriedades de atividades, da mesma forma que você use os parâmetros no software.  
  
- Criar entrada e saída pinos (1) sobre a ação de comportamento chamado, para cada parte dos dados que fluem para dentro ou fora a ação. Nome de cada um deles apropriadamente.  
  
- No diagrama de atividade de subpropriedades, criar uma **nó do parâmetro de atividade** (2) para cada pino de entrada e saído na chamada da ação. Atribua o mesmo nome como seu pino correspondente a cada nó.  
  
  > [!NOTE]
  >  Um nó de parâmetro de atividade é semelhante a um nó de objeto. Para verificar que tipo de nó que você está examinando, clique com botão direito no nó e, em seguida, clique em **propriedades**. O tipo de nó é mostrado no cabeçalho da janela Propriedades.  
  
- No diagrama de atividade de subpropriedades, desenhe conectores que mostram o fluxo de objetos para dentro ou fora de cada nó de parâmetro de atividade.  
  
  ![Os pinos em Call Behavior são mapeados para parâmetros de atividade](../modeling/media/uml-actguidesub.png "UML_ActGuideSub")  
  
###  <a name="Postcondition"></a> Definindo as pós-condições e pré-condições  
 Você pode usar o **Local pós-condições** e **pré-condições Local** propriedades para especificar detalhes do resultado de uma ação. Essas propriedades descrevem o efeito da ação sem descrevendo como o efeito é obtido.  
  
 Para definir essas propriedades, a ação com o botão direito e, em seguida, clique em **propriedades**. Digite valores para as propriedades na janela Propriedades.  
  
#### <a name="local-postconditions"></a>Pós-condições locais  
 Uma pós-condição é uma condição que deve ser atendida antes que a ação pode ser considerada concluída. Na ação do exemplo pedido de confirmação, a pós-condição pode ser:  
  
 O cliente forneceu os detalhes de válido e completas que são necessários para o processamento de seu cartão de crédito.  
  
 Uma pós-condição pode expressar uma relação entre os estados de antes e depois que a ação tenha ocorrido. Por exemplo:  
  
 A taxa de juros double é o que era antes.  
  
 Você pode escrever pós-condições em um estilo mais formal, referindo-se a atributos específicos dos dados tratados de ações. Por exemplo:  
  
 `InvoiceTotal == Sum(OrderItem.MenuItem.Price)`  
  
#### <a name="local-preconditions"></a>Pré-condições locais  
 Uma pré-condição é uma condição que deve ser verdadeira quando a ação está pronta para começar. Por exemplo, a ação pedido confirmar pode ter a pré-condição:  
  
 Cliente tiver optado pelo menos um item de menu.  
  
### <a name="describing-calls-to-operations"></a>Descrevendo as chamadas para operações  
 Em geral, uma ação descreve o trabalho executado por qualquer combinação de pessoas, software ou em computadores. Mas você pode usar uma ação de operação chamar para descrever uma chamada para a função ou método de software específico.  
  
-   Defina o nome da ação de operação chamar para indicar qual operação é chamada e em qual componente ou objeto.  
  
-   Adicione os pinos de entrada e saídos para a ação de operação de chamada, para descrever parâmetros e valores de retorno.  
  
-   Você pode definir as **é síncrona** propriedade da ação para indicar se sua atividade aguarda a conclusão da operação.  
  
    -   Se você definir **síncrona é** como false, você está indicando que o fluxo pode continuar para a próxima ação antes da operação de chamada é concluída. Você não deve definir a saída de fluem de pins ou dados de saída da ação.  
  
##  <a name="Concurrent"></a> Fluxos simultâneos  
 Você pode usar o **nó de bifurcação** e o **nó ingressar** para descrever dois ou mais threads de atividades que podem ser executadas ao mesmo tempo.  
  
 ![Os nós de bifurcação e junção mostram fluxos simultâneos](../modeling/media/uml-actguideconcurrent.png "UML_ActGuideConcurrent")  
  
 O efeito do **nós de bifurcação /** (1) é dividir o thread de controle em dois ou mais threads. Quando termina a ação anterior, todas as ações em relação à saída da bifurcação de podem iniciar.  
  
 Um **ingressar o nó** (2) reúne threads simultâneos. A ação após o **ingressar o nó** não pode começar até que todas as ações que levam ao **nó ingressar** forem concluídas.  
  
### <a name="describing-signals-and-events"></a>Descrevendo os sinais e eventos  
 Você pode mostrar uma etapa em um processo que envia um sinal como uma ação de sinal enviar em uma atividade. Você pode mostrar uma etapa que aguarda um evento antes de continuar a etapa como uma ação de evento aceitar ou sinal específico.  
  
 Por exemplo, você pode mostrar uma etapa que envia um pedido e, em seguida, outra etapa que deve receber a ordem antes que ele processa esse pedido.  
  
#### <a name="sending-a-signal"></a>Enviar um sinal  
 Use uma ação de sinal enviar (3) para indicar que uma mensagem de algum tipo ou um sinal é enviada para outros processos ou atividades. Use o nome da ação para indicar qual tipo de envios de mensagem-lo.  
  
-   Controle imediatamente passa para a próxima ação no fluxo de controle, se houver um.  
  
-   Você não pode usar uma ação de sinal enviar para descrever como o seu processo responde a todas as informações retornadas. Para fazer isso, use uma ação de evento aceitar separada.  
  
-   Você pode mostrar o fluxo de dados de entrada a uma ação de sinal enviar, para indicar quais dados podem ser enviados com a mensagem de saída. Para obter mais informações, consulte [que descreve o fluxo de dados](#DataFlows).  
  
#### <a name="waiting-for-a-signal-or-event"></a>Aguardando um sinal ou um evento  
 Use uma ação de evento aceitar (4) para indicar que essa atividade aguarda alguns eventos externos ou mensagem de entrada. Use o nome da ação para indicar o tipo de evento que ele aguarda.  
  
-   Para mostrar que sua atividade aguarda um evento externo ou uma mensagem em um ponto específico no seu fluxo, desenhe uma ação de evento aceitar com um fluxo de entrada, no local apropriado na atividade.  
  
-   Para mostrar que sua atividade pode responder a um evento externo ou uma mensagem a qualquer momento, desenhe uma ação de evento aceitar sem qualquer fluxo de entrada. Quando ocorre o evento externo nomeado, um novo thread começará em sua atividade, da aceitar a ação de evento.  
  
-   Você não pode usar uma ação de evento aceitar para descrever qualquer valor retornado para o remetente do sinal. Use uma ação de sinal enviar separada para essa finalidade.  
  
-   Você pode mostrar os fluxos de dados de saída da ação, para mostrar como sua atividade processa os dados recebidos no sinal de. Se você quiser mostrar mais de um fluxo de saída, você deve definir a **IsUnmarshall** propriedade da ação de evento aceitar, que indica que a ação analisa o sinal de entrada em seus componentes separados. Para obter mais informações, consulte [que descreve o fluxo de dados](#DataFlows).  
  
### <a name="describing-multiple-data-flows"></a>Descrevendo dados de vários fluxos  
 Você pode desenhar mais de um fluxo de controle ou saindo de uma ação para indicar que mais de um thread surge quando termina a ação de fluxo de objeto. O efeito é semelhante de uma bifurcação, exceto que você pode usar uma mistura de fluxos de controle e o objeto.  
  
 O exemplo a seguir mostra vários fluxos de e em ações.  
  
 ![Objeto fluem em paralelo](../modeling/media/uml-actguidemulti.png "UML_ActGuideMulti")  
  
 Quando a ação de "Cliente fornece detalhes" for concluído, ele produz dois objetos: "Endereço de remessa" e "Detalhes do cartão de crédito." Os dois objetos ir adiante para processamento por ações diferentes.  
  
 Como uma ação requer que todas as suas entradas para estar disponível antes de iniciar, a última ação não é iniciado até que todas as ações que levam a ele sejam concluídas.  
  
### <a name="streams"></a>Fluxos  
 Você pode usar um diagrama de atividade para ajudar você descrevem uma série de ações que são executadas ao mesmo tempo ou de um pipeline e passar continuamente os dados de uma ação para outro.  
  
 A intenção no exemplo a seguir é que cada ação pode produzir objetos e continuam a funcionar. Como não há nenhum fluxo de controle, cada ação pode iniciar assim que ele recebe seus objetos primeiro.  
  
 Observe que os conectores nesse exemplo são fluxos de objeto, porque todos eles têm pelo menos uma extremidade em um nó de parâmetro de atividade, o nó de objeto, ou em uma entrada ou o pino de saída.  
  
 ![Um fluxo de dados](../modeling/media/uml-actguidestream.png "UML_ActGuideStream")  
  
 1. O exemplo tem três nós de parâmetro de atividade, que representam suas entradas e saídas.  
  
 2. Nós de objeto, pinos de entrada e os pinos de saída podem representar buffers. Você pode definir o limite superior no buffer, a propriedade de um nó de objeto para o número de objetos de estado pode ser ao mesmo tempo.  
  
 3. Você pode usar nós de decisão para mostrar que divide um fluxo, enviando objetos diferentes ramificações diferentes. Você pode usar comentários ou os títulos de nós para explicar o que é o critério de divisão.  
  
 4. Você pode usar nós de bifurcação para mostrar que duas ou mais cópias dos objetos são feitas, enviá-los para processamento simultâneo.  
  
 5. Você pode usar nós de junção para mostrar que os dois fluxos de processamento são mesclados novamente em um.  
  
### <a name="selection-and-transformation"></a>Seleção e transformação  
 Você pode especificar que os objetos em um fluxo do objeto são transformados, selecionado, ou ambos. Fluxo de um objeto é um fluxo para ou de um pin ou um nó de objeto.  
  
- Uma transformação descreve como inserir um fluxo de objetos são convertidos em outro tipo.  
  
- Uma seleção como só descreve alguns dos objetos inserindo um fluxo são transmitidos para a ação de recebimento.  
  
  O exemplo mostra uma transformação. A primeira ação no diagrama 1 produz um CEP ou código postal, em um pino de saída. Isso está conectado a um pino de entrada na segunda ação. Mas a segunda ação espera um endereço totalmente especificado. A conversão de um tipo para outro é especificada em uma segunda atividade de pesquisa de endereço. Isso é referenciado na propriedade de transformação do fluxo de objeto. A atividade de pesquisa de endereço contém um nó de parâmetro de atividade para o CEP de entrada e outro nó de parâmetro de atividade para o endereço completo da saída.  
  
  ![Objeto definida em outro diagrama de transformação](../modeling/media/uml-actguidetransform.png "UML_ActGuideTransform")  
  
  Você pode especificar uma transformação ou seleção de duas maneiras:  
  
- Anexe um comentário ao pino de entrada ou saído.  
  
  -   Para distinguir esta descrição de um comentário geral, você pode começar o comentário com <\<**transformação**>> ou <\<**seleção**>>.  
  
- Especifique a transformação ou a seleção em detalhes em um diagrama de atividade separado.  
  
  -   Se você usar esse método, anexe um comentário também, para deixar claro para os leitores que a transformação foi definida.  
  
##### <a name="to-specify-a-transformation-or-selection-in-a-separate-activity-diagram"></a>Para especificar uma transformação ou a seleção em um diagrama de atividade separado  
  
1. Crie um novo diagrama de atividade na qual descrever o fluxo de transformação ou a seleção.  
  
   -   Na **Gerenciador de soluções**, clique em seu projeto, aponte para **Add**, clique em **Novo Item**e, em seguida, clique em **diagrama de atividade**. Dê um nome apropriado para o fluxo de transformação ou seleção de diagrama. Clique em **Adicionar**.  
  
2. No novo diagrama:  
  
   1.  Crie dois nós de parâmetro de atividade, uma para o fluxo de entrada e outra para a saída.  
  
   2.  Crie ações interconectadas com fluxos de objeto. Isso mostra como funciona a seleção ou transformação.  
  
3. Em qualquer diagrama em que você deseja usar a transformação ou seleção:  
  
   1.  Crie um fluxo de objeto, ou seja, um conector para ou de uma entrada ou pino de saída, um nó de objeto ou um nó de parâmetro de atividade.  
  
   2.  O fluxo do objeto com o botão direito e, em seguida, clique em **propriedades**.  
  
   3.  No **Transformation** ou **seleção** propriedade, selecione o diagrama em que você especificou o fluxo de transformação ou a seleção.  
  
   Você também pode definir uma seleção de um nó de objeto e na entrada individual e pinos de saída. Definir uma atividade de seleção como no procedimento anterior e, em seguida, defina as **seleção** propriedade de nó de objeto ou pino de entrada ou saído.  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Diagramas de caso de uso UML: referência](../modeling/uml-use-case-diagrams-reference.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Vídeo: Capturar fluxos de trabalho comerciais usando diagramas de atividade](http://channel9.msdn.com/posts/clinted/UML-with-VS-2010-Part-4-Capture-Business-Workflows/)



