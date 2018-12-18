---
title: 'Instruções passo a passo: criando um aplicativo de dados de N camadas'
ms.date: 09/08/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, creating
- n-tier applications, walkthroughs
ms.assetid: d15e4d31-2839-48d9-9e0e-2e73404d82a2
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 71c1c8dbaf34613d07ce29fa3f5e08d8e9c6961f
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305687"
---
# <a name="walkthrough-create-an-n-tier-data-application"></a>Passo a passo: Criar um aplicativo de dados de n camadas
Os aplicativos de dados de *N camadas* são aplicativos que acessam dados e são separados em várias *camadas* lógicas. A separação de componentes de aplicativos em camadas discretas aumenta a capacidade de manutenção e a escalabilidade do aplicativo. Isso é feito pela adoção com mais facilidade de novas tecnologias que podem ser aplicadas a uma única camada, sem precisar reprojetar toda a solução. A arquitetura de N camadas inclui uma camada de apresentação, uma camada intermediária e uma camada de dados. A camada intermediária geralmente inclui uma camada de acesso a dados, uma camada lógica de negócios e componentes compartilhados, tais como autenticação e validação. A camada de dados inclui um banco de dados relacional. Os aplicativos de N camadas geralmente armazenam informações confidenciais na camada de acesso a dados da camada intermediária para manter o isolamento de usuários finais que acessam a camada de apresentação. Para obter mais informações, consulte [visão geral dos aplicativos de dados de N camadas](../data-tools/n-tier-data-applications-overview.md).

Uma maneira de separar as várias camadas em um aplicativo de N camadas é criar projetos discretos para cada camada que você deseja incluir em seu aplicativo. Os conjuntos de dados digitados contêm uma propriedade `DataSet Project` que determina quais projetos o conjunto de dados gerado e o código `TableAdapter` devem acessar.

Esse passo a passo demonstra como separar o conjunto de dados e o código `TableAdapter` em projetos de biblioteca de classes discretas usando o **Designer de Conjunto de Dados**. Após você separar o conjunto de dados e o código TableAdapter, você cria um [serviços do Windows Communication Foundation e WCF Data Services no Visual Studio](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md) serviço para chamar a camada de acesso a dados. Por fim, você pode criar um aplicativo do Windows Forms como a camada de apresentação. Essa camada acessa dados do serviço de dados.

Durante este passo a passo, você deve executar as seguintes etapas:

-   Crie uma nova solução de n camadas que contém vários projetos.

-   Adicionar dois projetos de bibliotecas de classes na solução de N camadas.

-   Criar um conjunto de dados tipado usando o **Assistente de Configuração de Fonte de Dados**.

-   Separar gerado [TableAdapters](create-and-configure-tableadapters.md) e o código do conjunto de dados em projetos discretos.

-   Criar um serviço do Windows Communication Foundation (WCF) a ser chamado na camada de acesso a dados.

-   Criar funções no serviço para recuperar dados da camada de acesso a dados.

-   Criar um aplicativo do Windows Forms para servir como a camada de apresentação.

-   Criar controles do Windows Forms associados à fonte de dados.

-   Gravar código para preencher as tabelas de dados.

