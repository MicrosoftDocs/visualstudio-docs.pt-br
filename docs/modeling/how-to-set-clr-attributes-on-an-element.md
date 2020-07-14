---
title: Como definir atributos CLR em um elemento
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ebda963bf1afa55fa8d7f98774c72a75d242ceef
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532451"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>Como definir atributos CLR em um elemento
Atributos personalizados são atributos especiais que podem ser adicionados a elementos de domínio, formas, conectores e diagramas. Você pode adicionar qualquer atributo que herda da `System.Attribute` classe.

### <a name="to-add-a-custom-attribute"></a>Para adicionar um atributo personalizado

1. No **Gerenciador de DSL**, selecione o elemento ao qual você deseja adicionar um atributo personalizado.

2. Na janela **Propriedades** , ao lado da propriedade **atributos personalizados** , clique no ícone procurar (**...**).

     A caixa de diálogo **Editar atributos** é aberta.

3. Na coluna **nome** , clique **\<add attribute>** e digite o nome do seu atributo. Pressione ENTER.

4. A linha abaixo do nome do atributo mostra parênteses. Nessa linha, digite um tipo de parâmetro para o atributo (por exemplo, `string` ) e pressione Enter.

5. Na coluna **propriedade de nome** , digite um nome apropriado, por exemplo, `MyString` .

6. Clique em **OK**.

     A propriedade **atributos personalizados** agora exibe o atributo no seguinte formato:

     `[`*AttributeName* `(` *ParameterName* `=` *Tipo* de`)]`

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)