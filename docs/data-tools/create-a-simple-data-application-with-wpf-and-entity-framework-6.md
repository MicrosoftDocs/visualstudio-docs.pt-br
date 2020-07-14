---
title: Aplicativo de dados simples com o WPF e o Entity Framework 6
ms.date: 08/22/2017
ms.topic: conceptual
dev_langs:
- CSharp
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4aa978098c459d9e55ef0dc1423080357e067a5b
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282755"
---
# <a name="create-a-simple-data-application-with-wpf-and-entity-framework-6"></a>Criar um aplicativo de dados simples com o WPF e o Entity Framework 6

Este tutorial mostra como criar um aplicativo básico "formulários sobre dados" no Visual Studio. O aplicativo usa SQL Server LocalDB, o banco de dados Northwind, Entity Framework 6 (não Entity Framework Core) e Windows Presentation Foundation para .NET Framework (não .NET Core). Ele mostra como fazer DataBinding básica com um modo de exibição de detalhes mestre e também tem um navegador de associação personalizado com botões para **mover próximo**, **mover**para o **início**, mover para **o fim**, **Atualizar** e **excluir**.

Este artigo se concentra no uso de ferramentas de dados no Visual Studio e não tenta explicar as tecnologias subjacentes em qualquer profundidade. Ele pressupõe que você tenha uma familiaridade básica com XAML, Entity Framework e SQL. Este exemplo também não demonstra a arquitetura MVVM (Model-View-ViewModel), que é o padrão para aplicativos do WPF. No entanto, você pode copiar esse código em seu próprio aplicativo MVVM com poucas modificações.

## <a name="install-and-connect-to-northwind"></a>Instalar e conectar-se à Northwind

Este exemplo usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind. Se o provedor de dados ADO.NET para esse produto der suporte a Entity Framework, ele também deverá funcionar com outros produtos de banco de dado SQL.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **Instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho do **Desenvolvimento para desktop com .NET** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O**pesquisador de objetos do SQL Server** é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no **instalador do Visual Studio**.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

3. [Adicionar novas conexões](../data-tools/add-new-connections.md) para a Northwind.

## <a name="configure-the-project"></a>Configurar o projeto

1. No Visual Studio, crie um novo projeto de **aplicativo do WPF** em C#.

2. Adicione o pacote NuGet para o Entity Framework 6. Em **Gerenciador de soluções**, selecione o nó do projeto. No menu principal, escolha **projeto**  >  **gerenciar pacotes NuGet**.

     ![Item de menu gerenciar pacotes NuGet](../data-tools/media/raddata_vs2015_manage_nuget_packages.png)

3. No **Gerenciador de pacotes NuGet**, clique no link **procurar** . Entity Framework é provavelmente o pacote superior na lista. Clique em **instalar** no painel direito e siga os prompts. A janela de saída informa quando a instalação é concluída.

     ![Entity Framework pacote NuGet](../data-tools/media/raddata_vs2015_nuget_ef.png)

4. Agora você pode usar o Visual Studio para criar um modelo com base no banco de dados Northwind.

## <a name="create-the-model"></a>Criar o modelo

1. Clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e escolha **Adicionar**  >  **novo item**. No painel esquerdo, no nó C#, escolha **dados** e, no painel central, escolha **ADO.NET modelo de dados de entidade**.

   ![Novo item do modelo de Entity Framework](../data-tools/media/raddata-ef-new-project-item.png)

2. Chame o modelo `Northwind_model` e escolha **OK**. O **Assistente de modelo de dados de entidade** é aberto. Escolha o **designer do EF no banco de dados** e clique em **Avançar**.

   ![Modelo de EF do banco de dados](../data-tools/media/raddata-ef-model-from-database.png)

3. Na próxima tela, insira ou escolha a sua conexão Northwind do LocalDB (por exemplo, (LocalDB) \MSSQLLocalDB), especifique o banco de dados Northwind e clique em **Avançar**.

4. Na próxima página do assistente, escolha quais tabelas, procedimentos armazenados e outros objetos de banco de dados incluir no modelo de Entity Framework. Expanda o nó dbo no modo de exibição de árvore e escolha **clientes**, **pedidos**e **detalhes do pedido**. Deixe os padrões marcados e clique em **concluir**.

    ![Escolher objetos de banco de dados para o modelo](../data-tools/media/raddata-choose-ef-objects.png)

