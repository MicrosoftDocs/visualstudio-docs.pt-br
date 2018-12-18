---
title: Criar um adorno de exibição, comandos e configurações | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 4a2df0a3-42da-4f7b-996f-ee16a35ac922
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7d0605798f5970411fa315d309807dc6f1f7a0cf
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872350"
---
# <a name="walkthrough-create-a-view-adornment-commands-and-settings-column-guides"></a>Passo a passo: Criar um adorno de exibição, comandos e configurações (guias de coluna)
Você pode estender o editor de texto/código do Visual Studio com comandos e efeitos de exibição. Este artigo mostra como começar com um recurso de extensão popular, guias de coluna. Guias de coluna são visualmente luz linhas desenhadas em modo de exibição do editor de texto para ajudá-lo a gerenciar seu código para as larguras das colunas específicas. Especificamente, o código formatado pode ser importante para os exemplos incluem em documentos, postagens de blog ou relatórios de bugs.  
  
 Neste passo a passo, você:  
  
- Crie um projeto VSIX  
  
- Adicionar um adorno de exibição do editor  
  
- Adicionar suporte para salvar e obter as configurações (onde a guias de coluna de desenho e suas cores)  
  
- Adicionar comandos (Adicionar/remover guias de coluna, alterar suas cores)  
  
- Coloque os comandos no menu de edição e menus de contexto do documento de texto  
  
- Adicionar suporte para invocar os comandos da janela de comando do Visual Studio  
  
  Você pode experimentar uma versão do recurso de guias de coluna com essa galeria do Visual Studio[extensão](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines).  
  
  **Observação**: neste passo a passo, você deve colar uma grande quantidade de código em alguns arquivos gerados pelos modelos de extensão do Visual Studio. No entanto, em breve neste passo a passo fará referência a uma solução completa no github com outros exemplos de extensão. O código completo é um pouco diferente porque tem ícones de comando real em vez de usar generictemplate ícones.  
  
## <a name="get-started"></a>Introdução  
 A partir do Visual Studio 2015, você não instale o SDK do Visual Studio no Centro de download. Ela está incluída como um recurso opcional na instalação do Visual Studio. Você também pode instalar o SDK do VS mais tarde. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).  
  
## <a name="set-up-the-solution"></a>Configurar a solução  
 Primeiro, crie um projeto VSIX, adicione um adorno de exibição do editor e, em seguida, adicionar um comando (o que adiciona um VSPackage próprio para o comando). A arquitetura básica é o seguinte:  
  
- Você tem um ouvinte de criação de exibição de texto que cria um `ColumnGuideAdornment` objeto por modo de exibição. Esse objeto escuta eventos sobre como alterar o modo de exibição ou guias de coluna de atualização ou de redesenhada configurações alterando, conforme necessário.  
  
- Há um `GuidesSettingsManager` que lida com a leitura e gravação do armazenamento de configurações do Visual Studio. O Gerenciador de configurações também oferece operações para atualizar as configurações que dão suporte os comandos do usuário (Adicionar coluna, remova a coluna, alterar a cor).  
  
- Há um pacote do VSIP é necessário se você tiver os comandos do usuário, mas é apenas um código clichê que inicializa o objeto de implementação de comandos.  
  
- Há um `ColumnGuideCommands` comandos de objeto que executa o usuário e conecta os manipuladores de comandos para comandos declarados em de *VSCT* arquivo.  
  
  **VSIX**. Use **arquivo &#124; novo...**  comando para criar um projeto. Escolha o **extensibilidade** nó sob **c#** no painel de navegação à esquerda e escolha **projeto VSIX** no painel direito. Insira o nome **ColumnGuides** e escolha **Okey** para criar o projeto.  
  
  **Exibir adornos**. Pressione o botão direito do ponteiro no nó do projeto no Gerenciador de soluções. Escolha o **adicionar &#124; Novo Item...**  comando para adicionar um novo item do adorno de exibição. Escolher **extensibilidade &#124; Editor** no painel de navegação à esquerda e escolha **Editor de visor adorno** no painel direito. Insira o nome **ColumnGuideAdornment** como o item de nome e escolha **Add** para adicioná-lo.  
  
  Você pode ver este modelo de item adicionados dois arquivos ao projeto (bem como referências e assim por diante): **ColumnGuideAdornment.cs** e **ColumnGuideAdornmentTextViewCreationListener.cs**. Os modelos de desenhar um retângulo roxo no modo de exibição. Na seção a seguir, você pode alterar algumas linhas no ouvinte de criação da exibição e substitua o conteúdo do **ColumnGuideAdornment.cs**.  
  
  **Comandos**. Na **Gerenciador de soluções**, pressione o botão direito do ponteiro no nó do projeto. Escolha o **adicionar &#124; Novo Item...**  comando para adicionar um novo item do adorno de exibição. Escolher **extensibilidade &#124; VSPackage** no painel de navegação à esquerda e escolha **comando personalizado** no painel direito. Insira o nome **ColumnGuideCommands** como o item de nome e escolha **Add**. Além das várias referências, adicionando os comandos e o pacote também adicionada **ColumnGuideCommands.cs**, **ColumnGuideCommandsPackage.cs**, e **ColumnGuideCommandsPackage.vsct** . Na seção a seguir, você deve substituir o conteúdo dos arquivos primeiro e último para definir e implementar os comandos.  
  
## <a name="set-up-the-text-view-creation-listener"></a>Configurar o ouvinte de criação de exibição de texto  
 Abra *ColumnGuideAdornmentTextViewCreationListener.cs* no editor. Esse código implementa um manipulador para sempre que o Visual Studio cria os modos de exibição de texto. Há atributos que controlam quando o manipulador é chamado dependendo das características do modo de exibição.  
  
 O código também deve declarar uma camada de adorno. Quando o editor de modos de exibição de atualizações, ele obtém as camadas de adorno para o modo de exibição e de que obtém os elementos de adorno. Você pode declarar a ordenação de sua camada em relação a outras pessoas com atributos. Substitua a linha a seguir:  
  
```csharp  
[Order(After = PredefinedAdornmentLayers.Caret)]  
```  
  
 com estas duas linhas:  
  
```csharp  
[Order(Before = PredefinedAdornmentLayers.Text)]  
[TextViewRole(PredefinedTextViewRoles.Document)]  
```  
  
 A linha que foi substituído está em um grupo de atributos que declaram uma camada de adorno. A primeira linha em que você alterou apenas as alterações feitas em que as linhas de guia de coluna serão exibidas. Desenhar as linhas "antes" significa que o texto no modo de exibição aparecem acima ou abaixo do texto. A segunda linha declara que os adornos de guia de coluna são aplicáveis às entidades de texto que se ajustam a noção de um documento, mas você poderia declarar o adorno, por exemplo, para funciona somente para texto editável. Há mais informações [pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)  
  
## <a name="implement-the-settings-manager"></a>Implementar o Gerenciador de configurações  
 Substitua o conteúdo do *GuidesSettingsManager.cs* com o código a seguir (explicado abaixo):  
  
