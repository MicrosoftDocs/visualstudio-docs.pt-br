---
title: Tratar uma exceção de simultaneidade
ms.date: 09/11/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- concurrency control, exceptions
- datasets [Visual Basic], errors
- exception handling, concurrency issues
- data concurrency, walkthroughs
- updating datasets, errors
- concurrency control, walkthroughs
ms.assetid: 73ee9759-0a90-48a9-bf7b-9d6fc17bff93
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9d1c151b7f3afe977786ef3b308eff2de1c0857f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282352"
---
# <a name="handle-a-concurrency-exception"></a>Tratar uma exceção de simultaneidade

As exceções de simultaneidade ( <xref:System.Data.DBConcurrencyException?displayProperty=fullName> ) são geradas quando dois usuários tentam alterar os mesmos dados em um banco de dado ao mesmo tempo. Neste tutorial, você cria um aplicativo do Windows que ilustra como pegar um <xref:System.Data.DBConcurrencyException> , localizar a linha que causou o erro e aprender uma estratégia de como tratá-lo.

Este passo a passos percorre o seguinte processo:

1. Para criar um novo projeto de **Aplicativo do Windows Forms**.

2. Crie um novo conjunto de uma com base na tabela clientes Northwind.

3. Crie um formulário com um <xref:System.Windows.Forms.DataGridView> para exibir os dados.

4. Preencha um DataSet com dados da tabela Customers no banco de dados Northwind.

5. Use o recurso **Mostrar dados de tabela** no **Gerenciador de servidores** para acessar os dados da tabela clientes e alterar um registro.

6. Altere o mesmo registro para um valor diferente, atualize o conjunto de dados e tente gravar as alterações no banco de dados, o que resulta em um erro de simultaneidade sendo gerado.

7. Capture o erro e exiba as diferentes versões do registro, permitindo que o usuário determine se deseja continuar e atualizar o banco de dados ou cancelar a atualização.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-new-project"></a>Criar um novo projeto

Comece criando um novo aplicativo Windows Forms:

1. No Visual Studio, no menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Expanda o **Visual C#** ou **Visual Basic** no painel esquerdo e, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione o tipo de projeto **Windows Forms aplicativo** .

4. Nomeie o projeto **ConcurrencyWalkthrough**e escolha **OK**.

     O projeto **ConcurrencyWalkthrough** é criado e adicionado ao **Gerenciador de soluções**, e um novo formulário é aberto no designer.

## <a name="create-the-northwind-dataset"></a>Criar o conjunto de conjuntos Northwind

Em seguida, crie um conjunto de um DataSet chamado **NorthwindDataSet**:

1. No menu **dados** , escolha **Adicionar nova fonte de dados**.

   O Assistente de Configuração de Fonte de Dados é aberto.

2. Na tela **escolher um tipo de fonte de dados** , selecione **Database**.

   ![Assistente de configuração de fonte de dados no Visual Studio](media/data-source-configuration-wizard.png)

3. Selecione uma conexão com o banco de dados de exemplo Northwind na lista de conexões disponíveis. Se a conexão não estiver disponível na lista de conexões, selecione **nova conexão**.

    > [!NOTE]
    > Se você estiver se conectando a um arquivo de banco de dados local, selecione **não** quando for perguntado se você deseja adicionar o arquivo ao seu projeto.

4. Na tela **salvar cadeia de conexão no arquivo de configuração do aplicativo** , selecione **Avançar**.

5. Expanda o nó **tabelas** e selecione a tabela **clientes** . O nome padrão do conjunto de os deve ser **NorthwindDataSet**.

6. Selecione **concluir** para adicionar o conjunto de os ao projeto.

## <a name="create-a-data-bound-datagridview-control"></a>Criar um controle DataGridView associado a dados

Nesta seção, você cria um <xref:System.Windows.Forms.DataGridView?displayProperty=nameWithType> arrastando o item **clientes** da janela **fontes de dados** para seu formulário do Windows.

1. Para abrir a janela **fontes de dados** , no menu **dados** , escolha **mostrar fontes de dados**.

2. Na janela **fontes de dados** , expanda o nó **NorthwindDataSet** e selecione a tabela **Customers** .

3. Selecione a seta para baixo no nó da tabela e, em seguida, selecione **DataGridView** na lista suspensa.

4. Arraste a tabela para uma área vazia do formulário.

     Um <xref:System.Windows.Forms.DataGridView> controle chamado **customersDataGridView**e um <xref:System.Windows.Forms.BindingNavigator> **CustomersBindingNavigator**nomeado é adicionado ao formulário associado ao <xref:System.Windows.Forms.BindingSource> . Isso é, por sua vez, associado à tabela Customers no NorthwindDataSet.

## <a name="test-the-form"></a>Testar o formulário

Agora você pode testar o formulário para certificar-se de que ele se comporta conforme o esperado até este ponto:

1. Selecione **F5** para executar o aplicativo.

     O formulário é exibido com um <xref:System.Windows.Forms.DataGridView> controle que é preenchido com dados da tabela Customers.

2. No menu **Depurar**, selecione **Interromper Depuração**.

## <a name="handle-concurrency-errors"></a>Tratar erros de simultaneidade

