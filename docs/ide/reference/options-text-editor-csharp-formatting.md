---
title: Opções de formatação do editor de C#
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Spacing
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.NewLines
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Indentation
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.Wrapping
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting
- VS.ToolsOptionsPages.Text_Editor.CSharp.Formatting.General
- VS.ToolsOptionsPages.Text_Editor.CSharp.Code_Style.Formatting.General
helpviewer_keywords:
- formatting options [C#]
- Text editor Options dialog box, formatting
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 542d14e5913b1537d5e5e6aabb7264cd15add793
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220515"
---
# <a name="options-text-editor-c-code-style-formatting"></a>Opções, Editor de Texto, C#, Estilo de Código, Formatação

Use a página de opções **Formatação** para definir opções para formatar o código no editor de códigos. Para acessar essa página de opções, escolha **Ferramentas** > **Opções**. Na caixa de diálogo **Opções**, escolha **Editor de Texto** > **C#** > **Estilo de Código** > **Formatação**.

## <a name="general-page"></a>Página geral

### <a name="general-settings"></a>Configurações gerais

Essas configurações afetam *quando* o editor de códigos aplica opções de formatação ao código.

|Rotular|Descrição|
|-----------|-----------------|
|**Formatar automaticamente ao digitar**|Quando estiver desmarcada, as opções **formatar instrução em ;** e **formatar bloco em }** estarão desabilitadas.|
|**Formatar instrução automaticamente em ;**|Quando selecionada, formata as instruções na conclusão de acordo com as opções de formatação selecionadas para o editor.|
|**Formatar bloco automaticamente em }**|Quando selecionada, formata blocos de código de acordo com as opções de formatação selecionadas para o editor assim que você conclui o bloco de código.|
|**Formatar automaticamente na devolução**|Quando selecionada, formata o texto quando **Enter** é pressionado, de acordo com as opções de formatação selecionadas para o editor.|
|**Formatar automaticamente ao colar**|Quando selecionada, formata o texto que é colado no editor de acordo com as opções de formatação selecionadas para o editor.|

### <a name="format-document-settings"></a>Configurações de Formatar Documento

