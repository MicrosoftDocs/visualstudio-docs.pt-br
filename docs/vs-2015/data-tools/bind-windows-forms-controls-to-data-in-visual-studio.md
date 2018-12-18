---
title: Associar controles dos Windows Forms a dados no Visual Studio | Microsoft Docs
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
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
caps.latest.revision: 40
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e63d20bc226abe0c0bdf4c77179a94b0d0e6212c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49293664"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>Associar controles dos Windows Forms a dados no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Você pode exibir dados para usuários do seu aplicativo pela associação de dados ao Windows Forms. Para criar esses controles ligados a dados, você pode arrastar itens dos **fontes de dados** janela para o Designer de formulários do Windows no Visual Studio. Este tópico descreve algumas das tarefas, ferramentas e classes envolvidas na criação de aplicativos do Windows Forms associado a dados mais comuns.  
  
 ![Operação de arrastar a fonte de dados](../data-tools/media/raddata-data-source-drag-operation.png "raddata fonte de dados de operação de arrastar")  
  
 Para obter informações gerais sobre como criar controles associados a dados no Visual Studio, consulte [associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md). Para obter mais informações sobre associação de dados nos Windows Forms, consulte [vinculação de dados do Windows Forms](http://msdn.microsoft.com/library/c3826d8e-ea25-4ad4-a669-45bfb19192aa).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Associar controles do Windows Forms a dados](../data-tools/bind-windows-forms-controls-to-data.md)  
  
-   [Confirmar edições em processo em controles associados a dados antes de salvar os dados](../data-tools/commit-in-process-edits-on-data-bound-controls-before-saving-data.md)  
  
-   [Criar tabelas de pesquisa em aplicativos do Windows Forms](../data-tools/create-lookup-tables-in-windows-forms-applications.md)  
  
-   [Criar um Windows Form para pesquisar dados](../data-tools/create-a-windows-form-to-search-data.md)  
  
-   [Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados simples](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)  
  
-   [Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados complexos](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)  
  
-   [Criar um controle de usuário do Windows Forms que dá suporte à vinculação de dados de consulta](../data-tools/create-a-windows-forms-user-control-that-supports-lookup-data-binding.md)  
  
-   [Passar dados entre formulários](../data-tools/pass-data-between-forms.md)  
  
## <a name="bindingsource-component"></a>Componente BindingSource  
 O <xref:System.Windows.Forms.BindingSource> componente tem duas finalidades. Primeiro, ele fornece uma camada de abstração ao associar os controles no formulário a dados. Controles no formulário são vinculados para o <xref:System.Windows.Forms.BindingSource> componente (em vez de sendo vinculados diretamente a uma fonte de dados).  
  
 Em segundo lugar, ele pode gerenciar uma coleção de objetos. Adição de um tipo para o <xref:System.Windows.Forms.BindingSource> cria uma lista desse tipo.  
  
 Para obter mais informações sobre o <xref:System.Windows.Forms.BindingSource> componente, consulte:  
  
-   [Componente BindingSource](http://msdn.microsoft.com/library/3e2faf4c-f5b8-4fa6-9fbc-f59c37ec2fb9)  
  
-   [Visão geral do componente BindingSource](http://msdn.microsoft.com/library/be838caf-fcb0-4b68-827f-58b2c04b747f)  
  
-   [Arquitetura do componente BindingSource](http://msdn.microsoft.com/library/7bc69c90-8a11-48b1-9336-3adab5b41591)  
  
## <a name="bindingnavigator-control"></a>Controle BindingNavigator  
 Esse componente fornece uma interface do usuário para navegar pelos dados exibidos por um aplicativo do Windows. Para obter mais informações, consulte [Controle BindingNavigator](http://msdn.microsoft.com/library/18c1e2a5-9834-40d3-9b2e-2b545e4e769e).  
  
## <a name="datagridview-control"></a>Controle DataGridView  
 Para exibir e editar dados tabulares de muitos tipos diferentes de fontes de dados, use o <xref:System.Windows.Forms.DataGridView> controle. Você pode associar dados a um <xref:System.Windows.Forms.DataGridView> usando o <xref:System.Windows.Forms.DataGridView.DataSource%2A> propriedade. Para obter mais informações, consulte [visão geral do controle DataGridView](http://msdn.microsoft.com/library/0a45c661-89dc-4390-9cc6-c47eee501488).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)

