---
title: Salvar dados com o TableAdapter DBDirect métodos | Microsoft Docs
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
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 6b7a7ec1d244f8bf711f0d1aaf4726c910846357
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219712"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>Salvar os dados com os métodos TableAdapter DBDirect
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este passo a passo fornece instruções detalhadas para executar instruções SQL diretamente em um banco de dados usando os métodos DBDirect de um TableAdapter. Os métodos DBDirect de um TableAdapter fornecem um bom nível de controle sobre as atualizações de banco de dados. Você pode usá-los para executar instruções SQL específicas e procedimentos armazenados, chamando o indivíduo `Insert`, `Update`, e `Delete` métodos conforme exigido pelo seu aplicativo (em vez de sobrecarregado `Update` método que executa a atualização INSERT e DELETE instruções todas em uma chamada).  
  
 Durante este passo a passo, você aprenderá a:  
  
-   Criar um novo **aplicativo do Windows**.  
  
-   Criar e configurar um conjunto de dados com o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Selecione o controle a ser criado no formulário ao arrastar itens dos **fontes de dados** janela. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
-   Criar um formulário de associação de dados arrastando itens dos **fontes de dados** janela para o formulário.  
  
-   Adicionar métodos para acessar o banco de dados diretamente e executar inserções, atualizações e exclusões...  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-a-windows-application"></a>Criar um aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**.  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  No Visual Studio, sobre o **arquivo** menu, crie uma nova **projeto**.  
  
2.  Nomeie o projeto **TableAdapterDbDirectMethodsWalkthrough**.  
  
3.  Selecione **aplicativo do Windows**e, em seguida, selecione **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **TableAdapterDbDirectMethodsWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados  
 Esta etapa usa a **Data Source Configuration Wizard** para criar uma fonte de dados com base no `Region` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, selecione **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3.  Sobre o **escolher um tipo de fonte de dados** tela, selecione **banco de dados**e, em seguida, selecione **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** tela, siga um destes procedimentos:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
         -ou-  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, selecione **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** tela, selecione **próxima**.  
  
7.  Sobre o **Choose your Database Objects** , expanda o **tabelas** nó.  
  
8.  Selecione o `Region` de tabela e, em seguida, selecione **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o `Region` tabela aparece no **fontes de dados** janela.  
  
## <a name="addcontrols-to-the-form-to-display-the-data"></a>Addcontrols ao formulário para exibir os dados  
 Criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Para criar dados de associação de controles do formulário do Windows  
  
-   Arraste principal **região** nó a partir do **fontes de dados** janela para o formulário.  
  
     Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [RegionTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
#### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>Para adicionar botões que chamam os métodos individuais DbDirect de um TableAdapter  
  
1.  Arraste três <xref:System.Windows.Forms.Button> controles do **caixa de ferramentas** até **Form1** (abaixo de **RegionDataGridView**).  
  
2.  Defina o seguinte **nome** e **texto** propriedades em cada botão.  
  
    |Nome|Texto|  
    |----------|----------|  
    |`InsertButton`|**Inserir**|  
    |`UpdateButton`|**Atualizar**|  
    |`DeleteButton`|**Excluir**|  
  
#### <a name="to-add-code-to-insert-new-records-into-the-database"></a>Para adicionar código para inserir novos registros no banco de dados  
  
1.  Selecione **InsertButton** para criar um manipulador de eventos para o evento click e abrir o formulário no editor de códigos.  
  
2.  Substitua o manipulador de eventos `InsertButton_Click` pelo seguinte código:  
  
     [!code-csharp[VbRaddataSaving#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#1)]
     [!code-vb[VbRaddataSaving#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#1)]  
  
#### <a name="to-add-code-to-update-records-in-the-database"></a>Para adicionar código para atualizar registros no banco de dados  
  
1.  Clique duas vezes o **UpdateButton** para criar um manipulador de eventos para o evento click e abrir o formulário no editor de códigos.  
  
2.  Substitua o manipulador de eventos `UpdateButton_Click` pelo seguinte código:  
  
     [!code-csharp[VbRaddataSaving#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#2)]
     [!code-vb[VbRaddataSaving#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#2)]  
  
#### <a name="to-add-code-to-delete-records-from-the-database"></a>Para adicionar código para excluir registros do banco de dados  
  
1.  Selecione **DeleteButton** para criar um manipulador de eventos para o evento click e abrir o formulário no editor de códigos.  
  
2.  Substitua o manipulador de eventos `DeleteButton_Click` pelo seguinte código:  
  
     [!code-csharp[VbRaddataSaving#3](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form1.cs#3)]
     [!code-vb[VbRaddataSaving#3](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form1.vb#3)]  
  
## <a name="run-the-application"></a>Executar o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Selecione **F5** para executar o aplicativo.  
  
-   Selecione o **inserir** botão e, em seguida, verifique se o novo registro aparece na grade.  
  
-   Selecione o **atualização** botão e, em seguida, verifique se o registro é atualizado na grade.  
  
-   Selecione o **excluir** botão e, em seguida, verifique se o registro é removido da grade.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, há várias etapas que você talvez queira realizar após criar um formulário de associação de dados. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:  
  
-   Adicionando funcionalidade de busca ao formulário. Para obter mais informações, consulte [como: adicionar uma consulta parametrizada a um aplicativo do Windows Forms](http://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416).  
  
-   Adicionar tabelas ao conjunto de dados, selecionando **configurar DataSet com assistente** de dentro de **fontes de dados** janela. Você pode adicionar controles que exibem dados relacionados, arrastando os nós relacionados para o formulário. Para obter mais informações, consulte [Como exibir dados relacionados em um aplicativo dos Windows Forms](../data-tools/how-to-display-related-data-in-a-windows-forms-application.md).  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)

