---
title: Opções, Editor de Texto, XAML, Formatação
ms.date: 10/29/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.Spacing
helpviewer_keywords:
- element spacing, XAML view settings
- attribute spacing, XAML view settings
- XAML view settings, auto-formatting events
- auto-formatting events, XAML view settings
- XAML view settings, tag wrapping
- XAML view settings, auto insert
- quotation mark style, XAML view settings
- XAML formatting, WPF Designer
- XAML view settings, Toolbox
- XAML view settings, element spacing
- default view, XAML view settings
- auto insert, XAML view settings
- XAML view settings, default view
- XAML view settings, quotation mark style
- tag wrapping, XAML view settings
- WPF Designer, XAML formatting
- XAML view settings, attribute spacing
ms.assetid: ad3820b1-0d94-4807-a74c-c3467ed973a2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 4686760625062fea7984cdc05386284f8f98c4ee
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388982"
---
# <a name="options-text-editor-xaml-formatting"></a>Opções, Editor de Texto, XAML, Formatação

Use a página de propriedades **Formatação** para especificar como elementos e atributos são formatados nos documentos XAML. Para abrir a caixa de diálogo **Opções**, clique no menu **Ferramentas** e clique em **Opções**. Para acessar a página de propriedades **Formatação**, expanda o nó **Editor de Texto** > **XAML** > **Formatação**.

## <a name="auto-formatting-events"></a>Eventos de Formatação Automática

A formatação automática poderá ocorrer quando qualquer um dos eventos a seguir for detectado.

-   Preenchimento de uma marcação de fim ou de uma marcação simples.

-   Preenchimento de uma marcação de início.

-   Colando da área de transferência.

-   Comandos de teclado de formatação.

É possível especificar quais eventos causam formatação automática.

**Ao preencher a marcação de fim ou der marca simples**

A formatação automática ocorre quando você termina de digitar uma marca de fim ou uma marca simples. Uma marcação simples não tem atributos, por exemplo `<Button />`.

**Ao preencher uma marcação de início**

A formatação automática ocorre quando você termina de digitar uma marca de início.

**Ao colar da área de transferência**

A formatação automática ocorre quando você cola o XAML da área de transferência na exibição XAML.

## <a name="quotation-mark-style"></a>Estilo de Aspas

Essa configuração indica se os valores de atributo são colocados entre aspas simples ou duplas. O formatador automático e o preenchimento automático IntelliSense usam essa configuração.

Ao definir essa opção, apenas atributos subsequentemente adicionados usando o designer ou manualmente na exibição XAML são afetados.

**Aspas duplas (")**

Valores de atributos são colocados entre aspas duplas.
`<Button Name="button1">Hello</Button>`

**Aspas simples (')**

Valores de atributos são colocados entre aspas simples.
`<Button Name='button1'>Hello</Button>`

## <a name="tag-wrapping"></a>Automática de marca

Você pode especificar um comprimento de linha para disposição de marcação. Quando a disposição de marcação está habilitada, qualquer XAML adicionado posteriormente usando o designer será disposto adequadamente.

**Encapsular marcações que excedam o comprimento especificado**

Especifica se as linhas são dispostas no comprimento de linha especificado por **Comprimento**.

**Comprimento**

O número de caracteres que uma linha pode conter. Se necessário, algumas linhas XAML poderão exceder o comprimento de linha especificado.

## <a name="attribute-spacing"></a>Espaçamento de Atributos

Use essa configuração para controlar como os atributos são organizados no documento XAML

**Preservar novas linhas e espaços entre atributos**

Novas linhas e espaços entre atributos não são afetados por formatação automática.

```xml
<Button Height="23"   Name="button1"
Width="75">Hello</Button>
```

**Inserir um espaço único entre os atributos**

Atributos ocupam uma linha, com um espaço separando atributos adjacentes. Configurações de disposição de marcação são aplicadas.

```xml
<Button Height="23" Name="button1" Width="75">Hello</Button>
```

**Posicionar cada atributo em uma linha separada**

Cada atributo ocupa sua própria linha, que é útil quando muitos atributos estão presentes.

```xml
<Button
Height="23"
Name="button1"
Width="75">Hello</Button>
```

**Posicionar primeiro atributo na mesma linha que a marcação de início**

Quando essa opção está marcada, o primeiro atributo aparece na mesma linha que a marcação de início do elemento.

```xml
<Button Height="23"
Name="button1"
Width="75">Hello</Button>
```

## <a name="element-spacing"></a>Espaçamento de Elementos

Use essa configuração para controlar como os elementos são organizados no documento XAML.

**Preservar novas linhas no conteúdo**

Linhas vazias no conteúdo do elemento não são removidas.

```xml
<Grid>


<Button Name="button1">Hello</Button>

</Grid>
```

**Recolher várias linhas vazias no conteúdo para uma linha única**

Linhas vazias no conteúdo do elemento são recolhidas em uma única linha.

```xml
<Grid>

<Button Name="button1">Hello</Button>

</Grid>
```

**Remover linhas vazias no conteúdo**

Todas as linhas vazias no conteúdo do elemento são removidas.

```xml
<Grid>
<Button Name="button1">Hello</Button>
</Grid>
```

## <a name="see-also"></a>Consulte também

- [XAML no WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)