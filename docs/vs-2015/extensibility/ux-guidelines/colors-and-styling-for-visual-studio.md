---
title: Cores e estilos para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 84ade82822d5481d098fe98408a130ba93f68ee0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51725714"
---
# <a name="colors-and-styling-for-visual-studio"></a>Cores e estilos para o Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="using-color-in-visual-studio"></a>Usando cores no Visual Studio  
 No Visual Studio, a cor é usada principalmente como uma ferramenta de comunicação, não apenas como decoração. Usar cor minimamente e reservá-lo para situações em que você deseja:  
  
- Comunicar o significado ou afiliação (por exemplo, plataforma ou linguagem modificadores)  
  
- Atrair a atenção (por exemplo, indicando uma alteração de status)  
  
- Melhorar a legibilidade e fornecer pontos de referência para a interface do usuário de navegação  
  
- Finalidade de aumento  
  
  Existem várias opções para atribuir cores aos elementos de interface do usuário no Visual Studio. Às vezes, pode ser difícil a Figura out qual opção você deverá para usar ou como usá-lo corretamente. Este tópico o ajudará a:  
  
1. Entenda os diferentes serviços e sistemas usados para definir as cores no Visual Studio.  
  
2. Selecione a opção correta para um determinado elemento.  
  
3. Corretamente, use a opção escolhida.  
  
   **IMPORTANTE:** nunca codificar hexadecimal, RGB ou cores do sistema para os elementos de interface do usuário. Usando os serviços permite flexibilidade no ajuste Matiz. Além disso, sem o serviço, você não poderá tirar proveito dos recursos de alternância de tema a [o serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).  
  
### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>Métodos para atribuir cores aos elementos de interface do Visual Studio  
 Escolha o método mais adequado para seus elementos de interface do usuário.  
  
|A interface do usuário|Método|Quais são elas?|  
|-------------|------------|--------------------|  
|Você ter incorporado ou caixas de diálogo autônomo.|**Cores do sistema**|Nomes de sistema que permitem que o sistema operacional definir a cor e a aparência dos elementos da interface do usuário, por exemplo, para controles de caixa de diálogo comuns.|  
|Você tem a interface do usuário personalizada que você deseja que seja consistente com o ambiente do VS geral e você tem elementos de interface do usuário que correspondem ao significado semântico dos tokens compartilhados e categoria.|**Cores compartilhadas comuns**|Nomes de cores predefinidas de token existente para elementos de interface do usuário específicos|  
|Você tem um recurso individual ou um grupo de recursos e não há nenhuma cor compartilhado para elementos semelhantes.|**Cores personalizadas**|Nomes de token de cor que são específicos para uma área e não se destina a ser compartilhado com outra interface de usuário|  
|Você deseja permitir que o usuário final personalizar a interface do usuário ou conteúdo (por exemplo, para editores de texto ou janelas de designer especializadas).|**Personalização de usuário final**<br /><br /> **(Ferramentas > caixa de diálogo Opções)**|As configurações definidas na página de "Fontes e cores" a **Ferramentas > Opções** caixa de diálogo ou uma página especializada específica para um recurso de interface do usuário.|  
 
  
### <a name="visual-studio-themes"></a>Temas do Visual Studio  
 O Visual Studio apresenta três temas de cores diferentes: claro, escuro e azul. Ele também detecta o modo de alto contraste, o que é um tema de cores de todo o sistema projetado para acessibilidade.  
  
 Os usuários são solicitados a selecionar um tema durante seu primeiro uso do Visual Studio e pode alternar temas mais tarde, acessando **Ferramentas > Opções > ambiente > geral** e escolhendo um novo tema no menu suspenso "tema de cores".  
  
 Os usuários também podem usar o painel de controle para alternar a seus sistemas inteiros em um dos vários temas de alto contraste. Se um usuário seleciona um tema de alto contraste, em seguida, o seletor de tema de cores do Visual Studio não afeta mais cores no Visual Studio, embora as alterações de tema são salvas para quando o usuário sai do modo de alto contraste. Para obter mais informações sobre o modo de alto contraste, consulte [cores escolhendo alto contraste](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors).  
  
