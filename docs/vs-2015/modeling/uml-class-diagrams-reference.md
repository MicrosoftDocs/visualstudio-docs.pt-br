---
title: 'Diagramas de classe UML: Referência | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.common.generalization.properties
- vs.teamarch.logicalclassdiagram.toolbox
- vs.teamarch.UMLModelExplorer.association
- vs.teamarch.common.unspecifiedtype.properties
- vs.teamarch.logicalclassdiagram.diagram
- vs.teamarch.UMLModelExplorer.logicalclassdiagram
- vs.teamarch.UMLModelExplorer.generalization
- vs.teamarch.common.unspecifiedtype
helpviewer_keywords:
- UML diagrams, class
- diagrams - modeling, class
- UML, class diagrams
- class diagrams - UML
- diagrams - modeling, UML class
ms.assetid: b7c88be0-0d86-4d65-af74-f37e8812d20f
caps.latest.revision: 43
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4f3a4fe9949236045238688a9edcd5eef911efb8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741055"
---
# <a name="uml-class-diagrams-reference"></a>Diagramas de classe UML: referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um diagrama de classe UML descreve o objeto e as informações de estruturas usadas pelo seu aplicativo, tanto internamente e em comunicação com seus usuários. Ele descreve as informações sem referência a qualquer implementação específica. Suas classes e relações podem ser implementadas de várias maneiras, como tabelas de banco de dados, nós XML ou composições de objetos de software.  
  