```csharp  
using Microsoft.VisualStudio.Settings;  
using Microsoft.VisualStudio.Shell;  
using Microsoft.VisualStudio.Shell.Settings;  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Windows.Media;  
  
namespace ColumnGuides  
{  
    internal static class GuidesSettingsManager  
    {  
        // Because my code is always called from the UI thred, this succeeds.  
        internal static SettingsManager VsManagedSettingsManager =  
            new ShellSettingsManager(ServiceProvider.GlobalProvider);  
  
        private const int _maxGuides = 5;  
        private const string _collectionSettingsName = "Text Editor";  
        private const string _settingName = "Guides";  
        // 1000 seems reasonable since primary scenario is long lines of code  
        private const int _maxColumn = 1000;   
  
        static internal bool AddGuideline(int column)  
        {  
            if (! IsValidColumn(column))  
                throw new ArgumentOutOfRangeException(  
                    "column",  
                    "The paramenter must be between 1 and " + _maxGuides.ToString());  
            var offsets = GuidesSettingsManager.GetColumnOffsets();  
            if (offsets.Count() >= _maxGuides)  
                return false;  
            // Check for duplicates  
            if (offsets.Contains(column))  
                return false;  
            offsets.Add(column);  
            WriteSettings(GuidesSettingsManager.GuidelinesColor, offsets);  
            return true;  
        }  
  
        static internal bool RemoveGuideline(int column)  
        {  
            if (!IsValidColumn(column))  
                throw new ArgumentOutOfRangeException(  
                    "column", "The paramenter must be between 1 and 10,000");  
            var columns = GuidesSettingsManager.GetColumnOffsets();  
            if (! columns.Remove(column))  
            {  
                // Not present.  Allow user to remove the last column   
                // even if they're not on the right column.  
                if (columns.Count != 1)  
                    return false;  
  
                columns.Clear();  
            }  
            WriteSettings(GuidesSettingsManager.GuidelinesColor, columns);  
            return true;  
        }  
  
        static internal bool CanAddGuideline(int column)  
        {  
            if (!IsValidColumn(column))  
                return false;  
            var offsets = GetColumnOffsets();  
            if (offsets.Count >= _maxGuides)  
                return false;  
            return ! offsets.Contains(column);  
        }  
  
        static internal bool CanRemoveGuideline(int column)  
        {  
            if (! IsValidColumn(column))  
                return false;  
            // Allow user to remove the last guideline regardless of the column.  
            // Okay to call count, we limit the number of guides.  
            var offsets = GuidesSettingsManager.GetColumnOffsets();  
            return offsets.Contains(column) || offsets.Count() == 1;  
        }  
  
        static internal void RemoveAllGuidelines()  
        {  
            WriteSettings(GuidesSettingsManager.GuidelinesColor, new int[0]);  
        }  
  
        private static bool IsValidColumn(int column)  
        {  
            // zero is allowed (per user request)  
            return 0 <= column && column <= _maxColumn;  
        }  
  
        // This has format "RGB(<int>, <int>, <int>) <int> <int>...".  
        // There can be any number of ints following the RGB part,   
        // and each int is a column (char offset into line) where to draw.  
        static private string _guidelinesConfiguration;  
        static private string GuidelinesConfiguration  
        {  
            get  
            {  
                if (_guidelinesConfiguration == null)  
                {  
                    _guidelinesConfiguration =   
                        GetUserSettingsString(  
                            GuidesSettingsManager._collectionSettingsName,  
                            GuidesSettingsManager._settingName)  
                        .Trim();  
                }  
                return _guidelinesConfiguration;  
            }  
  
            set  
            {  
                if (value != _guidelinesConfiguration)  
                {  
                    _guidelinesConfiguration = value;  
                    WriteUserSettingsString(  
                        GuidesSettingsManager._collectionSettingsName,  
                        GuidesSettingsManager._settingName, value);  
                    // Notify ColumnGuideAdornments to update adornments in views.  
                    var handler = GuidesSettingsManager.SettingsChanged;  
                    if (handler != null)  
                        handler();  
                }  
            }  
        }  
  
        internal static string GetUserSettingsString(string collection, string setting)  
        {  
            var store = GuidesSettingsManager  
                            .VsManagedSettingsManager  
                            .GetReadOnlySettingsStore(SettingsScope.UserSettings);  
            return store.GetString(collection, setting, "RGB(255,0,0) 80");  
        }  
  
        internal static void WriteUserSettingsString(string key, string propertyName,  
                                                     string value)  
        {  
            var store = GuidesSettingsManager  
                            .VsManagedSettingsManager  
                            .GetWritableSettingsStore(SettingsScope.UserSettings);  
            store.CreateCollection(key);  
            store.SetString(key, propertyName, value);  
        }  
  
        // Persists settings and sets property with side effect of signaling  
        // ColumnGuideAdornments to update.  
        static private void WriteSettings(Color color, IEnumerable<int> columns)  
        {  
            string value = ComposeSettingsString(color, columns);  
            GuidelinesConfiguration = value;  
        }  
  
        private static string ComposeSettingsString(Color color,  
                                                    IEnumerable<int> columns)  
        {  
            StringBuilder sb = new StringBuilder();  
            sb.AppendFormat("RGB({0},{1},{2})", color.R, color.G, color.B);  
            IEnumerator<int> columnsEnumerator = columns.GetEnumerator();  
            if (columnsEnumerator.MoveNext())  
            {  
                sb.AppendFormat(" {0}", columnsEnumerator.Current);  
                while (columnsEnumerator.MoveNext())  
                {  
                    sb.AppendFormat(", {0}", columnsEnumerator.Current);  
                }  
            }  
            return sb.ToString();  
        }  
  
        // Parse a color out of a string that begins like "RGB(255,0,0)"  
        static internal Color GuidelinesColor  
        {  
            get  
            {  
                string config = GuidelinesConfiguration;  
                if (!String.IsNullOrEmpty(config) && config.StartsWith("RGB("))  
                {  
                    int lastParen = config.IndexOf(')');  
                    if (lastParen > 4)  
                    {  
                        string[] rgbs = config.Substring(4, lastParen - 4).Split(',');  
  
                        if (rgbs.Length >= 3)  
                        {  
                            byte r, g, b;  
                            if (byte.TryParse(rgbs[0], out r) &&  
                                byte.TryParse(rgbs[1], out g) &&  
                                byte.TryParse(rgbs[2], out b))  
                            {  
                                return Color.FromRgb(r, g, b);  
                            }  
                        }  
                    }  
                }  
                return Colors.DarkRed;  
            }  
  
            set  
            {  
                WriteSettings(value, GetColumnOffsets());  
            }  
        }  
  
        // Parse a list of integer values out of a string that looks like  
        // "RGB(255,0,0) 1, 5, 10, 80"  
        static internal List<int> GetColumnOffsets()  
        {  
            var result = new List<int>();  
            string settings = GuidesSettingsManager.GuidelinesConfiguration;  
            if (String.IsNullOrEmpty(settings))  
                return new List<int>();  
  
            if (!settings.StartsWith("RGB("))  
                return new List<int>();  
  
            int lastParen = settings.IndexOf(')');  
            if (lastParen <= 4)  
                return new List<int>();  
  
            string[] columns = settings.Substring(lastParen + 1).Split(',');  
  
            int columnCount = 0;  
            foreach (string columnText in columns)  
            {  
                int column = -1;  
                // VS 2008 gallery extension didn't allow zero, so per user request ...  
                if (int.TryParse(columnText, out column) && column >= 0)  
                {  
                    columnCount++;  
                    result.Add(column);  
                    if (columnCount >= _maxGuides)  
                        break;  
                }  
            }  
            return result;  
        }  
  
        // Delegate and Event to fire when settings change so that ColumnGuideAdornments   
        // can update.  We need nothing special in this event since the settings manager   
        // is statically available.  
        //  
        internal delegate void SettingsChangedHandler();  
        static internal event SettingsChangedHandler SettingsChanged;  
  
    }  
}  
  
```  
  
 A maioria desse código cria e analisa o formato de configurações: "RGB (\<int >,\<int >,\<int >) \<int >, \<int >,...".  Os inteiros no final são as colunas com base em um onde você deseja que os guias de coluna. A extensão de guias de coluna captura todas as suas configurações em uma cadeia de caracteres do valor de configuração única.  
  
 Há algumas partes do código que vale a pena realce. A seguinte linha de código obtém o wrapper gerenciado do Visual Studio para o armazenamento de configurações. Geralmente, isso abstrai sobre o registro do Windows, mas essa API é independente do mecanismo de armazenamento.  
  
```csharp  
internal static SettingsManager VsManagedSettingsManager =  
    new ShellSettingsManager(ServiceProvider.GlobalProvider);  
```  
  
 O armazenamento de configurações do Visual Studio usa um identificador de categoria e um identificador de configuração para identificar exclusivamente a todas as configurações:  
  
```csharp  
private const string _collectionSettingsName = "Text Editor";  
private const string _settingName = "Guides";  
```  
  
 Você não precisa usar `"Text Editor"` como o nome da categoria. Você pode escolher que desejar.  
  
 As primeiro algumas funções são os pontos de entrada para alterar as configurações. Eles verificam as restrições de alto nível, como o número máximo permitido de guias.  Em seguida, eles chamam `WriteSettings`, que compõe uma cadeia de caracteres de configurações e define a propriedade `GuideLinesConfiguration`. A definição dessa propriedade salva o valor de configurações para o armazenamento de configurações do Visual Studio e aciona o `SettingsChanged` eventos para atualizar todos os o `ColumnGuideAdornment` objetos, cada um associado com uma exibição de texto.  
  
 Existem algumas funções de ponto de entrada, tais como `CanAddGuideline`, que são usados para implementar os comandos que alteram as configurações. Quando o Visual Studio mostra menus, ele consulta as implementações de comando para ver se o comando é habilitado no momento, o que é seu nome e assim por diante.  Abaixo, você verá como conectar esses pontos de entrada para as implementações de comando. Para obter mais informações sobre comandos, consulte [estendem os menus e comandos](../extensibility/extending-menus-and-commands.md).  
  
