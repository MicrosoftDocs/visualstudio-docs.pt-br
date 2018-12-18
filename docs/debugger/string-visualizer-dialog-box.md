---
title: Exibir cadeias de caracteres em um visualizador de cadeia de caracteres | Microsoft Docs
ms.custom: ''
ms.date: 10/10/2018
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.debug.stringviewer
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- string visualizer
- visualizers, string
ms.assetid: 080fd8f1-72b0-461f-8451-3c84d5dc51df
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: eb447a29ea669dbea3a68312884760f8984cc2de
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388550"
---
# <a name="view-strings-in-a-string-visualizer-in-visual-studio"></a>Cadeias de caracteres de exibição em um visualizador de cadeia de caracteres no Visual Studio

Enquanto você estiver depurando no Visual Studio, você pode exibir cadeias de caracteres com o Visualizador de cadeia de caracteres internas. O Visualizador de cadeia de caracteres mostra as cadeias de caracteres que são muito longos para uma janela de dica ou depurador de dados. Ele pode também ajudar a identificar cadeias de caracteres malformadas.

O Visualizador de cadeia de caracteres inclui o texto sem formatação, XML, HTML e JSON opções. Você também pode abrir os visualizadores para alguns outros tipos, como objetos do WPF, do **automóveis** ou outras janelas do depurador.

## <a name="open-a-string-visualizer"></a>Abrir um visualizador de cadeia de caracteres

Para abrir o Visualizador de cadeia de caracteres, você precisa ser interrompido durante a depuração. Passe o mouse sobre uma variável que possui um texto sem formatação, XML, HTML ou JSON valor de cadeia de caracteres e, em seguida, selecione o ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador").

![Abrir um visualizador de cadeia de caracteres](../debugger/media/dbg-tips-string-visualizers.png "visualizador aberto de cadeia de caracteres")

## <a name="view-string-visualizer-data"></a>Exibir dados do Visualizador de cadeia de caracteres

Na janela do Visualizador de cadeia de caracteres, o **expressão** campo mostra a variável ou expressão que você está passando o mouse sobre, e o **valor** campo mostra o valor de cadeia de caracteres.

Um espaço em branco **valor** significa que o visualizador escolhido não reconhece a cadeia de caracteres. Por exemplo, o **Visualizador XML** mostra um espaço em branco **valor** para uma cadeia de caracteres de texto sem marcas XML ou uma cadeia de caracteres JSON.

Para exibir cadeias de caracteres que o visualizador escolhido não pode reconhecer, escolha o **Visualizador de texto**. O **Visualizador de texto** mostra texto sem formatação.

### <a name="view-json-string-data"></a>Exibir dados de cadeia de caracteres JSON

Uma cadeia de caracteres JSON bem formada é semelhante à ilustração a seguir no visualizador JSON. JSON malformado pode exibir um ícone de erro (ou em branco, se não reconhecido). Para identificar o erro JSON, copie e cole a cadeia de caracteres em uma ferramenta de linting JSON como [JSLint](https://www.jslint.com/).

![Visualizador de cadeia de caracteres JSON](../debugger/media/dbg-tips-string-visualizer-json.png "Visualizador de cadeia de caracteres JSON")

### <a name="view-xml-string-data"></a>Exibir dados de cadeia de caracteres XML

Uma cadeia de caracteres XML bem formada é semelhante à ilustração a seguir no Visualizador XML. XML mal formado pode exibir sem marcas XML ou em branco se não reconhecido.

![Visualizador de cadeia de caracteres XML](../debugger/media/dbg-string-visualizers-xml.png "Visualizador de cadeia de caracteres XML")

### <a name="view-html-string-data"></a>Dados de cadeia de caracteres de exibição HTML

Uma cadeia de caracteres HTML bem formada aparece como se renderizado em um navegador, conforme mostrado na ilustração a seguir. HTML malformado pode exibir como texto sem formatação.

![Visualizador de cadeia de caracteres HTML](../debugger/media/dbg-string-visualizers-html.png "Visualizador de cadeia de caracteres de HTML")

## <a name="see-also"></a>Consulte também

- [Criar visualizadores personalizados (C#, Visual Basic)](../debugger/create-custom-visualizers-of-data.md)
- [Visualizações de dados no Visual Studio para Mac](/visualstudio/mac/data-visualizations)