A maneira como você lida com erros depende das regras de negócios específicas que regem seu aplicativo. Para esta explicação, usamos a seguinte estratégia como um exemplo de como tratar o erro de simultaneidade.

O aplicativo apresenta ao usuário três versões do registro:

- O registro atual no banco de dados

- O registro original que é carregado no conjunto de registros

- As alterações propostas no conjunto de

Em seguida, o usuário pode substituir o banco de dados pela versão proposta ou cancelar a atualização e atualizar o DataSet com os novos valores do banco de dados.

### <a name="to-enable-the-handling-of-concurrency-errors"></a>Para habilitar o tratamento de erros de simultaneidade

1. Crie um manipulador de erro personalizado.

2. Exibe as opções para o usuário.

3. Processar a resposta do usuário.

4. Reenvie a atualização ou redefina os dados no DataSet.

### <a name="add-code-to-handle-the-concurrency-exception"></a>Adicionar código para manipular a exceção de simultaneidade

Quando você tenta executar uma atualização e uma exceção é gerada, geralmente você deseja fazer algo com as informações fornecidas pela exceção gerada. Nesta seção, você adiciona o código que tenta atualizar o banco de dados. Você também lida com qualquer um <xref:System.Data.DBConcurrencyException> que possa ser gerado, bem como outras exceções.

> [!NOTE]
> Os `CreateMessage` `ProcessDialogResults` métodos e são adicionados posteriormente no passo a passos.

1. Adicione o seguinte código abaixo do `Form1_Load` método:

   [!code-csharp[VbRaddataConcurrency#1](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_1.cs)]
   [!code-vb[VbRaddataConcurrency#1](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_1.vb)]

2. Substitua o `CustomersBindingNavigatorSaveItem_Click` método para chamar o `UpdateDatabase` método para que fique semelhante ao seguinte:

   [!code-csharp[VbRaddataConcurrency#2](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_2.cs)]
   [!code-vb[VbRaddataConcurrency#2](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_2.vb)]

### <a name="display-choices-to-the-user"></a>Exibir opções para o usuário

O código que você acabou de escrever chama o `CreateMessage` procedimento para exibir informações de erro para o usuário. Para esta explicação, você usa uma caixa de mensagem para exibir as diferentes versões do registro para o usuário. Isso permite que o usuário escolha se deseja substituir o registro com as alterações ou cancelar a edição. Quando o usuário seleciona uma opção (clica em um botão) na caixa de mensagem, a resposta é passada para o `ProcessDialogResult` método.

Crie a mensagem adicionando o código a seguir ao **Editor de código**. Insira este código abaixo do `UpdateDatabase` método:

[!code-csharp[VbRaddataConcurrency#4](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_3.cs)]
[!code-vb[VbRaddataConcurrency#4](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_3.vb)]

### <a name="process-the-users-response"></a>Processar a resposta do usuário

Você também precisa de código para processar a resposta do usuário para a caixa de mensagem. As opções são substituir o registro atual no banco de dados pela alteração proposta, ou abandonar as alterações locais e atualizar a tabela data com o registro que está atualmente no banco de dado. Se o usuário escolher **Sim**, o <xref:System.Data.DataTable.Merge%2A> método será chamado com o argumento *PreserveChanges* definido como **true**. Isso faz com que a tentativa de atualização seja bem-sucedida, porque a versão original do registro agora corresponde ao registro no banco de dados.

Adicione o código a seguir abaixo do código que foi adicionado na seção anterior:

[!code-csharp[VbRaddataConcurrency#3](../data-tools/codesnippet/CSharp/handle-a-concurrency-exception_4.cs)]
[!code-vb[VbRaddataConcurrency#3](../data-tools/codesnippet/VisualBasic/handle-a-concurrency-exception_4.vb)]

## <a name="test-the-form"></a>Testar o formulário

Agora, é possível testar o formulário para garantir que ele se comporta da forma esperada. Para simular uma violação de simultaneidade, você altera os dados no banco de dado depois de preencher o NorthwindDataSet.

1. Selecione **F5** para executar o aplicativo.

2. Depois que o formulário for exibido, deixe-o em execução e alterne para o IDE do Visual Studio.

3. No menu **Exibir**, escolha **Gerenciador de Servidores**.

4. Em **Gerenciador de servidores**, expanda a conexão que seu aplicativo está usando e, em seguida, expanda o nó **tabelas** .

5. Clique com o botão direito do mouse na tabela **clientes** e selecione **Mostrar dados da tabela**.

6. No primeiro registro (**ALFKI**), altere **ContactName** para **Maria Anders2**.

    > [!NOTE]
    > Navegue até uma linha diferente para confirmar a alteração.

7. Alterne para o formulário em execução do ConcurrencyWalkthrough.

8. No primeiro registro no formulário (**ALFKI**), altere **ContactName** para **Maria anders1**.

9. Selecione o botão **Salvar**.

     O erro de simultaneidade é gerado e a caixa de mensagem é exibida.

   A seleção de **não** cancela a atualização e atualiza o conjunto de dados com os valores que estão no momento. Selecionar **Sim** grava o valor proposto no banco de dados.

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
