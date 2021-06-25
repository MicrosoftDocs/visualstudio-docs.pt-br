---
title: Cores e estilo do Visual Studio | Microsoft Docs
description: Saiba como a experiência do usuário do Visual Studio usa a cor como uma ferramenta de comunicação, em vez de por motivos puramente estéticos.
ms.custom: SEO-VS-2020
ms.date: 07/31/2017
ms.topic: reference
ms.assetid: 0e384ea1-4d9e-4307-8884-6e183900732c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 307a4013c06258524c60619c6eff40e4d64740b6
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904481"
---
# <a name="colors-and-styling-for-visual-studio"></a>Cores e estilo para Visual Studio

## <a name="use-color-in-visual-studio"></a>Usar cor no Visual Studio

No Visual Studio, a cor é usada principalmente como uma ferramenta de comunicação, não apenas como decoração. Use a cor minimamente e reserve-a para situações em que você deseja:

- Comunicar o significado ou a afiliação (por exemplo, modificadores de plataforma ou idioma)

- Atraia atenção (por exemplo, indicando uma alteração de status)

- Melhorar a legibilidade e fornecer pontos de referência para navegar pela interface do usuário

- Aumentar a indesejável

Existem várias opções para atribuir cores a elementos da interface do usuário no Visual Studio. Às vezes, pode ser difícil descobrir qual opção você deve usar ou como usá-la corretamente. Este tópico ajudará você a:

- Entenda os diferentes serviços e sistemas usados para definir cores no Visual Studio.

- Selecione a opção correta para um determinado elemento.

- Use corretamente a opção escolhida.

> [!NOTE]
> Nunca codifique as cores Hex, RGB ou do sistema para os elementos da interface do usuário. O uso dos serviços permite flexibilidade no ajuste do matiz. Além disso, sem o serviço, você não poderá aproveitar os recursos de alternância de tema do [serviço VSColor](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_TheVSColorService).

### <a name="methods-for-assigning-color-to-visual-studio-interface-elements"></a>Métodos para atribuir cores a elementos de interface do Visual Studio

Escolha o método mais adequado para seus elementos de interface do usuário.

| Sua interface do usuário | Método | Quais são eles? |
| --- | --- | --- |
| Você tem caixas de diálogo inseridas ou autônomas. | **Cores do sistema** | Nomes de sistema que permitem que o sistema operacional defina a cor e a aparência dos elementos da interface do usuário, como controles de diálogo comuns. |
| Você tem uma interface do usuário personalizada que você deseja que seja consistente com o ambiente VS geral e que você tenha elementos da interface do usuário que correspondam à categoria e ao significado da semântica dos tokens compartilhados. | **Cores compartilhadas comuns** | Nomes de token de cor predefinidos existentes para elementos específicos da interface do usuário |
| Você tem um recurso individual ou grupo de recursos e não há nenhuma cor compartilhada para elementos semelhantes. | **Cores personalizadas** | Nomes de token de cor que são específicos de uma área e não devem ser compartilhados com outra interface do usuário |
| Você deseja permitir que o usuário final Personalize a interface do usuário ou o conteúdo (por exemplo, para editores de texto ou janelas de designer especializadas). | **Personalização do usuário final**<br /><br />**(Ferramentas &gt; Caixa de diálogo Opções)** | Configurações definidas na página "fontes e cores" da caixa de **diálogo &gt; Opções de ferramentas** ou uma página especializada específica para um recurso de interface do usuário. |

### <a name="visual-studio-themes"></a>Temas do Visual Studio

O Visual Studio apresenta três temas de cores diferentes: Claro, escuro e azul. Ele também detecta o modo de Alto Contraste, que é um tema de cores de todo o sistema projetado para acessibilidade.

Os usuários são solicitados a selecionar um tema durante seu primeiro uso do Visual Studio e podem alternar os temas mais tarde, acessando **ferramentas &gt; opções &gt; ambiente &gt; geral** e escolhendo um novo tema no menu suspenso "tema de cores".

