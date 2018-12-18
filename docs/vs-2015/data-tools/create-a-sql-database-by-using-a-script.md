---
title: Criar um banco de dados SQL usando um script | Microsoft Docs
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
ms.assetid: 36f913c0-f5a7-4831-83a0-baba721ac95c
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 13816c499002f8eaf81067aba8d1854d06a41445
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49266585"
---
# <a name="create-a-sql-database-by-using-a-script"></a>Criar um banco de dados SQL usando um script
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Neste passo a passo, você usa o Visual Studio para criar um banco de dados pequeno que contém o código de exemplo [criar um aplicativo de dados simples usando o ADO.NET](../data-tools/create-a-simple-data-application-by-using-adonet.md).  
  
 **Neste tópico**  
  
-   [Criar um script que contém um esquema de banco de dados](../data-tools/create-a-sql-database-by-using-a-script.md#CreateScript)  
  
-   [Criar um projeto de banco de dados e importar um esquema](../data-tools/create-a-sql-database-by-using-a-script.md#CreateProject)  
  
-   [Implantar o banco de dados](../data-tools/create-a-sql-database-by-using-a-script.md#DeployDatabase)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você deve ter o SQL Server Express LocalDB ou outro banco de dados SQL instalado.  
  
##  <a name="CreateScript"></a> Criar um script que contém um esquema de banco de dados  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>Para criar um script do qual você pode importar um esquema  
  
1.  Na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], na barra de menus, selecione **arquivo** > **New** > **arquivo**.  
  
     O **novo arquivo** caixa de diálogo é exibida.  
  
2.  No **categorias** lista, selecione **geral**.  
  
3.  No **modelos** lista, selecione **arquivo Sql**e, em seguida, selecione o **abrir** botão.  
  
     Abre o editor Transact-SQL.  
  
4.  Copie o seguinte código Transact-SQL e, em seguida, cole-o editor Transact-SQL.  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40),  
    @CustomerID INT OUTPUT  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SET @CustomerID = SCOPE_IDENTITY();  
    RETURN @@ERROR  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5.  Na barra de menus, selecione **arquivo** > **salvar SqlQuery_1.sql como**.  
  
     O **salvar arquivo como** caixa de diálogo é exibida.  
  
6.  No **nome do arquivo** , digite `SampleImportScript.sql`, anote o local onde você salvará o arquivo e, em seguida, selecione o **salvar** botão.  
  
7.  Na barra de menus, selecione **arquivo** > **fechar solução**.  
  
     Em seguida, crie um projeto de banco de dados e, em seguida, importe o esquema do script que você criou.  
  
##  <a name="CreateProject"></a> Criar um projeto de banco de dados e importar um esquema  
  
#### <a name="to-create-a-database-project"></a>Para criar um projeto de banco de dados  
  
1.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
     A caixa de diálogo **Novo Projeto** é exibida.  
  
2.  Sob **instalados**, expanda o **modelos** nó, expanda o **outros idiomas** nó, selecione o **do SQL Server** categoria e, em seguida, Selecione o **projeto de banco de dados do SQL Server** modelo.  
  
    > [!NOTE]
    >  O **outras linguagens** nó não aparece em todas as instalações do Visual Studio.  
  
3.  No **nome** , digite `Small Database`.  
  
4.  Selecione o **criar diretório para solução** caixa de seleção se ainda não estiver selecionado.  
  
5.  Desmarque a **adicionar ao controle do código-fonte** caixa de seleção se ainda não estiver desmarcada e, em seguida, selecione o **Okey** botão.  
  
     O projeto de banco de dados é criado e aparece na **Gerenciador de soluções**.  
  
     Em seguida, importe o esquema de banco de dados do script.  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>Para importar um esquema de banco de dados de um script  
  
1.  Na barra de menus, selecione **Project** > **importação** > **Script**.  
  
2.  Sobre o **bem-vindo** página, examine o texto e, em seguida, selecione o **próxima** botão.  
  
3.  Selecione o **único arquivo** botão de opção e, em seguida, selecione o **procurar** botão.  
  
     O **importar Script SQL** caixa de diálogo é exibida.  
  
4.  Abra a pasta onde você salvou o arquivo Sampleimportscript SQL, selecione o arquivo e, em seguida, selecione a **abrir** botão.  
  
5.  Selecione o **terminar** botão para fechar o **importar Script SQL** caixa de diálogo.  
  
     O script é importado, e os objetos que o script define são adicionados ao seu projeto de banco de dados.  
  
6.  Examine o resumo e, em seguida, clique no **terminar** botão para fechar o **importar arquivo de Script SQL** caixa de diálogo.  
  
7.  Na **Gerenciador de soluções**, expanda vendas, Scripts e segurança pastas do seu projeto e verificar se eles contêm arquivos. SQL.  
  
8.  Na **Pesquisador de objetos do SQL Server**, verifique se o banco de dados aparece sob o **projetos** nó.  
  
     Neste ponto, o banco de dados contém apenas objetos do sistema, como tabelas e procedimentos armazenados. Depois de implantar o banco de dados, ele conterá as tabelas de usuário e os procedimentos armazenados que definem os scripts.  
  
##  <a name="DeployDatabase"></a> Implantar o banco de dados  
 Quando você pressiona o **F5** chave, você implantar (ou publica) o banco de dados para um banco de dados LocalDB por padrão. Você pode implantar o banco de dados para um local diferente abrindo a página de propriedades do projeto, selecionando o **depurar** guia e, em seguida, alterando a cadeia de caracteres de conexão.

