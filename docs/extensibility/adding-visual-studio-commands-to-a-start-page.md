---
title: Adicionando comandos do Visual Studio a uma página inicial | Microsoft Docs
description: Saiba mais sobre as diferentes maneiras de associar comandos do Visual Studio a objetos XAML em uma página inicial personalizada no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: 4e2ec238d3cb8c2e7d843018fc45e97207c6d5f4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097520"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>Adicionar comandos do Visual Studio a uma página inicial

Ao criar uma página inicial personalizada, você pode adicionar comandos do Visual Studio a ela. Este documento discute as diferentes maneiras de associar comandos do Visual Studio a objetos XAML em uma página inicial.

Para obter mais informações sobre comandos em XAML, consulte [visão geral](/dotnet/framework/wpf/advanced/commanding-overview) de comandos

## <a name="add-commands-from-the-command-well"></a>Adicionar comandos do bem-sucommand

A página inicial criada em [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md) adicionou os <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> namespaces e, da seguinte maneira.

```xml
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

Adicione outro namespace para Microsoft. VisualStudio. Shell a partir do assembly *Microsoft.VisualStudio.Shell.Immutable.11.0.dll*. (Talvez seja necessário adicionar uma referência a esse assembly em seu projeto.)

```xml
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"
```

Você pode usar o `vscom:` alias para associar comandos do Visual Studio a controles XAML na página definindo a <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> Propriedade do controle como `vscom:VSCommands.ExecuteCommand` . Em seguida, você pode definir a <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> propriedade como o nome do comando a ser executado, conforme mostrado no exemplo a seguir.

```xml
<Button Name="btnNewProj" Content="New Project"
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"
    CommandParameter="File.NewProject" >
</Button>
```

> [!NOTE]
> O `x:` alias, que se refere ao esquema XAML, é necessário no início de todos os comandos.

 Você pode definir o valor da `Command` propriedade para qualquer comando que possa ser acessado na janela de **comando** . Para obter uma lista de comandos disponíveis, consulte [aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

 Se o comando a ser adicionado exigir um parâmetro adicional, você poderá adicioná-lo ao valor da `CommandParameter` propriedade. Separe os parâmetros dos comandos usando espaços, conforme mostrado no exemplo a seguir.

```xml
<Button Content="Web Search"
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"
        CommandParameter="View.WebBrowser www.bing.com" />
```

### <a name="call-extensions-from-the-command-well"></a>Chamar extensões do comando
 Você pode chamar comandos de VSPackages registrados usando a mesma sintaxe usada para chamar outros comandos do Visual Studio. Por exemplo, se um VSPackage instalado Adicionar um comando **Home Page** ao menu **Exibir** , você poderá chamar esse comando definindo `CommandParameter` como `View.HomePage` .

> [!NOTE]
> Se você chamar um comando associado a um VSPackage, o pacote deverá ser carregado quando o comando for invocado.

## <a name="add-commands-from-assemblies"></a>Adicionar comandos de assemblies
 Para chamar um comando de um assembly ou para acessar o código em um VSPackage que não está associado a um comando de menu, você deve criar um alias para o assembly e, em seguida, chamar o alias.

### <a name="to-call-a-command-from-an-assembly"></a>Para chamar um comando de um assembly

1. Em sua solução, adicione uma referência ao assembly.

2. Na parte superior do arquivo *Startpage. XAML* , adicione uma diretiva de namespace para o assembly, conforme mostrado no exemplo a seguir.

    ```xml
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"
    ```

3. Invoque o comando definindo a `Command` propriedade de um objeto XAML, conforme mostrado no exemplo a seguir.

     XAML

    ```
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>
    ```

> [!NOTE]
> Você deve copiar seu assembly e, em seguida, colá-lo em *.. \\ {Pasta de instalação do Visual Studio} \Common7\IDE\PrivateAssemblies \* para certificar-se de que ela está carregada antes de ser chamada.

## <a name="add-commands-with-the-dte-object"></a>Adicionar comandos com o objeto DTE
 Você pode acessar o objeto DTE a partir de uma página inicial, tanto na marcação quanto no código.

 Na marcação, você pode acessá-lo usando a sintaxe de [extensão de marcação de associação](/dotnet/framework/wpf/advanced/binding-markup-extension) para chamar o <xref:EnvDTE.DTE> objeto. Você pode usar essa abordagem para associar propriedades simples, como aquelas que retornam coleções, mas não é possível associar a métodos ou serviços. O exemplo a seguir mostra um <xref:System.Windows.Controls.TextBlock> controle que é associado à <xref:EnvDTE._DTE.Name%2A> propriedade e um <xref:System.Windows.Controls.ListBox> controle que enumera as <xref:EnvDTE.Window.Caption%2A> Propriedades da coleção que é retornada pela <xref:EnvDTE._DTE.Windows%2A> propriedade.

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

 Para obter um exemplo, consulte [Walkthrough: salvar as configurações do usuário em uma página inicial](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md).

## <a name="see-also"></a>Confira também

- [Adicionando controle de usuário à página inicial](../extensibility/adding-user-control-to-the-start-page.md)
