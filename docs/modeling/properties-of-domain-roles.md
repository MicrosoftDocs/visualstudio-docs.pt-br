---
title: Propriedades de funções de domínio
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6c1c62126d65107bb25e3c4a475a794116c47193
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544138"
---
# <a name="properties-of-domain-roles"></a>Propriedades de funções de domínio
As propriedades na tabela a seguir são associadas a uma função de domínio. Para obter informações sobre funções de domínio, consulte [noções básicas sobre modelos, classes e relações](../modeling/understanding-models-classes-and-relationships.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalizando e estendendo uma linguagem específica de domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

|Propriedade|Descrição|Padrão|
|-|-|-|
|Tipo de coleção|Se essa função tiver multiplicidade de 0.. * ou 1.. \* , essa propriedade personalizará o tipo genérico que é usado para armazenar a coleção de links.|`(none)` - <xref:Microsoft.VisualStudio.Modeling.LinkedElementCollection%601>é usado|
|Atributos personalizados|Os atributos que você especificar aqui serão adicionados como atributos à classe de código gerada.|<nenhum\>|
|É propriedade navegável|Se `True` e se a multiplicidade da relação for 0.. 1 ou 1.. 1, a propriedade Role poderá ser procurada pelo usuário na janela **Propriedades** . A propriedade exibe o nome do elemento na outra extremidade do link de relacionamento.|`True`|
|É gerador de propriedade|Se `True` , uma propriedade de função é gerada para essa função, que você pode usar para atravessar a relação no código do programa. Se você definir esse falso, poderá percorrer a relação de maneira menos eficiente usando métodos estáticos da relação de domínio.|`True`|
|Modificador de acesso getter de propriedade|O modificador de acesso para o getter da propriedade gerada (,,, `public` `internal` `private` `protected` ou `protected internal` ).|`public`|
|Modificador de acesso setter de propriedade|O modificador de acesso para o setter da propriedade gerada (,,, `public` `internal` `private` `protected` ou `protected internal` ).|`public`|
|Multiplicidade|O número de elementos de modelo que podem reproduzir a função oposta ( `0..1` , `1..1` , `0..*` ou `1..*` ). Se a multiplicidade for `0..*` ou `1..*` , a propriedade gerada representará uma coleção; caso contrário, a propriedade gerada representará um único elemento de modelo.|Depende do tipo de relação e se esta é a função de origem ou de destino na relação.|
|Name|O nome da função de domínio. Esta propriedade não pode conter espaço em branco.|O nome da classe de domínio do representante da função para essa função.|
|Propaga a cópia|`DoNotPropagateCopy`-O representante da função copiado não terá nenhuma cópia desse link.<br /><br /> `PropagateCopyToLinkOnly`-O link copiado aponta para o representante de função oposto existente.<br /><br /> `PropagateCopyToLinkAndOppositeRolePlayer`-O link copiado aponta para uma cópia do representante da função oposto.|`PropagateCopyToLinkAndOppositeRolePlayer`para as funções de origem das incorporações.<br /><br /> `DoNotPropagateCopy`para outras funções.<br /><br /> Para obter mais informações, consulte [Personalizando o comportamento de cópia](../modeling/customizing-copy-behavior.md)|
|Propaga a exclusão|`True`para excluir o elemento que reproduz essa função quando o link associado é excluído.|`True`para o destino de uma função de incorporação.<br /><br /> `False`para outras funções.|
|Nome da propriedade|O nome da propriedade gerada no código do representante da função. Este nome não pode conter espaço em branco.|O nome da função oposta se essa função tiver uma multiplicidade zero-para-um ou um-para-um; caso contrário, o nome plural da função oposta.|
|Representante da função|A classe de domínio do elemento que pode reproduzir essa função na relação. Essa propriedade é somente leitura.|A classe de domínio do representante da função para essa função.|
|Observações|Observações informais que estão associadas à função de domínio.|<nenhum\>|
|Categoria|A categoria sob a qual a propriedade gerada aparece na janela **Propriedades** no designer gerado. Se essa propriedade estiver vazia, a propriedade gerada aparecerá sob a categoria **Miscelânea**|<nenhum\>|
|Descrição|A descrição usada para documentar o código e é usada na interface do usuário do designer gerado.<br /><br /> A descrição é exibida na dica de ferramenta do IntelliSense para a propriedade gerada na classe de representante da função.|`Description for`*o nome completo da função*|
|Nome de exibição|O nome que é exibido no designer gerado para a função de domínio.|O valor ajustado da propriedade Name.|
|Palavra-chave de ajuda|A palavra-chave opcional que é usada para indexar a ajuda F1 para a função de domínio.|\<none>|
|Nome de exibição da propriedade|O nome que é exibido no designer gerado para a propriedade de função gerada.|O valor ajustado da propriedade nome da propriedade.|

> [!NOTE]
> O valor padrão de um nome de exibição é baseado no valor da propriedade associada inserindo espaços antes de cada caractere maiúsculo que é precedido por um caractere minúsculo e que não é seguido por outro caractere em maiúsculas.

## <a name="see-also"></a>Consulte também

- [Propriedades de relacionamentos de domínios](../modeling/properties-of-domain-relationships.md)