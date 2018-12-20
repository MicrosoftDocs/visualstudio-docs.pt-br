---
title: Código-fonte de L2DBForm.xaml | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 624e96d4-6d27-4195-8ac2-2f3835f6c57e
caps.latest.revision: 4
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 291f7ece2c53d168125da32a11e50ca42e19f3fb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49207682"
---
# <a name="l2dbformxaml-source-code"></a>Código de L2DBForm.xaml
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico contém e descreve o arquivo de origem XAML para a [Vinculação de dados de WPF usando o exemplo LINQ to XML](../designers/wpf-data-binding-using-linq-to-xml-example.md), L2DBForm.xaml.  
  
## <a name="overall-ui-structure"></a>Estrutura geral de interface de usuário  
 Como típico é para um projeto de WPF, esse arquivo contém um elemento pai, um elemento XML <xref:System.Windows.Window> associado com a classe derivada `L2XDBFrom` no espaço de `LinqToXmlDataBinding` .  
  
 A área cliente está contida dentro de <xref:System.Windows.Controls.StackPanel> que recebe um plano de fundo azul. Esse painel contém quatro seções de <xref:System.Windows.Controls.DockPanel> interface do usuário separados por barras de <xref:System.Windows.Controls.Separator> . O objetivo dessas seções é descrito em **Comentários** no [tópico anterior](../designers/walkthrough-linqtoxmldatabinding-example.md).  
  
 Cada seção contém um rótulo que a identifica. Nas duas primeiras seções, este rótulo é girada em 90 graus com o uso de <xref:System.Windows.FrameworkElement.LayoutTransform%2A>. O restante da seção contém os elementos de interface do usuário apropriados para a finalidade dessa seção: blocos de texto, caixas de texto, botões, e assim por diante. Um filho <xref:System.Windows.Controls.StackPanel> são às vezes para alinhar esses controles filho.  
  
## <a name="window-resource-section"></a>Seção de recursos de janela  
 A marca de abertura `<Window.Resources>` na linha 9 indica o início da seção de recursos da janela. Termina com a marca de fechamento na linha 35.  
  
 A marca de `<ObjectDataProvider>` , que abrange as linhas 11 a 25, declara <xref:System.Windows.Data.ObjectDataProvider>, `LoadedBooks`chamado, que usa <xref:System.Xml.Linq.XElement> como a fonte. Este <xref:System.Xml.Linq.XElement> é inicializado analisar um documento XML inserido (um elemento de `CDATA` ). Observe que o espaço em branco é preservada quando declarar o documento XML inserido e também quando é analisado. Isso foi feito como o controle de <xref:System.Windows.Controls.TextBlock> , que é usado para exibir XML brutos, não tem XML especial que formata recursos.  
  
 Finalmente, <xref:System.Windows.DataTemplate> chamado `BookTemplate` é definido em linhas 28 a 34. Este modelo será usado para exibir as entradas na seção de interface do usuário da **Lista de Livros**. Usa associação de dados e propriedades dinâmicas LINQ to XML para recuperar a identificação do livro e o nome de livro com as atribuições seguintes:  
  
```  
Text="{Binding Path=Attribute[id].Value}"Text="{Binding Path=Value}"  
```  
  
## <a name="data-binding-code"></a>Código de associação de dados  
 Além do elemento de <xref:System.Windows.DataTemplate> , associação de dados é usada em um número de outros locais neste arquivo.  
  
 Na marca de abertura `<StackPanel>` na linha 38, a propriedade de <xref:System.Windows.FrameworkElement.DataContext%2A> desse painel é definida para o provedor de dados de `LoadedBooks` .  
  
```  
DataContext="{Binding Source={StaticResource LoadedBooks}}  
```  
  
 Isso torna possível na linha (46) para <xref:System.Windows.Controls.TextBlock> chamado `tbRawXml` para exibir XML brutos associando a propriedade de `Xml` deste provedor de dados:  
  
```  
Text="{Binding Path=Xml}"   
```  
  
 A <xref:System.Windows.Controls.ListBox> na seção da interface do usuário **Lista de Livros**, nas linhas 58 a 62, define o modelo para seus itens de exibição como o `BookTemplate` definido na seção de recursos de janela:  
  
```  
ItemTemplate ="{StaticResource BookTemplate}"   
```  
  
 Em seguida, linhas 59 a 62, os valores reais dos livros são associados à caixa de listagem:  
  
