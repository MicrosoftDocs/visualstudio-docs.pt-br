---
title: Usar dados de tempo de design com o Designer XAML no Visual Studio
description: Saiba como usar dados de tempo de design em XAML.
ms.date: 11/17/2020
ms.topic: overview
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: vs-2019
ms.openlocfilehash: 915fe38da63f0b3994a809b20515fdc18e0790ce
ms.sourcegitcommit: 5fb684ff8729eb118aa91ce9f049c79eeb9747b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2021
ms.locfileid: "107913066"
---
# <a name="use-design-time-data-with-the-xaml-designer-in-visual-studio"></a>Usar dados de tempo de design com o Designer XAML no Visual Studio

Alguns layouts são difíceis de Visualizar sem dados. Neste documento, vamos revisar uma das abordagens que os desenvolvedores que trabalham em projetos de desktop podem usar para simular dados no designer XAML. Essa abordagem é feita usando o namespace "d:" ignorável existente. Com essa abordagem, você pode adicionar rapidamente dados de tempo de design a suas páginas ou controles sem a necessidade de criar um ViewModel de simulação completo ou apenas testar como uma alteração de propriedade pode afetar seu aplicativo sem se preocupar que essas alterações afetarão suas compilações de versão. Todos os dados d: são usados somente pelo Designer XAML e nenhum valor de namespace ignorável é compilado no aplicativo.

> [!NOTE]
> Se você estiver usando o Xamarin. Forms, consulte [dados de tempo de design do xamarin. Forms](/xamarin/xamarin-forms/xaml/xaml-previewer/design-time-data)

## <a name="design-time-data-basics"></a>Noções básicas de dados de tempo de design

Os dados de tempo de design são dados fictícios que você define para facilitar a visualização dos seus controles no Designer XAML. Para começar, adicione as seguintes linhas de código ao cabeçalho do seu documento XAML se elas ainda não estiverem presentes:

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

Depois de adicionar os namespaces, você pode colocar `d:` na frente de qualquer atributo ou controle para mostrá-lo somente na Designer XAML, mas não em tempo de execução.

Por exemplo, você pode adicionar texto a um TextBlock que geralmente tem dados associados a ele.

```xml
<TextBlock Text="{Binding Name}" d:Text="Name!" />
```