Os usuários também podem usar o painel de controle para alternar seus sistemas inteiros em um dos vários temas de Alto Contraste. Se um usuário selecionar um tema de Alto Contraste, o seletor de tema de cores do Visual Studio não afetará mais as cores no Visual Studio, embora as alterações de tema sejam salvas para quando o usuário sair do modo de Alto Contraste. Para obter mais informações sobre o modo de Alto Contraste, consulte [escolhendo cores de alto contraste](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ChoosingHighContrastColors).

### <a name="the-vscolor-service"></a>O serviço VSColor

O Visual Studio fornece um serviço de cores de ambiente, conhecido como o serviço VSColor, que permite que você vincule os valores de cor dos elementos da interface do usuário a uma entrada nomeada que contém valores de cor para cada tema do Visual Studio. Isso garante que suas cores sejam alteradas automaticamente para refletir o atual tema selecionado pelo usuário ou o modo de Alto Contraste do sistema. O uso do serviço significa que a implementação de todas as alterações de cores relacionadas a temas é tratada em um único lugar e, se você estiver usando cores compartilhadas comuns do serviço, sua interface do usuário refletirá automaticamente novos temas em versões futuras do Visual Studio.

### <a name="implementation"></a>Implementação

O código-fonte do Visual Studio inclui vários arquivos de definição de pacote que contêm listas de nomes de token e os respectivos valores de cor para cada tema. O serviço de cores lê o VSColors definido nesses arquivos de definição de pacote. Essas cores são referenciadas na marcação XAML ou no código e, em seguida, carregadas por meio do `IVsUIShell5.GetThemedColor` método ou de um mapeamento DynamicResource.

### <a name="system-colors"></a>Cores do sistema

Os controles comuns fazem referência às cores do sistema por padrão. Se você quiser que sua interface do usuário use cores do sistema, como ao criar uma caixa de diálogo incorporada ou autônoma, você não precisará fazer nada.

### <a name="common-shared-colors-in-the-vscolor-service"></a>Cores compartilhadas comuns no serviço VSColor

Seus elementos de interface devem refletir o ambiente geral do Visual Studio. Ao reutilizar as cores compartilhadas comuns que são apropriadas para o componente da interface do usuário que você está criando, você garante que sua interface seja consistente com outras interfaces do Visual Studio e que suas cores serão atualizadas automaticamente quando os temas forem adicionados ou atualizados.

Antes de usar cores compartilhadas comuns, verifique se você entendeu como usá-las corretamente. O uso incorreto de cores compartilhadas comuns pode resultar em uma experiência inconsistente, frustrante ou confusa para seus usuários.

### <a name="user-customizable-colors"></a>Cores personalizáveis pelo usuário