5. O assistente gera as classes C# que representam o modelo de Entity Framework. As classes são classes C# antigas e são as que fazemos a vinculação à interface do usuário do WPF. O arquivo *. edmx* descreve as relações e outros metadados que associam as classes a objetos no banco de dados. Os arquivos *. tt* são modelos T4 que geram o código que opera no modelo e salva as alterações no banco de dados. Você pode ver todos esses arquivos em **Gerenciador de soluções** no nó Northwind_model:

      ![Arquivos de modelo do Gerenciador de Soluções EF](../data-tools/media/raddata-solution-explorer-ef-model-files.png)

    A superfície do designer para o arquivo *. edmx* permite que você modifique algumas propriedades e relações no modelo. Não usaremos o designer neste passo a passos.

6. Os arquivos *. tt* são de uso geral e você precisa ajustar um deles para trabalhar com a ligação de dados do WPF, o que exige ObservableCollections. Em **Gerenciador de soluções**, expanda o Northwind_model nó até encontrar *Northwind_model. tt*. (Verifique se você não está no *. Arquivo Context.tt* , que está diretamente abaixo do arquivo *. edmx* .)

   - Substitua as duas ocorrências de <xref:System.Collections.ICollection> por <xref:System.Collections.ObjectModel.ObservableCollection%601> .

   - Substitua a primeira ocorrência de <xref:System.Collections.Generic.HashSet%601> por pela <xref:System.Collections.ObjectModel.ObservableCollection%601> linha 51. Não substitua a segunda ocorrência de HashSet.

   - Substitua a única ocorrência de <xref:System.Collections.Generic> (em torno da linha 431) por <xref:System.Collections.ObjectModel> .

7. Pressione **Ctrl** + **Shift** + **B** para compilar o projeto. Quando a compilação é concluída, as classes de modelo são visíveis para o assistente de fontes de dados.

Agora você está pronto para conectar esse modelo à página XAML para que possa exibir, navegar e modificar os dados.

## <a name="databind-the-model-to-the-xaml-page"></a>Vincule o modelo à página XAML

É possível escrever seu próprio código de ligação de dados, mas é muito mais fácil permitir que o Visual Studio faça isso para você.

1. No menu principal, escolha **projeto**  >  **Adicionar nova fonte de dados** para abrir o **Assistente de configuração da fonte de dados**. Escolha o **objeto** porque você está associando às classes de modelo, não ao banco de dados:

     ![Assistente de configuração de fonte de dados com fonte de objeto](../data-tools/media/raddata-data-source-configuration-wizard-with-object-source.png)

2. Expanda o nó do seu projeto e selecione **cliente**. (As fontes para pedidos são geradas automaticamente a partir da propriedade de navegação Orders no Customer.)

     ![Adicionar classes de entidade como fontes de dados](../data-tools/media/raddata-add-entity-classes-as-data-sources.png)

3. Clique em **Concluir**.

4. Navegue até *MainWindow. XAML* na exibição de código. Estamos mantendo o XAML simples para os fins deste exemplo. Altere o título de MainWindow para algo mais descritivo e aumente sua altura e largura para 600 x 800 por enquanto. Você sempre pode alterá-lo mais tarde. Agora, adicione essas três definições de linha à grade principal, uma linha para os botões de navegação, uma para os detalhes do cliente e outra para a grade que mostra seus pedidos:

    ```xaml
        <Grid.RowDefinitions>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="auto"/>
            <RowDefinition Height="*"/>
        </Grid.RowDefinitions>
    ```

