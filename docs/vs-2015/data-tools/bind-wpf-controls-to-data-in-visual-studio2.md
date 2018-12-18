---
title: Associar controles WPF a dados no Visual Studio2 | Microsoft Docs
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
ms.assetid: 00dd5147-db0b-4b59-8d6c-8229b09ca9dd
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9cd13723e1483a33e4b98dc544c6e8448dc9a980
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49208229"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>Associar controles WPF a dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar uma associação de dados [!INCLUDE[TLA#tla_titlewinclient](../includes/tlasharptla-titlewinclient-md.md)] controles usando o **fontes de dados** janela. Primeiro, adicione uma fonte de dados para o **fontes de dados** janela. Em seguida, arraste itens dos **fontes de dados** janela para o**WPF Designer**.  
  
##  <a name="adding"></a> Adicionar uma fonte de dados à janela fontes de dados  
 Antes de criar controles associados a dados, você deve primeiro adicionar uma fonte de dados para o **fontes de dados** janela.  
  
#### <a name="to-add-a-data-source-to-the-data-sources-window"></a>Primeiro, adicione uma fonte de dados à janela Fontes de Dados.  
  
1.  Sobre o **modo de exibição** , aponte para **Other Windows**e, em seguida, clique em **fontes de dados**.  
  
2.  Clique em **Add New Data Source**e conclua a **configuração de fonte de dados** assistente.  
  