## <a name="implement-the-columnguideadornment-class"></a>Implementar a classe ColumnGuideAdornment  
 O `ColumnGuideAdornment` classe é instanciada para cada modo de exibição de texto que pode ter adornos. Essa classe de escuta para eventos sobre como alterar o modo de exibição ou a alteração de configurações e os guias de coluna de atualização ou de redesenho conforme necessário.  
  
 Substitua o conteúdo do *ColumnGuideAdornment.cs* com o código a seguir (explicado abaixo):  
  
```csharp  
using System;  
using System.Windows.Media;  
using Microsoft.VisualStudio.Text.Editor;  
using System.Collections.Generic;  
using System.Windows.Shapes;  
using Microsoft.VisualStudio.Text.Formatting;  
using System.Windows;  
  
namespace ColumnGuides  
{  
    /// <summary>  
    /// Adornment class, one instance per text view that draws a guides on the viewport  
    /// </summary>  
    internal sealed class ColumnGuideAdornment  
    {  
        private const double _lineThickness = 1.0;  
        private IList<Line> _guidelines;  
        private IWpfTextView _view;  
        private double _baseIndentation;  
        private double _columnWidth;  
  
        /// <summary>  
        /// Creates editor column guidelines  
        /// </summary>  
        /// <param name="view">The <see cref="IWpfTextView"/> upon   
        /// which the adornment will be drawn</param>  
        public ColumnGuideAdornment(IWpfTextView view)  
        {  
            _view = view;  
            _guidelines = CreateGuidelines();  
            GuidesSettingsManager.SettingsChanged +=   
                new GuidesSettingsManager.SettingsChangedHandler(SettingsChanged);  
            view.LayoutChanged +=   
                new EventHandler<TextViewLayoutChangedEventArgs>(OnViewLayoutChanged);  
            _view.Closed += new EventHandler(OnViewClosed);  
        }  
  
        void SettingsChanged()  
        {  
            _guidelines = CreateGuidelines();  
            UpdatePositions();  
            AddGuidelinesToAdornmentLayer();  
        }  
  
        void OnViewClosed(object sender, EventArgs e)  
        {  
            _view.LayoutChanged -= OnViewLayoutChanged;  
            _view.Closed -= OnViewClosed;  
            GuidesSettingsManager.SettingsChanged -= SettingsChanged;  
        }  
  
        private bool _firstLayoutDone;  
  
        void OnViewLayoutChanged(object sender, TextViewLayoutChangedEventArgs e)  
        {  
            bool fUpdatePositions = false;  
  
            IFormattedLineSource lineSource = _view.FormattedLineSource;  
            if (lineSource == null)  
            {  
                return;  
            }  
            if (_columnWidth != lineSource.ColumnWidth)  
            {  
                _columnWidth = lineSource.ColumnWidth;  
                fUpdatePositions = true;  
            }  
            if (_baseIndentation != lineSource.BaseIndentation)  
            {  
                _baseIndentation = lineSource.BaseIndentation;  
                fUpdatePositions = true;  
            }  
            if (fUpdatePositions ||  
                e.VerticalTranslation ||  
                e.NewViewState.ViewportTop != e.OldViewState.ViewportTop ||  
                e.NewViewState.ViewportBottom != e.OldViewState.ViewportBottom)  
            {  
                UpdatePositions();  
            }  
            if (!_firstLayoutDone)  
            {  
                AddGuidelinesToAdornmentLayer();  
                _firstLayoutDone = true;  
            }  
        }  
  
        private static IList<Line> CreateGuidelines()  
        {  
            Brush lineBrush = new SolidColorBrush(GuidesSettingsManager.GuidelinesColor);  
            DoubleCollection dashArray = new DoubleCollection(new double[] { 1.0, 3.0 });  
            IList<Line> result = new List<Line>();  
            foreach (int column in GuidesSettingsManager.GetColumnOffsets())  
            {  
                Line line = new Line()  
                {  
                    // Use the DataContext slot as a cookie to hold the column  
                    DataContext = column,  
                    Stroke = lineBrush,  
                    StrokeThickness = _lineThickness,  
                    StrokeDashArray = dashArray  
                };  
                result.Add(line);  
            }  
            return result;  
        }  
  
        void UpdatePositions()  
        {  
            foreach (Line line in _guidelines)  
            {  
                int column = (int)line.DataContext;  
                line.X2 = _baseIndentation + 0.5 + column * _columnWidth;  
                line.X1 = line.X2;  
                line.Y1 = _view.ViewportTop;  
                line.Y2 = _view.ViewportBottom;  
            }  
        }  
  
        void AddGuidelinesToAdornmentLayer()  
        {  
            // Grab a reference to the adornment layer that this adornment   
            // should be added to  
            // Must match exported name in ColumnGuideAdornmentTextViewCreationListener  
            IAdornmentLayer adornmentLayer =   
                _view.GetAdornmentLayer("ColumnGuideAdornment");  
            if (adornmentLayer == null)  
                return;  
            adornmentLayer.RemoveAllAdornments();  
            // Add the guidelines to the adornment layer and make them relative   
            // to the viewport  
            foreach (UIElement element in _guidelines)  
                adornmentLayer.AddAdornment(AdornmentPositioningBehavior.OwnerControlled,  
                                            null, null, element, null);  
        }  
    }  
  
}  
```  
  
 As instâncias dessa classe mantêm associado <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> e uma lista de `Line` objetos desenhados na exibição.  
  
 O construtor (chamado de `ColumnGuideAdornmentTextViewCreationListener` quando o Visual Studio cria novos modos de exibição) cria o guia de coluna `Line` objetos.  O construtor também adiciona manipuladores para o `SettingsChanged` evento (definidos no `GuidesSettingsManager`) e os eventos de exibição `LayoutChanged` e `Closed`.  
  
 O `LayoutChanged` evento aciona devido a vários tipos de alterações no modo de exibição, incluindo quando o Visual Studio cria o modo de exibição. O `OnViewLayoutChanged` chamadas do manipulador `AddGuidelinesToAdornmentLayer` para executar. O código no `OnViewLayoutChanged` determina se é necessário atualizar as posições de linhas com base nas alterações, como alterações de tamanho de fonte, medianizes do modo de exibição, a rolagem horizontal e assim por diante. O código em `UpdatePositions` faz com que as linhas de guia desenhar entre caracteres ou logo após a coluna de texto que está no deslocamento de caractere especificado na linha de texto.  
  
 Sempre que alterar as configurações a `SettingsChanged` função apenas recria todos os `Line` objetos com que as novas configurações estão. Depois de definir as posições de linha, o código remove todos os últimos `Line` objetos do `ColumnGuideAdornment` camada de adorno e adiciona as novas.  
  
## <a name="define-the-commands-menus-and-menu-placements"></a>Definir os comandos, menus e posicionamentos de menu  
 Pode haver muito declarando menus e comandos, colocando os grupos de comandos ou menus em vários outros menus e vinculando manipuladores de comandos. Este passo a passo que destaca como os comandos funcionam nesta extensão, mas para obter mais informações, consulte [estendem os menus e comandos](../extensibility/extending-menus-and-commands.md).  
  
### <a name="introduction-to-the-code"></a>Introdução ao código  
 A extensão de guias de coluna mostra a declaração de um grupo de comandos que pertencem juntas (Adicionar coluna, remova a coluna, alterar a cor da linha) e, em seguida, colocar esse grupo em um submenu do menu de contexto do editor.  A extensão de guias de coluna também adiciona os comandos ao principal **editar** menu, mas manterá invisível, abordamos como um padrão comum abaixo.  
  
 Há três partes para a implementação de comandos: ColumnGuideCommandsPackage.cs, ColumnGuideCommandsPackage.vsct e ColumnGuideCommands.cs. O código gerado pelos modelos coloca um comando na **ferramentas** menu que aparece uma caixa de diálogo como a implementação. Você pode examinar como que é implementado na *VSCT* e *ColumnGuideCommands.cs* arquivos, pois ele é simples. Você substitua o código nesses arquivos abaixo.  
  
 O código de pacote contém declarações de texto clichê necessárias para o Visual Studio para descobrir a extensão oferece comandos e localizar onde colocar os comandos. Quando o pacote for inicializado, ele instancia a classe de implementação de comandos. Para obter mais informações sobre os pacotes relacionados aos comandos, consulte [estendem os menus e comandos](../extensibility/extending-menus-and-commands.md).  
  
