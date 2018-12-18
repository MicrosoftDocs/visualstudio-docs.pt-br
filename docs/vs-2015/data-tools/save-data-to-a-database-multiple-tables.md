---
title: Salvar dados em um banco de dados (várias tabelas) | Microsoft Docs
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
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 986df2d58c9a8955c9de9b45edaa5276b2e68bfb
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50218384"
---
# <a name="save-data-to-a-database-multiple-tables"></a>Salvar dados em um banco de dados (várias tabelas)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Um dos cenários mais comuns no desenvolvimento de aplicativos é exibir dados de um formulário em um aplicativo do Windows, editar e enviá-los atualizados de volta para o banco de dados. Essa explicação passo a passo cria um formulário que exibe dados de duas tabelas relacionadas e mostra como editar registros e salvar alterações no banco de dados. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind.  
  
 Você pode salvar os dados em seu aplicativo de volta no banco de dados chamando o método `Update` de um TableAdapter. Quando você arrasta tabelas do **fontes de dados** janela em um formulário, o código necessário para salvar dados é adicionada automaticamente. Quaisquer tabelas adicionais que são adicionadas a um formulário exigem a adição manual desse código. Essa explicação passo a passo mostra como adicionar código para salvar atualizações de mais de uma tabela.  
  
> [!NOTE]
>  As caixas de diálogo e comandos de menu que você vê podem diferir dos descritos na Ajuda, dependendo de suas configurações ativas ou a edição que você está usando. Para alterar as configurações, escolha **Importar e Exportar Configurações** no menu **Ferramentas**. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criando um novo **aplicativo do Windows** projeto.  
  
-   Criando e configurando uma fonte de dados em seu aplicativo com o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Configurando os controles dos itens na [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992). Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
-   Criando controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
-   Modificando alguns registros em cada tabela no conjunto de dados.  
  
-   Modificando o código para enviar os dados atualizados no conjunto de dados de volta ao banco de dados.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind.  Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-the-windows-application"></a>Criar o aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**. Atribuir um nome para o projeto é opcional durante esta etapa, mas vamos dar a ele um nome porque estamos planejando salvá-lo posteriormente.  
  
#### <a name="to-create-the-new-windows-application-project"></a>Para criar o novo projeto de aplicativo do Windows  
  
1.  Sobre o **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `UpdateMultipleTablesWalkthrough`.  
  
3.  Selecione **aplicativo do Windows**e, em seguida, selecione **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **UpdateMultipleTablesWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="create-the-data-source"></a>Criar a fonte de dados  
 Esta etapa cria uma fonte de dados do banco de dados Northwind usando o **Data Source Configuration Wizard**. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, selecione**Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione**Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3.  Sobre o **escolher um tipo de fonte de dados**tela, selecione **banco de dados**e, em seguida, selecione **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados**tela faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
         -ou-  
  
    -   Selecione **nova Conexão** para abrir o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, selecione **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo**, selecione **próxima**.  
  
7.  Sobre o **Choose your Database Objects**, expanda o **tabelas** nó.  
  
8.  Selecione o **clientes** e **pedidos** tabelas e, em seguida, selecione **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto, e as tabelas aparecem na **fontes de dados** janela.  
  
## <a name="set-the-controls-to-be-created"></a>Defina os controles a serem criados  
 Para este passo a passo, os dados na `Customers` a tabela está em um **detalhes** layout onde os dados são exibidos em controles individuais. Os dados do `Orders` a tabela está em um **grade** layout que é exibido em um <xref:System.Windows.Forms.DataGridView> controle.  
  
#### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>Definir o tipo de remoção dos itens na Janela Fontes de Dados  
  
1.  No **fontes de dados** janela, expanda o **clientes** nó.  
  
2.  Sobre o **clientes** nó, selecione **detalhes** na lista de controle para alterar o controle do **clientes** tabela para controles individuais. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
## <a name="create-the-data-bound-form"></a>Criar o formulário de associação de dados  
 Você pode criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>Para criar controles de associação de dados no formulário  
  
1.  Arraste principal **clientes** nó a partir do **fontes de dados** window para **Form1**.  
  
     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
2.  Arraste relacionado **pedidos** nó a partir do **fontes de dados** window para **Form1**.  
  
    > [!NOTE]
    >  Relacionado **pedidos** nó está localizado abaixo de **Fax** coluna e é um nó filho do **clientes** nó.  
  
     Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Uma [OrdersTableAdapter](../data-tools/tableadapter-overview.md) e <xref:System.Windows.Forms.BindingSource> aparecem na bandeja de componentes.  
  
## <a name="addcode-to-update-the-database"></a>Addcode para atualizar o banco de dados  
 Você pode atualizar o banco de dados chamando o `Update` métodos do **clientes** e **pedidos** TableAdapters. Por padrão, um manipulador de eventos para o **salve** botão do<xref:System.Windows.Forms.BindingNavigator> é adicionado ao código do formulário para enviar atualizações para o banco de dados. Este procedimento modifica o código para enviar atualizações na ordem correta. Isso elimina a possibilidade de gerar erros de integridade referencial. O código também implementa manipulação de erros com a quebra automática da chamada de atualização em um bloco try-catch. Você pode mudar o código para atender às necessidades do seu aplicativo.  
  
> [!NOTE]
>  Para maior clareza, este passo a passo não usa uma transação. No entanto, se você estiver atualizando dois ou mais tabelas relacionadas, inclua toda a lógica de atualização dentro de uma transação. Uma transação é um processo que garante que todas as alterações relacionadas a um banco de dados são bem-sucedidas antes que as alterações sejam confirmadas. Para obter mais informações, consulte [transações e simultaneidade](http://msdn.microsoft.com/library/f46570de-9e50-4fe6-8710-a8c31fa8569b).  
  
#### <a name="to-add-update-logic-to-the-application"></a>Para adicionar lógica de atualização ao aplicativo  
  
1.  Selecione o **salve** botão o <xref:System.Windows.Forms.BindingNavigator>. Isso abre o Editor de códigos para o `bindingNavigatorSaveItem_Click` manipulador de eventos.  
  
2.  Substitua o código no manipulador de eventos para chamar os métodos `Update` dos TableAdapters relacionados. O código a seguir primeiro cria três tabelas de dados temporárias para armazenar as informações de cada <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState>, <xref:System.Data.DataRowState> e <xref:System.Data.DataRowState>). Em seguida, as atualizações são executadas na ordem correta. O código deve se parecer com o seguinte:  
  
     [!code-csharp[VbRaddataSaving#10](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form4.cs#10)]
     [!code-vb[VbRaddataSaving#10](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form4.vb#10)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Selecione **F5**.  
  
2.  Faça algumas alterações nos dados de um ou mais registros em cada tabela.  
  
3.  Selecione o **salvar** botão.  
  
4.  Confira os valores no banco de dados para verificar se as alterações foram salvas.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, há várias etapas que você talvez queira realizar após criar um formulário de associação de dados em seu aplicativo do Windows. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:  
  
-   Adicionando funcionalidade de busca ao formulário. Para obter mais informações, consulte [como: adicionar uma consulta parametrizada a um aplicativo do Windows Forms](http://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416).  
  
-   Editando a fonte de dados para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [como: editar um conjunto de dados](http://msdn.microsoft.com/library/f2dade5f-9c7a-4ddb-96a8-e0a39e50bfd3).  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)

