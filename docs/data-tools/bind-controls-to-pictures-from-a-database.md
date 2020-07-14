---
title: Associar controles a imagens de um banco de dados
ms.date: 11/04/2016
ms.topic: how-to
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
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e9093c2a2d7cec95e4fdd08ff4273ae8f8126a36
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282978"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>Associar controles a imagens de um banco de dados

Você pode usar a janela **Data Sources** para associar uma imagem em um banco de dados a um controle em seu aplicativo. Por exemplo, você pode associar uma imagem a um <xref:System.Windows.Controls.Image> controle em um aplicativo WPF ou a um <xref:System.Windows.Forms.PictureBox> controle em um aplicativo Windows Forms.

As imagens em um banco de dados normalmente são armazenadas como matrizes de bytes. Os itens na janela **fontes de dados** que são armazenados como matrizes de bytes têm seu tipo de controle definido como **nenhum** por padrão, pois as matrizes de bytes podem conter qualquer coisa de uma matriz simples de bytes para o arquivo executável de um aplicativo grande. Para criar um controle de associação de dados para um item de matriz de bytes na janela **fontes de dados** que representa uma imagem, você deve selecionar o controle a ser criado.

O procedimento a seguir pressupõe que a janela de **fontes de dados** já esteja preenchida com um item associado à sua imagem.

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>Para associar uma imagem em um banco de dados a um controle

1. Verifique se a superfície de design à qual você deseja adicionar o controle está aberta no designer do WPF ou na Designer de Formulários do Windows.

2. Na janela **fontes de dados** , expanda a tabela ou o objeto desejado para exibir suas colunas ou propriedades.

   > [!TIP]
   > Se a janela **fontes de dados** não estiver aberta, abra-a selecionando **Exibir**  >  **outras**  >  **fontes de dados**do Windows.

3. Selecione a coluna ou propriedade que contém os dados da imagem e selecione um dos seguintes controles na lista suspensa controle:

    - Se o designer do WPF estiver aberto, selecione **imagem**.

    - Se o designer de Windows Forms estiver aberto, selecione **PictureBox**.

    - Como alternativa, você pode selecionar um controle diferente que dá suporte à vinculação de dados e que pode exibir imagens. Se o controle que você deseja usar não estiver na lista de controles disponíveis, você poderá adicioná-lo à lista e, em seguida, selecioná-lo. Para obter mais informações, consulte [Adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).

## <a name="see-also"></a>Veja também

- [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