> [!NOTE]
>  Este tópico é sobre diagramas de classe UML. Há outro tipo de diagrama de classe, o diagrama de classe do .NET, que é usado para visualizar o código do programa. Para obter mais informações, consulte [Projetando e exibindo Classes e tipos](http://go.microsoft.com/fwlink/?LinkId=142231).  
  
 Para criar um diagrama de classe UML, nos **arquitetura** menu, escolha **UML novo ou diagrama de camada**. Para obter mais informações sobre como desenhar diagramas de classe UML, consulte [diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md). Para obter mais informações sobre como criar e desenhar diagramas de modelagem, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="reading-class-diagrams"></a>Diagramas de classe de leitura  
 A tabela nesta seção descreve os elementos que você pode ver no diagrama de classe UML. Para obter informações sobre as propriedades desses elementos, consulte os tópicos a seguir:  
  
- [Propriedades de tipos em diagramas de classe UML](../modeling/properties-of-types-on-uml-class-diagrams.md)  
  
- [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)  
  
- [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)  
  
- [Propriedades de associações em diagramas de classes UML](../modeling/properties-of-associations-on-uml-class-diagrams.md)  
  
  ![Três classes mostrando relações e as propriedades](../modeling/media/uml-classovreading.png "UML_ClassOvReading")  
  
| **Forma** |       **Elemento**        |                                                                                                                                                             **Descrição**                                                                                                                                                              |
|-----------|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     1     |        **Class**         |                                                           Uma definição de objetos que compartilham dado características estruturais ou comportamentais. Para obter mais informações, consulte [diagramas de classe de propriedades de tipos em UML](../modeling/properties-of-types-on-uml-class-diagrams.md).                                                            |
|     1     |        Classificador        |                                                                                                             O nome geral para uma classe, interface ou enumeração. Casos de uso de componentes, e os atores são também classificadores.                                                                                                             |
|     2     | Recolher / expandir de controles |                                                                                         Se você não conseguir ver os detalhes de um classificador, clique no expansor no canto superior esquerdo do classificador. Você também terá que clique em [+] em cada segmento.                                                                                         |
|     3     |      **Atributo**       |   Um valor tipado anexado a cada instância de um classificador.<br /><br /> Para adicionar um atributo, clique o **atributos** seção e, em seguida, pressione **ENTER**. Digite a assinatura do atributo. Para obter mais informações, consulte [diagramas de classe de propriedades de atributos em UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md).   |
|     4     |      **operação**       | Um método ou função que pode ser executada por instâncias de um classificador. Para adicionar uma operação, clique o **operações** seção e, em seguida, pressione **ENTER**. Digite a assinatura da operação. Para obter mais informações, consulte [diagramas de classe de propriedades de operações em UML](../modeling/properties-of-operations-on-uml-class-diagrams.md). |
|     5     |     **Associação**      |                                                                  Uma relação entre os membros dos dois classificadores. Para obter mais informações, consulte [diagramas de classe de propriedades de associações em UML](../modeling/properties-of-associations-on-uml-class-diagrams.md).                                                                   |
|    5a     |     **Agregação**      |                                                                                                    Uma associação que representa uma relação de propriedade compartilhada. O **agregação** propriedade da função proprietário é definida como **compartilhado**.                                                                                                     |
|    5b     |     **Composição**      |                                                                                                      Uma associação que representa uma relação de parte do todo. O **agregação** propriedade da função proprietário é definida como **composto**.                                                                                                      |
|     6     |   **Nome da associação**   |                                                                                                                                         O nome de uma associação. O nome pode ser deixado vazio.                                                                                                                                          |
|     7     |      **Nome da função**       |                       O nome de uma função, ou seja, uma extremidade de uma associação. Pode ser usado para fazer referência ao objeto associado. Na ilustração anterior, para qualquer ordem `O`, `O.ChosenMenu` é seu Menu associado.<br /><br /> Cada função tem suas próprias propriedades listadas nas propriedades da associação.                       |
|     8     |     **Multiplicidade**     |                                         Indica quantos dos objetos no fim pode ser vinculada a cada objeto em outro. No exemplo, cada pedido deve ser vinculado a exatamente um Menu.<br /><br /> **\\**\* significa que não há nenhum limite superior para o número de links que podem ser feitas.                                         |
|     9     |    **Generalização**    |  O *específicos* classificador herda parte de sua definição da *geral* classificador. O classificador geral é no final de seta do conector. Atributos, associações e operações são herdadas pelo classificador específico.<br /><br /> Use o **herança** ferramenta para criar uma generalização entre os dois classificadores.   |
  
 ![Pacote que contém a interface e a enumeração](../modeling/media/uml-classovpackage.png "UML_ClassOvPackage")  
  
|Forma|Elemento|Descrição|  
|-----------|-------------|-----------------|  
|10|**Interface**|Uma definição de parte do comportamento externamente visível de um objeto. Para obter mais informações, consulte [diagramas de classe de propriedades de tipos em UML](../modeling/properties-of-types-on-uml-class-diagrams.md).|  
|11|**Enumeração**|Um classificador que consiste em um conjunto de valores literais.|  
|12|**Pacote**|Um grupo de classificadores, associações, ações, as linhas de vida, componentes e pacotes. Um diagrama de classe lógicos mostra os classificadores de membro e os pacotes são contidos no pacote.<br /><br /> Nomes estão no escopo dentro de pacotes, de modo que **Class1** dentro **pacote1** é diferente da **Class1** fora desse pacote. O nome do pacote é exibido como parte do **nome qualificado** propriedades de seu conteúdo.<br /><br /> Você pode definir as **pacote vinculado** propriedade de qualquer diagrama UML para se referir a um pacote. Todos os elementos que você cria no diagrama, em seguida, vai se tornar parte do pacote. Eles serão exibidos sob o pacote na **Gerenciador de modelos UML**.|  
|13|**Importarar**|Uma relação entre pacotes, que indica que um pacote inclui todas as definições de outro.|  
|14|**dependência**|A definição ou a implementação do classificador dependente pode alterar se o classificador ao final da seta é alterado.|  
  
 ![Realização mostrada com conector e interface pirulito](../modeling/media/uml-classovrealize.png "UML_ClassOvRealize")  
  
|Forma|**Elemento**|Descrição|  
|-----------|-----------------|-----------------|  
|15|**realização**|A classe implementa as operações e atributos definidos pela interface.<br /><br /> Use o **herança** ferramenta para criar uma realização entre uma classe e uma interface.|  
|16|**realização**|Uma apresentação alternativa da mesma relação. O rótulo no símbolo de pirulito identifica a interface.<br /><br /> Para criar esta apresentação, selecione uma relação de realização existente. Uma marca de ação aparece próximo a associação. Clique na marca de ação e, em seguida, clique em **mostrar como pirulito**.|  
  
## <a name="see-also"></a>Consulte também  
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)   
 [Propriedades de tipos em diagramas de classe UML](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)   
 [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [Propriedades de associações em diagramas de classes UML](../modeling/properties-of-associations-on-uml-class-diagrams.md)



