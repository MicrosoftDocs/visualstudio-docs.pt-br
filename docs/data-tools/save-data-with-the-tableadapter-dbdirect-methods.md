---
title: Salvar os dados com os métodos TableAdapter DBDirect
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: ef1860274c9234774b8af42525a0215d9468a858
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52304565"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>Salvar os dados com os métodos TableAdapter DBDirect

Este passo a passo fornece instruções detalhadas para executar instruções SQL diretamente em um banco de dados usando os métodos DBDirect de um TableAdapter. Os métodos DBDirect de um TableAdapter fornecem um bom nível de controle sobre as atualizações do seu banco de dados. Você pode usá-los para executar instruções SQL específicas e procedimentos armazenados, chamando o indivíduo `Insert`, `Update`, e `Delete` métodos conforme exigido pelo seu aplicativo (em vez de sobrecarregado `Update` método que executa a atualização INSERT e DELETE instruções todas em uma chamada).

Durante este passo a passo, você aprenderá a:

-   Criar um novo **Aplicativo do Windows Forms**.

-   Criar e configurar um conjunto de dados com o [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png).

-   Selecionar o controle a ser criado no formulário ao arrastar itens da janela **Fontes de Dados**. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

-   Cria controles de associação de dados arrastando itens da janela **Fontes de Dados** para um formulário.

-   Adicione métodos para acessar o banco de dados diretamente e executar inserções, atualizações e exclusões.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms

A primeira etapa é criar uma **aplicativo do Windows Forms**.

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **TableAdapterDbDirectMethodsWalkthrough**e, em seguida, escolha **Okey**.

     O projeto **TableAdapterDbDirectMethodsWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do banco de dados

Esta etapa usa o **Assistente de Configuração de Fonte de Dados** para criar uma fonte de dados com base na tabela `Region` no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar bancos de dados de exemplo](../data-tools/installing-database-systems-tools-and-samples.md).

### <a name="to-create-the-data-source"></a>Para criar a fonte de dados

1. Sobre o **dados** menu, selecione **Show Data Sources**.

   A janela **Fontes de Dados** é aberta.

2. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o **Assistente de Configuração de Fonte de Dados**.

3. Sobre o **escolher um tipo de fonte de dados** tela, selecione **banco de dados**e, em seguida, selecione **próxima**.

4. Sobre o **escolha sua Conexão de dados** tela, siga um destes procedimentos:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

         -ou-

    -   Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, selecione **próxima**.

6. Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** tela, selecione **próxima**.

7. Sobre o **Choose your Database Objects** , expanda o **tabelas** nó.

8. Selecione o `Region` de tabela e, em seguida, selecione **concluir**.

     O **NorthwindDataSet** é adicionado ao projeto e a tabela `Region` aparece na janela **Fontes de Dados**.

## <a name="add-controls-to-the-form-to-display-the-data"></a>Adicionar controles ao formulário para exibir os dados

Crie controles de associação de dados arrastando itens da janela **Fontes de Dados** para seu formulário.

Para criar controles associados a dados do formulário do Windows, arraste principal **região** nó a partir do **fontes de dados** janela para o formulário.

Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `RegionTableAdapter`, <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>Para adicionar botões que chamam os métodos individuais DbDirect de um TableAdapter

1. Arraste três controles <xref:System.Windows.Forms.Button> da **Caixa de Ferramentas** para **Form1** (abaixo de **RegionDataGridView**).

2. Defina as propriedades **Nome** e **Texto** a seguir em cada botão.

    |Nome|Texto|
    |----------|----------|
    |`InsertButton`|**Inserir**|
    |`UpdateButton`|**Atualizar**|
    |`DeleteButton`|**Excluir**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>Para adicionar código para inserir novos registros no banco de dados

1. Selecione **InsertButton** para criar um manipulador de eventos para o evento click e abrir o formulário no editor de códigos.

2. Substitua o manipulador de eventos `InsertButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#1](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_1.vb)]
     [!code-csharp[VbRaddataSaving#1](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_1.cs)]

### <a name="to-add-code-to-update-records-in-the-database"></a>Para adicionar código para atualizar registros no banco de dados

1. Clique duas vezes em **UpdateButton** para criar um manipulador de eventos para o evento Click e abrir o formulário no editor de códigos.

2. Substitua o manipulador de eventos `UpdateButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#2](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_2.vb)]
     [!code-csharp[VbRaddataSaving#2](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_2.cs)]

### <a name="to-add-code-to-delete-records-from-the-database"></a>Para adicionar código para excluir registros do banco de dados

1. Selecione **DeleteButton** para criar um manipulador de eventos para o evento click e abrir o formulário no editor de códigos.

2. Substitua o manipulador de eventos `DeleteButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#3](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_3.vb)]
     [!code-csharp[VbRaddataSaving#3](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_3.cs)]

## <a name="run-the-application"></a>Executar o aplicativo

-   Selecione **F5** para executar o aplicativo.

-   Selecione o **inserir** botão e, em seguida, verifique se o novo registro aparece na grade.

-   Selecione o **atualização** botão e, em seguida, verifique se o registro é atualizado na grade.

-   Selecione o **excluir** botão e, em seguida, verifique se o registro é removido da grade.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, há várias etapas que você talvez queira realizar após criar um formulário de associação de dados. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:

-   Adicionando funcionalidade de busca ao formulário.

-   Adicionar tabelas ao conjunto de dados, selecionando **Configurar DataSet com Assistente** na janela **Fontes de Dados**. Você pode adicionar controles que exibem dados relacionados, arrastando os nós relacionados para o formulário. Para obter mais informações, consulte [relacionamentos em conjuntos de dados](relationships-in-datasets.md).

## <a name="see-also"></a>Consulte também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)