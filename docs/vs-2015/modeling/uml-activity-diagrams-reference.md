---
title: 'Diagramas de atividade UML: referência | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 960e9469290bca42abd252d497c2ce72e62e41a4
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531528"
---
# <a name="uml-activity-diagrams-reference"></a>Diagramas de atividade UML: referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um *diagrama de atividade* mostra um processo de negócios ou um processo de software como um fluxo de trabalho por meio de uma série de ações. Pessoas, componentes de software ou computadores podem executar essas ações.

 Você pode usar um diagrama de atividade para descrever os processos de vários tipos, como os exemplos a seguir:

- Um processo de negócios ou um fluxo de trabalho entre usuários e seu sistema. Para obter mais informações, consulte [requisitos de usuário de modelo](../modeling/model-user-requirements.md).

- As etapas executadas em um caso de uso. Para obter mais informações, consulte [diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md).

- Um protocolo de software, ou seja, as sequências de interações permitidas entre os componentes.

- Um algoritmo de software.

  Este tópico descreve os elementos que você pode usar em diagramas de atividade. Para obter informações mais detalhadas sobre diagramas de atividade de desenho, consulte [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md). Para criar um diagrama de atividade UML, no menu **arquitetura** , clique em **novo UML ou diagrama de camada**. Para obter mais informações sobre como desenhar diagramas de modelagem em geral, consulte [Editar diagramas e modelos UML](../modeling/edit-uml-models-and-diagrams.md).

## <a name="reading-activity-diagrams"></a>Lendo diagramas de atividade
 As tabelas nas seções a seguir descrevem os elementos que você pode usar em um diagrama de atividade e suas propriedades principais. Para obter uma lista completa das propriedades dos elementos, consulte [Propriedades de elementos em diagramas de atividade UML](../modeling/properties-of-elements-on-uml-activity-diagrams.md).

 As ações e outros elementos que aparecem em um diagrama de atividade formam uma atividade. Você pode ver a atividade no Gerenciador de modelos UML. Ele é criado quando você adiciona o primeiro elemento ao diagrama.

 Para ler um diagrama, imagine que um token, ou thread de controle, passe os conectores de uma ação para a próxima.

### <a name="simple-control-flows"></a>Fluxos de controle simples
 Você pode mostrar uma sequência de ações com branches e loops. Para obter mais informações sobre como usar os elementos descritos aqui, consulte a seção descrevendo o fluxo de controle do tópico [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md).

 ![Um fluxo de controle simples](../modeling/media/uml-actovsimple.png "UML_ActOvSimple")

|**La**|**Elemento**|**Descrição e propriedades principais**|
|-|-|-|
|1|**Ação**|Uma etapa na atividade, na qual os usuários ou software executam alguma tarefa.<br /><br /> A ação pode ser iniciada quando um token chega a todos os fluxos de entrada. Quando termina, os tokens são enviados em todos os fluxos de saída.<br /><br /> -   **Corpo** -especifica a ação em detalhes.<br />-   **Idioma** -o idioma da expressão no corpo.<br />-   **Condições locais** -restrições que devem ser satisfeitas quando a execução termina. A meta alcançada pela ação.<br />-   **Precondições locais** -restrições que devem ser atendidas antes do início da execução.|
|2|**Fluxo de controle**|Um conector que mostra o fluxo de controle entre as ações. Para interpretar o diagrama, imagine que um token flua de uma ação para a seguinte.<br /><br /> Para criar um fluxo de controle, use a ferramenta **conector** .|
|3|**Nó inicial**|Indica a primeira ação ou ações na atividade. Quando a atividade é iniciada, um token flui do nó inicial.|
|4|**Nó final da atividade**|Um End para a atividade. Quando um token chega, a atividade é encerrada.|
|5|**Nó de decisão**|Uma ramificação condicional em um fluxo. Tem uma entrada e duas ou mais saídas. Um token de entrada surge em apenas uma das saídas.|
|6|**Proteja**|Uma condição que especifica se um token pode fluir ao longo de um conector. Usado com mais frequência nos fluxos de saída de um nó de decisão.<br /><br /> Para definir uma proteção, clique com o botão direito do mouse em um fluxo, clique em **Propriedades** e defina a propriedade **Guard** .|
|7|**Mesclar nó**|Necessário para mesclar os fluxos que foram divididos com um nó de decisão. Tem duas ou mais entradas e uma saída. Um token em qualquer entrada surge na saída.|
|8|**Comentário**|Fornece informações adicionais sobre os elementos aos quais ele está vinculado.|
|9|**Ação de comportamento da chamada**|Uma ação que é definida em mais detalhes em outro diagrama de atividade.<br /><br /> -   **IsSynchronous** -se for true, a ação aguardará até que a atividade seja encerrada.<br />-   **Comportamento** -a atividade invocada.|
|(não exibido)|**Ação de operação de chamada**|Uma ação que chama uma operação em uma instância de uma classe.|
||**Atividade**|O fluxo de trabalho que é representado por um diagrama de atividade. Para ver as propriedades de uma atividade, você deve selecioná-la no **Gerenciador de modelos UML**.<br /><br /> -   **É somente leitura** -se for true, a atividade não deverá alterar o estado de nenhum objeto.<br />-   **É execução única** -se for true, haverá no máximo uma execução deste diagrama por vez.|
||**Diagrama de Atividade UML**|O diagrama que exibe uma atividade. Para ver suas propriedades, clique em uma parte vazia do diagrama. **Observação:**  Os nomes do diagrama de atividade, o arquivo que contém o diagrama e a atividade exibida pelo diagrama podem ser diferentes.|

