---
title: Criar e editar Datasets tipados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Designer_Microsoft.VSDesigner.DataSource.Designer.DataSourceRootDesigner
- vs.data.adddataset
dev_langs:
- VB
- CSharp
- C++
- aspx
- aspx
helpviewer_keywords:
- datasets [Visual Basic], visual designer
- data [Visual Studio], Dataset Designer
- Dataset Designer
ms.assetid: cd0dbe93-be9b-41e4-bc39-e9300678c1f2
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 8c18717cd2a5c7e05b79dbe575d919ef0c8670dd
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49225830"
---
# <a name="creating-and-editing-typed-datasets"></a>Criando e editando conjuntos de dados tipados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O**Dataset Designer** é um conjunto de ferramentas visuais que você pode usar para criar e editar datasets tipados e os itens individuais que eles contêm.  
  
 O **Dataset Designer** fornece representações visuais dos objetos contidos em datasets tipados. Criar e modificar [TableAdapters](../data-tools/tableadapter-overview.md), [consultas TableAdapter](../data-tools/how-to-create-tableadapter-queries.md), <xref:System.Data.DataTable>s, <xref:System.Data.DataColumn>s, e <xref:System.Data.DataRelation>s com o **Dataset Designer**.  
  
 Para abrir o **Dataset Designer**, clique duas vezes em um conjunto de dados no **Gerenciador de soluções**, ou clique com botão direito em um conjunto de dados do **fontes de dados** janela e clique em **editar Conjunto de dados com o Designer**. Para obter mais informações, consulte [como: abrir um conjunto de dados no Designer de conjunto de dados](http://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3). Adição de uma nova <xref:System.Data.DataSet> de item com o **Adicionar Novo Item** caixa de diálogo será aberta a **Dataset Designer** com um dataset vazio pronto para edição.  
  
> [!NOTE]
>  O **Dataset Designer** pode ser usado para estender a funcionalidade de um conjunto de dados. Clique duas vezes na superfície de design ou com o botão direito e escolha **Exibir código** para criar um arquivo de classe parcial onde você pode adicionar código ao conjunto de dados que não será alterado ou excluído pelo designer. Para obter informações sobre como estender a funcionalidade de um TableAdapter, consulte [estendem a funcionalidade de um TableAdapter](../data-tools/extend-the-functionality-of-a-tableadapter.md).  
  
 A tabela a seguir lista as tarefas comuns que você pode realizar com o **Dataset Designer**.  
  
|Para|Consulte|  
|--------|---------|  
|Criar um TableAdapter|[Criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md)|  
|Editar um TableAdapter|[Como: editar TableAdapters](http://msdn.microsoft.com/library/ca178745-e35a-45f1-a395-23cddfd8f855)|  
|Criar uma consulta TableAdapter|[Como criar consultas TableAdapter](../data-tools/how-to-create-tableadapter-queries.md)|  
|Editar uma consulta do TableAdapter|[Como editar consultas TableAdapter](../data-tools/how-to-edit-tableadapter-queries.md)|  
|Criar um <xref:System.Data.DataTable>|[Como criar tabelas de dados](../data-tools/how-to-create-data-tables.md)|  
|Editar um <xref:System.Data.DataTable>|[Criando DataTables](../data-tools/designing-datatables.md)|  
|Criar um <xref:System.Data.DataColumn>|[Como: adicionar colunas a uma DataTable](http://msdn.microsoft.com/library/8ca21f77-b99a-47a7-a656-7cfd7a1bd9df)|  
|Criar uma relação entre dois <xref:System.Data.DataTable>s|[Como: criar DataRelations com o Designer de conjunto de dados](http://msdn.microsoft.com/library/a3ab4803-0b50-4b74-9920-ab20bfbf1aa2)|  
|Estender a funcionalidade do conjunto de dados|[Como: estender a funcionalidade de um conjunto de dados](http://msdn.microsoft.com/library/dfbc21eb-7ea2-4942-addd-49677f5493be)|  
|Adicionar validação a uma tabela de dados <xref:System.Data.DataTable.ColumnChanging> evento|[Como: validar dados durante alterações de coluna](http://msdn.microsoft.com/library/a2680600-67b6-4a40-a77e-b5bc638281c5)|  
|Adicionar validação a uma tabela de dados <xref:System.Data.DataTable.RowChanging> evento|[Como: validar dados durante alterações de linha](http://msdn.microsoft.com/library/afc03c77-dfed-4302-9376-929400468ecc)|  
  
## <a name="creating-objects-on-the-design-surface"></a>Criando objetos na superfície de Design  
 Você pode criar conjuntos de dados, adicionar e editar os objetos individuais que compõem um conjunto de dados. A tabela a seguir fornece uma explicação sobre os diferentes objetos na **DataSet** guia o **caixa de ferramentas** que podem ser arrastados para a superfície de design:  
  
|Objeto|Descrição|  
|------------|-----------------|  
|TableAdapter|Contém uma coleção de comandos de dados e uma conexão de dados que são usadas para se comunicar com o banco de dados subjacente e popular uma tabela de dados. Para obter mais informações, consulte [visão geral de TableAdapter](../data-tools/tableadapter-overview.md) e [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).|  
|Consulta|Consultas TableAdapter são métodos fortemente tipados que executam instruções SQL e procedimentos armazenados. Executando uma consulta do TableAdapter preenche uma tabela de dados com dados ou executa outras tarefas de banco de dados. Para obter mais informações, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md). Arrastar uma consulta para uma tabela adiciona a consulta à tabela, enquanto arrastar uma consulta para uma área vazia do **Dataset Designer** cria uma consulta global. Para obter mais informações, consulte [como: adicionar consultas globais a um TableAdapter](../data-tools/how-to-add-global-queries-to-a-tableadapter.md).|  
|<xref:System.Data.DataTable>|Representa uma coleção em memória das linhas retornadas de um banco de dados.|  
|Relação (<xref:System.Data.DataRelation>)|Representa uma relação pai-filho entre dois <xref:System.Data.DataTable>s. Para obter mais informações, consulte [Introdução a objetos DataRelation](http://msdn.microsoft.com/library/89d8a881-8265-41f2-a88b-61311ab06192) e [passo a passo: Criando uma relação entre tabelas de dados](http://msdn.microsoft.com/library/9b3f1c87-7098-4ed4-a710-cde8f8059f82).|  
  
> [!NOTE]
>  O **Dataset Designer** se conecta a um banco de dados subjacente é criado somente quando um conjunto de dados; o designer não detectará automaticamente as alterações subsequentes no banco de dados. Para atualizar um existente. de XSD, execute novamente o **Assistente de configuração**. Se as relações de tabela foram alterados, remova e adicione novamente as tabelas relevantes para a. xsd.  
  
## <a name="linq-to-dataset"></a>LINQ to Dataset  
 [!INCLUDE[linq_dataset](../includes/linq-dataset-md.md)] Habilita [LINQ (consulta integrada à linguagem)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d) sobre os dados em um <xref:System.Data.DataSet> objeto. Para obter mais informações, consulte [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criando um conjunto de dados com o Designer de conjunto de dados](../data-tools/walkthrough-creating-a-dataset-with-the-dataset-designer.md)   
 [Passo a passo: Criando um TableAdapter com várias consultas](../data-tools/walkthrough-creating-a-tableadapter-with-multiple-queries.md)   
 [Passo a passo: Criando um DataTable no Dataset Designer](../data-tools/walkthrough-creating-a-datatable-in-the-dataset-designer.md)   
 [Passo a passo: Criando uma relação entre tabelas de dados](http://msdn.microsoft.com/library/9b3f1c87-7098-4ed4-a710-cde8f8059f82)   
 [Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md)   
 [Janela Fontes de Dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)   
 [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)