[![Dados de tempo de design com texto em um TextBlock](media\xaml-design-time-textblock.png "Dados de tempo de design com um rótulo de texto")](media\xaml-design-time-textblock.png#lightbox)

Neste exemplo, sem `d:Text` , o designer XAML não mostraria nada para o TextBlock. Em vez disso, ele mostra "Name!" onde o TextBlock terá dados reais em tempo de execução.

Você pode usar `d:` com atributos para qualquer controle do .NET Core UWP ou do WPF, como cores, tamanhos de fonte e espaçamento. Você pode até mesmo adicioná-lo ao próprio controle.

```xml
<d:Button Content="Design Time Button" />
```

[![Dados de tempo de design com um controle de botão](media\xaml-design-time-button.png "Dados de tempo de design com um controle de botão")](media\xaml-design-time-button.png#lightbox)

Neste exemplo, o botão só aparece em tempo de design. Use este método para colocar um espaço reservado no para um controle personalizado ou para testar diferentes controles. Todos os `d:` atributos e controles serão ignorados durante o tempo de execução.

## <a name="preview-images-at-design-time"></a>Visualizar imagens em tempo de design

Você pode definir uma fonte de tempo de design para imagens vinculadas à página ou carregadas dinamicamente. Adicione a imagem que você deseja mostrar no Designer XAML ao seu projeto. Em seguida, você pode mostrar essa imagem no Designer XAML em tempo de design:

```xml
<Image Source={Binding ProfilePicture} d:Source="DesignTimePicture.jpg" />
```

> [!NOTE]
> A imagem neste exemplo deve existir na solução.

## <a name="design-time-data-for-listviews"></a>Dados de tempo de design para ListViews

ListViews são uma maneira popular de exibir dados em seu aplicativo de área de trabalho. No entanto, é difícil Visualizar sem nenhum dado. Você pode usar esse recurso para criar uma fonte de dados de tempo de design embutida ou itens. O Designer XAML exibe o que está nessa matriz em seu ListView em tempo de design.

### <a name="wpf-net-core--example"></a>Exemplo do WPF .NET Core
Para usar o tipo System: String, certifique-se `xmlns:system="clr-namespace:System;assembly=mscorlib` de incluir no seu cabeçalho XAML.

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

[![Dados de tempo de design com um ListView](media\xaml-design-time-listview-strings.png "Dados de tempo de design com um ListView")](media\xaml-design-time-listview-strings.png#lightbox)

Este exemplo anterior mostra um ListView com três TextBlocks no Designer XAML.

Você também pode criar uma matriz de objetos de dados. Por exemplo, as propriedades públicas de um `City` objeto de dados podem ser construídas como dados de tempo de design.

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

[![Modelo real em dados de tempo de design com um ListView](media\xaml-design-time-listview-models.png "Dados reais de tempo de design de modelo com um ListView")](media\xaml-design-time-listview-models.png#lightbox)

O benefício aqui é que você pode associar seus controles a uma versão estática de tempo de design de seu modelo.

### <a name="uwp-example"></a>Exemplo de UWP 

Não há suporte para x:Array no UWP. Portanto, podemos usar `<d:ListView.Items>` em vez disso. Para usar o tipo System: String, certifique-se `http://schemas.microsoft.com/winfx/2009/xaml` de incluir no seu cabeçalho XAML.

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

## <a name="use-design-time-data-with-custom-types-and-properties"></a>Usar dados de tempo de design com tipos e propriedades personalizados

Por padrão, esse recurso funciona apenas com controles de plataforma e propriedades. Nesta seção, abordaremos as etapas necessárias para permitir que você use seus próprios controles personalizados como controles em tempo de design, um novo recurso disponível para os clientes que usam o Visual Studio 2019 versão [16,8](/visualstudio/releases/2019/release-notes/) ou posterior. Há três requisitos para habilitar isso:

- Um namespace xmlns personalizado

    ```xml
    xmlns:myControls="http://MyCustomControls"
    ```

- Uma versão de tempo de design do seu namespace. Isso pode ser obtido simplesmente acrescentando/design ao final.

     ```xml
    xmlns:myDesignTimeControls="http://MyCustomControls/design"
    ```

- Adicionando seu prefixo de tempo de design para o MC: Ignorable

    ```xml
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d myDesignTimeControls"
    ```

Depois de executar todas essas etapas, você pode usar seu `myDesignTimeControls` prefixo para criar seus controles de tempo de design.

```xml
<myDesignTimeControls:MyButton>I am a design time Button</myDesignTimeControls:MyButton>
```

### <a name="creating-a-custom-xmlns-namespace"></a>Criando um namespace xmlns personalizado

Para criar um namespace xmlns personalizado no WPF .NET Core, você precisa mapear seu namespace XML personalizado para o namespace CLR em que os controles estão. Você pode fazer isso adicionando o `XmlnsDefinition` atributo de nível de assembly em seu `AssemblyInfo.cs` arquivo. O arquivo é encontrado na hierarquia raiz do seu projeto.

   ```C#
[assembly: XmlnsDefinition("http://MyCustomControls", "MyViews.MyButtons")]
   ```

## <a name="troubleshooting"></a>Solução de problemas

Se você tiver um problema que não esteja listado nesta seção, informe-nos usando o [relatório uma ferramenta problemática](../ide/how-to-report-a-problem-with-visual-studio.md) .

### <a name="requirements"></a>Requisitos

- Os dados de tempo de design exigem o Visual Studio 2019 versão [16,7](/visualstudio/releases/2019/release-notes-v16.7) ou posterior.

- Dá suporte a projetos de área de trabalho do Windows que se destinam a Windows Presentation Foundation (WPF) para .NET Core e UWP. Esse recurso também está disponível para .NET Framework no [canal de visualização](/visualstudio/releases/2019/release-notes-preview). Para habilitá-lo, vá para **ferramentas**  >  **Opções**  >    >  **recursos de visualização** do ambiente, selecione **novo designer XAML do WPF para .NET Framework** e reinicie o Visual Studio.

- A partir do Visual Studio 2019 versão 16,7, esse recurso funciona com todos os controles prontos do WPF e das estruturas UWP. O suporte para controles de terceiros agora está disponível na [versão 16,8](/visualstudio/releases/2019/release-notes/).

### <a name="the-xaml-designer-stopped-working"></a>O Designer XAML parou de funcionar

Tente fechar e reabrir o arquivo XAML e limpar e recompilar seu projeto.

## <a name="see-also"></a>Confira também

- [Dados de tempo de design com o webviewer Xamarin. Forms](/xamarin/xamarin-forms/xaml/xaml-Designer/design-time-data/)
- [XAML em aplicativos WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [XAML em aplicativos UWP](/windows/uwp/xaml-platform/xaml-overview)
- [XAML em aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)