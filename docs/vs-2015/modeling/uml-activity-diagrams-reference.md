---
title: 'Diagramas de atividade UML: Referência | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.activitydiagram.diagram
- vs.teamarch.activitydiagram.toolbox
- vs.teamarch.UMLModelExplorer.activitydiagram
helpviewer_keywords:
- UML diagrams, activity
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- activity diagrams
- UML, activity diagrams
- behaviors, UML
ms.assetid: 07efcd17-2a96-4052-9957-6dcccbb725ee
caps.latest.revision: 50
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 2dcfa13a7ac97a5afd3e315fcef13a706c5f4bce
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810462"
---
# <a name="uml-activity-diagrams-reference"></a>Diagramas de atividade UML: referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma *diagrama de atividade* mostra um processo de negócios ou um software como um fluxo de trabalho por meio de uma série de ações. As pessoas, os componentes de software ou computadores podem executar essas ações.  
  
 Você pode usar um diagrama de atividade para descrever os processos de vários tipos, como os exemplos a seguir:  
  
- Um processo de negócios ou um fluxo de trabalho entre usuários e seu sistema. Para obter mais informações, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
- As etapas realizadas em um caso de uso. Para obter mais informações, consulte [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md).  
  
- Um protocolo de software, ou seja, as sequências permitidos de interações entre componentes.  
  
- Um algoritmo de software.  
  
  Este tópico descreve os elementos que você pode usar diagramas de atividade. Para obter mais informações detalhadas na informações sobre atividade de desenho consulte diagramas [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md). Para criar um diagrama de atividade UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**. Para obter mais informações sobre como desenhar diagramas de modelagem em geral, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
## <a name="reading-activity-diagrams"></a>Diagramas de atividade de leitura  
 As tabelas nas seções a seguir descrevem os elementos que você pode usar em um diagrama de atividade e suas propriedades principais. Para obter uma lista completa das propriedades dos elementos, consulte [propriedades de elementos em diagramas de atividade UML](../modeling/properties-of-elements-on-uml-activity-diagrams.md).  
  
 As ações e outros elementos que aparecem em um diagrama de atividade formam uma atividade. Você pode ver a atividade no Gerenciador de modelos UML. Ele é criado quando você adiciona o primeiro elemento no diagrama.  
  
 Para ler um diagrama, imagine que um token ou o thread de controle, passa os conectores de uma ação para a próxima.  
  
### <a name="simple-control-flows"></a>Fluxos de controle simples  
 Você pode mostrar uma sequência de ações com ramificações e loops. Para obter mais informações sobre como usar os elementos descritos aqui, consulte a seção que descreve o fluxo de controle do tópico [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).  
  
 ![Um fluxo de controle simples](../modeling/media/uml-actovsimple.png "UML_ActOvSimple")  
  
||||  
|-|-|-|  
|**Forma**|**Elemento**|**Descrição e propriedades principais**|  
|1|**Ação**|Uma etapa na atividade, no qual os usuários ou software executam alguma tarefa.<br /><br /> A ação pode iniciar quando um token tiver atingido todos os seus fluxos de entrada. Quando ele termina, os tokens são enviados em todos os fluxos de saída.<br /><br /> -   **Corpo** -Especifica a ação em detalhes.<br />-   **Linguagem** -o idioma da expressão no corpo.<br />-   **Pós-condições locais** -restrições que devem ser atendidas quando a execução termina. A meta obtida pela ação.<br />-   **As pré-condições locais** -restrições que devem ser atendidas antes do início da execução.|  
|2|**Fluxo de Controle**|Um conector que mostra o fluxo de controle entre ações. Para interpretar o diagrama, imagine que um token de fluxos de uma ação para a próxima.<br /><br /> Para criar um fluxo de controle, use o **conector** ferramenta.|  
|3|**Nó inicial**|Indica a primeira ação ou ações na atividade. Quando a atividade é iniciado, um token de fluxos a partir do nó inicial.|  
|4|**Nó Final da atividade**|Acabando com a atividade. Quando um token é recebido, a atividade será finalizada.|  
|5|**Nó de decisão**|Uma ramificação condicional em um fluxo. Tem uma entrada e duas ou mais saídas. Um token de entrada surge em apenas uma das saídas.|  
|6|**Guard**|Uma condição que especifica se um token pode fluir ao longo de um conector. Mais frequentemente usada nos fluxos de saída de um nó de decisão.<br /><br /> Para definir um protetor, um fluxo com o botão direito, clique em **propriedades** e, em seguida, defina as **proteger** propriedade.|  
|7|**Nó de mesclagem**|Necessário para mesclar os fluxos foram divididos com um nó de decisão. Tem duas ou mais entradas e uma saída. Um token em qualquer entrada surge na saída.|  
|8|**Comentário**|Fornece informações adicionais sobre os elementos aos quais ele está vinculado.|  
|9|**Plano de ação de comportamento**|Uma ação que é definida em mais detalhes em outro diagrama de atividade.<br /><br /> -   **IsSynchronous** – se for true, a ação aguarda até que a atividade será finalizada.<br />-   **Comportamento** -a atividade invocada.|  
|(não mostrado)|**Ação de operação de chamada**|Uma ação que chama uma operação em uma instância de uma classe.|  
||**Atividade**|O fluxo de trabalho que é representado por um diagrama de atividade. Para ver as propriedades de uma atividade, você deve selecioná-lo na **Gerenciador de modelos UML**.<br /><br /> -   **É somente leitura** – se for true, a atividade não deve alterar o estado de qualquer objeto.<br />-   **É a única execução** – se for true, há no máximo uma execução de neste diagrama, cada vez.|  
||**Diagrama de Atividade UML**|O diagrama que exibe uma atividade. Para ver suas propriedades, clique em uma parte vazia do diagrama. **Observação:** os nomes de diagrama de atividade, o arquivo que contém o diagrama e a atividade exibida no diagrama pode todos ser diferente.|  
  