### <a name="the-vscolor-service"></a>O serviço VSColor  
 O Visual Studio fornece um serviço de cor de ambiente, conhecido como o serviço de VSColor, que permite que você associe os valores de cor de seus elementos de interface do usuário para uma entrada nomeada que contém os valores de cor para cada tema do Visual Studio. Isso garante que suas cores serão alterado automaticamente para refletir o modo atual de alto contraste de sistema ou tema selecionado pelo usuário. O uso do serviço significa que a implementação de todas as alterações de cor de tema relacionadas é tratada em um só lugar, e se você estiver usando cores compartilhadas comuns do serviço, sua interface de usuário refletirá automaticamente os novos temas em versões futuras do Visual Studio.  
  
### <a name="implementation"></a>Implementação  
 O código de origem do Visual Studio inclui vários arquivos de definição de pacote que contêm listas de nomes de token e os valores de cor respectivos para cada tema. O serviço de cor lê o VSColors definidas nesses arquivos de definição de pacote. Essas cores são referenciados na marcação XAML ou no código e, em seguida, carregados por meio de uma a **IVsUIShell5.GetThemedColor** método ou um mapeamento de DynamicResource.  
  
### <a name="system-colors"></a>Cores do sistema  
 As cores do sistema de referência de controles comuns por padrão. Se você quiser que sua interface do usuário para usar cores do sistema, como quando você estiver criando uma caixa de diálogo incorporada ou autônomo, você não precisa fazer nada.  
  
### <a name="common-shared-colors-in-the-vscolor-service"></a>Cores compartilhadas comuns no serviço VSColor  
 Os elementos de interface devem refletir o ambiente geral do Visual Studio. Reutilizando as cores comuns compartilhadas que são apropriadas para o componente de interface do usuário que você está projetando, você pode garantir que sua interface seja consistente com outras interfaces do Visual Studio, e que suas cores serão atualizado automaticamente quando os temas são adicionados ou atualizados.  
  
 Antes de usar cores compartilhadas comuns, certifique-se de que você compreenda como usá-los corretamente. Uso incorreto de cores compartilhadas comuns pode resultar em uma experiência inconsistente, frustrante ou confusa para seus usuários.  
  
