---
title: 'Passo a passo: personalizando a inserção, a atualização e o comportamento de exclusão de classes de entidade'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 03ff1146-706e-4780-91cb-56a83df63eea
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: f665d860597bc99d7c9e496c115a82a60d596e09
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305527"
---
# <a name="walkthrough-customize-the-insert-update-and-delete-behavior-of-entity-classes"></a>Passo a passo: Personalizar o insert, update e o comportamento de exclusão de classes de entidade

O [LINQ to SQL das ferramentas no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornece uma superfície de design visual para criar e editar o LINQ para SQL classes (classes de entidade) que são baseadas em objetos em um banco de dados. Usando [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index), você pode usar a tecnologia LINQ para acessar bancos de dados SQL. Para saber mais, confira [LINQ (consulta integrada à linguagem)](/dotnet/csharp/linq/).

Por padrão, a lógica para executar atualizações é fornecida pelo LINQ to SQL de tempo de execução. O tempo de execução cria padrão `Insert`, `Update`, e `Delete` instruções com base no esquema da tabela (as definições de coluna e informações de chave primária). Quando você não deseja usar o comportamento padrão, poderá configurar o comportamento de atualização e designar procedimentos armazenados específicos para executar as inserções, as atualizações e as exclusões necessárias para trabalhar com os dados no banco de dados. Você também pode fazer isso quando o comportamento padrão não é gerado, por exemplo, quando as classes de entidade mapeiam para as exibições. Além disso, você pode substituir o comportamento de atualização padrão quando o banco de dados exige acesso à tabela por meio dos procedimentos armazenados. Para obter mais informações, consulte [personalizando operações usando procedimentos armazenados](/dotnet/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures).

> [!NOTE]
> Essa explicação passo a passo exige a disponibilidade dos procedimentos armazenados **InsertCustomer**, **UpdateCustomer** e **DeleteCustomer** para o banco de dados Northwind.

Essa explicação passo a passo fornece as etapas que você deve seguir para substituir o comportamento padrão de tempo de execução LINQ to SQL para salvar dados de volta para um banco de dados usando procedimentos armazenados.

Durante este passo a passo, você aprenderá a executar as seguintes tarefas:

-   Criar um novo aplicativo Windows Forms e adicione um LINQ para o arquivo SQL a ele.

-   Criar uma classe de entidade que é mapeada para o Northwind `Customers` tabela.

-   Criar uma fonte de dados de objeto que referencia o LINQ to SQL `Customer` classe.

-   Criar um formulário do Windows que contém um <xref:System.Windows.Forms.DataGridView> que está associado a `Customer` classe.

-   Implemente a funcionalidade de salvar para o formulário.

-   Crie <xref:System.Data.Linq.DataContext> métodos adicionando procedimentos armazenados para o **Relational Designer**.

-   Configurar o `Customer` classe usar procedimentos armazenados para executar inserções, atualizações e exclusões.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (**Pesquisador de objetos do SQL Server** é instalado como parte do **armazenamento de dados e processamento** carga de trabalho no **instalador do Visual Studio**.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="creating-an-application-and-adding-linq-to-sql-classes"></a>Criando um aplicativo e adicionando classes LINQ to SQL

Porque você está trabalhando com LINQ para classes SQL e exibindo os dados em um formulário do Windows, crie um novo aplicativo Windows Forms e adicione um LINQ ao arquivo de Classes do SQL.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-a-new-windows-forms-application-project-that-contains-linq-to-sql-classes"></a>Para criar um novo projeto de aplicativo do Windows Forms que contém o LINQ para classes SQL

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **UpdatingWithSProcsWalkthrough**e, em seguida, escolha **Okey**.

     O projeto de **UpdatingWithSProcsWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

4.  No menu **Projeto**, clique em **Adicionar Novo Item**.

5.  Clique no modelo **Classes LINQ to SQL** e digite **Northwind.dbml** na caixa **Nome**.

6.  Clique em **Adicionar**.

     Um vazio arquivo LINQ to SQL Classes (**dbml**) é adicionado ao projeto e o **Relational Designer** é aberta.

## <a name="create-the-customer-entity-class-and-object-data-source"></a>Criar cliente entidade classe e objeto de fonte de dados

Criar LINQ to SQL classes são mapeadas para tabelas de banco de dados arrastando tabelas do **Gerenciador de servidores** ou **Database Explorer** até o **Relational Designer**. O resultado são classes de entidade do LINQ to SQL que mapeiam para as tabelas no banco de dados. Depois de criar classes de entidade, elas podem ser usadas como fontes de dados de objeto assim como outras classes que têm propriedades públicas.

### <a name="to-create-a-customer-entity-class-and-configure-a-data-source-with-it"></a>Para criar uma classe de entidade Customer e configurar uma fonte de dados com ela

1.  Na **Gerenciador de servidores** ou **Database Explorer**, localize o **cliente** tabela na versão do SQL Server do banco de dados de exemplo Northwind.

2.  Arraste o **clientes** nó a partir **Gerenciador de servidores** ou **Database Explorer** para o **Relational Designer* superfície.

     Uma classe de entidade chamada **Customer** é criada. Ela tem propriedades que correspondem às colunas na tabela Customers. A classe de entidade é chamada de **Customer** (e não **Customers**) porque representa um único cliente da tabela Customers.

    > [!NOTE]
    > Esse comportamento de renomeação é chamado de *pluralização*. Ele pode ser ativado ou desativado [caixa de diálogo Opções](../ide/reference/options-dialog-box-visual-studio.md). Para obter mais informações, consulte [como: ative em pluralization e off (O/R Designer)](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md).

3.  No menu **Compilar**, clique em **Compilar UpdatingwithSProcsWalkthrough** para criar o projeto.

4.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

5.  Na janela **Fontes de Dados**, clique em **Adicionar Nova Fonte de Dados**.

6.  Clique em **Objeto** na página **Escolher um Tipo de Fonte de Dados** e clique em **Avançar**.

7.  Expanda o nó **UpdatingwithSProcsWalkthrough** e localize e selecione a classe **Customer**.

    > [!NOTE]
    > Se a classe **Customer** não estiver disponível, cancele o assistente, compile o projeto e execute o assistente novamente.
8.  Clique em **Concluir** para criar a fonte de dados e adicionar a classe de entidade **Customer** à janela **Fontes de Dados**.

## <a name="create-a-datagridview-to-display-the-customer-data-on-a-windows-form"></a>Criar um DataGridView para exibir os dados do cliente em um formulário do Windows

Crie controles que estão associados às classes de entidade arrastando o LINQ para itens de fonte de dados SQL do **fontes de dados** janela em um formulário do Windows.

### <a name="to-add-controls-that-are-bound-to-the-entity-classes"></a>Para adicionar controles que estão associados às classes de entidade

1.  Abra **Form1** no modo de exibição de Design.

2.  Da janela **Fontes de Dados**, arraste o nó **Customer** para o **Form1**.

    > [!NOTE]
    > Para exibir a janela **Fontes de Dados**, clique em **Mostrar Fontes de Dados** no menu **Dados**.

3.  Abra o **Form1** no Editor de Códigos.

4.  Adicione o seguinte código ao formulário, global para o formulário, fora de qualquer método específico, mas dentro do `Form1` classe:

    ```vb
    Private NorthwindDataContext1 As New NorthwindDataContext
    ```

    ```csharp
    private NorthwindDataContext northwindDataContext1
        = new NorthwindDataContext();
    ```

5.  Crie um manipulador de eventos para o evento `Form_Load` e adicione o seguinte código ao manipulador:

    ```vb
    CustomerBindingSource.DataSource = NorthwindDataContext1.Customers
    ```

    ```csharp
    customerBindingSource.DataSource
        = northwindDataContext1.Customers;
    ```

## <a name="implement-save-functionality"></a>Implementar a funcionalidade de salvar

Por padrão, o botão de salvar não está habilitado e a funcionalidade de salvar não está implementada. Além disso, o código não será automaticamente adicionado para salvar dados modificados no banco de dados quando os controles associados a dados forem criados para fontes de dados de objeto. Esta seção explica como habilitar o salvamento botão e implementar a funcionalidade de salvar para LINQ para objetos do SQL.

### <a name="to-implement-save-functionality"></a>Para implementar a funcionalidade de salvar

1.  Abra **Form1** no modo de exibição de Design.

2.  Selecione o botão de salvar no **CustomerBindingNavigator** (o botão com o ícone de disquete).

3.  Na janela **Propriedades**, defina a propriedade **Habilitado** como **True**.

4.  Clique duas vezes no botão de salvar para criar um manipulador de eventos e alternar para o Editor de Códigos.

5.  Adicione o código a seguir no manipulador de eventos do botão de salvar:

    ```vb
    NorthwindDataContext1.SubmitChanges()
    ```

    ```csharp
    northwindDataContext1.SubmitChanges();
    ```

## <a name="override-the-default-behavior-for-performing-updates-inserts-updates-and-deletes"></a>Substituir o comportamento padrão para realizar atualizações (inserções, atualizações e exclusões)

### <a name="to-override-the-default-update-behavior"></a>Para substituir o comportamento padrão de atualização

1.  Abra o arquivo LINQ to SQL no **Relational Designer**. (Clique duas vezes no arquivo **Northwind.dbml** no **Gerenciador de Soluções**.)

2.  Em **Gerenciador de Servidores**/**Gerenciador de Banco de Dados**, expanda o nó **Procedimentos Armazenados** de bancos de dados Northwind e localize os procedimentos armazenados **InsertCustomers**, **UpdateCustomers** e **DeleteCustomers**.

3.  Arraste todos os três procedimentos armazenados para o **Relational Designer**.

     Os procedimentos armazenados são adicionados ao painel dos métodos como métodos <xref:System.Data.Linq.DataContext>. Para obter mais informações, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).

4.  Selecione o **Customer** classe de entidade na **Relational Designer**.

5.  Na janela **Propriedades**, selecione a propriedade **Insert**.

6.  Clique nas reticências (**…**) ao lado de **Usar tempo de execução** para abrir a caixa de diálogo **Configurar Comportamento**.

7.  Selecione **Personalizar**.

8.  Selecione o método **InsertCustomers** na lista **Personalizar**.

9. Clique em **Aplicar** para salvar a configuração para a Classe e o Comportamento selecionados.

    > [!NOTE]
    > Você pode continuar a configurar o comportamento para cada combinação de classe/comportamento quando você clica em **Aplicar** depois de cada alteração. Se você alterar a classe ou o comportamento antes de clicar em **aplicar**, uma caixa de diálogo de aviso fornecendo uma oportunidade de aplicar as alterações é exibida.

10. Selecione **Atualizar** na lista **Comportamento**.

11. Selecione **Personalizar**.

12. Selecione o método **UpdateCustomers** na lista **Personalizar**.

     Inspecione a lista de **Argumentos de Método** e de **Propriedades de Classe** e observe que há dois **Argumentos de Método** e duas **Propriedades de Classe** para algumas colunas na tabela. Isso facilita controlar as alterações e criar as instruções que conferem a existência de violações de simultaneidade.

13. Mapeie o argumento do método **Original_CustomerID** para a propriedade de classe **CustomerID (Original)**.

    > [!NOTE]
    > Por padrão, os argumentos do método mapearão para as propriedades da classe quando os nomes corresponderem. Se os nomes de propriedade forem modificados e não corresponderem entre a tabela e a classe de entidade, poderá ser preciso selecionar a propriedade da classe equivalente para a qual mapear se o **Designer Relacional de Objetos** não puder determinar o mapeamento correto. Além disso, se os argumentos do método não tiverem propriedades da classe válidas para a qual mapear, você poderá definir o valor de **Propriedades de Classe** como **(Nenhum)**.

14. Clique em **Aplicar** para salvar a configuração para a Classe e o Comportamento selecionados.

15. Selecione **Excluir** na lista **Comportamento**.

16. Selecione **Personalizar**.

17. Selecione o método **DeleteCustomers** na lista **Personalizar**.

18. Mapeie o argumento do método **Original_CustomerID** para a propriedade de classe **CustomerID (Original)**.

19. Clique em **OK**.

> [!NOTE]
> Embora não seja um problema para este passo a passo específica, vale a pena observar que o LINQ to SQL lida com valores gerados por banco de dados automaticamente para a identidade (incremento automático), rowguidcol (GUID gerado por banco de dados) e colunas de carimbo de hora durante inserções e atualizações. Os valores gerados pelo banco de dados em outros tipos de coluna resultarão inesperadamente em um valor nulo. Para retornar os valores gerados pelo banco de dados, você deve definir manualmente <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> à `true` e <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> para um dos seguintes: [AutoSync.Always](<xref:System.Data.Linq.Mapping.AutoSync.Always>), [AutoSync.OnInsert](<xref:System.Data.Linq.Mapping.AutoSync.OnInsert>), ou [AutoSync.OnUpdate](<xref:System.Data.Linq.Mapping.AutoSync.OnUpdate>).

## <a name="test-the-application"></a>Testar o aplicativo

Execute o aplicativo novamente para verificar se o procedimento armazenado **UpdateCustomers** atualiza corretamente o registro do cliente no banco de dados.

1.  Pressione **F5**.

2.  Modifique um registro na grade para testar o comportamento de atualização.

3.  Adicione um novo registro para testar o comportamento de inserção.

4.  Clique no botão de salvar para salvar as alterações de volta para o banco de dados.

5.  Feche o formulário.

6.  Pressione **F5** e verifique se o registro atualizado e o registro inserido recentemente persistiram.

7.  Exclua o novo registro que você criou na etapa 3 para testar o comportamento de exclusão.

8.  Clique no botão de salvar para enviar as alterações e remova o registro excluído do banco de dados.

9. Feche o formulário.

10. Pressione **F5** e verifique se o registro excluído foi removido do banco de dados.

    > [!NOTE]
    > Se o aplicativo usar o SQL Server Express Edition, dependendo do valor da propriedade **Copiar para Diretório de Saída** do arquivo de banco de dados, as alterações poderão não aparecer quando você pressiona **F5** na etapa 10.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos do aplicativo, há várias etapas que você talvez queira realizar após você cria classes LINQ to SQL entidade. Entre algumas das melhorias que você pode fazer neste aplicativo estão:

- Implementar verificação de simultaneidade durante atualizações. Para obter informações, consulte [simultaneidade otimista: Visão geral do](/dotnet/framework/data/adonet/sql/linq/optimistic-concurrency-overview).

- Adicionar consultas LINQ para filtrar dados. Para obter informações, consulte [Introdução a consultas LINQ (c#)](/dotnet/csharp/programming-guide/concepts/linq/introduction-to-linq-queries).

## <a name="see-also"></a>Consulte também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Métodos DataContext](../data-tools/datacontext-methods-o-r-designer.md)
- [Como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Consultas do LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/linq-to-sql-queries)