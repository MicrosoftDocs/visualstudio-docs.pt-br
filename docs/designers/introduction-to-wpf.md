---
title: Introdução ao WPF
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: b8d7cf43-d1f2-4f3d-adb0-4f3a6428edc0
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- csharp
- vb
ms.workload:
- multiple
ms.openlocfilehash: db06323da8ccd3009c52be3ba9dd51478d1d722c
ms.sourcegitcommit: 96a6d1f16d06ca28d309d05b6e9fbd52f628cdbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2018
ms.locfileid: "40008454"
---
# <a name="wpf-overview"></a>Visão geral do WPF

O Windows Presentation Foundation (WPF) permite criar aplicativos para cliente de área de trabalho do Windows com experiências de usuário visualmente impressionantes.

![Amostra de interface do usuário do Contoso Healthcare](../designers/media/wpfintrofigure24.png)

O núcleo do WPF é um mecanismo de renderização que não depende da resolução e baseado em vetor, criado para tirar proveito de hardwares gráficos modernos. O WPF estende o núcleo com um conjunto abrangente de funcionalidades de desenvolvimento de aplicativos que incluem linguagem XAML, controles, associação de dados, layout, elementos gráficos 2D e 3D, animação, estilos, modelos, documentos, mídia, texto e tipografia. O WPF está incluído no .NET Framework, portanto, você pode criar aplicativos que incorporam outros elementos da biblioteca de classes do .NET Framework.

Esta visão geral é destinada para principiantes e aborda os principais conceitos e funcionalidades do WPF.

## <a name="program-with-wpf"></a>Programar com o WPF

O WPF existe como um subconjunto de tipos do .NET Framework que geralmente estão localizados no namespace <xref:System.Windows>. Se você tiver criado aplicativos com o .NET Framework anteriormente usando tecnologias gerenciadas como ASP.NET e Windows Forms, a experiência essencial do WPF em programação deverá ser familiar; você instancia classes, define propriedades, chama métodos e manipula eventos usando sua linguagem de programação .NET favorita como C# ou Visual Basic.

O WPF inclui constructos de programação adicionais que aprimoram as propriedades e eventos: [propriedades de dependência](/dotnet/framework/wpf/advanced/dependency-properties-overview) e [eventos roteados](/dotnet/framework/wpf/advanced/routed-events-overview).

## <a name="markup-and-code-behind"></a>Marcação e code-behind

O WPF permite que você desenvolva um aplicativo usando *marcação* e *code-behind*, uma experiência com a qual os desenvolvedores do ASP.NET devem estar familiarizados. Você geralmente usa marcação XAML para implementar a aparência de um aplicativo enquanto usa linguagens de programação gerenciadas (code-behind) para implementar seu comportamento. Essa separação de aparência e comportamento apresenta os seguintes benefícios:

- Custos de desenvolvimento e manutenção são reduzidos, pois a marcação específica da aparência não está acoplada ao comportamento específico do código.

- O desenvolvimento é mais eficiente porque os designers podem implementar a aparência de um aplicativo simultaneamente com os desenvolvedores que estão implementando o comportamento do aplicativo.

- A [globalização e localização](/dotnet/framework/wpf/advanced/wpf-globalization-and-localization-overview) de aplicativos WPF é simplificada.

### <a name="markup"></a>Marcação

O XAML é uma linguagem de marcação baseada em XML que implementa a aparência de um aplicativo de forma declarativa. Normalmente, ele é usado para criar janelas, caixas de diálogo, páginas e controles de usuário e para preenchê-los com controles, formas e elementos gráficos.

O exemplo a seguir usa XAML para implementar a aparência de uma janela que contém um único botão.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    Title="Window with Button"
    Width="250" Height="100">

  <!-- Add button to window -->
  <Button Name="button">Click Me!</Button>

</Window>
```

Especificamente, esse XAML define uma janela e um botão usando os elementos `Window` e `Button`, respectivamente. Cada elemento é configurado com atributos, como o atributo `Title` do elemento `Window` para especificar o texto da barra de título da janela. Em tempo de execução, o WPF converte os elementos e atributos que estão definidos na marcação para instâncias de classes do WPF. Por exemplo, o elemento `Window` é convertido em uma instância da classe <xref:System.Windows.Window>, cuja propriedade <xref:System.Windows.Window.Title%2A> é o valor do atributo `Title`.

A figura a seguir mostra a IU (interface do usuário) que é definida pelo XAML no exemplo anterior.

![Uma janela que contém um botão](../designers/media/wpfintrofigure10.png)

Já que o XAML é baseado em XML, a interface do usuário que você escreve com ele é montada em uma hierarquia de elementos aninhados conhecida como uma [árvore de elementos](/dotnet/framework/wpf/advanced/trees-in-wpf). A árvore de elementos fornece uma maneira lógica e intuitiva para criar e gerenciar interfaces do usuário.

### <a name="code-behind"></a>Code-behind

O comportamento principal de um aplicativo é implementar a funcionalidade que responde às interações do usuário, incluindo a manipulação de eventos (por exemplo, clicar em um menu, barra de ferramentas ou botão) e chamar a lógica de negócios e lógica de acesso a dados como resposta. No WPF, esse comportamento é implementado no código que está associado à marcação. Esse tipo de código é conhecido como code-behind. O exemplo a seguir mostra a marcação atualizada do exemplo anterior e o code-behind.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.AWindow"
    Title="Window with Button"
    Width="250" Height="100">

  <!-- Add button to window -->
  <Button Name="button" Click="button_Click">Click Me!</Button>

</Window>
```

