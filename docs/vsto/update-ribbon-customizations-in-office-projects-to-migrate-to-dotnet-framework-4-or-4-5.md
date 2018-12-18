---
title: Atualizar personalizações da faixa de opções em projetos do Office que você migrar para o .NET Framework 4 ou o .NET Framework 4.5
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office projects [Office development in Visual Studio], migrating to .NET Framework 4
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4cfd5fb259db7903541e0a86f16c720c9ff9c4d2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49937415"
---
# <a name="update-ribbon-customizations-in-office-projects-that-you-migrate-to-the-net-framework-4-or-the-net-framework-45"></a>Atualizar personalizações da faixa de opções em projetos do Office que você migrar para o .NET Framework 4 ou o .NET Framework 4.5
  Se o projeto contém uma personalização da faixa de opções que foi criada usando o **faixa de opções (Visual Designer)** de item de projeto, você deve fazer as seguintes alterações ao seu código de projeto se a estrutura de destino é alterada para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou mais tarde.  
  
-   Modificar o código gerado da faixa de opções.  
  
-   Modificar qualquer código que cria uma instância de controles da faixa de opções em tempo de execução, manipula os eventos da faixa de opções ou define a posição de um componente de faixa de opções por meio de programação.  
  
## <a name="update-the-generated-ribbon-code"></a>Atualizar o código gerado da faixa de opções  
 Se a estrutura de destino do seu projeto é alterada para o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve alterar o código gerado para o item da faixa de opções, executando as etapas a seguir. Os arquivos de código que você precisa atualizar dependem da linguagem de programação e como você criou o projeto:  
  
-   Em projetos do Visual Basic ou em projetos do Visual c# que você criou no [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] ou [!INCLUDE[vs_dev10_long](../sharepoint/includes/vs-dev10-long-md.md)] execute todas as etapas no arquivo code-behind da faixa de opções (*YourRibbonItem*. Designer.cs ou *YourRibbonItem*. VB). Para ver o arquivo code-behind em projetos do Visual Basic, clique o **Show All Files** botão na **Gerenciador de soluções**.  
  
-   Em projetos do Visual c# que você criou no Visual Studio 2008 e, em seguida, atualizado para [!INCLUDE[vs_dev12](../vsto/includes/vs-dev12-md.md)], execute as duas primeiras etapas no arquivo de código da faixa de opções (*YourRibbonItem*. cs ou *YourRibbonItem*. vb), e Execute as etapas restantes no arquivo code-behind da faixa de opções.  
  
### <a name="to-change-the-generated-ribbon-code"></a>Para alterar o código gerado da faixa de opções  
  
1.  Modifique a declaração da classe da faixa de opções, de modo que ele deriva <xref:Microsoft.Office.Tools.Ribbon.RibbonBase> em vez de `Microsoft.Office.Tools.Ribbon.OfficeRibbon`.  
  
2.  Modifique o construtor da classe da faixa de opções, conforme mostrado abaixo. Se você tiver adicionado a qualquer um dos seus próprios códigos para o construtor, não altere seu código. Em projetos do Visual Basic, modifique apenas o construtor sem parâmetros. Ignore o outro construtor.  
  
     O exemplo de código a seguir mostra o construtor padrão de uma classe de faixa de opções em um projeto que tem como alvo o .NET Framework 3.5.  
  
    ```vb  
    Public Sub New()  
        MyBase.New()  
        InitializeComponent()  
    End Sub  
    ```  
  
    ```csharp  
    public Ribbon1()  
    {  
        InitializeComponent();  
    }  
    ```  
  
     O exemplo de código a seguir mostra o construtor padrão de uma classe de faixa de opções em um projeto que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
    ```vb  
    Public Sub New()  
        MyBase.New(Globals.Factory.GetRibbonFactory())  
        InitializeComponent()  
    End Sub  
    ```  
  
    ```csharp  
    public Ribbon1()  
        : base(Globals.Factory.GetRibbonFactory())  
    {  
        InitializeComponent();  
    }  
    ```  
  