Consulte: [expondo cores para usuários finais](../../extensibility/ux-guidelines/colors-and-styling-for-visual-studio.md#BKMK_ExposingColorsForEndUsers)

Às vezes, você desejará permitir que o usuário final Personalize sua interface do usuário, como quando você está criando um editor de código ou uma superfície de design. Os componentes da interface do usuário personalizáveis são encontrados na seção **fontes e cores** da caixa de diálogo **&gt; Opções de ferramentas** , em que os usuários podem optar por alterar a cor do primeiro plano, a cor do plano de fundo ou ambos.

![&gt;Caixa de diálogo opções de ferramentas](../../extensibility/ux-guidelines/media/0301-a_toolsoptionsdialog.png "0301-a_ToolsOptionsDialog")<br />&gt;Caixa de diálogo opções de ferramentas

## <a name="the-vscolor-service"></a><a name="BKMK_TheVSColorService"></a> O serviço VSColor

O Visual Studio fornece um serviço de cores de ambiente, também chamado de serviço VSColor ou o serviço de cores do Shell. Esse serviço permite associar os valores de cor dos elementos da interface do usuário a um conjunto de cores de valor de nome que contém cores para cada tema. O serviço VSColor deve ser usado para todos os elementos da interface do usuário, de forma que as cores sejam alteradas automaticamente para refletir o tema atual selecionado pelo usuário e, assim, a interface do usuário vinculada ao serviço de cores do ambiente será integrada a novos temas em versões futuras do Visual Studio.

### <a name="how-the-service-works"></a>Como funciona o serviço

O serviço de cores do ambiente lê VSColors definido no. pkgdef para o componente da interface do usuário. Esses VSColors são então referenciados em marcação XAML ou código e são carregados por meio de `IVsUIShell5.GetThemedColor` um `DynamicResource` mapeamento ou.

![Arquitetura do serviço de cores do ambiente](../../extensibility/ux-guidelines/media/0302-a_environmentcolorservicearchitecture.png "0302-a_EnvironmentColorServiceArchitecture")<br />Arquitetura do serviço de cores do ambiente

### <a name="accessing-the-service"></a>Acessando o serviço

Há várias maneiras diferentes de acessar o serviço VSColor, dependendo do tipo de tokens de cor que você está usando e do tipo de código que você tem.

#### <a name="predefined-environment-colors"></a>Cores de ambiente predefinidas

##### <a name="from-native-code"></a>Do código nativo

O Shell fornece um serviço que fornece acesso às `COLORREF` cores. O serviço/interface é:

```
IVsUIShell2::GetVSSysColorEx(VSSYSCOLOR dwSysColIndex, DWORD *pdwRGBval)
```

No arquivo VSShell80. idl, a enumeração `__VSSYSCOLOREX` tem constantes de cores do Shell. Para usá-lo, passe como o valor do índice, seja um dos valores do `enum __VSSYSCOLOREX` documentado no MSDN ou um número de índice regular que a API do sistema do Windows, `GetSysColor` , aceita. Fazer isso obtém novamente o valor RGB da cor que deve ser usada no segundo parâmetro.

Se estiver armazenando uma caneta ou um pincel com uma nova cor, você deverá `AdviseBroadcastMessages` (fora do shell do Visual Studio) e escuta `WM_SYSCOLORCHANGE` e `WM_THEMECHANGED` mensagens.

Para acessar o serviço de cores em código nativo, você fará uma chamada semelhante a esta:

```
pUIShell2->GetVSSysColorEx(VSCOLOR_COLOR_NAME, &rgbLOCAL_COLOR);
```

> [!NOTE]
> Os `COLORREF` valores retornados por `GetVSSysColorEx()` contêm apenas os componentes R, G, B de uma cor de tema. Se uma entrada de tema usar transparência, o valor do canal alfa será descartado antes de retornar. Portanto, se a cor de interesse do ambiente precisar ser usada em um local em que o canal de transparência é importante, você deverá usar `IVsUIShell5.GetThemedColor` em vez de `IVsUIShell2::GetVSSysColorEx` , conforme descrito posteriormente neste tópico.

##### <a name="from-managed-code"></a>Do código gerenciado

Acessar o serviço VSColor por meio de código nativo é razoavelmente simples. No entanto, se você estiver trabalhando com código gerenciado, determinar como usar o serviço pode ser complicado. Com isso em mente, aqui está um trecho de código em C# demonstrando esse processo:

```csharp
private void VSColorPaint(object sender, System.Windows.Forms.PaintEventArgs e)
{
    //getIVSUIShell2
    IVsUIShell2 uiShell2 = Package.GetService(typeof(SVsUIShell)) as IVsUIShell2;
    Debug.Assert (uiShell2 != null, "failed to get IVsUIShell2");

    if (uiShell2 != null)
    {
        //get the COLORREF structure
        uint win32Color;
        uiShell2.GetVSSysColorEx((int)__VSSYSCOLOREX.VSCOLOR_SMARTTAG_HOVER_FILL, out win32Color);

        //translate it to a managed Color structure
        Color myColor = ColorTranslator.FromWin32((int)win32Color);
        //use it
        e.Graphics.FillRectangle(new SolidBrush(myColor), 0, 0, 100, 100);
    }
}
```

Se você estiver trabalhando em Visual Basic, use:

```vb
Dim myColor As Color = ColorTranslator.FromWin32((Integer)win32Color)
```

##### <a name="from-wpf-ui"></a>Da interface do usuário do WPF

Você pode associar as cores do Visual Studio por meio de valores exportados para o aplicativo `ResourceDictionary` . Veja abaixo um exemplo de como usar os recursos da tabela de cores, bem como a associação aos dados de fonte do ambiente em XAML.

```xml
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

Para código gerenciado, a biblioteca de estrutura de pacote gerenciada do Shell ( `Microsoft.VisualStudio.Shell.12.0.dll` ) contém algumas classes auxiliares que facilitam o uso de cores com tema.

Os métodos auxiliares na `Microsoft.VisualStudio.Shell.VsColors` classe no MPF incluem `GetThemedGDIColor()` e `GetThemedWPFColor()` . Esses métodos auxiliares retornam o valor de cor de uma entrada de tema como ou , a ser usado `System.Drawing.Color` `System.Windows.Media.Color` no WinForms ou na interface do usuário do WPF.

```csharp
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

A classe também pode ser usada para obter identificadores VSCOLOR para uma determinada chave de recurso de cor do WPF ou vice-versa.

```csharp
public static string GetColorBaseKey(int vsSysColor);
public static bool TryGetColorIDFromBaseKey(string baseKey, out int vsSysColor);
```

Os métodos de classe `VsColors` consultam o serviço VSColor para retornar o valor de cor sempre que são invocados. Para obter um valor de cor como , uma alternativa com melhor desempenho é usar os métodos da classe , que armazena em cache os valores de cor obtidos do `System.Drawing.Color` `Microsoft.VisualStudio.PlatformUI.VSThemeColor` serviço VSColor. A classe assina internamente eventos de mensagens de difusão de shell e descarta o valor armazenado em cache quando ocorre um evento de alteração de tema. Além disso, a classe fornece um . Evento amigável do NET para assinar alterações de tema. Use o evento para adicionar um novo manipulador e use o método `ThemeChanged` para obter valores de cor para o de `GetThemedColor()` `ThemeResourceKeys` interesse. Um código de exemplo pode ter esta aparência:

```csharp
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

## <a name="choosing-high-contrast-colors"></a><a name="BKMK_ChoosingHighContrastColors"></a> Escolhendo Alto Contraste cores

### <a name="overview"></a>Visão geral

O Windows usa vários temas de alto contraste no nível do sistema que aumentam o contraste de cores de texto, telas de fundo e imagens, fazendo com que os elementos apareçam mais distintos na tela. Por motivos de acessibilidade, é importante que Visual Studio de interface responda corretamente quando os usuários alternam para um Alto Contraste tema.

Apenas algumas cores do sistema podem ser usadas para Alto Contraste temas. Ao escolher os nomes de cores do sistema, lembre-se das seguintes dicas:

- **Escolha cores do sistema que têm o mesmo significado semântico** que o elemento que você está colorindo. Por exemplo, se você estiver escolhendo uma cor de alto contraste para texto em uma janela, use WindowText e não ControlText.

- **Escolha os pares de primeiro plano/plano** de fundo juntos ou você não terá certeza de que sua escolha de cor funcionará em todos os Alto Contraste temas.

- **Determine quais partes da interface do usuário são as mais importantes e verifique se as áreas de conteúdo se destacarão.** Você perderá muitos detalhes que diferenças sutis no matiz de cores normalmente distinguiriam, portanto, o uso de cores de borda fortes é comum para definir áreas de conteúdo, pois não há variantes de cores para diferentes áreas de conteúdo.

### <a name="system-color-set"></a>Conjunto de cores do sistema

A tabela no Blog da Equipe do [WPF: Referência de SystemColors](/archive/blogs/wpf/systemcolors-reference) indica o conjunto completo de nomes de cores do sistema e os matizs correspondentes exibidos em cada tema.

Ao aplicar esse conjunto limitado de cores à interface do usuário, espera-se que você perca detalhes sutis que estavam presentes nos *temas "normais".* Aqui está um exemplo de interface do usuário com cores cinza sutis que são usadas para distinguir áreas dentro de uma janela de ferramentas. Quando emparelhadas com a mesma janela exibida no modo Alto Contraste, você pode ver que todas as telas de fundo são do mesmo matiz e as bordas dessas áreas são indicadas apenas pela borda:

![Exemplo de como detalhes sutis são perdidos Alto Contraste](../../extensibility/ux-guidelines/media/030303-a_propertieswindow.png "030303-a_PropertiesWindow")<br />Exemplo de como detalhes sutis são perdidos Alto Contraste

#### <a name="choosing-text-colors-in-an-editor"></a>Escolhendo cores de texto em um editor

O texto colorido é usado em um editor ou em uma superfície de design para indicar significado, como permitir a fácil identificação de grupos de itens semelhantes. Em um Alto Contraste, no entanto, você não tem a capacidade de diferenciar entre mais de três cores de texto. WindowText, GrayText e HotTrackText são as únicas cores disponíveis nas superfícies WindowBackground. Como você não pode usar mais de três cores, escolha cuidadosamente as diferenças mais importantes que você deseja exibir quando estiver Alto Contraste modo.

Matizes para cada um dos nomes de token permitidos em uma superfície do editor, conforme eles aparecem em cada Alto Contraste tema:

![Alto Contraste do editor](../../extensibility/ux-guidelines/media/030303-b_hceditorcomparison.png "030303-b_HCEditorComparison")<br />Alto Contraste do editor

Exemplos da superfície do editor no tema Azul:

![Tema do Editor em Azul](../../extensibility/ux-guidelines/media/030303-c_editorblue.png "030303-c_EditorBlue")<br />Tema do Editor em Azul

![Editor no Alto Contraste #1 tema](../../extensibility/ux-guidelines/media/030303-d_editorhc1.png "030303-d_EditorHC1")<br />Editor no Alto Contraste #1 tema

### <a name="usage-patterns"></a>Padrões de uso

Muitos elementos comuns da interface do usuário já têm Alto Contraste cores definidas. Você pode referenciar esses padrões de uso ao escolher seus próprios nomes de cores do sistema, para que os elementos da interface do usuário sejam consistentes com componentes semelhantes.

| Cor do sistema | Uso |
| --- | --- |
| Activecaption | – IDE ativo e glifos de botão de janela remada ao passar o mouse e pressionar<br />– Plano de fundo da barra de título para IDE e janelas remadas<br />– Plano de fundo da barra de status padrão |
| Activecaptiontext | - IDE ativo e janelas remadas para primeiro plano da barra de título (texto e glifos)<br />– Plano de fundo e borda dos botões de janela ativos ao passar o mouse e pressionar |
| Control | - Caixa de combinação, lista de listas listadas e padrão do controle de pesquisa e plano de fundo desabilitado, incluindo o botão de lista de listas<br />– Plano de fundo do botão de destino de encaixe<br />- Plano de fundo da barra de comandos<br />– Plano de fundo da janela de ferramentas |
| Controldark | - Plano de fundo do IDE<br />– Separadores de menu e barra de comandos<br />- Borda da barra de comandos<br />– Sombras de menu<br />– Padrão da guia janela de ferramentas e borda de foco e separador<br />– Plano de fundo do botão de estouro do documento<br />- Encaixe da borda do glifo de destino |
| Controldarkdark |- Janela de guia do documento não desfocedida e selecionada |
| Controllight |- Ocultar automaticamente a borda da guia<br />– Caixa de combinação e borda da lista de listas listada<br />– Plano de fundo e borda de destino de encaixe |
| Controllightlight | – Borda selecionada e focada |
| Controltext | – Caixa de combinação e glifo de lista de listas listada<br />– Texto de guia não selecionado da janela de ferramentas |
| Graytext |- Caixa de combinação e lista de menus desabilitados borda, glifo suspenso, texto e texto do item de menu<br />- Texto do menu desabilitado<br />- Texto do controle de pesquisa 'opções de pesquisa'<br />– Separador de seção de controle de pesquisa |
| Realce | - Todas as bordas e plano de fundo pressionados e de foco, exceto o plano de fundo do botão de combinação e a borda do botão de estouro da caixa de combinação<br />– Plano de fundo do item selecionado |
| Highlighttext | - Todos os focos e primeiro plano pressionados (texto e glifos)<br />– Janela de ferramentas focalizada e primeiro plano do controle de janela da guia do documento<br />– Borda da barra de título da janela de ferramentas voltada<br />– Primeiro plano da guia focalizada selecionada<br />– Documentar a borda do botão de estouro ao passar o mouse e pressionar<br />– Borda do ícone selecionado|
| Hottrack | – Tela de fundo e borda da barra de rolagem pressionada<br />– Glifo de seta da barra de rolagem ao pressionar |
| Inactivecaption | – IDE inativo e glifos de botão de janela remada ao passar o mouse<br />– Plano de fundo da barra de título para IDE e janelas remadas<br />– Plano de fundo do controle de pesquisa desabilitado |
| Inactivecaptiontext | - IDE inativo e primeiro plano da barra de título de janelas remadas (texto e glifos)<br />– Plano de fundo e borda dos botões de janela inativos ao passar o mouse<br />– Plano de fundo e borda do botão da janela de ferramentas desfocados<br />– Primeiro plano do controle de pesquisa desabilitado |
| Menu | - Plano de fundo do menu suspenso<br />– Plano de fundo da marca de seleção marcada e desabilitada |
| Menutext | - Borda do menu suspenso<br />– Marcas de verificação<br />- Glifos de menu<br />- Texto do menu suspenso<br />– Borda do ícone selecionado |
| Scrollbar | – Tela de fundo da seta da barra de rolagem e da barra de rolagem, todos os estados |
| Janela | - Ocultar automaticamente a plano de fundo da guia<br />- Barra de menus e plano de fundo da prateleira do comando<br />– Plano de fundo da guia da janela de documentos não selecionado ou desfocado e borda do documento, para guias abertas e provisoriamente<br />– Plano de fundo da barra de título da janela de ferramentas desfocado<br />– Plano de fundo da guia janela de ferramentas, selecionado e não selecionado |
| Windowframe | - Borda do IDE |
| Windowtext | - Primeiro plano da guia ocultar automaticamente<br />– Primeiro plano da guia da janela de ferramentas selecionada<br />- Guia da janela de documentos desfoque e primeiro plano da guia desfoques ou não selecionados<br />- Primeiro plano padrão do modo de exibição de árvore e passe o mouse sobre o glifo não selecionado<br />– Borda da guia selecionada da janela de ferramentas<br />– Tela de fundo, borda e glifo da barra de rolagem |

## <a name="exposing-colors-for-end-users"></a><a name="BKMK_ExposingColorsForEndUsers"></a> Expondo cores para usuários finais

### <a name="overview"></a>Visão geral

Às vezes, você deseja permitir que o usuário final personalize sua interface do usuário, como quando você está criando um editor de código ou uma superfície de design. A maneira mais comum de fazer isso é usando a caixa de **diálogo Opções &gt; de** Ferramentas. A menos que você tenha uma interface do usuário altamente especializada que exija **controles**  especiais, a maneira mais fácil de apresentar a personalização é por meio da página Fontes e Cores na seção Ambiente da caixa de diálogo. Para cada elemento que você expõe para personalização, o usuário pode optar por alterar a cor de primeiro plano, a cor da tela de fundo ou ambos.

### <a name="building-a-vspackage-for-your-customizable-colors"></a>Criando um VSPackage para suas cores personalizáveis

Um VSPackage pode controlar as fontes e cores por meio de categorias personalizadas e exibir itens na página de propriedades Fontes e Cores. Ao usar esse mecanismo, o VSPackages deve implementar a interface [IVsFontAndColorDefaultsProvider](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider) e suas interfaces associadas.

Em princípio, esse mecanismo pode ser usado para modificar todos os itens de exibição existentes e as categorias que os contêm. No entanto, ele não deve ser usado para modificar a categoria editor de texto ou seus itens de exibição. Para obter mais informações sobre a categoria Editor de Texto, consulte [Visão geral de fonte e cor.](/previous-versions/visualstudio/visual-studio-2015/extensibility/font-and-color-overview?preserve-view=true&view=vs-2015)

Para implementar categorias personalizadas ou exibir Itens, um VSPackage deve:

- **Crie ou identifique categorias no Registro.** A implementação do IDE da página de propriedades **Fontes** e Cores usa essas informações para consultar corretamente o serviço que dá suporte a uma determinada categoria.

- **Criar ou identificar grupos no Registro (opcional).** Pode ser útil definir um grupo, que representa a união de duas ou mais categorias. Se um grupo for definido, o IDE mesclará automaticamente subcategorias e distribuirá itens de exibição dentro do grupo.

- **Implemente o suporte ao IDE.**

- **Manipular alterações de fonte e cor.**

#### <a name="to-create-or-identify-categories"></a>Para criar ou identificar categorias

Construa um tipo especial de entrada de registro de categoria em em que é o nome `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<Category\>]` `<Category>` não localizado da categoria.

Preencha o Registro com dois valores:

| Nome | Tipo | Dados | Descrição |
| --- | --- | --- | --- |
| Categoria | REG_SZ | GUID | Um GUID criado para identificar a categoria |
| Pacote | REG_SZ | GUID | O GUID do serviço VSPackage que dá suporte à categoria |

 O serviço especificado no Registro deve fornecer uma implementação [de IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) para a categoria correspondente.

#### <a name="to-create-or-identify-groups"></a>Para criar ou identificar grupos

Construa um tipo especial de entrada de registro de categoria em em que é o nome `[HKLM\SOFTWARE\Microsoft \Visual Studio\\<Visual Studio version\>\FontAndColors\\<group\>]` `<group>` não localizado do grupo.

Preencha o Registro com dois valores:

| Nome | Tipo | Dados | Descrição |
|--- | --- | --- | --- |
| Categoria | REG_SZ | GUID | Um GUID criado para identificar a categoria |
| Pacote | REG_SZ | GUID | O GUID do serviço VSPackage que dá suporte à categoria |

O serviço especificado no Registro deve fornecer uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> para o grupo correspondente.

![Implementação de IVsFontAndColorGroup](../../extensibility/ux-guidelines/media/0304-a_fontandcolorgroup.png "0304-a_FontAndColorGroup")<br />Implementação de `IVsFontAndColorGroup`

### <a name="to-implement-ide-support"></a>Para implementar o suporte ao IDE

Implemente [GetObject](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaultsprovider.getobject), que retorna uma interface [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) ou uma interface para o IDE para cada categoria ou <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> GUID de grupo fornecido.

Para cada categoria compatível, um VSPackage implementa uma instância separada da interface [IVsFontAndColorDefaults.](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults)

Os métodos implementados por [meio de IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) devem fornecer o IDE com:

- Listas de itens de exibição na categoria

- Nomes localizáveis para itens de exibição

- Exibir informações para cada membro da categoria

> [!NOTE]
> Cada categoria deve conter pelo menos um item de exibição.

O IDE usa a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorGroup> interface para definir uma união de várias categorias.

Sua implementação fornece o IDE com:

- Uma lista das categorias que comem um determinado grupo

- Acesso a instâncias de [IVsFontAndColorDefaults](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolordefaults) que suportam cada Categoria dentro do grupo

- Nomes de grupo localizáveis

#### <a name="updating-the-ide"></a>Atualizando o IDE

O IDE armazena em cache informações sobre as configurações de Fonte e Cor. Portanto, após qualquer modificação da configuração de Fonte e Cor do IDE, garantir que o cache está atualizado é uma melhor prática.

A atualização do cache é feita por meio da interface [IvsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) e pode ser executada globalmente ou apenas em itens selecionados.

### <a name="handling-font-and-color-changes"></a>Manipulando alterações de fonte e cor

Para dar suporte corretamente à colorização do texto que um VSPackage exibe, o serviço de colorização que suporta o VSPackage deve responder às alterações iniciadas pelo usuário feitas por meio da página de propriedades Fontes e Cores.

Para fazer isso, um VSPackage deve:

- **manipular eventos gerados pelo IDE** implementando a interface [IVsFontAndColorEvents.](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents) O IDE chama o método apropriado após as modificações do usuário da página Fontes e Cores. Por exemplo, ele chamará o [método OnFontChanged](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorevents.onfontchanged) se uma nova fonte for selecionada.

  **OR**

- **sondar o IDE em busca de alterações.** Isso pode ser feito por meio da interface [IVsFontAndColorStorage](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage) implementada pelo sistema. Embora principalmente para suporte de persistência, o [método GetItem](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage.getitem) pode obter informações de fonte e cor para Itens de Exibição. Para obter mais informações sobre as configurações de fonte e cor, consulte o artigo do MSDN Acessando configurações de fonte e [cor armazenadas.](/previous-versions/visualstudio/visual-studio-2015/extensibility/accessing-stored-font-and-color-settings?preserve-view=true&view=vs-2015)

> [!NOTE]
> Para garantir que os resultados da sondagem estão corretos, use a interface [IVsFontAndColorCacheManager](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorcachemanager) para determinar se uma liberação e atualização de cache são necessárias antes de chamar os métodos de recuperação da interface [IVsFontAndColorStorage.](/dotnet/api/microsoft.visualstudio.shell.interop.ivsfontandcolorstorage)

#### <a name="registering-custom-font-and-color-category-without-implementing-interfaces"></a>Registrando a fonte personalizada e a categoria de cores sem implementar interfaces

O exemplo de código a seguir demonstra como registrar a fonte personalizada e a categoria de cores sem implementar interfaces:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\FontAndColors\CSharp Tool Window]
"Package"="{F5E7E71D-1401-11D1-883B-0000F87579D2}"
"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"
"ToolWindowPackage"="{7259e420-6241-4e0d-b535-5b820671d183}"

    "NameID"=dword:00000064
```