Essas configurações definem o comando **Formatar Documento** para executar a limpeza de código adicional em um arquivo. Para obter mais informações sobre como essas configurações são aplicadas, confira [Comando Formatar Documento](../code-styles-and-quick-actions.md#format-document-command).

|Rotular|Descrição|EditorConfig e ferramentas correspondentes > Regras de opções|
|-----------|-----------------|-----------------|-----------------|
|**Aplicar todas as regras de formatação de C# (recuo, quebra automática, espaçamento)**|O comando **Formatar Documento** sempre corrige os problemas de formatação. Essa configuração não pode ser alterada.| [Principais opções do EditorConfig](../../ide/create-portable-custom-editor-options.md)<br/>[Opções de formatação do EditorConfig do .NET](../../ide/editorconfig-code-style-settings-reference.md#formatting-conventions)<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Formatação** > [**Recuo** ou **Novas Linhas** ou **Espaçamento** ou **Quebra automática**]|
|**Executar limpeza de código de adição durante a formatação**|Quando selecionada, aplica correções para as regras especificadas abaixo no comando **Edit.FormatDocument**.| N/D |
|**Remover usings desnecessárias**|Quando selecionada, remove as diretivas `using` desnecessários quando **Edit.FormatDocument** é disparado.| N/D |
|**Classificar usings**|Quando selecionada, classifica as diretivas `using` quando **Edit.FormatDocument** é disparado.| dotnet_sort_system_directives_first<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Avançado** > **Colocar as diretivas 'System' primeiro ao classificar usings** |
|**Adicionar/remover chaves de instruções de controle de única linha**|Quando selecionado, adiciona ou remove as chaves das instruções de controle de única linha quando **Edit.FormatDocument** é disparado.| csharp_prefer_braces<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências do bloco de código** > **Preferir chaves** |
|**Adicionar modificadores de acessibilidade**|Quando selecionada, adiciona os modificadores de acessibilidade ausentes quando **Edit.FormatDocument** é disparado.| dotnet_style_require_accessibility_modifiers |
|**Classificar modificadores de acessibilidade**|Quando selecionada, classifica os modificadores de acessibilidade quando **Edit.FormatDocument** é disparado.| csharp_preferred_modifier_order<br/>visual_basic_preferred_modifier_order |
|**Aplicar preferências de corpo de expressão/bloco**|Quando selecionada, converte os membros no corpo da expressão em corpos de bloco, ou vice-versa, quando **Edit.FormatDocument** é disparado.| [Opções do EditorConfig para membro no corpo da expressão](../../ide/editorconfig-code-style-settings-reference.md#expression_bodied_members)<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de expressão** > **Usar o corpo da expressão para métodos, construtores etc.** |
|**Aplicar preferências de tipo implícitas/explícitas**|Quando selecionada, converte `var` no tipo explícito, ou vice-versa, quando **Edit.FormatDocument** é disparado.| [Opções do EditorConfig para tipo explícito](../../ide/editorconfig-code-style-settings-reference.md#implicit-and-explicit-types)<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de 'var'** |
|**Aplicar preferências de variáveis 'out' embutidas**|Quando selecionada, embute as variáveis `out` onde possível quando **Edit.FormatDocument** é disparado.| csharp_style_inlined_variable_declaration<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de variável** > **Preferir declaração de variável embutida** |
|**Aplicar preferências de tipo de linguagem/estrutura**|Quando selecionada, converte tipos de linguagem em tipos de estrutura, ou vice-versa, quando **Edit.FormatDocument** é disparado.| dotnet_style_predefined_type_for_locals_parameters_members<br/>dotnet_style_predefined_type_for_member_access<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de tipo predefinidas** |
|**Aplicar preferências de inicialização de objeto/coleção**|Quando selecionada, usa os inicializadores de objeto e de coleção sempre que possível quando **Edit.FormatDocument** é disparado.| dotnet_style_object_initializer<br/>dotnet_style_collection_initializer<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de expressão** > **Preferir inicializador de objeto** ou **Preferir inicializador de coleção** |
|**Aplicar preferências de qualificação 'this.'**|Quando marcada, aplica as preferências de `this.` quando **Edit.FormatDocument** é disparado.| [Opções do EditorConfig para a qualificação this.](../../ide/editorconfig-code-style-settings-reference.md#this_and_me)<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de 'this.'** |
|**Tornar campos particulares readonly quando possível**|Quando selecionada, torna os campos particulares `readonly` sempre que possível quando **Edit.FormatDocument** é disparado.| dotnet_style_readonly_field<br/><br/>**Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Estilo de Código** > **Preferências de campo** > **Preferir readonly** |
|**Remover conversões desnecessárias**|Quando selecionada, remove as conversões desnecessárias sempre que possível quando **Edit.FormatDocument** é disparado.| N/D |
|**Remover variáveis não usadas**|Quando selecionada, remove as variáveis que não são usadas quando **Edit.FormatDocument** é disparado.| N/D |

![Configurações de limpeza de código para C# no Visual Studio](media/format-document-settings.png)

## <a name="preview-windows"></a>Janelas de visualização

As subpáginas **Recuo**, **Novas Linhas**, **Espaçamento** e **Quebra Automática** exibem uma janela de visualização na parte inferior. A janela de visualização mostra o efeito de cada opção. Para usar a janela de visualização, selecione uma opção de formatação. A janela de visualização mostra um exemplo da opção selecionada. Quando você altera uma configuração selecionando um botão de opção ou marcando uma caixa de seleção, a janela de visualização é atualizada para mostrar o efeito da nova configuração.

## <a name="indentation-remarks"></a>Comentários de recuo

As opções de recuo nas páginas **Guias** de cada linguagem determinam apenas onde o editor de códigos coloca o cursor quando você pressiona **Enter** no final de uma linha. As opções de recuo em **Formatação** são aplicadas quando o código é formatado automaticamente, por exemplo, quando você cola um código no arquivo e **Formatar automaticamente ao colar** está selecionada e quando o bloco que está sendo formatado é digitado manualmente.

## <a name="see-also"></a>Consulte também

- [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)