---
title: Usar dados de tempo de design com o Designer XAML em Visual Studio
description: Saiba como usar dados em tempo de design em XAML.
ms.date: 04/22/2021
ms.topic: overview
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: 47bf978bc32c651cb90130ecc90517bfe1c29cdd
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111761102"
---
# <a name="use-design-time-data-with-the-xaml-designer-in-visual-studio"></a>Usar dados de tempo de design com o Designer XAML em Visual Studio

Alguns layouts são difíceis de visualizar sem dados. Neste documento, revisaremos uma das abordagens que os desenvolvedores que trabalham em projetos da área de trabalho podem usar para simular dados no designer XAML. Essa abordagem é feita usando o namespace "d:" ignorável existente. Com essa abordagem, você pode adicionar rapidamente dados em tempo de design a suas páginas ou controles sem a necessidade de criar um ViewModel simulado completo ou apenas testar como uma alteração de propriedade pode afetar seu aplicativo sem se preocupar que essas alterações afetarão seus builds de versão. Todos os dados d: são usados apenas pelo Designer XAML e nenhum valor de namespace ignorável é compilado no aplicativo.

> [!NOTE]
> se você estiver usando o Xamarin.Forms, consulte Dados de tempo de design do [Xamarin.Forms](/xamarin/xamarin-forms/xaml/xaml-previewer/design-time-data)

## <a name="design-time-data-basics"></a>Noções básicas de dados de tempo de design

Os dados em tempo de design são dados simulados que você definiu para facilitar a visualização dos controles no Designer XAML. Para começar, adicione as seguintes linhas de código ao header do documento XAML se elas ainda não estão presentes:

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

Depois de adicionar os namespaces, você pode colocar na frente de qualquer atributo ou controle para exibi-lo somente no Designer XAML, mas não `d:` no runtime.

Por exemplo, você pode adicionar texto a um TextBlock que geralmente tem dados vinculados a ele.

```xml
<TextBlock Text="{Binding Name}" d:Text="Name!" />
```

[![Dados em tempo de design com texto em um TextBlock](media\xaml-design-time-textblock.png "Dados em tempo de design com texto um rótulo")](media\xaml-design-time-textblock.png#lightbox)

Neste exemplo, sem `d:Text` , o Designer XAML mostraria nada para o TextBlock. Em vez disso, ele mostra "Nome!" em que o TextBlock terá dados reais em runtime.

Você pode usar `d:` com atributos para qualquer controle UWP ou WPF .NET Core, como cores, tamanhos de fonte e espaçamento. Você pode até mesmo adicioná-lo ao próprio controle.

```xml
<d:Button Content="Design Time Button" />
```

[![Dados em tempo de design com um controle Button](media\xaml-design-time-button.png "Dados de tempo de design com um controle Button")](media\xaml-design-time-button.png#lightbox)

Neste exemplo, o botão só aparece em tempo de design. Use esse método para colocar um espaço reservado em para um controle personalizado ou para experimentar controles diferentes. Todos `d:` os atributos e controles serão ignorados durante o runtime.

## <a name="preview-images-at-design-time"></a>Visualizar imagens em tempo de design

Você pode definir uma Fonte em tempo de design para imagens que são vinculadas à página ou carregadas dinamicamente. Adicione a imagem que você deseja mostrar no Designer XAML ao seu projeto. Em seguida, você pode mostrar essa imagem no Designer XAML em tempo de design:

```xml
<Image Source={Binding ProfilePicture} d:Source="DesignTimePicture.jpg" />
```

> [!NOTE]
> A imagem neste exemplo deve existir na solução.

## <a name="design-time-data-for-listviews"></a>Dados em tempo de design para ListViews

ListViews são uma maneira popular de exibir dados em seu aplicativo da Área de Trabalho. No entanto, é difícil visualizar sem dados. Você pode usar esse recurso para criar um ItemSource ou Itens de dados em tempo de design em linha. O Designer XAML exibe o que está nessa matriz em seu ListView em tempo de design.

### <a name="wpf-net-core-example"></a>Exemplo de .NET Core do WPF
Para usar o tipo system:String, certifique-se de `xmlns:system="clr-namespace:System;assembly=mscorlib` incluir no seu header XAML.

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type system:String}">
                <system:String>Item One</system:String>
                <system:String>Item Two</system:String>
                <system:String>Item Three</system:String>
            </x:Array>
        </d:ListView.ItemsSource>
    <ListView.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding ItemName}" d:Text="{Binding .}" />
        </DataTemplate>
    </ListView.ItemTemplate>
   </ListView>