5. Agora, abra *MainWindow. XAML* para exibi-lo no designer. Isso faz com que a janela **fontes de dados** apareça como uma opção na margem da janela do Visual Studio ao lado da **caixa de ferramentas**. Clique na guia para abrir a janela ou pressione **Shift** + **ALT** + **D** ou escolha **Exibir**  >  **outras**  >  **fontes de dados**do Windows. Vamos exibir cada propriedade na classe Customers em sua própria caixa de texto individual. Primeiro, clique na seta na caixa de combinação **clientes** e escolha **detalhes**. Em seguida, arraste o nó para a parte intermediária da superfície de design para que o designer saiba que você deseja que ele vá para a linha intermediária. Se você o perdeu, poderá especificar a linha manualmente mais tarde no XAML. Por padrão, os controles são colocados verticalmente em um elemento de grade, mas, neste ponto, você pode organizá-los no desejado no formulário. Por exemplo, pode fazer sentido colocar a caixa de texto **nome** na parte superior, acima do endereço. O aplicativo de exemplo para este artigo reordena os campos e os reorganiza em duas colunas.

     ![Associação de fonte de dados de clientes a controles individuais](../data-tools/media/raddata-customers-data-source-binding-to-individual-controls.png)

     No modo de exibição de código, agora você pode ver um novo `Grid` elemento na linha 1 (a linha intermediária) da grade pai. A grade pai tem um `DataContext` atributo que se refere a um CollectionViewSource que foi adicionado ao `Windows.Resources` elemento. Dado esse contexto de dados, quando a primeira caixa de texto é vinculada ao **endereço**, esse nome é mapeado para a `Address` propriedade no `Customer` objeto atual no CollectionViewSource.

    ```xaml
    <Grid DataContext="{StaticResource customerViewSource}">
    ```

6. Quando um cliente fica visível na metade superior da janela, você deseja ver seus pedidos na metade inferior. Você mostra os pedidos em um controle de exibição de grade única. Para que a associação de dados de detalhes mestre funcione conforme o esperado, é importante que você se vincule à propriedade Orders na classe Customers, não ao nó Orders separado. Arraste a propriedade Orders da classe Customers para a metade inferior do formulário, para que o designer a coloque na linha 2:

     ![Arrastar classes Orders como grade](../data-tools/media/raddata-drag-orders-classes-as-grid.png)

