---
title: Diagramas de classe de propriedades de associações em UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.common.association.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: f82bcd34-7903-4c00-8da1-613efa07d223
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b132ee2aa0f67662fcfcad92b8ae945c2d66c680
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51810269"
---
# <a name="properties-of-associations-on-uml-class-diagrams"></a>Propriedades de associações em diagramas de classes UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de classe UML, você pode desenhar *associações* entre qualquer par de tipos. Um tipo é uma classe, interface ou enumeração.  

 Uma associação indica que o sistema que você está desenvolvendo armazena links de algum tipo entre as instâncias dos tipos associados. Em geral, isso não significa nada sobre a implementação dos links. Por exemplo, eles podem ser ponteiros, linhas em uma tabela, a referência cruzada nomes em XML e assim por diante.  

 Uma associação é um método diagramática de mostrar um atributo ou um par de atributos. Por exemplo, se você tiver definido uma classe Restaurant para ter um atributo de tipo Menu, você pode declarar a mesma definição desenhando uma associação entre o restaurante e Menu.  

 Para desenhar uma associação, clique em **associação** na caixa de ferramentas, clique no primeiro tipo, em seguida, o segundo. Você pode clicar duas vezes do mesmo tipo para mostrar que as instâncias podem ser vinculadas a outras instâncias do mesmo tipo.  

## <a name="properties"></a>Propriedades  
 Estas são as propriedades de uma associação em um diagrama de classe UML.  

 Para ver as propriedades de uma associação, a associação com o botão direito e, em seguida, clique em **propriedades**. As propriedades aparecerão na janela Propriedades.  

 Algumas das propriedades também são visíveis no diagrama, conforme mostrado na ilustração a seguir.  

 ![Propriedades em associações](../modeling/media/uml-classprop.png "UML_ClassProp")  

|**Property**|Descrição|  
|------------------|-----------------|  
|**Nome (1)**|Identifica a associação. Também é exibido no diagrama próximo ao ponto intermediário da associação.|  
|**Nome qualificado**|Identifica exclusivamente a associação. O prefixo com o nome qualificado do pacote que contém a primeira função da associação.|  
|**Itens de trabalho**|O número de itens de trabalho vinculados a esta associação. Para vincular itens de trabalho, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).|  
|**Cor**|A cor do conector. Ao contrário das outras propriedades, esta é uma propriedade dessa exibição de associação, não uma propriedade da relação no modelo subjacente.|  
|**Primeira função**<br /><br /> **Segunda função**|Cada extremidade da associação é chamada de uma função. Cada função descreve as propriedades do atributo equivalente na classe na extremidade oposta da associação.<br /><br /> No diagrama de exemplo, a associação entre o Menu e o Item de Menu tem funções chamadas de Menu e conteúdo.<br /><br /> Conteúdo é o nome de um atributo na classe de Menu.|  

### <a name="properties-of-each-role"></a>Propriedades de cada função  
 Para ver as propriedades de cada função, expanda o **função primeiro** ou **segunda função** propriedade.  


|     **Property**     |          **Padrão**          |                                                                                                                                                                                                                                                                                                                                        Descrição                                                                                                                                                                                                                                                                                                                                         |
|----------------------|-------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  **Nome da função (2)**   | Nome do tipo a essa função |                                                                                                                                                                                                                                                                                                       O nome da função. É exibido próximo ao final da associação no diagrama.                                                                                                                                                                                                                                                                                                        |
|   **Agregação**    |             Nenhum              |                                                                        **Nenhum** (4) – representa uma relação geral entre instâncias de classes.<br /><br /> **Composição** (5) – o objeto essa função contém o objeto na função oposta. Você pode usar o **composto** ferramenta para criar uma associação com agregação composta.<br /><br /> **Compartilhado** (6) – objeto essa função contém referências ao objeto em outra função. Você pode usar o **agregação** ferramenta para criar uma associação com a agregação compartilhada.<br /><br /> A interpretação exata é aberta a convenção de local.                                                                         |
|    **É derivado**    |             False             |                                                                                                                                                                                                                          Se for true, o objeto final do link é calculado de outros atributos e associações. Por exemplo, MyWorkPlace calculado a partir MyEmployer.WorkPlace. Os detalhes devem ser digitados na descrição ou um comentário anexado.                                                                                                                                                                                                                           |
| **É derivado de união** |             False             |                                                                                                                                                                                                                                                                                                             Se for true, a função é a união de um conjunto de funções em tipos derivados.                                                                                                                                                                                                                                                                                                             |
|   **É navegável**   |             verdadeiro              |                                                 A associação pode ser lidos nessa direção. Dada uma instância da função oposta, o software que você descrevendo com eficiência pode determinar a instância associada essa função.<br /><br /> Se uma função é Navigable e o outro não é, uma seta aparece (7) sobre a associação na direção navegável.<br /><br /> Por padrão, a ferramenta de associação cria uma associação que é navegável em uma única direção. Para convertê-lo em uma associação bidirecional, você pode selecionar a associação, clique na marca de ação que é exibida e, em seguida, clique em **bidirecional tornar**.                                                 |
|   **É somente leitura**   |             False             |                                                                                                                                                                                                                                                                                   Se for true, uma instância de associação não pode ser alterada depois que ele é criado. O link é sempre o mesmo objeto.                                                                                                                                                                                                                                                                                    |
| **Multiplicidade (3)** |               1               | **1** -essa extremidade da associação sempre vincula a um objeto. Na figura, cada Item de Menu tem um Menu.<br /><br /> **entre 0 e 1** – a essa extremidade de associação vincula a um objeto, ou há um link.<br /><br /> **\\**\* -todos os objetos na outra extremidade da associação está vinculado a uma coleção de objetos Este final, e a coleção pode estar vazia.<br /><br /> **1...\\**  \* -todos os objetos na outra extremidade da associação é vinculado a pelo menos um objeto este final. Na figura, cada Menu tem pelo menos um Item de Menu.<br /><br /> *n* **...** *m* -cada objeto na outra extremidade tem uma coleção de entre *n* e *m* links para objetos neste final. |
|    **É ordenada**    |             False             |                                                                                                                                                                                                                                                                                                  Se for true, a coleção retornada constitui uma lista sequencial. Para a multiplicidade mais do que 1.                                                                                                                                                                                                                                                                                                   |
|    **É exclusivo**     |             False             |                                                                                                                                                                                                                                                                                              Não se for true, há nenhum valor duplicado na coleção retornada. Para a multiplicidade mais do que 1.                                                                                                                                                                                                                                                                                              |
|    **Visibilidade**    |            Público             |                                                                                                                                                                                                                                 Público - visível globalmente<br /><br /> Privado - não é visível fora do tipo proprietário<br /><br /> Protegido - visível a tipos derivados do proprietário<br /><br /> Package - visível para outros tipos de dentro do mesmo pacote.                                                                                                                                                                                                                                  |

## <a name="see-also"></a>Consulte também  
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Propriedades de tipos em diagramas de classe UML](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)   
 [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)



