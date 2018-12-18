---
title: 'Passo a passo: criando um Serviço de Dados WCF com WPF e Entity Framework'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data services in Visual Studio
- WCF Data Services, Visual Studio
- ADO.NET Data Services, Visual Studio
- WCF data services in Visual Studio
ms.assetid: da66ad1b-a25d-485c-af13-2d18f0422e3d
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: cbafb006091956ce5359bc6b575accd057b2ee37
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305345"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>Passo a passo: criando um Serviço de Dados WCF com WPF e Entity Framework
Este passo a passo demonstra como criar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] simples que é hospedado em um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e como acessá-lo de um aplicativo do Windows Forms.

Neste passo a passo você:

- Criará um aplicativo Web para hospedar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Criar uma [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] que representa o `Customers` tabela no banco de dados Northwind.

- Criará um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Criará um aplicativo cliente e adicionará uma referência ao [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Habilitará a associação de dados ao serviço e gerará a interface de usuário.

- Se desejar, adicionará recursos de filtragem ao aplicativo.

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (**Pesquisador de objetos do SQL Server** é instalado como parte do **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="creating-the-service"></a>Criando o serviço
Para criar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)], você adicionará um projeto Web, criará um [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] e, em seguida, criará o serviço usando o modelo.

A primeira etapa, você adiciona um projeto web para hospedar o serviço.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-the-web-project"></a>Para criar o projeto Web

1. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.

2. Na caixa de diálogo **Novo Projeto**, expanda os nós **Visual Basic** ou **Visual C#** e **Web** e escolha o modelo **Aplicativo Web ASP .NET**.

3. Na caixa de texto **Nome**, insira **NorthwindWeb** e escolha o botão **OK**.

4. Na caixa de diálogo **Novo Projeto ASP.NET**, na lista **Selecionar um modelo**, escolha **Vazio** e o botão **OK**.

A próxima etapa, você criará um [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] que representa o `Customers` tabela no banco de dados Northwind.

### <a name="to-create-the-entity-data-model"></a>Para criar o Modelo de Dados de Entidade

1. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar Novo Item**, escolha o nó **Dados** e, em seguida, o item **Modelo de Dados de Entidade ADO.NET**.

3. No **nome** texto, digite `NorthwindModel`e, em seguida, escolha o **Add** botão.

     O Assistente do Modelo de Dados de Entidade é aberto.

4. No Assistente de modelo de dados de entidade, na **escolher conteúdo do modelo** , escolha o **EF Designer do banco de dados** item e, em seguida, escolha o **próxima** botão.

5. Na página **Escolha a Conexão de Dados**, executa uma das seguintes etapas:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-a.

         -ou-

    -   Escolha o botão **Nova Conexão** para configurar uma nova conexão de dados. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

6. Se o banco de dados exigir uma senha, escolha o botão de opção **Sim, incluir os dados confidenciais da cadeia de conexão** e escolha o botão **Avançar**.

    > [!NOTE]
    > Se uma caixa de diálogo for exibida, escolha **Sim** para salvar o arquivo no seu projeto.

