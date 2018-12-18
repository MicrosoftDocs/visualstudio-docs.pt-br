---
title: Propriedades de funções de domínio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5a7bb18c-638e-45e8-9d79-9aa6a9e14b0e
caps.latest.revision: 11
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 51149979544c19b0a887ad77e80a26284051778b
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49244082"
---
# <a name="properties-of-domain-roles"></a>Propriedades de funções de domínio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As propriedades na tabela a seguir estão associadas com uma função de domínio. Para obter informações sobre as funções de domínio, consulte [Noções básicas sobre modelos, Classes e relacionamentos](../modeling/understanding-models-classes-and-relationships.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).  
  
|Propriedade|Descrição|Padrão|  
|--------------|-----------------|-------------|  
|Tipo de coleção|Se essa função tem a multiplicidade 0.. * ou 1... \*, essa propriedade personaliza o tipo genérico que é usado para armazenar a coleção de links.|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601> é usado|  
|Atributos personalizados|Os atributos que você especificar aqui serão adicionados como atributos para a classe do código gerado.|\<Nenhum >|  
|Propriedade é navegável|Se `True`, e se a multiplicidade da relação for entre 0 e 1. 1 ou 1, a propriedade de função pode ser navegada pelo usuário na **propriedades** janela. A propriedade exibe o nome do elemento na outra extremidade do link de relação.|`True`|  
|É o gerador de propriedade|Se `True`, uma propriedade de função é gerada para essa função, o que você pode usar para percorrer a relação no código do programa. Se você definir isso false, você pode percorrer a relação de forma menos eficiente usando métodos estáticos da relação de domínio.|`True`|  
|Modificador de acesso do Getter de propriedade|O modificador de acesso do getter da propriedade gerada (`public`, `internal`, `private`, `protected`, ou `protected internal`).|`public`|  
|Modificador de acesso do Setter de propriedade|O modificador de acesso do setter para a propriedade gerada (`public`, `internal`, `private`, `protected`, ou `protected internal`).|`public`|  
|Multiplicidade|O número de elementos de modelo que pode desempenhar a função oposta (`0..1`, `1..1`, `0..*`, ou `1..*`). Se a multiplicidade for `0..*` ou `1..*`, em seguida, a propriedade gerada representará uma coleção; caso contrário, a propriedade gerada representará um elemento de modelo único.|Depende do tipo de relação e se essa é a função de origem ou destino na relação.|  
|Nome|O nome da função de domínio. Essa propriedade não pode conter espaço em branco.|O nome da classe de domínio do representante da função para essa função.|  
|Propaga cópia|`DoNotPropagateCopy` -O representante da função copiado não terá nenhuma cópia desse link.<br /><br /> `PropagateCopyToLinkOnly` -O link copiado aponta para o existente oposto.<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer` -O link copiado aponta para uma cópia do representante da função oposta.|`PropagateCopyToLinkAndOppositeRolePlayer` para as funções de origem dos objetos incorporados.<br /><br /> `DoNotPropagateCopy` para outras funções.<br /><br /> Para obter mais informações, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)|  
|Propaga a exclusão|`True` Para excluir o elemento que desempenha essa função quando o link associado é excluído.|`True` para o destino de uma função de inserção.<br /><br /> `False` para outras funções.<br /><br /> Para obter mais informações, consulte [Personalizando o comportamento de exclusão](../modeling/customizing-deletion-behavior.md).|  
|Nome da Propriedade|O nome da propriedade gerada no código de representante da função. Esse nome não pode conter espaço em branco.|O nome da função oposta se essa função tem um zero-para-um ou uma-para-um multiplicidade; Caso contrário, o nome pluralizado da função oposta.|  
|Representante da função|A classe de domínio do elemento que pode desempenhar esta função na relação. Esta propriedade é somente para leitura.|A classe de domínio do representante da função para essa função.|  
|Observações|Observações informais que estão associadas com a função de domínio.|\<Nenhum >|  
|Categoria|A categoria na qual a propriedade gerada aparece na **propriedades** janela no designer gerado. Se essa propriedade estiver vazia, a propriedade gerada aparece sob o **Misc** categoria|\<Nenhum >|  
|Descrição|A descrição que é usada para documentar código e é usada na interface do usuário do designer gerado.<br /><br /> A descrição aparece na dica de ferramenta Intellisense para a propriedade gerada na classe de player de função.|`Description for` *o nome completo da função*|  
|Nome de Exibição|O nome que é exibido no designer gerado para a função de domínio.|O valor ajustado da propriedade Name.|  
|Palavra-chave de ajuda|A palavra-chave opcional que é usada para indexar a Ajuda de F1 para a função de domínio.|\<Nenhum >|  
|Nome de exibição de propriedade|O nome que é exibido no designer gerado para a propriedade de função gerado.|O valor ajustado da propriedade nome da propriedade.|  
  
> [!NOTE]
>  O valor padrão de um nome de exibição baseia-se no valor da propriedade associado inserindo espaços antes de cada caractere maiusculo, que é precedido por um caractere em minúscula e que não é seguido por outro caractere maiusculo.  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades de relacionamentos de domínios](../modeling/properties-of-domain-relationships.md)



