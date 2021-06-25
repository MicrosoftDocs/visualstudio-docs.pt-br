---
title: Adicionando Visual Studio comandos a uma página inicial | Microsoft Docs
description: Saiba mais sobre as diferentes maneiras de Visual Studio comandos a objetos XAML em uma Página Inicial personalizada Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 0bf0f9a3db21dd93b1a497731bca9142a4377acc
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901507"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>Adicionar Visual Studio comandos a uma página inicial

Ao criar uma Página Inicial personalizada, você pode adicionar Visual Studio comandos a ela. Este documento discute as diferentes maneiras de Visual Studio comandos a objetos XAML em uma Página Inicial.

Para obter mais informações sobre comandos em XAML, consulte Visão geral [dos comandos](/dotnet/framework/wpf/advanced/commanding-overview)

## <a name="add-commands-from-the-command-well"></a>Adicionar comandos do comando bem

A Página Inicial criada em [Criar uma Página Inicial personalizada](../extensibility/creating-a-custom-start-page.md) adicionou os <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> namespaces e , da seguinte forma.

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

Adicione outro namespace para Microsoft.VisualStudio.Shell do assembly *Microsoft.VisualStudio.Shell.Immutable.11.0.dll*. (Talvez seja necessário adicionar uma referência a esse assembly em seu projeto.)

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

Você pode usar o alias para Visual Studio comandos a controles XAML na página definindo a propriedade `vscom:` <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> do controle como `vscom:VSCommands.ExecuteCommand` . Em seguida, você pode definir <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> a propriedade como o nome do comando a ser executado, conforme mostrado no exemplo a seguir.

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> O `x:` alias, que se refere ao esquema XAML, é necessário no início de todos os comandos.

 Você pode definir o valor da propriedade `Command` para qualquer comando que possa ser acessado na janela **Comando.** Para ver uma lista de comandos disponíveis, consulte [Visual Studio aliases de comando](../ide/reference/visual-studio-command-aliases.md).

 Se o comando a ser adicionar exigir um parâmetro adicional, você poderá adicioná-lo ao valor da `CommandParameter` propriedade . Separe parâmetros de comandos usando espaços, conforme mostrado no exemplo a seguir.

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>Chamar extensões da área de comando
 Você pode chamar comandos de VSPackages registrados usando a mesma sintaxe usada para chamar outros Visual Studio comandos. Por exemplo, se um VSPackage instalado adiciona um comando home **page** ao **menu** Exibir, você pode chamar esse comando definindo como `CommandParameter` `View.HomePage` .

> [!NOTE]
> Se você chamar um comando associado a um VSPackage, o pacote deverá ser carregado quando o comando for invocado.

## <a name="add-commands-from-assemblies"></a>Adicionar comandos de assemblies
 Para chamar um comando de um assembly ou para acessar o código em um VSPackage que não está associado a um comando de menu, você deve criar um alias para o assembly e, em seguida, chamar o alias.

### <a name="to-call-a-command-from-an-assembly"></a>Para chamar um comando de um assembly

1. Em sua solução, adicione uma referência ao assembly.

2. Na parte superior do arquivo *StartPage.xaml,* adicione uma diretiva de namespace para o assembly, conforme mostrado no exemplo a seguir.

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. Invoque o comando definindo `Command` a propriedade de um objeto XAML, conforme mostrado no exemplo a seguir.

     Xaml

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> Você deve copiar o assembly e, em seguida, colar em *.. \\ {Visual Studio pasta de instalação}\Common7\IDE\PrivateAssemblies para garantir que ele seja \* carregado antes de ser chamado.

## <a name="add-commands-with-the-dte-object"></a>Adicionar comandos com o objeto DTE
 Você pode acessar o objeto DTE de uma Página Inicial, tanto na marcação quanto no código.

 Na marcação, você pode acessá-lo usando a sintaxe de Extensão de [Marcação de](/dotnet/framework/wpf/advanced/binding-markup-extension) Associação para chamar o <xref:EnvDTE.DTE> objeto . Você pode usar essa abordagem para se vincular a propriedades simples, como aquelas que retornam coleções, mas não pode se vincular a métodos ou serviços. O exemplo a seguir mostra um controle que se vincula à propriedade e um controle que enumera as propriedades da coleção <xref:System.Windows.Controls.TextBlock> <xref:EnvDTE._DTE.Name%2A> <xref:System.Windows.Controls.ListBox> <xref:EnvDTE.Window.Caption%2A> retornada pela <xref:EnvDTE._DTE.Windows%2A> propriedade .

```xml
<TextBlock Text="{Binding Path=DTE.Name}" FontSize="12" HorizontalAlignment="Center"/>
<ListBox ItemsSource="{Binding Path=DTE.Windows}">
    <ListBox.ItemTemplate>
        <DataTemplate>
            <TextBlock Text="{Binding Path=Caption}"/>
        </DataTemplate>
    </ListBox.ItemTemplate>
</ListBox
```

 Para ver um exemplo, consulte [Passo a passo: salvando as configurações do usuário em uma página inicial.](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)

## <a name="see-also"></a>Confira também

- [Adicionando o controle de usuário à Página Inicial](../extensibility/adding-user-control-to-the-start-page.md)
