---
title: Criar um aplicativo de dados simples usando o ADO.NET
ms.date: 08/23/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: 2222841f-e443-4a3d-8c70-4506aa905193
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 75043a1716cca0c727eb0530cd63ca715a60424b
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53064866"
---
# <a name="create-a-simple-data-application-by-using-adonet"></a>Criar um aplicativo de dados simples usando o ADO.NET

Quando você cria um aplicativo que manipule dados em um banco de dados, você pode executar tarefas básicas como definir cadeias de caracteres de conexão, inserção de dados e executar procedimentos armazenados. Ao seguir este tópico, você pode descobrir como interagir com um banco de dados de dentro de um aplicativo simples de "formulários sobre dados" do Windows Forms usando o Visual c# ou Visual Basic e ADO.NET.  Todas as tecnologias de dados do .NET — inclusive conjuntos de dados, o LINQ to SQL e Entity Framework —, por fim, execute as etapas que são muito semelhantes às mostradas neste artigo.

Este artigo demonstra uma maneira simples de obter dados para fora de um banco de dados de uma maneira rápida. Se seu aplicativo precisa modificar dados de maneiras não triviais e atualizar o banco de dados, você deve considerar usando o Entity Framework e usando a associação de dados para sincronizar automaticamente os controles de interface do usuário para as alterações nos dados subjacentes.

> [!IMPORTANT]
> Para manter o código simples, ele não inclui tratamento de exceção pronta para produção.

## <a name="prerequisites"></a>Pré-requisitos

Para criar o aplicativo, você precisará de:

-   Visual Studio.

-   LocalDB do SQL Server Express. Se você não tiver o SQL Server Express LocalDB, você pode instalá-lo partir o [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express).