```csharp
using System.Windows; // Window, RoutedEventArgs, MessageBox 

namespace SDKSample
{
    public partial class AWindow : Window
    {
        public AWindow()
        {
            // InitializeComponent call is required to merge the UI 
            // that is defined in markup with this class, including  
            // setting properties and registering event handlers
            InitializeComponent();
        }

        void button_Click(object sender, RoutedEventArgs e)
        {
            // Show message box when button is clicked
            MessageBox.Show("Hello, Windows Presentation Foundation!");
        }
    }
}
```

```vb
Namespace SDKSample

    Partial Public Class AWindow
        Inherits System.Windows.Window

        Public Sub New()

            ' InitializeComponent call is required to merge the UI 
            ' that is defined in markup with this class, including  
            ' setting properties and registering event handlers
            InitializeComponent()

        End Sub 

        Private Sub button_Click(ByVal sender As Object, ByVal e As RoutedEventArgs)

            ' Show message box when button is clicked
            MessageBox.Show("Hello, Windows Presentation Foundation!")

        End Sub 

    End Class 

End Namespace
```

Neste exemplo, o code-behind implementa uma classe derivada da classe <xref:System.Windows.Window>. O atributo `x:Class` é usado para associar a marcação com a classe code-behind. `InitializeComponent` é chamado de construtor da classe code-behind para mesclar a interface do usuário que é definida na marcação com a classe code-behind. (`InitializeComponent` é gerado para você quando seu aplicativo é criado, motivo pelo qual você não precisa implementá-lo manualmente.) A combinação de `x:Class` e `InitializeComponent` assegura que sua implementação será inicializada corretamente sempre que ela for criada. A classe code-behind também implementa um manipulador de eventos para o evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> do botão. Quando o botão é clicado, o manipulador de eventos mostra uma caixa de mensagem ao chamar o método <xref:System.Windows.MessageBox.Show%2A?displayProperty=fullName>.

A figura a seguir mostra o resultado quando o botão é clicado.

![Um MessageBox](../designers/media/wpfintrofigure25.png)

## <a name="controls"></a>Controles

As experiências de usuário que são entregues pelo modelo de aplicativo são controles construídos. No WPF, *controle* é um termo abrangente que se aplica a uma categoria de classes do WPF que são hospedadas em uma janela ou uma página, que têm uma interface do usuário e que implementam um comportamento.

Para obter mais informações, consulte [Controles](/dotnet/framework/wpf/controls/index).

### <a name="wpf-controls-by-function"></a>Controles do WPF por função

Os controles internos do WPF são listados aqui.

- **Botões**: <xref:System.Windows.Controls.Button> e <xref:System.Windows.Controls.Primitives.RepeatButton>.

- **Exibição de dados**: <xref:System.Windows.Controls.DataGrid>, <xref:System.Windows.Controls.ListView> e <xref:System.Windows.Controls.TreeView>.

- **Exibição e a seleção de dados**: <xref:System.Windows.Controls.Calendar> e <xref:System.Windows.Controls.DatePicker>.

- **Caixas de diálogo**: <xref:Microsoft.Win32.OpenFileDialog>, <xref:System.Windows.Controls.PrintDialog> e <xref:Microsoft.Win32.SaveFileDialog>.

- **Tinta digital**: <xref:System.Windows.Controls.InkCanvas> e <xref:System.Windows.Controls.InkPresenter>.

- **Documentos**: <xref:System.Windows.Controls.DocumentViewer>, <xref:System.Windows.Controls.FlowDocumentPageViewer>, <xref:System.Windows.Controls.FlowDocumentReader>, <xref:System.Windows.Controls.FlowDocumentScrollViewer> e <xref:System.Windows.Controls.StickyNoteControl>.

- **Entrada**: <xref:System.Windows.Controls.TextBox>, <xref:System.Windows.Controls.RichTextBox> e <xref:System.Windows.Controls.PasswordBox>.

- **Layout**: <xref:System.Windows.Controls.Border>, <xref:System.Windows.Controls.Primitives.BulletDecorator>, <xref:System.Windows.Controls.Canvas>, <xref:System.Windows.Controls.DockPanel>, <xref:System.Windows.Controls.Expander>, <xref:System.Windows.Controls.Grid>, <xref:System.Windows.Controls.GridView>, <xref:System.Windows.Controls.GridSplitter>, <xref:System.Windows.Controls.GroupBox>, <xref:System.Windows.Controls.Panel>, <xref:System.Windows.Controls.Primitives.ResizeGrip>, <xref:System.Windows.Controls.Separator>, <xref:System.Windows.Controls.Primitives.ScrollBar>, <xref:System.Windows.Controls.ScrollViewer>, <xref:System.Windows.Controls.StackPanel>, <xref:System.Windows.Controls.Primitives.Thumb>, <xref:System.Windows.Controls.Viewbox>, <xref:System.Windows.Controls.VirtualizingStackPanel>, <xref:System.Windows.Window> e <xref:System.Windows.Controls.WrapPanel>.

- **Mídia**: <xref:System.Windows.Controls.Image>, <xref:System.Windows.Controls.MediaElement> e <xref:System.Windows.Controls.SoundPlayerAction>.

- **Menus**: <xref:System.Windows.Controls.ContextMenu>, <xref:System.Windows.Controls.Menu> e <xref:System.Windows.Controls.ToolBar>.

- **Navegação**: <xref:System.Windows.Controls.Frame>, <xref:System.Windows.Documents.Hyperlink>, <xref:System.Windows.Controls.Page>, <xref:System.Windows.Navigation.NavigationWindow> e <xref:System.Windows.Controls.TabControl>.

- **Seleção**: <xref:System.Windows.Controls.CheckBox>, <xref:System.Windows.Controls.ComboBox>, <xref:System.Windows.Controls.ListBox>, <xref:System.Windows.Controls.RadioButton> e <xref:System.Windows.Controls.Slider>.

