---
title: 'Passo a passo: Exibindo dados em um formulário do Windows | Microsoft Docs'
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
- displaying data on forms, walkthroughs
- Windows Forms, displaying data
- Windows applications, displaying data
- data binding, Windows Forms
- data [Visual Studio], displaying on Windows Forms
- forms, displaying data
ms.assetid: f6e08c2c-c792-43de-adf3-3e52c0100225
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: f623f639458a9f5c9c055b5d6de384f6fd39cad1
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49201195"
---
# <a name="walkthrough-displaying-data-on-a-windows-form"></a>Instruções passo a passo: exibindo dados em um Windows Form
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um dos cenários mais comuns no desenvolvimento de aplicativos é exibir dados de um formulário em um aplicativo baseado no Windows. Você pode exibir dados em um formulário arrastando itens dos [janela fontes de dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992) para o formulário. Este passo a passo cria um formulário simples que exibe dados de uma única tabela em vários controles individuais. Este exemplo usa a tabela `Customers` do banco de dados de exemplo Northwind.  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criando um novo **aplicativo do Windows** projeto.  
  
-   Criando e configurando um conjunto de dados com o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Selecionando o controle a ser criado no formulário ao arrastar itens dos **fontes de dados** janela. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
-   Criando um controle associado a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="creating-the-windows-application"></a>Criando o aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows** projeto.  
  
#### <a name="to-create-the-new-windows-application-project"></a>Para criar o novo projeto de Aplicativo do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `DisplayingDataonaWindowsForm`.  
  
3.  Selecione **aplicativo do Windows** e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **DisplayingDataonaWindowsForm** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="creating-the-data-source"></a>Criando a Fonte de Dados  
 Esta etapa cria uma fonte de dados usando o **Data Source Configuration Wizard** com base no `Customers` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** página faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
         -ou-  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo...  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **próxima**.  
  
6.  Clique em **próxima** sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** página.  
  
7.  Expanda o **tabelas** nó na **Choose your Database Objects** página.  
  
8.  Selecione o **clientes** tabela e, em seguida, clique em **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o **clientes** tabela aparece no **fontes de dados** janela.  
  
## <a name="setting-the-controls-to-be-created"></a>Configurando os controles a serem criados  
 Este passo a passo os dados estarão em um **detalhes** layout onde os dados são exibidos em controles individuais. (A abordagem alternativa é o padrão **grade** layout no qual os dados são exibidos em um <xref:System.Windows.Forms.DataGridView> controle.)  
  
#### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>Definir o tipo de remoção dos itens na Janela Fontes de Dados  
  
1.  Expanda o **clientes** nó na **fontes de dados** janela.  
  
2.  Alterar o tipo de descarte a **clientes** de tabela para **detalhes** selecionando **detalhes** na lista suspensa o **clientes** nó. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
3.  Alterar o **CustomerID** tipo de descarte da coluna para um rótulo selecionando **rótulo** da lista de controle a **CustomerID** nó.  
  
## <a name="creating-the-form"></a>Criando o formulário  
 Criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-form"></a>Para criar controles de associação de dados no formulário  
  
-   Arraste principal **clientes** nó a partir do **fontes de dados** janela para o formulário.  
  
     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Pressione F5.  
  
-   Navegue nos registros usando o controle <xref:System.Windows.Forms.BindingNavigator>.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, existem várias etapas que você talvez queira realizar após criar um Windows Form de associação de dados. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:  
  
-   Adicionando funcionalidade de busca ao formulário. Para obter mais informações, consulte [como: adicionar uma consulta parametrizada a um aplicativo do Windows Forms](http://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416).  
  
-   Adicionar a funcionalidade para enviar atualizações de volta ao banco de dados. Para obter mais informações, consulte [instruções passo a passo: salvando dados para um banco de dados (tabela única)](http://msdn.microsoft.com/library/68befa96-7463-43e8-abcf-dc2f42ccd53d).  
  
-   Adicionando o `Orders` tabela ao conjunto de dados, selecionando **configurar DataSet com assistente** de dentro de **fontes de dados** janela. Em seguida, você pode adicionar controles que exibem dados relacionados, arrastando o **pedidos** nó (abaixo a **Fax** coluna dentro a **clientes** tabela) para o formulário. Para obter mais informações, consulte [Como exibir dados relacionados em um aplicativo dos Windows Forms](../data-tools/how-to-display-related-data-in-a-windows-forms-application.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)