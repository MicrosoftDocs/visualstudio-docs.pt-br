---
title: Criar um aplicativo de dados simples usando o ADO.NET
description: Aprenda a criar um aplicativo simples de formulário para dados usando Windows Forms e ADO.NET no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 08/23/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c499e36b7ee6bb15980fe89c6185a105681d4d05
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106216495"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>Criar um aplicativo de dados simples usando o ADO.NET

Quando você cria um aplicativo que manipula dados em um banco de dado, executa tarefas básicas, como definir cadeias de conexão, inserir dados e executar procedimentos armazenados. Ao seguir este tópico, você pode descobrir como interagir com um banco de dados de dentro de um aplicativo simples Windows Forms "formulários por data" usando o Visual C# ou Visual Basic e ADO.NET.  Todas as tecnologias de dados do .NET, incluindo conjuntos, LINQ to SQL e Entity Framework, por fim, executam etapas muito semelhantes às mostradas neste artigo.

Este artigo demonstra uma maneira simples de obter dados de um banco de dado de maneira rápida. Se seu aplicativo precisar modificar dados de maneiras não triviais e atualizar o banco de dado, você deverá considerar o uso de Entity Framework e o uso da vinculação de dados para sincronizar automaticamente os controles de interface do usuário com as alterações nos dados subjacentes.

> [!IMPORTANT]
> Para manter o código simples, ele não inclui manipulação de exceção pronta para produção.

## <a name="prerequisites"></a>Pré-requisitos

Para criar o aplicativo, você precisará de:

- Visual Studio.

- LocalDB do SQL Server Express. Se você não tiver SQL Server Express LocalDB, poderá instalá-lo na [página de download SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express).

