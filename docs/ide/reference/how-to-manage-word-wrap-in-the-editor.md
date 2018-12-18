---
title: Quebra automática de linha
ms.date: 11/07/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
ms.assetid: 442f33ef-9f52-4515-b55f-fb816d664645
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6fc38d1ee5a8e5543675700c35cc0cb298aefad9
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349108"
---
# <a name="how-to-manage-word-wrap-in-the-editor"></a>Como gerenciar a quebra automática de linha no editor

É possível definir e desmarcar a opção **Quebra automática de linha**. Quando essa opção for definida, a parte de uma linha longa que se estender além da largura atual da janela Editor de Código será exibida na próxima linha. Quando essa opção estiver desmarcada, por exemplo, para facilitar o uso de numeração de linha, será possível rolar para a direita para ver os finais das linhas longas.

> [!NOTE]
> Este tópico aplica-se apenas ao Visual Studio no Windows. Atualmente, o Visual Studio para Mac não dá suporte para a quebra automática de linha.

## <a name="to-set-word-wrap-preferences"></a>Para definir preferências de quebra automática de linha

1.  No menu **Ferramentas**, selecione **Opções**.

2.  Na pasta **Editor de Texto**, escolha as opções **Gerais** na subpasta **Todas as Linguagens** para definir essa opção globalmente.

     – ou —

     Escolha as opções **Gerais** na subpasta da linguagem na qual você está programando.

3.  Em **Configurações**, marque ou desmarque a opção **Quebra automática de linha**.

     Quando a opção **Quebra automática de linha** estiver selecionada, a opção **Mostrar glifos visuais para quebra automática de linha** será habilitada.

4.  Selecione a opção **Mostrar glifos visuais para quebra automática de linha** caso prefira exibir um indicador de seta de retorno em que uma linha longa é quebrada em uma segunda linha. Desmarque esta opção se você preferir não exibir setas indicadoras.

    > [!NOTE]
    > Essas setas de lembrete não são adicionadas ao código, elas são apenas para exibição.

## <a name="known-issues"></a>Problemas conhecidos

Se você estiver familiarizado com a quebra automática de linha no Notepad++, Sublime Text, ou Visual Studio Code, fique ciente dos seguintes problemas em que o Visual Studio tem um comportamento diferente dos outros editores:

* [O clique triplo não seleciona a linha inteira](https://developercommunity.visualstudio.com/content/problem/268989/triple-click-doesnt-select-whole-line-when-word-wr.html)
* [O comando Recortar não exclui a linha inteira](https://developercommunity.visualstudio.com/content/problem/138259/cut-command-should-delete-logical-line.html)
* [A tecla End pressionada duas vezes não move o cursor para o fim da linha](https://developercommunity.visualstudio.com/content/problem/138274/pressing-end-key-twice-should-move-cursor-to-end-o.html)

## <a name="see-also"></a>Consulte também

- [Personalizando o editor](../../ide/customizing-the-editor.md)
- [Caixa de diálogo Opções do Editor de Texto](../../ide/reference/text-editor-options-dialog-box.md)
- [Recursos do Editor de Códigos](../../ide/writing-code-in-the-code-and-text-editor.md)