Este tópico pressupõe que você está familiarizado com a funcionalidade básica do IDE do Visual Studio e pode criar um aplicativo Windows Forms, adicionar formulários para o projeto, colocar botões e outros controles em formulários, definem propriedades de controles e codificar eventos simples. Se você não estiver confortável com essas tarefas, sugerimos que você conclua a [Introdução ao Visual c# e Visual Basic](../ide/getting-started-with-visual-csharp-and-visual-basic.md) tópico antes de começar este passo a passo.

## <a name="set-up-the-sample-database"></a>Configurar o banco de dados de exemplo

Crie o banco de dados de exemplo seguindo estas etapas:

1. No Visual Studio, abra o **Gerenciador de servidores** janela.

2. Clique duas vezes em **conexões de dados** e escolha **Create New SQL Server Database**.

3. No **nome do servidor** texto, digite **(localdb) \mssqllocaldb**.

4. No **nome do novo banco de dados** texto, digite **vendas**, em seguida, escolha **Okey**.

     A esvaziar **vendas** banco de dados é criado e adicionado ao nó de conexões de dados no Gerenciador de servidores.

5. Clique com botão direito no **Sales** conexão de dados e selecione **nova consulta**.

     Abre uma janela do editor de consulta.

6. Cópia de [script Transact-SQL de vendas](https://github.com/MicrosoftDocs/visualstudio-docs/raw/master/docs/data-tools/samples/sales.sql) na área de transferência.

7. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

     Após alguns instantes, a consulta termina a execução e os objetos de banco de dados são criados. O banco de dados contém duas tabelas: Os clientes e pedidos. Essas tabelas não contêm dados inicialmente, mas você pode adicionar dados ao executar o aplicativo que você vai criar. O banco de dados também contém quatro procedimentos armazenados simples.

## <a name="create-the-forms-and-add-controls"></a>Criar os formulários e adicionar controles

1. Criar um projeto para um aplicativo do Windows Forms e nomeie- **SimpleDataApp**.

    O Visual Studio cria o projeto e vários arquivos, incluindo um formulário vazio do Windows chamado **Form1**.

2. Adicione dois formulários do Windows ao seu projeto para que ele tenha três formulários e forneça a eles os seguintes nomes:

   -   **Navegação**

   -   **NewCustomer**

   -   **FillOrCancel**

3. Para cada formulário, adicione as caixas de texto, botões e outros controles que aparecem nas ilustrações a seguir. Para cada controle, defina as propriedades que descrevem as tabelas.

   > [!NOTE]
   > A caixa de grupo e os controles de rótulo adicionam clareza mas não são usados no código.

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
|TextBox|Nome = txtCustomerID<br /><br /> ReadOnly = True|
|Botão|Nome = btnCreateAccount|
|NumericUpdown|DecimalPlaces = 0<br /><br /> Máximo = 5000<br /><br /> Nome = numOrderAmount|
|DateTimePicker|Formato = abreviado<br /><br /> Nome = dtpOrderDate|
|Botão|Nome = btnPlaceOrder|
|Botão|Nome = btnAddAnotherAccount|
|Botão|Nome = btnAddFinish|

 **Formulário FillOrCancel**

 ![preencher ou Cancelar ordens](../data-tools/media/simpleappcancelfill.png)

|Controles para o formulário FillOrCancel|Propriedades|
| - |----------------|
|TextBox|Nome = txtOrderID|
|Botão|Nome = btnFindByOrderID|
|DateTimePicker|Formato = abreviado<br /><br /> Nome = dtpFillDate|
|DataGridView|Nome = dgvCustomerOrders<br /><br /> ReadOnly = True<br /><br /> RowHeadersVisible = False|
|Botão|Nome = btnCancelOrder|
|Botão|Nome = btnFillOrder|
|Botão|Nome = btnFinishUpdates|

## <a name="store-the-connection-string"></a>A cadeia de caracteres de conexão da Store
 Quando seu aplicativo tenta abrir uma conexão ao banco de dados, seu aplicativo deve ter acesso à cadeia de conexão. Para evitar inserir a cadeia de caracteres manualmente em cada formulário, armazenar a cadeia de caracteres na *App. config* no seu projeto e crie um método que retorna a cadeia de caracteres quando o método é chamado de qualquer formulário em seu aplicativo.

 Você pode encontrar a cadeia de conexão clicando com o **Sales** conexão de dados no **Gerenciador de servidores** e selecionando **propriedades**. Localize o **ConnectionString** propriedade, em seguida, use **Ctrl**+**um**, **Ctrl**+**C**  para selecionar e copiar a cadeia de caracteres para a área de transferência.

1.  Se você estiver usando c#, em **Gerenciador de soluções**, expanda o **Properties** nó sob o projeto e, em seguida, abra o **Settings** arquivo.
    Se você estiver usando Visual Basic, em **Gerenciador de soluções**, clique em **Show All Files**, expanda o **My Project** nó e, em seguida, abra o **Settings** arquivo.

2.  No **nome** coluna, digite `connString`.

3.  No **tipo** lista, selecione **(cadeia de caracteres de Conexão)**.

4.  No **escopo** lista, selecione **aplicativo**.

5.  No **valor** coluna, insira sua cadeia de conexão (sem qualquer fora de aspas) e, em seguida, salve suas alterações.

> [!NOTE]
> Em um aplicativo real, você deve armazenar a cadeia de caracteres de conexão com segurança, conforme descrito em [cadeias de caracteres de Conexão e arquivos de configuração](/dotnet/framework/data/adonet/connection-strings-and-configuration-files).

##  <a name="write-the-code-for-the-forms"></a>Escreva o código para os formulários

Esta seção contém uma breve visão geral do que cada formulário faz. Ele também fornece o código que define a lógica subjacente quando um botão no formulário é clicado.

### <a name="navigation-form"></a>Formulário de navegação

O formulário navegação abre quando você executar o aplicativo. O **adicionar uma conta** botão abre o formulário NewCustomer. O **preencher ou Cancelar ordens** botão abre o formulário FillOrCancel. O **Exit** botão fecha o aplicativo.

#### <a name="make-the-navigation-form-the-startup-form"></a>Tornar a navegação formam o formulário de inicialização

Se você estiver usando c#, em **Gerenciador de soluções**, abra **Program.cs**e, em seguida, altere o `Application.Run` linha a esta: `Application.Run(new Navigation());`

Se você estiver usando Visual Basic, em **Gerenciador de soluções**, abra o **Properties** janela, selecione o **aplicativo** guia e, em seguida, selecione  **Simpledataapp** no **formulário de inicialização** lista.

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerado automaticamente

Clique duas vezes em três botões no formulário de navegação para criar métodos do manipulador de eventos vazio. Também clicar duas vezes nos botões adiciona o código gerado automaticamente no arquivo de código de Designer que permite que um clique de botão disparar um evento.

#### <a name="add-code-for-the-navigation-form-logic"></a>Adicione código para a lógica de formulário de navegação

Na página de código para o formulário de navegação, completa os corpos de método para o botão três manipuladores de eventos clicar conforme mostrado no código a seguir.

[!code-csharp[Navigation#1](../data-tools/codesnippet/CSharp/SimpleDataApp/Navigation.cs#1)]
[!code-vb[Navigation#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/Navigation.vb#1)]

### <a name="newcustomer-form"></a>Formulário NewCustomer

Quando você inserir um nome de cliente e, em seguida, selecione a **criar conta** botão, o formulário de NewCustomer cria uma conta de cliente e do SQL Server retorna um valor de identidade como a nova ID do cliente. Em seguida, você pode fazer um pedido para a nova conta especificando um valor e uma data do pedido e selecionando o **fazer pedido** botão.

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerado automaticamente

Criar um vazio, clique em cada botão no formulário de NewCustomer clicando duas vezes em cada um dos quatro botões no manipulador de eventos. Também clicar duas vezes nos botões adiciona o código gerado automaticamente no arquivo de código de Designer que permite que um clique de botão disparar um evento.

#### <a name="add-code-for-the-newcustomer-form-logic"></a>Adicione código para a lógica de formulário de NewCustomer

Para concluir a lógica de formulário de NewCustomer, siga estas etapas.

1. Traga o `System.Data.SqlClient` namespace no escopo para que você não precise totalmente qualificar os nomes de seus membros.

     ```csharp
     using System.Data.SqlClient;
     ```
     ```vb
     Imports System.Data.SqlClient
     ```

2. Adicione algumas variáveis e métodos auxiliares à classe, conforme mostrado no código a seguir.

     [!code-csharp[NewCustomer#1](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#1)]
     [!code-vb[NewCustomer#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#1)]

3. Concluída os corpos de método para o botão quatro clique manipuladores de eventos conforme mostrado no código a seguir.

     [!code-csharp[NewCustomer#2](../data-tools/codesnippet/CSharp/SimpleDataApp/NewCustomer.cs#2)]
     [!code-vb[NewCustomer#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/NewCustomer.vb#2)]

### <a name="fillorcancel-form"></a>Formulário FillOrCancel

O formulário FillOrCancel executa uma consulta para retornar uma ordem quando você inserir uma ID de pedido e, em seguida, clique no **localizar ordem** botão. A linha retornada aparece em uma grade de dados somente leitura. Você pode marcar a ordem como cancelada (X), se você selecionar o **Cancelar pedido** botão, ou você pode marcar a ordem como preenchida (F) se você selecionar a **preencher ordem** botão. Se você selecionar o **localizar ordem** novamente no botão, a linha atualizada aparecerá.

#### <a name="create-auto-generated-event-handlers"></a>Criar manipuladores de eventos gerado automaticamente

Criar vazio clique manipuladores de eventos para os quatro botões no formulário FillOrCancel clicando duas vezes nos botões. Também clicar duas vezes nos botões adiciona o código gerado automaticamente no arquivo de código de Designer que permite que um clique de botão disparar um evento.

#### <a name="add-code-for-the-fillorcancel-form-logic"></a>Adicione código para a lógica de formulário FillOrCancel

Para concluir a lógica de formulário de FillOrCancel, siga estas etapas.

1. Trazer os namespaces a seguir para o escopo para que você não precise qualificar totalmente os nomes de seus membros.

     ```csharp
     using System.Data.SqlClient;
     using System.Text.RegularExpressions;
     ```
     ```vb
     Imports System.Data.SqlClient
     Imports System.Text.RegularExpressions
     ```

2. Adicione um método de variável e auxiliares à classe, conforme mostrado no código a seguir.

     [!code-csharp[FillOrCancel#1](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#1)]
     [!code-vb[FillOrCancel#1](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#1)]

3. Concluída os corpos de método para o botão quatro clique manipuladores de eventos conforme mostrado no código a seguir.

     [!code-csharp[FillOrCancel#2](../data-tools/codesnippet/CSharp/SimpleDataApp/FillOrCancel.cs#2)]
     [!code-vb[FillOrCancel#2](../data-tools/codesnippet/VisualBasic/SimpleDataApp/FillOrCancel.vb#2)]

## <a name="test-your-application"></a>Testar seu aplicativo

Selecione o **F5** tecla para compilar e testar seu aplicativo depois que você codifica cada manipulador de eventos de clique e, em seguida, depois de concluir a codificação.

## <a name="see-also"></a>Consulte também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
