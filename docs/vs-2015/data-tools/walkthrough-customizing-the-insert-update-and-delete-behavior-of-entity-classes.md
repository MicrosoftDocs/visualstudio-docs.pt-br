---
title: 'Passo a passo: Personalizando a inserção, atualização e exclusão de comportamento de classes de entidade | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 03ff1146-706e-4780-91cb-56a83df63eea
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 4d8ef69258d9c672bb5deb01b9c2e0972d4e8303
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49193538"
---
# <a name="walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes"></a>Passo a passo: Personalizando a inserção, atualização e exclusão de comportamento de classes de entidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
O [ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) fornece uma superfície de design visual para criar e editar [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] classes (classes de entidade) que são baseadas em objetos em um banco de dados. Usando [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655), você pode usar a tecnologia LINQ para acessar bancos de dados SQL. Para saber mais, veja [LINQ (Consulta Integrada à Linguagem)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d).  
  
 Por padrão, a lógica para executar atualizações é fornecida pelo tempo de execução do [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]. O tempo de execução cria instruções padrão Insert, Update e Delete com base no esquema da tabela (as definições de coluna e as informações da chave primária). Quando você não deseja usar o comportamento padrão, poderá configurar o comportamento de atualização e designar procedimentos armazenados específicos para executar as inserções, as atualizações e as exclusões necessárias para trabalhar com os dados no banco de dados. Você também pode fazer isso quando o comportamento padrão não é gerado, por exemplo, quando as classes de entidade mapeiam para as exibições. Além disso, você pode substituir o comportamento de atualização padrão quando o banco de dados exige acesso à tabela por meio dos procedimentos armazenados. Para obter mais informações, consulte [personalizando operações por usando procedimentos armazenados](http://msdn.microsoft.com/library/aedbecc1-c33c-4fb4-8861-fdf7e1dc6b8a).  
  
> [!NOTE]
>  Este passo a passo exige a disponibilidade dos **InsertCustomer**, **UpdateCustomer**, e **DeleteCustomer** procedimentos armazenados para o banco de dados Northwind. Para obter detalhes sobre como criar esses procedimentos armazenados, consulte [instruções passo a passo: Criando procedimentos de armazenado de atualização para a tabela de clientes Northwind](../data-tools/walkthrough-creating-update-stored-procedures-for-the-northwind-customers-table.md).  
  
 Essa explicação passo a passo fornece as etapas que você deve seguir para substituir o comportamento padrão de tempo de execução LINQ to SQL para salvar dados de volta para um banco de dados usando procedimentos armazenados.  
  
 Durante essa explicação passo a passo, será ensinado como realizar as seguintes tarefas:  
  
-   Crie um novo aplicativo do Windows Forms e adicione um arquivo [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] a ele.  
  
-   Crie uma classe de entidade que está mapeada para a tabela Customers Northwind.  
  
-   Crie uma fonte de dados de objeto que referencia a classe de cliente LINQ to SQL.  
  
-   Crie um Windows Form que contém um <xref:System.Windows.Forms.DataGridView> que está associado à classe Customer.  
  
-   Implemente a funcionalidade de salvar para o formulário.  
  
-   Crie métodos de <xref:System.Data.Linq.DataContext> adicionando procedimentos armazenados ao [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
-   Configure a classe Customer para usar procedimentos armazenados para executar inserções, atualizações e exclusões.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir esta explicação passo a passo, você precisará do seguinte:  
  
-   Acessar a versão do SQL Server do banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
-   O **InsertCustomer**, **UpdateCustomer**, e **DeleteCustomer** procedimentos armazenados para o banco de dados Northwind. Para obter mais informações, consulte [instruções passo a passo: Criando procedimentos de armazenado de atualização para a tabela de clientes Northwind](../data-tools/walkthrough-creating-update-stored-procedures-for-the-northwind-customers-table.md).  
  
## <a name="creating-an-application-and-adding-linq-to-sql-classes"></a>Criando um aplicativo e adicionando classes LINQ to SQL  
 Como você estará trabalhando com classes do [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] e exibindo os dados em um Windows Form, crie um novo aplicativo do Windows Forms e adicione um arquivo de classes LINQ to SQL.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-a-new-windows-application-project-that-contains-linq-to-sql-classes"></a>Para criar um novo projeto de aplicativo do Windows que contém classes LINQ to SQL  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto **UpdatingwithSProcsWalkthrough**.  
  
    > [!NOTE]
    >  O [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] tem suporte em projetos de [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] e C#. Portanto, crie o novo projeto em uma dessas linguagens.  
  
3.  Clique o **aplicativo do Windows Forms** modelo e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O projeto de UpdatingwithSProcsWalkthrough é criado e adicionado ao **Gerenciador de soluções**.  
  
4.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
5.  Clique o **Classes LINQ to SQL** modelo e o tipo **dbml** no **nome** caixa.  
  
6.  Clique em **Adicionar**.  
  
     Um arquivo de classes LINQ to SQL vazio (Northwind.dbml) é adicionado ao projeto, e o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] é aberto.  
  
## <a name="creating-the-customer-entity-class-and-object-data-source"></a>Criando a Classe Entidade de Cliente e o Objeto de Fonte de Dados  
 Crie [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] classes que são mapeadas para tabelas de banco de dados arrastando tabelas do **Gerenciador de servidores**/**Database Explorer** até o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. O resultado são classes de entidade do LINQ to SQL que mapeiam para as tabelas no banco de dados. Depois de criar classes de entidade, elas podem ser usadas como fontes de dados de objeto assim como outras classes que têm propriedades públicas.  
  
#### <a name="to-create-a-customer-entity-class-and-configure-a-data-source-with-it"></a>Para criar uma classe de entidade Customer e configurar uma fonte de dados com ela  
  
1.  Na **Gerenciador de servidores**/**Gerenciador de banco de dados**, localize a tabela Customer na versão do SQL Server do banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: conectar-se ao banco de dados Northwind](../data-tools/how-to-connect-to-the-northwind-database.md).  
  