![link para vídeo](../data-tools/media/playvideo.gif) para uma versão em vídeo deste tópico, consulte [vídeo de instruções: criar um aplicativo de dados de n camadas](http://go.microsoft.com/fwlink/?LinkId=115188).

## <a name="prerequisites"></a>Pré-requisitos
Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **desenvolvimento de área de trabalho do .NET** carga de trabalho, ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (**Pesquisador de objetos do SQL Server** é instalado como parte do **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-the-n-tier-solution-and-class-library-to-hold-the-dataset-dataentitytier"></a>Criar a biblioteca de classe e de solução de n camadas para manter o conjunto de dados (DataEntityTier)
 A primeira etapa deste passo a passo é criar uma solução e dois projetos de biblioteca de classes. A biblioteca de primeira classe contém o conjunto de dados (o gerado digitada `DataSet` DataTables que mantêm os dados do aplicativo e classe). Este projeto é usado como a camada de entidade de dados do aplicativo e geralmente está localizada na camada intermediária. O conjunto de dados cria o conjunto de dados inicial e automaticamente separa o código em duas bibliotecas de classes.

> [!NOTE]
> Dê o nome correto ao projeto e à solução antes de clicar em **OK**. Isso facilitará a conclusão deste passo a passo.

### <a name="to-create-the-n-tier-solution-and-dataentitytier-class-library"></a>Para criar a solução de N camadas e a biblioteca de classes DataEntityTier

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **biblioteca de classes** tipo de projeto.

4. Nomeie o projeto como **DataEntityTier**.

5. Nomeie a solução **NTierWalkthrough**e, em seguida, escolha **Okey**.

     Uma solução NTierWalkthrough que contém o projeto DataEntityTier é criada e adicionada ao **Gerenciador de Soluções**.

## <a name="create-the-class-library-to-hold-the-tableadapters-dataaccesstier"></a>Criar a biblioteca de classes para manter os TableAdapters (DataAccessTier)
 A próxima etapa após a criação do projeto DataEntityTier é criar outro projeto de biblioteca de classes. Este projeto contém os TableAdapters gerados e é chamado de *camada de acesso de dados* do aplicativo. A camada de acesso a dados contém as informações necessárias para se conectar ao banco de dados e geralmente está localizada na camada intermediária.

### <a name="to-create-a-separate-class-library-for-the-tableadapters"></a>Para criar uma biblioteca de classes separado para os TableAdapters

1. Clique com botão direito na solução no **Gerenciador de soluções** e escolha **Add** > **novo projeto**.

2. No **novo projeto** caixa de diálogo, no painel central, selecione **biblioteca de classes**.

3. Nomeie o projeto **DataAccessTier** e escolha **Okey**.

     O projeto DataAccessTier é criado e adicionado à solução NTierWalkthrough.

## <a name="create-the-dataset"></a>Criar o conjunto de dados
 A próxima etapa é criar um conjunto de dados tipado. Conjuntos de dados tipados são criados com a classe de conjunto de dados (incluindo `DataTables` classes) e o `TableAdapter` classes em um único projeto. (Todas as classes são geradas em um único arquivo.) Quando você separar o conjunto de dados e TableAdapters em diferentes projetos, é a classe de conjunto de dados é movida para outro projeto, deixando o `TableAdapter` classes no projeto original. Portanto, crie o conjunto de dados no projeto que conterá, por fim, os TableAdapters (no projeto DataAccessTier). Criar o conjunto de dados usando o **Data Source Configuration Wizard**.

> [!NOTE]
> É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar bancos de dados de exemplo](../data-tools/installing-database-systems-tools-and-samples.md).

### <a name="to-create-the-dataset"></a>Para criar o conjunto de dados

1. Selecione o **DataAccessTier** na **Gerenciador de soluções**.

2. Sobre o **dados** menu, selecione **Show Data Sources**.

   A janela **Fontes de Dados** é aberta.

3. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o **Assistente de Configuração de Fonte de Dados**.

4. Sobre o **escolher um tipo de fonte de dados** página, selecione **banco de dados** e, em seguida, selecione **próxima**.

5. Na página **Escolha a Conexão de Dados**, execute uma das seguintes ações:

     Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

     -ou-

     Selecione **nova Conexão** para abrir o **Adicionar Conexão** caixa de diálogo.

6. Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, escolha **próxima**.

    > [!NOTE]
    > Se você escolheu um arquivo do banco de dados local (em vez de se conectar ao SQL Server), talvez seja perguntado se deseja adicionar o arquivo ao projeto. Escolher **Sim** para adicionar o arquivo de banco de dados ao projeto.

7. Selecione **próxima** sobre o **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** página.

8. Expanda o nó **Tabelas** na página **Escolher Objetos do Banco de Dados**.

9. Marque as caixas de seleção para o **clientes** e **pedidos** tabelas e, em seguida, escolha **concluir**.

     NorthwindDataSet é adicionado ao projeto DataAccessTier e aparece na janela **Fontes de Dados**.

## <a name="separate-the-tableadapters-from-the-dataset"></a>Separar os TableAdapters do conjunto de dados
 Depois de criar o conjunto de dados, separe a classe do conjunto de dados gerada a partir dos TableAdapters. Você faz isso ao configurar a propriedade **Projeto do Conjunto de Dados** para o nome do projeto que armazenará a classe do conjunto de dados separada.

### <a name="to-separate-the-tableadapters-from-the-dataset"></a>Para separar os TableAdapters do Conjunto de Dados

1. Clique duas vezes em **NorthwindDataSet.xsd** no **Gerenciador de Soluções** para abrir o conjunto de dados no **Designer de Conjunto de Dados**.

2. Selecione uma área vazia no designer.

3. Localize o nó **Projeto do Conjunto de Dados** na janela **Propriedades**.

4. No **projeto DataSet** lista, selecione **DataEntityTier**.

5. No menu **Build**, selecione **Compilar Solução**.

   O conjunto de dados e os TableAdapters são separados em dois projetos de biblioteca de classes. O projeto que continha originalmente todo o conjunto de dados (`DataAccessTier`) agora contém somente os TableAdapters. O projeto atribuído a **projeto DataSet** propriedade (`DataEntityTier`) contém o conjunto de dados tipado: *NorthwindDataSet* (ou  *NorthwindDataSet.Dataset.Designer.cs*).

> [!NOTE]
> Quando você separa os conjuntos de dados e os TableAdapters (configurando a propriedade **Projeto de Conjunto de Dados**), as classes dos conjuntos de dados parciais existentes no projeto não são movidas automaticamente. As classes parciais do conjunto de dados existentes devem ser movidas manualmente para o projeto do conjunto de dados.

## <a name="create-a-new-service-application"></a>Criar um novo aplicativo de serviço
Este passo a passo demonstra como acessar a camada de acesso de dados por meio de um serviço WCF, então, vamos criar um novo aplicativo de serviço do WCF.

### <a name="to-create-a-new-wcf-service-application"></a>Para criar um novo aplicativo de Serviço WCF

1. Clique com botão direito na solução no **Gerenciador de soluções** e escolha **Add** > **novo projeto**.

2. No **novo projeto** caixa de diálogo, no painel esquerdo, selecione **WCF**. No painel central, selecione **WCF Service Library**.

3. Nomeie o projeto **DataService** e selecione **Okey**.

     O projeto DataService é criado e adicionado à solução NTierWalkthrough.

## <a name="create-methods-in-the-data-access-tier-to-return-the-customers-and-orders-data"></a>Crie métodos na camada de acesso a dados para retornar os dados de clientes e pedidos
 O serviço de dados tem que chamar dois métodos na camada de acesso a dados: `GetCustomers` e `GetOrders`. Esses métodos retornam o Northwind `Customers` e `Orders` tabelas. Criar o `GetCustomers` e `GetOrders` métodos no `DataAccessTier` projeto.

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-customers-table"></a>Para criar um método na camada de acesso a dados que retorna a tabela Clientes

1. Na **Gerenciador de soluções**, clique duas vezes em **NorthwindDataSet** para abrir o conjunto de dados.

2. Clique com botão direito **CustomersTableAdapter** e clique em **Add Query**.

3. Na página **Escolher um Tipo de Comando**, mantenha o valor padrão de **Usar instruções SQL** e clique em **Próximo**.

4. Na página **Escolher um Tipo de Consulta**, mantenha o valor padrão de **SELECT que retorna linhas** e clique em **Próximo**.

5. Na página **Especificar uma instrução SQL SELECT**, mantenha a consulta padrão e clique em **Próximo**.

6. Na página **Escolher Métodos a Serem Gerados**, digite **GetCustomers** para o **Nome do método** na seção **Retornar uma DataTable**.

7. Clique em **Finalizar**.

### <a name="to-create-a-method-in-the-data-access-tier-that-returns-the-orders-table"></a>Para criar um método na camada de acesso a dados que retorna a tabela Pedidos

1. Clique com o botão direito do mouse em **OrdersTableAdapter** e clique em **Adicionar Consulta**.

2. Na página **Escolher um Tipo de Comando**, mantenha o valor padrão de **Usar instruções SQL** e clique em **Próximo**.

3. Na página **Escolher um Tipo de Consulta**, mantenha o valor padrão de **SELECT que retorna linhas** e clique em **Próximo**.

4. Na página **Especificar uma instrução SQL SELECT**, mantenha a consulta padrão e clique em **Próximo**.

5. Na página **Escolher Métodos a Serem Gerados**, digite **GetOrders** para o **Nome do método** na seção **Retornar uma DataTable**.

6. Clique em **Finalizar**.

7. No menu **Compilar**, clique em **Compilar Solução**.

## <a name="add-a-reference-to-the-data-entity-and-data-access-tiers-to-the-data-service"></a>Adicione uma referência à entidade de dados e camadas de acesso a dados para o serviço de dados
 Como o serviço de dados requer informações do conjunto de dados e dos TableAdapters, adicione referências aos projetos **DataEntityTier** e **DataAccessTier**.

### <a name="to-add-references-to-the-data-service"></a>Para adicionar referência aos serviço de dados

1. Clique com o botão direito do mouse em **DataService** no **Gerenciador de Soluções** e clique em **Adicionar Referência**.

2. Clique na guia **Projetos** na caixa de diálogo **Adicionar Referência**.

3. Escolha os projetos **DataAccessTier** e **DataEntityTier**.

4. Clique em **OK**.

## <a name="add-functions-to-the-service-to-call-the-getcustomers-and-getorders-methods-in-the-data-access-tier"></a>Adicionar funções ao serviço para chamar os métodos GetCustomers e GetOrders na camada de acesso a dados
 Agora que a camada de acesso a dados contém os métodos para retornar dados, crie métodos no serviço de dados para chamar os métodos na camada de acesso a dados.

> [!NOTE]
> Para projetos C#, adicione uma referência ao assembly `System.Data.DataSetExtensions` para que o código a seguir seja compilado.

### <a name="to-create-the-getcustomers-and-getorders-functions-in-the-data-service"></a>Para criar as funções GetCustomers e GetOrders no serviço de dados

1. No projeto **DataService**, clique duas vezes em **IService1.vb** ou **IService1.cs**.

2. Adicione o seguinte código no comentário **Adicionar suas operações de serviço aqui**:

    ```vb
    <OperationContract()> _
    Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable

    <OperationContract()> _
    Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable
    ```

    ```csharp
    [OperationContract]
    DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers();

    [OperationContract]
    DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders();
    ```

3. No projeto DataService, clique duas vezes em **Service1.vb** (ou **Service1.cs**).

4. Adicione o seguinte código à classe **Service1**:

    ```vb
    Public Function GetCustomers() As DataEntityTier.NorthwindDataSet.CustomersDataTable Implements IService1.GetCustomers
        Dim CustomersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
        Return CustomersTableAdapter1.GetCustomers()
    End Function

    Public Function GetOrders() As DataEntityTier.NorthwindDataSet.OrdersDataTable Implements IService1.GetOrders
        Dim OrdersTableAdapter1 As New DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
        Return OrdersTableAdapter1.GetOrders()
    End Function
    ```

    ```csharp
    public DataEntityTier.NorthwindDataSet.CustomersDataTable GetCustomers()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter
             CustomersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.CustomersTableAdapter();
        return CustomersTableAdapter1.GetCustomers();
    }
    public DataEntityTier.NorthwindDataSet.OrdersDataTable GetOrders()
    {
        DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter
             OrdersTableAdapter1
            = new DataAccessTier.NorthwindDataSetTableAdapters.OrdersTableAdapter();
        return OrdersTableAdapter1.GetOrders();
    }
    ```

5. No menu **Compilar**, clique em **Compilar Solução**.

## <a name="create-a-presentation-tier-to-display-data-from-the-data-service"></a>Criar uma camada de apresentação para exibir dados do serviço de dados
 Agora que a solução contém o serviço de dados que tem métodos que chamam os dados de camada de acesso, crie outro projeto que chama o serviço de dados e apresentá-los para os usuários. Neste passo a passo, crie um aplicativo do Windows Forms, o qual será a camada de apresentação do aplicativo de N camadas.

### <a name="to-create-the-presentation-tier-project"></a>Para criar o projeto da camada de apresentação

1. Clique com botão direito na solução no **Gerenciador de soluções** e escolha **Add** > **novo projeto**.

2. No **novo projeto** caixa de diálogo, no painel esquerdo, selecione **área de trabalho do Windows**. No painel central, selecione **aplicativo de formulários do Windows**.

3. Nomeie o projeto como **PresentationTier** e clique em **OK**.

    O projeto PresentationTier é criado e adicionado à solução NTierWalkthrough.

## <a name="set-the-presentationtier-project-as-the-startup-project"></a>Defina o projeto PresentationTier como o projeto de inicialização
Vamos definir a **PresentationTier** projeto como o projeto de inicialização para a solução, porque ele é o aplicativo cliente real que apresenta e interage com os dados.

### <a name="to-set-the-new-presentation-tier-project-as-the-startup-project"></a>Para configurar o novo projeto de camada de apresentação como o projeto de inicialização

-   Em **Gerenciador de Soluções**, clique com o botão direito do mouse em **PresentationTier** e clique em **Definir como Projeto de Inicialização**.

## <a name="add-references-to-the-presentation-tier"></a>Adicione referências à camada de apresentação
 O aplicativo cliente PresentationTier requer uma referência de serviço para o serviço de dados para acessar os métodos no serviço. Além disso, uma referência ao conjunto de dados é necessária para permitir o compartilhamento de tipos pelo serviço WCF. Até que você habilite o compartilhamento por meio do serviço de dados de tipo, o código adicionado à classe parcial do conjunto de dados não está disponível para a camada de apresentação. Como você geralmente adiciona código, como o código de validação para a linha e coluna alterando eventos de uma tabela de dados, é provável que você desejará acessar esse código do cliente.

### <a name="to-add-a-reference-to-the-presentation-tier"></a>Para adicionar uma referência à camada de apresentação

1. Na **Gerenciador de soluções**, clique com botão direito **PresentationTier** e selecione **Add Reference**.

2. No **adicionar referência** caixa de diálogo, selecione o **projetos** guia.

3. Selecione **DataEntityTier** e escolha **Okey**.

### <a name="to-add-a-service-reference-to-the-presentation-tier"></a>Para adicionar uma referência de serviço à camada de apresentação

1. Na **Gerenciador de soluções**, clique com botão direito **PresentationTier** e selecione **Add Service Reference**.

2. No **adicionar referência de serviço** caixa de diálogo, selecione **Discover**.

3. Selecione **Service1** e escolha **Okey**.

    > [!NOTE]
    > Se você tiver vários serviços no computador atual, selecione o serviço que você criou anteriormente neste passo a passo (o serviço que contém o `GetCustomers` e `GetOrders` métodos).

## <a name="add-datagridviews-to-the-form-to-display-the-data-returned-by-the-data-service"></a>Adicionar DataGridViews ao formulário para exibir os dados retornados pelo serviço de dados
 Depois de adicionar a referência de serviço ao serviço de dados, a janela **Fontes de Dados** é preenchida automaticamente com os dados retornados pelo serviço.

### <a name="to-add-two-data-bound-datagridviews-to-the-form"></a>Para adicionar duas associações de dados DataGridViews ao formulário

1. No **Gerenciador de Soluções**, escolha o projeto **PresentationTier**.

2. Na janela **Fontes de Dados**, expanda **NorthwindDataSet** e localize o nó **Clientes**.

3. Arraste o nó **Clientes** para Form1.

4. Na janela **Fontes de Dados**, expanda o nó **Clientes** e localize o nó **Pedidos** relacionado (o nó **Pedidos** aninhado no nó **Clientes**).

5. Arraste o nó **Pedidos** relacionado para Form1.

6. Crie um manipulador de eventos `Form1_Load` ao clicar duas vezes em uma área vazia do formulário.

7. Adicione o seguinte código ao manipulador de eventos do `Form1_Load`.

    ```vb
    Dim DataSvc As New ServiceReference1.Service1Client
    NorthwindDataSet.Customers.Merge(DataSvc.GetCustomers)
    NorthwindDataSet.Orders.Merge(DataSvc.GetOrders)
    ```

    ```csharp
    ServiceReference1.Service1Client DataSvc =
        new ServiceReference1.Service1Client();
    northwindDataSet.Customers.Merge(DataSvc.GetCustomers());
    northwindDataSet.Orders.Merge(DataSvc.GetOrders());
    ```

## <a name="increase-the-maximum-message-size-allowed-by-the-service"></a>Aumentar o tamanho máximo permitido pelo serviço
O valor padrão para `maxReceivedMessageSize` não é grande o suficiente para manter os dados recuperados do `Customers` e `Orders` tabelas. Nas etapas a seguir, você irá aumentar o valor para 6553600. Você altere o valor no cliente, que atualiza automaticamente a referência de serviço.

> [!NOTE]
> O menor tamanho padrão se destina a limitar a exposição para ataques de negação de serviço (DoS). Para obter mais informações, consulte <xref:System.ServiceModel.WSHttpBindingBase.MaxReceivedMessageSize%2A>.

### <a name="to-increase-the-maxreceivedmessagesize-value"></a>Para aumentar o valor maxReceivedMessageSize

1. No **Gerenciador de Soluções**, clique duas vezes no arquivo **app.config** no projeto **PresentationTier**.

2. Encontre o atributo de tamanho **maxReceivedMessage** e altere o valor para `6553600`.

## <a name="test-the-application"></a>Testar o aplicativo
Execute o aplicativo pressionando **F5**. Os dados a partir de `Customers` e `Orders` tabelas é recuperado do serviço de dados e exibido no formulário.

## <a name="next-steps"></a>Próximas etapas
 Dependendo dos requisitos do aplicativo, existem várias etapas que você talvez queira realizar após salvar os dados relacionados no aplicativo baseado em Windows. Por exemplo, você poderia fazer as seguintes melhorias a este aplicativo:

-   Adicionar validação ao conjunto de dados.

-   Adicionar métodos adicionais ao serviço para atualizar dados novamente no banco de dados.

## <a name="see-also"></a>Consulte também

- [Trabalhando com conjuntos de dados em aplicativos de N camadas](../data-tools/work-with-datasets-in-n-tier-applications.md)
- [Atualização hierárquica](../data-tools/hierarchical-update.md)
- [Acessando dados no Visual Studio](../data-tools/accessing-data-in-visual-studio.md)