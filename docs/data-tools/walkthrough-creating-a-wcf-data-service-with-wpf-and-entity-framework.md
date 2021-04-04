---
title: Criar um serviço de dados WCF com o & do WPF Entity Framework
description: Crie um serviço de dados WCF com o WPF e Entity Framework hospedados em um aplicativo Web ASP.NET e, em seguida, acesse-o de um aplicativo Windows Forms.
ms.custom: SEO-VS-2020
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
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: f519d8e3bfe01fc3e4a1e4cfe82f4f8502c84821
ms.sourcegitcommit: 80fc9a72e9a1aba2d417dbfee997fab013fc36ac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/02/2021
ms.locfileid: "106215689"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>Passo a passo: criando um Serviço de Dados WCF com WPF e Entity Framework
Este passo a passo demonstra como criar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] simples que é hospedado em um aplicativo Web do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] e como acessá-lo de um aplicativo do Windows Forms.

Neste tutorial, você:

- Criará um aplicativo Web para hospedar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Crie um [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] que represente a `Customers` tabela no banco de dados Northwind.

- Criará um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Criará um aplicativo cliente e adicionará uma referência ao [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)].

- Habilitará a associação de dados ao serviço e gerará a interface de usuário.

- Se desejar, adicionará recursos de filtragem ao aplicativo.

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O **pesquisador de objetos do SQL Server** é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="creating-the-service"></a>Criando o serviço
Para criar um [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)], você adicionará um projeto Web, criará um [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] e, em seguida, criará o serviço usando o modelo.

Na primeira etapa, você adiciona um projeto Web para hospedar o serviço.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-the-web-project"></a>Para criar o projeto Web

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na caixa de diálogo **Novo Projeto**, expanda os nós **Visual Basic** ou **Visual C#** e **Web** e escolha o modelo **Aplicativo Web ASP .NET**.

3. Na caixa de texto **Nome**, insira **NorthwindWeb** e escolha o botão **OK**.

4. Na caixa de diálogo **Novo Projeto ASP.NET**, na lista **Selecionar um modelo**, escolha **Vazio** e o botão **OK**.

Na próxima etapa, você cria um [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] que representa a `Customers` tabela no banco de dados Northwind.

### <a name="to-create-the-entity-data-model"></a>Para criar o Modelo de Dados de Entidade

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

2. Na caixa de diálogo **Adicionar Novo Item**, escolha o nó **Dados** e, em seguida, o item **Modelo de Dados de Entidade ADO.NET**.

3. Na caixa de texto **nome** , digite `NorthwindModel` e, em seguida, escolha o botão **Adicionar** .

     O Assistente do Modelo de Dados de Entidade é aberto.

4. No assistente de Modelo de Dados de Entidade, na página **escolher conteúdo do modelo** , escolha o **designer do EF do item do banco de dados** e, em seguida, escolha o botão **Avançar** .

5. Na página **Escolha a Conexão de Dados**, executa uma das seguintes etapas:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-a.

         – ou –

    - Escolha o botão **Nova Conexão** para configurar uma nova conexão de dados. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

6. Se o banco de dados exigir uma senha, escolha o botão de opção **Sim, incluir os dados confidenciais da cadeia de conexão** e escolha o botão **Avançar**.

    > [!NOTE]
    > Se uma caixa de diálogo for exibida, escolha **Sim** para salvar o arquivo no seu projeto.