2.  Arraste o **clientes** nó a partir **Gerenciador de servidores**/**Database Explorer** até o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] superfície.  
  
     Uma classe de entidade nomeada **cliente** é criado. Ela tem propriedades que correspondem às colunas na tabela Customers. A classe de entidade é nomeada **Customer** (não **clientes**) porque ele representa um único cliente na tabela Customers.  
  
    > [!NOTE]
    >  Esse comportamento de renomeação é chamado *pluralização*. Ele pode ser ativado ou desativado [caixa de diálogo Opções](../ide/reference/options-dialog-box-visual-studio.md). Para obter mais informações, consulte [como: ative em pluralization e off (O/R Designer)](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md).  
  
3.  Sobre o **construir** menu, clique em **compilar UpdatingwithSProcsWalkthrough** para compilar o projeto.  
  
4.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
5.  No **fontes de dados** janela, clique em **Add New Data Source**.  
  
6.  Clique em **objeto** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
7.  Expanda o **UpdatingwithSProcsWalkthrough** nó e localize e selecione o **cliente** classe.  
  
    > [!NOTE]
    >  Se o **cliente** classe não estiver disponível, cancele o assistente, compile o projeto e execute o assistente novamente.  
  
8.  Clique em **terminar** para criar a fonte de dados e adicionar o **Customer** classe de entidade para o **fontes de dados** janela.  
  
## <a name="creating-a-datagridview-to-display-the-customer-data-on-a-windows-form"></a>Criando um DataGridView para exibir os dados do cliente em um Windows Form  
 Crie controles que estão associados às classes de entidade arrastando [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] itens da fonte de dados do **fontes de dados** janela em um formulário do Windows.  
  
#### <a name="to-add-controls-that-are-bound-to-the-entity-classes"></a>Para adicionar controles que estão associados às classes de entidade  
  
1.  Abrir Form1 na exibição Design.  
  
2.  Dos **fontes de dados** janela, arraste a **cliente** nó para Form1.  
  
    > [!NOTE]
    >  Para exibir o **fontes de dados** janela, clique em **Show Data Sources** sobre o **dados** menu.  
  
3.  Abra o Form1 no Editor de Códigos.  
  
4.  Adicione o seguinte código ao formulário, global para o formulário, fora de qualquer método específico, mas dentro da classe Form1:  
  
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
  
## <a name="implementing-save-functionality"></a>Implementando a funcionalidade de salvar  
 Por padrão, o botão de salvar não está habilitado e a funcionalidade de salvar não está implementada. Além disso, o código não será automaticamente adicionado para salvar dados modificados no banco de dados quando os controles associados a dados forem criados para fontes de dados de objeto. Esta seção explica como habilitar o salvamento botão e implementar a funcionalidade de salvar para [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] objetos.  
  
#### <a name="to-implement-save-functionality"></a>Para implementar a funcionalidade de salvar  
  
1.  Abrir Form1 na exibição Design.  
  
2.  Selecione Salvar no botão de **CustomerBindingNavigator** (o botão com o ícone de disquete).  
  
3.  No **propriedades** janela, defina o **Enabled** propriedade a ser **verdadeiro**.  
  
4.  Clique duas vezes no botão de salvar para criar um manipulador de eventos e alternar para o Editor de Códigos.  
  
5.  Adicione o código a seguir no manipulador de eventos do botão de salvar:  
  
    ```vb  
    NorthwindDataContext1.SubmitChanges()  
    ```  
  
    ```csharp  
    northwindDataContext1.SubmitChanges();  
    ```  
  
## <a name="overriding-the-default-behavior-for-performing-updates-inserts-updates-and-deletes"></a>Substituindo o comportamento padrão para realizar atualizações (inserções, atualizações e exclusões)  
  
#### <a name="to-override-the-default-update-behavior"></a>Para substituir o comportamento padrão de atualização  
  
1.  Abra o arquivo LINQ to SQL no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. (Clique duas vezes o **dbml** arquivo no **Gerenciador de soluções**.)  
  
2.  Na **Gerenciador de servidores**/**Database Explorer**, expanda os bancos de dados Northwind **Stored Procedures** nó e localize o  **InsertCustomers**, **UpdateCustomers**, e **DeleteCustomers** procedimentos armazenados.  
  