3.  Realize uma das seguintes tarefas para criar controles de associação de dados:  
  
    -   [Criando um controle que está associado a um único campo de dados](#simple).  
  
    -   [Criando um controle que está associado a vários campos de dados](#complex).  
  
    -   [Criar um conjunto de controles que estão associados a vários campos de dados](#details).  
  
    -   [Associando dados a controles existentes no designer de](#existing).  
  
##  <a name="simple"></a> Criar um controle que está associado a um único campo de dados  
 Depois de adicionar uma fonte de dados para o **fontes de dados** janela, você pode criar um novo controle de associação de dados que exibe um único campo de dados, como um <xref:System.Windows.Controls.ComboBox> ou <xref:System.Windows.Controls.TextBox>.  
  
#### <a name="to-create-a-control-that-is-bound-to-a-single-field-of-data"></a>Para criar um controle que seja associado a único campo de dados  
  
1.  No **fontes de dados** janela, expanda um item que representa uma tabela ou um objeto. Localize o item filho que representa a coluna ou a propriedade a que deseja se associar. Para obter um exemplo visual, consulte [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
2.  Opcionalmente, selecione o controle a ser criado. Cada item na **fontes de dados** janela tem um controle padrão que é criado quando você arrasta o item para o designer. O controle padrão depende do tipo de dados subjacentes ao item.  
  
     Para escolher um controle diferente, clique na seta suspensa próxima ao item e selecione um controle. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
3.  Arraste o item para um contêiner válido no designer. Para obter mais informações sobre contêineres válidos, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria o novo controle de associação de dados e apropriadamente intitulado <xref:System.Windows.Controls.Label> no contêiner. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] também gera [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] e o código para associar o controle aos dados. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
##  <a name="complex"></a> Criar um controle que está associado a vários campos de dados  
 Depois de adicionar uma fonte de dados para o **fontes de dados** janela, você pode criar um novo controle de associação de dados que exibe vários campos de dados, como um <xref:System.Windows.Controls.DataGrid> ou <xref:System.Windows.Controls.ListView>.  
  
#### <a name="to-create-a-control-that-is-bound-to-multiple-fields-of-data"></a>Para criar um controle que seja associado a vários campos de dados.  
  
1.  No **fontes de dados** janela, selecione um item que representa uma tabela ou objeto. Para obter um exemplo visual, consulte [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
2.  Opcionalmente, selecione o controle a ser criado. Por padrão, cada item de **fontes de dados** que representa uma tabela de dados ou objeto de janela é definida para criar um <xref:System.Windows.Controls.DataGrid> (se seu projeto tem como alvo o .NET Framework 4) ou <xref:System.Windows.Controls.ListView> (para versões anteriores do .NET Framework).  
  
     Para selecionar um controle diferente, clique na seta suspensa próxima ao item e selecione um controle. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
    > [!NOTE]
    >  Caso não deseje exibir uma coluna ou propriedade específica, expanda o item para exibir seus filhos. Clique na seta suspensa ao lado da coluna ou propriedade que você não deseja exibir e, em seguida, clique em **None**.  
  
3.  Arraste o item para um contêiner válido no designer, como uma <xref:System.Windows.Controls.Grid>. Para obter mais informações sobre contêineres válidos, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria o novo controle de associação de dados no contêiner. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] também gera [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] e o código para associar o controle aos dados. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
##  <a name="details"></a> Criar um conjunto de controles que estão associados a vários campos de dados  
 Depois de adicionar uma fonte de dados para o **fontes de dados** janela, você pode associar uma tabela de dados ou objeto a um conjunto de controles. Um controle diferente é criado para cada coluna ou propriedade na tabela ou no objeto.  
  
#### <a name="to-create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a>Criação de um conjunto de controles que está associado a vários campos de dados  
  
1.  No **fontes de dados** janela, selecione um item que representa uma tabela ou objeto. Para obter um exemplo visual, consulte [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992).  
  
2.  Clique na seta suspensa ao lado do item e selecione **detalhes**.  
  
    > [!NOTE]
    >  Caso não deseje exibir uma coluna ou propriedade específica, expanda o item para exibir seus filhos. Clique na seta suspensa ao lado da coluna ou propriedade que você não deseja exibir e, em seguida, clique em **None**.  
  
3.  Arraste o item para um contêiner válido no designer, como uma <xref:System.Windows.Controls.Grid>. Para obter mais informações sobre contêineres válidos, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] cria os novos controles de associação de dados no contêiner. Cada controle é associado a uma coluna ou propriedade diferente e cada controle é acompanhado por um apropriadamente intitulado <xref:System.Windows.Controls.Label> controle. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] também gera [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] e o código para associar os controles aos dados. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
##  <a name="existing"></a> Binddata a controles existentes no designer  
 Depois de adicionar uma fonte de dados para o **fontes de dados** janela, você pode adicionar uma associação a um controle existente no designer de dados.  
  
#### <a name="to-bind-data-to-an-existing-control-in-the-designer"></a>Para associar dados a um controle existente no designer  
  
1.  No **fontes de dados** janela, use um dos procedimentos a seguir:  
  
    -   Para adicionar uma associação de dados a um controle existente que exibe vários campos de dados, como uma <xref:System.Windows.Controls.DataGrid> ou <xref:System.Windows.Controls.ListView>, selecione o item que representa a tabela ou objeto que deseja associar ao controle.  
  
    -   Para adicionar uma associação de dados a um controle existente que exibe um único campo de dados, como uma <xref:System.Windows.Controls.ComboBox> ou <xref:System.Windows.Controls.TextBox>, expanda o item que representa a tabela ou objeto que contém os dados e, em seguida, selecione o item que representa os dados que deseja associar ao controle.  
  
2.  Arraste o item selecionado dos **fontes de dados** janela para um controle existente no designer. O controle deve ser uma reprodução automática válida. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] gera [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] e o código para associar o controle aos dados. Para obter mais informações, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
    > [!NOTE]
    >  Se o controle já estiver associado aos dados, a associação de dados para o controle é reiniciada para aquele item que foi arrastado para o controle mais recentemente.  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [Criar tabelas de pesquisa em aplicativos WPF](../data-tools/create-lookup-tables-in-wpf-applications.md)   
 [Exibir dados relacionados em aplicativos WPF](../data-tools/display-related-data-in-wpf-applications.md)   
 [Associar controles WPF a um conjunto de dados](../data-tools/bind-wpf-controls-to-a-dataset.md)   
 [Associar controles WPF a um WCF data service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)   
 [Passo a passo: exibindo dados relacionados em um aplicativo WPF](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)

