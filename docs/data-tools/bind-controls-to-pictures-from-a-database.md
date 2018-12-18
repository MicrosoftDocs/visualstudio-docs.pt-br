---
title: Associar controles a imagens de um banco de dados
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- images [Visual Basic], displaying on Windows Forms
- data binding [Windows Forms], pictures
- images [Visual Basic], data binding
- pictures, data binding
- pictures, dragging from Data Sources window
- Data Sources Window, setting controls to display images
- PictureBox control [Windows Forms], data binding
- images [Visual Basic], dragging from Data Sources window
ms.assetid: 9748815e-3556-49e8-86b1-c6aa593c6163
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: d93ca95a67bc3816d8d65a799282dc6c7969e093
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304903"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>Associar controles a imagens de um banco de dados

Você pode usar o **fontes de dados** window para vincular uma imagem em um banco de dados a um controle em seu aplicativo. Por exemplo, você pode vincular uma imagem para uma <xref:System.Windows.Controls.Image> de controle em um aplicativo WPF, ou como um <xref:System.Windows.Forms.PictureBox> controle em um aplicativo Windows Forms.

Imagens em um banco de dados normalmente são armazenadas como matrizes de bytes. Os itens na **fontes de dados** janela que são armazenados como matrizes de bytes têm seu controle tipo definido como **None** por padrão, como matrizes de bytes podem conter qualquer coisa, desde uma simples matriz de bytes para o arquivo executável de um aplicativo grande. Para criar um controle associado a dados para um item de matriz de bytes na **fontes de dados** janela que representa uma imagem, você deve selecionar o controle para criar.

O procedimento a seguir pressupõe que o **fontes de dados** janela já está preenchida com um item que está associado à sua imagem.

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>Para vincular uma imagem em um banco de dados a um controle

1.  Certifique-se de que a superfície de design que você deseja adicionar o controle é aberta no Designer do WPF ou o Designer de formulários do Windows.

2.  No **fontes de dados** janela, expanda a tabela desejada ou para exibir suas colunas ou propriedades do objeto.

   > [!TIP]
   > Se o **fontes de dados** janela não estiver aberta, abra-o selecionando **exibição** > **Other Windows** > **fontes de dados**.

3.  Selecione a coluna ou propriedade que contém os dados de imagem e selecione um dos seguintes controles na sua lista de controle de lista suspensa:

    - Se o WPF designer estiver aberto, selecione **imagem**.

    - Se o designer de formulários do Windows é aberto, selecione **PictureBox**.

    - Como alternativa, você pode selecionar um controle diferente, que dá suporte à vinculação de dados e que pode exibir imagens. Se o controle que você deseja usar não estiver na lista de controles disponíveis, você pode adicioná-lo à lista e, em seguida, selecioná-lo. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

## <a name="see-also"></a>Consulte também

- [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)