---
title: Opções, Editor de Texto, XAML, Formatação | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.XAML.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.XAML.Miscellaneous
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
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 537223aab878aee2fb00e9417d0415f0a17d2dd5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534128"
---
# <a name="options-text-editor-xaml-formatting"></a>Opções, Editor de Texto, XAML, Formatação
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Use a página de propriedades **Formatação** para especificar como elementos e atributos são formatados nos documentos XAML. Para abrir a caixa de diálogo **Opções**, clique no menu **Ferramentas** e clique em **Opções**. Para acessar a página de propriedades de **Formatação**, expanda o nó **Editor de Texto**, **XAML**, **Formatação**.

> [!NOTE]
> As caixas de diálogo e os comandos de menu encontrados podem diferir daqueles descritos na Ajuda, dependendo das configurações ativas ou edição. Para alterar suas configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas** . Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3).

## <a name="auto-formatting-events"></a>Eventos de Formatação Automática
Formatação automática pode ocorrer quando qualquer um dos eventos a seguir é detectado.

- Preenchimento de uma marcação de fim ou de uma marcação simples.

- Preenchimento de uma marcação de início.

- Colando da área de transferência.

- Comandos de teclado de formatação.

  Você pode especificar os eventos que causam formatação automática.

|Nome|Descrição|
|-|-|
|**Ao preencher a marcação de fim ou der marca simples**|Formatação automática ocorre quando você termina de digitar uma marcação de fim ou uma marcação simples. Uma marcação simples não tem atributos, por exemplo `<Button />`.|
|**Ao preencher uma marcação de início**|Formatação automática ocorre quando você termina de digitar uma marcação de início.|
|**Ao colar da área de transferência**|Formatação automática ocorre quando você cola XAML da área de transferência para a exibição XAML.|

## <a name="quotation-mark-style"></a>Estilo de Aspas
Essa configuração indica se os valores de atributo são colocados entre aspas simples ou duplas. O formatador automático e o preenchimento automático IntelliSense usam essa configuração.

Ao definir essa opção, apenas atributos subsequentemente adicionados usando o designer ou manualmente na exibição XAML são afetados.

|Nome|Descrição|
|-|-|
|**Aspas duplas (")**|Valores de atributos são colocados entre aspas duplas.<br /><br /> `<Button Name="button1">Hello</Button>`|
|**Aspas simples (')**|Valores de atributos são colocados entre aspas simples.<br /><br /> `<Button Name='button1'>Hello</Button>`|

## <a name="tag-wrapping"></a>Automática de marca
Você pode especificar um comprimento de linha para disposição de marcação. Quando a disposição de marcação está habilitada, qualquer XAML adicionado posteriormente usando o designer será disposto adequadamente.

|Nome|Descrição|
|-|-|
|**Encapsular marcações que excedam o comprimento especificado**|Especifica se as linhas são dispostas no comprimento de linha especificado por **Comprimento**.|
|**Comprimento**|O número de caracteres que uma linha pode conter. Se necessário, algumas linhas XAML poderão exceder o comprimento de linha especificado.|

## <a name="attribute-spacing"></a>Espaçamento de Atributos
Use essa configuração para controlar como os atributos são organizados no documento XAML

|Nome|Descrição|
|-|-|
|**Preservar novas linhas e espaços entre atributos**|Novas linhas e espaços entre atributos não são afetados por formatação automática.<br /><br /> `<Button Height="23" Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**Inserir um espaço único entre os atributos**|Atributos ocupam uma linha, com um espaço separando atributos adjacentes. Configurações de disposição de marcação são aplicadas.<br /><br /> `<Button Height="23" Name="button1" Width="75">Hello</Button>`|
|**Posicionar cada atributo em uma linha separada**|Cada atributo ocupa sua própria linha. Isso é útil quando existem muitos atributos.<br /><br /> `<Button`<br /><br /> `Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|
|**Posicionar primeiro atributo na mesma linha que a marcação de início**|Quando essa opção está marcada, o primeiro atributo aparece na mesma linha que a marcação de início do elemento.<br /><br /> `<Button Height="23"`<br /><br /> `Name="button1"`<br /><br /> `Width="75">Hello</Button>`|

## <a name="element-spacing"></a>Espaçamento de Elementos
Use essa configuração para controlar como os elementos são organizados no documento XAML

|                                                               |                                                                                                                                                                                       |
|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Preservar novas linhas no conteúdo**                             | Linhas vazias no conteúdo do elemento não são removidas.<br /><br /> `<Grid>`<br /><br /><br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>\`   |
| **Recolher várias linhas vazias no conteúdo para uma linha única** | Linhas vazias no conteúdo do elemento são recolhidas em uma única linha.<br /><br /> `<Grid>`<br /><br /><br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /><br /><br /> `</Grid>` |
| **Remover linhas vazias no conteúdo**                             | Todas as linhas vazias no conteúdo do elemento são removidas.<br /><br /> `<Grid>`<br /><br /> `<Button Name="button1">Hello</Button>`<br /><br /> `</Grid>`                                        |

## <a name="auto-insert"></a>Inserir automaticamente
Use essa configuração para controlar quando marcas e aspas são geradas automaticamente.

|Nome|Descrição|
|-|-|
|**Marcas de fechamento**|Especifica se a marcação de fechamento de um elemento é gerada automaticamente ao você fechar a marcação de abertura com o caractere de maior que (>).|
|**Citações de atributo**|Especifica se as aspas de fechamento são geradas quando um valor de atributo é selecionado na lista suspensa de preenchimento de declaração.|
|**Chaves de fechamento para MarkupExtensions**|Especifica se uma chave de fechamento (}) de uma extensão de marcação é gerada automaticamente ao digitar o caractere de chave de abertura ({).|
|**Vírgulas para separar parâmetros MarkupExtension**|Especifica se vírgulas são geradas quando você digita mais de um parâmetro em uma extensão de marcação.|

## <a name="default-view"></a>Exibição padrão
Use essa configuração para controlar se o modo de exibição de Design aparece quando documentos XAML são carregados.

|Nome|Descrição|
|-|-|
|**Sempre abrir documentos na exibição XAML completa**|Especifica se os documentos XAML aparecem apenas no modo de exibição XAML, sem modo de exibição de Design. Útil para carregar documentos grandes.|

## <a name="toolbox"></a>Caixa de Ferramentas
Use essa configuração para especificar se controles de usuário e controles personalizados são mostrados na caixa de ferramentas.

|Nome|Descrição|
|-|-|
|**Popular automaticamente os itens da caixa de ferramentas**|Especifica se os controles de usuário e os controles personalizados na solução atual são mostrados automaticamente na caixa de ferramentas.|

## <a name="see-also"></a>Consulte Também
[XAML no WPF](https://msdn.microsoft.com/library/5d858575-a83b-42df-ad3f-047ed2d6e3c8) 
 [Como alterar as configurações](https://msdn.microsoft.com/aee87c79-ca01-4f84-8fb7-a9e47048ee47) 
 de exibição XAML [Instruções XAML e código](https://msdn.microsoft.com/b3ff41a0-a2a3-4f61-b698-ac88ec8f799c)
