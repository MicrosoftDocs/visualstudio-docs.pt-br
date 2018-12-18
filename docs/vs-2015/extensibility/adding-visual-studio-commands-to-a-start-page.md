---
title: Adicionando comandos do Visual Studio para uma página inicial | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- start page commands
- vs:VSCommands
ms.assetid: a8e2765c-cfb5-47b5-a414-6e48b434e0c2
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6a5a0e205d04fb219d000dd87e97735cdfd26162
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51748753"
---
# <a name="adding-visual-studio-commands-to-a-start-page"></a>Adicionando comandos do Visual Studio a uma página inicial
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você cria uma página inicial personalizada, você pode adicionar comandos do Visual Studio a ele. Este documento discute as diferentes maneiras de associar comandos do Visual Studio a objetos XAML em uma página de início.  
  
 Para obter mais informações sobre os comandos no XAML, consulte [visão geral dos comandos](http://msdn.microsoft.com/library/bc208dfe-367d-426a-99de-52b7e7511e81)  
  
## <a name="adding-commands-from-the-command-well"></a>Adição dos comandos do comando também  
 A página inicial criado na [criando uma página de início personalizada](../extensibility/creating-a-custom-start-page.md) adicionado a <xref:Microsoft.VisualStudio.PlatformUI?displayProperty=fullName> e <xref:Microsoft.VisualStudio.Shell?displayProperty=fullName> namespaces, da seguinte maneira.  
  
```  
xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"  
```  
  
 Adicione outro namespace para Microsoft.VisualStudio.Shell do assembly Microsoft.VisualStudio.Shell.Immutable.11.0.dll. (Talvez seja necessário adicionar uma referência a esse assembly em seu projeto.)  
  
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
  
 Você pode definir o valor da `Command` propriedade para qualquer comando que pode ser acessado do **comando** janela. Para obter uma lista dos comandos disponíveis, consulte [Aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).  
  
 Se o comando Adicionar requer um parâmetro adicional, você pode adicioná-lo ao valor da `CommandParameter` propriedade. Parâmetros separados de comandos usando espaços, conforme mostrado no exemplo a seguir.  
  
```xml  
<Button Content="Web Search"   
        Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
        CommandParameter="View.WebBrowser www.bing.com" />  
```  
  
### <a name="calling-extensions-from-the-command-well"></a>Extensões de chamada do comando também  
 Você pode chamar comandos de VSPackages registrados usando a mesma sintaxe que é usada para chamar outros comandos do Visual Studio. Por exemplo, se um VSPackage instalado adiciona uma **Home Page** comando para o **exibição** menu, você pode chamar esse comando, definindo `CommandParameter` para `View.HomePage`.  
  
> [!NOTE]
>  Se você chamar um comando que está associado um VSPackage, o pacote deve ser carregado quando o comando é invocado.  
  
## <a name="adding-commands-from-assemblies"></a>Adicionando comandos a partir de Assemblies  
 Para chamar um comando de um assembly, ou código de acesso em um VSPackage que não está associado um comando de menu, você deve criar um alias para o assembly e, em seguida, chame o alias.  
  
#### <a name="to-call-a-command-from-an-assembly"></a>Para chamar um comando de um assembly  
  
1.  Em sua solução, adicione uma referência ao assembly.  
  
2.  Na parte superior do arquivo StartPage, adicione uma diretiva de namespace para o assembly, conforme mostrado no exemplo a seguir.  
  
    ```xml  
    xmlns:vsc="clr-namespace:WebUserControl;assembly=WebUserControl"  
    ```  
  
3.  Invocar o comando, definindo o `Command` propriedade de um objeto XAML, conforme mostrado no exemplo a seguir.  
  
     XAML  
  
    ```  
    <vs:Button Text="Hide me" Command="{x:Static vsc:HideControl}" .../>  
    ```  
  
> [!NOTE]
>  Você deve copiar o assembly e, em seguida, cole-o no... \\ *Pasta de instalação do visual Studio*\Common7\IDE\PrivateAssemblies\ para garantir que ele é carregado antes que ele é chamado.  
  
## <a name="adding-commands-with-the-dte-object"></a>Adicionando comandos com o objeto DTE  
 Você pode acessar o objeto DTE de uma página inicial, na marcação e no código.  
  
 Na marcação, você pode acessá-lo usando o [extensão de marcação Binding](http://msdn.microsoft.com/library/83d6e2a4-1b0c-4fc8-bd96-b5e98800ab63) sintaxe para chamar o <xref:EnvDTE.DTE> objeto. Você pode usar essa abordagem para associar a propriedades simples, como aqueles que retornam coleções, mas você não pode associar a métodos ou serviços. A exemplo a seguir mostra um <xref:System.Windows.Controls.TextBlock> controle que está associado a <xref:EnvDTE._DTE.Name%2A> propriedade e um <xref:System.Windows.Controls.ListBox> controle que enumera os <xref:EnvDTE.Window.Caption%2A> propriedades da coleção que é retornado pelo <xref:EnvDTE._DTE.Windows%2A> propriedade.  
  
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
  
 Por exemplo, consulte [instruções passo a passo: salvando configurações de usuário de uma página inicial](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md).  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar um controle de usuário à página inicial](../extensibility/adding-user-control-to-the-start-page.md)

