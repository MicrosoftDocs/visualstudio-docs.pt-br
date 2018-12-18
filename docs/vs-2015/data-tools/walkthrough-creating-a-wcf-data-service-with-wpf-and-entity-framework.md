---
title: 'Passo a passo: Criando um serviço de dados do WCF com WPF e Entity Framework | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data services in Visual Studio
- WCF Data Services, Visual Studio
- ADO.NET Data Services, Visual Studio
- WCF data services in Visual Studio
ms.assetid: da66ad1b-a25d-485c-af13-2d18f0422e3d
caps.latest.revision: 28
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3d115c7ea7b2739f49492fb28fe855e2638d972c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889588"
---
# <a name="walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework"></a>Passo a passo: Criando um serviço de dados do WCF com WPF e Entity Framework
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este passo a passo demonstra como criar um simples [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] que é hospedado em um [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo Web e, em seguida, acessá-lo de um aplicativo Windows Forms.  
  
 Neste passo a passo, você realizará as seguintes tarefas:  
  
-   Criará um aplicativo Web para hospedar um [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)].  
  
-   Criará um [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] que representa a tabela Customers no banco de dados da Northwind.  
  
-   Criará um [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)].  
  
-   Criará um aplicativo cliente e adicionará uma referência ao [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)].  
  
-   Habilitará a associação de dados ao serviço e gerará a interface de usuário.  
  
-   Se desejar, adicionará recursos de filtragem ao aplicativo.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   O banco de dados de exemplo Northwind.  
  
     Se você não tiver esse banco de dados no computador de desenvolvimento, você pode baixá-lo partir o [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088). Para obter instruções, consulte [Downloading Sample Databases](http://msdn.microsoft.com/library/ef9d69a1-9461-43fe-94bb-7c836754bcb5).  
  
## <a name="creating-the-service"></a>Criando o serviço  
 Para criar um [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)], você adicionará um projeto Web, criará um [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] e, em seguida, criará o serviço usando o modelo.  
  
 Na primeira etapa, você adicionará um projeto Web para hospedar o serviço.  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-the-web-project"></a>Para criar o projeto Web  
  
1. Na barra de menus, escolha **arquivo**, **New**, **projeto**.  
  
2. No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** e **Web** nós e, em seguida, escolha o **ASP. Aplicativo de Web do NET** modelo.  
  
3. No **nome** texto, digite **NorthwindWeb**e, em seguida, escolha o **Okey** botão.  
  
4. No **novo projeto ASP.NET** na caixa de **selecionar um modelo** , escolha **vazio**e, em seguida, escolha o **Okey** botão.  
  
   Nesta etapa, você criará um [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] que representa a tabela Customers no banco de dados da Northwind.  
  
#### <a name="to-create-the-entity-data-model"></a>Para criar o Modelo de Dados de Entidade  
  
1. Na barra de menus, escolha **Project**, **Adicionar Novo Item**.  
  
2. No **Adicionar Novo Item** diálogo caixa, escolha o **dados** nó e, em seguida, escolha o **modelo de dados de entidade ADO.NET** item.  
  
3. No **nome** texto, digite `NorthwindModel`e, em seguida, escolha o **Add** botão.  
  
    O Assistente do Modelo de Dados de Entidade é aberto.  
  
4. No Assistente de modelo de dados de entidade, na **escolher conteúdo do modelo** , escolha o **EF Designer do banco de dados** item e, em seguida, escolha o **próxima** botão.  
  
5. Sobre o **escolha sua Conexão de dados** , execute uma das seguintes etapas:  
  
   -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-a.  
  
        -ou-  
  
   -   Escolha o **nova Conexão** botão para configurar uma nova conexão de dados. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).  
  
6. Se o banco de dados exigir uma senha, escolha o **Sim, incluir dados confidenciais na cadeia de conexão** botão de opção e, em seguida, escolha o **próxima** botão.  
  
   > [!NOTE]
   >  Se uma caixa de diálogo for exibida, escolha **Sim** para salvar o arquivo ao seu projeto.  
  