3.  No `InitializeComponent` método, modificar qualquer código que constrói um controle de faixa de opções para que o código em vez disso, usa um dos métodos de auxiliar a <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> objeto.  
  
    > [!NOTE]  
    >  Em projetos do Visual c#, você deve expandir a região em que é denominada `Component Designer generated code` para ver o `InitializeComponent` método.  
  
     Por exemplo, suponha que o arquivo contém a seguinte linha de código que cria uma instância de um <xref:Microsoft.Office.Tools.Ribbon.RibbonButton> denominado `button1` em um projeto que tem como alvo o .NET Framework 3.5.  
  
    ```vb  
    Me.button1 = New Microsoft.Office.Tools.Ribbon.RibbonButton()  
    ```  
  
    ```csharp  
    this.button1 = new Microsoft.Office.Tools.Ribbon.RibbonButton();  
    ```  
  
     Em um projeto que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve usar o código a seguir em vez disso.  
  
    ```vb  
    Me.button1 = Me.Factory.CreateRibbonButton()  
    ```  
  
    ```csharp  
    this.button1 = this.Factory.CreateRibbonButton();  
    ```  
  
     Para obter uma lista completa dos métodos auxiliares para os controles da faixa de opções, consulte [controles de faixa de opções instanciar](#ribboncontrols).  
  
4.  Em projetos do Visual c#, modifique qualquer linha de código na `InitializeComponent` método que usa um <xref:System.EventHandler%601> delegado a ser usado um delegado específico de faixa de opções em vez disso.  
  
     Por exemplo, suponha que o arquivo contém a seguinte linha de código que manipula o <xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click> eventos em um projeto que tem como alvo o .NET Framework 3.5.  
  
    <CodeContentPlaceHolder>8</CodeContentPlaceHolder>  
     Em um projeto que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve usar o código a seguir em vez disso.  
  
    <CodeContentPlaceHolder>9</CodeContentPlaceHolder>  
     Para obter uma lista completa dos delegados da faixa de opções, consulte [eventos tratar da faixa de opções](#ribbonevents).  
  
5.  Em projetos do Visual Basic, localize o `ThisRibbonCollection` classe no final do arquivo. Modifique a declaração dessa classe para que ele não herde mais da `Microsoft.Office.Tools.Ribbon.RibbonReadOnlyCollection`.  
  
##  <a name="ribboncontrols"></a> Criar uma instância de controles da faixa de opções  
 Você deve modificar qualquer código que instancia dinamicamente os controles de faixa de opções. Em projetos que direcionam o .NET Framework 3.5, os controles da faixa de opções são classes que você pode instanciar diretamente em determinados cenários. Em projetos que segmentam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores, esses controles são interfaces que você não pode instanciar diretamente. Você deve criar os controles usando métodos que são fornecidos pelo <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> objeto.  
  
 Existem duas maneiras de acessar o objeto <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory>:  
  
- Usando a propriedade de fábrica da faixa de opções de classe. Use essa abordagem no código na classe Ribbon.  
  
- Usando o método `Globals.Factory.GetRibbonFactory`. Use essa abordagem no código fora da classe Ribbon. Para obter mais informações sobre a classe Globals, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
  O exemplo de código a seguir demonstra como criar uma <xref:Microsoft.Office.Tools.Ribbon.RibbonButton> em uma classe de faixa de opções em um projeto que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
<CodeContentPlaceHolder>10</CodeContentPlaceHolder>  
<CodeContentPlaceHolder>11</CodeContentPlaceHolder>  
 A tabela a seguir lista os controles que você pode criar programaticamente e o método a ser usado para criar os controles em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
|Controle|Método RibbonFactory para usar na [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e projetos posteriores|  
|-------------| - |  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButton%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButtonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonButtonGroup%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonCheckBox%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonComboBox%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDialogLauncher>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDialogLauncher%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown>:|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDown%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonDropDownItem>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonDropDownItem%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonEditBox%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGallery>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGallery%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonGroup>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonGroup%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonLabel>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonLabel%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonManager>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonManager%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonMenu>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonMenu%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSeparator>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSeparator%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonSplitButton%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonTab>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonTab%2A>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton>|<xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.CreateRibbonToggleButton%2A>|  
  
##  <a name="ribbonevents"></a> Manipular eventos da faixa de opções  
 Você deve modificar qualquer código que manipula os eventos de controles da faixa de opções. Em projetos direcionados ao .NET Framework 3.5, esses eventos são manipulados pelo genérica <xref:System.EventHandler%601> delegar. Em projetos que segmentam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou versões posteriores, esses eventos estão agora controlados pelos outros delegados.  
  
 A tabela a seguir lista os eventos da faixa de opções e os delegados que são associados com eles em projetos direcionados a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior.  
  
|evento|Delegado a ser usado em [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] e projetos posteriores|  
|-----------| - |  
|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.LoadImage> evento em uma classe gerada da faixa de opções|<xref:Microsoft.Office.Tools.Ribbon.RibbonLoadImageEventHandler>|  
|<xref:Microsoft.Office.Tools.Ribbon.OfficeRibbon.Load>|<xref:Microsoft.Office.Tools.Ribbon.RibbonUIEventHandler>|  
|<xref:Microsoft.Office.Tools.Ribbon.RibbonButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonCheckBox.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonComboBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonDropDown.SelectionChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonEditBox.TextChanged><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ButtonClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGallery.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonGroup.DialogLauncherClick><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonMenu.ItemsLoading><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonSplitButton.Click><br /><br /> <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click>|<xref:Microsoft.Office.Tools.Ribbon.RibbonControlEventHandler>|  
  
## <a name="set-the-position-of-a-ribbon-component-programmatically"></a>Definir a posição de um componente de faixa de opções programaticamente  
 Você deve modificar qualquer código que define a posição de grupos, tabulações ou controles da faixa de opções. Em projetos direcionados ao .NET Framework 3.5, você pode usar o `AfterOfficeId` e `BeforeOfficeId` métodos estáticos `Microsoft.Office.Tools.Ribbon.RibbonPosition` classe para atribuir o `Position` propriedade de um controle, grupo ou guia. Em projetos que se destinam a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou posterior, você deve acessar esses métodos usando o <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory.RibbonPosition%2A> propriedade fornecida pelo <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory> objeto.  
  
 Existem duas maneiras de acessar o objeto <xref:Microsoft.Office.Tools.Ribbon.RibbonFactory>:  
  
- Usando a propriedade `Factory` da classe Ribbon. Use essa abordagem no código na classe Ribbon.  
  
- Usando o método `Globals.Factory.GetRibbonFactory`. Use essa abordagem no código fora da classe Ribbon. Para obter mais informações sobre a classe Globals, consulte [Global de acesso a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).  
  
  O exemplo de código a seguir demonstra como definir o `Position` propriedade de uma guia em uma classe de faixa de opções em um projeto que tem como alvo o .NET Framework 3.5.  
  
```vb  
Me.tab1.Position = RibbonPosition.AfterOfficeId("TabHome")  
```  
  
```csharp  
this.tab1.Position = RibbonPosition.AfterOfficeId("TabHome");  
```  
  
 O exemplo de código a seguir demonstra a mesma tarefa em um projeto que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)].  
  
```vb  
Me.tab1.Position = Me.Factory.RibbonPosition.AfterOfficeId("TabHome")  
```  
  
```csharp  
this.tab1.Position = this.Factory.RibbonPosition.AfterOfficeId("TabHome");  
```  
  
## <a name="see-also"></a>Consulte também  
 [Migrar soluções do Office para o .NET Framework 4 ou posterior](../vsto/migrating-office-solutions-to-the-dotnet-framework-4-or-later.md)   
 [Designer da faixa de opções](../vsto/ribbon-designer.md)  
  
  