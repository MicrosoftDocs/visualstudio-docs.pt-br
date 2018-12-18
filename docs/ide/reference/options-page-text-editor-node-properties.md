---
title: Página de Propriedades, Editor de Texto, Propriedades do Nó
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Tools Options settings, Text Editor node properties
- automation [Visual Studio], controlling Tools Options
ms.assetid: 19438302-0677-4f4d-9720-5667e6a22ab2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e16bdece503babe9a50bc83d64da582d390843b6
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50670813"
---
# <a name="options-page-text-editor-node-properties"></a>Página de Propriedades, Editor de Texto, Propriedades do Nó
Este documento descreve algumas páginas (ou coleções de propriedades) associadas à categoria **Editor de Texto**, `DTE.Properties("TextEditor", <Property Page>)`, da caixa de diálogo **Opções**. O título de cada subseção é a chamada que é usada para acessar a coleção `Properties` e a tabela em cada subseção lista as propriedades na coleção.

 As macros do Visual Basic em [Controlando as configurações de opções](https://msdn.microsoft.com/Library/a09ed242-7494-4cde-bbd1-7a8ec617965d) demonstram como exibir as opções atuais e seus valores para cada página da caixa de diálogo **Opções**.

## <a name="general"></a>Geral
 `DTE.Properties("TextEditor", "General")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|GoToAnchorAfterEscape|Get/Set (Booliano)|Se `True`, pressionar escape enquanto houver uma coleção fará com que o ponto de inserção seja movido para onde a ação que criou a seleção foi iniciada. `False` move o ponto de inserção para outra extremidade da seleção.|
|DragNDropTextEditing|Get/Set (Booliano)|Determina se você pode arrastar uma região de texto selecionada de um local para outro no documento para copiar ou recortar/colar operações.|
|HorizontalScrollBar|Get/Set (Booliano)|Determina se há uma barra de rolagem horizontal nas janelas do editor.|
|VerticalScrollBar|Get/Set (Booliano)|Determina se há uma barra de rolagem vertical nas janelas do editor.|
|SelectionMargin|Get/Set (Booliano)|Determina se há espaço à esquerda do painel de texto para operações de seleção especiais, ícones de ponto de interrupção de desenho, etc.|
|MarginIndicatorBar|Get/Set (Booliano)|Determina se há uma linha vertical dividindo a margem esquerda do painel de texto do corpo principal do painel de texto.|
|UndoCaretActions|Get/Set (Booliano)|Se `True`. as operações de desfazer incluem movimentação do ponto de inserção, comandos de seleção, e assim por diante, além da edição de ações que modificam o buffer.|
|AutoDelimiterHighlighting|Get/Set (Booliano)|Determina se digitar um delimitador de fechamento faz com que o editor realce o delimitador de abertura. O editor sempre coloca em negrito o delimitador de abertura, independentemente do valor dessa propriedade.|
|EditorEmulation|Get/Set (Enum)||
|DetectUTF8WithoutSignature|Get/Set (Booliano)|Detecta se um arquivo usa codificação UTF-8 quando ele não tem uma assinatura de codificação.|
|TrackChanges|Get/Set (Booliano)||

## <a name="plain-text"></a>Texto sem formatação
 `DTE.Properties("TextEditor", "PlainText")`

 As opções do editor de `PlainText` afetam as configurações do editor quando os arquivos de texto são editados. Cada linguagem de programação e pacote do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] tem suas próprias configurações específicas do **Editor de Texto**. Por exemplo, para exibir ou alterar as configurações de editor do [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)], use `DTE.Properties("TextEditor", "CSharp") or DTE.Properties("TextEditor", "CSharp-Specific")`. Para as configurações de editor do **SQL Script**, use `DTE.Properties("TextEditor", "SQL ")`.

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|AutoListMembers|Get/Set (Booliano)|Determina se uma lista de membros disponível é exibida automaticamente quando um usuário digita um ponto depois de uma referência de variável.|
|AutoListParams|Get/Set (Booliano)|Determina se uma descrição de uma lista de argumentos é exibida automaticamente quando o usuário digita um "(" depois de um nome de função.|
|HideAdvancedMembers|Get/Set (Booliano)|Determina se o preenchimento de declaração lista todos os membros ou apenas os usados frequentemente.|
|VirtualSpace|Get/Set (Booliano)|Determina se caracteres de espaço em branco são exibidos como gráficos. Definir como `true` faz com que o item de propriedade `WordWrap` (nesta lista) seja definido como `false`.|
|WordWrap|Get/Set (Booliano)|Determina se a exibição quebra linhas longas nos limites da palavra. Definir como `true` faz com que o item de propriedade `VirtualSpace` (nesta lista) seja definido como `false`.|
|WordWrapGlyphs|Get/Set (Booliano)|Exibe um glifo no fim de uma linha; indica que a linha é quebrada para a próxima linha.|
|EnableLeftClickForURLs|Get/Set (Booliano)|Determina se o editor sublinha URLs e permite que com um único clique no botão esquerdo do mouse seja possível pular para a URL no navegador da Web registrado pelo sistema.|
|IndentStyle|Get/Set (<xref:EnvDTE.vsIndentStyle>)|Determina o estilo do recuo: Padrão, Inteligente ou Nenhum.|
|TabSize|Get/Set (Longo)|Representa o número de espaços que é igual a uma tabulação. Definir um inteiro fora do intervalo de 1 a 60 (inclusive) causa falhas.|
|InsertTabs|Get/Set (Booliano)|Se `True`, caracteres de tabulação serão usados no recuo.|
|IndentSize|Get/Set (Longo)|Representa o número de espaços que é igual a um nível de recuo. Definir um valor inteiro fora do intervalo de 1 a 60 (inclusive) causa falhas.|
|ShowLineNumbers|Get/Set (Booliano)|Determina se a exibição de um documento de editor de núcleo exibe números de linha ao longo da margem esquerda.|
|ShowNavigationBar|Get/Set (Booliano)|Determina se as listas suspensas e os botões aparecem na parte superior das janelas do editor.|
|CutCopyBlankLines|Get/Set (Booliano)|Recorta ou copia linhas em branco quando são selecionadas.|

## <a name="see-also"></a>Consulte também

- [Controlando as configurações de opções](https://msdn.microsoft.com/Library/a09ed242-7494-4cde-bbd1-7a8ec617965d)
- [Determinando os nomes dos itens de propriedade nas páginas de opções](https://msdn.microsoft.com/Library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)
- [Página de Opções, Propriedades do Nó de Ambiente](../../ide/reference/options-page-environment-node-properties.md)
- [Página de Opções, Propriedades do Nó de Fontes e Cores](../../ide/reference/options-page-fonts-and-colors-node-properties.md)