```  
<ListBox.ItemsSource>  
    <Binding Path="Elements[{http://www.mybooks.com}book]"/>  
</ListBox.ItemsSource>  
```  
  
 A terceira seção da interface do usuário, **Editar Livro Selecionado**, primeiro associa o <xref:System.Windows.FrameworkElement.DataContext%2A> do <xref:System.Windows.Controls.StackPanel> pai ao item que está selecionado no momento na seção da interface do usuário **Lista de Livros** (linha 82):  
  
```  
DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}"  
```  
  
 Ele usa a associação de dados bidirecional, para que os valores atuais dos elementos de livro são exibidos para e atualizados das duas caixas de texto nesse o painel. Associação de dados às propriedades dinâmicas são semelhantes ao usado no modelo de dados de `BookTemplate` :  
  
```  
Text="{Binding Path=Attribute[id].Value}"...Text="{Binding Path=Value}"  
```  
  
 A seção a mais recente de interface do usuário, **Adicionar Novo Livro**, não usa vinculação de dados no seu código XAML; em vez disso, esse código pode ser encontrado no seu código de manipulação de eventos no arquivo L2DBForm.xaml.cs.  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Descrição  
  
> [!NOTE]
>  Recomendamos que você copie o seguinte código abaixo em um editor de códigos, como o editor de código-fonte C# no Visual Studio, de modo que a linha números é mais fácil de controlar.  
  
### <a name="code"></a>Código  
  