- **Informações do usuário**: <xref:System.Windows.Controls.AccessText>, <xref:System.Windows.Controls.Label>, <xref:System.Windows.Controls.Primitives.Popup>, <xref:System.Windows.Controls.ProgressBar>, <xref:System.Windows.Controls.Primitives.StatusBar>, <xref:System.Windows.Controls.TextBlock> e <xref:System.Windows.Controls.ToolTip>.

## <a name="input-and-commands"></a>Entrada e comandos

Controles normalmente detectam e respondem a entradas do usuário. O [sistema de entrada do WPF](/dotnet/framework/wpf/advanced/input-overview) usa tanto os eventos diretos como os roteados para dar suporte a entrada de texto, foco de gerenciamento e posicionamento do mouse.

Aplicativos muitas vezes têm requisitos de entrada complexos. O WPF fornece um [sistema de comando](/dotnet/framework/wpf/advanced/commanding-overview) que separa as ações de entrada do usuário do código que responde a essas ações.

## <a name="layout"></a>Layout

Quando você cria uma interface do usuário, você organiza os controles por local e tamanho para formar um layout. Um requisito chave de qualquer layout é se adaptar a alterações no tamanho da janela e exibir as configurações. Em vez de forçá-lo a escrever o código para adaptar um layout nessas circunstâncias, o WPF fornece um sistema de layout extensível e de primeira classe para você.

A base do sistema de layout é o posicionamento relativo, que aumenta a capacidade de se adaptar às modificações da janela e condições de exibição. Além disso, o sistema de layout gerencia a negociação entre os controles para determinar o layout. A negociação é um processo de duas etapas: primeiro, um controle informa ao pai o local e tamanho requerido; segundo, o pai informa ao controle qual espaço ele pode ter.

O sistema de layout é exposto aos controles filho por meio de classes base do WPF. Para layouts comuns, como grades, empilhamento e encaixe, o WPF inclui vários controles de layout:

- <xref:System.Windows.Controls.Canvas>: os controles filho fornecem seus próprios layouts.

- <xref:System.Windows.Controls.DockPanel>: os controles filho são alinhados com as bordas do painel.

- <xref:System.Windows.Controls.Grid>: os controles filho são posicionados por linhas e colunas.

- <xref:System.Windows.Controls.StackPanel>: os controles filho são empilhados verticalmente ou horizontalmente.

- <xref:System.Windows.Controls.VirtualizingStackPanel>: os controles filho são virtualizados e organizados em uma única linha, que é orientada horizontal ou verticalmente.

- <xref:System.Windows.Controls.WrapPanel>: os controles filho são posicionados na ordem da esquerda para a direita e, quando há mais controles na linha atual do que o espaço permite, sofrem quebra automática para a próxima linha.

O exemplo a seguir usa <xref:System.Windows.Controls.DockPanel> para o layout de vários controles <xref:System.Windows.Controls.TextBox>.

