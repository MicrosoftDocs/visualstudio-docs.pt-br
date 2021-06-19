---
title: Como definir atributos CLR em um elemento
description: Saiba como você pode adicionar qualquer atributo que herda da classe System.Attribute.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b11a6bd4a04bdb469cdf5c2fe2d7b78e0c0fe29a
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387327"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>Como definir atributos CLR em um elemento
Atributos personalizados são atributos especiais que podem ser adicionados a elementos de domínio, formas, conectores e diagramas. Você pode adicionar qualquer atributo que herda da `System.Attribute` classe .

### <a name="to-add-a-custom-attribute"></a>Para adicionar um atributo personalizado

1. No **DSL Explorer,** selecione o elemento ao qual você deseja adicionar um atributo personalizado.

2. Na janela **Propriedades,** ao lado da **propriedade Atributos Personalizados,** clique no ícone Procurar (**...**).

     A **caixa de diálogo** Editar Atributos é aberta.

3. Na coluna **Nome** , clique **\<add attribute>** e digite o nome do atributo. Pressione ENTER.

4. A linha sob o nome do atributo mostra parênteses. Nessa linha, digite um tipo de parâmetro para o atributo (por exemplo, `string` ) e pressione ENTER.

5. Na coluna **Propriedade de Nome,** digite um nome apropriado, por exemplo, `MyString` .

6. Clique em **OK**.

     A **propriedade Atributos** Personalizados agora exibe o atributo no seguinte formato:

     `[`*AttributeName* `(` *ParameterName* `=` *Tipo*`)]`

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))