</StackPanel>
```

[![Dados em tempo de design com um ListView](media\xaml-design-time-listview-strings.png "Dados em tempo de design com um ListView")](media\xaml-design-time-listview-strings.png#lightbox)

Este exemplo anterior mostra um ListView com três TextBlocks no Designer XAML.

Você também pode criar uma matriz de objetos de dados. Por exemplo, as propriedades públicas de `City` um objeto de dados podem ser construídas como dados em tempo de design.

```csharp
namespace Cities.Models
{
    public class City
    {
        public string Name { get; set; }
        public string Country { get; set; }
    }
}
```

Para usar a classe em XAML, você deve importar o namespace no nó raiz.

```xaml
xmlns:models="clr-namespace:Cities.Models"
```

```xml
<StackPanel>
    <ListView ItemsSource="{Binding Items}">
        <d:ListView.ItemsSource>
            <x:Array Type="{x:Type models:City}">
                <models:City Name="Seattle" Country="United States"/>
                <models:City Name="London" Country="United Kingdom"/>
                <models:City Name="Panama City" Country="Panama"/>
            </x:Array>
        </d:ListView.ItemsSource>
        <ListView.ItemTemplate>
            <DataTemplate>
                 <StackPanel Orientation="Horizontal" >
                    <TextBlock Text="{Binding Name}" Margin="0,0,5,0" />
                    <TextBlock Text="{Binding Country}" />
                 </StackPanel>
            </DataTemplate>
        </ListView.ItemTemplate>
    </ListView>
</StackPanel>
```

[![Modelo real em dados de tempo de design com um ListView](media\xaml-design-time-listview-models.png "Dados reais em tempo de design do modelo com um ListView")](media\xaml-design-time-listview-models.png#lightbox)

O benefício aqui é que você pode vincular seus controles a uma versão estática em tempo de design do modelo.

### <a name="uwp-example"></a>Exemplo de UWP

Não há suporte para x:Array na UWP. Portanto, podemos usar `<d:ListView.Items>` em vez disso. Para usar o tipo system:String, certifique-se de `http://schemas.microsoft.com/winfx/2009/xaml` incluir no seu header XAML.

```xml
    <StackPanel>
        <ListView>
            <d:ListView.Items>
                <system:String>Item One</system:String>
                <system:String>Item Two</system:String>
                <system:String>Item Three</system:String>
            </d:ListView.Items>
        </ListView>
    </StackPanel>
```

## <a name="use-design-time-data-with-custom-types-and-properties"></a>Usar dados em tempo de design com tipos e propriedades personalizados

Por padrão, esse recurso funciona apenas com controles de plataforma e propriedades. Nesta seção, vamos sobre as etapas necessárias para permitir que você use seus próprios controles personalizados como controles de tempo de design, uma nova funcionalidade disponível para clientes que usam o Visual Studio 2019 versão [16.8](/visualstudio/releases/2019/release-notes/) ou posterior. Há três requisitos para habilitar isso:

- Um namespace xmlns personalizado

    ```xml
    xmlns:myControls="http://MyCustomControls"
    ```

- Uma versão em tempo de design do namespace. Isso pode ser feito simplesmente pela adoção de /design no final.

     ```xml
    xmlns:myDesignTimeControls="http://MyCustomControls/design"
    ```

- Adicionando seu prefixo de tempo de design ao mc:Ignorable

    ```xml
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d myDesignTimeControls"
    ```

Depois de seguir todas essas etapas, você pode usar seu `myDesignTimeControls` prefixo para criar seus controles de tempo de design.

```xml
<myDesignTimeControls:MyButton>I am a design time Button</myDesignTimeControls:MyButton>
```

### <a name="creating-a-custom-xmlns-namespace"></a>Criando um namespace xmlns personalizado

Para criar um namespace xmlns personalizado no WPF .NET Core, você precisa mapear seu namespace XML personalizado para o namespace CLR em que seus controles estão. Você pode fazer isso adicionando o `XmlnsDefinition` atributo de nível de assembly em seu `AssemblyInfo.cs` arquivo. O arquivo é encontrado na hierarquia raiz do seu projeto.

   ```C#
[assembly: XmlnsDefinition("http://MyCustomControls", "MyViews.MyButtons")]
   ```

## <a name="troubleshooting"></a>Solução de problemas

Se você tiver um problema que não está listado nesta seção, informe-nos usando [a ferramenta Relatar um](../ide/how-to-report-a-problem-with-visual-studio.md) Problema.

### <a name="requirements"></a>Requisitos

- Os dados em tempo de design Visual Studio versão [16.7](/visualstudio/releases/2019/release-notes-v16.7) ou posterior de 2019.

- Dá suporte a projetos da área de trabalho do Windows Windows Presentation Foundation WPF para .NET Core e UWP. Esse recurso também está disponível para .NET Framework no canal [de visualização](/visualstudio/releases/2019/release-notes-preview). Para habilita-lo, acesse **Ferramentas** Opções Recursos de Visualização do Ambiente , selecione Novo Designer XAML WPF para .NET Framework e, em seguida,  >    >    >  reinicie Visual Studio. 

- A partir do Visual Studio 2019 versão 16.7, esse recurso funciona com todos os controles in-the-box das estruturas WPF e UWP. O suporte para controles de terceiros agora está disponível na [versão 16.8](/visualstudio/releases/2019/release-notes/).

### <a name="the-xaml-designer-stopped-working"></a>O Designer XAML parou de funcionar

Tente fechar e reabrir o arquivo XAML e limpar e recriar seu projeto.

## <a name="see-also"></a>Confira também

- [Dados de tempo de design com o Visualizador do Xamarin.Forms](/xamarin/xamarin-forms/xaml/xaml-Designer/design-time-data/)
- [XAML em aplicativos WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [XAML em aplicativos UWP](/windows/uwp/xaml-platform/xaml-overview)
- [XAML em aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)