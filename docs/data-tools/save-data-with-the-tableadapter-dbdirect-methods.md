---
title: Salvar os dados com os métodos TableAdapter DBDirect
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 77d7aa0859ee383258f80dfd74f36d584790e464
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281603"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>Salvar os dados com os métodos TableAdapter DBDirect

Este tutorial fornece instruções detalhadas para executar instruções SQL diretamente em um banco de dados usando os métodos DBDirect de um TableAdapter. Os métodos DBDirect de um TableAdapter fornecem um bom nível de controle sobre as atualizações do seu banco de dados. Você pode usá-los para executar instruções SQL específicas e procedimentos armazenados chamando os `Insert` métodos individuais, `Update` e `Delete` conforme necessário pelo seu aplicativo (em oposição ao `Update` método sobrecarregado que executa as instruções UPDATE, INSERT e Delete em uma única chamada).

Durante este passo a passo, você aprenderá a:

- Crie um novo **aplicativo Windows Forms**.

- Crie e configure um conjunto de dados com o [Assistente de configuração de fonte de dados](../data-tools/media/data-source-configuration-wizard.png).

- Selecionar o controle a ser criado no formulário ao arrastar itens da janela **Fontes de Dados**. Para obter mais informações, consulte [definir o controle a ser criado ao arrastar da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

- Cria controles de associação de dados arrastando itens da janela **Fontes de Dados** para um formulário.

- Adicione métodos para acessar diretamente o banco de dados e executar inserções, atualizações e exclusões.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms

A primeira etapa é criar um **aplicativo Windows Forms**.

1. No Visual Studio, no menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Expanda o **Visual C#** ou **Visual Basic** no painel esquerdo e, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione o tipo de projeto **Windows Forms aplicativo** .

4. Nomeie o projeto **TableAdapterDbDirectMethodsWalkthrough**e escolha **OK**.

     O projeto **TableAdapterDbDirectMethodsWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="create-a-data-source-from-your-database"></a>Criar uma fonte de dados do seu banco de dados

Esta etapa usa o **Assistente de Configuração de Fonte de Dados** para criar uma fonte de dados com base na tabela `Region` no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [How to: Install exemplo databases](../data-tools/installing-database-systems-tools-and-samples.md).

### <a name="to-create-the-data-source"></a>Para criar a fonte de dados

1. No menu **dados** , selecione **mostrar fontes de dados**.

   A janela **Fontes de Dados** é aberta.

2. Na janela **fontes de dados** , selecione **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Na tela **escolher um tipo de fonte de dados** , selecione **banco**de dado e, em seguida, selecione **Avançar**.

4. Na tela **escolher sua conexão de dados** , siga um destes procedimentos:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

         -ou-

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o seu banco de dados exigir uma senha, selecione a opção para incluir um dado confidencial e, em seguida, selecione **Avançar**.

6. Na tela **salvar cadeia de conexão no arquivo de configuração do aplicativo** , selecione **Avançar**.

7. Na tela **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione a `Region` tabela e, em seguida, selecione **concluir**.

     O **NorthwindDataSet** é adicionado ao projeto e a tabela `Region` aparece na janela **Fontes de Dados**.

## <a name="add-controls-to-the-form-to-display-the-data"></a>Adicionar controles ao formulário para exibir os dados

Crie controles de associação de dados arrastando itens da janela **Fontes de Dados** para seu formulário.

Para criar controles associados a dados no Windows Form, arraste o nó da **região** principal da janela **fontes de dados** para o formulário.

Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `RegionTableAdapter` , <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja do componente.

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>Para adicionar botões que chamam os métodos individuais DbDirect de um TableAdapter

1. Arraste três controles <xref:System.Windows.Forms.Button> da **Caixa de Ferramentas** para **Form1** (abaixo de **RegionDataGridView**).

2. Defina as propriedades **Nome** e **Texto** a seguir em cada botão.

    |Nome|Texto|
    |----------|----------|
    |`InsertButton`|**Inserir**|
    |`UpdateButton`|**Atualização**|
    |`DeleteButton`|**Delete (excluir)**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>Para adicionar código para inserir novos registros no banco de dados

1. Selecione **InsertButton** para criar um manipulador de eventos para o evento de clique e abra o formulário no editor de código.

2. Substitua o manipulador de eventos `InsertButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#1](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_1.vb)]
     [!code-csharp[VbRaddataSaving#1](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_1.cs)]

### <a name="to-add-code-to-update-records-in-the-database"></a>Para adicionar código para atualizar registros no banco de dados

1. Clique duas vezes em **UpdateButton** para criar um manipulador de eventos para o evento Click e abrir o formulário no editor de códigos.

2. Substitua o manipulador de eventos `UpdateButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#2](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_2.vb)]
     [!code-csharp[VbRaddataSaving#2](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_2.cs)]

### <a name="to-add-code-to-delete-records-from-the-database"></a>Para adicionar código para excluir registros do banco de dados

1. Selecione **DeleteButton** para criar um manipulador de eventos para o evento de clique e abra o formulário no editor de código.

2. Substitua o manipulador de eventos `DeleteButton_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#3](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_3.vb)]
     [!code-csharp[VbRaddataSaving#3](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_3.cs)]

## <a name="run-the-application"></a>Executar o aplicativo

- Selecione **F5** para executar o aplicativo.

- Selecione o botão **Inserir** e verifique se o novo registro aparece na grade.

- Selecione o botão **Atualizar** e verifique se o registro está atualizado na grade.

- Selecione o botão **excluir** e verifique se o registro foi removido da grade.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, há várias etapas que você pode querer executar depois de criar um formulário associado a dados. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:

- Adicionando funcionalidade de busca ao formulário.

- Adicionar tabelas ao conjunto de dados, selecionando **Configurar DataSet com Assistente** na janela **Fontes de Dados**. Você pode adicionar controles que exibem dados relacionados, arrastando os nós relacionados para o formulário. Para obter mais informações, consulte [relações em conjuntos de](relationships-in-datasets.md)dados.

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
