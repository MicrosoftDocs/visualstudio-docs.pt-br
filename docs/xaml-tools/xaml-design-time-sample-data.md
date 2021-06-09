---
title: Usar dados de exemplo de tempo de design com o Designer XAML em Visual Studio
description: Saiba como usar dados de exemplo em tempo de design em XAML.
ms.date: 06/01/2021
ms.topic: conceptual
author: alihamie
ms.author: tglee
manager: jmartens
monikerRange: '>=vs-2019'
ms.openlocfilehash: 66418d351280a0c067327716766725d22488131b
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760907"
---
# <a name="use-design-time-sample-data-with-the-xaml-designer-in-visual-studio"></a>Usar dados de exemplo de tempo de design com o Designer XAML em Visual Studio

Alguns controles dependentes de dados, como ListView, ListBox ou DataGrid, são difíceis de visualizar sem dados. Neste documento, vamos analisar uma nova abordagem que permite aos desenvolvedores trabalharem em projetos **WPF .NET Core** ou projetos **WPF .NET Framework** com o novo designer para habilitar dados de exemplo nesses controles. 

## <a name="sample-data-feature-basics"></a>Noções básicas do recurso de dados de exemplo

Os dados de exemplo são apenas para visualização em tempo de design, o que significa que eles aparecem apenas no designer XAML, não no aplicativo em execução. Assim, ele é aplicado à versão em tempo de design da propriedade ItemsSource `d:ItemsSource` . Dados de exemplo precisam que o namespace de tempo de design funcione. Para começar, adicione as seguintes linhas de código ao header do documento XAML se elas ainda não estão presentes:

> [!NOTE]
> Visite [propriedades de tempo de design XAML](../xaml-tools/xaml-designtime-data.md) para saber mais sobre as propriedades de tempo de design em XAML.

```xml
xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
mc:Ignorable="d"
```

Depois de adicionar os namespaces, você pode usar para habilitar dados de exemplo em `d:ItemsSource="{d:SampleData}"` ListView, Listbox ou DataGrid. Por exemplo:

```xml
<DataGrid d:ItemsSource="{d:SampleData}"/>
```

[![Dados de exemplo com DataGrid](media\xaml-sample-data-empty-datagrid.png "Dados de exemplo habilitados em um DataGrid")](media\xaml-sample-data-empty-datagrid.png#lightbox)

Neste exemplo, sem `d:ItemsSource="{d:SampleData}"` o Designer XAML mostraria um DataGrid vazio. Em vez disso, `d:SampleData` com ele agora mostra os dados de exemplo padrão gerados.

Por padrão, você obterá 5 itens exibidos. No entanto, você pode usar a **propriedade ItemCount** para especificar quantos itens você gostaria de exibir. por exemplo: `d:ItemsSource="{d:SampleData ItemCount=2}"`

## <a name="sample-data-works-with-datatemplates"></a>Os dados de exemplo funcionam com datatemplates

Os Dados de Exemplo funcionam para controles ListBox, ListView ou DataGrid quando você usa modelos de dados. O recurso Dados de Exemplo analisará o DataTemplate e tentará gerar os dados apropriados para ele. Dados de exemplo serão gerados apenas para elementos em DataTemplates que usam associação. Os dados de exemplo serão gerados mesmo que as vinculações ainda não tenham uma origem.
Por exemplo:

```xml
<ListView d:ItemsSource="{d:SampleData ItemCount=3}">
     <ListView.ItemTemplate>
        <DataTemplate>
            <StackPanel Orientation="Horizontal">
                <Image Width="50" Source="{Binding ProfilePicture}"/>
                <StackPanel Orientation="Vertical">
                    <TextBlock Text="{Binding FirstName}" Margin="5"/>
                    <Label Content="{Binding LastName}"/>
                </StackPanel>
            </StackPanel>
        </DataTemplate>
    </ListView.ItemTemplate>
</ListView>
```

[![ListView de dados de exemplo com um DataTemplate](media\xaml-sample-data-templated-listview.png "Dados de exemplo usados em um ListView com um DataTemplate")](media\xaml-sample-data-templated-listview.png#lightbox)

## <a name="enable-sample-data-with-suggested-actions"></a>Habilitar dados de exemplo com ações sugeridas

Para habilitar ou desabilitar facilmente dados de exemplo para um controle do designer, você pode usar o recurso Ações Sugeridas. Ações sugeridas é uma lâmpada no designer que aparece no canto superior direito quando você seleciona um controle. Você pode habilitar Dados de Exemplo selecionando seu controle, clicando na lâmpada e, em seguida, clicando em `Show Sample Data` . Por exemplo:

[![Exemplo de ações sugeridas de dados](media\xaml-sample-data-suggested-actions.png "Habilitar dados de exemplo com ações sugeridas")](media\xaml-sample-data-suggested-actions.png#lightbox)

## <a name="sample-data-with-ivalueconverters"></a>Dados de exemplo com IValueConverters 

Conversores não são totalmente suportados pelo recurso Dados de Exemplo. No entanto, você pode fazê-lo funcionar fazendo um ou ambos os seguintes:
- Certifique-se de que `Convert` sua função possa lidar com um cenário em que o valor já seja seu targetType.

- Implemente `ConvertBack` a função que converterá seu valor de volta no tipo original. 

## <a name="troubleshooting"></a>Solução de problemas

Se os Dados de Exemplo não mostrarem nada ou não mostrarem o tipo correto, você poderá tentar atualizar o designer ou fechar e abrir novamente a página.

Se você tiver um problema que não está listado nesta seção ou não puder ser corrigido atualize a página, informe-nos usando a ferramenta Relatar [um](../ide/how-to-report-a-problem-with-visual-studio.md) Problema.

### <a name="requirements"></a>Requisitos

- Os Dados de Exemplo Visual Studio versão 2019 [16.10](/visualstudio/releases/2019/release-notes-v16.10) ou posterior.

- Dá suporte a projetos da área de trabalho do Windows Windows Presentation Foundation WPF para .NET Core ou .NET Framework ao usar o novo designer. Para habilitar o novo designer para .NET Framework acesse Ferramentas > Opções > Recursos de Versão Prévia do Ambiente >, selecione Novo Designer XAML WPF para .NET Framework e reinicie Visual Studio.

## <a name="see-also"></a>Confira também

- [Propriedades de tempo de design XAML](../xaml-tools/xaml-designtime-data.md)
- [XAML em aplicativos WPF](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [XAML em aplicativos UWP](/windows/uwp/xaml-platform/xaml-overview)
- [XAML em aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)