7. O Visual Studio gerou todo o código de ligação que conecta os controles da interface do usuário a eventos no modelo. Tudo o que você precisa fazer para ver alguns dados é escrever algum código para preencher o modelo. Primeiro, navegue até *MainWindow.XAML.cs* e adicione um membro de dados à classe MainWindow para o contexto de dados. Esse objeto, que foi gerado para você, atua como um controle que controla as alterações e eventos no modelo. Você também adicionará membros de dados do CollectionViewSource para clientes e pedidos e a lógica de inicialização do Construtor associada. A parte superior da classe deve ter a seguinte aparência:

     [!code-csharp[MainWindow#1](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#1)]

     Adicione uma `using` diretiva para System. Data. Entity para colocar o método de extensão de carga no escopo:

     ```csharp
     using System.Data.Entity;
     ```

     Agora, role para baixo e localize o `Window_Loaded` manipulador de eventos. Observe que o Visual Studio adicionou um objeto CollectionViewSource. Isso representa o objeto NorthwindEntities que você selecionou quando criou o modelo. Você adicionou isso já, portanto, não precisa dela aqui. Vamos substituir o código `Window_Loaded` para que o método agora se pareça com o seguinte:

     [!code-csharp[Window_Loaded#2](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#2)]

8. Pressione **F5**. Você deve ver os detalhes do primeiro cliente que foi recuperado para o CollectionViewSource. Você também deve ver seus pedidos na grade de dados. A formatação não é ótima, então vamos corrigi-la. Você também pode criar uma maneira de exibir os outros registros e realizar operações CRUD básicas.

## <a name="adjust-the-page-design-and-add-grids-for-new-customers-and-orders"></a>Ajustar o design da página e adicionar grades para novos clientes e pedidos

A organização padrão produzida pelo Visual Studio não é ideal para seu aplicativo, portanto, forneceremos o XAML final aqui para copiar em seu código. Você também precisa de alguns "formulários" (que são, na verdade, grades) para permitir que o usuário adicione um novo cliente ou pedido. Para poder adicionar um novo cliente e uma ordem, você precisa de um conjunto separado de caixas de texto que não sejam associadas a dados ao `CollectionViewSource` . Você controlará qual grade o usuário vê em um determinado momento definindo a propriedade Visible nos métodos do manipulador. Por fim, você adiciona um botão excluir a cada linha na grade Orders para permitir que o usuário exclua uma ordem individual.

Primeiro, adicione esses estilos ao `Windows.Resources` elemento em *MainWindow. XAML*:

```xaml
<Style x:Key="Label" TargetType="{x:Type Label}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Left"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="23"/>
</Style>
<Style x:Key="CustTextBox" TargetType="{x:Type TextBox}" BasedOn="{x:Null}">
    <Setter Property="HorizontalAlignment" Value="Right"/>
    <Setter Property="VerticalAlignment" Value="Center"/>
    <Setter Property="Margin" Value="3"/>
    <Setter Property="Height" Value="26"/>
    <Setter Property="Width" Value="120"/>
</Style>
```

Em seguida, substitua toda a grade externa por esta marcação:

```xaml
<Grid>
     <Grid.RowDefinitions>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="auto"/>
         <RowDefinition Height="*"/>
     </Grid.RowDefinitions>
     <Grid x:Name="existingCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" Margin="5" Visibility="Visible" VerticalAlignment="Top" Background="AntiqueWhite" DataContext="{StaticResource customerViewSource}">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newCustomerGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding RelativeSource={RelativeSource FindAncestor, AncestorType={x:Type Window}}, Path=newCustomer, UpdateSourceTrigger=Explicit}" Visibility="Collapsed" Background="CornflowerBlue">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="Customer ID:" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_customerIDTextBox" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding CustomerID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Company Name:" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_companyNameTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding CompanyName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true }"/>
         <Label Content="Contact Name:" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactNameTextBox" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactName, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Contact title:" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_contactTitleTextBox" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding ContactTitle, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Address:" Grid.Row="4" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_addressTextBox" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding Address, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="City:" Grid.Column="1" Grid.Row="0" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_cityTextBox" Grid.Column="1" Grid.Row="0" Style="{StaticResource CustTextBox}"
                  Text="{Binding City, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Country:" Grid.Column="1" Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_countryTextBox" Grid.Column="1" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding Country, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Fax:" Grid.Column="1" Grid.Row="2" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_faxTextBox" Grid.Column="1" Grid.Row="2" Style="{StaticResource CustTextBox}"
                  Text="{Binding Fax, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Phone:" Grid.Column="1" Grid.Row="3" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_phoneTextBox" Grid.Column="1" Grid.Row="3" Style="{StaticResource CustTextBox}"
                  Text="{Binding Phone, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Postal Code:" Grid.Column="1" Grid.Row="4" VerticalAlignment="Center" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_postalCodeTextBox" Grid.Column="1" Grid.Row="4" Style="{StaticResource CustTextBox}"
                  Text="{Binding PostalCode, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Region:" Grid.Column="1" Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_regionTextBox" Grid.Column="1" Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding Region, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <Grid x:Name="newOrderGrid" Grid.Row="1" HorizontalAlignment="Left" VerticalAlignment="Top" Margin="5" DataContext="{Binding Path=newOrder, Mode=TwoWay}" Visibility="Collapsed" Background="LightGreen">
         <Grid.ColumnDefinitions>
             <ColumnDefinition Width="Auto" MinWidth="233"/>
             <ColumnDefinition Width="Auto" MinWidth="397"/>
         </Grid.ColumnDefinitions>
         <Grid.RowDefinitions>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
             <RowDefinition Height="Auto"/>
         </Grid.RowDefinitions>
         <Label Content="New Order Form" FontWeight="Bold"/>
         <Label Content="Employee ID:"  Grid.Row="1" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_employeeIDTextBox" Grid.Row="1" Style="{StaticResource CustTextBox}"
                  Text="{Binding EmployeeID, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Order Date:"  Grid.Row="2" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_orderDatePicker" Grid.Row="2"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Required Date:" Grid.Row="3" Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_requiredDatePicker" Grid.Row="3" HorizontalAlignment="Right" Width="120"
                  SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Shipped Date:"  Grid.Row="4"  Style="{StaticResource Label}"/>
         <DatePicker x:Name="add_shippedDatePicker"  Grid.Row="4"  HorizontalAlignment="Right" Width="120"
                 SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
         <Label Content="Ship Via:"  Grid.Row="5" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_ShipViaTextBox"  Grid.Row="5" Style="{StaticResource CustTextBox}"
                  Text="{Binding ShipVia, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
         <Label Content="Freight"  Grid.Row="6" Style="{StaticResource Label}"/>
         <TextBox x:Name="add_freightTextBox" Grid.Row="6" Style="{StaticResource CustTextBox}"
                  Text="{Binding Freight, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true}"/>
     </Grid>
     <DataGrid x:Name="ordersDataGrid" SelectionUnit="Cell" SelectionMode="Single" AutoGenerateColumns="False" CanUserAddRows="false" IsEnabled="True" EnableRowVirtualization="True" Width="auto" ItemsSource="{Binding Source={StaticResource customerOrdersViewSource}}" Margin="10,10,10,10" Grid.Row="2" RowDetailsVisibilityMode="VisibleWhenSelected">
         <DataGrid.Columns>
             <DataGridTemplateColumn>
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <Button Content="Delete" Command="{StaticResource DeleteOrderCommand}" CommandParameter="{Binding}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="customerIDColumn" Binding="{Binding CustomerID}" Header="Customer ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="employeeIDColumn" Binding="{Binding EmployeeID}" Header="Employee ID" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="freightColumn" Binding="{Binding Freight}" Header="Freight" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="orderDateColumn" Header="Order Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding OrderDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="orderIDColumn" Binding="{Binding OrderID}" Header="Order ID" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="requiredDateColumn" Header="Required Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding RequiredDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipAddressColumn" Binding="{Binding ShipAddress}" Header="Ship Address" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCityColumn" Binding="{Binding ShipCity}" Header="Ship City" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipCountryColumn" Binding="{Binding ShipCountry}" Header="Ship Country" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipNameColumn" Binding="{Binding ShipName}" Header="Ship Name" Width="SizeToHeader"/>
             <DataGridTemplateColumn x:Name="shippedDateColumn" Header="Shipped Date" Width="SizeToHeader">
                 <DataGridTemplateColumn.CellTemplate>
                     <DataTemplate>
                         <DatePicker SelectedDate="{Binding ShippedDate, Mode=TwoWay, NotifyOnValidationError=true, ValidatesOnExceptions=true, UpdateSourceTrigger=PropertyChanged}"/>
                     </DataTemplate>
                 </DataGridTemplateColumn.CellTemplate>
             </DataGridTemplateColumn>
             <DataGridTextColumn x:Name="shipPostalCodeColumn" Binding="{Binding ShipPostalCode}" Header="Ship Postal Code" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipRegionColumn" Binding="{Binding ShipRegion}" Header="Ship Region" Width="SizeToHeader"/>
             <DataGridTextColumn x:Name="shipViaColumn" Binding="{Binding ShipVia}" Header="Ship Via" Width="SizeToHeader"/>
         </DataGrid.Columns>
     </DataGrid>
 </Grid>
```

## <a name="add-buttons-to-navigate-add-update-and-delete"></a>Adicionar botões para navegar, adicionar, atualizar e excluir

Em Windows Forms aplicativos, você obtém um objeto BindingNavigator com botões para navegar pelas linhas de um banco de dados e fazer operações CRUD básicas. O WPF não fornece um BindingNavigator, mas é fácil de criar um. Você faz isso com botões dentro de um StackPanel horizontal e associa os botões a comandos que são associados a métodos no code-behind.

Há quatro partes para a lógica de comando: (1) os comandos, (2) as associações, (3) os botões e (4) os manipuladores de comandos no code-behind.

### <a name="add-commands-bindings-and-buttons-in-xaml"></a>Adicionar comandos, associações e botões em XAML

1. Primeiro, adicione os comandos no arquivo *MainWindow. XAML* dentro do `Windows.Resources` elemento:

    ```xaml
    <RoutedUICommand x:Key="FirstCommand" Text="First"/>
    <RoutedUICommand x:Key="LastCommand" Text="Last"/>
    <RoutedUICommand x:Key="NextCommand" Text="Next"/>
    <RoutedUICommand x:Key="PreviousCommand" Text="Previous"/>
    <RoutedUICommand x:Key="DeleteCustomerCommand" Text="Delete Customer"/>
    <RoutedUICommand x:Key="DeleteOrderCommand" Text="Delete Order"/>
    <RoutedUICommand x:Key="UpdateCommand" Text="Update"/>
    <RoutedUICommand x:Key="AddCommand" Text="Add"/>
    <RoutedUICommand x:Key="CancelCommand" Text="Cancel"/>
    ```

2. Um CommandBinding mapeia um `RoutedUICommand` evento para um método no code-behind. Adicione este `CommandBindings` elemento após a `Windows.Resources` marca de fechamento:

    ```xaml
    <Window.CommandBindings>
        <CommandBinding Command="{StaticResource FirstCommand}" Executed="FirstCommandHandler"/>
        <CommandBinding Command="{StaticResource LastCommand}" Executed="LastCommandHandler"/>
        <CommandBinding Command="{StaticResource NextCommand}" Executed="NextCommandHandler"/>
        <CommandBinding Command="{StaticResource PreviousCommand}" Executed="PreviousCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteCustomerCommand}" Executed="DeleteCustomerCommandHandler"/>
        <CommandBinding Command="{StaticResource DeleteOrderCommand}" Executed="DeleteOrderCommandHandler"/>
        <CommandBinding Command="{StaticResource UpdateCommand}" Executed="UpdateCommandHandler"/>
        <CommandBinding Command="{StaticResource AddCommand}" Executed="AddCommandHandler"/>
        <CommandBinding Command="{StaticResource CancelCommand}" Executed="CancelCommandHandler"/>
    </Window.CommandBindings>
    ```

3. Agora, adicione o `StackPanel` com os botões de navegação, adicionar, excluir e atualizar. Primeiro, adicione este estilo a `Windows.Resources` :

    ```xaml
    <Style x:Key="NavButton" TargetType="{x:Type Button}" BasedOn="{x:Null}">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontFamily" Value="Segoe UI Symbol"/>
        <Setter Property="Margin" Value="2,2,2,0"/>
        <Setter Property="Width" Value="40"/>
        <Setter Property="Height" Value="auto"/>
    </Style>
    ```

     Em segundo lugar, Cole esse código logo após o `RowDefinitions` para o `Grid` elemento externo, em direção à parte superior da página XAML:

    ```xaml
    <StackPanel Orientation="Horizontal" Margin="2,2,2,0" Height="36" VerticalAlignment="Top" Background="Gainsboro" DataContext="{StaticResource customerViewSource}" d:LayoutOverrides="LeftMargin, RightMargin, TopMargin, BottomMargin">
        <Button Name="btnFirst" Content="|◄" Command="{StaticResource FirstCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnPrev" Content="◄" Command="{StaticResource PreviousCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnNext" Content="►" Command="{StaticResource NextCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnLast" Content="►|" Command="{StaticResource LastCommand}" Style="{StaticResource NavButton}"/>
        <Button Name="btnDelete" Content="Delete Customer" Command="{StaticResource DeleteCustomerCommand}" FontSize="11" Width="120" Style="{StaticResource NavButton}"/>
        <Button Name="btnAdd" Content="New Customer" Command="{StaticResource AddCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="New Order" Name="btnNewOrder" FontSize="11" Width="80" Style="{StaticResource NavButton}" Click="NewOrder_click"/>
        <Button Name="btnUpdate" Content="Commit" Command="{StaticResource UpdateCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
        <Button Content="Cancel" Name="btnCancel" Command="{StaticResource CancelCommand}" FontSize="11" Width="80" Style="{StaticResource NavButton}"/>
    </StackPanel>
    ```

### <a name="add-command-handlers-to-the-mainwindow-class"></a>Adicionar manipuladores de comandos à classe MainWindow

O code-behind é mínimo, exceto para os métodos Add e Delete. A navegação é executada por meio da chamada de métodos na Propriedade View do CollectionViewSource. O `DeleteOrderCommandHandler` mostra como executar uma exclusão em cascata em um pedido. Precisamos primeiro excluir os Order_Details associados a ele. O `UpdateCommandHandler` adiciona um novo cliente ou uma ordem à coleção, ou apenas atualiza um cliente existente ou uma ordem com as alterações que o usuário fez nas caixas de texto.

Adicione esses métodos de manipulador à classe MainWindow em *MainWindow.XAML.cs*. Se o seu CollectionViewSource para a tabela Customers tiver um nome diferente, você precisará ajustar o nome em cada um destes métodos:

[!code-csharp[CommandHandlers#3](../data-tools/codesnippet/CSharp/CreateWPFDataApp/MainWindow.xaml.cs#3)]

## <a name="run-the-application"></a>Executar o aplicativo

Para iniciar a depuração, pressione **F5**. Você deve ver os dados do cliente e do pedido populados na grade e os botões de navegação devem funcionar conforme o esperado. Clique em **confirmar** para adicionar um novo cliente ou pedido ao modelo depois de inserir os dados. Clique em **Cancelar** para voltar a um novo formulário de cliente ou de novo pedido sem salvar os dados. Você pode fazer edições em clientes e pedidos existentes diretamente nas caixas de texto, e essas alterações são gravadas automaticamente no modelo.

## <a name="see-also"></a>Veja também

- [Ferramentas de dados do Visual Studio para .NET](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Documentação do Entity Framework](/ef/)
