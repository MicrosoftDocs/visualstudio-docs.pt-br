---
title: Formatação, XML, editor de texto, a caixa de diálogo opções
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: reference
ms.assetid: bb539b3a-027c-4b2f-906e-403e0e22ba8d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5f92ced5ca5ac007969a06cec7f253617ee293e3
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34548785"
---
# <a name="formatting-xml-text-editor-options-dialog-box"></a>Formatação, XML, editor de texto, caixa de diálogo Opções

Esta caixa de diálogo permite que você especifique as configurações de formatação para o editor XML. Você pode acessar o **opções** na caixa de diálogo de **ferramentas** menu.

> [!NOTE]
> Essas configurações estão disponíveis quando você seleciona o **Editor de texto** pasta, o **XML** pasta e, em seguida, o **formatação** opção o **opções** caixa de diálogo.

## <a name="attributes"></a>Atributos
 **Preservar formatação manual de atributos**

 Os atributos não são reformatados. Esse é o padrão.

> [!NOTE]
> Se os atributos estão em várias linhas, o editor recua cada linha de atributos para coincidir com o recuo de elemento pai.

 **Alinhar cada atributo em sua própria linha**

 Alinha os segundos e atributos subsequentes verticalmente para coincidir com o recuo do primeiro atributo. O texto a seguir XML é um exemplo de como os atributos seriam alinhados.

```xml
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>Reformatação automática
 **Ao colar da área de transferência**

 Reformatar o texto XML colado da área de transferência.

 **Após a conclusão da marca de fim**

 Reformatar o elemento quando a marca de fim é concluída.

## <a name="mixed-content"></a>Conteúdo misto
 **Preservar o conteúdo misto por padrão**

 Determina se o editor reformate conteúdo misturado. Por padrão, o editor tenta reformatar conteúdo misturado, a não ser que quando o conteúdo for encontrado em um escopo de `xml:space="preserve"` .

 Se um elemento contém uma mistura de texto e de marcação, os conteúdos são consideradas conteúdo misturado. O código a seguir é um exemplo de um elemento com conteúdo misturado.

```xml
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>Consulte também

- [Propriedades de documento XML, janela de propriedades](../xml-tools/xml-document-properties-properties-window.md)
- [Componentes do Editor de XML](../xml-tools/xml-editor-components.md)