### <a name="a-common-commands-pattern"></a>Um padrão comum de comandos  
 Os comandos na extensão de guias de coluna são um exemplo de um padrão muito comum no Visual Studio. Coloque os comandos relacionados em um grupo, e você coloque esse grupo em um menu principal, geralmente com "`<CommandFlag>CommandWellOnly</CommandFlag>`" definida para tornar o comando invisível.  Colocar comandos nos menus principais (como **editar**) fornece a eles nomes BOM (como **Edit.AddColumnGuide**), que são úteis para localizar os comandos ao atribuir novamente as associações de teclas no **ferramentas Opções de**. Também é útil para obtenção de conclusão ao invocar comandos a partir de **janela de comando**.  
  
 Você, em seguida, adicione o grupo de comandos a menus de contexto ou sub em que você espera que o usuário use os comandos de menus. O Visual Studio trata `CommandWellOnly` como um sinalizador de invisibilidade de menus principais somente. Quando você coloca o mesmo grupo de comandos em um menu de contexto ou o submenu, os comandos são visíveis.  
  
 Como parte do padrão comum, a extensão de guias de coluna cria um segundo grupo que contém um único submenu. Por sua vez, o submenu contém o grupo primeiro com os comandos do guia de quatro colunas. O segundo grupo que contém o submenu é ativos reutilizáveis que você coloca nos vários menus de contexto, que coloca um submenu nesses menus de contexto.  
  
### <a name="the-vsct-file"></a>O arquivo. VSCT  
 O *VSCT* arquivo declara os comandos e onde eles acompanharem, ícones e assim por diante. Substitua o conteúdo do *VSCT* arquivo pelo código a seguir (explicado abaixo):  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  
  <!--  This is the file that defines the actual layout and type of the commands.  
        It is divided in different sections (e.g. command definition, command  
        placement, ...), with each defining a specific set of properties.  
        See the comment before each section for more details about how to  
        use it. -->  
  
  <!--  The VSCT compiler (the tool that translates this file into the binary  
        format that VisualStudio will consume) has the ability to run a preprocessor  
        on the vsct file; this preprocessor is (usually) the C++ preprocessor, so  
        it is possible to define includes and macros with the same syntax used  
        in C++ files. Using this ability of the compiler here, we include some files  
        defining some of the constants that we will use inside the file. -->  
  
  <!--This is the file that defines the IDs for all the commands exposed by   
      VisualStudio. -->  
  <Extern href="stdidcmd.h"/>  
  
  <!--This header contains the command ids for the menus provided by the shell. -->  
  <Extern href="vsshlids.h"/>  
  
  <!--The Commands section is where commands, menus, and menu groups are defined.  
      This section uses a Guid to identify the package that provides the command   
      defined inside it. -->  
  <Commands package="guidColumnGuideCommandsPkg">  
    <!-- Inside this section we have different sub-sections: one for the menus, another    
    for the menu groups, one for the buttons (the actual commands), one for the combos   
    and the last one for the bitmaps used. Each element is identified by a command id  
    that is a unique pair of guid and numeric identifier; the guid part of the identifier  
    is usually called "command set" and is used to group different command inside a  
    logically related group; your package should define its own command set in order to  
    avoid collisions with command ids defined by other packages. -->  
  
    <!-- In this section you can define new menu groups. A menu group is a container for   
         other menus or buttons (commands); from a visual point of view you can see the   
         group as the part of a menu contained between two lines. The parent of a group   
         must be a menu. -->  
    <Groups>  
  
      <!-- The main group is parented to the edit menu. All the buttons within the group  
           have the "CommandWellOnly" flag, so they're actually invisible, but it means  
           they get canonical names that begin with "Edit". Using placements, the group  
           is also placed in the GuidesSubMenu group. -->  
      <!-- The priority 0xB801 is chosen so it goes just after   
           IDG_VS_EDIT_COMMANDWELL -->  
      <Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"  
             priority="0xB801">  
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />  
      </Group>  
  
      <!-- Group for holding the "Guidelines" sub-menu anchor (the item on the menu that  
           drops the sub menu). The group is parented to  
           the context menu for code windows. That takes care of most editors, but it's  
           also placed in a couple of other windows using Placements -->  
      <Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"   
             priority="0x0600">  
        <Parent guid="guidSHLMainMenu" id="IDM_VS_CTXT_CODEWIN" />  
      </Group>  
  
    </Groups>  
  
    <Menus>  
      <Menu guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" priority="0x1000"  
            type="Menu">  
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup" />  
        <Strings>  
          <ButtonText>&Column Guides</ButtonText>  
        </Strings>  
      </Menu>  
    </Menus>  
  
    <!--Buttons section. -->  
    <!--This section defines the elements the user can interact with, like a menu command or a button   
        or combo box in a toolbar. -->  
    <Buttons>  
      <!--To define a menu group you have to specify its ID, the parent menu and its   
          display priority.   
          The command is visible and enabled by default. If you need to change the   
          visibility, status, etc, you can use the CommandFlag node.  
          You can add more than one CommandFlag node e.g.:  
              <CommandFlag>DefaultInvisible</CommandFlag>  
              <CommandFlag>DynamicVisibility</CommandFlag>  
          If you do not want an image next to your command, remove the Icon node or   
          set it to <Icon guid="guidOfficeIcon" id="msotcidNoIcon" /> -->  
  
      <Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"   
              priority="0x0100" type="Button">  
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />  
        <Icon guid="guidImages" id="bmpPicAddGuide" />  
        <CommandFlag>CommandWellOnly</CommandFlag>  
        <CommandFlag>AllowParams</CommandFlag>  
        <Strings>  
          <ButtonText>&Add Column Guide</ButtonText>  
        </Strings>  
      </Button>  
  
      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveColumnGuide"   
              priority="0x0101" type="Button">  
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />  
        <Icon guid="guidImages" id="bmpPicRemoveGuide" />  
        <CommandFlag>CommandWellOnly</CommandFlag>  
        <CommandFlag>AllowParams</CommandFlag>  
        <Strings>  
          <ButtonText>&Remove Column Guide</ButtonText>  
        </Strings>  
      </Button>  
  
      <Button guid="guidColumnGuidesCommandSet" id="cmdidChooseGuideColor"   
              priority="0x0103" type="Button">  
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />  
        <Icon guid="guidImages" id="bmpPicChooseColor" />  
        <CommandFlag>CommandWellOnly</CommandFlag>  
        <Strings>  
          <ButtonText>Column Guide &Color...</ButtonText>  
        </Strings>  
      </Button>  
  
      <Button guid="guidColumnGuidesCommandSet" id="cmdidRemoveAllColumnGuides"   
              priority="0x0102" type="Button">  
        <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />  
        <CommandFlag>CommandWellOnly</CommandFlag>  
        <Strings>  
          <ButtonText>Remove A&ll Columns</ButtonText>  
        </Strings>  
      </Button>  
    </Buttons>  
  
    <!--The bitmaps section is used to define the bitmaps that are used for the  
        commands.-->  
    <Bitmaps>  
      <!--  The bitmap id is defined in a way that is a little bit different from the  
            others:   
            the declaration starts with a guid for the bitmap strip, then there is the  
            resource id of the bitmap strip containing the bitmaps and then there are   
            the numeric ids of the elements used inside a button definition. An important  
            aspect of this declaration is that the element id   
            must be the actual index (1-based) of the bitmap inside the bitmap strip. -->  
      <Bitmap guid="guidImages" href="Resources\ColumnGuideCommands.png"   
              usedList="bmpPicAddGuide, bmpPicRemoveGuide, bmpPicChooseColor" />  
    </Bitmaps>  
  
  </Commands>  
  
  <CommandPlacements>  
  
    <!-- Define secondary placements for our groups -->  
  
    <!-- Place the group containing the three commands in the sub-menu -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"   
                      priority="0x0100">  
      <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />  
    </CommandPlacement>  
  
    <!-- The HTML editor context menu, for some reason, redefines its own groups  
         so we need to place a copy of our context menu there too. -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"   
                      priority="0x1001">  
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_HTML" />  
    </CommandPlacement>  
  
    <!-- The HTML context menu in Dev12 changed. -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"   
                      priority="0x1001">  
      <Parent guid="CMDSETID_HtmEdGrp_Dev12" id="IDMX_HTM_SOURCE_HTML_Dev12" />  
    </CommandPlacement>  
  
    <!-- Similarly for Script -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"  
                      priority="0x1001">  
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_SCRIPT" />  
    </CommandPlacement>  
  
    <!-- Similarly for ASPX  -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"   
                      priority="0x1001">  
      <Parent guid="CMDSETID_HtmEdGrp" id="IDMX_HTM_SOURCE_ASPX" />  
    </CommandPlacement>  
  
    <!-- Similarly for the XAML editor context menu -->  
    <CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"  
                      priority="0x0600">  
      <Parent guid="guidXamlUiCmds" id="IDM_XAML_EDITOR" />  
    </CommandPlacement>  
  
  </CommandPlacements>  
  
  <!-- This defines the identifiers and their values used above to index resources  
       and specify commands. -->  
  <Symbols>  
    <!-- This is the package guid. -->  
    <GuidSymbol name="guidColumnGuideCommandsPkg"   
                value="{e914e5de-0851-4904-b361-1a3a9d449704}" />  
  
    <!-- This is the guid used to group the menu commands together -->  
    <GuidSymbol name="guidColumnGuidesCommandSet"   
                value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">  
      <IDSymbol name="GuidesContextMenuGroup" value="0x1020" />  
      <IDSymbol name="GuidesMenuItemsGroup" value="0x1021" />  
      <IDSymbol name="GuidesSubMenu" value="0x1022" />  
      <IDSymbol name="cmdidAddColumnGuide" value="0x0100" />  
      <IDSymbol name="cmdidRemoveColumnGuide" value="0x0101" />  
      <IDSymbol name="cmdidChooseGuideColor" value="0x0102" />  
      <IDSymbol name="cmdidRemoveAllColumnGuides" value="0x0103" />  
    </GuidSymbol>  
  
    <GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">  
      <IDSymbol name="bmpPicAddGuide" value="1" />  
      <IDSymbol name="bmpPicRemoveGuide" value="2" />  
      <IDSymbol name="bmpPicChooseColor" value="3" />  
    </GuidSymbol>  
  
    <GuidSymbol name="CMDSETID_HtmEdGrp_Dev12"   
                value="{78F03954-2FB8-4087-8CE7-59D71710B3BB}">  
      <IDSymbol name="IDMX_HTM_SOURCE_HTML_Dev12" value="0x1" />  
    </GuidSymbol>  
  
    <GuidSymbol name="CMDSETID_HtmEdGrp" value="{d7e8c5e1-bdb8-11d0-9c88-0000f8040a53}">  
      <IDSymbol name="IDMX_HTM_SOURCE_HTML" value="0x33" />  
      <IDSymbol name="IDMX_HTM_SOURCE_SCRIPT" value="0x34" />  
      <IDSymbol name="IDMX_HTM_SOURCE_ASPX" value="0x35" />  
    </GuidSymbol>  
  
    <GuidSymbol name="guidXamlUiCmds" value="{4c87b692-1202-46aa-b64c-ef01faec53da}">  
      <IDSymbol name="IDM_XAML_EDITOR" value="0x103" />  
    </GuidSymbol>  
  </Symbols>  
  