3.  Arraste os três procedimentos armazenados para o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
     Os procedimentos armazenados são adicionados ao painel dos métodos como métodos <xref:System.Data.Linq.DataContext>. Para obter mais informações, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).  
  
4.  Selecione o **Customer** classe de entidade no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
5.  No **propriedades** janela, selecione a **inserir** propriedade.  
  
6.  Clique nas reticências (...) próximo a **usar tempo de execução** para abrir o **configurar comportamento** caixa de diálogo.  
  
7.  Selecione **personalizar**.  
  
8.  Selecione o **InsertCustomers** método o **personalizar** lista.  
  
9. Clique em **aplicar** para salvar a configuração para a classe e comportamento selecionados.  
  
    > [!NOTE]
    >  Você pode continuar a configurar o comportamento para cada combinação de classe/comportamento desde que você clique em **aplicar** após cada alteração. Se você alterar a classe ou o comportamento antes de clicar em **aplicar**, uma caixa de diálogo de aviso fornecendo uma oportunidade de aplicar as alterações serão exibidas.  
  
10. Selecione **atualização** na **comportamento** lista.  
  
11. Selecione **personalizar**.  
  
12. Selecione o **UpdateCustomers** método o **personalizar** lista.  
  
     Inspecione a lista de **argumentos de método** e **propriedades da classe** e observe que há dois **argumentos de método** e dois **propriedades da classe**para algumas colunas na tabela. Isso facilita controlar as alterações e criar as instruções que conferem a existência de violações de simultaneidade.  
  
