---
title: Diagramas de classe de propriedades de atributos em UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.teamarch.logicalclassdiagram.attribute.properties
helpviewer_keywords:
- UML, element properties
ms.assetid: ba01e064-7424-4e72-98fa-42fa1c30e153
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 0129242593596ea7e3875db2a748045c50863c4c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51817354"
---
# <a name="properties-of-attributes-on-uml-class-diagrams"></a>Propriedades de atributos em diagramas de classes UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em um diagrama de classe UML, você pode adicionar *atributos* a classes e interfaces. Um atributo define os valores que podem ser anexados a instâncias da classe ou interface.  

 Para adicionar um atributo, clique com botão direito a classe ou interface, aponte para **Add**e, em seguida, clique em **atributo**.  

 Se os atributos de uma classe no diagrama não estiverem visíveis, clique na divisa na parte superior da classe ou interface para expandi-lo. Se você pode ver os **atributos** cabeçalho, clique em **[+]** para expandir a seção de atributos.  

## <a name="signature-of-an-attribute"></a>Assinatura de um atributo  
 Assinatura de um atributo é a linha que representa a ele em uma classe ou interface em um diagrama de classe UML. Ele tem este formato:  

```  
+ AttributeName : TypeName [*]  
```  

 \+ indica a visibilidade pública. Os outros valores permitidos são - (privados) # (protegido) ~ (pacote).  

 `AttributeName` está sublinhado se o atributo é estático.  

 `: TypeName` é omitido se o atributo não tem nenhum tipo.  

 `[*]` indica a multiplicidade. Ele é omitido se a multiplicidade for 1.  

## <a name="properties"></a>Propriedades  
 A tabela a seguir descreve as propriedades de um atributo em uma classe ou interface em um diagrama de classe UML.  

 Para ver as propriedades de um atributo, o atributo na classe ou interface no diagrama com o botão direito e, em seguida, clique em **propriedades**. As propriedades aparecem na janela Propriedades.  

 Para exibir as propriedades de um atributo, clique duas vezes e, em seguida, clique em **propriedades**.  


|   **Property**    | **Padrão**  |                                                                                                                                                                                                         Descrição                                                                                                                                                                                                          |
|-------------------|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Valor padrão** |   (vazio)    |                                                                                                                                                                               O valor do atributo quando o classificador é instanciado.                                                                                                                                                                                |
| **É somente leitura**  |    False     |                                                                                                                                                                                    Se for true, o valor do atributo não pode ser alterado.                                                                                                                                                                                    |
|   **É estático**   |    False     |                                                                                                                    Se for true, um único valor para esse atributo é compartilhado entre todas as instâncias desse tipo.<br /><br /> Se for true, o nome do atributo é sublinhado onde ele aparece no diagrama.                                                                                                                    |
|     **Nome**      | (um novo nome) |                                                                                                                                                                                        Deve ser exclusivo dentro do classificador proprietário.                                                                                                                                                                                        |
|     **Tipo**      |    (nenhum)    |                                                Um tipo primitivo, como **inteiro**, ou um tipo que é definido no modelo. Você não pode usar tipos de não primitivos, como **Decimal** porque o valor deve ser codificado em metadados. Se você inserir um nome para um novo tipo nesta propriedade, um tipo será adicionado para o **tipos não especificados** seção do Gerenciador de modelos UML.                                                 |
|  **Visibilidade**   |    Público    |                                     Os valores permitidos e os caracteres que aparecem na assinatura são da seguinte maneira:<br /><br /> **+ Público** - visível globalmente<br /><br /> **-Privada** - não é visível fora do tipo proprietário<br /><br /> **# Protegido** - visível a tipos derivados do proprietário<br /><br /> **~ Empacotar** - visível para outros tipos de dentro do mesmo pacote.                                      |
|  **Itens de trabalho**   | 0 associados |                                                                                                                          Contagem de itens de trabalho associados. Somente leitura.<br /><br /> Para obter mais informações, consulte [vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md).                                                                                                                           |
|    **É folha**    |    False     |                                                                                                                                                                    Se for true, ele não se destina para permitir que a redefinição desse atributo em tipos derivados.                                                                                                                                                                     |
|  **É derivado**   |    False     |                                                                                                              Se for true, esse atributo é calculado de outros atributos. Por exemplo, Diagonal, calculado de largura e altura. Os detalhes devem ser escritos **descrição** ou um comentário anexado.                                                                                                              |
|  **Descrição**  |   (vazio)    |                                                                                                                                                                        Para obter notas gerais, ou para definir restrições nos valores no atributo.                                                                                                                                                                        |
| **Multiplicidade**  |      1       | **1** -este atributo tem um único valor do tipo especificado.<br /><br /> **entre 0 e 1** -esse atributo pode ter um valor de `null`.<br /><br /> **\\**\* -valor desse atributo é uma coleção de valores.<br /><br /> **1...\\**  \* -valor desse atributo é uma coleção que contém pelo menos um valor.<br /><br /> *n* **...** *m* -valor desse atributo é uma coleção que contenha entre *n* e *m* valores. |
|  **É ordenada**   |    False     |                                                                                                                                                                    Se for true, a coleção de forma uma lista sequencial. Para **multiplicidade** de mais de 1.                                                                                                                                                                     |
|   **É exclusivo**   |    False     |                                                                                                                                                                Não se for true, há nenhum valor duplicado na coleção. Para **multiplicidade** de mais de 1.                                                                                                                                                                |

## <a name="see-also"></a>Consulte também  
 [Diagramas de classe UML: referência](../modeling/uml-class-diagrams-reference.md)   
 [Propriedades de tipos em diagramas de classe UML](../modeling/properties-of-types-on-uml-class-diagrams.md)   
 [Propriedades de operações em diagramas de classe UML](../modeling/properties-of-operations-on-uml-class-diagrams.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)   
 [Diagramas de classe UML: diretrizes](../modeling/uml-class-diagrams-guidelines.md)