</CommandTable>  
  
```  
  
 **GUIDS**. Para o Visual Studio localizar seus manipuladores de comandos e invocá-los, você precisa garantir que o GUID declarado no pacote do *ColumnGuideCommandsPackage.cs* (gerado a partir do modelo de item de projeto) do arquivo corresponde ao GUID declarado no pacote o *VSCT* arquivo (copiado acima). Se você reutilizar esse código de exemplo, certifique-se de que ter um GUID diferente para que você não entrem em conflito com qualquer pessoa que copiou esse código.  
  
 Localize esta linha na *ColumnGuideCommandsPackage.cs* e copie o GUID do intervalo entre as aspas:  
  
```csharp  
public const string PackageGuidString = "ef726849-5447-4f73-8de5-01b9e930f7cd";  
```  
  
 Em seguida, cole o GUID na *VSCT* de arquivo para que você tenha a seguinte linha seu `Symbols` declarações:  
  
```xml  
<GuidSymbol name="guidColumnGuideCommandsPkg"   
            value="{ef726849-5447-4f73-8de5-01b9e930f7cd}" />  
```  
  
 Defina os GUIDs para o comando e o arquivo de imagem de bitmap deve ser exclusivo para suas extensões muito:  
  
```xml  
<GuidSymbol name="guidColumnGuidesCommandSet"   
            value="{c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e}">  
<GuidSymbol name="guidImages" value="{2C99F852-587C-43AF-AA2D-F605DE2E46EF}">  
```  
  
 Mas, você não precisa alterar o conjunto de comandos e GUIDs de imagem neste passo a passo para obter o código funcione de bitmap. O conjunto de comandos GUID precisa coincidir com a declaração de *ColumnGuideCommands.cs* arquivo, mas você substitua o conteúdo do arquivo, muito; portanto, os GUIDs fará a correspondência.  
  
 Outros GUIDs na *VSCT* arquivo identificar menus já existentes para o qual os comandos de guia de coluna são adicionados, para que eles nunca alterar.  
  
 **Seções do arquivo**. O *VSCT* possui três seções externas: comandos, posicionamentos e símbolos. A seção de comandos define grupos de comando, menus, botões ou itens de menu e bitmaps para ícones. A seção de posicionamentos declara onde grupos ir em menus ou posicionamentos adicionais em menus já existentes. Seção símbolos declara identificadores usados em outro lugar na *. VSCT* arquivo, o que torna o *VSCT* código mais legível do que GUIDs e hex números em todos os lugares.  
  
 **Seção de comandos, agrupa as definições de**. A seção comandos primeiro define grupos de comando. Os grupos de comandos são comandos que você vê nos menus com pequenas linhas cinzas, separando os grupos. Um grupo também pode preencher um menu inteiro sub, como neste exemplo, e você não vir a cinza a separação de linhas nesse caso. O *VSCT* arquivos declarar dois grupos, o `GuidesMenuItemsGroup` que é o pai para o `IDM_VS_MENU_EDIT` (principal **editar** menu) e o `GuidesContextMenuGroup` que é o pai para o `IDM_VS_CTXT_CODEWIN` (o código menu de contexto do Editor).  
  
 A segunda declaração de grupo tem um `0x0600` prioridade:  
  
```xml  
<Group guid="guidColumnGuidesCommandSet" id="GuidesContextMenuGroup"   
             priority="0x0600">  
