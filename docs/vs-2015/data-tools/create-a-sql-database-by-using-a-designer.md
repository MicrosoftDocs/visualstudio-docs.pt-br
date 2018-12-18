---
title: Criar um banco de dados SQL usando um designer | Microsoft Docs
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
- SQL Server Express
- local data
- LocalDB
- SQLEXPRESS
- data [Visual Studio], Local data
- SQL Express
- data [Visual Studio], walkthroughs
- databases, creating
- database files, creating
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
caps.latest.revision: 54
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 0ef261ec4ea803dcfc42b6151a5c828d5b03811a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49860316"
---
# <a name="create-a-sql-database-by-using-a-designer"></a>Criar um banco de dados SQL usando um designer
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
É possível explorar tarefas básicas, como adicionar tabelas e definir colunas, usando o Visual Studio para criar e atualizar um arquivo de banco de dados local no SQL Server Express LocalDB. Depois de concluir essa explicação passo a passo, você poderá descobrir recursos mais avançados usando o banco de dados local como um ponto de partida para outras explicações passo a passo que o exigem.  
  
 Você também pode criar um banco de dados usando o SQL Server Management Studio (um download separado) ou instruções Transact-SQL no **SQL Server Object Explorer** janela de ferramentas no Visual Studio.  
  
 Durante essa explicação passo a passo, você explorará as seguintes tarefas:  
  
-   [Criar um projeto e um arquivo de banco de dados local](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewSQLDB)  
  
-   [Criar tabelas, colunas, chaves primárias e chaves estrangeiras](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewTbls)  
  
-   [Preencher as tabelas com dados](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_Populating)  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, certifique-se de que você tenha o SQL Server Data Tools instalado. Sobre o **modo de exibição** menu, você deverá ver **Pesquisador de objetos do SQL Server**. Se não estiver, vá para **adicionar ou remover programas**, clique em **Visual Studio 2015**, selecione **alteração**e marque a caixa ao lado **doSQLServerDataTools**.  
  
##  <a name="BKMK_CreateNewSQLDB"></a> Criar um projeto e um arquivo de banco de dados local  
  
#### <a name="to-create-a-project-and-a-database-file"></a>Para criar um projeto e um arquivo de banco de dados  
  
1. Criar um projeto Windows Forms chamado `SampleDatabaseWalkthrough`.  
  
2. Na barra de menus, selecione **Project** > **Adicionar Novo Item**.  
  
3. Na lista de modelos de item, role para baixo e selecione **banco de dados baseado em serviço**.  
  
    ![Caixa de diálogo de modelos de item](../data-tools/media/raddata-vsitemtemplates.png "raddata VSItemTemplates")  
  
4. Nomeie o banco de dados **SampleDatabase**e, em seguida, selecione o **Add** botão.  
  
5. Se o **fontes de dados** janela não estiver aberta, abra-o, selecionando as teclas Shift + Alt + D ou, na barra de menus, selecionando **exibição** > **Other Windows**  >  **Fontes de dados**.  
  
6. No **fontes de dados** janela, selecione a **Add New Data Source** link.  
  
7. No **Data Source Configuration Wizard**, selecione o **próxima** botão quatro vezes para aceitar as configurações padrão e, em seguida, selecione o **concluir** botão.  
  
   Abrindo-se a janela de propriedades do banco de dados, é possível exibir sua cadeia de conexão e o local do arquivo .mdf principal. Você verá que o arquivo de banco de dados está na pasta do projeto.  
  
-   No Visual Studio, selecione **modo de exibição** > **SQL Server Object Explorer** se essa janela não estiver aberta. Abra a janela Propriedades, expandindo a **conexões de dados** nó, abrindo o menu de atalho de SampleDatabase e, em seguida, selecionando **propriedades**.  
  
-   Como alternativa, você pode selecionar **modo de exibição** > **Gerenciador de servidores**, se essa janela não estiver aberta. Abra a janela Propriedades, expandindo a **conexões de dados** nó. Abra o menu de atalho de SampleDatabase e, em seguida, selecione **propriedades**.  
  
##  <a name="BKMK_CreateNewTbls"></a> Criar tabelas, colunas, chaves primárias e chaves estrangeiras  
 Nesta seção, você criará algumas tabelas, uma chave primária em cada tabela e algumas linhas de dados de exemplo. Na próxima explicação passo a passo, você terá uma idea de como essas informações podem ser exibidas em um aplicativo. Você também criará uma chave estrangeira para especificar como os registros em uma tabela podem corresponder aos registros na outra tabela.  
  
#### <a name="to-create-the-customers-table"></a>Para criar a tabela Customers  
  
1.  Na **Gerenciador de servidores** ou **Pesquisador de objetos do SQL Server**, expanda o **conexões de dados** nó e, em seguida, expanda o **SampleDatabase**nó.  
  
2.  Abra o menu de atalho **tabelas**e, em seguida, selecione **adicionar nova tabela**.  
  
     O **Designer de tabela** é aberta e mostra uma grade com uma linha padrão, que representa uma única coluna na tabela que você está criando. Adicionando linhas à grade, você adicionará colunas na tabela.  
  