[!code-xaml[IntroToWPFSnippets#LayoutMARKUP](../designers/codesnippet/Xaml/introduction-to-wpf_1.xaml)]

O <xref:System.Windows.Controls.DockPanel> permite que os controles <xref:System.Windows.Controls.TextBox> filho informem como organizá-los. Para fazer isso, o <xref:System.Windows.Controls.DockPanel> implementa uma propriedade anexada `Dock` que é exposta aos controles filho para permitir que cada um especifique um estilo de encaixe.

> [!NOTE]
> Uma propriedade que é implementada por um controle pai para uso por controles filho é uma constructo do WPF chamado de [propriedade anexada](/dotnet/framework/wpf/advanced/attached-properties-overview).

A figura a seguir mostra o resultado da marcação XAML no exemplo anterior.

![Página DockPanel](../designers/media/wpfintrofigure11.png)

## <a name="data-binding"></a>Associação de dados

A maioria dos aplicativos são criados para fornecer aos usuários os meios para exibir e editar dados. Para aplicativos WPF, o trabalho de armazenar e acessar dados já é fornecido por tecnologias, como SQL Server e ADO.NET. Depois que os dados são acessados e carregados em objetos gerenciados do aplicativo, começa o trabalho pesado para os aplicativos WPF. Essencialmente, isso envolve duas coisas:

1.  Copiar os dados dos objetos gerenciados para controles, nos quais os dados podem ser exibidos e editados.

2.  Assegurar que as alterações feitas nos dados usando controles sejam copiadas para os objetos gerenciados.

Para simplificar o desenvolvimento de aplicativos, o WPF fornece um mecanismo de vinculação de dados para executar essas etapas automaticamente. A unidade principal do mecanismo de associação de dados é a classe <xref:System.Windows.Data.Binding>, cujo trabalho é associar um controle (o destino da associação) a um objeto de dados (a origem da associação). Essa relação é ilustrada pela figura a seguir:

![Diagrama de associação de dados básica](../designers/media/databindingmostbasic.png)

O exemplo a seguir demonstra como associar um <xref:System.Windows.Controls.TextBox> a uma instância de um objeto `Person` personalizado. A implementação de `Person` é mostrada no código a seguir:

[!code-vb[SimpleDataBindingSnippets#PersonClassCODE](../designers/codesnippet/VisualBasic/introduction-to-wpf_2.vb)]
[!code-csharp[SimpleDataBindingSnippets#PersonClassCODE](../designers/codesnippet/CSharp/introduction-to-wpf_2.cs)]

A marcação a seguir associa o <xref:System.Windows.Controls.TextBox> a uma instância de um objeto `Person` personalizado.

 ```xaml
 <Window
     xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
     xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
     x:Class="SDKSample.DataBindingWindow">

   <!-- Bind the TextBox to the data source (TextBox.Text to Person.Name) -->
   <TextBox Name="personNameTextBox" Text="{Binding Path=Name}" />

 </Window>
 ```

[!code-vb[SimpleDataBindingSnippets#DataBindingCODEBEHIND](../designers/codesnippet/VisualBasic/introduction-to-wpf_6.vb)]
[!code-csharp[SimpleDataBindingSnippets#DataBindingCODEBEHIND](../designers/codesnippet/CSharp/introduction-to-wpf_6.cs)]

Neste exemplo, a classe `Person` é instanciada no code-behind e é definida como o contexto de dados para o `DataBindingWindow`. Na marcação, a propriedade <xref:System.Windows.Controls.TextBox.Text%2A> do <xref:System.Windows.Controls.TextBox> está associada à propriedade `Person.Name` (usando a sintaxe XAML "`{Binding ... }`"). Esse XAML solicita que o WPF associe o controle <xref:System.Windows.Controls.TextBox> ao objeto `Person` armazenado na propriedade <xref:System.Windows.FrameworkElement.DataContext%2A> da janela.

O mecanismo de vinculação de dados do WPF fornece suporte adicional que inclui a validação, classificação, filtragem e agrupamento. Além disso, a vinculação de dados dá suporte ao uso de modelos de dados para criar a interface do usuário personalizada para dados associados quando a interface do usuário exibida pelos controles WPF padrão não é apropriada.

Para obter mais informações, confira [Visão geral de associação de dados](/dotnet/framework/wpf/data/data-binding-overview).

## <a name="graphics"></a>Gráficos

O WPF introduz um conjunto amplo, escalonável e flexível de funcionalidades gráficas com os seguintes benefícios:

- **Elementos gráficos independentes de resolução e de dispositivo**. A unidade básica de medida no sistema gráfico do WPF é o pixel independente de dispositivo, que é 1/96 de polegada, independentemente da resolução de tela e que fornece a base para a renderização independente de resolução e de dispositivo. Cada pixel independente de dispositivo pode ser dimensionado automaticamente para corresponder à configuração de dpi (pontos por polegada) do sistema em que ele é renderizado.

- **Maior precisão**. O sistema de coordenadas do WPF é medido com números de ponto flutuante de precisão dupla em vez de precisão simples. Transformações e valores opacidade também são expressos com precisão dupla. O WPF também dá suporte a uma gama de cores (scRGB) e oferece suporte integrado para gerenciar entradas de diferentes espaços de cores.

- **Suporte a animação e elementos gráficos avançados**. O WPF simplifica a programação de elementos gráficos ao gerenciar cenas de animação para você; não é necessário se preocupar sobre o processamento da cena, loops de renderização e interpolação bilinear. Além disso, o WPF dá suporte a teste de clique e suporte completo a composição alfa.

- **Aceleração de hardware**. Sistema gráfico do WPF tira proveito do hardware gráfico para minimizar o uso da CPU.

### <a name="2d-shapes"></a>Formas 2D

O WPF fornece uma biblioteca de formas vetoriais 2D comuns como retângulos e elipses, que são mostradas na ilustração a seguir:

![Elipses e retângulos](../designers/media/wpfintrofigure4.PNG)

Uma funcionalidade interessante de formas é que elas não são apenas para exibição; as formas implementam muitas das funcionalidades que você espera dos controles, incluindo entrada de teclado e de mouse. O exemplo a seguir mostra o evento <xref:System.Windows.UIElement.MouseUp> de um <xref:System.Windows.Shapes.Ellipse> que está sendo manipulado.

[!code-xaml[IntroToWPFSnippets#HandleEllipseMouseUpEventMARKUP](../designers/codesnippet/Xaml/introduction-to-wpf_7.xaml)]

[!code-vb[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](../designers/codesnippet/VisualBasic/introduction-to-wpf_8.vb)]
[!code-csharp[IntroToWPFSnippets#HandleEllipseMouseUpEventCODEBEHIND](../designers/codesnippet/CSharp/introduction-to-wpf_8.cs)]

A figura a seguir mostra o que é produzido pelo código anterior.

![Uma janela com o texto "você clicou na elipse&#33"](../designers/media/wpfintrofigure12.png)

Para obter mais informações, confira [Visão geral de formas e desenho básico no WPF](/dotnet/framework/wpf/data/data-binding-overview).

### <a name="2d-geometries"></a>Geometrias 2D

As formas 2D fornecidas pelo WPF abrangem o conjunto padrão de formas básicas. No entanto, talvez seja necessário criar formas personalizadas para facilitar o design de uma interface do usuário personalizada. Para essa finalidade, o WPF fornece geometrias. A figura a seguir demonstra o uso de geometrias para criar uma forma personalizada que pode ser desenhada diretamente, usada como um pincel ou usada para recortar outras formas e controles.

Os objetos <xref:System.Windows.Shapes.Path> podem ser usados para desenhar formas fechadas ou abertas, várias formas e até mesmo formas curvas.

Os objetos <xref:System.Windows.Media.Geometry> podem ser usados para recorte, teste de clique e renderização de dados gráficos 2D.

![Vários usos de um demarcador](../designers/media/wpfintrofigure5.png)

Para obter mais informações, confira [Visão geral de geometria](/dotnet/framework/wpf/graphics-multimedia/geometry-overview).

### <a name="2d-effects"></a>Efeitos 2D

Um subconjunto de funcionalidades 2D do WPF inclui efeitos visuais como gradientes, bitmaps, desenhos, pintura com vídeos, rotação, dimensionamento e distorção. Eles são todas obtidos com pincéis; a figura a seguir mostra alguns exemplos.

![Ilustração de diferentes pincéis](../designers/media/wpfintrofigure6.png)

Para obter mais informações, confira [Visão geral de pincéis do WPF](/dotnet/framework/wpf/graphics-multimedia/wpf-brushes-overview).

### <a name="3d-rendering"></a>Renderização 3D

O WPF também inclui funcionalidades de renderização 3D que se integram com elementos gráficos em 2D para permitir a criação de interfaces do usuário mais interessantes e empolgantes. Por exemplo, a figura a seguir mostra imagens 2D renderizadas em formas 3D.

![Captura de tela de exemplo do Visual3D](../designers/media/wpfintrofigure13.png)

Para obter mais informações, confira [Visão geral de elementos gráficos 3D](/dotnet/framework/wpf/graphics-multimedia/3-d-graphics-overview).

## <a name="animation"></a>Animação

O suporte a animação do WPF permite que você faça os controles crescerem, tremerem, rodarem e esmaecerem, para criar transições de página interessantes e muito mais. Você pode animar a maioria das classes do WPF, até mesmo classes personalizadas. A figura a seguir mostra uma animação simples em ação.

![Imagens de um cubo animado](../designers/media/wpfintrofigure7.png)

Para obter mais informações, confira [Visão geral de animação](/dotnet/framework/wpf/graphics-multimedia/animation-overview).

## <a name="media"></a>Mídia

Uma maneira de transmitir conteúdo rico é pelo uso de mídia audiovisual. O WPF dá suporte especial para imagens, áudio e vídeo.

### <a name="images"></a>Imagens

Imagens são comuns à maioria dos aplicativos e o WPF fornece várias maneiras de usá-las. A figura a seguir mostra uma interface do usuário com uma caixa de listagem que contém imagens em miniatura. Quando uma miniatura é selecionada, a imagem é mostrada em tamanho normal.

![Imagens em miniatura e uma imagem em tamanho original](../designers/media/wpfintrofigure8.png)

Para obter mais informações, confira [Visão geral de geração de imagens](/dotnet/framework/wpf/graphics-multimedia/imaging-overview).

### <a name="video-and-audio"></a>Áudio e vídeo

O controle <xref:System.Windows.Controls.MediaElement> é capaz de executar áudio e vídeo e é flexível o suficiente para ser a base de um player de mídia personalizado. A marcação XAML a seguir implementa um player de mídia.

[!code-xaml[IntroToWPFSnippets#MediaElementMARKUP](../designers/codesnippet/Xaml/introduction-to-wpf_9.xaml)]

A janela na figura a seguir mostra o controle <xref:System.Windows.Controls.MediaElement> em ação.

![Um controle MediaElement com áudio e vídeo](../designers/media/wpfintrofigure1.png)

Para obter mais informações, confira [Elementos gráficos e multimídia](/dotnet/framework/wpf/graphics-multimedia).

## <a name="text-and-typography"></a>Texto e tipografia

Para facilitar a renderização de texto de alta qualidade, o WPF oferece as seguintes funcionalidades:

- Suporte a fontes OpenType.

- Aprimoramentos de ClearType.

- Alto desempenho que tira proveito da aceleração de hardware.

- Integração do texto com mídia, elementos gráficos e animação.

- Mecanismos de fallback e suporte a fontes internacionais.

Como uma demonstração de integração de texto com elementos gráficos, a figura a seguir mostra o aplicativo de decoração de texto.

![Texto com várias decorações](../designers/media/wpfintrofigure23.png)

Para obter mais informações, consulte [Tipografia na Windows Presentation Foundation](/dotnet/framework/wpf/advanced/typography-in-wpf).

## <a name="customize-wpf-apps"></a>Personalizar aplicativos do WPF

Até aqui, você viu os principais blocos de construção do WPF principal para o desenvolvimento de aplicativos. Você pode usar o modelo de aplicativo para hospedar e entregar conteúdo do aplicativo, que consiste principalmente de controles. Para simplificar a organização dos controles em uma interface do usuário e assegurar que a organização seja mantida em caso de alterações no tamanho da janela e configurações de exibição, você deverá usar o sistema de layout do WPF. Já que a maioria dos aplicativos permite aos usuários interagir com os dados, use a associação de dados para reduzir o trabalho de integração da interface do usuário com os dados. Para melhorar a aparência visual do seu aplicativo, você deve usar a ampla gama de suporte a elementos gráficos, animação e mídia fornecido pelo WPF.

Muitas vezes, no entanto, os conceitos básicos não são suficientes para criar e gerenciar uma experiência do usuário realmente distinta e visualmente impressionante. Os controles padrão do WPF podem não ser integrados à aparência desejada do aplicativo. Os dados podem não ser exibidos da maneira mais eficiente. A experiência do usuário geral do seu aplicativo pode não ser adequada para a aparência padrão de temas do Windows. Em muitos aspectos, uma tecnologia de apresentação precisa de extensibilidade visual, assim como qualquer outro tipo de extensibilidade.

Por esse motivo, o WPF fornece uma variedade de mecanismos para criar experiências de usuário exclusivas, incluindo um modelo rico de conteúdo para controles, gatilhos, modelos de dados e de controle, estilos, recursos de interface do usuário, temas e capas.

### <a name="content-model"></a>Modelo de conteúdo

O principal objetivo da maioria dos controles WPF é exibir conteúdo. No WPF, o tipo e o número de itens que podem constituir o conteúdo de um controle são conhecidos como o *modelo de conteúdo* do controle. Alguns controles podem conter um único item e o tipo de conteúdo. Por exemplo, o conteúdo de um <xref:System.Windows.Controls.TextBox> é um valor de cadeia de caracteres que é atribuído à propriedade <xref:System.Windows.Controls.TextBox.Text%2A>. O exemplo a seguir define o conteúdo de um <xref:System.Windows.Controls.TextBox>.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.TextBoxContentWindow"
    Title="TextBox Content">

    <TextBox Text="This is the content of a TextBox." />
</Window>
```

A figura a seguir mostra o resultado.

![Um Controle TextBox que contém texto](../designers/media/wpfintrofigure21.png)

Outros controles, entretanto, podem conter vários itens de diferentes tipos de conteúdo. O conteúdo de um <xref:System.Windows.Controls.Button>, especificado pela propriedade <xref:System.Windows.Controls.ContentControl.Content%2A>, pode conter uma variedade de itens, incluindo controles de layout, texto, imagens e formas. O exemplo a seguir mostra um <xref:System.Windows.Controls.Button> com conteúdo que inclui um <xref:System.Windows.Controls.DockPanel>, um <xref:System.Windows.Controls.Label>, um <xref:System.Windows.Controls.Border> e um <xref:System.Windows.Controls.MediaElement>.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.ButtonContentWindow"
    Title="Button Content">

  <Button Margin="20">
    <!-- Button Content -->
    <DockPanel Width="200" Height="180">
      <Label DockPanel.Dock="Top" HorizontalAlignment="Center">Click Me!</Label>
      <Border Background="Black" BorderBrush="Yellow" BorderThickness="2"
        CornerRadius="2" Margin="5">
        <MediaElement Source="media/wpf.wmv" Stretch="Fill" />
      </Border>
    </DockPanel>
  </Button>
</Window>
```

A figura a seguir mostra o conteúdo desse botão.

![Um botão que contém vários tipos de conteúdo](../designers/media/wpfintrofigure22.png)

Para obter mais informações sobre os tipos de conteúdo compatíveis com vários controles, confira [Modelo de conteúdo do WPF](/dotnet/framework/wpf/controls/wpf-content-model).

### <a name="triggers"></a>Gatilhos

Embora o objetivo principal da marcação XAML seja implementar a aparência de um aplicativo, você também pode usar XAML para implementar alguns aspectos do comportamento do aplicativo. Um exemplo é o uso de gatilhos para alterar a aparência de um aplicativo com base em interações do usuário. Para obter mais informações, confira [Estilo e modelagem](/dotnet/framework/wpf/controls/styling-and-templating).

### <a name="control-templates"></a>Modelos de controle

As interfaces do usuário padrão para controles WPF normalmente são construídas de outros controles e formas. Por exemplo, um <xref:System.Windows.Controls.Button> é composto de dois controles, <xref:Microsoft.Windows.Themes.ButtonChrome> e <xref:System.Windows.Controls.ContentPresenter>. O <xref:Microsoft.Windows.Themes.ButtonChrome> fornece a aparência padrão do botão, enquanto o <xref:System.Windows.Controls.ContentPresenter> exibe o conteúdo do botão, conforme especificado pela propriedade <xref:System.Windows.Controls.ContentControl.Content%2A>.

Às vezes, a aparência padrão de um controle pode ser incongruente com a aparência geral de um aplicativo. Nesse caso, você pode usar um <xref:System.Windows.Controls.ControlTemplate> para alterar a aparência da interface do usuário do controle sem alterar seu conteúdo e seu comportamento.

Por exemplo, o exemplo a seguir mostra como alterar a aparência de um <xref:System.Windows.Controls.Button> usando um <xref:System.Windows.Controls.ControlTemplate>.

[!code-xaml[IntroToWPFSnippets#ButtonControlTemplateWindowMARKUP](../designers/codesnippet/Xaml/introduction-to-wpf_16.xaml)]

[!code-csharp[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](../designers/codesnippet/CSharp/introduction-to-wpf_17.cs)]
[!code-vb[IntroToWPFSnippets#ButtonControlTemplateWindowCODEBEHIND](../designers/codesnippet/VisualBasic/introduction-to-wpf_17.vb)]

Neste exemplo, a interface do usuário padrão do botão foi substituída por um <xref:System.Windows.Shapes.Ellipse> que tem uma borda azul-escuro e foi preenchido usando um <xref:System.Windows.Media.RadialGradientBrush>. O controle <xref:System.Windows.Controls.ContentPresenter> exibe o conteúdo de <xref:System.Windows.Controls.Button>, "Clique-me!" Quando o <xref:System.Windows.Controls.Button> é clicado, o evento <xref:System.Windows.Controls.Primitives.ButtonBase.Click> ainda é gerado como parte do comportamento padrão do controle <xref:System.Windows.Controls.Button>. O resultado é mostrado na figura a seguir:

![Um botão elíptico e uma segunda janela](../designers/media/wpfintrofigure2.png)

### <a name="data-templates"></a>Modelos de dados

Enquanto um modelo de controle permite que você especifique a aparência de um controle, um modelo de dados permite que você especifique a aparência do conteúdo de um controle. Modelos de dados são frequentemente usados para aprimorar o modo como os dados associados são exibidos. A figura a seguir mostra a aparência padrão de um <xref:System.Windows.Controls.ListBox> que está associado a uma coleção de objetos `Task`, em que cada tarefa tem um nome, uma descrição e uma prioridade.

![Uma caixa de listagem com a aparência padrão](../designers/media/wpfintrofigure18.png)

A aparência padrão é o que seria esperado de <xref:System.Windows.Controls.ListBox>. No entanto, a aparência padrão de cada tarefa contém somente o nome da tarefa. Para mostrar o nome da tarefa, a descrição e a prioridade, a aparência padrão dos itens da lista associada ao controle <xref:System.Windows.Controls.ListBox> deve ser alterada usando um <xref:System.Windows.DataTemplate>. O XAML a seguir define um <xref:System.Windows.DataTemplate> desse, que é aplicado a cada tarefa usando o atributo <xref:System.Windows.Controls.ItemsControl.ItemTemplate%2A>.

```xaml
<Window
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="SDKSample.DataTemplateWindow"
  Title="With a Data Template">
  <Window.Resources>
    <!-- Data Template (applied to each bound task item in the task collection) -->
    <DataTemplate x:Key="myTaskTemplate">
      <Border Name="border" BorderBrush="DarkSlateBlue" BorderThickness="2"
        CornerRadius="2" Padding="5" Margin="5">
        <Grid>
          <Grid.RowDefinitions>
            <RowDefinition/>
            <RowDefinition/>
            <RowDefinition/>
          </Grid.RowDefinitions>
          <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto" />
            <ColumnDefinition />
          </Grid.ColumnDefinitions>
          <TextBlock Grid.Row="0" Grid.Column="0" Padding="0,0,5,0" Text="Task Name:"/>
          <TextBlock Grid.Row="0" Grid.Column="1" Text="{Binding Path=TaskName}"/>
          <TextBlock Grid.Row="1" Grid.Column="0" Padding="0,0,5,0" Text="Description:"/>
          <TextBlock Grid.Row="1" Grid.Column="1" Text="{Binding Path=Description}"/>
          <TextBlock Grid.Row="2" Grid.Column="0" Padding="0,0,5,0" Text="Priority:"/>
          <TextBlock Grid.Row="2" Grid.Column="1" Text="{Binding Path=Priority}"/>
        </Grid>
      </Border>
    </DataTemplate>
  </Window.Resources>

  <!-- UI -->
  <DockPanel>
    <!-- Title -->
    <Label DockPanel.Dock="Top" FontSize="18" Margin="5" Content="My Task List:"/>

    <!-- Data template is specified by the ItemTemplate attribute -->
    <ListBox
      ItemsSource="{Binding}"
      ItemTemplate="{StaticResource myTaskTemplate}"
      HorizontalContentAlignment="Stretch"
      IsSynchronizedWithCurrentItem="True"
      Margin="5,0,5,5" />

 </DockPanel>
</Window>
```

A figura a seguir mostra o efeito desse código.

![Caixa de listagem que usa um modelo de dados](../designers/media/wpfintrofigure19.png)

Observe que o <xref:System.Windows.Controls.ListBox> manteve seu comportamento e sua aparência geral. Apenas a aparência do conteúdo que está sendo exibido pela caixa de listagem foi alterada.

Para obter mais informações, confira [Visão geral de modelagem de dados](/dotnet/framework/wpf/data/data-templating-overview).

### <a name="styles"></a>Estilos

Os estilos permitem que os desenvolvedores e designers padronizem uma determinada aparência para seus produtos. O WPF fornece um modelo de estilo sólido, cuja base é o elemento <xref:System.Windows.Style>. O exemplo a seguir cria um estilo que define a cor da tela de fundo de cada <xref:System.Windows.Controls.Button> em uma janela para `Orange`.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.StyleWindow"
    Title="Styles">
  <!-- Style that will be applied to all buttons -->
  <Style TargetType="{x:Type Button}">
    <Setter Property="Background" Value="Orange" />
    <Setter Property="BorderBrush" Value="Crimson" />
    <Setter Property="FontSize" Value="20" />
    <Setter Property="FontWeight" Value="Bold" />
    <Setter Property="Margin" Value="5" />
  </Style>
  <!-- This button will have the style applied to it -->
  <Button>Click Me!</Button>

  <!-- This label will not have the style applied to it -->
  <Label>Don't Click Me!</Label>

  <!-- This button will have the style applied to it -->
  <Button>Click Me!</Button>
</Window>
```

Já que esse estilo atinge todos os controles <xref:System.Windows.Controls.Button>, o estilo é aplicado automaticamente a todos os botões na janela, conforme mostrado na figura a seguir:

![Dois botões alaranjados](../designers/media/wpfintrofigure20.png)

Para obter mais informações, confira [Estilo e modelagem](/dotnet/framework/wpf/controls/styling-and-templating).

### <a name="resources"></a>Recursos

Controles em um aplicativo devem compartilhar a mesma aparência, que pode incluir qualquer coisa de fontes e cores da tela de fundo até estilos, modelos de dados e modelos de controle. Você pode usar o suporte do WPF para recursos de interface do usuário para encapsular esses recursos em um único local para reutilização.

O exemplo a seguir define uma cor da tela de fundo comum que é compartilhada por um <xref:System.Windows.Controls.Button> e um <xref:System.Windows.Controls.Label>.

```xaml
<Window
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.ResourcesWindow"
    Title="Resources Window">

  <!-- Define window-scoped background color resource -->
  <Window.Resources>
    <SolidColorBrush x:Key="defaultBackground" Color="Red" />
  </Window.Resources>

  <!-- Button background is defined by window-scoped resource -->
  <Button Background="{StaticResource defaultBackground}">One Button</Button>

  <!-- Label background is defined by window-scoped resource -->
  <Label Background="{StaticResource defaultBackground}">One Label</Label>
</Window>
```

Este exemplo implementa um recurso de cor da tela de fundo usando o elemento da propriedade `Window.Resources`. Este recurso está disponível para todos os filhos de <xref:System.Windows.Window>. Há uma variedade de recursos escopos, incluindo os seguintes, listados na ordem em que eles são resolvidos:

1.  Um controle individual (usando a propriedade <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName> herdada).

2.  Um <xref:System.Windows.Window> ou um <xref:System.Windows.Controls.Page> (também usando a propriedade herdada <xref:System.Windows.FrameworkElement.Resources%2A?displayProperty=fullName>).

3.  Um <xref:System.Windows.Application> (usando a propriedade <xref:System.Windows.Application.Resources%2A?displayProperty=fullName>).

A variedade de escopos oferece flexibilidade em relação à maneira na qual você pode definir e compartilhar seus recursos.

Como uma alternativa a associar diretamente os recursos a um escopo específico, você pode compactar um ou mais recursos usando um <xref:System.Windows.ResourceDictionary> separado, que pode ser referenciado em outras partes de um aplicativo. O exemplo a seguir define uma cor da tela de fundo padrão em um dicionário de recursos.

```xaml
<ResourceDictionary
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">

  <!-- Define background color resource -->
  <SolidColorBrush x:Key="defaultBackground" Color="Red" />

  <!-- Define other resources -->
</ResourceDictionary>
```

 O exemplo a seguir faz referência o dicionário de recursos definido no exemplo anterior para que ele seja compartilhado por um aplicativo.

```xaml
<Application
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    x:Class="SDKSample.App">

  <Application.Resources>
    <ResourceDictionary>
      <ResourceDictionary.MergedDictionaries>
        <ResourceDictionary Source="BackgroundColorResources.xaml"/>
      </ResourceDictionary.MergedDictionaries>
    </ResourceDictionary>
  </Application.Resources>
</Application>
```

Recursos e dicionários de recurso são a base do suporte do WPF a temas e capas.

Para obter mais informações, consulte [Recursos](/dotnet/framework/wpf/advanced/xaml-resources).

### <a name="custom-controls"></a>Controles personalizados

Embora o WPF forneça um host de suporte a personalização, você poderá encontrar situações em que os controles WPF existentes não atendam às necessidades de seu aplicativo ou seus usuários. Isso pode ocorrer quando:

- Não é possível criar a interface do usuário que você precisa ao personalizar a aparência de implementações existentes do WPF.

- Não há suporte para o comportamento que você precisa (ou não é um suporte obtido facilmente) por implementações existentes do WPF.

Neste ponto, no entanto, você pode tirar proveito de um dos três modelos do WPF para criar um novo controle. Cada modelo destina-se a um cenário específico e requer que o controle personalizado derive de uma classe base específica do WPF. Os três modelos estão listados aqui:

- **Modelo de Controle de Usuário**. Um controle personalizado é derivado de <xref:System.Windows.Controls.UserControl> e é composto de um ou mais controles.

- **Modelo de Controle**. Um controle personalizado é derivado de <xref:System.Windows.Controls.Control> e é usado para criar implementações que separam seu comportamento de sua aparência usando modelos, como a maioria dos controles do WPF. Derivar de <xref:System.Windows.Controls.Control> proporciona mais liberdade para criar uma interface do usuário personalizada de controles de usuário, mas pode exigir mais esforço.

- **Modelo de elemento de estrutura**. Um controle personalizado é derivado de <xref:System.Windows.FrameworkElement> quando sua aparência é definida pela lógica de renderização personalizada (e não por modelos).

O exemplo a seguir mostra um controle numérico para cima/para baixo personalizado derivado de <xref:System.Windows.Controls.UserControl>.

[!code-xaml[IntroToWPFSnippets#UserControlMARKUP](../designers/codesnippet/Xaml/introduction-to-wpf_33.xaml)]

[!code-csharp[IntroToWPFSnippets#UserControlCODEBEHIND1](../designers/codesnippet/CSharp/introduction-to-wpf_34.cs)]
[!code-vb[IntroToWPFSnippets#UserControlCODEBEHIND1](../designers/codesnippet/VisualBasic/introduction-to-wpf_34.vb)]

O exemplo a seguir ilustra o XAML que é necessário para incorporar o controle de usuário em um <xref:System.Windows.Window>.

[!code-xaml[IntroToWPFSnippets#UserControlWindowMARKUP1](../designers/codesnippet/Xaml/introduction-to-wpf_37.xaml)]

A figura a seguir mostra o controle `NumericUpDown` hospedado em um <xref:System.Windows.Window>.

![Um UserControl personalizado](../designers/media/wpfintrofigure3.png)

Para obter mais informações sobre controles personalizados, confira [Visão geral da criação de controles](/dotnet/framework/wpf/controls/control-authoring-overview).

## <a name="wpf-best-practices"></a>Melhores práticas do WPF

Assim como com qualquer plataforma de desenvolvimento, o WPF pode ser usado de várias maneiras para atingir o resultado desejado. Como uma maneira de garantir que os aplicativos WPF forneçam a experiência de usuário necessária e atendam às demandas do público em geral, há melhores práticas para acessibilidade, globalização e localização e desempenho. Para obter mais informações, consulte:

- [Acessibilidade](/dotnet/framework/ui-automation/accessibility-best-practices)
- [Globalização e localização do WPF](/dotnet/framework/wpf/advanced/wpf-globalization-and-localization-overview)
- [Desempenho de aplicativo do WPF](/dotnet/framework/wpf/advanced/optimizing-wpf-application-performance)
- [Segurança do WPF](/dotnet/framework/wpf/security-wpf)

## <a name="next-steps"></a>Próximas etapas

Analisamos os principais recursos do WPF. Agora, é hora de criar seu primeiro aplicativo do WPF.

> [!div class="nextstepaction"]
> [Passo a passo: meu primeiro aplicativo da área de trabalho do WPF](/dotnet/framework/wpf/getting-started/walkthrough-my-first-wpf-desktop-application)

## <a name="see-also"></a>Consulte também

- [Introdução ao WPF](../designers/getting-started-with-wpf.md)
- [Windows Presentation Foundation](/dotnet/framework/wpf/index)
- [Recursos da comunidade do WPF](/dotnet/framework/wpf/getting-started/community-feedback)