```xml  
<Window x:Class="LinqToXmlDataBinding.L2XDBForm"  
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
    xmlns:system="clr-namespace:System;assembly=mscorlib"  
    xmlns:xlinq="clr-namespace:System.Xml.Linq;assembly=System.Xml.Linq"  
    xmlns:local="clr-namespace:LinqToXmlDataBinding"  
    Title="WPF Data Binding using LINQ-to-XML" Height="665" Width="500" ResizeMode="NoResize">  
  
    <Window.Resources>  
        <!-- Books provider and inline data -->  
        <ObjectDataProvider x:Key="LoadedBooks" ObjectType="{x:Type xlinq:XElement}" MethodName="Parse">  
            <ObjectDataProvider.MethodParameters>  
                <system:String xml:space="preserve">  
<![CDATA[  
<books xmlns="http://www.mybooks.com">  
  <book id="0">book zero</book>  
  <book id="1">book one</book>  
  <book id="2">book two</book>  
  <book id="3">book three</book>  
</books>  
]]>                  
                </system:String>  
                <xlinq:LoadOptions>PreserveWhitespace</xlinq:LoadOptions>  
            </ObjectDataProvider.MethodParameters>  
        </ObjectDataProvider>  
  
        <!-- Template for use in Books List listbox. -->  
        <DataTemplate x:Key="BookTemplate">  
            <StackPanel Orientation="Horizontal">  
                <TextBlock Margin="3" Text="{Binding Path=Attribute[id].Value}"/>  
                <TextBlock Margin="3" Text="-"/>  
                <TextBlock Margin="3" Text="{Binding Path=Value}"/>  
            </StackPanel>  
        </DataTemplate>  
    </Window.Resources>  
  
    <!-- Main visual content container -->  
    <StackPanel Background="lightblue" DataContext="{Binding Source={StaticResource LoadedBooks}}">  
        <!-- Raw XML display section -->  
        <DockPanel Margin="5">  
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">XML  
            <Label.LayoutTransform>  
                <RotateTransform Angle="90"/>  
            </Label.LayoutTransform>  
            </Label>  
            <TextBlock Name="tbRawXml" Height="200" Background="LightGray" Text="{Binding Path=Xml}" TextTrimming="CharacterEllipsis" />  
        </DockPanel>  
  
        <Separator Height="4" Margin="5" />  
  
        <!-- List box to display all books section -->  
        <DockPanel Margin="5">  
            <Label  Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" FontWeight="Bold">Book List  
                <Label.LayoutTransform>  
                    <RotateTransform Angle="90"/>  
                </Label.LayoutTransform>  
            </Label>  
            <ListBox Name="lbBooks" Height="200" Width="415" ItemTemplate ="{StaticResource BookTemplate}">  
                <ListBox.ItemsSource>  
                    <Binding Path="Elements[{http://www.mybooks.com}book]"/>  
                </ListBox.ItemsSource>  
            </ListBox>  
            <Button Margin="5" DockPanel.Dock="Right" Height="30" Width ="130" Content="Remove Selected Book" Click="OnRemoveBook">      
            <Button.LayoutTransform>  
                <RotateTransform Angle="90"/>  
            </Button.LayoutTransform>  
            </Button>  
        </DockPanel>  
  
        <Separator Height="4" Margin="5" />  
  
        <!-- Edit current selection section -->  
        <DockPanel Margin="5">  
            <TextBlock Margin="5" Height="30" Width="65" DockPanel.Dock="Right" Background="LightGray" TextWrapping="Wrap" TextAlignment="Center">  
                    Changes are live!  
                <TextBlock.LayoutTransform>  
                    <RotateTransform Angle="90"/>  
                </TextBlock.LayoutTransform>  
            </TextBlock>  
            <StackPanel>  
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Edit Selected Book</Label>      
                <StackPanel Margin="1" DataContext="{Binding ElementName=lbBooks, Path=SelectedItem}">  
                    <StackPanel Orientation="Horizontal">  
                        <Label Width="40">ID:</Label>  
                        <TextBox Name="editAttributeTextBox" Width="410" Text="{Binding Path=Attribute[id].Value}">  
                            <TextBox.ToolTip>  
                                <TextBlock FontWeight="Bold" TextAlignment="Center">  
                                    <Label>Edit the selected book ID and see it changed.</Label>  
                                </TextBlock>  
                            </TextBox.ToolTip>  
                        </TextBox>  
                    </StackPanel>  
                    <StackPanel Orientation="Horizontal">  
                        <Label Width="40">Value:</Label>  
                        <TextBox Name="editValueTextBox" Width="410" Text="{Binding Path=Value}" Height="25">  
                            <TextBox.ToolTip>  
                                <TextBlock FontWeight="Bold" TextAlignment="Center">  
                                    <Label>Edit the selected book Value and see it changed.</Label>  
                                </TextBlock>  
                            </TextBox.ToolTip>  
                        </TextBox>  
                    </StackPanel>  
                </StackPanel>  
            </StackPanel>  
        </DockPanel>  
  
        <Separator Height="4" Margin="5" />  
  
        <!-- Add new book section -->  
        <DockPanel Margin="5">  
            <Button Margin="5" Height="30" DockPanel.Dock="Right" Click ="OnAddBook">Add Book  
                <Button.LayoutTransform>  
                    <RotateTransform Angle="90"/>  
                </Button.LayoutTransform>  
            </Button>  
            <StackPanel>  
                <Label Width="450" Background="Gray" FontSize="12" BorderBrush="Black" BorderThickness="1" HorizontalAlignment="Left" FontWeight="Bold">Add New Book</Label>  
                <StackPanel Margin="1">  
                    <StackPanel Orientation="Horizontal">  
                        <Label Width="40">ID:</Label>  
                        <TextBox Name="tbAddID" Width="410">  
                            <TextBox.ToolTip>  
                                <TextBlock FontWeight="Bold" TextAlignment="Center">  
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>  
                                </TextBlock>  
                            </TextBox.ToolTip>  
                        </TextBox>  
                    </StackPanel>  
                    <StackPanel Orientation="Horizontal">  
                        <Label Width="40">Value:</Label>  
                        <TextBox Name="tbAddValue" Width="410" Height="25">  
                            <TextBox.ToolTip>  
                                <TextBlock FontWeight="UltraBold" TextAlignment="Center">  
                                    <Label>Enter a book ID and Value pair, then click Add Book.</Label>  
                                </TextBlock>  
                            </TextBox.ToolTip>  
                        </TextBox>  
                    </StackPanel>  
                </StackPanel>  
            </StackPanel>  
        </DockPanel>  
    </StackPanel>  
</Window>  
  
```  
  
### <a name="comments"></a>Comentários  
 Para o código-fonte de C# para os manipuladores de eventos associados com os elementos de interface do usuário WPF, consulte [Código-fonte de L2DBForm.xaml.cs](../designers/l2dbform-xaml-cs-source-code.md).  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: exemplo de LinqToXmlDataBinding](../designers/walkthrough-linqtoxmldatabinding-example.md)   
 [Código-fonte de L2DBForm.xaml.cs](../designers/l2dbform-xaml-cs-source-code.md)



