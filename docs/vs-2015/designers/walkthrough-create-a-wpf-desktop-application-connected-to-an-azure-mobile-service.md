---
title: 'Passo a passo: Criar um aplicativo de área de trabalho do WPF conectado a um serviço móvel do Azure | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8d42620f-553b-4b04-a38b-f6b306d73a50
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9ab2c5bbea358c226407ba83e2a367195ecfef06
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49270602"
---
# <a name="walkthrough-create-a-wpf-desktop-application-connected-to-an-azure-mobile-service"></a>Passo a passo: Criar um aplicativo de área de trabalho do WPF conectado a um serviço móvel do Azure
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o WPF (Windows Presentation Foundation) para criar rapidamente um aplicativo de área de trabalho moderno que usa um serviço móvel do Azure para armazenar e fornecer dados.  
  
##  <a name="Requirements"></a> Pré-requisitos  
 Você precisará dos seguintes itens para concluir este passo a passo:  
  
-   Visual Studio 2015 – qualquer versão que dê suporte ao desenvolvimento do WPF.  
  
-   Uma conta ativa do Microsoft Azure.  
  
    -   Você pode se inscrever para uma conta de avaliação gratuita [aqui](http://azure.microsoft.com/pricing/free-trial/).  
  
    -   Você pode ativar os [benefícios de assinante do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F). Sua assinatura do MSDN fornece a você créditos mensais que podem ser usados para serviços pagos do Azure.  
  
## <a name="create-a-project-and-add-references"></a>Criar um projeto e adicionar referências  
 A primeira etapa é criar um projeto WPF e adicionar um pacote NuGet que permita conexão com os serviços móveis do Azure.  
  
#### <a name="to-create-the-project"></a>Para criar o projeto  
  
1.  Na barra de menus, escolha **Arquivo**, **Novo**, **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, expanda o nó **Visual C#** ou **Visual Basic** e escolha o nó **Windows**, depois expanda o nó **Windows** e escolha o nó **Área de trabalho clássica**.  
  
3.  Na lista de modelos, escolha o modelo **Aplicativo WPF**.  
  
4.  Na caixa de texto **Nome** insira `WPFQuickStart` e, em seguida, escolha o botão **OK**.  
  
     O projeto é criado e os arquivos do projeto são adicionados ao **Gerenciador de Soluções** e o designer da janela do aplicativo padrão **MainWindow.xaml** é exibido.  
  
#### <a name="to-add-a-reference-to-the-windows-azure-mobile-services-sdk"></a>Para adicionar uma referência ao SDK de Serviços Móveis do Microsoft Azure  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho para o nó **Referências** e escolha **Gerenciar Pacotes do NuGet**.  
  
2.  Em **Gerenciar Pacotes do NuGet**, escolha o campo **Pesquisar** e insira `mobileservices`.  
  
3.  No painel esquerdo, escolha **WindowsAzure.MobileServices**e, em seguida, no painel direito, escolha o botão **Instalar**.  
  
    > [!NOTE]
    >  Se uma caixa de diálogo **Visualização** aparecer, examine as alterações propostas e, em seguida, escolha o botão **OK**.  
  
4.  Na caixa de diálogo **Aceitação da Licença**, examine os termos da licença e aceite-os, escolhendo o botão **Eu aceito**.  
  
     As referências necessárias serão adicionadas ao **Gerenciador de Soluções**.  
  
    > [!NOTE]
    >  Se você não concordar com os termos de licença, escolha o botão **Eu recuso**. Você não poderá concluir o restante do passo a passo.  
  
## <a name="create-the-user-interface"></a>Criar a interface do usuário  
 A próxima etapa é criar a interface do usuário para o aplicativo. Primeiro, você cria um controle de usuário reutilizável que exibe um layout padrão lado a lado com dois painéis. Em seguida, adiciona o controle do usuário à janela principal do aplicativo e acrescenta controles para inserir e exibir dados e escreve um código para definir a interação com o back-end do serviço móvel.  
  
#### <a name="to-add-a-user-control"></a>Para adicionar um controle de usuário  
  
1.  No **Gerenciador de Soluções**, abra o menu de atalho do nó **WPFQuickStart** e escolha **Adicionar**, **Nova Pasta**.  
  
2.  Nomeie a pasta `Common`.  
  
3.  Abra o menu de atalho para a pasta **Comum** e escolha **Adicionar**, **Controle de Usuário**.  
  
4.  Na caixa de diálogo **Adicionar Novo Item**, escolha o campo de nome, insira `QuickStartTask`, em seguida, escolha o botão **Adicionar**.  
  
     O controle de usuário será adicionado ao projeto e o arquivo **QuickStartTask.xaml** arquivo será aberto no designer.  
  
5.  No painel inferior do designer, selecione as marcas `<Grid>` e `</Grid>`, e substitua-as pelo seguinte código XAML:  
  
    ```xaml  
    <Grid VerticalAlignment="Top">  
            <StackPanel Orientation="Horizontal">  
                <Border BorderThickness="0,0,1,0" BorderBrush="DarkGray" Margin="0,10" MinWidth="70">  
                    <TextBlock Text="{Binding Number}" FontSize="45" Foreground="DarkGray" Margin="20,0"/>  
                </Border>  
                <StackPanel>  
                    <TextBlock Text="{Binding Title}" Margin="10,10,0,0" FontSize="16" FontWeight="Bold" />  
                    <TextBlock Text="{Binding Description}" Margin="10,0,0,0" TextWrapping="Wrap" MaxWidth="500" />  
                </StackPanel>  
            </StackPanel>  
        </Grid>  
    ```  
  
     Esse código XAML cria um layout reutilizável com espaços reservados para campos de número, título e campos de descrição. Em tempo de execução, os espaços reservados podem ser substituídos por texto, conforme mostrado na ilustração a seguir.  
  
     ![O controle de usuário QuickStartTask](../designers/media/wpfquickstart1.PNG "WPFQuickStart1")  
  
6.  No **Gerenciador de Soluções**, expanda o nó **QuickStartTask.xaml** e abra o arquivo **QuickStartTask.xaml.cs** ou **QuickStartTask.xaml.vb**.  
  
7.  No editor de códigos, substitua o namespace `namespace WPFQuickStart.Common` (C#) ou o método `Public Class QuickStartTask` (VB) pelo seguinte código:  
  
    ```csharp  
    namespace WPFQuickStart.Common  
    {  
        /// <summary>  
        /// Interaction logic for QuickStartTask.xaml  
        /// </summary>  
        public partial class QuickStartTask : UserControl  
        {  
            public QuickStartTask()  
            {  
                this.InitializeComponent();  
                this.DataContext = this;  
            }  
  
            public int Number  
            {  
                get { return (int)GetValue(NumberProperty); }  
                set { SetValue(NumberProperty, value); }  
            }  
  
            // Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...  
            public static readonly DependencyProperty NumberProperty =  
                DependencyProperty.Register("Number", typeof(int), typeof(QuickStartTask), new PropertyMetadata(0));  
  
            public string Title  
            {  
                get { return (string)GetValue(TitleProperty); }  
                set { SetValue(TitleProperty, value); }  
            }  
  
            // Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...  
            public static readonly DependencyProperty TitleProperty =  
                DependencyProperty.Register("Title", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));  
  
            public string Description  
            {  
                get { return (string)GetValue(DescriptionProperty); }  
                set { SetValue(DescriptionProperty, value); }  
            }  
  
            // Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...  
            public static readonly DependencyProperty DescriptionProperty =  
                DependencyProperty.Register("Description", typeof(string), typeof(QuickStartTask), new PropertyMetadata(default(string)));  
        }  
    }  
    ```  
  
    ```vb  
    Partial Public Class QuickStartTask  
            Inherits UserControl  
  
            Public Sub New()  
                Me.InitializeComponent()  
                Me.DataContext = Me  
            End Sub  
  
            Public Property Number() As Integer  
                Get  
                    Return CInt(Fix(GetValue(NumberProperty)))  
                End Get  
                Set(ByVal value As Integer)  
                    SetValue(NumberProperty, value)  
                End Set  
            End Property  
  
            ' Using a DependencyProperty as the backing store for Number.  This enables animation, styling, binding, etc...  
            Public Shared ReadOnly NumberProperty As DependencyProperty = DependencyProperty.Register("Number", GetType(Integer), GetType(QuickStartTask), New PropertyMetadata(0))  
  
            Public Property Title() As String  
                Get  
                    Return CStr(GetValue(TitleProperty))  
                End Get  
                Set(ByVal value As String)  
                    SetValue(TitleProperty, value)  
                End Set  
            End Property  
  
            ' Using a DependencyProperty as the backing store for Title.  This enables animation, styling, binding, etc...  
            Public Shared ReadOnly TitleProperty As DependencyProperty = DependencyProperty.Register("Title", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))  
  
            Public Property Description() As String  
                Get  
                    Return CStr(GetValue(DescriptionProperty))  
                End Get  
                Set(ByVal value As String)  
                    SetValue(DescriptionProperty, value)  
                End Set  
            End Property  
  
            ' Using a DependencyProperty as the backing store for Description.  This enables animation, styling, binding, etc...  
            Public Shared ReadOnly DescriptionProperty As DependencyProperty = DependencyProperty.Register("Description", GetType(String), GetType(QuickStartTask), New PropertyMetadata(Nothing))  
        End Class  
    ```  
  
     Esse código usa propriedades de dependência para definir os valores para os campos de número, título e descrição, em tempo de execução.  
  
8.  Na barra de menus, escolha **Compilar**, **WPFQuickStart Build** para compilar o controle de usuário.  
  
#### <a name="to-create-and-modify-the-main-window"></a>Para criar e modificar a janela principal  
  
1.  No **Gerenciador de Soluções**, clique duas vezes no arquivo **MainWindow.xaml**.  
  
2.  **Importante**. Essa etapa é apenas para C#. Se você estiver usando Visual Basic, pule para a próxima etapa. No painel inferior do designer, localize a linha `xmlns:local=”clr-namespace:WPFQuickStart”` e substitua-a pelo seguinte código XAML:  
  
    ```xaml  
    xmlns:local=”clr-namespace:WPFQuickStart.Common”  
    ```  
  
3.  Na janela **Propriedades**, expanda o nó de categoria **Comum**, escolha a propriedade **Título** e, em seguida, insira `WPF Todo List` e pressione a tecla **Enter**.  
  
     Observe que o elemento **Título** na janela do XAML é alterado para corresponder ao novo valor. Você pode modificar as propriedades de XAML na janela XAML ou na janela **Propriedades** e as alterações são sincronizadas.  
  
4.  Na janela XAML, defina o valor do elemento **Altura** como `768` e defina o valor da propriedade **Largura** como `1280`.  
  
     Esses elementos correspondem às propriedades **Altura** e **Largura**, encontradas na categoria **Layout** na janela **Propriedades**.  
  
5.  Selecione as marcas `<Grid>` e `</Grid>`, e substitua-as pelo seguinte código XAML:  
  
    ```xaml  
    <Grid>  
  
            <Grid Margin="50,50,10,10">  
                <Grid.ColumnDefinitions>  
                    <ColumnDefinition Width="*" />  
                    <ColumnDefinition Width="*" />  
                </Grid.ColumnDefinitions>  
                <Grid.RowDefinitions>  
                    <RowDefinition Height="Auto" />  
                    <RowDefinition Height="*" />  
                </Grid.RowDefinitions>  
  
                <Grid Grid.Row="0" Grid.ColumnSpan="2" Margin="0,0,0,20">  
                    <StackPanel>  
                        <TextBlock Foreground="#0094ff" FontFamily="Segoe UI Light" Margin="0,0,0,6">MICROSOFT AZURE MOBILE SERVICES</TextBlock>  
                        <TextBlock Foreground="Gray" FontFamily="Segoe UI Light" FontSize="45" ><Run Text="My Todo List"/></TextBlock>  
                    </StackPanel>  
                </Grid>  
  
                <Grid Grid.Row="1">  
                    <StackPanel>  
  
                        <local:QuickStartTask Number="1" Title="Insert a TodoItem" Description="Enter some text below and click Save to insert a new todo item into the list." />  
  
                        <StackPanel Orientation="Horizontal" Margin="72,0,0,0">  
                            <TextBox x:Name="TodoInput" Margin="5" MinWidth="300"/>  
                            <Button x:Name="ButtonSave" Click="ButtonSave_Click" Content="Save"/>  
                        </StackPanel>  
  
                    </StackPanel>  
                </Grid>  
  
                <Grid Grid.Row="1" Grid.Column="1">  
                    <Grid.RowDefinitions>  
                        <RowDefinition Height="Auto" />  
                        <RowDefinition />  
                    </Grid.RowDefinitions>  
                    <StackPanel>  
                        <local:QuickStartTask Number="2" Title="Query and Update Data" Description="Click the Refresh button to load the unfinished TodoItems from the Azure Mobile Service. Select the checkbox to mark a ToDo item as complete and update the list." />  
                        <Button Margin="72,0,0,0" Name="ButtonRefresh" Click="ButtonRefresh_Click">Refresh</Button>  
                    </StackPanel>  
  
                    <ListView Name="ListItems" Margin="62,10,0,0" Grid.Row="1">  
                        <ListView.ItemTemplate>  
                            <DataTemplate>  
                                <StackPanel Orientation="Horizontal">  
                                    <CheckBox Name="CheckBoxComplete" IsChecked="{Binding Complete, Mode=TwoWay}" Checked="CheckBoxComplete_Checked" Content="{Binding Text}" Margin="10,5" VerticalAlignment="Center"/>  
                                </StackPanel>  
                            </DataTemplate>  
                        </ListView.ItemTemplate>  
                    </ListView>  
  
                </Grid>  
  
            </Grid>  
        </Grid>  
    ```  
  
     Observe que as alterações são refletidas na janela de Design. Novamente, você também pode definir a interface do usuário adicionando controles na janela **Caixa de Ferramentas** e configurando propriedades na janela **Propriedades**. Tudo o que pode ser feito no designer pode ser feito no código XAML e vice-versa.  
  
     Neste ponto, seu design deve ser semelhante à ilustração a seguir.  
  
     ![MainWindow no designer](../designers/media/wpfquickstart2.PNG "WPFQuickStart2")  
  
    > [!NOTE]
    >  Ao seguir os próximos procedimentos, você poderá ver erros na **Lista de Erros** se ela estiver aberta. Não se preocupe; esses erros desaparecerão após a conclusão dos procedimentos restantes.  
  
6.  No **Gerenciador de Soluções**, expanda o nó **MainWindow.xaml** e abra o arquivo **MainWindow.xaml.cs** ou **MainWindow.xaml.vb**.  
  
7.  No Editor de Códigos, adicione as seguintes diretivas `using` ou `Imports` na parte superior do arquivo:  
  
    ```csharp  
    using Microsoft.WindowsAzure.MobileServices;  
    using Newtonsoft.Json;   
    ```  
  
    ```vb  
    Imports Microsoft.WindowsAzure.MobileServices  
    Imports Newtonsoft.Json  
    ```  
  
8.  Substitua todo o código no namespace **WPFQuickStart** (C#) ou **Classe MainWindow** (VB) pelo código a seguir:  
  
    ```csharp  
    namespace WPFQuickStart  
    {  
        /// <summary>  
        /// Interaction logic for MainWindow.xaml  
        /// </summary>  
        public class TodoItem  
        {  
            public string Id { get; set; }  
  
            [JsonProperty(PropertyName = "text")]  
            public string Text { get; set; }  
  
            [JsonProperty(PropertyName = "complete")]  
            public bool Complete { get; set; }  
        }  
  
        public partial class MainWindow : Window  
        {  
            private MobileServiceCollection<TodoItem, TodoItem> items;  
            private IMobileServiceTable<TodoItem> todoTable = App.MobileService.GetTable<TodoItem>();  
  
            public MainWindow()  
            {  
                InitializeComponent();  
            }  
  
            private async void InsertTodoItem(TodoItem todoItem)  
            {  
                // This code inserts a new TodoItem into the database. When the operation completes  
                // and Mobile Services has assigned an Id, the item is added to the CollectionView  
                await todoTable.InsertAsync(todoItem);  
                items.Add(todoItem);  
            }  
  
            private async void RefreshTodoItems()  
            {  
                try  
                {  
                    // This code refreshes the entries in the list view by querying the TodoItem table.  
                    // The query excludes completed TodoItems  
                    items = await todoTable  
                        .Where(todoItem => todoItem.Complete == false)  
                        .ToCollectionAsync();  
                    ListItems.ItemsSource = items;  
                }  
                catch (MobileServiceInvalidOperationException e)  
                {  
                    MessageBox.Show(e.Message, "Error loading items");  
                }  
            }  
  
            private async void UpdateCheckedTodoItem(TodoItem item)  
            {  
                // This code takes a freshly completed TodoItem and updates the database. When the MobileService   
                // responds, the item is removed from the list   
                await todoTable.UpdateAsync(item);  
                items.Remove(item);  
            }  
  
            private void ButtonRefresh_Click(object sender, RoutedEventArgs e)  
            {  
                RefreshTodoItems();  
            }  
  
            private void ButtonSave_Click(object sender, RoutedEventArgs e)  
            {  
                var todoItem = new TodoItem { Text = TodoInput.Text };  
                InsertTodoItem(todoItem);  
                TodoInput.Text = "";  
            }  
  
            private void CheckBoxComplete_Checked(object sender, RoutedEventArgs e)  
            {  
                CheckBox cb = (CheckBox)sender;  
                TodoItem item = cb.DataContext as TodoItem;  
                UpdateCheckedTodoItem(item);  
            }  
  
            protected override void OnActivated(EventArgs e)  
            {  
                RefreshTodoItems();  
            }  
        }  
  
    }  
    ```  
  
    ```vb  
    Public Class TodoItem  
        Public Property Id() As String  
  
        <JsonProperty(PropertyName:="text")>  
        Public Property Text() As String  
  
        <JsonProperty(PropertyName:="complete")>  
        Public Property Complete() As Boolean  
    End Class  
  
    Partial Public Class MainWindow  
        Inherits Window  
  
        Private items As MobileServiceCollection(Of TodoItem, TodoItem)  
        Private todoTable As IMobileServiceTable(Of TodoItem) = Application.MobileService.GetTable(Of TodoItem)()  
  
        Public Sub New()  
            InitializeComponent()  
        End Sub  
  
        Private Async Sub InsertTodoItem(ByVal todoItem As TodoItem)  
            ' This code inserts a new TodoItem into the database. When the operation completes  
            ' and Mobile Services has assigned an Id, the item is added to the CollectionView  
            Await todoTable.InsertAsync(todoItem)  
            items.Add(todoItem)  
        End Sub  
  
        Private Async Sub RefreshTodoItems()  
            Dim exception As MobileServiceInvalidOperationException = Nothing  
            Try  
                ' This code refreshes the entries in the list view by querying the TodoItem table.  
                ' The query excludes completed TodoItems  
                items = Await todoTable.Where(Function(todoItem) todoItem.Complete = False).ToCollectionAsync()  
            Catch e As MobileServiceInvalidOperationException  
                exception = e  
            End Try  
  
            If exception IsNot Nothing Then  
                MessageBox.Show(exception.Message, "Error loading items")  
            Else  
                ListItems.ItemsSource = items  
            End If  
        End Sub  
  
        Private Async Sub UpdateCheckedTodoItem(ByVal item As TodoItem)  
            ' This code takes a freshly completed TodoItem and updates the database. When the MobileService   
            ' responds, the item is removed from the list   
            Await todoTable.UpdateAsync(item)  
            items.Remove(item)  
        End Sub  
  
        Private Sub ButtonRefresh_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)  
            RefreshTodoItems()  
        End Sub  
  
        Private Sub ButtonSave_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)  
            Dim todoItem = New TodoItem With {.Text = TodoInput.Text}  
            InsertTodoItem(todoItem)  
            TodoInput.Text = ""  
        End Sub  
  
        Private Sub CheckBoxComplete_Checked(ByVal sender As Object, ByVal e As RoutedEventArgs)  
            Dim cb As CheckBox = DirectCast(sender, CheckBox)  
            Dim item As TodoItem = TryCast(cb.DataContext, TodoItem)  
            UpdateCheckedTodoItem(item)  
        End Sub  
  
        Protected Overrides Sub OnActivated(ByVal e As EventArgs)  
            RefreshTodoItems()  
        End Sub  
    End Class  
    ```  
  
     Esse código define a interação entre o banco de dados e a interface do usuário no serviço móvel, usando métodos assíncronos.  
  
## <a name="create-the-azure-mobile-service"></a>Criar o serviço móvel do Azure  
 A etapa final é criar um serviço móvel no Microsoft Azure, adicionar uma tabela para armazenar os dados e, em seguida, fazer referência à instância de serviço no seu aplicativo.  
  
#### <a name="to-create-a-mobile-service"></a>Para criar um serviço móvel  
  
1.  Abra um navegador da Web e faça logon no portal do Microsoft Azure e escolha a guia **SERVIÇOS MÓVEIS**.  
  
2.  Escolha o botão **NOVO** e na caixa de diálogo pop-up escolha **COMPUTAÇÃO**, **SERVIÇO MÓVEL,CRIAR**.  
  
3.  Na caixa de diálogo **NOVO SERVIÇO MÓVEL**, escolha a caixa de texto **URL** e insira `wpfquickstart01`.  
  
    > [!NOTE]
    >  Talvez seja necessário alterar a parte numérica da URL. O Microsoft Azure requer uma URL exclusiva para cada serviço móvel.  
  
     Isso define a URL para o serviço *https://wpfquickstart01.azure-mobile.net/*.  
  
4.  Na lista **BANCO DE DADOS**, escolha uma opção de banco de dados. Como esse é um aplicativo que provavelmente não terá muito uso, você pode escolher a opção **Criar um banco de dados SQL de 20 MB gratuito** ou escolher o banco de dados gratuito já associado à sua assinatura.  
  
5.  Na lista **REGIÃO**, escolha o data center em que você deseja implantar o serviço móvel e, em seguida, escolha o botão **Avançar** (seta para a direita).  
  
    > [!NOTE]
    >  Para este serviço, você usará a configuração padrão de **BACK-END**, **JavaScript**.  
  
6.  Se você estiver criando um novo banco de dados na página **Especificar configurações de banco de dados**, na lista **SERVIDOR** escolha **Novo servidor de banco de dados SQL**, insira seu **NOME DE LOGON DO SQL** e sua **SENHA**e, em seguida, escolha o botão **Concluir** (marca de seleção).  
  
7.  Se você escolher um banco de dados existente, na página **Configurações de Banco de Dados**, insira sua **SENHA DE LOGON** e, em seguida, escolha o botão **Concluir** (marca de seleção).  
  
     O processo de criação de serviço móvel será iniciado. Quando o processo é concluído, o status é alterado para **Pronto** e você pode ir para a próxima etapa.  
  
8.  No portal, selecione o serviço móvel recém-criado e, em seguida, escolha o botão **GERENCIAR CHAVES**.  
  
9. Na caixa de diálogo **Gerenciar Chaves de Acesso**, copie a **CHAVE DO APLICATIVO**.  
  
     Você a usará no próximo procedimento.  
  
#### <a name="to-create-a-table"></a>Para criar uma tabela  
  
1.  No portal do Microsoft Azure, escolha a seta para a direita ao lado do nome do seu serviço móvel e, na barra de menus, escolha **DADOS**e, em seguida, escolha o link **ADICIONAR UMA TABELA**.  
  
2.  Na caixa de diálogo **Criar Nova Tabela**, na caixa de texto **NOME DA TABELA**, insira `TodoItem` e, em seguida, escolha o botão **Concluir** (marca de seleção).  
  
     Aguarde a tabela ser criada e, em seguida, passe para o procedimento final.  
  
#### <a name="to-add-a-declaration-for-the-mobile-service"></a>Para adicionar uma declaração para o serviço móvel  
  
1.  Retorne ao Visual Studio. No **Gerenciador de Soluções**, expanda o nó **App.xaml** (C#) ou **Application.xaml** (Visual Basic) e abra o arquivo **App.xaml.cs** ou **App.xaml.vb**.  
  
2.  No Editor de Códigos, adicione as seguintes diretivas `using` ou **Importações** ao topo do arquivo:  
  
    ```csharp  
    using Microsoft.WindowsAzure.MobileServices;  
    ```  
  
    ```vb  
    Imports Microsoft.WindowsAzure.MobileServices  
    ```  
  
3.  Adicione a seguinte declaração à classe, substituindo *YOUR-SERVICE_HERE* pelo nome da URL de seu serviço e substituindo *YOUR-KEY-HERE* pela chave do aplicativo que você copiou no procedimento anterior:  
  
    ```csharp  
    public static MobileServiceClient MobileService = new MobileServiceClient(  
                 "https://YOUR-SERVICE-HERE.azure-mobile.net/",  
                 "YOUR-KEY-HERE"  
             );  
    ```  
  
    ```vb  
    Public Shared MobileService As New MobileServiceClient("https://YOUR-SERVICE-HERE.azure-mobile.net/", "YOUR-KEY-HERE")  
    ```  
  
     Esse código permite que o aplicativo acesse o serviço móvel em execução no Microsoft Azure.  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 É isso – você criou um aplicativo de área de trabalho do WPF que acessa um serviço móvel do Azure. Agora tudo o que resta é executar o aplicativo e vê-lo em ação.  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
1.  Na barra de menus, selecione **Depurar**, **Iniciar Depuração** (ou pressione F5).  
  
2.  Na caixa de texto **Inserir um TodoItem**, digite `Do something`e, em seguida, escolha o botão **Salvar**.  
  
3.  Digite `Do something else`e, em seguida, escolha o botão **Salvar** novamente.  
  
     Observe que as duas entradas são adicionadas á lista **Consultar e Atualizar Dados**, conforme mostrado na ilustração a seguir.  
  
     ![Os itens Todo são adicionados à lista. ](../designers/media/wpfquickstart3.PNG "WPFQuickStart3")  
  
4.  Marque a caixa de seleção para a entrada **Fazer algo mais** na lista.  
  
     Isso chama o método **UpdateCheckedTodoItem** e remove o item da lista e do banco de dados.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você concluiu um exemplo bastante simples de um aplicativo de área de trabalho do WPF com um back-end do Azure. Naturalmente um aplicativo real é muito mais complexo, mas os mesmos conceitos básicos se aplicam. Consulte [WPF no .NET Framework](https://msdn.microsoft.com/library/ms754130\(v=vs.100\).aspx).  
  
 Você pode tornar a interface do usuário mais atraente adicionando cores, formas, gráficos e até animações. Consulte [Criando o XAML no Visual Studio e no Blend for Visual Studio](../designers/designing-xaml-in-visual-studio.md).  
  
 Você pode se conectar a bancos de dados do SQL existentes ou outras fontes de dados usando os serviços móveis do Azure. Consulte [Documentação dos serviços móveis](http://azure.microsoft.com/services/app-service/mobile/).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Meu primeiro aplicativo da área de trabalho do WPF](../designers/walkthrough-my-first-wpf-desktop-application2.md)   
 [Criar modernos aplicativos da área de trabalho com o Windows Presentation Foundation](../designers/create-modern-desktop-applications-with-windows-presentation-foundation.md)