3.  Na grade, adicione uma linha para cada uma das seguintes entradas:  
  
    |Nome da coluna|Tipo de dados|Permitir nulos|  
    |-----------------|---------------|-----------------|  
    |`CustomerID`|`nchar(5)`|Falso (desmarcado)|  
    |`CompanyName`|`nvarchar(50)`|Falso (desmarcado)|  
    |`ContactName`|`nvarchar (50)`|Verdadeiro (marcado)|  
    |`Phone`|`nvarchar (24)`|Verdadeiro (marcado)|  
  
4.  Abra o menu de atalho para o `CustomerID` de linha e, em seguida, selecione **definir chave primária**.  
  
5.  Abra o menu de atalho da linha padrão e, em seguida, selecione **excluir**.  
  
6.  Nomeie a tabela Clientes atualizando a primeira linha no painel de script de acordo com o seguinte exemplo:  
  
    ```  
    CREATE TABLE [dbo].[Customers]  
    ```  
  
     Você deve ver algo parecido com isso:  
  
     ![Designer de tabela](../data-tools/media/raddata-table-designer.png "raddata Designer de tabela")  
  
7.  No canto superior esquerdo dos **Designer de tabela**, selecione o **atualização** botão.  
  
8.  No **atualizações de banco de dados de visualização** caixa de diálogo, selecione o **Atualizar banco de dados** botão.  
  
     As alterações são salvas no arquivo do banco de dados local.  
  
#### <a name="to-create-the-orders-table"></a>Para criar a tabela Orders  
  
1.  Adicione outra tabela e uma linha para cada entrada na seguinte tabela:  
  
    |Nome da coluna|Tipo de dados|Permitir nulos|  
    |-----------------|---------------|-----------------|  
    |`OrderID`|`int`|Falso (desmarcado)|  
    |`CustomerID`|`nchar(5)`|Falso (desmarcado)|  
    |`OrderDate`|`datetime`|Verdadeiro (marcado)|  
    |`OrderQuantity`|`int`|Verdadeiro (marcado)|  
  
2.  Definir **OrderID** como a chave primária e, em seguida, exclui a linha padrão.  
  
3.  Nomeie a tabela Orders atualizando a primeira linha no painel de script de acordo com o seguinte exemplo:  
  
    ```  
    CREATE TABLE [dbo].[Orders]  
    ```  
  
4.  No canto superior esquerdo dos **Designer de tabela**, selecione o **atualização** botão.  
  
5.  No **atualizações de banco de dados de visualização** caixa de diálogo, selecione o **Atualizar banco de dados** botão.  
  
     As alterações são salvas no arquivo do banco de dados local.  
  
#### <a name="to-create-a-foreign-key"></a>Para criar uma chave estrangeira  
  
1.  No painel de contexto no lado direito da grade, abra o menu de atalho **chaves estrangeiras**e, em seguida, selecione **adicionar nova chave estrangeira**, como mostra a ilustração a seguir.  
  
     ![Adicionar uma chave estrangeira no Designer de tabela](../data-tools/media/foreignkey.png "ForeignKey")  
  
2.  Na caixa de texto que aparece, substitua **ToTable** com `Customers`.  
  
3.  No painel de T-SQL, atualize a última linha para coincidir com o exemplo a seguir:  
  
    ```  
    CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])  
    ```  
  
4.  No canto superior esquerdo dos **Designer de tabela**, selecione o **atualização** botão.  
  
5.  No **atualizações de banco de dados de visualização** caixa de diálogo, selecione o **Atualizar banco de dados** botão.  
  
     As alterações são salvas no arquivo do banco de dados local.  
  
##  <a name="BKMK_Populating"></a> Preencher as tabelas com dados  
  
#### <a name="to-populate-the-tables-with-data"></a>Para popular as tabelas com dados  
  
1.  Na **Gerenciador de servidores** ou **SQL Server Object Explorer**, expanda o nó para o banco de dados de exemplo.  
  
2.  Abra o menu de atalho para o **tabelas** nó, selecione **atualize**e, em seguida, expanda o **tabelas** nó.  
  
3.  Abra o menu de atalho para a tabela clientes e, em seguida, selecione **Mostrar dados da tabela**.  
  
4.  Adicione os dados desejados para pelo menos três clientes.  
  
     É possível especificar cinco caracteres desejados como IDs de cliente, mas escolha pelo menos um do qual é possível se lembrar para uso posteriormente neste procedimento.  
  
5.  Abra o menu de atalho da tabela Orders e, em seguida, selecione **Mostrar dados da tabela**.  
  
6.  Adicione dados para pelo menos três pedidos.  
  
    > [!IMPORTANT]
    >  Verifique se todas as IDs e as quantidades de pedido são inteiros e se cada ID do cliente corresponde a um valor especificado na coluna CustomerID da tabela Customers.  
  
7.  Na barra de menus, selecione **arquivo** > **Salvar tudo**.  
  
8.  Na barra de menus, selecione **arquivo** > **fechar solução**.  
  
    > [!NOTE]
    >  Como prática recomendada, é possível fazer backup do arquivo de banco de dados recém-criado copiando-o e colando a cópia em outro local ou dando à cópia um nome diferente.  
  
## <a name="next-steps"></a>Próximas etapas  
 Agora que você tem um arquivo de banco de dados local com alguns dados de exemplo, você pode concluir qualquer uma das instruções passo a passo que demonstram tarefas de banco de dados.