### <a name="user-customizable-colors"></a>Cores personalizáveis pelo usuário  
 Consulte: [expondo as cores para os usuários finais](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)  
  
 Às vezes, você desejará permitir que o usuário final personalizar a interface do usuário, como quando você estiver criando um editor de código ou a superfície de design. Componentes de interface do usuário personalizáveis são encontrados na **fontes e cores** seção o **Ferramentas > Opções** caixa de diálogo, onde os usuários podem optar por alterar a cor de primeiro plano, cor de plano de fundo ou ambos.  
  
 ![Ferramentas &#62; caixa de diálogo de opções no Visual Studio](../../extensibility/ux-guidelines/media/0301-a-toolsoptionsdialog.png "a_ToolsOptionsDialog 0301")  
  
 **Ferramentas > caixa de diálogo Opções**  
  
 
##  <a name="BKMK_TheVSColorService"></a> O serviço VSColor  
 Visual Studio fornece um serviço de cor de ambiente, também chamado de serviço VSColor ou o serviço de cor do shell. Esse serviço permite que você associe os valores de cor de seus elementos de interface do usuário a um conjunto que contém as cores para cada tema de cores de nome-valor. O serviço de VSColor deve ser usado para todos os elementos de interface do usuário, para que as cores automaticamente alterada para refletir o tema selecionado pelo usuário atual e para que a interface do usuário associado ao serviço de cor de ambiente serão integradas novos temas em futuras versões do Visual Studio.  
  
### <a name="how-the-service-works"></a>Como funciona o serviço  
 O serviço de cor de ambiente lê que vscolors definidos na. pkgdef para o componente de interface do usuário. Esses VSColors, em seguida, são referenciados na marcação XAML ou código e são carregados por meio de uma a **IVsUIShell5.GetThemedColor** ou um mapeamento de DynamicResource.  
  
 ![Arquitetura de serviço de cor de ambiente](../../extensibility/ux-guidelines/media/0302-a-environmentcolorservicearchitecture.png "a_EnvironmentColorServiceArchitecture 0302")  
  
 **Arquitetura de serviço de cor de ambiente**  
  
### <a name="accessing-the-service"></a>Acessando o serviço  
 Há várias maneiras diferentes de acesso usando o serviço VSColor, dependendo de qual tipo de cor de tokens e que tipo de código que você tem.  
  
#### <a name="predefined-environment-colors"></a>Cores de ambiente predefinidas  
  
##### <a name="from-native-code"></a>Do código nativo  
 O shell fornece um serviço que fornece acesso para o COLORREF das cores. A interface de serviço/é:  
  
```  
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)  
```  
  
 No arquivo VSShell80.idl, a enumeração **__VSSYSCOLOREX** tem constantes de cores do shell. Para usá-la, passe em como o índice de valor de qualquer um dos valores da __VSSYSCOLOREX enum documentados no MSDN ou um índice regular número que o sistema Windows API, **GetSysColor**, aceita. Isso obtém de volta o valor RGB da cor que deve ser usado no segundo parâmetro.  
  
 Se armazenar uma caneta ou um pincel com uma nova cor, você deve AdviseBroadcastMessages (fora do shell do Visual Studio) e escuta mensagens WM_SYSCOLORCHANGE e WM_THEMECHANGED.  
  
```  
// To access the color service in native code, you'll make a call that resembles this:  
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);  
  
```  
  
 **Observação:** os valores COLORREF retornados por **GetVSSysColorEx()** contêm apenas R, G, componentes de B de uma cor de tema. Se uma entrada de tema usa transparência, o valor de canal alfa é descartado antes de retornar. Portanto, se a cor de ambiente de interesse precisa ser usado em um local em que o canal de transparência é importante, você deve usar IVsUIShell5.GetThemedColor em vez de IVsUIShell2::GetVSSysColorEx, conforme descrito mais adiante neste tópico.  
  
##### <a name="from-managed-code"></a>No código gerenciado  
 Acessando o serviço VSColor por meio de código nativo é bastante simples. Se você estiver trabalhando por meio de código gerenciado, no entanto, determinar como usar o serviço pode ser complicado. Com isso em mente, aqui está um trecho de código c# que demonstra esse processo:  
  
```  
private void VSColorPaint(object sender, System.Windows.Forms.PaintEventArgs e)  
{  
    //getIVSUIShell2  
    IVsUIShell2 uiShell2 = Package.GetService(typeof(SVsUIShell)) as IVsUIShell2;  
    Debug.Assert (uiShell2 != null, "failed to get IVsUIShell2");  
  
    if (uiShell2 != null)  
    {  
        //get the COLORREF structure  
        uint win32Color;  
        uiShell.GetVSSysColorEx(VSSYSCOLOREX.VSCOLOR_SMARTTAG_HOVER_FILL, out win32Color);  
  
        //translate it to a managed Color structure  
        Color myColor = ColorTranslator.FromWin32((int)win32Color);  
        //use it  
        e.Graphics.FillRectangle(new SolidBrush(myColor), 0, 0, 100, 100);  
    }  
}  
```  
  
 Se você estiver trabalhando no Visual Basic, use:  
  
```  
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)  
```  
  
##### <a name="from-wpf-ui"></a>Na interface do usuário do WPF  
 Você pode associar a cores do Visual Studio por meio de valores exportados para o dicionário de recurso do aplicativo. Abaixo está um exemplo de usando os recursos de tabela de cores, bem como a associação para os dados da fonte de ambiente no XAML.  
  
```  
<Style TargetType="{x:Type Button}">  
    <Setter Property="TextBlock.FontFamily"  
            Value="{DynamicResource VsFont.EnvironmentFontFamily}" />  
    <Setter Property="TextBlock.FontSize"  
            Value="{DynamicResource VsFont.EnvironmentFontSize}" />  
    <Setter Property="Background"  
            Value="{DynamicResource VsBrush.EnvironmentBackgroundGradient}" />  
</Style>  
```  
  
#### <a name="helper-classes-and-methods-for-managed-code"></a>Classes auxiliares e métodos para código gerenciado  
 Para código gerenciado, a biblioteca de estrutura de pacote gerenciado do shell (Microsoft.VisualStudio.Shell.12.0.dll) contém algumas classes auxiliares que facilita o uso de cores de tema.  
  
 Os métodos auxiliares na **Microsoft.VisualStudio.Shell.VsColors** classe no MPF incluem **GetThemedGDIColor()** e **GetThemedWPFColor()**. Esses métodos auxiliares retornam o valor de cor de uma entrada de tema como Drawing ou Color, a ser usado no WinForms ou UI WPF.  
  
```  
IVsUIShell5 shell5;  
Button button = new Button();  
button.BackColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemBrushKey);  
button.ForeColor = GetThemedGDIColor(shell5, SolutionExplorerColors.SelectedItemTextBrushKey);  
  
/// <summary>  
/// Gets a System.Drawing.Color value from the current theme for the given color key.  
/// </summary>  
/// <param name="vsUIShell">The IVsUIShell5 service, used to get the color's value.</param>  
/// <param name="themeResourceKey">The key to find the color for.</param>  
/// <returns>The current theme's value of the named color.</returns>  
public static System.Drawing.Color GetThemedGDIColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)  
{  
   Validate.IsNotNull(vsUIShell, "vsUIShell");  
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");  
  
   byte[] colorComponents = GetThemedColorRgba(vsUIShell, themeResourceKey);  
  
   // Note: The Win32 color we get back from IVsUIShell5.GetThemedColor is ABGR  
   return System.Drawing.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);  
}  
  
private static byte[] GetThemedColorRgba(IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)  
{  
   Guid category = themeResourceKey.Category;  
   __THEMEDCOLORTYPE colorType = __THEMEDCOLORTYPE.TCT_Foreground  
   if (themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundColor || themeResourceKey.KeyType == ThemeResourceKeyType.BackgroundBrush)  
   {  
      colorType = __THEMEDCOLORTYPE.TCT_Background;  
   }  
  
   // This call will throw an exception if the color is not found  
   uint rgbaColor = vsUIShell.GetThemedColor(ref category, themeResourceKey.Name, (uint)colorType);  
   return BitConverter.GetBytes(rgbaColor);  
}  
public static System.Windows.Media.Color GetThemedWPFColor(this IVsUIShell5 vsUIShell, ThemeResourceKey themeResourceKey)  
{  
   Validate.IsNotNull(vsUIShell, "vsUIShell");  
   Validate.IsNotNull(themeResourceKey, "themeResourceKey");  
  
   byte[] colorComponents = GetThemedColorComponents(vsUIShell, themeResourceKey);  
  
    return System.Windows.Media.Color.FromArgb(colorComponents[3], colorComponents[0], colorComponents[1], colorComponents[2]);  
}  
  
```  
  
 A classe também pode ser usada para obter identificadores VSCOLOR para uma determinada chave de recurso de cor WPF, ou vice-versa.  
  
```  
public static string GetColorBaseKey(int vsSysColor);  
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);  
```  
  
 Os métodos de **VsColors** classe consultar o serviço de VSColor para retornar o valor de cor de cada vez que eles são invocados. Para obter um valor de cor como **Drawing**, é uma alternativa com melhor desempenho em vez disso, use os métodos das **Microsoft.VisualStudio.PlatformUI.VSThemeColor** classe quais caches os valores de cor obtidos do serviço VSColor. A classe assina os eventos de mensagens de difusão de shell internamente e descartará o valor armazenado em cache quando ocorre um evento de alteração de tema. Além disso, a classe fornece um. Evento compatível com NET para assinar as alterações de tema. Use o **ThemeChanged** eventos para adicionar um novo manipulador e usar o **GetThemedColor()** método para obter a cor de valores para o **ThemeResourceKeys** de interesse. Um exemplo de código poderia ter esta aparência:  
  
```  
public MyWindowPanel()  
{  
    InitializeComponent();  
  
    // Subscribe to theme changes events so we can refresh the colors  
    VSColorTheme.ThemeChanged += VSColorTheme_ThemeChanged;  
  
    RefreshColors();  
}  
  
private void VSColorTheme_ThemeChanged(ThemeChangedEventArgs e)  
{  
    RefreshColors();  
  
    // Also post a message to all the children so they can apply the current theme appropriately  
    foreach (System.Windows.Forms.Control child in this.Controls)  
    {  
        NativeMethods.SendMessage(child.Handle, e.Message, IntPtr.Zero, IntPtr.Zero);  
    }  
}  
  
private void RefreshColors()  
{  
    this.BackColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowBackgroundColorKey);  
    this.ForeColor = VSColorTheme.GetThemedColor(EnvironmentColors.ToolWindowTextColorKey);  
}  
  
protected override void Dispose(bool disposing)  
{  
    if (disposing)  
    {  
        VSColorTheme.ThemeChanged -= this.VSColorTheme_ThemeChanged;  
        base.Dispose(disposing);}  
}  
```  
  
##  <a name="BKMK_ChoosingHighContrastColors"></a> Escolher as cores de alto contraste  
  
### <a name="overview"></a>Visão geral  
 Windows usa vários temas de nível de sistema de alto contraste que aumentam o contraste de cores de texto, planos de fundo e imagens, fazendo com que elementos são mais destacadas na tela. Por motivos de acessibilidade, é importante que os elementos de interface do Visual Studio respondam corretamente quando os usuários alternam para um tema de alto contraste.  
  
 Apenas algumas poucas cores do sistema podem ser usada para temas de alto contraste. Ao escolher seu sistema de nomes de cores, lembre-se as dicas a seguir:  
  
1.  **Escolha as cores do sistema que têm o mesmo significado semântico** como o elemento que são de cores. Por exemplo, se você está escolhendo uma cor de alto contraste do texto dentro de uma janela, use WindowText e não ControlText.  
  
2.  **Escolha pares primeiro e segundo plano** juntos ou pode não estar certo de que sua opção de cor funcionará em todos os temas de alto contraste.  
  
3.  **Determinar quais partes da sua interface do usuário são os mais importantes e certifique-se de que áreas de conteúdo destacará.** Você perderá muitos detalhes que normalmente seriam distinguir a diferenças sutis de matiz da cor, portanto, o uso de cores da borda forte é comum definir áreas de conteúdo, porque não há nenhum variações de cor para diferentes áreas de conteúdo.  
  
### <a name="system-color-set"></a>Conjunto de cores do sistema  
 A tabela no [Blog da equipe WPF: referência SystemColors](http://blogs.msdn.com/b/wpf/archive/2010/11/30/systemcolors-reference.aspx) indica o conjunto completo de nomes de cores do sistema e os matizes correspondentes exibidos em cada tema.  
  
 Ao aplicar este conjunto limitado de cores para a interface do usuário *espera-se que você perderá detalhes sutis que estavam presentes nos temas "normais"*. Aqui está um exemplo de interface do usuário com as cores cinza sutis que são usadas para distinguir as áreas em uma janela de ferramentas. Quando combinado com a mesma janela exibida no modo de alto contraste, você pode ver que os planos de fundo são o mesmo matiz e as bordas dessas áreas são indicadas pela borda sozinha:  
  
 ![Janela propriedades](../../extensibility/ux-guidelines/media/030303-a-propertieswindow.png "030303 a_PropertiesWindow")  
  
 **Exemplo de detalhes como sutis são perdidas quando em alto contraste**  
  
#### <a name="choosing-text-colors-in-an-editor"></a>Escolher as cores do texto em um editor  
 Texto coloridos serão é usado em um editor ou em uma superfície de design para indicar o significado, como permitir que para facilitar a identificação dos grupos de itens semelhantes. Em um tema de alto contraste, no entanto, você não tem a capacidade de diferenciar entre mais de três cores de texto. WindowText, texto cinza e HotTrackText são as cores somente disponíveis em superfícies WindowBackground. Uma vez que você não pode usar mais de três cores, escolha cuidadosamente as diferenças mais importantes que você deseja exibir no modo de alto contraste.  
  
 Matizes para cada um dos nomes de token permitidos em uma superfície do editor, que aparecem em cada tema de alto contraste:  
  
 ![Comparação de editor do alta contraste](../../extensibility/ux-guidelines/media/030303-b-hceditorcomparison.png "030303 b_HCEditorComparison")  
  
 **Comparação de editor do alta contraste**  
  
 Exemplos da superfície do editor no tema azul:  
  
 ![Editor de tema azul](../../extensibility/ux-guidelines/media/030303-c-editorblue.png "030303 c_EditorBlue")  
  
 **Editor de tema azul**  
  
 ![Editor de tema de alto contraste](../../extensibility/ux-guidelines/media/030303-d-editorhc1.png "030303 d_EditorHC1")  
  
 **Editor de tema de alto contraste #1**  
  
### <a name="usage-patterns"></a>Padrões de uso  
 Vários elementos de interface do usuário comuns já têm cores de alto contraste definidas. Você pode referenciar esses padrões de uso ao escolher seu próprio sistema de nomes de cores, para que seus elementos de interface do usuário são consistentes com os componentes similares.  
  
|Cor do sistema|Uso|  
|------------------|-----------|  
|Legenda ativa|-IDE ativa e glifos de botão de janela rafted no hover e pressione<br />-Plano de fundo do título barra do IDE e windows rafted<br />-Plano de fundo de barra de status padrão|  
|ActiveCaptionText|-IDE Active Directory e o windows rafted de primeiro plano da barra de título (texto e glifos)<br />-Em segundo plano e da borda dos botões da janela ativa no hover e pressione|  
|Controle|-Caixa de combinação lista suspensa e pesquisa controle padrão e desabilitado em segundo plano, incluindo o botão suspenso<br />-Plano de fundo do botão de encaixe destino<br />-Plano de fundo de barra de comando<br />-Plano de fundo de janela de ferramenta|  
|ControlDark|-Plano de fundo IDE<br />-Separadores de barra de menu e comando<br />-Borda da barra de comando<br />-Sombras menu<br />-Guia padrão e passe o mouse borda da janela e o separador de ferramenta<br />-De documentos bem fundo do botão de estouro<br />-Borda de glifo de destino dock|  
|ControlDarkDark|– Janela de guia de documento sem foco, selecionado|  
|ControlLight|-Borda de guia ocultar automaticamente<br />-Borda de lista de caixa e a lista suspensa caixa de combinação<br />-Encaixar o plano de fundo de destino e a borda|  
|ControlLightLight|-Borda provisória selecionada, focalizada|  
|ControlText|-Glifo de caixa de combinação suspensa e de caixa de lista<br />-Texto da guia ferramenta cancelou a seleção de janela|  
|Texto cinza|-Caixa de combinação e da borda do menu suspenso lista desabilitada, o glifo de menu suspenso, texto e texto do item de menu<br />-Texto de menu desabilitado<br />-Texto do cabeçalho pesquisa controle 'Opções de pesquisa'<br />-Separador de seção de controle pesquisa|  
|Realce|-All passe o mouse e pressionado planos de fundo e bordas, exceto a lista suspensa de caixa de combinação documento e o plano de fundo do botão bem overflow da borda do botão<br />-Planos de fundo do item selecionado|  
|Texto realçado|-Todas as em foco e colorir pressionado (texto e glifos)<br />-Ferramenta focalizado janela e documento guia janela controle em primeiro plano<br />-Borda de barra de título de janela de ferramenta focalizado<br />-Em primeiro plano de guia provisória concentrado e selecionado<br />-Borda do botão de estouro de bem documento em foco e pressione<br />-Borda de ícone selecionado|  
|HotTrack|-Plano de fundo de thumb barra de rolagem e borda na imprensa<br />-Glifo de seta da barra de rolagem pressionar|  
|Legenda inativa|-IDE inativo e glifos de botão de janela rafted ao focalizar<br />-Plano de fundo do título barra do IDE e windows rafted<br />-Plano de fundo de controle de pesquisa desabilitado|  
|InactiveCaptionText|-IDE inativo e primeiro plano o barra de título windows rafted (texto e glifos)<br />-Plano de fundo de botões de janela inativa e a borda ao focalizar<br />-Borda e o plano de fundo de botão de janela ferramenta sem foco<br />-Em primeiro plano de controle de pesquisa desabilitado|  
|Menu|-Tela de fundo de menu lista suspensa<br />-Plano de fundo de marca de seleção marcado e desabilitado|  
|MenuText|-Borda do menu suspenso<br />-A marca de seleção seleção<br />-Glifos menu<br />-Texto do menu drop-down<br />-Borda de ícone selecionado|  
|Barra de rolagem|-Barra de rolagem e a barra de rolagem seta em segundo plano, todos os estados|  
|Janela|-Ocultar automaticamente em segundo plano de guia<br />-O menu de barras e plano de fundo de prateleira de comando<br />– Plano de fundo do documento sem foco ou desmarcados janela guia e a borda de documento, as guias abertas e provisional<br />-Em segundo plano barra de título janela ferramenta sem foco<br />-Ferramenta janela guia plano de fundo, ambos marcados e desmarcados|  
|WindowFrame|-Borda IDE|  
|WindowText|-Em primeiro plano de guia ocultar automaticamente<br />-Primeiro plano de guia de janela de ferramenta selecionada<br />– Guia da janela de documento sem foco e primeiro plano de guia provisória sem foco ou não selecionado<br />-Árvore em primeiro plano do modo de exibição padrão e passe o mouse sobre o glifo não selecionado<br />-Borda da guia selecionada de janela de ferramenta<br />-Glifo, borda e tela de fundo de thumb barra de rolagem|  
  
##  <a name="BKMK_ExposingColorsForEndUsers"></a> Expondo as cores para os usuários finais  
  
### <a name="overview"></a>Visão geral  
 Às vezes, você desejará permitir que o usuário final personalizar a interface do usuário, como quando você estiver criando um editor de código ou a superfície de design. A maneira mais comum de fazer isso é usando o **Ferramentas > Opções** caixa de diálogo. A menos que você tenha altamente especializadas da interface do usuário que requer que os controles especiais, a maneira mais fácil para apresentar a personalização é por meio do **fontes e cores** página dentro de **ambiente** seção da caixa de diálogo. Para cada elemento que você expõe para personalização, o usuário pode optar por alterar a cor de primeiro plano, cor de plano de fundo ou ambos.  
  
### <a name="building-a-vspackage-for-your-customizable-colors"></a>Criação de um VSPackage para as cores personalizáveis  
 Um VSPackage pode controlar as fontes e cores por meio de categorias personalizadas e exibir os itens na página de propriedades de fontes e cores. Ao usar esse mecanismo, VSPackages deve implementar o [IVsFontAndColorDefaultsProvider](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.aspx) interface e respectivas interfaces associadas.  
  
 Em princípio, esse mecanismo pode ser usado para modificar todos os itens de exibição existente e as categorias que os contêm. No entanto, ele não deve ser usado para modificar a categoria do Editor de texto ou seus itens de exibição. Para obter mais informações sobre a categoria do Editor de texto, consulte [visão geral de cor e de fonte](https://msdn.microsoft.com/library/bb165065.aspx).  
  
 Para implementar categorias personalizadas ou exibir itens, um VSPackage deve:  
  
-   **Crie ou identifique categorias no registro.** Implementação do IDE do **fontes e cores** página de propriedades usa essas informações para consultar corretamente para o serviço que dão suporte a uma determinada categoria.  
  
-   **Criar ou identificar grupos no registro (opcional).** Pode ser útil definir um grupo, que representa a união de duas ou mais categorias. Se um grupo estiver definido, o IDE automaticamente mescla subcategorias e distribui itens de exibição dentro do grupo.  
  
-   **Implementar o suporte do IDE.**  
  
-   **Manipule as alterações de fonte e cor.**  
  
#### <a name="to-create-or-identify-categories"></a>Para criar ou identificar categorias  
 Construir um tipo especial de entrada de registro de categoria em [HKLM\Software\Microsoft. \Visual Studio\\< versão do Visual Studio\>\FontAndColors\\< categoria\>]. \<Categoria > é o nome não localizado da categoria.  
  
 Preencha o registro com dois valores:  
  
|Nome|Tipo|Dados|Descrição|  
|----------|----------|----------|-----------------|  
|Categoria|REG_SZ|GUID|Um GUID criado para identificar a categoria|  
|Pacote|REG_SZ|GUID|O GUID do serviço VSPackage que dá suporte a categoria|  
  
 O serviço especificado no registro deve fornecer uma implementação de [IVsFontAndColorDefaults](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults.aspx) para a categoria correspondente.  
  
#### <a name="to-create-or-identify-groups"></a>Para criar ou identificar grupos  
 Construir um tipo especial de entrada de registro de categoria em [HKLM\Software\Microsoft. \Visual Studio\\< versão do Visual Studio\>\FontAndColors\\< grupo\>]. \<grupo > é o nome não localizado do grupo.  
  
 Preencha o registro com dois valores:  
  
|Nome|Tipo|Dados|Descrição|  
|----------|----------|----------|-----------------|  
|Categoria|REG_SZ|GUID|Um GUID criado para identificar a categoria|  
|Pacote|REG_SZ|GUID|O GUID do serviço VSPackage que dá suporte a categoria|  
  
 O serviço especificado no registro deve fornecer uma implementação de **T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup** para o grupo correspondente.  
  
 ![Interface IVsFontAndColorGroup](../../extensibility/ux-guidelines/media/0304-a-fontandcolorgroup.png "a_FontAndColorGroup 0304")  
  
### <a name="to-implement-ide-support"></a>Para implementar o suporte IDE  
 Implemente [GetObject](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject.aspx), que retorna um [IVsFontAndColorDefaults](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults.aspx) interface ou uma **T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup** interface para o IDE para cada categoria ou o grupo GUID fornecida.  
  
 Para cada categoria que oferece suporte a ele, um VSPackage implementa uma instância separada do [IVsFontAndColorDefaults](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults.aspx) interface.  
  
 Os métodos implementados por meio [IVsFontAndColorDefaults](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults.aspx) deve fornecer o IDE com:  
  
- Listas de itens de exibição na categoria  
  
- Nomes localizáveis para itens de exibição  
  
- Exibir informações de cada membro da categoria  
  
  **Observação:** cada categoria deve conter pelo menos um item de exibição.  
  
  O IDE usa o **T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup** interface para definir uma união de várias categorias.  
  
  Sua implementação fornece o IDE com:  
  
- Uma lista de categorias que compõem um grupo específico  
  
- Acesso às instâncias do [IVsFontAndColorDefaults](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults.aspx) que dão suporte a cada categoria de dentro do grupo  
  
- Nomes de grupo localizáveis  
  
#### <a name="updating-the-ide"></a>Atualizando o IDE  
 O IDE armazena em cache as informações sobre as configurações de fonte e cor. Portanto, após qualquer modificação da configuração do IDE de fontes e cores, garantindo que o cache seja atualizado é uma prática recomendada.  
  
 Atualizar o cache é feito por meio de [IvsFontAndColorCacheManager](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager.aspx) de interface e pode ser realizados itens selecionados globalmente ou apenas no.  
  
### <a name="handling-font-and-color-changes"></a>Tratando alterações de fonte e cor  
 Para suportar adequadamente a colorização do texto que exibe um VSPackage, o serviço de colorização VSPackage de suporte deve responder às alterações iniciadas pelo usuário feitas por meio da página de propriedades de fontes e cores.  
  
 Para fazer isso, um VSPackage deve:  
  
- **manipular eventos gerados pelo IDE** implementando as [IVsFontAndColorEvents](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.aspx) interface. O IDE chama o método apropriado seguindo as modificações do usuário da página fontes e cores. Por exemplo, ele chama o [OnFontChanged](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged.aspx) método se uma nova fonte é selecionada.  
  
  **OU**  
  
- **sondar o IDE para que as alterações**. Isso pode ser feito por meio do sistema implementado [IVsFontAndColorStorage](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.aspx) interface. Embora principalmente para oferecer suporte a persistência, o [GetItem](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem.aspx) método pode obter informações de fonte e cor para itens de exibição. Para obter mais informações sobre configurações de fonte e cor, consulte o artigo do MSDN [acessar fonte armazenados e as configurações de cor](https://msdn.microsoft.com/library/bb166382.aspx).  
  
  **Observação:** para garantir que os resultados da pesquisa estão corretos, use o [IVsFontAndColorCacheManager](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager.aspx) interface para determinar se uma liberação do cache e atualização são necessários antes de chamar os métodos de recuperação do [ IVsFontAndColorStorage](https://msdn.microsoft.com/library/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.aspx) interface.  
  
#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>Registrando fontes personalizadas e cores categoria sem implementar interfaces  
 O exemplo de código a seguir demonstra como registrar a fonte personalizada e categoria de cor sem implementar interfaces:  
  
```xml  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]  
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"  
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"  
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"  
  
    "NameID"=dword:00000064  
```  
  
 **OBSERVAÇÃO:**  
  
-   "NameID" = a ID de recurso do nome de categoria localizada em seu pacote  
  
-   "ToolWindowPackage" = GUID do pacote  
  
-   "Category" = "{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}" é apenas um exemplo e o valor real pode ser um novo GUID fornecido pelo implementador.  
  
### <a name="set-the-font-and-color-property-category-guid"></a>Defina a categoria de propriedade da fonte e cor GUID  
 O exemplo de código a seguir demonstra como definir os GUIDs de categoria.  
  
```cs  
// m_pView is your IVsTextView  
IVsTextEditorPropertyCategoryContainer spPropCatContainer =  
(IVsTextEditorPropertyCategoryContainer)m_pView;  
if (spPropCatContainer != null)  
{  
  IVsTextEditorPropertyContainer spPropContainer;  
  Guid GUID_EditPropCategory_View_MasterSettings =  
  new Guid("{D1756E7C-B7FD-49a8-B48E-87B14A55655A}");  
  hr = spPropCatContainer.GetPropertyCategory(  
  ref GUID_EditPropCategory_View_MasterSettings, out spPropContainer);  
  if(hr == 0)  
  {  
    hr = spPropContainer.SetProperty(VSEDITPROPID.VSEDITPROPID_ViewGeneral_FontCategory, catGUID);  
    hr = spPropContainer.SetProperty(VSEDITPROPID.VSEDITPROPID_ViewGeneral_ColorCategory, catGUID);  
  }  
}  
```  
