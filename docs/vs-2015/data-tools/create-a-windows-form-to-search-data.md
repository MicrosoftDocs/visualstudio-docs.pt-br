---
title: Criar um formulário do Windows para pesquisar dados | Microsoft Docs
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
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: e42c86cf94115d317eb20df66f4cef005e05eba9
ms.sourcegitcommit: c9a01c599ce19a5845605b3b28c0229fd0abb93f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52281791"
---
# <a name="create-a-windows-form-to-search-data"></a>Criar um Windows Form para pesquisar dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Um cenário de aplicativo comum exibirá dados selecionados em um formulário. Por exemplo, você pode querer exibir os pedidos de um cliente específico ou os detalhes de um pedido específico. Nesse cenário, um usuário insere informações em um formulário e uma consulta é executada com a entrada do usuário como parâmetro, ou seja, os dados são selecionados com base em uma consulta parametrizada. A consulta retorna apenas os dados que satisfazem os critérios inseridos pelo usuário. Este passo a passo mostra como criar uma consulta que retorna clientes de uma cidade específica, como mudar a interface do usuário para que os usuários possam inserir o nome de uma cidade e pressionar um botão para executar a consulta.  
  
 O uso de consultas parametrizadas ajuda a tornar seu aplicativo eficiente, permitindo que o banco de dados funcione melhor, filtrando registros rapidamente. Por outro lado, se você solicitar uma tabela de banco de dados inteiro, transferi-la pela rede e, em seguida, use a lógica do aplicativo para localizar os registros que deseja, seu aplicativo pode ficar lento e ineficiente.  
  
 Você pode adicionar consultas parametrizadas a qualquer TableAdapter (e controles para aceitar valores de parâmetro e executar a consulta), usando o **construtor de critérios de pesquisa** caixa de diálogo. Abra a caixa de diálogo selecionando o **Add Query** comando as **dados** menu (ou em qualquer marca inteligente TableAdapter).  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criar um novo projeto de aplicativo do Windows Forms.  
  
-   Criando e configurando a fonte de dados em seu aplicativo com o **configuração de fonte de dados** assistente.  
  
-   Definição do tipo subjacente dos itens na **fontes de dados** janela.  
  
-   Criando controles que exibem dados arrastando itens dos **fontes de dados** janela em um formulário.  
  
-   Adicionar controles para exibir os dados no formulário.  
  
-   Concluindo a **construtor de critérios de pesquisa** caixa de diálogo.  
  
-   Inserir parâmetros no formulário e executar a consulta parametrizada.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind.  
  
## <a name="create-the-windows-application"></a>Criar o aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**. Atribuir um nome para o projeto é opcional nesta etapa, mas você dar a ele um nome aqui porque você salvá-lo mais tarde.  
  
#### <a name="to-create-the-new-windows-application-project"></a>Para criar o novo projeto de Aplicativo do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `WindowsSearchForm`.  
  
3.  Selecione **aplicativo do Windows** e clique em **Okey**.  
  
     O **WindowsSearchForm** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="create-the-data-source"></a>Criar a fonte de dados  
 Esta etapa cria uma fonte de dados de um banco de dados usando o **configuração de fonte de dados** assistente. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [bancos de dados de exemplo de instalar o SQL Server](../data-tools/install-sql-server-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **configuração de fonte de dados** assistente.  
  
3.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** página faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.  
  
7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.  
  
8.  Selecione o **clientes** tabela e, em seguida, clique em **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o **clientes** tabela aparece no **fontes de dados** janela.  
  
## <a name="create-the-form"></a>Criar o formulário  
 Você pode criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>Para criar controles de associação de dados no formulário  
  
1.  Expanda o **clientes** nó na **fontes de dados** janela.  
  
2.  Arraste o **clientes** nó a partir do **fontes de dados** janela ao seu formulário.  
  
     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
## <a name="addparameterization-search-functionality-to-the-query"></a>Addparameterization (funcionalidade Pesquisar) à consulta  
 Você pode adicionar uma cláusula WHERE à consulta original usando o **construtor de critérios de pesquisa** caixa de diálogo.  
  
#### <a name="to-create-a-parameterized-query-and-controls-to-enter-the-parameters"></a>Para criar uma consulta parametrizada e controles para inserir os parâmetros  
  
1.  Selecione o <xref:System.Windows.Forms.DataGridView> controlar e, em seguida, escolha **Add Query** sobre o **dados** menu.  
  
2.  Tipo `FillByCity` no **nome da nova consulta** área o **Pesquisar Construtor de critérios** caixa de diálogo.  
  
3.  Adicione `WHERE City = @City` para a consulta na **texto da consulta** área.  
  
     A consulta deve ser semelhante ao seguinte:  
  
     `SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax`  
  
     `FROM Customers`  
  
     `WHERE City = @City`  
  
    > [!NOTE]
    >  Fontes de dados do Access e o OLE DB usam o ponto de interrogação ('? ') para denotar parâmetros, portanto, a cláusula WHERE seria algo como este: `WHERE City = ?`.  
  
4.  Clique em **Okey** para fechar o **construtor de critérios de pesquisa** caixa de diálogo.  
  
     Um **FillByCityToolStrip** é adicionado ao formulário.  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
 A execução do aplicativo abre o formulário pronto para receber o parâmetro como entrada.  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Pressione F5 para executar o aplicativo.  
  
2.  Tipo **Londres** para o **City** caixa de texto e clique **FillByCity**.  
  
     A grade de dados é preenchida com os clientes que atendem aos critérios. Neste exemplo, a grade de dados exibe clientes que têm um valor de **Londres** em seus **City** coluna.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após criar um formulário parametrizado. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:  
  
-   Adicionar controles que exibem dados relacionados. Para obter mais informações, consulte [Como exibir dados relacionados em um aplicativo dos Windows Forms](../data-tools/how-to-display-related-data-in-a-windows-forms-application.md).  
  
-   Editando o conjunto de dados para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

