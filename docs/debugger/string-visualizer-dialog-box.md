---
title: Caixa de diálogo do Visualizador de cadeia de caracteres | Microsoft Docs
ms.date: 10/10/2018
ms.custom: seoapril2019
ms.topic: reference
f1_keywords:
- vs.debug.stringviewer
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- string visualizer
- visualizers, string
ms.assetid: 080fd8f1-72b0-461f-8451-3c84d5dc51df
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 982db296fd17fb86b4a139e02a9418eeb507cd91
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62902513"
---
# <a name="string-visualizer-dialog-box"></a>Caixa de diálogo Visualizador da Cadeia de Caracteres

Enquanto você estiver depurando no Visual Studio, você pode exibir cadeias de caracteres com o Visualizador de cadeia de caracteres internas. O Visualizador de cadeia de caracteres mostra as cadeias de caracteres que são muito longos para uma janela de dica ou depurador de dados. Ele pode também ajudar a identificar cadeias de caracteres malformadas.

O Visualizador de cadeia de caracteres inclui o texto sem formatação, XML, HTML e JSON opções. Você também pode abrir visualizadores internos para alguns outros tipos, como [DataSet, DataTable e DataView](../debugger/dataset-visualizer-dialog-box.md) objetos, da **Autos** ou outras janelas do depurador.

> [!NOTE]
> Se você precisar inspecionar elementos XAML ou UI WPF em um visualizador, consulte ou [propriedades de XAML de inspecionar durante a depuração](../debugger/inspect-xaml-properties-while-debugging.md) ou [como usar o Visualizador de árvore do WPF](../debugger/how-to-use-the-wpf-tree-visualizer.md).

Para abrir o Visualizador de cadeia de caracteres, você precisa ser interrompido durante a depuração. Passe o mouse sobre uma variável que possui um texto sem formatação, XML, HTML ou JSON valor de cadeia de caracteres e, em seguida, selecione o ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador").

## <a name="uielement-list"></a>Lista UIElement

**Expressão** campo mostra a variável ou expressão que você está focalizando.

**Valor** campo mostra o valor de cadeia de caracteres. Um espaço em branco **valor** significa que o visualizador escolhido não reconhece a cadeia de caracteres. Por exemplo, o **Visualizador XML** mostra um espaço em branco **valor** para uma cadeia de caracteres de texto sem marcas XML ou uma cadeia de caracteres JSON. Para exibir cadeias de caracteres que o visualizador escolhido não pode reconhecer, escolha o **Visualizador de texto** em vez disso. O **Visualizador de texto** mostra texto sem formatação.

### <a name="json-string-data"></a>Dados de cadeia de caracteres JSON

Uma cadeia de caracteres JSON bem formada é semelhante à ilustração a seguir no visualizador JSON. JSON malformado pode exibir um ícone de erro (ou em branco, se não reconhecido). Para identificar o erro JSON, copie e cole a cadeia de caracteres em uma ferramenta de linting JSON como [JSLint](https://www.jslint.com/).

![Visualizador de cadeia de caracteres JSON](../debugger/media/dbg-tips-string-visualizer-json.png "Visualizador de cadeia de caracteres JSON")

### <a name="xml-string-data"></a>Dados de cadeia de caracteres XML

Uma cadeia de caracteres XML bem formada é semelhante à ilustração a seguir no Visualizador XML. XML mal formado pode exibir sem marcas XML ou em branco se não reconhecido.

![Visualizador de cadeia de caracteres XML](../debugger/media/dbg-string-visualizers-xml.png "Visualizador de cadeia de caracteres XML")

### <a name="html-string-data"></a>Dados de cadeia de caracteres HTML

Uma cadeia de caracteres HTML bem formada aparece como se renderizado em um navegador, conforme mostrado na ilustração a seguir. HTML malformado pode exibir como texto sem formatação.

![Visualizador de cadeia de caracteres HTML](../debugger/media/dbg-string-visualizers-html.png "Visualizador de cadeia de caracteres de HTML")

## <a name="see-also"></a>Consulte também

- [Criar visualizadores personalizados (c#, Visual Basic)](../debugger/create-custom-visualizers-of-data.md)
- [Visualizações de dados no Visual Studio para Mac](/visualstudio/mac/data-visualizations)