7. Na página **Escolha sua versão**, escolha o botão de opção **Entity Framework 5.0** e o botão **Avançar**.

    > [!NOTE]
    > Para usar a versão mais recente do Entity Framework 6 com Serviço WCF, você precisará instalar o pacote NuGet do provedor do Entity Framework do WCF Data Services. Consulte [usando WCF Data Services 5.6.0 com Entity Framework 6 +](https://devblogs.microsoft.com/odata/using-wcf-data-services-5-6-0-with-entity-framework-6/).

8. Na página **Escolher Objetos do Banco de Dados**, expanda o nó **Tabelas**, marque a caixa de seleção **Clientes** e escolha o botão **Concluir**.

     O diagrama de modelo de entidade é exibido e um arquivo *NorthwindModel. edmx* é adicionado ao seu projeto.

Na próxima etapa, você criará e testará o serviço de dados.

### <a name="to-create-the-data-service"></a>Para criar o serviço de dados

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

2. Na caixa de diálogo **Adicionar Novo Item**, escolha o nó **Web** e, em seguida, o item **WCF Data Services 5.6**.

3. Na caixa de texto **nome** , digite `NorthwindCustomers` e, em seguida, escolha o botão **Adicionar** .

     O arquivo **NorthwindCustomers.svc** aparece no **Editor de Códigos**.

4. No **Editor de Códigos**, localize o primeiro comentário `TODO:` e substitua o código pelo seguinte:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb" id="Snippet1":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs" id="Snippet1":::

5. Substitua os comentários no manipulador de eventos `InitializeService` pelo seguinte código:

     :::code language="vb" source="../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb" id="Snippet2":::
     :::code language="csharp" source="../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs" id="Snippet2":::


6. Na barra de menus, escolha **depurar**  >  **Iniciar sem depuração** para executar o serviço. Uma janela do navegador é aberta e o esquema XML para o serviço é exibido.

7. Na barra de **endereços** , digite `Customers` no final da URL para **NorthwindCustomers. svc** e escolha a tecla **Enter** .

     Uma representação XML dos dados na `Customers` tabela é exibida.

    > [!NOTE]
    > Em alguns casos, o Internet Explorer interpretará incorretamente os dados como um RSS feed. Você deve verificar se a opção para exibir RSS feeds está desabilitada. Para obter mais informações, consulte [Solucionando problemas de referências de serviço](../data-tools/troubleshooting-service-references.md).

8. Feche a janela do navegador.

Nas próximas etapas, você criará um aplicativo cliente Windows Forms para consumir o serviço.

## <a name="creating-the-client-application"></a>Criando o aplicativo cliente
Para criar o aplicativo cliente, você adiciona um segundo projeto, adiciona uma referência de serviço ao projeto, configura uma fonte de dados e cria uma interface do usuário para exibir os dados do serviço.

Na primeira etapa, você adiciona um projeto Windows Forms à solução e o define como o projeto de inicialização.

### <a name="to-create-the-client-application"></a>Para criar o aplicativo cliente

1. Na barra de menus, escolha Arquivo, **Adicionar**  >  **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó **Visual Basic** ou **Visual C#** , escolha o nó **Windows** e, em seguida, escolha **Windows Forms aplicativo**.

3. Na caixa de texto **Nome**, insira `NorthwindClient` e, em seguida, escolha o botão **OK**.

4. No **Gerenciador de Soluções**, escolha o nó de projeto **NorthwindClient**.

5. Na barra de menus, escolha **Projeto**, **Definir como Projeto de Inicialização**.

Na próxima etapa, você adiciona uma referência de serviço ao [!INCLUDE[ss_data_service](../data-tools/includes/ss_data_service_md.md)] no projeto Web.

### <a name="to-add-a-service-reference"></a>Para adicionar uma referência de serviço

1. Na barra de menus, escolha **projeto**  >  **Adicionar referência de serviço**.

2. Na caixa de diálogo **Adicionar Referência de Serviço**, escolha o botão **Descobrir**.

     A URL do serviço NorthwindCustomers é exibida no campo **Endereço**.

3. Escolha o botão **OK** para adicionar a referência de serviço.

Na próxima etapa, você configura uma fonte de dados para habilitar a vinculação de dados ao serviço.

### <a name="to-enable-data-binding-to-the-service"></a>Para habilitar a associação de dados ao serviço

1. Na barra de menus, escolha **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

   A janela **Fontes de Dados** é aberta.

2. Na janela **Fontes de Dados**, escolha o botão **Adicionar Nova Fonte de Dados**.

3. Na página **Escolher um Tipo de Fonte de Dados** do **Assistente de Configuração de Fonte de Dados**, escolha **Objeto** e, em seguida, o botão **Próximo**.

4. Na página **Selecionar os Objetos de Dados**, expanda os nós **NorthwindClient** e **NorthwindClient.ServiceReference1**.

5. Marque a caixa de seleção **Customer** e escolha o botão **Finalizar**.

Na próxima etapa, você cria a interface do usuário que exibe os dados do serviço.

### <a name="to-create-the-user-interface"></a>Para criar a interface do usuário

1. Na janela **Fontes de Dados**, abra o menu de atalho do nó **Clientes** e escolha **Copiar**.

2. No designer de formulários **Form1.vb** ou **Form1.cs**, abra o menu de atalho e escolha **Colar**.

    Um controle <xref:System.Windows.Forms.DataGridView>, um componente <xref:System.Windows.Forms.BindingSource> e um componente <xref:System.Windows.Forms.BindingNavigator> são adicionados ao formulário.

3. Escolha o controle **customersDataGridView** e, na janela **Propriedades** , defina a propriedade **Dock** como **Fill**.

4. No **Gerenciador de soluções**, abra o menu de atalho para o nó **Form1** e escolha **Exibir código** para abrir o editor de código e adicione a `Imports` seguinte `Using` instrução ou na parte superior do arquivo:

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

6. No **Gerenciador de Soluções**, abra o menu de atalho do arquivo **NorthwindCustomers.svc** e escolha **Exibir no Navegador**. O Internet Explorer é aberto e o esquema XML para o serviço é exibido.

7. Copie a URL da barra de endereços do Internet Explorer.

8. No código que você adicionou na etapa 4, selecione `http://localhost:53161/NorthwindCustomers.svc/` e o substitua pela URL que acabou de copiar.

9. Na barra de menus, escolha **depurar**  >  **Iniciar Depuração** para executar o aplicativo. As informações do cliente são mostradas.

   Agora você tem um aplicativo funcional que exibe uma lista de clientes do serviço NorthwindCustomers. Se desejar expor dados adicionais por meio do serviço, você pode modificar o [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] para incluir tabelas adicionais do banco de dados da Northwind.

Na próxima etapa opcional, você aprenderá a filtrar os dados retornados pelo serviço.

## <a name="adding-filtering-capabilities"></a>Adicionando recursos de filtragem
Nesta etapa, você personaliza o aplicativo para filtrar os dados pela cidade do cliente.

### <a name="to-add-filtering-by-city"></a>Para adicionar a filtragem por cidade

1. No **Gerenciador de Soluções**, abra o menu de atalho do nó **Form1.vb** ou **Form1.cs** e escolha **Abrir**.

2. Adicione um controle <xref:System.Windows.Forms.TextBox> e um controle <xref:System.Windows.Forms.Button> da **Caixa de Ferramentas** ao formulário.

3. Abra o menu de atalho para o <xref:System.Windows.Forms.Button> controle, escolha **Exibir código** e, em seguida, adicione o seguinte código ao `Button1_Click` manipulador de eventos:

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

5. Na barra de menus, escolha **depurar**  >  **Iniciar Depuração** para executar o aplicativo.

6. Na caixa de texto, insira **Londres** e escolha o botão. Somente os clientes de London são exibidos.

## <a name="see-also"></a>Confira também

- [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)
- [Como: Adicionar, atualizar ou remover uma referência do WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)
