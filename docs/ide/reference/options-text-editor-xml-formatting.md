---
title: Opções, Editor de texto, XML, Formatação
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XML.Formatting
ms.assetid: 203e60b2-7b80-4ff4-9fa1-aa9f4374377b
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 652d9ff3b2178089b4ef35838a4181408aef7f09
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388293"
---
# <a name="options-text-editor-xml-formatting"></a>Opções, Editor de texto, XML, Formatação

Use a página de propriedades **Formatação** para especificar como elementos e atributos são formatados nos documentos XML. Para abrir a caixa de diálogo **Opções**, clique no menu **Ferramentas** e clique em **Opções**. Para acessar a página de propriedades **Formatação**, expanda o nó **Editor de texto** > **XML** > **Formatação**.

## <a name="attributes"></a>Atributos

**Preservar formatação manual de atributos**

Não reformate os atributos. Essa é a configuração padrão.

> [!NOTE]
> Se os atributos estão em várias linhas, o editor recua cada linha de atributos para coincidir com o recuo de elemento pai.

**Alinhar cada atributo em uma linha separada**

Alinhe o segundo atributo e os subsequentes verticalmente para coincidir com o recuo do primeiro atributo. O texto a seguir XML é um exemplo de como os atributos seriam alinhados.

```xml
<item id = "123-A"
      name = "hammer"
      price = "9.95">
</item>
```

## <a name="auto-reformat"></a>Reformatação Automática

**Ao colar da área de transferência**

Reformatar o texto XML colado da área de transferência.

**Na conclusão de marca de fim**

Reformatar o elemento quando a marca de fim é concluída.

## <a name="mixed-content"></a>Conteúdo Misto

**Formatar conteúdo misto por padrão.**

Tente reformatar o conteúdo misto, exceto quando o conteúdo é encontrado em um escopo de `xml:space="preserve"`. Essa é a configuração padrão.

Se um elemento contém uma mistura de texto e de marcação, os conteúdos são consideradas conteúdo misturado. Veja a seguir um exemplo de um elemento com conteúdo misto.

```xml
<dir>c:\data\AlphaProject\
  <file readOnly="false">test1.txt</file>
  <file readOnly="false">test2.txt</file>
</dir>
```

## <a name="see-also"></a>Consulte também

- [Como criar documentação XML (Visual Basic)](/dotnet/visual-basic/programming-guide/program-structure/how-to-create-xml-documentation)
- [Geração de código](../code-generation-in-visual-studio.md)