```  
  
 A ideia é colocar a coluna orienta o submenu do final de qualquer menu de contexto para o qual você adiciona o grupo de menus do sub. Mas, você não deve supor que você conhece melhor e força o submenu para sempre ser o último por meio de uma prioridade de `0xFFFF`. Você precisa fazer experiências com o número para ver onde seu submenu reside nos menus de contexto onde colocá-lo. Nesse caso, `0x0600` é alto o suficiente para colocá-lo no final dos menus que você pode ver, mas deixa espaço para outra pessoa para projetar a sua extensão para ser menor do que a extensão de guias de coluna se for desejável.  
  
 **Seção, definição de menu comandos**. Em seguida, a seção de comando define o submenu `GuidesSubMenu`, o pai para o `GuidesContextMenuGroup`. O `GuidesContextMenuGroup` é o grupo que você adicionar a todos os menus de contexto relevante. Na seção de posicionamentos, o código coloca o grupo com os comandos do guia de quatro colunas nesse menu sub.  
  
 **Seção de comandos, botões definições**. A seção de comandos, em seguida, define os itens de menu ou botões que são os comandos de guias de quatro colunas. `CommandWellOnly`, discutidas acima, significa que os comandos são invisíveis quando colocada em um menu principal. Dois do item de menu botões declarações (Adicionar guia e remover guia) também têm um `AllowParams` sinalizador:  
  
```xml  
<CommandFlag>AllowParams</CommandFlag>  
```  
  
 Esse sinalizador habilita, juntamente com o posicionamento do menu principal, o comando para receber argumentos quando o Visual Studio chama o manipulador de comandos.  Se o usuário executa o comando na janela de comando, o argumento é passado para o manipulador de comandos no evento argumentos.  
  
 **Seções de comando, definições de bitmaps**. Por fim, a seção comandos declara os bitmaps ou ícones usados para os comandos. Esta seção é uma declaração simples que identifica o recurso do projeto e a lista de índices com base em um dos ícones usados. Seção símbolos do *VSCT* arquivo declara os valores dos identificadores usados como índices. Este passo a passo usa a faixa de bitmap fornecida com o modelo de item de comando personalizado adicionado ao projeto.  
  
 **Seção de posicionamentos**. Após os comandos a seção é a seção de posicionamentos. O primeiro é onde o código adiciona o primeiro grupo discutido acima que contém o guia de quatro colunas comandos ao menu sub no qual os comandos são exibidos:  
  
```xml  
<CommandPlacement guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"   
                  priority="0x0100">  
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesSubMenu" />  
</CommandPlacement>  
```  
  
 Todos os outros posicionamentos adicionar o `GuidesContextMenuGroup` (que contém o `GuidesSubMenu`) para outros menus de contexto do editor. Quando o código declarado o `GuidesContextMenuGroup`, ele era um pai ao menu de contexto do editor de código. É por isso que você não vir um posicionamento para o menu de contexto do editor de código.  
  
 **Símbolos seção**. Como mencionado acima, a seção símbolos declara identificadores usados em outro lugar na *. VSCT* arquivo, o que torna o *. VSCT* código mais legível do que GUIDs e hex números em todos os lugares. Os pontos importantes nesta seção são que o GUID do pacote deve concordar com a declaração de classe de pacote. E o conjunto de comandos que GUID deve concordar com a declaração na classe de implementação do comando.  
  
## <a name="implement-the-commands"></a>Implementar os comandos  
 O *ColumnGuideCommands.cs* arquivo implementa os comandos e conecta os manipuladores. Quando o Visual Studio carrega o pacote e a inicializa, por sua vez chama o pacote `Initialize` na classe de implementação de comandos. A inicialização de comandos simplesmente instancia a classe e o construtor conecta todos os manipuladores de comando.  
  
 Substitua o conteúdo do *ColumnGuideCommands.cs* arquivo pelo código a seguir (explicado abaixo):  
  
```csharp  
using System;  
using System.ComponentModel.Design;  
using System.Globalization;  
using Microsoft.VisualStudio.Shell;  
using Microsoft.VisualStudio.Shell.Interop;  
using Microsoft.VisualStudio.TextManager.Interop;  
using Microsoft.VisualStudio.Text.Editor;  
using Microsoft.VisualStudio;  
  
namespace ColumnGuides  
{  
    /// <summary>  
    /// Command handler  
    /// </summary>  
    internal sealed class ColumnGuideCommands  
    {  
  
        const int cmdidAddColumnGuide = 0x0100;  
        const int cmdidRemoveColumnGuide = 0x0101;  
        const int cmdidChooseGuideColor = 0x0102;  
        const int cmdidRemoveAllColumnGuides = 0x0103;  
  
        /// <summary>  
        /// Command menu group (command set GUID).  
        /// </summary>  
        static readonly Guid CommandSet =   
            new Guid("c2bc0047-8bfa-4e5a-b5dc-45af8c274d8e");  
  
        /// <summary>  
        /// VS Package that provides this command, not null.  
        /// </summary>  
        private readonly Package package;  
  
        OleMenuCommand _addGuidelineCommand;  
        OleMenuCommand _removeGuidelineCommand;  
  
        /// <summary>  
        /// Initializes the singleton instance of the command.  
        /// </summary>  
        /// <param name="package">Owner package, not null.</param>  
        public static void Initialize(Package package)  
        {  
            Instance = new ColumnGuideCommands(package);  
        }  
  
        /// <summary>  
        /// Gets the instance of the command.  
        /// </summary>  
        public static ColumnGuideCommands Instance  
        {  
            get;  
            private set;  
        }  
  
        /// <summary>  
        /// Initializes a new instance of the <see cref="ColumnGuideCommands"/> class.  
        /// Adds our command handlers for menu (commands must exist in the command   
        /// table file)  
        /// </summary>  
        /// <param name="package">Owner package, not null.</param>  
        private ColumnGuideCommands(Package package)  
        {  
            if (package == null)  
            {  
                throw new ArgumentNullException("package");  
            }  
  
            this.package = package;  
  
            // Add our command handlers for menu (commands must exist in the .vsct file)  
  
            OleMenuCommandService commandService =  
                this.ServiceProvider.GetService(typeof(IMenuCommandService))  
                    as OleMenuCommandService;  
            if (commandService != null)  
            {  
                // Add guide  
                _addGuidelineCommand =   
                    new OleMenuCommand(AddColumnGuideExecuted, null,  
                                       AddColumnGuideBeforeQueryStatus,  
                                       new CommandID(ColumnGuideCommands.CommandSet,  
                                                     cmdidAddColumnGuide));  
                _addGuidelineCommand.ParametersDescription = "<column>";  
                commandService.AddCommand(_addGuidelineCommand);  
                // Remove guide  
                _removeGuidelineCommand =  
                    new OleMenuCommand(RemoveColumnGuideExecuted, null,  
                                       RemoveColumnGuideBeforeQueryStatus,  
                                       new CommandID(ColumnGuideCommands.CommandSet,  
                                                     cmdidRemoveColumnGuide));  
                _removeGuidelineCommand.ParametersDescription = "<column>";  
                commandService.AddCommand(_removeGuidelineCommand);  
                // Choose color  
                commandService.AddCommand(  
                    new MenuCommand(ChooseGuideColorExecuted,  
                                    new CommandID(ColumnGuideCommands.CommandSet,  
                                                  cmdidChooseGuideColor)));  
                // Remove all  
                commandService.AddCommand(  
                    new MenuCommand(RemoveAllGuidelinesExecuted,  
                                    new CommandID(ColumnGuideCommands.CommandSet,  
                                                  cmdidRemoveAllColumnGuides)));  
            }  
        }  
  
        /// <summary>  
        /// Gets the service provider from the owner package.  
        /// </summary>  
        private IServiceProvider ServiceProvider  
        {  
            get  
            {  
                return this.package;  
            }  
        }  
  
        private void AddColumnGuideBeforeQueryStatus(object sender, EventArgs e)  
        {  
            int currentColumn = GetCurrentEditorColumn();  
            _addGuidelineCommand.Enabled =  
                GuidesSettingsManager.CanAddGuideline(currentColumn);  
        }  
  
        private void RemoveColumnGuideBeforeQueryStatus(object sender, EventArgs e)  
        {  
            int currentColumn = GetCurrentEditorColumn();  
            _removeGuidelineCommand.Enabled =  
                GuidesSettingsManager.CanRemoveGuideline(currentColumn);  
        }  
  
        private int GetCurrentEditorColumn()  
        {  
            IVsTextView view = GetActiveTextView();  
            if (view == null)  
            {  
                return -1;  
            }  
  
            try  
            {  
                IWpfTextView textView = GetTextViewFromVsTextView(view);  
                int column = GetCaretColumn(textView);  
  
                // Note: GetCaretColumn returns 0-based positions. Guidelines are 1-based  
                // positions.  
                // However, do not subtract one here since the caret is positioned to the  
                // left of  
                // the given column and the guidelines are positioned to the right. We  
                // want the  
                // guideline to line up with the current caret position. e.g. When the  
                // caret is  
                // at position 1 (zero-based), the status bar says column 2. We want to  
                // add a  
                // guideline for column 1 since that will place the guideline where the  
                // caret is.  
                return column;  
            }  
            catch (InvalidOperationException)  
            {  
                return -1;  
            }  
        }  
  
