---
title: Opções, Editor de Texto, C#, IntelliSense
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Intellisense
helpviewer_keywords:
- underlines, wavy
- IntelliSense [C#], options
- IntelliSense [C#], wavy underlines
- wavy underlines
- Text Editor Options dialog box, IntelliSense
ms.assetid: 3466dedb-e5f4-424c-8dd8-e4941b2f4fc2
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 041b3c5d0a67d590bc409c21dd53d5d162b0a0b9
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389241"
---
# <a name="options-text-editor-c-intellisense"></a>Opções, Editor de Texto, C#, IntelliSense

Use a página de opções **IntelliSense** para modificar as configurações que afetam o comportamento do IntelliSense para C#. Para acessar essa página de opções, escolha **Ferramentas** > **Opções** e, em seguida, **Editor de Texto** > **C#** > **IntelliSense**.

As opções do **IntelliSense** contém as seguintes seções:

## <a name="completion-lists"></a>Listas de Conclusão

- Mostrar lista de conclusão depois que um caractere for digitado*

   Quando essa opção estiver selecionada, o IntelliSense exibirá automaticamente a lista de preenchimento quando você começar a digitar. Quando essa opção não estiver selecionada, o preenchimento do IntelliSense ainda estará disponível no menu **IntelliSense** ou pressionando **Ctrl**+**Espaço**.

- Mostrar lista de conclusão depois que um caractere for excluído

- Realçar partes correspondentes de itens da lista de conclusão

- Mostrar itens de filtro de conclusão

## <a name="snippets-behavior"></a>Comportamento de snippets

- Nunca incluir snippets

   Quando essa opção estiver selecionada, o IntelliSense nunca adicionará aliases de snippets de código C# à lista de conclusão.

- Sempre incluir snippets

   Quando essa opção estiver selecionada, o IntelliSense adicionará aliases de snippets de código C# à lista de preenchimento. Caso o alias do snippet de código seja igual a uma palavra-chave, por exemplo, [classe](/dotnet/csharp/language-reference/keywords/class), a palavra-chave será substituída pelo atalho. Para saber mais, consulte [Snippets de código C#](../../ide/visual-csharp-code-snippets.md).

- Incluir snippets quando ?-Tab for digitado após um identificador

   Quando essa opção estiver selecionada, o IntelliSense adicionará aliases de snippets de código C# à lista de conclusão quando **?**+**Tab** for pressionado após um identificador

## <a name="enter-key-behavior"></a>Comportamento da tecla Enter

- Nunca adicionar uma nova linha ao pressionar Enter

   Especifica que uma nova linha nunca será adicionada automaticamente depois de selecionar um item na lista de conclusão e pressionar **Enter**.

- Apenas adicionar uma nova linha ao pressionar Enter após o final de uma palavra totalmente digitada

   Especifica que, se você digitar todos os caracteres de uma entrada na lista de conclusão e, em seguida, pressionar **Enter**, uma nova linha será adicionada automaticamente e o cursor será movido para a nova linha.

   Por exemplo, se você digitar `else` e, em seguida, pressionar **Enter**, o seguinte será exibido no editor:

   `else`

   `|` (local do cursor)

   No entanto, se você digitar apenas `el` e, em seguida, pressionar **Enter**, o seguinte será exibido no editor:

   `else|` (local do cursor)

- Sempre adicionar uma nova linha ao pressionar Enter

   Especifica que, se você digitar *qualquer* um dos caracteres de uma entrada na lista de conclusão e depois pressionar **Enter**, uma nova linha será adicionada automaticamente e o cursor passará para a nova linha.

## <a name="show-name-suggestions"></a>Mostrar sugestões de nome

Executa a conclusão automática do nome de objeto dos membros que você selecionou recentemente.

## <a name="see-also"></a>Consulte também

- [Caixa de diálogo Geral, Ambiente, Opções](../../ide/reference/general-environment-options-dialog-box.md)
- [Usando o IntelliSense](../../ide/using-intellisense.md)