Para este exemplo de código:

- `"NameID"` = a ID do recurso do nome da categoria localizada em seu pacote
- `"ToolWindowPackage"` = GUID do pacote
- `"Category"="{9FF46859-A47E-47bf-8AC5-EC3DBE69D1FE}"` é apenas um exemplo e o valor real pode ser um novo GUID fornecido pelo implementador.

### <a name="set-the-font-and-color-property-category-guid"></a>Definir o GUID da categoria de propriedade Fonte e Cor

O exemplo de código a seguir demonstra a configuração de GUIDs de categoria.

```csharp
// m_pView is your IVsTextView
IVsTextEditorPropertyCategoryContainer spPropCatContainer =
(IVsTextEditorPropertyCategoryContainer)m_pView;
if (spPropCatContainer != null)
{
IVsTextEditorPropertyContainer spPropContainer;
Guid GUID_EditPropCategory_View_MasterSettings =
new Guid("{D1756E7C-B7FD-49a8-B48E-87B14A55655A}");
hr = spPropCatContainer.GetPropertyCategory(
ref GUID_EditPropCategory_View_MasterSettings,
out spPropContainer);
if(hr == 0)
{
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_FontCategory,
catGUID);
hr =
spPropContainer.SetProperty(
VSEDITPROPID.VSEDITPROPID_ViewGeneral_ColorCategory,
catGUID);
}
}
```
