---
title: Adicionando comandos do Visual Studio para uma página inicial | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 22ae9ebb5e9acb3fa1787f2af3b0fbb159c1485d
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39153625"
---
# <a name="add-visual-studio-commands-to-a-start-page"></a>Adicionar comandos do Visual Studio para uma página inicial
Quando você cria uma página inicial personalizada, você pode adicionar comandos do Visual Studio a ele. Este documento discute as diferentes maneiras de associar comandos do Visual Studio a objetos XAML em uma página inicial.  
  
 Para obter mais informações sobre os comandos no XAML, consulte [Commanding overview](/dotnet/framework/wpf/advanced/commanding-overview)  
  
## <a name="add-commands-from-the-command-well"></a>Adicionar comandos do comando também  
 A página de início é criado na [criar uma página inicial personalizada](../extensibility/creating-a-custom-start-page.md) adicionado a <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> e <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> namespaces, da seguinte maneira.  
  
```  
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
```  
  
 Adicionar outro namespace para Microsoft.VisualStudio.Shell do assembly *Microsoft.VisualStudio.Shell.Immutable.11.0.dll*. (Talvez seja necessário adicionar uma referência a esse assembly em seu projeto.)  
  
```xml  
xmlns:vscom="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.Immutable.11.0"  
```  
  
 Você pode usar o `vscom:` alias para associar os comandos do Visual Studio ao XAML controles da página, definindo o <xref:System.Windows.Controls.Primitives.ButtonBase.Command%2A> propriedade do controle para `vscom:VSCommands.ExecuteCommand`. Você pode definir o <xref:System.Windows.Controls.Primitives.ButtonBase.CommandParameter%2A> propriedade para o nome do comando ser executado, conforme mostrado no exemplo a seguir.  
  
```xml  
<Button Name="btnNewProj" Content="New Project"   
    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
    CommandParameter="File.NewProject" >  
</Button>  
```  
  
> [!NOTE]
>  O `x:` alias que se refere ao esquema de XAML, é necessário no início de todos os comandos.  
  
 Você pode definir o valor da `Command` propriedade para qualquer comando que pode ser acessado do **comando** janela. Para obter uma lista dos comandos disponíveis, consulte [aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).  
  
 Se o comando Adicionar requer um parâmetro adicional, você pode adicioná-lo ao valor da `CommandParameter` propriedade. Parâmetros separados de comandos usando espaços, conforme mostrado no exemplo a seguir.  
  
```xml  
<Button Content="Web Search"   
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
        CommandParameter="View.WebBrowser www.bing.com" />  
```  
  
### <a name="call-extensions-from-the-command-well"></a>Chame as extensões do comando também  
 Você pode chamar comandos de VSPackages registrados usando a mesma sintaxe que é usada para chamar outros comandos do Visual Studio. Por exemplo, se um VSPackage instalado adiciona uma **Home Page** comando para o **exibição** menu, você pode chamar esse comando, definindo `CommandParameter` para `View.HomePage`.  
  
> [!NOTE]
>  Se você chamar um comando que está associado um VSPackage, o pacote deve ser carregado quando o comando é invocado.  
  
## <a name="add-commands-from-assemblies"></a>Adicionar comandos de assemblies  
 Para chamar um comando de um assembly, ou código de acesso em um VSPackage que não está associado um comando de menu, você deve criar um alias para o assembly e, em seguida, chame o alias.  
  
### <a name="to-call-a-command-from-an-assembly"></a>Para chamar um comando de um assembly  
  
1.  Em sua solução, adicione uma referência ao assembly.  
  
2.  Na parte superior do *StartPage* de arquivo, adicione uma diretiva de namespace para o assembly, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
    ```  
  
3.  Invocar o comando, definindo o `Command` propriedade de um objeto XAML, conforme mostrado no exemplo a seguir.  
  
     XAML  
  
    ```  
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>  
    ```  
  
> [!NOTE]
>  Você deve copiar o assembly e, em seguida, cole-o no *... \\{Pasta de instalação do visual Studio} \Common7\IDE\PrivateAssemblies\* para garantir que ele é carregado antes que ele é chamado.  
  
## <a name="add-commands-with-the-dte-object"></a>Adicionar comandos com o objeto DTE  
 Você pode acessar o objeto DTE de uma página inicial, na marcação e no código.  
  
 Na marcação, você pode acessá-lo usando o [extensão de marcação Binding](/dotnet/framework/wpf/advanced/binding-markup-extension) sintaxe para chamar o <xref:EnvDTE.DTE> objeto. Você pode usar essa abordagem para associar a propriedades simples, como aqueles que retornam coleções, mas você não pode associar a métodos ou serviços. A exemplo a seguir mostra um <xref:System.Windows.Controls.TextBlock> controle que está associado a <xref:EnvDTE._DTE.Name%2A> propriedade e um <xref:System.Windows.Controls.ListBox> controle que enumera os <xref:EnvDTE.Window.Caption%2A> propriedades da coleção que é retornado pelo <xref:EnvDTE._DTE.Windows%2A> propriedade.  
  
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
  
 Por exemplo, consulte [instruções passo a passo: salvando as configurações do usuário em uma página Iniciar](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionando o controle de usuário para a página de início](../extensibility/adding-user-control-to-the-start-page.md)