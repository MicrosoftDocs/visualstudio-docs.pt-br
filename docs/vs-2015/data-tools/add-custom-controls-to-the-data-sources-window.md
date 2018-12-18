---
title: Adicionar controles personalizados à janela fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
caps.latest.revision: 45
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 7e84224d4ebd066891d4fdf90b4ad488a79cc0b1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49183632"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>Adicionar controles personalizados à janela Fontes de Dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Quando você arrasta um item a partir de **fontes de dados** janela para uma superfície de design para criar um controle associado a dados, você pode selecionar o tipo de controle que você criar. Cada item na janela tem uma lista suspensa que exibe os controles que podem ser escolhidos. O conjunto de controles associados a cada item é determinado pelo tipo de dados do item. Se o controle que você deseja criar não aparecer na lista, você pode seguir as instruções neste tópico para adicionar o controle à lista.  
  
 Para obter mais informações sobre como selecionar os controles ligados a dados para criar para itens na **fontes de dados** janela, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
> [!NOTE]
>  As caixas de diálogo e os comandos do menu que você vê podem ser diferentes dos descritos na Ajuda, dependendo da edição ou das configurações ativas. Para alterar suas configurações, nos **ferramentas** menu, selecione **Import and Export Settings**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
##  <a name="customizinglist"></a> Personalizar a lista de controles associáveis para um tipo de dados  
 Para adicionar ou remover os controles de lista de controles disponíveis para itens na **fontes de dados** janela que tem um tipo de dados específico, execute as seguintes etapas.  
  
#### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>Para selecionar os controles a serem listados para um tipo de dados  
  
1.  Certifique-se de que o WPF Designer ou o Designer de formulários do Windows é aberto.  
  
2.  No **fontes de dados** janela, clique em um item que faz parte de uma fonte de dados que você adicionou à janela e, em seguida, clique no menu suspenso para o item.  
  
3.  No menu suspenso, clique em **personalizar**. Uma das seguintes caixas de diálogo é aberta:  
  
    -   Se o Windows Forms Designer estiver aberto, o **personalização da IU de dados** página do **opções** caixa de diálogo é aberta.  
  
    -   Se o WPF Designer estiver aberto, o **personalizar associação de controle** caixa de diálogo é aberta.  
  
4.  Na caixa de diálogo, selecione um tipo de dados do **tipo de dados** lista suspensa.  
  
    -   Para personalizar a lista de controles para uma tabela ou objeto, selecione **[List]**.  
  
    -   Para personalizar a lista de controles para uma coluna de uma tabela ou uma propriedade de um objeto, selecione o tipo de dados da coluna ou propriedade no armazenamento de dados subjacente.  
  
    -   Para personalizar a lista de controles para exibir os objetos de dados que têm formas definidas pelo usuário, selecione **[Other]**. Por exemplo, selecione **[Other]** se seu aplicativo tiver um controle personalizado que exibe dados de mais de uma propriedade de um objeto específico.  
  
5.  No **associados a controles** caixa, selecione cada controle que você deseja estar disponíveis para o tipo de dados selecionado ou desmarque a seleção de todos os controles que você deseja remover da lista.  
  
    > [!NOTE]
    >  Se o controle que você deseja selecionar não aparecerá na **associados a controles** caixa, você deve adicionar o controle à lista. Para obter mais informações, consulte [adicionando controles para a lista de controles associados para um tipo de dados](#addingcontrols).  
  
6.  Clique em **OK**.  
  
7.  No **fontes de dados** janela, clique em um item de dados que você associou a apenas um ou mais controles de tipo e, em seguida, clique no menu suspenso para o item.  
  
     Os controles que você selecionou na **associados a controles** caixa agora aparecem no menu suspenso para o item.  
  
##  <a name="addingcontrols"></a> Addcontrols à lista de controles associados para um tipo de dados  
 Se você deseja associar um controle com um tipo de dados, mas o controle não aparecer na **associados a controles** caixa, você deve adicionar o controle à lista. O controle deve estar localizado na solução atual ou em um assembly referenciado. Ele também deve estar disponível na **caixa de ferramentas**, e ter um atributo que especifica o comportamento de associação de dados do controle.  
  
#### <a name="to-add-controls-to-the-list-of-associated-controls"></a>Para adicionar controles à lista de controles associados  
  
1.  Adicione o controle desejado para o **caixa de ferramentas** clicando com o **caixa de ferramentas** e selecionando **escolher itens**.  
  
     O controle deve ter um dos seguintes atributos.  
  
    |Atributo|Descrição|  
    |---------------|-----------------|  
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|Implemente este atributo em controles simples que exibe uma única coluna (ou propriedade) de dados, como um <xref:System.Windows.Forms.TextBox>.|  
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|Implemente este atributo em controles que exibem listas (ou tabelas) de dados, como um <xref:System.Windows.Forms.DataGridView>.|  
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|Implemente este atributo em controles que exibem listas (ou tabelas) de dados, mas também precisam apresentar uma única coluna ou propriedade, como um <xref:System.Windows.Forms.ComboBox>.|  
  
2.  Para formulários do Windows, sobre o **opções** caixa de diálogo, abra o **personalização da IU de dados** página. Ou, para WPF, abra o **personalizar associação de controle** caixa de diálogo. Para obter mais informações, consulte [Personalizando a lista de controles associáveis para um tipo de dados](#customizinglist).  
  
3.  No **associados a controles** controle de caixa, o que você acabou de adicionar para o **caixa de ferramentas** agora deve aparecer.  
  
    > [!NOTE]
    >  Somente os controles que estão localizados dentro da solução atual ou em um assembly referenciado podem ser adicionados à lista de controles associados. (Os controles também devem implementar um dos atributos de associação de dados na tabela anterior.) Para associar dados a um controle personalizado que não está disponível na **fontes de dados** janela, arraste o controle dos **caixa de ferramentas** para a superfície de design e, em seguida, arraste o item para vincular a partir o **dados Fontes** janela para o controle.  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)

