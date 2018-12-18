---
title: 'Diagramas de caso de uso UML: Referência | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.usecasediagram.toolbox
- vs.teamarch.usecasediagram.diagram
- vs.teamarch.UMLModelExplorer.usecasediagram
helpviewer_keywords:
- diagrams - modeling, use case
- UML, use case diagrams
- diagrams - modeling, UML use case
- use case diagrams
- UML diagrams, use case
ms.assetid: aa15772b-eb67-4366-b145-b559112817df
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 64eece28fc46fce799eff01e7ed1e7302e939dbc
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791755"
---
# <a name="uml-use-case-diagrams-reference"></a>Diagramas de caso de uso UML: referência
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, uma *diagrama de caso de uso* resume quem usa o aplicativo ou sistema e o que podem fazer com ele. Para criar um diagrama de caso de uso UML, nos **arquitetura** menu, clique em **UML novo ou diagrama de camada**.  
  
 Um diagrama de caso de uso atua como um foco para a descrição dos requisitos de usuário. Ele descreve as relações entre os principais componentes, os usuários e requisitos. Ele descreve os requisitos em detalhes. eles podem ser descritos em diagramas separados ou em documentos que podem ser vinculados a cada caso de uso. Para obter informações sobre como os diagramas de caso de uso podem ajudá-lo a entender, discuta e comunicar-se suas necessidades de usuários, consulte [requisitos de usuário do modelo](../modeling/model-user-requirements.md).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
> [!NOTE]
>  Este tópico descreve os elementos que estão disponíveis em diagramas de caso de uso. Para obter mais informações sobre como desenhar diagramas de caso de uso, consulte [diagramas de caso de usar o UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md). Para obter mais informações sobre como criar e desenhar diagramas de modelagem, consulte [modelos e diagramas UML editar](../modeling/edit-uml-models-and-diagrams.md).  
  
## <a name="reading-use-case-diagrams"></a>Diagramas de caso de uso de leitura  
 As tabelas nas seções a seguir descrevem os elementos que estão disponíveis em um diagrama de caso de uso, junto com suas propriedades principais. Para obter uma lista completa das propriedades, consulte [propriedades de elementos em UML usam diagramas de caso](../modeling/properties-of-elements-on-uml-use-case-diagrams.md).  
  
### <a name="actors-use-cases-and-subsystems"></a>Os atores, casos de uso e subsistemas  
 ![Elementos em um diagrama de caso de uso](../modeling/media/uml-ucovactor.png "UML_UCOvActor")  
  
|**Forma**|**Elemento**|**Descrição e propriedades principais**|  
|---------------|-----------------|-----------------------------------------|  
|1|**Ator**|Representa um usuário, uma organização ou um sistema externo que interage com o aplicativo ou sistema. Um ator é uma espécie de tipo.<br /><br /> -   **O caminho da imagem** -o caminho do arquivo de uma imagem que deve ser usado em vez do ícone padrão do ator. O ícone deve ser um arquivo de recurso dentro do projeto do Visual Studio.|  
|2|**Caso de uso**|Representa as ações executadas por um ou mais atores na busca de uma meta específica. Um caso de uso é uma espécie de tipo.<br /><br /> -   **Assuntos** -o subsistema no qual o caso de uso é exibido.|  
|3|**Associação**|Indica que um ator faz parte de um caso de uso.|  
|4|**Subsistema ou componente**|O sistema ou aplicativo que você está trabalhando ou uma parte dele. Pode ser qualquer coisa, desde uma grande rede a uma única classe em um aplicativo.<br /><br /> Os casos de uso que oferece suporte a um sistema ou componente aparecem dentro de seu retângulo. Ele pode ser útil mostrar que alguns casos de uso fora do retângulo, para esclarecer o escopo do seu sistema.<br /><br /> Um subsistema de um diagrama de caso de uso tem basicamente o mesmo tipo como um componente em um diagrama de componente.<br /><br /> -   **É instanciado indiretamente** - se FALSO, o sistema em execução tem um ou mais objetos que diretamente correspondem a esse subsistema. Se for true, o subsistema é uma construção em seu design que aparece no sistema em execução por meio da instanciação de suas partes constituintes.|  
  
### <a name="structuring-use-cases"></a>Estruturar os casos de uso  
 ![Casos de uso com include, estender e generalização](../modeling/media/uml-ucovstructure.png "UML_UCOvStructure")  
  
|Forma|**Elemento**|Descrição|  
|-----------|-----------------|-----------------|  
|5|**Incluir**|Um caso de uso incluindo chama ou invoca um incluído. Inclusão é usada para mostrar como um caso de uso se divide em etapas menores. É o caso de uso incluído ao final da seta.<br /><br /> Observe que o diagrama não mostra a ordem das etapas. Você pode usar um diagrama de atividade, o diagrama de sequência ou a outro documento para descrever esses detalhes.|  
|6|**Estender**|Um caso de uso estendendo adiciona metas e etapas para o caso de uso estendido. As extensões operam apenas sob determinadas condições. É o caso de uso estendidos ao final da seta.<br /><br /> Observe que o diagrama não mostra as circunstâncias exatas em que se aplica a extensão: você pode gravar em um comentário ou outro documento.|  
|7|**Herança**|Relaciona especializado e um elemento generalizado. O elemento generalizado é ao final da seta.<br /><br /> Um caso de uso especializado herda as metas e os atores de seu generalização e pode adicionar mais específico de metas e etapas para a obtenção de-los.<br /><br /> Um ator especializado herda os casos de uso, atributos e associações de seu generalização e pode adicionar mais.|  
|8|**dependência**|Indica que o design da fonte de dependerá do design do destino.|  
|9|**Comentário**|Usado para adicionar observações gerais ao diagrama.|  
|10|**Artefato**|Um artefato fornece um link para outro diagrama ou documento. Você pode criá-lo, arrastando um arquivo no Gerenciador de soluções. Ele pode ser vinculado a uma dependência para qualquer outro elemento no diagrama. Um artefato é normalmente usado para vincular um caso de uso para um diagrama de sequência, a página do OneNote, o documento do Word ou a apresentação do PowerPoint que o descreve em detalhes. O documento pode ser um item no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] solução ou um documento em um local compartilhado, como um site do SharePoint.<br /><br /> -   **Hiperlink**. O caminho de arquivo ou URL do diagrama ou do documento.<br /><br /> Clique duas vezes em um artefato para abrir o arquivo ou página da web ao qual ela está vinculada.|  
|11 (não mostrado)|**Pacotes**|Casos de uso, atores e subsistemas podem estar contidos em pacotes. Formas de pacote não aparecem no diagrama, mas você pode definir as **LinkedPackage** propriedade do diagrama. Elementos que você criar posteriormente no diagrama são colocados dentro do pacote. Para obter mais informações, consulte [definir pacotes e namespaces](../modeling/define-packages-and-namespaces.md).|  
  
## <a name="see-also"></a>Consulte também  
 [Diagramas de caso de uso UML: diretrizes](../modeling/uml-use-case-diagrams-guidelines.md)   
 [Editar modelos e diagramas UML](../modeling/edit-uml-models-and-diagrams.md)   
 [Diagramas de sequência UML: referência](../modeling/uml-sequence-diagrams-reference.md)   
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)   
 [Diagramas de componente UML: referência](../modeling/uml-component-diagrams-reference.md)