### <a name="concurrent-flows"></a>Fluxos simultâneos
 Você pode descrever as sequências de ações que são executadas ao mesmo tempo. Para obter mais informações, consulte desenhando fluxos simultâneos.

 ![Diagrama de atividade mostrando o fluxo simultâneo](../modeling/media/uml-actovconcurrent.png "UML_ActovConcurrent")

|**La**|**Elemento**|**Descrição**|
|-|-|-|
|11|**Nó de bifurcação**|Divide um único fluxo em fluxos simultâneos. Cada token de entrada produz um token em cada conector de saída.|
|12|**Nó de junção**|Combina fluxos simultâneos em um único fluxo. Quando cada fluxo de entrada tem um token aguardando, um token é produzido na saída.|
|13|**Enviar ação de sinal**|Uma ação que envia uma mensagem ou um sinal para outra atividade ou para um thread simultâneo na mesma atividade. O tipo e o conteúdo da mensagem são implícitos pelo título da ação ou especificados em comentários adicionais.<br /><br /> A ação pode enviar dados no sinal, que podem ser passados para a ação em um fluxo de objeto ou PIN de entrada (16).|
|14|**Ação de evento Accept**|Uma ação que aguarda uma mensagem ou um sinal antes que a ação possa continuar. O tipo de mensagem que a ação pode receber é implícito pelo título ou especificado em comentários adicionais.<br /><br /> Se a ação não tiver nenhum fluxo de controle de entrada, ela produzirá um token sempre que receber uma mensagem.<br /><br /> A ação pode receber dados no sinal, que podem ser passados em um fluxo de objeto ou pino de saída (17).<br /><br /> -   **IsUnmarshall** -se true, pode haver vários Pins de saída digitados e os dados são desempacotados para eles. Se for false, todos os dados aparecerão em um PIN.|

### <a name="data-flows"></a><a name="DataFlow"></a>Fluxos de dados
 Você pode descrever o fluxo de dados de uma ação para outra. Para obter mais informações sobre os elementos usados nesta seção, consulte a seção desenho de fluxos de dados do tópico diretrizes para desenhar um diagrama de atividade.

 ![Diagrama de atividade mostrando o fluxo de dados](../modeling/media/uml-actovdata.png "UML_ActOvData")

|**La**|**Elemento**|**Descrição**|
|-|-|-|
|15|**Nó de objeto**|Representa os dados que passam em um fluxo.<br /><br /> -   **Ordenando** -como vários tokens são armazenados.<br />-   **Seleção** – invoca um processo, que pode ser definido em outro diagrama, que filtra os dados.<br />-   **Limite superior** -0 indica que os dados devem passar diretamente ao longo do fluxo; \*indica que os dados podem ser armazenados no fluxo.<br />-   **Tipo** -o tipo de objetos armazenados e transmitidos.|
|16|**PIN de entrada**|Representa os dados que uma ação pode receber ao ser executada.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|
|17|**Pino de saída**|Representa os dados que uma ação produz quando ela é executada.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|
|18|**Nó de parâmetro de atividade**|Um nó de objeto por meio do qual os dados podem ser recebidos ou produzidos pela atividade.<br /><br /> Usado quando a atividade representada pelo diagrama é chamada de outra atividade ou quando o diagrama descreve uma operação ou função.<br /><br /> -   **Tipo** -o tipo de objetos transmitidos.|
|(não exibido)|**Fluxo de objeto**|Um conector que mostra o fluxo de dados entre ações e nós de objeto.<br /><br /> Para criar um fluxo de objeto, use a ferramenta de **conector** para vincular um PIN de entrada ou de saída ou um nó de objeto a outro elemento.<br /><br /> -   **Seleção** – invoca um processo, que pode ser definido em outro diagrama, que filtra os dados.<br />-   **Transformation** – invoca um processo, que pode ser definido em outro diagrama, que transforma os dados.<br />-   **IsMulticast** – indica que pode haver vários objetos ou componentes de destinatário.<br />-   **IsMultireceive** -indica que as entradas podem ser recebidas de vários objetos ou componentes.|

## <a name="see-also"></a>Consulte Também
 [Editar modelos UML e](../modeling/edit-uml-models-and-diagrams.md) diagramas [diagramas de atividade UML: diretrizes](../modeling/uml-activity-diagrams-guidelines.md)
