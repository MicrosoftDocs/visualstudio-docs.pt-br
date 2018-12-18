---
title: Seletor de trecho de código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.expansionpicker
helpviewer_keywords:
- Code Snippet Picker
- IntelliSense code snippets, Code Snippet Picker
- code snippets, Code Snippet Picker
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 774ee47f02fe146caade0540be5ee2fb7f59904e
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31944174"
---
# <a name="code-snippet-picker"></a>Seletor de trecho de código

O Editor de Códigos do Visual Studio fornece um **Seletor de Trecho de Código** que permite inserir blocos de código prontos no documento ativo com alguns cliques do mouse.

O procedimento para exibir o **Seletor de Trecho de Código** varia de acordo com a linguagem que você está usando.

- Visual Basic – clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho de Código**.

- C# – clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho de Código** ou **Envolver Com**.

- C++ – o **Seletor de Trecho de Código** não está disponível.

- F # – o **Seletor de Trecho de Código** não está disponível.

- JavaScript – clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho de Código** ou **Envolver Com**.

- XML – Clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho** ou **Envolver com**.

- HTML – Clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho** ou **Envolver com**.

- SQL – Clique com o botão direito do mouse no local desejado no Editor de Códigos para exibir o menu de atalho e selecione **Inserir Trecho**.

Na maioria das linguagens de desenvolvimento do Visual Studio, é possível usar o **Gerenciador de Trechos de Código** para adicionar pastas à lista de pastas que o **Seletor de Trecho de Código** examina em busca de arquivos com trecho XML. Você também pode criar seus próprios trechos para adicionar à lista. Para obter mais informações, consulte [Instruções passo a passo: criando um trecho de código](../../ide/walkthrough-creating-a-code-snippet.md).

## <a name="uielement-list"></a>Lista UIElement

Nome do Item

Um campo de texto editável que exibe o nome do item selecionado na **Lista de Itens**. Para executar uma pesquisa incremental do item que você deseja, comece digitando seu nome neste campo. Continue adicionando letras até que o item desejado seja selecionado na **Lista de Itens**.

Lista de Itens

Uma lista de trechos de código disponíveis para inserção ou uma lista de pastas que contêm trechos de código. Para inserir um trecho ou expandir uma pasta, selecione o item desejado e pressione Enter.

## <a name="see-also"></a>Consulte também

- [Melhores práticas para usar trechos de código](../../ide/best-practices-for-using-code-snippets.md)
- [Trechos de Código do Visual Basic IntelliSense](/dotnet/visual-basic/developing-apps/using-ide/intellisense-code-snippets)
- [Configurando identificadores no código](../../ide/setting-bookmarks-in-code.md)
- [Como usar trechos de código Surround-with](../../ide/how-to-use-surround-with-code-snippets.md)