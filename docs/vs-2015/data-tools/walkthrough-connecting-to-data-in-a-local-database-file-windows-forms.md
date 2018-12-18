---
title: 'Passo a passo: Conectando a dados em um arquivo de banco de dados Local (Windows Forms) | Microsoft Docs'
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
- databases, connecting to
- local data, SQL Express
- SQL Express, walkthroughs
- SQL Express, connecting
- data [Visual Studio], local
- data [Visual Studio], connecting to SQL Express
ms.assetid: 5e16b7da-3fdc-4e69-bdb4-e8e700481811
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 71898c88a8d7a1d4a119a7e7a932e295ae12eb34
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176157"
---
# <a name="walkthrough-connecting-to-data-in-a-local-database-file-windows-forms"></a>Instruções passo a passo: conectando a dados em um arquivo de banco de dados local (Windows Forms)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível exibir rápida e facilmente dados com base em um arquivo de banco de dados local no aplicativo criando-se um conjunto de dados e, em seguida, adicionando-se controles de associação de dados ao aplicativo. Neste passo a passo, você exibirá dados do arquivo de banco de dados local que você criou seguindo as etapas em [criar um banco de dados SQL usando um designer](../data-tools/create-a-sql-database-by-using-a-designer.md). Depois de criar um projeto do Windows Forms, você se conectará a esse banco de dados e especificará que deseja que os dados da tabela Customers sejam exibidos em uma grade de dados no formulário do aplicativo.  
  
 Durante a criação de um banco de dados no Visual Studio 2013, o mecanismo LocalDB do SQL Server Express é usado para acessar um arquivo de banco de dados (.mdf) no SQL Server 2012. Em versões anteriores do Visual Studio, o mecanismo do SQL Server Express é usado para acessar um arquivo de banco de dados (.mdf). Ver [visão geral de dados Local](../data-tools/local-data-overview.md).  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
 Esta explicação passo a passo inclui as seguintes tarefas:  
  
-   [Criando e configurando um conjunto de dados](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md#BKMK_CreateDataset)  
  
-   [Adicionando controles ligados a dados](../data-tools/walkthrough-connecting-to-data-in-a-local-database-file-windows-forms.md#BKMK_AddCtrls)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisa de acesso ao banco de dados SampleDatabase. mdf criado Concluindo [criar um banco de dados SQL usando um designer](../data-tools/create-a-sql-database-by-using-a-designer.md).  
  
##  <a name="BKMK_CreateDataset"></a> Criando e configurando um conjunto de dados  
  
#### <a name="to-create-and-configure-a-dataset"></a>Para criar e configurar um conjunto de dados  
  
1.  Criar um projeto Windows Forms e nomeie- **como ConnectLocalData**.  
  
     Ver [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
2.  Se o **fontes de dados** janela não estiver visível, escolha as teclas Shift-Alt-D ou, na barra de menus, escolha **exibição**, **Other Windows**, **Show Data Sources**.  
  
3.  No **fontes de dados** janela, escolha o **Add New Data Source** link.  
  
     No **Data Source Configuration Wizard**, escolha o **próxima** botão duas vezes para aceitar as configurações padrão.  
  
4.  Sobre o **escolha sua Conexão de dados** , escolha o **nova Conexão** botão.  
  
     O **Choose Data Source** caixa de diálogo é exibida.  
  
5.  No **fonte de dados** , escolha **arquivo de banco de dados do Microsoft SQL Server**e, em seguida, escolha o **continuar** botão.  
  
     O **Adicionar Conexão** caixa de diálogo é exibida.  
  
6.  No **nome do arquivo de banco de dados** , especifique o arquivo que você criou ao concluir [criar um banco de dados SQL usando um designer](../data-tools/create-a-sql-database-by-using-a-designer.md), ou escolher o **procurar** e, em seguida, localize Esse arquivo.  
  
     Por padrão, o arquivo está em que os usuários\\*Suaconta*\Documents\Visual Studio *versão*\projects\sampledatabasewalkthrough\sampledatabasewalkthrough.  
  
7.  Sob **faça logon no servidor**, aceite os valores padrão, escolha o **Okey** botão e, em seguida, escolha o **próxima** botão.  
  
    > [!NOTE]
    >  Ao se conectar a um arquivo de banco de dados local, você pode criar uma cópia do banco de dados no projeto ou se conectar ao arquivo de banco de dados em seu local atual. Ver [como: gerenciar arquivos de dados locais em seu projeto](../data-tools/how-to-manage-local-data-files-in-your-project.md).  
  
8.  Na caixa de diálogo que aparece, escolha **Sim** para copiar o arquivo de banco de dados ao seu projeto.  
  
9. No **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** , escolha o **próxima** botão.  
  
10. No **Choose Your Database Objects** página, expanda o **tabelas** nó, selecione o **clientes** e **pedidos** caixas de seleção e, em seguida, Escolha o **concluir** botão.  
  
     O **SampleDatabaseDataSet** é adicionado ao seu projeto e o **clientes** e **pedidos** tabelas aparecem no **fontes de dados** janela.  
  
##  <a name="BKMK_AddCtrls"></a> Adicionando controles ligados a dados  
  
#### <a name="to-add-data-bound-controls"></a>Para adicionar controles de associação de dados  
  
1.  Mover principal **clientes** nó a partir do **fontes de dados** window para **Form1**.  
  
     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [SampleDatabaseDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
2.  Para executar o aplicativo e mostrar os dados adicionados na explicação passo a passo anterior, use a tecla F5.  
  
3.  Escolha o ícone amarelo de adição (![adicionar botão no formulário do Windows](../data-tools/media/addrecord.png "AddRecord")), adicione um registro de cliente e, em seguida, salve suas alterações, escolhendo o ícone de disco (![botão Salvar no formulário do Windows](../data-tools/media/saveinwf.png "SaveInWF")).  
  
4.  Excluir o registro recém-criado escolhendo-lo e, em seguida, escolhendo o ícone de exclusão vermelho (![botão Excluir em um Windows Form](../data-tools/media/deleterecord.png "DeleteRecord")).  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode criar ou modificar objetos no conjunto de dados, se você abrir a fonte de dados na [criando e editando conjuntos de dados tipados](../data-tools/creating-and-editing-typed-datasets.md). Também é possível adicionar lógica de validação aos eventos <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> das tabelas de dados no conjunto de dados. Ver [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de dados local](../data-tools/local-data-overview.md)   
 [Como: gerenciar arquivos de dados locais em seu projeto](../data-tools/how-to-manage-local-data-files-in-your-project.md)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)