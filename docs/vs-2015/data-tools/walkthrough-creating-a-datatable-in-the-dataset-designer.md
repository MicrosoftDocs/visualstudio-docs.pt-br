---
title: 'Passo a passo: Criando um DataTable no Designer de conjunto de dados | Microsoft Docs'
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
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
ms.assetid: abf0a2b5-e4e5-422e-97ef-55a0e35a82df
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 1f0f31528239794b9c7a3b4a4bf98542ed4bbcf2
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49299956"
---
# <a name="walkthrough-creating-a-datatable-in-the-dataset-designer"></a>Instruções passo a passo: criando um DataTable no Designer de Conjunto de Dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo explica como criar uma <xref:System.Data.DataTable> (sem um TableAdapter) usando o **Dataset Designer**. Para obter informações sobre como criar tabelas de dados que incluem TableAdapters, consulte [criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md).  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criar um novo projeto de aplicativo do Windows  
  
-   Adicionando um novo conjunto de dados para o aplicativo  
  
-   Adicionando uma nova tabela de dados para o conjunto de dados  
  
-   Adicionando colunas à tabela de dados  
  
-   Definindo a chave primária da tabela  
  
## <a name="creating-a-new-windows-application"></a>Criando um novo Aplicativo do Windows  
  
#### <a name="to-create-a-new-windows-application-project"></a>Para criar um novo projeto de Aplicativo do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Escolha uma linguagem de programação a **tipos de projeto** painel.  
  
3.  Clique em **aplicativo do Windows** na **modelos** painel.  
  
4.  Nomeie o projeto `DataTableWalkthrough`e, em seguida, clique em **Okey**.  
  
     O projeto para o Visual Studio adiciona **Gerenciador de soluções** e exibe **Form1** no designer.  
  
## <a name="adding-a-new-dataset-to-the-application"></a>Adicionando um novo conjunto de dados para o aplicativo  
  
#### <a name="to-add-a-new-dataset-item-to-the-project"></a>Para adicionar um novo item de conjunto de dados ao projeto  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
     A caixa de diálogo Adicionar Novo Item é exibido.  
  
2.  No **modelos** caixa, selecione **conjunto de dados**.  
  
3.  Clique em **Adicionar**.  
  
     Visual Studio irá adicionar um arquivo chamado **dataSet1** ao projeto e abri-lo na **Dataset Designer**.  
  
## <a name="adding-a-new-datatable-to-the-dataset"></a>Adicionando uma nova DataTable para o conjunto de dados  
  
#### <a name="to-add-a-new-data-table-to-the-dataset"></a>Para adicionar uma nova tabela de dados para o conjunto de dados  
  
1.  Arraste uma **DataTable** da **conjunto de dados** guia da **caixa de ferramentas** para o **Dataset Designer**.  
  
     Uma tabela denominada **DataTable1** é adicionado ao conjunto de dados.  
  
    > [!NOTE]
    >  Para criar uma tabela de dados que inclui um TableAdapter, consulte [instruções passo a passo: Criando um TableAdapter com várias consultas](../data-tools/walkthrough-creating-a-tableadapter-with-multiple-queries.md).  
  
2.  Clique na barra de título do **DataTable1** e renomeie- `Music`.  
  
## <a name="adding-columns-to-the-data-table"></a>Adicionando colunas à tabela de dados  
  
#### <a name="to-add-columns-to-the-data-table"></a>Para adicionar colunas à tabela de dados  
  
1.  Clique com botão direito do **música** tabela. Aponte para **Add**e, em seguida, clique em **coluna**.  
  
2.  Nome da coluna `SongID`.  
  
3.  No **propriedades** janela, defina as <xref:System.Data.DataColumn.DataType%2A> propriedade <xref:System.Int16?displayProperty=fullName>.  
  
4.  Repita esse processo e adicione as seguintes colunas:  
  
     `SongTitle`: <xref:System.String?displayProperty=fullName>  
  
     `Artist`: <xref:System.String?displayProperty=fullName>  
  
     `Genre`: <xref:System.String?displayProperty=fullName>  
  
## <a name="setting-the-primary-key-for-the-table"></a>Definindo a chave primária da tabela  
 Todas as tabelas de dados devem ter uma chave primária. Uma chave primária identifica exclusivamente um registro específico em uma tabela de dados.  
  
#### <a name="to-set-the-primary-key-of-the-data-table"></a>Para definir a chave primária da tabela de dados  
  
-   Clique com botão direito do **SongID** coluna e clique **definir chave primária**.  
  
     Um ícone de chave aparece ao lado de **SongID** coluna.  
  
## <a name="saving-your-project"></a>Salvando seu projeto  
  
#### <a name="to-save-the-datatablewalkthrough-project"></a>Para salvar o projeto DataTableWalkthrough  
  
-   Sobre o **arquivo** menu, clique em **Salvar tudo**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você criou a tabela, você talvez queira executar uma das seguintes ações:  
  
|Para|Consulte|  
|--------|---------|  
|Criar um formulário para dados de entrada|[Passo a passo: Exibindo dados em um formulário do Windows](../data-tools/walkthrough-displaying-data-on-a-windows-form.md).|  
|Adicionar dados à tabela|[Adicionando dados a um DataTable](http://msdn.microsoft.com/library/d6aa8474-7bde-48f7-949d-20dc38a1625b).|  
|Exibir dados em uma tabela|[Exibindo dados em uma DataTable](http://msdn.microsoft.com/library/1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc).|  
|Editar dados|[Edições de DataTable](http://msdn.microsoft.com/library/f08008a9-042e-4de9-94f3-4f0e502b1eb5)|  
|Excluir uma linha de uma tabela|[Exclusão de DataRow](http://msdn.microsoft.com/library/c34f531d-4b9b-4071-b2d7-342c402aa586)|  
  
## <a name="see-also"></a>Consulte também  
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)