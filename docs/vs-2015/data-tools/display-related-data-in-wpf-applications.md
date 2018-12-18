---
title: Exibir dados relacionados em aplicativos WPF | Microsoft Docs
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
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 3aa80194-0191-474d-9d28-5ec05654b426
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f6c939ee1a64834bd305d0ae744d9ac02e3b4410
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49174132"
---
# <a name="display-related-data-in-wpf-applications"></a>Exibir dados relacionados em aplicativos WPF
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Em alguns aplicativos, você talvez queira trabalhar com dados que vêm de várias tabelas ou entidades que estão relacionadas entre si em uma relação pai-filho. Por exemplo, você talvez queira exibir uma grade que exibe os clientes de um `Customers` tabela. Quando o usuário seleciona um cliente específico, outra grade exibe os pedidos desse cliente de um relacionados `Orders` tabela.  
  
 Você pode criar controles associados a dados que exibem dados relacionados, arrastando itens dos **fontes de dados** janela para o WPF Designer.  
  
## <a name="to-create-controls-that-display-related-records"></a>Para criar controles que exibem registros relacionados  
  
1.  Sobre o **dados** menu, clique em **Mostrar fontes de dados** para abrir o **fontes de dados** janela.  
  
2.  Clique em **Add New Data Source**e conclua a **configuração de fonte de dados** assistente.  
  
3.  Abra o designer WPF e certifique-se de que o designer contém um contêiner que é um destino de soltar válido para os itens na **fontes de dados** janela.  
  
     Para obter mais informações sobre destinos depósitos válidos, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
4.  No **fontes de dados** janela, expanda o nó que representa a tabela pai ou de objeto na relação. A tabela pai ou o objeto está no lado "um" de uma relação um-para-muitos.  
  
5.  Arraste o nó pai (ou todos os itens individuais no nó pai) a **fontes de dados** window para um destino de soltar válido no designer.  
  
     O Visual Studio gera XAML que cria novos controles de associação de dados para cada item que você arrasta. O XAML também adiciona um novo <xref:System.Windows.Data.CollectionViewSource> para a tabela pai ou o objeto para os recursos de destino de soltar. Para algumas fontes de dados, o Visual Studio também gera código para carregar os dados na tabela pai ou do objeto. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
6.  No **fontes de dados** janela, localize a tabela filho relacionada ou o objeto. Tabelas filho relacionados e os objetos aparecem como nós expansíveis na parte inferior da lista do nó pai de dados.  
  
7.  Arraste o nó filho (ou todos os itens individuais no nó filho) a **fontes de dados** window para um destino de soltar válido no designer.  
  
     O Visual Studio gera XAML que cria novos controles de associação de dados para cada um dos itens que você arrasta. O XAML também adiciona um novo <xref:System.Windows.Data.CollectionViewSource> para a tabela filho ou o objeto para os recursos de destino de soltar. Esse novo <xref:System.Windows.Data.CollectionViewSource> está associado à propriedade da tabela pai ou do objeto que você acabou de arrastar para o designer. Para algumas fontes de dados, o Visual Studio também gera código para carregar os dados na tabela filho ou objeto.  
  
     A figura a seguir demonstra o relacionados **pedidos** tabela da **clientes** tabela em um conjunto de dados no **fontes de dados** janela.  
  
     ![Janela de fontes de dados que mostra a relação](../data-tools/media/datasources2.gif "DataSources2")  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)   
 [Criar tabelas de pesquisa em aplicativos WPF](../data-tools/create-lookup-tables-in-wpf-applications.md)   
 [Passo a passo: exibindo dados relacionados em um aplicativo WPF](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)