### <a name="concurrent-flows"></a>Fluxos simultâneos  
 Você pode descrever as sequências de ações que são executadas ao mesmo tempo. Para obter mais informações, consulte fluxos simultâneos de desenho.  
  
 ![Diagrama de atividade mostrando o fluxo simultâneo](../modeling/media/uml-actovconcurrent.png "UML_ActovConcurrent")  
  
||||  
|-|-|-|  
|**Forma**|**Elemento**|**Descrição**|  
|11|**Nó de bifurcação**|Divide um único fluxo em fluxos simultâneos. Cada token de entrada produz um token em cada conector de saída.|  
|12|**Adicionar nó**|Combina fluxos simultâneos em um único fluxo. Quando cada fluxo de entrada tem uma token em espera, um token é produzido na saída.|  
|13|**Enviar ação de sinal**|Uma ação que envia uma mensagem ou um sinal para outra atividade ou a um thread simultâneo na mesma atividade. O tipo e o conteúdo da mensagem é indicado pelo título da ação ou especificado nos comentários adicionais.<br /><br /> A ação pode enviar dados do sinal, que pode ser passado para a ação em um fluxo de objeto ou o pino de entrada (16).|  
|14|**Aceitar a ação de evento**|Uma ação que aguarda uma mensagem ou um sinal de que a ação possa continuar. O tipo de mensagem, que a ação pode receber é indicado pelo título ou especificado nos comentários adicionais.<br /><br /> Se a ação não tem nenhum fluxo de controle de entrada, ele produz um token, sempre que receber uma mensagem.<br /><br /> A ação pode receber dados em sinal, que pode ser passado em um objeto fluxo ou saída de pin (17).<br /><br /> -   **IsUnmarshall** - se verdadeiro, pode haver vários pinos de saída com tipo e os dados são unmarshalled neles. Se for false, todos os dados apareçam em um pin.|  
  
###  <a name="DataFlow"></a> Fluxos de dados  
 Você pode descrever o fluxo de dados de uma ação para outro. Para obter mais informações sobre os elementos usados nesta seção, consulte a seção de fluxos de dados de desenho do tópico de diretrizes para desenhar um diagrama de atividade.  
  
 ![Diagrama de atividade mostrando o fluxo de dados](../modeling/media/uml-actovdata.png "UML_ActOvData")  
  
||||  
|-|-|-|  
|**Forma**|**Elemento**|**Descrição**|  
|15|**Nó de objeto**|Representa os dados que passam ao longo de um fluxo.<br /><br /> -   **Ordenação** - como vários tokens são armazenados.<br />-   **Seleção** -invoca um processo, que pode ser definido em outro diagrama, que filtra os dados.<br />-   **Limite superior** -0 indica que os dados devem passar diretamente ao longo do fluxo; \* indica que os dados podem ser armazenados no fluxo.<br />-   **Tipo** -o tipo de objetos armazenados e transmitidas.|  
|16|**Entrada de Pin**|Representa a data em que uma ação pode receber quando ele é executado.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|  
|17|**Pinos de saída**|Representa os dados que uma ação gera quando ele é executado.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|  
|18|**Nó de parâmetro de atividade**|Um nó de objeto por meio do qual dados podem ser recebidos ou produzidos pela atividade.<br /><br /> Usado quando a atividade representada pelo diagrama é chamada de outra atividade, ou quando o diagrama descreve uma operação ou função.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|  
|(não mostrado)|**Fluxo de objeto**|Um conector que mostra o fluxo de dados entre os nós de objeto e ações.<br /><br /> Para criar um fluxo de objeto, use o **conector** ferramenta para vincular uma entrada ou o pino de saída ou um nó de objeto para outro elemento.<br /><br /> -   **Seleção** -invoca um processo, que pode ser definido em outro diagrama, que filtra os dados.<br />-   **Transformação** -invoca um processo, que pode ser definido em outro diagrama, que transforma os dados.<br />-   **IsMulticast** -indica que pode haver vários objetos de destinatário ou componentes.<br />-   **IsMultiReceive** -indica que entradas podem ser recebidas de vários objetos ou componentes.|  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)