13. Mapa de **Original_CustomerID** argumento de método para o **CustomerID (Original)** propriedade da classe.  
  
    > [!NOTE]
    >  Por padrão, os argumentos do método mapearão para as propriedades da classe quando os nomes corresponderem. Se os nomes de propriedade forem modificados e não corresponderem entre a tabela e a classe de entidade, você poderá ter que selecionar a propriedade da classe equivalente para a qual mapear se o Designer Relacional de Objetos não puder determinar o mapeamento correto. Além disso, se não tiverem propriedades de classe válida para mapear para argumentos de método, você pode definir as **propriedades da classe** valor para **(nenhum)**.  
  
14. Clique em **aplicar** para salvar a configuração para a classe e comportamento selecionados.  
  
15. Selecione **exclua** na **comportamento** lista.  
  
16. Selecione **personalizar**.  
  
17. Selecione o **DeleteCustomers** método o **personalizar** lista.  
  
18. Mapa de **Original_CustomerID** argumento de método para o **CustomerID (Original)** propriedade da classe.  
  
19. Clique em **OK**.  
  
> [!NOTE]
>  Embora isso não seja um problema para essa explicação passo a passo específica, vale observar que o [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] manipula automaticamente os valores gerados por banco de dados para as colunas identidade (incremento automático), rowguidcol (GUID gerado por banco de dados) e carimbo de data/hora durante inserções e atualizações. Os valores gerados pelo banco de dados em outros tipos de coluna resultarão inesperadamente em um valor nulo. Para retornar os valores gerados pelo banco de dados, você deve definir manualmente <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> à `true` e <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> para um dos seguintes: <xref:System.Data.Linq.Mapping.AutoSync>, <xref:System.Data.Linq.Mapping.AutoSync>, ou <xref:System.Data.Linq.Mapping.AutoSync>.  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
 Executar o aplicativo novamente para verificar se o **UpdateCustomers** procedimento armazenado atualiza corretamente o registro do cliente no banco de dados.  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Pressione F5.  
  
2.  Modifique um registro na grade para testar o comportamento de atualização.  
  
3.  Adicione um novo registro para testar o comportamento de inserção.  
  
4.  Clique no botão de salvar para salvar as alterações de volta para o banco de dados.  
  
5.  Feche o formulário.  
  
6.  Pressione F5 e verifique se o registro atualizado e o registro inserido recentemente persistiram.  
  
7.  Exclua o novo registro que você criou na etapa 3 para testar o comportamento de exclusão.  
  
8.  Clique no botão de salvar para enviar as alterações e remova o registro excluído do banco de dados  
  
9. Feche o formulário.  
  
10. Pressione F5 e verifique se o registro excluído foi removido do banco de dados.  
  
    > [!NOTE]
    >  Se seu aplicativo usa o SQL Server Express Edition, dependendo do valor da **Copy to Output Directory** propriedade do arquivo de banco de dados, as alterações podem não aparecer quando você pressiona F5 na etapa 10. Para obter mais informações, consulte [como: gerenciar arquivos de dados locais em seu projeto](../data-tools/how-to-manage-local-data-files-in-your-project.md).  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos do aplicativo, há várias etapas que você talvez queira realizar após criar [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] classes de entidade. Entre algumas das melhorias que você pode fazer neste aplicativo estão:  
  
-   Implementar verificação de simultaneidade durante atualizações. Para obter informações, consulte [simultaneidade otimista: Visão geral do](http://msdn.microsoft.com/library/c2e38512-d0c8-4807-b30a-cb7e30338694).  
  
-   Adicionar consultas LINQ para filtrar dados. Para obter informações, consulte [Introdução a consultas LINQ (c#)](http://msdn.microsoft.com/library/37895c02-268c-41d5-be39-f7d936fa88a8).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Consultas LINQ to SQL](http://msdn.microsoft.com/library/f4897aaa-7f44-4c20-a471-b948c2971aae)   
 [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)   
 [Como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)   
 [PREPARAR o que há de novo para o desenvolvimento de aplicativo de dados no Visual Studio 2012](http://msdn.microsoft.com/en-us/3d50d68f-5f44-4915-842f-6d42fce793f1)

