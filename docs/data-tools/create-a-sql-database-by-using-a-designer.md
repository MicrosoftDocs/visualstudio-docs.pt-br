---
title: Criar um arquivo de banco de dados e usar o designer de tabela
description: Tutorial que descreve como adicionar tabelas e chaves estrangeiras a um banco de dados usando Designer de Tabela no Visual Studio. Ele também mostra como adicionar dados por meio da interface gráfica.
ms.date: 09/19/2019
ms.topic: conceptual
helpviewer_keywords:
- database tables, creating
- database files, creating
- table designer
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e31be90ff24f110fda66449187d3372976f269a7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282716"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>Criar um banco de dados e adicionar tabelas no Visual Studio

Você pode usar o Visual Studio para criar e atualizar um arquivo de banco de dados local no SQL Server Express LocalDB. Você também pode criar um banco de dados executando instruções Transact-SQL na janela de ferramentas do **pesquisador de objetos do SQL Server** no Visual Studio. Neste tópico, vamos criar um arquivo *. MDF* e adicionar tabelas e chaves usando o designer de tabela.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este passo a passos, você precisará do **desenvolvimento de área de trabalho do .net** e de armazenamento de **dados e** cargas de trabalho de processamento instalados no Visual Studio. Para instalá-los, abra **instalador do Visual Studio** e escolha **Modificar** (ou **mais**  >  **Modificar**) ao lado da versão do Visual Studio que você deseja modificar.

> [!NOTE]
> Os procedimentos neste artigo se aplicam apenas a projetos .NET Framework Windows Forms, e não a projetos de Windows Forms do .NET Core.

## <a name="create-a-project-and-a-local-database-file"></a>Criar um projeto e um arquivo de banco de dados local

1. Crie um novo projeto de **aplicativo de Windows Forms (.NET Framework)** e nomeie-o **SampleDatabaseWalkthrough**.

2. Na barra de menus, selecione **projeto**  >  **Adicionar novo item**.

3. Na lista de modelos de item, role para baixo e selecione **banco de dados baseado em serviço**.

   ![Caixa de diálogo modelos de item](../data-tools/media/raddata-vsitemtemplates.png)

4. Nomeie o banco de dados **SampleDatabase**e clique em **Adicionar**.

### <a name="add-a-data-source"></a>Adicionar uma fonte de dados

1. Se a janela **fontes de dados** não estiver aberta, abra-a pressionando **Shift** + **ALT** + **D** ou selecionando **Exibir**  >  **outras**  >  **fontes de dados** do Windows na barra de menus.

1. Na janela **fontes de dados** , selecione **Adicionar nova fonte de dados**.

   ![Adicionar nova fonte de dados no Visual Studio](media/add-new-data-source.png)

   O **Assistente de configuração de fonte de dados** é aberto.

1. Na página **escolher um tipo de fonte de dados** , escolha **Database** e, em seguida, escolha **Avançar**.

1. Na página **escolher um modelo de banco de dados** , escolha **Avançar** para aceitar o padrão (DataSet).

1. Na página **escolher sua conexão de dados** , selecione o arquivo **SampleDatabase. MDF** na lista suspensa e escolha **Avançar**.

1. Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , escolha **Avançar**.

1. Na página **escolher seus objetos de banco de dados** , você verá uma mensagem dizendo que o banco de dados não contém nenhum objeto. Escolha **Concluir**.

### <a name="view-properties-of-the-data-connection"></a>Exibir as propriedades da conexão de dados

Você pode exibir a cadeia de conexão para o arquivo *SampleDatabase. MDF* abrindo o janela Propriedades da conexão de dados:

- Selecione **Exibir**  >  **pesquisador de objetos do SQL Server** para abrir a janela **pesquisador de objetos do SQL Server** . Expanda **(LocalDB) \MSSQLLocalDB**  >  **bancos de dados**e clique com o botão direito do mouse em *SampleDatabase. MDF* e selecione **Propriedades**.

- Como alternativa, você pode selecionar **Exibir**  >  **Gerenciador de servidores**, se essa janela ainda não estiver aberta. Abra o janela Propriedades expandindo o nó **conexões de dados** , clicando com o botão direito do mouse em *SampleDatabase. MDF*e, em seguida, selecionando **Propriedades**.

  > [!TIP]
  > Se você não puder expandir o nó conexões de dados, ou se a conexão SampleDatabase. MDF não estiver listada, selecione o botão **conectar ao Database** na barra de ferramentas Gerenciador de servidores. Na caixa de diálogo **Adicionar conexão** , certifique-se de que **Microsoft SQL Server arquivo de banco** de dados esteja selecionado em **fonte de dados**e, em seguida, navegue até e selecione o arquivo SampleDatabase. MDF. Conclua a adição da conexão selecionando **OK**.

## <a name="create-tables-and-keys-by-using-table-designer"></a>Criar tabelas e chaves usando Designer de Tabela

Nesta seção, você criará duas tabelas, uma chave primária em cada tabela e algumas linhas de dados de exemplo. Você também criará uma chave estrangeira para especificar como os registros em uma tabela correspondem aos registros na outra tabela.

### <a name="create-the-customers-table"></a>Criar a tabela Customers

