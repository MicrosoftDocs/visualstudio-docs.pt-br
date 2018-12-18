---
title: 'Passo a passo: Criando procedimentos armazenados atualizados para a tabela de clientes Northwind | Microsoft Docs'
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
- Northwind sample database
- stored procedures [Visual Studio]
- O/R Designer, stored procedures
ms.assetid: 6fd9e7e0-6862-44d3-9710-acc5a72d4ffd
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 4972c1341490f78bba03bdd390ac13903c55be84
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49204042"
---
# <a name="walkthrough-creating-update-stored-procedures-for-the-northwind-customers-table"></a>Instruções passo a passo: criando procedimentos armazenados atualizados para a tabela Clientes do Northwind
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Alguns tópicos da Ajuda no [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] documentação exigem outros procedimentos armazenados no banco de dados de exemplo Northwind para realizar atualizações (inserções, atualizações e exclusões) de dados na tabela Customers.  
  
 Essa explicação passo a passo fornece orientações para criar esses procedimentos armazenados adicionais nos bancos de dados de exemplo Northwind para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 A seção Próximas Etapas mais adiante neste tópico fornece links para tópicos que demonstram como trabalhar com esses procedimentos armazenados adicionais.  
  
 Durante essa explicação passo a passo, será ensinado como realizar as seguintes tarefas:  
  
-   Criar uma conexão de dados com o banco de dados de exemplo Northwind.  
  
-   Criar os procedimentos armazenados.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir esta explicação passo a passo, será necessário:  
  
-   Acessar a versão do SQL Server do banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="connecting-to-the-northwind-database"></a>Conectando ao Banco de Dados Northwind  
 Essa explicação passo a passo exige uma conexão com a versão do SQL Server do banco de dados Northwind. O procedimento a seguir fornece orientações para criar a conexão de dados.  
  
> [!NOTE]
>  Se já houver uma conexão de dados com o banco de dados Northwind, avance para a próxima seção, Criando os Procedimentos Armazenados.  
  
#### <a name="to-create-a-data-connection-to-the-northwind-sql-server-database"></a>Criar uma conexão de dados com o banco de dados Northwind do SQL Server  
  
1.  Sobre o **exibição** menu, clique em **Gerenciador de servidores**/**Database Explorer**.  
  
2.  Clique com botão direito **conexões de dados** e clique em **Adicionar Conexão**.  
  
3.  No **Choose Data Source** caixa de diálogo, clique em **Microsoft SQL Server**e, em seguida, clique em **Okey**.  
  
     Se o **Adicionar Conexão** caixa de diálogo é aberta e o **fonte de dados** não é **Microsoft SQL Server (SqlClient)**, clique em **alteração** para abrir o **Escolher/alterar fonte de dados** caixa de diálogo, clique em **Microsoft SQL Server**e, em seguida, clique em **Okey**.  
  
4.  Clique em uma **nome do servidor** na lista suspensa lista ou digite o nome do servidor no qual o banco de dados Northwind está localizado.  
  
5.  Com base nos requisitos do banco de dados ou aplicativo, clique em **usar autenticação do Windows** ou usar um nome de usuário específico e uma senha para fazer logon no computador que executa o SQL Server (**deautenticaçãodoSQLServer**).  
  
6.  Clique em banco de dados Northwind na **selecione ou insira um nome de banco de dados** lista.  
  
7.  Clique em **OK**.  
  
     A conexão de dados é adicionada à **Gerenciador de servidores**/**Gerenciador de banco de dados**.  
  