        /// <summary>  
        /// Find the active text view (if any) in the active document.  
        /// </summary>  
        /// <returns>The IVsTextView of the active view, or null if there is no active  
        /// document or the  
        /// active view in the active document is not a text view.</returns>  
        private IVsTextView GetActiveTextView()  
        {  
            IVsMonitorSelection selection =  
                this.ServiceProvider.GetService(typeof(IVsMonitorSelection))  
                                                    as IVsMonitorSelection;  
            object frameObj = null;  
            ErrorHandler.ThrowOnFailure(  
                selection.GetCurrentElementValue(  
                    (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame, out frameObj));  
  
            IVsWindowFrame frame = frameObj as IVsWindowFrame;  
            if (frame == null)  
            {  
                return null;  
            }  
  
            return GetActiveView(frame);  
        }  
  
        private static IVsTextView GetActiveView(IVsWindowFrame windowFrame)  
        {  
            if (windowFrame == null)  
            {  
                throw new ArgumentException("windowFrame");  
            }  
  
            object pvar;  
            ErrorHandler.ThrowOnFailure(  
                windowFrame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView, out pvar));  
  
            IVsTextView textView = pvar as IVsTextView;  
            if (textView == null)  
            {  
                IVsCodeWindow codeWin = pvar as IVsCodeWindow;  
                if (codeWin != null)  
                {  
                    ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));  
                }  
            }  
            return textView;  
        }  
  
        private static IWpfTextView GetTextViewFromVsTextView(IVsTextView view)  
        {  
  
            if (view == null)  
            {  
                throw new ArgumentNullException("view");  
            }  
  
            IVsUserData userData = view as IVsUserData;  
            if (userData == null)  
            {  
                throw new InvalidOperationException();  
            }  
  
            object objTextViewHost;  
            if (VSConstants.S_OK  
                   != userData.GetData(Microsoft.VisualStudio  
                                                .Editor  
                                                .DefGuidList.guidIWpfTextViewHost,  
                                       out objTextViewHost))  
            {  
                throw new InvalidOperationException();  
            }  
  
            IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;  
            if (textViewHost == null)  
            {  
                throw new InvalidOperationException();  
            }  
  
            return textViewHost.TextView;  
        }  
  
        /// <summary>  
        /// Given an IWpfTextView, find the position of the caret and report its column  
        /// number. The column number is 0-based  
        /// </summary>  
        /// <param name="textView">The text view containing the caret</param>  
        /// <returns>The column number of the caret's position. When the caret is at the  
        /// leftmost column, the return value is zero.</returns>  
        private static int GetCaretColumn(IWpfTextView textView)  
        {  
            // This is the code the editor uses to populate the status bar.  
            Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =  
                textView.Caret.ContainingTextViewLine;  
            double columnWidth = textView.FormattedLineSource.ColumnWidth;  
            return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)  
                                       / columnWidth));  
        }  
  
        /// <summary>  
        /// Determine the applicable column number for an add or remove command.  
        /// The column is parsed from command arguments, if present. Otherwise  
        /// the current position of the caret is used to determine the column.  
        /// </summary>  
        /// <param name="e">Event args passed to the command handler.</param>  
        /// <returns>The column number. May be negative to indicate the column number is  
        /// unavailable.</returns>  
        /// <exception cref="ArgumentException">The column number parsed from event args  
        /// was not a valid integer.</exception>  
        private int GetApplicableColumn(EventArgs e)  
        {  
            var inValue = ((OleMenuCmdEventArgs)e).InValue as string;  
            if (!string.IsNullOrEmpty(inValue))  
            {  
                int column;  
                if (!int.TryParse(inValue, out column) || column < 0)  
                    throw new ArgumentException("Invalid column");  
                return column;  
            }  
  
            return GetCurrentEditorColumn();  
        }  
  
        /// <summary>  
        /// This function is the callback used to execute a command when the a menu item  
        /// is clicked. See the Initialize method to see how the menu item is associated  
        /// to this function using the OleMenuCommandService service and the MenuCommand  
        /// class.  
        /// </summary>  
        private void AddColumnGuideExecuted(object sender, EventArgs e)  
        {  
            int column = GetApplicableColumn(e);  
            if (column >= 0)  
            {  
                GuidesSettingsManager.AddGuideline(column);  
            }  
        }  
  
        private void RemoveColumnGuideExecuted(object sender, EventArgs e)  
        {  
            int column = GetApplicableColumn(e);  
            if (column >= 0)  
            {  
                GuidesSettingsManager.RemoveGuideline(column);  
            }  
        }  
  
        private void RemoveAllGuidelinesExecuted(object sender, EventArgs e)  
        {  
            GuidesSettingsManager.RemoveAllGuidelines();  
        }  
  
        private void ChooseGuideColorExecuted(object sender, EventArgs e)  
        {  
            System.Windows.Media.Color color = GuidesSettingsManager.GuidelinesColor;  
  
            using (System.Windows.Forms.ColorDialog picker =   
                new System.Windows.Forms.ColorDialog())  
            {  
                picker.Color = System.Drawing.Color.FromArgb(255, color.R, color.G,  
                                                             color.B);  
                if (picker.ShowDialog() == System.Windows.Forms.DialogResult.OK)  
                {  
                    GuidesSettingsManager.GuidelinesColor =   
                        System.Windows.Media.Color.FromRgb(picker.Color.R,  
                                                           picker.Color.G,   
                                                           picker.Color.B);  
                }  
            }  
        }  
  
    }  
}  
  
```  
  
 **Corrigir referências**. Está faltando uma referência neste momento. Pressione o botão direito do ponteiro no nó referências no Gerenciador de soluções. Escolha o **adicionar...**  comando.  O **adicionar referência** caixa de diálogo tem uma caixa de pesquisa no canto superior direito. Insira "editor" (sem as aspas duplas). Escolha o **Microsoft.VisualStudio.Editor** item (você deve marcar a caixa à esquerda do item, não basta selecionar o item) e escolha **Okey** para adicionar a referência.  
  
 **Inicialização**.  Quando a classe de pacote é inicializado, ele chama `Initialize` na classe de implementação de comandos. O `ColumnGuideCommands` instancia a classe de inicialização e salva a instância da classe e a referência de pacote em membros de classe.  
  
 Vamos examinar um dos gancho-ups de manipulador de comando do construtor da classe:  
  
```csharp  
_addGuidelineCommand =   
    new OleMenuCommand(AddColumnGuideExecuted, null,  
                       AddColumnGuideBeforeQueryStatus,  
                       new CommandID(ColumnGuideCommands.CommandSet,  
                                     cmdidAddColumnGuide));  
  
```  
  
 Você cria um `OleMenuCommand`. O Visual Studio usa o sistema de linha de comando do Microsoft Office. Os argumentos de chave ao instanciar um `OleMenuCommand` é a função que implementa o comando (`AddColumnGuideExecuted`), a função ser chamada quando o Visual Studio mostra um menu com o comando (`AddColumnGuideBeforeQueryStatus`) e a ID de comando. O Visual studio chama a função de status da consulta antes de mostrar um comando em um menu para que o comando pode tornar o próprio invisível ou esmaecido para um determinado vídeo do menu (por exemplo, desabilitando **cópia** se não houver nenhuma seleção), alterar seu ícone, ou até mesmo alterar seu nome (por exemplo, de adicionar algo para remover algo) e assim por diante. A ID de comando deve corresponder a um comando ID declarado na *VSCT* arquivo. As cadeias de caracteres para o conjunto de comandos e os guias de coluna adicionar comando deve ser correspondentes entre o *VSCT* arquivo e o *ColumnGuideCommands.cs*.  
  
 A linha a seguir fornece assistência para quando os usuários invocam o comando por meio da janela de comando (explicado abaixo):  
  
```csharp  
_addGuidelineCommand.ParametersDescription = "<column>";  
```  
  
 **Consultar status**. As funções de status de consulta `AddColumnGuideBeforeQueryStatus` e `RemoveColumnGuideBeforeQueryStatus` verificar algumas configurações (como o número máximo de guias ou coluna max) ou se há um guia de coluna a ser removido. Elas permitem os comandos se as condições forem atendidas.  Funções de consulta de status precisam ser eficiente, já que eles executam toda vez que o Visual Studio mostra um menu e para cada comando no menu.  
  
 **Função AddColumnGuideExecuted**. A parte interessante da adição de um guia é descobrir o local atual de modo de exibição e o cursor do editor.  Em primeiro lugar, essa função chama `GetApplicableColumn`, que verifica se há um argumento fornecido pelo usuário em argumentos de evento do manipulador de comandos e, se não houver nenhum, a função verifica a exibição do editor:  
  
```csharp  
private int GetApplicableColumn(EventArgs e)  
{  
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;  
    if (!string.IsNullOrEmpty(inValue))  
    {  
        int column;  
        if (!int.TryParse(inValue, out column) || column < 0)  
            throw new ArgumentException("Invalid column");  
        return column;  
    }  
  
    return GetCurrentEditorColumn();  
}  
  