7. Na página **Escolha sua versão**, escolha o botão de opção **Entity Framework 5.0** e o botão **Avançar**.

    > [!NOTE]
    > Para usar a versão mais recente do Entity Framework 6 com Serviço WCF, você precisará instalar o pacote NuGet do provedor do Entity Framework do WCF Data Services. Ver [usar o WCF Data Services 5.6.0 com o Entity Framework 6 +](https://blogs.msdn.microsoft.com/odatateam/2013/10/02/using-wcf-data-services-5-6-0-with-entity-framework-6/).

8. Na página **Escolher Objetos do Banco de Dados**, expanda o nó **Tabelas**, marque a caixa de seleção **Clientes** e escolha o botão **Concluir**.

     Exibe o diagrama de modelo de entidade e um *NorthwindModel* arquivo é adicionado ao seu projeto.

Na próxima etapa, você pode cria e testar o serviço de dados.

### <a name="to-create-the-data-service"></a>Para criar o serviço de dados

1. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar Novo Item**, escolha o nó **Web** e, em seguida, o item **WCF Data Services 5.6**.

3. No **nome** texto, digite `NorthwindCustomers`e, em seguida, escolha o **Add** botão.

     O arquivo **NorthwindCustomers.svc** aparece no **Editor de Códigos**.

4. No **Editor de Códigos**, localize o primeiro comentário `TODO:` e substitua o código pelo seguinte:

     [!code-vb[WCFDataServiceWalkthrough#1](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework_1.vb)]
     [!code-csharp[WCFDataServiceWalkthrough#1](../data-tools/codesnippet/CSharp/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework_1.cs)]

5. Substitua os comentários no manipulador de eventos `InitializeService` pelo seguinte código:

     [!code-vb[WCFDataServiceWalkthrough#2](../data-tools/codesnippet/VisualBasic/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework_2.vb)]
     [!code-csharp[WCFDataServiceWalkthrough#2](../data-tools/codesnippet/CSharp/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework_2.cs)]

6. Na barra de menus, escolha **Debug** > **Start Without Debugging** para executar o serviço. Uma janela do navegador abre e exibe o esquema XML para o serviço.

7. No **endereço** barra, insira `Customers` no final da URL **Northwindcustomers**e, em seguida, escolha o **Enter** chave.

     Uma representação XML dos dados no `Customers` tabela é exibida.

    > [!NOTE]
    > Em alguns casos, o Internet Explorer interpretará incorretamente os dados como um RSS feed. Você deve verificar se a opção para exibir RSS feeds está desabilitada. Para obter mais informações, consulte [Solucionando problemas de referências de serviço](../data-tools/troubleshooting-service-references.md).

8. Feche a janela do navegador.

As próximas etapas, você cria um aplicativo de cliente do Windows Forms para consumir o serviço.

## <a name="creating-the-client-application"></a>Criando o aplicativo cliente
 Para criar o aplicativo cliente, você adiciona um segundo projeto, adiciona uma referência de serviço ao projeto, configura uma fonte de dados e cria uma interface do usuário para exibir os dados do serviço.

 Na primeira etapa, você pode adicionar um projeto do Windows Forms à solução e defini-lo como o projeto de inicialização.

### <a name="to-create-the-client-application"></a>Para criar o aplicativo cliente

1. Na barra de menus, escolha arquivo, **Add** > **novo projeto**.

2. No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó, escolha o **Windows** nó e, em seguida, escolha  **Aplicativo de formulários do Windows**.

3. Na caixa de texto **Nome**, insira `NorthwindClient` e, em seguida, escolha o botão **OK**.

4. No **Gerenciador de Soluções**, escolha o nó de projeto **NorthwindClient**.

5. Na barra de menus, escolha **Projeto**, **Definir como Projeto de Inicialização**.

Na próxima etapa, você adiciona uma referência de serviço para o [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] no projeto da web.

### <a name="to-add-a-service-reference"></a>Para adicionar uma referência de serviço

1. Na barra de menus, escolha **Project** > **Add Service Reference**.

2. Na caixa de diálogo **Adicionar Referência de Serviço**, escolha o botão **Descobrir**.

     A URL do serviço NorthwindCustomers é exibida no campo **Endereço**.

3. Escolha o botão **OK** para adicionar a referência de serviço.

Na próxima etapa, você deve configurar uma fonte de dados para habilitar a associação de dados para o serviço.

### <a name="to-enable-data-binding-to-the-service"></a>Para habilitar a associação de dados ao serviço

1. Na barra de menus, escolha **modo de exibição** > **Other Windows** > **fontes de dados**.

   A janela **Fontes de Dados** é aberta.

2. Na janela **Fontes de Dados**, escolha o botão **Adicionar Nova Fonte de Dados**.

3. Na página **Escolher um Tipo de Fonte de Dados** do **Assistente de Configuração de Fonte de Dados**, escolha **Objeto** e, em seguida, o botão **Próximo**.

4. Na página **Selecionar os Objetos de Dados**, expanda os nós **NorthwindClient** e **NorthwindClient.ServiceReference1**.

5. Marque a caixa de seleção **Customer** e escolha o botão **Finalizar**.

A próxima etapa, você cria a interface do usuário que exibe os dados do serviço.

### <a name="to-create-the-user-interface"></a>Para criar a interface do usuário

1. Na janela **Fontes de Dados**, abra o menu de atalho do nó **Clientes** e escolha **Copiar**.

2. No designer de formulários **Form1.vb** ou **Form1.cs**, abra o menu de atalho e escolha **Colar**.

    Um controle <xref:System.Windows.Forms.DataGridView>, um componente <xref:System.Windows.Forms.BindingSource> e um componente <xref:System.Windows.Forms.BindingNavigator> são adicionados ao formulário.

3. Escolha o **CustomersDataGridView** controle e, em seguida, no **propriedades** conjunto de janela a **Dock** propriedade a ser **preencher**.

4. Na **Gerenciador de soluções**, abra o menu de atalho para o **Form1** nó e escolha **Exibir código** para abrir o Editor de códigos e adicione o seguinte `Imports` ou `Using`instrução na parte superior do arquivo:

   ```vb
   Imports NorthwindClient.ServiceReference1
   ```

   ```csharp
   using NorthwindClient.ServiceReference1;
   ```

5. Adicione o seguinte código ao manipulador de eventos do `Form1_Load`:

   ```vb
   Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
           Dim proxy As New NorthwindEntities _
   (New Uri("http://localhost:53161/NorthwindCustomers.svc/"))
           Me.CustomersBindingSource.DataSource = proxy.Customers
       End Sub
   ```

   ```csharp
   private void Form1_Load(object sender, EventArgs e)
   {
   NorthwindEntities proxy = new NorthwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc/"));
   this.CustomersBindingSource.DataSource = proxy.Customers;
   }
   ```

6. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo **NorthwindCustomers.svc** e escolha **Exibir no Navegador**. Internet Explorer é aberto e exibe o esquema XML para o serviço.

7. Copie a URL da barra de endereços do Internet Explorer.

8. No código que você adicionou na etapa 4, selecione `http://localhost:53161/NorthwindCustomers.svc/` e o substitua pela URL que acabou de copiar.

9. Na barra de menus, escolha **Debug** > **iniciar depuração** para executar o aplicativo. As informações do cliente são mostradas.

   Agora você tem um aplicativo funcional que exibe uma lista de clientes do serviço NorthwindCustomers. Se desejar expor dados adicionais por meio do serviço, você pode modificar o [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] para incluir tabelas adicionais do banco de dados da Northwind.

A próxima etapa opcional, você aprenderá como filtrar os dados que são retornados pelo serviço.

## <a name="adding-filtering-capabilities"></a>Adicionando recursos de filtragem
 Nesta etapa, você deve personalizar o aplicativo para filtrar os dados por cidade do cliente.

### <a name="to-add-filtering-by-city"></a>Para adicionar a filtragem por cidade

1. No **Gerenciador de Soluções**, abra o menu de atalho do nó **Form1.vb** ou **Form1.cs** e escolha **Abrir**.

2. Adicione um controle <xref:System.Windows.Forms.TextBox> e um controle <xref:System.Windows.Forms.Button> da **Caixa de Ferramentas** ao formulário.

3. Abra o menu de atalho para o <xref:System.Windows.Forms.Button> de controle, escolha **Exibir código**e, em seguida, adicione o seguinte código no `Button1_Click` manipulador de eventos:

    ```vb
    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
            Dim proxy As New northwindEntities _
    (New Uri("http://localhost:53161/NorthwindCustomers.svc"))
            Dim city As String = TextBox1.Text

            If city <> "" Then
                Me.CustomersBindingSource.DataSource = From c In _
             proxy.Customers Where c.City = city
            End If

        End Sub
    ```

    ```csharp
    private void Button1_Click(object sender, EventArgs e)
    {
    ServiceReference1.northwindModel.northwindEntities proxy = new northwindEntities(new Uri("http://localhost:53161/NorthwindCustomers.svc"));
    string city = TextBox1.Text;

    if (!string.IsNullOrEmpty(city)) {
    this.CustomersBindingSource.DataSource = from c in proxy.Customers where c.City == city;
    }

    }
    ```

4. No código anterior, substitua `http://localhost:53161/NorthwindCustomers.svc` pela URL do manipulador de eventos `Form1_Load`.

5. Na barra de menus, escolha **Debug** > **iniciar depuração** para executar o aplicativo.

6. Na caixa de texto, insira **Londres** e escolha o botão. Somente os clientes de London são exibidos.

## <a name="see-also"></a>Consulte também

- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
- [Como adicionar, atualizar ou remover uma referência de WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)