## <a name="creating-the-stored-procedures"></a>Criando os procedimentos armazenados  
 Criar os procedimentos armazenados, executando o script SQL no banco de dados Northwind usando o [Visual Database Tools](http://msdn.microsoft.com/en-us/6b145922-2f00-47db-befc-bf351b4809a1) disponível no **Gerenciador de servidores** /  **Gerenciador de banco de dados**.  
  
#### <a name="to-create-the-stored-procedures-by-using-a-sql-script"></a>Criar os procedimentos armazenados usando um script SQL  
  
1.  Expanda o banco de dados Northwind **Gerenciador de servidores**/**Gerenciador de banco de dados**.  
  
2.  Clique com botão direito do **procedimentos armazenados** nó e clique em **adicionar novo procedimento armazenado**.  
  
3.  Cole o seguinte código no Editor de Códigos, substituindo o modelo `CREATE PROCEDURE`:  
  
    ```  
    IF EXISTS (SELECT * FROM sysobjects WHERE name = 'SelectCustomers' AND user_name(uid) = 'dbo')  
        DROP PROCEDURE dbo.[SelectCustomers]  
    GO  
  
    CREATE PROCEDURE dbo.[SelectCustomers]  
    AS  
        SET NOCOUNT ON;  
    SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax FROM dbo.Customers  
    GO  
  
    IF EXISTS (SELECT * FROM sysobjects WHERE name = 'InsertCustomers' AND user_name(uid) = 'dbo')  
        DROP PROCEDURE dbo.InsertCustomers  
    GO  
  
    CREATE PROCEDURE dbo.InsertCustomers  
    (  
        @CustomerID nchar(5),  
        @CompanyName nvarchar(40),  
        @ContactName nvarchar(30),  
        @ContactTitle nvarchar(30),  
        @Address nvarchar(60),  
        @City nvarchar(15),  
        @Region nvarchar(15),  
        @PostalCode nvarchar(10),  
        @Country nvarchar(15),  
        @Phone nvarchar(24),  
        @Fax nvarchar(24)  
    )  
    AS  
        SET NOCOUNT OFF;  
    INSERT INTO [dbo].[Customers] ([CustomerID], [CompanyName], [ContactName], [ContactTitle], [Address], [City], [Region], [PostalCode], [Country], [Phone], [Fax]) VALUES (@CustomerID, @CompanyName, @ContactName, @ContactTitle, @Address, @City, @Region, @PostalCode, @Country, @Phone, @Fax);  
  
    SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax FROM Customers WHERE (CustomerID = @CustomerID)  
    GO  
  
    IF EXISTS (SELECT * FROM sysobjects WHERE name = 'UpdateCustomers' AND user_name(uid) = 'dbo')  
        DROP PROCEDURE dbo.UpdateCustomers  
    GO  
  
    CREATE PROCEDURE dbo.UpdateCustomers  
    (  
        @CustomerID nchar(5),  
        @CompanyName nvarchar(40),  
        @ContactName nvarchar(30),  
        @ContactTitle nvarchar(30),  
        @Address nvarchar(60),  
        @City nvarchar(15),  
        @Region nvarchar(15),  
        @PostalCode nvarchar(10),  
        @Country nvarchar(15),  
        @Phone nvarchar(24),  
        @Fax nvarchar(24),  
        @Original_CustomerID nchar(5)  
    )  
    AS  
        SET NOCOUNT OFF;  
    UPDATE [dbo].[Customers] SET [CustomerID] = @CustomerID, [CompanyName] = @CompanyName, [ContactName] = @ContactName, [ContactTitle] = @ContactTitle, [Address] = @Address, [City] = @City, [Region] = @Region, [PostalCode] = @PostalCode, [Country] = @Country, [Phone] = @Phone, [Fax] = @Fax WHERE (([CustomerID] = @Original_CustomerID));  
  
    SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax FROM Customers WHERE (CustomerID = @CustomerID)  
    GO  
  
    IF EXISTS (SELECT * FROM sysobjects WHERE name = 'DeleteCustomers' AND user_name(uid) = 'dbo')  
        DROP PROCEDURE dbo.DeleteCustomers  
    GO  
  
    CREATE PROCEDURE dbo.DeleteCustomers  
    (  
        @Original_CustomerID nchar(5)  
    )  
    AS  
        SET NOCOUNT OFF;  
    DELETE FROM [dbo].[Customers] WHERE (([CustomerID] = @Original_CustomerID))  
    GO  
    ```  
  
4.  Selecione todo o texto no Editor de códigos, clique com botão direito no texto selecionado e clique em **Run Selection**.  
  
     Os procedimentos armazenados SelectCustomers, InsertCustomers, UpdateCustomers e DeleteCustomers são criados para o banco de dados Northwind.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que os procedimentos armazenados foram criados, tente as seguintes explicações passo a passo que demonstram como trabalhar com eles:  
  
 [Como atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer Relacional de Objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)  
  
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)  
  
 [Passo a passo: personalizando a inserção, a atualização e o comportamento de exclusão de classes de entidade](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)