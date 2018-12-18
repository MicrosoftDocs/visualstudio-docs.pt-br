---
title: Página de Opções, Fontes e Cores, Propriedades de Nó
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Tools Options settings, Fonts and Colors node properties
- automation [Visual Studio], controlling Tools Options
ms.assetid: 8e1ab784-5f85-4e2b-8ef9-e5d59ca4dbcb
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 94a253d6e723cfa810ada9a7384fe1cda0826ac4
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672256"
---
# <a name="options-page-fonts-and-colors-node-properties"></a>Página de Opções, Fontes e Cores, Propriedades de Nó
Este documento descreve as propriedades de fonte e de cor de uma janela de ferramentas registrada para ser exibida em **Fontes e Cores** na categoria **Ambiente** da caixa de diálogo **Opções**. Isso dá suporte à natureza dinâmica de grupos de itens de coloração, que poderão ser alterados se os VSPackages forem instalados ou desinstalados.

 A seção a seguir mostra um exemplo de um tipo de janela registrada e as propriedades disponíveis para cada janela.

## <a name="text-editor-or-printer-or-dialogs-and-tool-windows"></a>Editor de Texto, impressora ou caixas de diálogo e janelas de ferramentas
 `DTE.Properties("FontsAndColors", "TextEditor")`

 -ou-

 `DTE.Properties("FontsAndColors", "Printer")`

 -ou-

 `DTE.Properties("FontsAndColors", "Dialogs and Tool Windows")`

|Nome do item de propriedade|Valor|Descrição|
| - |-----------|-----------------|
|FontFamily|Get/Set (Cadeia de Caracteres)|O nome da fonte a ser usado, como “Courier New”.|
|FontCharacterSet|Get/Set (<xref:EnvDTE.vsFontCharSet>)|Um valor de <xref:EnvDTE.vsFontCharSet>, especificando o tipo de conjunto de caracteres a ser usado, como hebraico ou russo.|
|FontSize|Get/Set (Curto)|O tamanho da fonte a ser usado, em pontos. Por exemplo, 10 ou 12.|

## <a name="see-also"></a>Consulte também

- [Controlando as configurações de opções](https://msdn.microsoft.com/Library/a09ed242-7494-4cde-bbd1-7a8ec617965d)
- [Determinando os nomes dos itens de propriedade nas páginas de opções](https://msdn.microsoft.com/Library/d450422d-47c7-4eeb-9f9f-3286264bc5aa)
- [Página de Opções, Propriedades do Nó de Ambiente](../../ide/reference/options-page-environment-node-properties.md)
- [Página de Opções, Propriedades do Nó de Editor de Texto](../../ide/reference/options-page-text-editor-node-properties.md)