Este tópico pressupõe que você esteja familiarizado com a funcionalidade básica do IDE do Visual Studio e pode criar um aplicativo Windows Forms, adicionar formulários ao projeto, colocar botões e outros controles nos formulários, definir propriedades dos controles e codificar eventos simples. Se você não estiver familiarizado com essas tarefas, sugerimos que você conclua o tópico [introdução ao Visual C# e à Visual Basic antes de](../ide/quickstart-visual-basic-console.md) iniciar este passo a passos.

## <a name="set-up-the-sample-database"></a>Configurar o banco de dados de exemplo

Crie o banco de dados de exemplo seguindo estas etapas:

1. No Visual Studio, abra a janela **Gerenciador de servidores** .

2. Clique com o botão direito do mouse em **conexões de dados** e escolha **criar novo banco de SQL Server**.

3. Na caixa de texto **nome do servidor** , digite **(LocalDB) \mssqllocaldb**.

4. Na caixa de texto **nome do novo banco de dados** , insira **vendas** e escolha **OK**.

     O banco de dados de **vendas** vazio é criado e adicionado ao nó conexões de Data no Gerenciador de servidores.

5. Clique com o botão direito do mouse na conexão dados de **vendas** e selecione **nova consulta**.

     Uma janela do editor de consultas é aberta.

6. Copie o [script Transact-SQL Sales](https://github.com/MicrosoftDocs/visualstudio-docs/raw/master/docs/data-tools/samples/sales.sql) para a área de transferência.

7. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

     Após um curto período, a consulta terminará de ser executada e os objetos de banco de dados serão criados. O banco de dados contém duas tabelas: Customer e Orders. Essas tabelas não contêm dados inicialmente, mas você pode adicionar dados ao executar o aplicativo que você criará. O banco de dados também contém quatro procedimentos armazenados simples.

## <a name="create-the-forms-and-add-controls"></a>Criar os formulários e adicionar controles

1. Crie um projeto para um aplicativo Windows Forms e nomeie-o **SimpleDataApp**.

    O Visual Studio cria o projeto e vários arquivos, incluindo um Windows Form vazio chamado **Form1**.

2. Adicione dois formulários do Windows ao seu projeto para que ele tenha três formulários e dê a eles os seguintes nomes:

   - **Navegação**

   - **NewCustomer**

   - **FillOrCancel**

3. Para cada formulário, adicione as caixas de texto, os botões e outros controles que aparecem nas ilustrações a seguir. Para cada controle, defina as propriedades que as tabelas descrevem.

   > [!NOTE]
   > A caixa de grupo e os controles de rótulo adicionam clareza, mas não são usados no código.

   **Formulário de navegação**

   ![Caixa de diálogo de navegação](../data-tools/media/simpleappnav.png)

|Controles para o formulário de navegação|Propriedades|
| - |----------------|
|Botão|Nome = btnGoToAdd|
|Botão|Nome = btnGoToFillOrCancel|
|Botão|Nome = btnExit|

**Formulário NewCustomer**

![Adicionar um novo cliente e fazer um pedido](../data-tools/media/simpleappnewcust.png)

|Controles para o formulário NewCustomer|Propriedades|
| - |----------------|
|TextBox|Nome = txtCustomerName|
|TextBox|Nome = txtCustomerID<br /><br /> ReadOnly = true|
|Botão|Nome = btnCreateAccount|
|NumericUpdown|DecimalPlaces = 0<br /><br /> Máximo = 5000<br /><br /> Nome = numOrderAmount|
|DateTimePicker|Formato = curto<br /><br /> Nome = dtpOrderDate|
|Botão|Nome = btnPlaceOrder|
|Botão|Nome = btnAddAnotherAccount|
|Botão|Nome = btnAddFinish|

**Formulário FillOrCancel**

![preencher ou cancelar pedidos](../data-tools/media/simpleappcancelfill.png)

|Controles para o formulário FillOrCancel|Propriedades|
| - |----------------|
|TextBox|Nome = txtOrderID|
|Botão|Nome = btnFindByOrderID|
|DateTimePicker|Formato = curto<br /><br /> Nome = dtpFillDate|
|DataGridView|Nome = dgvCustomerOrders<br /><br /> ReadOnly = true<br /><br /> RowHeadersVisible = False|
|Botão|Nome = btnCancelOrder|
|Botão|Nome = btnFillOrder|
|Botão|Nome = btnFinishUpdates|

## <a name="store-the-connection-string"></a>Armazenar a cadeia de conexão
Quando seu aplicativo tenta abrir uma conexão com o banco de dados, seu aplicativo deve ter acesso à cadeia de conexão. Para evitar inserir a cadeia de caracteres manualmente em cada formulário, armazene a cadeia de caracteres no arquivo de *App.config* em seu projeto e crie um método que retorne a cadeia de caracteres quando o método for chamado de qualquer formulário em seu aplicativo.

Você pode encontrar a cadeia de conexão clicando com o botão direito do mouse na conexão dados de **vendas** em **Gerenciador de servidores** e escolhendo **Propriedades**. Localize a propriedade **ConnectionString** e, em seguida, use **Ctrl** + **A**, **Ctrl** + **C** para selecionar e copiar a cadeia de caracteres para a área de transferência.

1. Se você estiver usando C#, em **Gerenciador de soluções**, expanda o nó **Propriedades** no projeto e, em seguida, abra o arquivo **Settings. Settings** .
    Se você estiver usando Visual Basic, em **Gerenciador de soluções**, clique em **Mostrar todos os arquivos**, expanda o nó **meu projeto** e, em seguida, abra o arquivo **Settings. Settings** .

2. Na coluna **nome** , digite `connString` .

3. Na lista **tipo** , selecione **(cadeia de conexão)**.

4. Na lista **escopo** , selecione **aplicativo**.

5. Na coluna **valor** , insira sua cadeia de conexão (sem aspas externas) e, em seguida, salve as alterações.

> [!NOTE]
> Em um aplicativo real, você deve armazenar a cadeia de conexão com segurança, conforme descrito em [cadeias de conexão e arquivos de configuração](/dotnet/framework/data/adonet/connection-strings-and-configuration-files).

## <a name="write-the-code-for-the-forms"></a>Escreva o código para os formulários

Esta seção contém breves visões gerais do que cada formulário faz. Ele também fornece o código que define a lógica subjacente quando um botão no formulário é clicado.

### <a name="navigation-form"></a>Formulário de navegação

O formulário de navegação é aberto quando você executa o aplicativo. O botão **Adicionar uma conta** abre o formulário NewCustomer. O botão **preencher ou cancelar pedidos** abre o formulário FillOrCancel. O botão **sair** fecha o aplicativo.

#### <a name="make-the-navigation-form-the-startup-form"></a>Tornar o formulário de navegação o formulário de inicialização

Se você estiver usando C#, em **Gerenciador de soluções**, abra **Program. cs** e, em seguida, altere a `Application.Run` linha para: `Application.Run(new Navigation());`

Se você estiver usando Visual Basic, em **Gerenciador de soluções**, abra a janela **Propriedades** , selecione a guia **aplicativo** e, em seguida, selecione **SimpleDataApp. Navigation** na lista **formulário de inicialização** .

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerados automaticamente

Clique duas vezes nos três botões no formulário de navegação para criar métodos de manipulador de eventos vazios. Clicar duas vezes nos botões também adiciona o código gerado automaticamente no arquivo de código do designer que habilita um clique de botão para gerar um evento.

#### <a name="add-code-for-the-navigation-form-logic"></a>Adicionar código para a lógica do formulário de navegação

Na página de código do formulário de navegação, conclua os corpos de método dos manipuladores de eventos de clique de três botões, conforme mostrado no código a seguir.

:::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/Navigation.cs" id="Snippet1":::
:::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/Navigation.vb" id="Snippet1":::

### <a name="newcustomer-form"></a>Formulário NewCustomer

Quando você insere um nome de cliente e, em seguida, seleciona o botão **criar conta** , o formulário NewCustomer cria uma conta de cliente e SQL Server retorna um valor de identidade como a nova ID do cliente. Em seguida, você pode fazer um pedido para a nova conta especificando uma quantidade e uma data de pedido e selecionando o botão **fazer pedido** .

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerados automaticamente

Crie um manipulador de eventos de clique vazio para cada botão no formulário NewCustomer clicando duas vezes em cada um dos quatro botões. Clicar duas vezes nos botões também adiciona o código gerado automaticamente no arquivo de código do designer que habilita um clique de botão para gerar um evento.

#### <a name="add-code-for-the-newcustomer-form-logic"></a>Adicionar código para a lógica do formulário NewCustomer

Para concluir a lógica do formulário NewCustomer, siga estas etapas.

1. Coloque o `System.Data.SqlClient` namespace no escopo para que você não precise qualificar totalmente os nomes de seus membros.

     ```csharp
     using System.Data.SqlClient;
     ```

     ```vb
     Imports System.Data.SqlClient
     ```

2. Adicione algumas variáveis e métodos auxiliares à classe, conforme mostrado no código a seguir.

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs" id="Snippet1":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb" id="Snippet1":::

3. Conclua os corpos de método para os quatro manipuladores de eventos de clique no botão, conforme mostrado no código a seguir.

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs" id="Snippet2":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb" id="Snippet2":::

### <a name="fillorcancel-form"></a>Formulário FillOrCancel

O formulário FillOrCancel executa uma consulta para retornar um pedido quando você insere uma ID do pedido e, em seguida, clica no botão **Localizar ordem** . A linha retornada aparece em uma grade de dados somente leitura. Você pode marcar a ordem como cancelada (X) se selecionar o botão **Cancelar pedido** , ou pode marcar a ordem como preenchida (F) se você selecionar o botão **ordem de preenchimento** . Se você selecionar o botão **Localizar ordem** novamente, a linha atualizada será exibida.

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerados automaticamente

Crie manipuladores de eventos de clique vazios para os quatro botões no formulário FillOrCancel clicando duas vezes nos botões. Clicar duas vezes nos botões também adiciona o código gerado automaticamente no arquivo de código do designer que habilita um clique de botão para gerar um evento.

#### <a name="add-code-for-the-fillorcancel-form-logic"></a>Adicionar código para a lógica do formulário FillOrCancel

Para concluir a lógica do formulário FillOrCancel, siga estas etapas.

1. Coloque os dois namespaces a seguir no escopo para que você não precise qualificar totalmente os nomes de seus membros.

     ```csharp
     using System.Data.SqlClient;
     using System.Text.RegularExpressions;
     ```

     ```vb
     Imports System.Data.SqlClient
     Imports System.Text.RegularExpressions
     ```

2. Adicione uma variável e um método auxiliar à classe, conforme mostrado no código a seguir.

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs" id="Snippet1":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb" id="Snippet1":::

3. Conclua os corpos de método para os quatro manipuladores de eventos de clique no botão, conforme mostrado no código a seguir.

     :::code language="csharp" source="../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs" id="Snippet2":::
     :::code language="vb" source="../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb" id="Snippet2":::

## <a name="test-your-application"></a>Teste seu aplicativo

Selecione a tecla **F5** para compilar e testar seu aplicativo depois de codificar cada manipulador de eventos de clique e depois de concluir a codificação.

## <a name="see-also"></a>Confira também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