1. Em **Gerenciador de servidores**, expanda o nó **conexões de dados** e expanda o nó **SampleDatabase. MDF** .

   Se você não puder expandir o nó conexões de dados, ou se a conexão SampleDatabase. MDF não estiver listada, selecione o botão **conectar ao Database** na barra de ferramentas Gerenciador de servidores. Na caixa de diálogo **Adicionar conexão** , certifique-se de que **Microsoft SQL Server arquivo de banco** de dados esteja selecionado em **fonte de dados**e, em seguida, navegue até e selecione o arquivo SampleDatabase. MDF. Conclua a adição da conexão selecionando **OK**.

2. Clique com o botão direito do mouse em **tabelas** e selecione **Adicionar nova tabela**.

   O Designer de Tabela é aberto e mostra uma grade com uma linha padrão, que representa uma única coluna na tabela que você está criando. Adicionando linhas à grade, você adicionará colunas na tabela.

3. Na grade, adicione uma linha para cada uma das seguintes entradas:

   |Nome da coluna|Tipo de dados|Permitir nulos|
   |-----------------|---------------|-----------------|
   |`CustomerID`|`nchar(5)`|Falso (desmarcado)|
   |`CompanyName`|`nvarchar(50)`|Falso (desmarcado)|
   |`ContactName`|`nvarchar (50)`|Verdadeiro (marcado)|
   |`Phone`|`nvarchar (24)`|Verdadeiro (marcado)|

4. Clique com o botão direito do mouse na `CustomerID` linha e selecione **definir chave primária**.

5. Clique com o botão direito do mouse na linha padrão ( `Id` ) e selecione **excluir**.

6. Nomeie a tabela Clientes atualizando a primeira linha no painel de script de acordo com o seguinte exemplo:

   ```sql
   CREATE TABLE [dbo].[Customers]
   ```

   Você deverá ver algo assim:

   ![Criador de Tabelas](../data-tools/media/table-designer.png)

7. No canto superior esquerdo da **Designer de tabela**, selecione **Atualizar**.

8. Na caixa de diálogo **Visualizar atualizações do banco de dados** , selecione **Atualizar banco de dados**.

   A tabela Customers é criada no arquivo de banco de dados local.

### <a name="create-the-orders-table"></a>Criar a tabela de pedidos

1. Adicione outra tabela e uma linha para cada entrada na seguinte tabela:

   |Nome da coluna|Tipo de dados|Permitir nulos|
   |-----------------|---------------|-----------------|
   |`OrderID`|`int`|Falso (desmarcado)|
   |`CustomerID`|`nchar(5)`|Falso (desmarcado)|
   |`OrderDate`|`datetime`|Verdadeiro (marcado)|
   |`OrderQuantity`|`int`|Verdadeiro (marcado)|

2. Defina **OrderID** como a chave primária e, em seguida, exclua a linha padrão.

3. Nomeie a tabela Orders atualizando a primeira linha no painel de script de acordo com o seguinte exemplo:

   ```sql
   CREATE TABLE [dbo].[Orders]
   ```

4. No canto superior esquerdo da **Designer de tabela**, selecione **Atualizar**.

5. Na caixa de diálogo **Visualizar atualizações do banco de dados** , selecione **Atualizar banco de dados**.

   A tabela Orders é criada no arquivo de banco de dados local. Se você expandir o nó **tabelas** no Gerenciador de servidores, verá as duas tabelas:

   ![Nó de tabelas expandido no Gerenciador de Servidores](media/server-explorer-tables-node.png)

### <a name="create-a-foreign-key"></a>Criar uma chave estrangeira

1. No painel de contexto no lado direito da grade de Designer de Tabela da tabela Orders, clique com o botão direito do mouse em **chaves estrangeiras** e selecione **Adicionar nova chave estrangeira**.

   ![Adicionar uma chave estrangeira em Designer de Tabela no Visual Studio](../data-tools/media/add-foreign-key.png)

2. Na caixa de texto exibida, substitua o texto pela **tabela** por **clientes**.

3. No painel T-SQL, atualize a última linha para corresponder ao exemplo a seguir:

   ```sql
   CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
   ```

4. No canto superior esquerdo da **Designer de tabela**, selecione **Atualizar**.

5. Na caixa de diálogo **Visualizar atualizações do banco de dados** , selecione **Atualizar banco de dados**.

   A chave estrangeira é criada.

## <a name="populate-the-tables-with-data"></a>Preencher as tabelas com dados

1. Em **Gerenciador de servidores** ou **pesquisador de objetos do SQL Server**, expanda o nó do banco de dados de exemplo.

2. Abra o menu de atalho para o nó **tabelas** , selecione **Atualizar**e, em seguida, expanda o nó **tabelas** .

3. Abra o menu de atalho da tabela clientes e selecione **Mostrar dados da tabela**.

4. Adicione quaisquer dados desejados para alguns clientes.

    É possível especificar cinco caracteres desejados como IDs de cliente, mas escolha pelo menos um do qual é possível se lembrar para uso posteriormente neste procedimento.

5. Abra o menu de atalho da tabela pedidos e selecione **Mostrar dados da tabela**.

6. Adicione dados para alguns pedidos.

    > [!IMPORTANT]
    > Verifique se todas as IDs de pedidos e quantidades de pedidos são inteiros e se cada ID de cliente corresponde a um valor que você especificou na coluna **CustomerID** da tabela Customers.

7. Na barra de menus, selecione **arquivo**  >  **salvar tudo**.

## <a name="see-also"></a>Veja também

- [Acessando dados no Visual Studio](accessing-data-in-visual-studio.md)