```  
  
 `GetCurrentEditorColumn` tem se aprofundar um pouco para obter um <xref:Microsoft.VisualStudio.Text.Editor.IWpfTextView> exibição do código.  Se você rastrear por meio `GetActiveTextView`, `GetActiveView`, e `GetTextViewFromVsTextView`, você pode ver como fazer isso. O código a seguir está o código relevante abstraído, começando com a seleção atual, em seguida, obtendo o quadro da seleção e Obtendo DocView do quadro como uma <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>, em seguida, obtendo um <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUserData> do IVsTextView, em seguida, obtendo um host do modo de exibição, e Por fim o IWpfTextView:  
  
```csharp  
   IVsMonitorSelection selection =  
       this.ServiceProvider.GetService(typeof(IVsMonitorSelection))   
           as IVsMonitorSelection;  
   object frameObj = null;  
  
ErrorHandler.ThrowOnFailure(selection.GetCurrentElementValue(  
                                (uint)VSConstants.VSSELELEMID.SEID_DocumentFrame,  
                                out frameObj));  
  
   IVsWindowFrame frame = frameObj as IVsWindowFrame;  
   if (frame == null)  
       <<do nothing>>;  
  
...  
   object pvar;  
   ErrorHandler.ThrowOnFailure(frame.GetProperty((int)__VSFPROPID.VSFPROPID_DocView,  
                                                  out pvar));  
  
   IVsTextView textView = pvar as IVsTextView;  
   if (textView == null)  
   {  
       IVsCodeWindow codeWin = pvar as IVsCodeWindow;  
       if (codeWin != null)  
       {  
           ErrorHandler.ThrowOnFailure(codeWin.GetLastActiveView(out textView));  
       }  
   }  
  
...  
   if (textView == null)  
       <<do nothing>>  
  
   IVsUserData userData = textView as IVsUserData;  
   if (userData == null)  
       <<do nothing>>  
  
   object objTextViewHost;  
   if (VSConstants.S_OK   
           != userData.GetData(Microsoft.VisualStudio.Editor.DefGuidList  
                                                            .guidIWpfTextViewHost,  
                                out objTextViewHost))  
   {  
       <<do nothing>>  
   }  
  
   IWpfTextViewHost textViewHost = objTextViewHost as IWpfTextViewHost;  
   if (textViewHost == null)  
       <<do nothing>>  
  
   IWpfTextView textView = textViewHost.TextView;  
  
```  
  
 Quando você tiver um IWpfTextView, você pode obter a coluna onde o cursor está localizado:  
  
```csharp  
private static int GetCaretColumn(IWpfTextView textView)  
{  
    // This is the code the editor uses to populate the status bar.  
    Microsoft.VisualStudio.Text.Formatting.ITextViewLine caretViewLine =  
        textView.Caret.ContainingTextViewLine;  
    double columnWidth = textView.FormattedLineSource.ColumnWidth;  
    return (int)(Math.Round((textView.Caret.Left - caretViewLine.Left)  
                                / columnWidth));  
}  
  
```  
  
 Com a coluna atual em mãos onde o usuário é clicado, o código simplesmente chama no Gerenciador de configurações para adicionar ou remover a coluna. O settings manager dispara o evento ao qual todas as `ColumnGuideAdornment` objetos escutam. Quando o evento é acionado, esses objetos atualizar seus modos de exibição de texto associado com novas configurações de guia de coluna.  
  
## <a name="invoke-command-from-the-command-window"></a>Invocar comando na janela de comando  
 O exemplo de guias de coluna permite aos usuários invocar os dois comandos da janela de comando como uma forma de extensibilidade. Se você usar o **exibição &#124; Other Windows &#124; janela comando** de comando, você pode ver a janela de comando. Você pode interagir com a janela de comando, digitando "Editar", e com a conclusão de nome de comando e fornecendo o argumento 120, você tem o seguinte resultado:  
  
```csharp  
> Edit.AddColumnGuide 120  
>  
```  
  
 As partes da amostra que habilitar esse comportamento estão na *. VSCT* arquivo declarações, o `ColumnGuideCommands` construtor de classe quando ele conecta manipuladores de comandos e as implementações de manipulador de comando que verificam os argumentos do evento.  
  
 Você viu "`<CommandFlag>CommandWellOnly</CommandFlag>`" na *. VSCT* do arquivo, bem como posicionamentos no **editar** menu principal mesmo que os comandos não são mostrados no **editar** menu da interface do usuário. Tendo essas principal **edite** menu dá a eles nomes como **Edit.AddColumnGuide**. A declaração de grupo de comandos que contém os quatro comandos colocado o grupo na **editar** diretamente no menu:  
  
```xml  
<Group guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup"  
             priority="0xB801">  
        <Parent guid="guidSHLMainMenu" id="IDM_VS_MENU_EDIT" />  
      </Group>  
  
```  
  
 A seção de botões posteriormente declarada como os comandos `CommandWellOnly` para mantê-los invisível no menu principal e declarado-los com `AllowParams`:  
  
```xml  
<Button guid="guidColumnGuidesCommandSet" id="cmdidAddColumnGuide"   
        priority="0x0100" type="Button">  
  <Parent guid="guidColumnGuidesCommandSet" id="GuidesMenuItemsGroup" />  
  <Icon guid="guidImages" id="bmpPicAddGuide" />  
  <CommandFlag>CommandWellOnly</CommandFlag>  
  <CommandFlag>AllowParams</CommandFlag>  
  
```  
  
 Você viu o manipulador de comandos ligar o código no `ColumnGuideCommands` construtor da classe forneceu uma descrição do parâmetro permitido:  
  
```csharp  
_addGuidelineCommand.ParametersDescription = "<column>";  
  
```  
  
 Você viu a `GetApplicableColumn` verificações de função `OleMenuCmdEventArgs` para um valor antes de verificar o modo de exibição do editor para uma coluna atual:  
  
```csharp  
private int GetApplicableColumn(EventArgs e)  
{  
    var inValue = ((OleMenuCmdEventArgs)e).InValue as string;  
    if (!string.IsNullOrEmpty(inValue))  
    {  
        int column;  
        if (!int.TryParse(inValue, out column) || column < 0)  
            throw new ArgumentException("Invalid column");  
        return column;  
    }  
  
```  
  
## <a name="try-your-extension"></a>Tente sua extensão  
 Agora, você pode pressionar **F5** para executar sua extensão de guias de coluna. Abrir um arquivo de texto e use o menu de contexto do editor para adicionar linhas de guia, removê-los e alterar suas cores. Clique no texto (não o espaço em branco passado o final da linha) para adicionar uma coluna guia ou o editor adiciona à última coluna na linha. Se você usa a janela de comando e invocar os comandos com um argumento, você pode adicionar guias de coluna em qualquer lugar.  
  
 Se você deseja tentar posicionamentos de comandos diferentes, alterar os nomes, alterar os ícones e assim por diante, e você tiver problemas com o Visual Studio mostrando o código mais recente nos menus, você pode redefinir o hive experimental na qual você está depurando. Abrir o **Menu Iniciar do Windows** e digite "Redefinir". Procure e execute o comando **redefinir a instância Experimental do Visual Studio próxima**. Este comando limpa o hive do registro experimental de todos os componentes de extensão. Não limpa as configurações de componentes, portanto, qualquer guias que tinha quando você desligar o hive de experimental do Visual Studio ainda estão lá quando o código lê o repositório de configurações na próxima inicialização.  
  
## <a name="finished-code-project"></a>Projeto de código concluído  
 Em breve haverá um projeto do github de exemplos de extensibilidade do Visual Studio e o projeto concluído estará lá. Este artigo será atualizado para apontar lá quando isso acontece. O projeto de exemplo completo pode ter diferentes guids e terá uma faixa de bitmaps diferentes para os ícones de comando.  
  
 Você pode experimentar uma versão do recurso de guias de coluna com essa galeria do Visual Studio[extensão](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.EditorGuidelines).  
  
## <a name="see-also"></a>Consulte também  
 [Dentro do editor](../extensibility/inside-the-editor.md)   
 [Estender os serviços do editor e linguagem](../extensibility/extending-the-editor-and-language-services.md)   
 [Pontos de extensão de editor e o serviço de linguagem](../extensibility/language-service-and-editor-extension-points.md)   
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)   
 [Adicionar um submenu a um menu](../extensibility/adding-a-submenu-to-a-menu.md)   
 [Criar uma extensão com um modelo de item editor](../extensibility/creating-an-extension-with-an-editor-item-template.md)