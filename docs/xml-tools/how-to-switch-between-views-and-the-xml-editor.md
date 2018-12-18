---
title: 'Como: Alternar entre modos de exibição e o editor XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: cb69fbbd-d99c-439e-9498-5df9050f8df0
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0b0eb90f2ead313ce94d609d71385b595f3e964b
ms.sourcegitcommit: d1824ab926ebbc4a8057163e0edeaf35cec57433
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34477724"
---
# <a name="how-to-switch-between-views-and-the-xml-editor"></a>Como: alternar entre modos de exibição e o Editor de XML

Este tópico mostra como alternar entre os modos de exibição do designer de esquema XML (XSD) designer e o editor XML. Este exemplo usa o [esquema de ordem de compra](../xml-tools/sample-xsd-file-simple-schema.md).

## <a name="to-switch-between-the-views-and-the-xml-editor"></a>Para alternar entre modos de exibição e o editor XML

1.  Para criar e editar um novo arquivo de esquema XML, siga as etapas em [como: criar e editar um arquivo de esquema XSD](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md).

2.  Para alternar para o Designer de esquema XML no Editor de XML, clique em qualquer lugar no Editor de XML e selecione **Designer de exibição**.

3.  Para alternar para o modo de exibição do gráfico usando a marca d'água, clique o **usar o modo de exibição de gráfico para ver a relação entre os nós** link no modo de exibição de iniciar.

4.  Arraste o `USAddress` nó do **XML Schema Explorer** para o modo de exibição de gráfico. Clique com botão direito do `USAddress` nó no modo de exibição de gráfico e selecione **Mostrar na exibição do modelo de conteúdo** no menu de contexto.

     A exibição do modelo de conteúdo com os detalhes de nó de `USAddress` aparece.

5.  Para alternar para a exibição início da exibição do modelo de conteúdo usando a barra de ferramentas, clique o **exibição início** na barra de ferramentas XSD.

6.  Para alternar entre os modos de exibição usando as teclas de atalho, pressione **Ctrl**+**1** para a exibição de início, **Ctrl**+**2** para o modo de exibição do gráfico e **Ctrl**+**3** para o modo de exibição do modelo de conteúdo.

7.  Para ir para o Editor de XML da exibição do conteúdo do modelo, clique com botão direito no nó e selecione **Exibir código** no menu de contexto.