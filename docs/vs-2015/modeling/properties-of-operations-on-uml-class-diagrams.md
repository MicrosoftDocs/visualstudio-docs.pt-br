---
title: Diagramas de classe de propriedades de operações em UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.logicalclassdiagram.operation.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: 4128f3e2-3a51-4edf-b3e4-b7f170a32f6b
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7a5a2e18c41f99462231da2a11dc80a0ae01e99e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51804456"
---
# <a name="properties-of-operations-on-uml-class-diagrams"></a>Propriedades de operações em diagramas de classes UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de classe UML, você pode adicionar *operações* a classes e interfaces. Uma operação é um método ou função que pode ser executada por uma instância de uma classe ou interface.  

 Para adicionar uma operação, clique com botão direito a classe ou interface, aponte para **Add**e, em seguida, clique em **operação**.  

 Se as operações de uma classe no diagrama não estiverem visíveis, clique na divisa de expansão na parte superior da classe ou interface. Se você pode ver os **operação** cabeçalho, clique em **[+]** para expandir a seção de operações.  

## <a name="signature-of-an-operation"></a>Assinatura de uma operação  
 A assinatura de uma operação é a linha de texto que representa a ele em uma classe ou interface em um diagrama de classe UML. Ele tem o seguinte formato:  

 \+ OperationName (parameter1: Type1 [*],...): ReturnType [\*]  

 \+ indica a visibilidade pública. Os outros valores permitidos são - (privados) # (protegido) ~ (pacote).  

 `OperationName` está sublinhado, se o **é estática** propriedade é true e está em itálico se o **Is Abstract** propriedade é true.  

 `: ReturnType` é omitido se nenhum tipo de retorno é definido.  

 `[*]` indica a multiplicidade de um parâmetro ou tipo de retorno. Ele é omitido se a multiplicidade for 1.  

 Consulte a próxima seção para obter uma descrição completa dessas propriedades.  

## <a name="properties"></a>Propriedades  
 Estas são as propriedades de uma operação em uma classe ou interface em um diagrama de classe UML.  

 Para ver as propriedades de uma operação, a operação na classe ou interface no diagrama com o botão direito e, em seguida, clique em **propriedades**. As propriedades aparecem na **propriedades** janela.  


|      Propriedade       |   Padrão    |                                                                                                                                                                                 Descrição                                                                                                                                                                                 |
|---------------------|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      **Nome**       | (um novo nome) |                                                                                                                                                                Deve ser exclusivo dentro do tipo recipiente.                                                                                                                                                                 |
|   **Parâmetros**    |    (nenhum)    |      Uma lista que tem o formato <em>nome</em>**:**<em>tipo</em>**,** <em>nome</em>**:**  <em>Tipo de</em>**,...** Clique em **[...]**  para editar a lista.<br /><br /> Os tipos podem ser tipos primitivos ou tipos que são definidos no modelo. Se você inserir um nome para um novo tipo nesta propriedade, um tipo será adicionado para o **tipos não especificados** seção do Gerenciador de modelos UML.      |
|   **Tipo de retorno**   |    (nenhum)    |                                                                               **(nenhum)** , ou um tipo primitivo ou um tipo que é definido no modelo. Se você inserir um nome para um novo tipo nesta propriedade, um tipo será adicionado para o **tipos não especificados** seção do Gerenciador de modelos UML.                                                                                |
| **Pós-condições**  |    (nenhum)    |                                                                                                                         Uma condição opcional especificando uma relação entre o estado do sistema antes e após a execução da operação.                                                                                                                         |
|  **Pré-condições**  |    (nenhum)    |                                                                                                                            Uma condição opcional especificando as suposições sobre o estado do sistema antes da operação inicia a execução.                                                                                                                            |
| **Condições de corpo** |    (nenhum)    |                                                                                                                                                       Uma restrição opcional nos valores retornados pela operação.                                                                                                                                                       |
|   **Visibilidade**    |    Público    |                  Os caracteres que aparecem na assinatura e os valores permitidos são:<br /><br /> **+ Público** - visível globalmente<br /><br /> **-Privada** - não é visível fora do tipo proprietário<br /><br /> **# Protegido** - visível a tipos derivados do proprietário<br /><br /> **~ Empacotar** - visível para outros tipos de dentro do mesmo pacote.                   |
|    **Assinatura**    |  +*Nome*)   |                                                                                      Resume a visibilidade, nome, parâmetros e tipo de retorno dessa operação. Você pode alterar essas propriedades, editando a assinatura no diagrama ou editando as propriedades individuais.                                                                                      |
|   **Itens de trabalho**    | 0 associados |                                                                                                  Contagem de itens de trabalho associados. Somente leitura.<br /><br /> Para obter mais informações, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).                                                                                                  |
|   **Simultaneidade**   |  Sequencial  | **Sequencial** -a operação está ou será criada sem controle de simultaneidade. Chamar essa operação simultânea pode resultar em falhas.<br /><br /> **Protegido** -a operação bloqueará automaticamente até que outras instâncias dele sejam concluídas.<br /><br /> **Simultâneas** -a operação foi projetada para que podem ser executadas simultaneamente várias chamadas para ele. |
|    **É estático**    |    False     |                                                                                                  Se for true, esta operação é compartilhada entre todas as instâncias desse tipo.<br /><br /> Se for true, o nome da operação será sublinhado, onde ele aparece no diagrama.                                                                                                   |
|   **É abstrato**   |    False     |                                                                                                                                        Se verdadeiro, nenhum código é associado esta operação. Portanto, a classe proprietária é abstrata.                                                                                                                                         |
|     **É folha**     |    False     |                                                                                                                                              O designer pretende que esta operação não pode ser substituída em classes derivadas.                                                                                                                                              |
|    **É a consulta**     |    False     |                                                                                                 Se for true, não há alterações significativas para o estado do sistema são feitas por essa operação. Portanto, ele pode ser usado, por exemplo, em um teste para verificar o estado do sistema.                                                                                                  |
|  **Multiplicidade**   |      1       |                                 **1** -um único valor do tipo especificado.<br /><br /> **entre 0 e 1** -pode ser `null`.<br /><br /> \* -uma coleção de valores do tipo especificado.<br /><br /> **1...\\**  \* – uma coleção que contém pelo menos um valor.<br /><br /> *n* `..` *m* -uma coleção que contém entre `n` e `m` valores.                                  |
|   **É ordenada**    |    False     |                                                                                                                                             Se for true, a coleção de forma uma lista sequencial. Para **multiplicidade** mais de 1.                                                                                                                                              |
|    **É exclusivo**    |    False     |                                                                                                                                         Não se for true, há nenhum valor duplicado na coleção. Para **multiplicidade** mais de 1.                                                                                                                                         |

## <a name="see-also"></a>Consulte também  
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Propriedades de tipos em diagramas de classe UML](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [Propriedades de atributos em diagramas de classe UML](../modeling/properties-of-attributes-on-uml-class-diagrams.md)   
 [Propriedades de associações em diagramas de classe UML](../modeling/properties-of-associations-on-uml-class-diagrams.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)



