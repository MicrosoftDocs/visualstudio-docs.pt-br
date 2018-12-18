---
title: Associar controles a imagens de um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
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
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: fbaca836cb5b620c596b72bc991e91c1cfc2312c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189495"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>Associar controles a imagens de um banco de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode usar o **fontes de dados** window para vincular uma imagem em um banco de dados a um controle em seu aplicativo. Por exemplo, você pode vincular uma imagem para uma <xref:System.Windows.Controls.Image> de controle em um aplicativo WPF, ou como um <xref:System.Windows.Forms.PictureBox> controle em um aplicativo Windows Forms.  
  
 Imagens em um banco de dados normalmente são armazenadas como matrizes de bytes. Os itens na **fontes de dados** janela que são armazenados como matrizes de bytes têm seu controle tipo definido como **None** por padrão, como matrizes de bytes podem conter qualquer coisa, desde uma simples matriz de bytes para o arquivo executável de um aplicativo grande. Para criar um controle associado a dados para um item de matriz de bytes na **fontes de dados** janela que representa uma imagem, você deve selecionar o controle para criar.  
  
 O procedimento a seguir pressupõe que o **fontes de dados** janela já está preenchida com um item que está associado à sua imagem. Para obter mais informações, consulte [como: conectar a dados em um banco de dados](../data-tools/how-to-connect-to-data-in-a-database.md).  
  
### <a name="to-bind-a-picture-in-a-database-to-a-control"></a>Para vincular uma imagem em um banco de dados a um controle  
  
1.  Certifique-se de que a superfície de design que você deseja adicionar o controle é aberta no Designer do WPF ou o Designer de formulários do Windows.  
  
2.  No **fontes de dados** janela, expanda a tabela desejada ou para exibir suas colunas ou propriedades do objeto.  
  
3.  Selecione a coluna ou propriedade que contém os dados de imagem e selecione um dos seguintes controles na sua lista de controle de lista suspensa:  
  
    -   Se o WPF designer estiver aberto, selecione **imagem**.  
  
    -   Se o designer de formulários do Windows é aberto, selecione **PictureBox**.  
  
    -   Como alternativa, você pode selecionar um controle diferente, que dá suporte à vinculação de dados e que pode exibir imagens. Se o controle que você deseja usar não estiver na lista de controles disponíveis, você pode adicioná-lo à lista e, em seguida, selecioná-lo. Para obter mais informações, consulte [adicionar controles personalizados à janela fontes de dados](../data-tools/add-custom-controls-to-the-data-sources-window.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)