7. No **escolha sua versão** , escolha o **Entity Framework 5.0** botão de opção e, em seguida, escolha o **próxima** botão.  
  
   > [!NOTE]
   >  Para usar a versão mais recente do Entity Framework 6 com Serviço WCF, você precisará instalar o pacote NuGet do provedor do Entity Framework do WCF Data Services. Ver [usar o WCF Data Services 5.6.0 com o Entity Framework 6 +](http://blogs.msdn.com/b/odatateam/archive/2013/10/02/using-wcf-data-services-5-6-0-with-entity-framework-6.aspx).  
  
8. No **Choose Your Database Objects** página, expanda o **tabelas** nó, selecione o **clientes** caixa de seleção e, em seguida, escolha o **concluir** botão.  
  
    O diagrama do modelo da entidade será exibido e um arquivo NorthwindModel.edmx será adicionado ao projeto.  
  
   Nesta etapa, você vai criar e testar o serviço de dados.  
  
#### <a name="to-create-the-data-service"></a>Para criar o serviço de dados  
  
1. Na barra de menus, escolha **Project**, **Adicionar Novo Item**.  
  
2. No **Adicionar Novo Item** diálogo caixa, escolha o **Web** nó e, em seguida, escolha o **WCF Data Services 5.6** item.  
  
3. No **nome** texto, digite `NorthwindCustomers`e, em seguida, escolha o **Add** botão.  
  
    O arquivo Northwindcustomers SVC aparece na **Editor de códigos**.  
  
4. No **Editor de códigos**, localize o primeiro `TODO:` comentar e substitua o código a seguir:  
  
    [!code-csharp[WCFDataServiceWalkthrough#1](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#1)]
    [!code-vb[WCFDataServiceWalkthrough#1](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#1)]  
  
5. Substitua os comentários no manipulador de eventos `InitializeService` pelo seguinte código:  
  
    [!code-csharp[WCFDataServiceWalkthrough#2](../snippets/csharp/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/cs/northwindcustomers.svc.cs#2)]
    [!code-vb[WCFDataServiceWalkthrough#2](../snippets/visualbasic/VS_Snippets_VBCSharp/wcfdataservicewalkthrough/vb/northwindcustomers.svc.vb#2)]  
  
6. Na barra de menus, escolha **Debug**, **Start Without Debugging** para executar o serviço. Uma janela do navegador é aberta e o esquema XML do serviço é exibido.  
  
7. No **endereço** barra, insira `Customers` no final da URL para Northwindcustomers e, em seguida, escolha o **ENTER** chave.  
  
    É exibida uma representação XML dos dados na tabela Customers.  
  
   > [!NOTE]
   >  Em alguns casos, o Internet Explorer interpretará incorretamente os dados como um RSS feed. Você deve verificar se a opção para exibir RSS feeds está desabilitada. Para obter mais informações, consulte [solução de problemas de referências de serviço](../data-tools/troubleshooting-service-references.md).  
  
8. Feche a janela do navegador.  
  
   Nas próximas etapas, você criará um aplicativo cliente do Windows Forms para consumir o serviço.  
  
## <a name="creating-the-client-application"></a>Criando o aplicativo cliente  
 Para criar o aplicativo cliente, você vai adicionar um segundo projeto, adicionar uma referência de serviço ao projeto, configurar uma fonte de dados e criar uma interface do usuário para exibir os dados do serviço.  
  
 Na primeira etapa, você vai adicionar um projeto do Windows Forms à solução e defini-lo como o projeto de inicialização.  
  
#### <a name="to-create-the-client-application"></a>Para criar o aplicativo cliente  
  
1. Na barra de menus, escolha arquivo, **Add**, **novo projeto**.  
  
2. No **novo projeto** diálogo caixa, expanda o **Visual Basic** ou **Visual c#** nó e escolha o **Windows** nó e, em seguida, escolha  **Aplicativo de formulários do Windows**.  
  
3. Na caixa de texto **Nome**, insira `NorthwindClient` e, em seguida, escolha o botão **OK**.  
  
4. Na **Gerenciador de soluções**, escolha o **NorthwindClient** nó do projeto.  
  
5. Na barra de menus, escolha **Project**, **definir como projeto de inicialização**.  
  
   Nesta etapa, você adicionará uma referência de serviço ao [!INCLUDE[ss_data_service](../includes/ss-data-service-md.md)] no projeto Web.  
  
#### <a name="to-add-a-service-reference"></a>Para adicionar uma referência de serviço  
  
1. Na barra de menus, escolha **Project**, **Add Service Reference**.  
  
2. No **adicionar referência de serviço** diálogo caixa, escolha o **Discover** botão.  
  
    A URL do serviço NorthwindCustomers é exibida na **endereço** campo.  
  
3. Escolha o **Okey** botão para adicionar a referência de serviço.  
  
   Nesta etapa, você vai configurar um fonte de dados para habilitar a associação de dados ao serviço.  
  
#### <a name="to-enable-data-binding-to-the-service"></a>Para habilitar a associação de dados ao serviço  
  
1. Na barra de menus, escolha **modo de exibição**, **Other Windows**, **fontes de dados**.  
  
2. No **fontes de dados** janela, escolha o **Add New Data Source** botão.  
  
3. No **escolher um tipo de fonte de dados** página do **Data Source Configuration Wizard**, escolha **objeto**e, em seguida, escolha o **Avançar** botão .  
  
4. Sobre o **selecione os objetos de dados** página, expanda o **NorthwindClient** nó e, em seguida, expanda o **NorthwindClient.ServiceReference1** nó.  
  
5. Selecione **Customer** caixa de seleção e, em seguida, escolha o **concluir** botão.  
  
   Nesta etapa, você criará a interface do usuário que exibirá os dados do serviço.  
  
#### <a name="to-create-the-user-interface"></a>Para criar a interface do usuário  
  
1. No **fontes de dados** janela, abra o menu de atalho para o **clientes** nó e escolha **cópia**.  
  
2. No **Form1.vb** ou **Form1.cs** designer de formulário, abra o menu de atalho e escolha **colar**.  
  
    Um controle <xref:System.Windows.Forms.DataGridView>, um componente <xref:System.Windows.Forms.BindingSource> e um componente <xref:System.Windows.Forms.BindingNavigator> são adicionados ao formulário.  
  
3. Escolha o **CustomersDataGridView** controle e, em seguida, no **propriedades** conjunto de janela a **Dock** propriedade a ser **preencher**.  
  
4. Na **Gerenciador de soluções**, abra o menu de atalho para o **Form1** nó e escolha **Exibir código** para abrir o Editor de códigos e adicione as seguintes importações ou usando a instrução no parte superior do arquivo:  
  
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
  
6. Na **Gerenciador de soluções**, abra o menu de atalho para o arquivo Northwindcustomers SVC e escolha **exibir no navegador**. O Internet Explorer é aberto e o esquema XML do serviço é exibido.  
  
7. Copie a URL da barra de endereços do Internet Explorer.  
  
8. No código que você adicionou na etapa 4, selecione `http://localhost:53161/NorthwindCustomers.svc/` e o substitua pela URL que acabou de copiar.  
  
9. Na barra de menus, escolha **Debug**, **iniciar depuração** para executar o aplicativo. As informações do cliente são exibidas.  
  
   Agora você tem um aplicativo funcional que exibe uma lista de clientes do serviço NorthwindCustomers. Se desejar expor dados adicionais por meio do serviço, você pode modificar o [!INCLUDE[adonet_edm](../includes/adonet-edm-md.md)] para incluir tabelas adicionais do banco de dados da Northwind.  
  
   Na próxima etapa opcional, você aprenderá como filtrar os dados que são retornados pelo serviço.  
  
## <a name="adding-filtering-capabilities"></a>Adicionando recursos de filtragem  
 Nesta etapa, você personalizará o aplicativo para filtrar os dados por cidade do cliente.  
  
#### <a name="to-add-filtering-by-city"></a>Para adicionar a filtragem por cidade  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **Form1.vb** ou **Form1.cs** nó e escolha **abrir**.  
  
2.  Adicionar um <xref:System.Windows.Forms.TextBox> controle e um <xref:System.Windows.Forms.Button> controlar da **caixa de ferramentas** ao formulário.  
  
3.  Abra o menu de atalho para o <xref:System.Windows.Forms.Button> controlar e, em seguida, escolha **Exibir código**e, em seguida, adicione o seguinte código no `Button1_Click` manipulador de eventos:  
  
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
  
4.  No código anterior, substitua `http://localhost:53161/NorthwindCustomers.svc` pela URL do manipulador de eventos `Form1_Load`.  
  
5.  Na barra de menus, escolha **Debug**, **iniciar depuração** para executar o aplicativo.  
  
6.  Na caixa de texto, insira **Londres**e, em seguida, escolha o botão. Somente os clientes de London são exibidos.  
  
## <a name="see-also"></a>Consulte também  
 [Serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)   
 [Como adicionar, atualizar ou remover uma referência de WCF Data Service](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md)

