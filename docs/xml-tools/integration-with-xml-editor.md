---
title: Integração do Designer de esquema XML com o Editor de XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 43d7a8e6-bd94-4407-a800-15a145c74223
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3ae7595121fcefa36998a88b53aae466d3a726cb
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34573317"
---
# <a name="integration-with-xml-editor"></a>Integração com o editor de XML

O designer de esquema XML está integrado com o editor XML. Se você modificar um arquivo XSD no Editor de XML, a alteração será refletida no [XML Schema Explorer](../xml-tools/xml-schema-explorer.md). Se você tiver o [exibição de gráfico](../xml-tools/graph-view.md) ou [exibição do modelo de conteúdo](../xml-tools/content-model-view.md) aberto, a alteração também será refletida lá. Você pode navegar entre o designer de esquema XML e o editor XML das seguintes maneiras:

-   No Editor de XML, clique em um nó e selecione **Mostrar em XML Schema Explorer**.

-   No modo de exibição de gráfico e o **XML Schema Explorer**, clique duas vezes em um nó, ou um nó e selecione **Exibir código**. Na exibição do modelo de conteúdo, clique em um nó e selecione **Exibir código**.

Captura de tela a seguir mostra um esquema XML aberto no **XML Schema Explorer**. O **XML Schema Explorer** exibe o esquema definido em uma exibição de árvore. O Editor de XML exibe o texto do nó que está ativo no momento o **XML Schema Explorer**.

![XSDDesignerWithXMLEditor](../xml-tools/media/xsddesignerwithxmleditor.gif)

Às vezes é útil consulte o código no editor XML e no designer gráfico lado a lado. Para exibir os dois arquivos ao mesmo tempo, clique em qualquer lugar no Editor de XML e selecione **Designer de exibição**. No menu do Windows do Visual Studio, selecione **novo Horizontal (ou Vertical) grupo de guias**.

![XSDDesignerWithXMLEditorAndCMV](../xml-tools/media/xsddesignerwithxmleditorandcmv.gif)

## <a name="see-also"></a>Consulte também

- [XML Schema Explorer](../xml-tools/xml-schema-explorer.md)