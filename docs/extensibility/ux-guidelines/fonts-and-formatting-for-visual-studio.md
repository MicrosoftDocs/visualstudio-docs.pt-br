---
title: Fontes e formatação para Visual Studio | Microsoft Docs
description: Saiba mais sobre fontes e formatação para novos recursos que você projeta para Visual Studio, incluindo como usar a fonte de ambiente.
ms.custom: SEO-VS-2020
ms.date: 04/26/2017
ms.topic: reference
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e6e26b18c838fc240d7fab398f8626890eed0d31
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901676"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Fontes e formatação para Visual Studio
## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a> A fonte do ambiente
 Todas as fontes dentro Visual Studio devem ser expostas ao usuário para personalização. Isso é feito principalmente por meio da **página Fontes** e Cores na caixa de diálogo Ferramentas **> Opções.** As três principais categorias de configurações de fonte são:

- **Fonte do** ambiente – a fonte primária para o IDE (ambiente de desenvolvimento integrado), usada para todos os elementos de interface, incluindo caixas de diálogo, menus, janelas de ferramentas e janelas de documentos. Por padrão, a fonte do ambiente é vinculada a uma fonte do sistema que aparece como 9 pt Segoe UI nas versões atuais do Windows. Usar uma fonte para todos os elementos de interface ajuda a garantir uma aparência de fonte consistente em todo o IDE.

- **Editor de** texto – elementos que são publicados no código e outros editores baseados em texto podem ser personalizados na página Editor de Texto em Ferramentas **> Opções**.

- **Coleções específicas** – janelas de designer que oferecem personalização do usuário de seus elementos de interface podem expor fontes específicas à superfície de design em sua própria página de configurações em Ferramentas **> Opções**.

### <a name="editor-font-customization-and-resizing"></a>Personalização e reizing de fonte do editor
 Os usuários geralmente ampliarão ou ampliarão o tamanho e/ou a cor do texto no editor de acordo com suas preferências, independentemente da interface do usuário geral. Como a fonte de ambiente é usada em elementos que podem aparecer dentro ou como parte de um editor/designer, é importante observar o comportamento esperado quando uma dessas classificações de fonte é alterada.

 Ao criar elementos de interface do usuário que aparecem no editor, mas não fazem parte do conteúdo *,* é importante usar a fonte do ambiente e não a fonte de texto para que os elementos sejam reessados de maneira previsível.

1. Para texto de código no editor, reize com a configuração de fonte de texto do código e responda ao nível de zoom do texto do editor.

2. Todos os outros elementos da interface devem estar vinculados à configuração de fonte de ambiente e responder a quaisquer alterações globais no ambiente. Isso inclui (entre outros):

    - Texto em menus de contexto

    - Texto em um adorno do editor, como texto de menu de lâmpada, painel do editor de local rápido e navegação até o painel

    - Rotular texto em caixas de diálogo, **como Encontrar em Arquivos** ou **Refactor**

### <a name="accessing-the-environment-font"></a>Acessando a fonte do ambiente
 No código Nativo ou WinForms, a fonte do ambiente pode ser acessada chamando o método depois de consultar a `IUIHostLocale::GetDialogFont` interface do `SID_SUIHostLocale` serviço.

 Por Windows Presentation Foundation (WPF), derive sua classe de janela de diálogo da classe do shell `DialogWindow` em vez da classe do `Window` WPF.

 Em XAML, o código tem esta aparência:

```xaml
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>
```

Code-behind:

```csharp
internal partial class WebConfigModificationWindow : DialogWindow
{
}
```

 (Substitua `Microsoft.VisualStudio.Shell.11.0` pela versão atual da dll do MPF.)

 Para exibir a caixa de diálogo, chame `ShowModal()` " " na classe sobre `ShowDialog()` . `ShowModal()` define o estado modal correto no shell, garante que a caixa de diálogo seja centralizada na janela pai e assim por diante.

 O código será o seguinte:

```csharp
MyWindow window = new MyWindow();
window.ShowModal()
```

 `ShowModal` retorna um bool? (booliana anulada) com `DialogResult` o , que pode ser usado se necessário. O valor de retorno será true se a caixa de diálogo tiver sido fechada com **OK.**

 Se você precisar exibir alguma interface do usuário do WPF que não é uma caixa de diálogo e está hospedada em seu próprio , como uma janela pop-up ou uma janela filho do WPF de uma janela pai Win32/WinForms, você precisará definir e no elemento raiz do `HwndSource` `FontFamily` elemento `FontSize` WPF. (O shell define as propriedades na janela principal, mas elas não serão herdadas após um `HWND` ). O shell fornece recursos aos quais as propriedades podem ser vinculadas, desta forma:

```xaml
<Setter Property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter Property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />
```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a> Referência de formatação (dimensionamento/negrito)
 Alguns diálogos exigem que um texto específico seja negrito ou um tamanho diferente da fonte do ambiente. Anteriormente, as fontes maiores que a fonte de ambiente eram codificadas como " `environment font +2` " ou semelhantes. O uso dos snippets de código fornecidos dará suporte a monitores de DPI alto e garantirá que o texto de exibição sempre apareça com o tamanho e o peso corretos (como Light ou Semilight).

> [!NOTE]
> Antes de aplicar a formatação, verifique se você está seguindo as diretrizes encontradas em [Estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).**

 Para dimensionar a fonte do ambiente, de definido o estilo do TextBlock ou Rótulo, conforme indicado. Cada um desses snippets de código, usados corretamente, gerará a fonte correta, incluindo as variações de tamanho e peso apropriadas.

 Em que " `vsui` " é uma referência ao namespace `Microsoft.VisualStudio.Shell` :

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
```

#### <a name="375-environment-font--light"></a>Fonte de ambiente de 375% + Luz

**Aparece como:** 34 pt Segoe UI Light

::: moniker range="vs-2017"

**Use para:** (rara) interface do usuário de marca exclusiva, como na Página Inicial

::: moniker-end

::: moniker range=">=vs-2019"

**Use para:** (raro) interface do usuário com marca exclusiva

::: moniker-end

**Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);
```

**XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado.

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>
```

#### <a name="310-environment-font--light"></a>Fonte de ambiente de 310% + Luz
 **Aparece como:** 28 pt Segoe UI Light **Use para: títulos** de caixa de diálogo de assinatura grande, título principal em relatórios

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado.

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>
```

#### <a name="200-environment-font--semilight"></a>Fonte de ambiente de 200% + Semáforo
 **Aparece como:** 18 pt Segoe UI **Semilight Use for:** subheadings, titles in small and medium dialogs

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado:

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>
```

#### <a name="155-environment-font"></a>Fonte de ambiente de 155%
 **Aparece como:** 14 pt Segoe UI **Usar para:** títulos de seção na interface do usuário ou relatórios do documento

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado:

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>
```

#### <a name="133-environment-font"></a>Fonte de ambiente de 133%
 **Aparece como:** 12 pt Segoe UI **Use para:** subheadings menores em caixas de diálogo de assinatura e interface do usuário do documento bem

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado:

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>
```

#### <a name="122-environment-font"></a>Fonte de ambiente de 122%
 **Aparece como:** 11 pt Segoe UI **Use para:** títulos de seção em caixas de diálogo de assinatura, nós principais no modo de exibição de árvore, navegação com tabulação vertical

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado:

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>
```

#### <a name="environment-font--bold"></a>Fonte do ambiente + negrito
 **Aparece como: 9** pt em negrito Segoe UI **Use para:** rótulos e subheads em diálogos de assinatura, relatórios e interface do usuário do documento bem

 **Código de procedimento:** Em `textBlock` que é um TextBlock definido anteriormente e é um Rótulo definido `label` anteriormente:

```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);
```

 **XAML:** De acordo com o estilo do TextBlock ou do Rótulo, conforme mostrado:

```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>
```

### <a name="localizable-styles"></a>Estilos localizáveis
 Em alguns casos, os localizadores precisarão modificar estilos de fonte para localidades diferentes, como remover negrito do texto para idiomas do Leste da Ásia. Para tornar possível a localização de estilos de fonte, esses estilos devem estar dentro do arquivo .resx. A melhor maneira de fazer isso e ainda editar estilos de fonte no designer Visual Studio formulário é definir explicitamente os estilos de fonte em tempo de design. Embora isso crie um objeto de fonte completo e possa parecer quebrar a herança de fontes pai, somente a propriedade FontStyle é usada para definir a fonte.

 A solução é conectar o evento do formulário de `FontChanged` diálogo. No evento `FontChanged` , ande por todos os controles e verifique se sua fonte está definida. Se estiver definido, altere-o para uma nova fonte com base na fonte do formulário e no estilo de fonte anterior do controle. Um exemplo disso no código é:

```csharp
private void Form1_FontChanged(object sender, System.EventArgs e)
{
          SetFontStyles();
}

/// <summary>
/// SetFontStyles - This function will iterate all controls on a page
/// and recreate their font with the desired fontstyle.
/// It should be called in the OnFontChanged handler (and also in the constructor
/// in case the IUIService is not available so OnFontChange doesn't fire).
/// This way, when the VS shell font is given to us the controls that have
/// a different style for the font (bolded for example) will recreate their font
/// and use the VS shell font but with a style variation (bolded ...).
/// </summary>
protected void SetFontStyles()
{
     SetFontStyles(this, this, this.Font);
}

protected static void SetFontStyles(Control topControl, Control parent, Font referenceFont)
{
     foreach(Control c in parent.Controls)
     {
          if (c.Controls != null && c.Controls.Count > 0) {
               SetFontStyles(topControl, c, referenceFont);
          }
          if (c.Font != topControl.Font) {
               c.Font = new Font(referenceFont, c.Font.Style);
          }
     }
}
```

 O uso desse código garante que, quando a fonte do formulário for atualizada, as fontes de controles também serão atualizadas. Esse método também deve ser chamado do construtor do formulário, porque o diálogo pode falhar ao obter uma instância do e o `IUIService` evento nunca será a `FontChanged` incêndio. A conexão `FontChanged` permitirá que os diálogos escolham dinamicamente a nova fonte mesmo se a caixa de diálogo já estiver aberta.

### <a name="testing-the-environment-font"></a>Testando a fonte do ambiente
 Para garantir que sua interface do usuário está usando a fonte do ambiente e respeita as configurações de tamanho, abra Ferramentas > Opções > Fontes e Cores do Ambiente **>** e selecione "Fonte do Ambiente" no menu suspenso "Mostrar configurações para:".

 ![Configurações de fontes e cores na caixa de diálogo &gt; Opções de Ferramentas](../../extensibility/ux-guidelines/media/0201-a_optionsfonts.png "0201-a_OptionsFonts")<br />Configurações de fontes e cores na caixa de diálogo &gt; Opções de Ferramentas

 De definir a fonte como algo muito diferente do padrão. Para tornar óbvio qual interface do usuário não é atualizada, escolha uma fonte com serifs (como "Times New Roman") e de definir um tamanho muito grande. Em seguida, teste sua interface do usuário para garantir que ela respeita o ambiente. Aqui está um exemplo usando a caixa de diálogo de licença:

 ![Exemplo de texto da interface do usuário que não respeita a fonte do ambiente](../../extensibility/ux-guidelines/media/0201-b_wrongfontdialog.png "0201-b_WrongFontDialog")<br />Exemplo de texto da interface do usuário que não respeita a fonte do ambiente

 Nesse caso, "Informações do Usuário" e "Informações do Produto" não estão respeitando a fonte. Em alguns casos, isso pode ser uma opção explícita de design, mas pode ser um bug se a fonte explícita não for especificada como parte das especificações de linha vermelha.

 Para redefinir a fonte, clique em "Usar Padrões" em Ferramentas **> Opções > Ambiente > Fontes e Cores**.

## <a name="text-style"></a><a name="BKMK_TextStyle"></a> Estilo de texto
 O estilo de texto se refere ao tamanho da fonte, peso e capitalização. Para obter diretrizes de implementação, consulte [a fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).

### <a name="text-casing"></a>Capitalização de texto

#### <a name="all-caps"></a>Todo em maiúsculas
 Não use todos os limites para títulos ou rótulos no Visual Studio.

#### <a name="all-lowercase"></a>Todas as letras minúsculas
 Não use todas as letras minúsculas para títulos ou rótulos no Visual Studio.

#### <a name="sentence-and-title-case"></a>Sentença e caso de título
 O texto no Visual Studio deve usar o caso de título ou de sentença, dependendo da situação.

|Usar caso de título para:|Usar caso de sentença para:|
|-------------------------|----------------------------|
|Títulos de caixa de diálogo|Rótulos|
|Caixas de grupo|Caixas de seleção|
|Itens de menu|Botões de opção|
|Itens de menu de contexto|Itens da caixa de listagem|
|Botões|Barras de status|
|Rótulos de tabela||
|Cabeçalhos da coluna||
|Dicas de ferramenta||

##### <a name="title-case"></a>Capitalização de título
 A caixa de título é um estilo no qual as primeiras letras da maioria ou todas as palavras em uma frase são capitalizadas. No Visual Studio, o caso de título é usado para muitos itens, incluindo:

- **Dicas.** Exemplo: "Visualizar itens selecionados"

- **Cabeçalhos de coluna.** Exemplo: "resposta do sistema"

- **Itens de menu.** Exemplo: "salvar tudo"

  Ao usar o caso de título, essas são as diretrizes para quando colocar palavras em maiúsculas e quando deixá-las em minúsculas:

|Maiúsculas|Comentários e exemplos|
|---------------|---------------------------|
|Todos os substantivos||
|Todos os verbos|Incluindo "is" e outras formas de "a ser"|
|Todos os advérbios|Incluindo "de" e "quando"|
|Todos os adjetivos|Incluindo "This" e "que"|
|Todos os substantivos|Incluindo o Possessive "seu", bem como "é", uma contratação do pronoun "It" e o verbo "is"|
|Primeira e última palavras, independentemente de partes da fala||
|Preposições que fazem parte de uma frase verbal|"Fechar todas as janelas" ou "desligar o sistema"|
|Todas as letras de um acrônimo|HTML, XML, URL, IDE, RGB|
|A segunda palavra em uma palavra composta, se for um substantivo ou um adjetivo apropriado, ou se as palavras tiverem um peso igual|Referência cruzada, software anterior da Microsoft, acesso de leitura/gravação Run-Time|

|Minúsculas|Exemplos|
|---------------|--------------|
|A segunda palavra em uma palavra composta se ela for outra parte da fala ou de um particípio modificando a primeira palavra|Como fazer, tirar|
|Artigos, a menos que uma seja a primeira palavra no título|um, uma, o, a|
|Coordenar conconjuntos|e, mas, para, ou ou|
|Preposições com palavras de quatro ou menos letras fora de uma frase verbal|para, até, para, de, em cima de|
|"Para" quando usado em uma frase infinita|"Como formatar seu disco rígido"|

##### <a name="sentence-case"></a>Caso de sentença
 O caso de sentença é o método de capitalização padrão para escrever no qual apenas a primeira palavra da frase é capitalizada, junto com quaisquer substantivos próprios e o pronoun "I". Em geral, o caso de sentença é mais fácil para um público mundial ler, especialmente quando o conteúdo será traduzido por um computador. Usar caso de sentença para:

1. **Mensagens da barra de status.** Elas são simples, curtas e fornecem apenas informações de status. Exemplo: "Carregando arquivo de projeto"

2. **Todos os outros elementos da interface do usuário**, incluindo rótulos, caixas de seleção, botões de opção e itens da caixa de listagem. Exemplo: "selecionar todos os itens na lista"

### <a name="text-formatting"></a>Formatação de texto
 A formatação de texto padrão no Visual Studio 2013 é controlada pela [fonte do ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont). Esse serviço ajuda a garantir uma aparência de fonte consistente em todo o IDE (ambiente de desenvolvimento integrado) e você deve usá-la para garantir uma experiência consistente para seus usuários.

 O tamanho padrão usado pelo serviço de fontes do Visual Studio é proveniente do Windows e aparece como 9 pt.

 Você pode aplicar a formatação à fonte do ambiente. Este tópico aborda como e onde usar os estilos. Para obter informações de implementação, consulte [a fonte do ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).

#### <a name="bold-text"></a>Texto em negrito
 O texto em negrito é usado com moderação no Visual Studio e deve ser reservado para:

- rótulos de pergunta em assistentes

- designando o projeto ativo no Gerenciador de Soluções

- valores substituídos na janela de ferramentas Propriedades

- determinados eventos nas listas suspensas do editor de Visual Basic

- conteúdo gerado pelo servidor na estrutura de tópicos do documento para páginas da Web

- cabeçalhos de seção em interface de usuário ou designer de caixa de diálogo complexa

#### <a name="italics"></a>Itálico
 O Visual Studio não usa texto em itálico itálico ou negrito.

#### <a name="color"></a>Cor

- O azul é reservado para hiperlinks (navegação e comando) e nunca deve ser usado para orientação.

- Títulos maiores (fonte de ambiente x 155% ou superior) podem ser coloridos para essas finalidades:

  - Para fornecer apelo visual para assinatura da interface do usuário do Visual Studio

  - Para chamar a atenção para uma área específica

  - Para oferecer o alívio da cor de texto do ambiente cinza-escuro padrão/preto

- A cor dos títulos deve aproveitar as cores de marca existentes do Visual Studio, principalmente o principal roxo, #FF68217A.

- Ao usar cores em títulos, você deve aderir às [diretrizes de cores do Windows](/windows/desktop/uxguide/vis-color), incluindo a taxa de contraste e outras considerações sobre acessibilidade.

### <a name="font-size"></a>Tamanho da fonte
 Visual Studio design de interface do usuário apresenta uma aparência mais clara com mais espaço em branco. Sempre que possível, as barras de chrome e title foram reduzidas ou removidas. Embora a densidade de informações seja um requisito Visual Studio, a tipografia continua sendo importante, com ênfase no espaçamento de linha mais aberto e em uma variação de tamanhos e pesos de fonte.

 As tabelas a seguir incluem detalhes de design e exemplos visuais para as fontes de exibição usadas Visual Studio. Algumas variações de fonte de exibição têm o tamanho e o peso, como Semilight ou Light, codificados em sua aparência.

 Os snippets de código de implementação para todas as fontes de exibição podem ser encontrados na referência [formatação (dimensionamento/negrito).](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting)

#### <a name="375-environment-font--light"></a>Fonte de ambiente de 375% + Luz

|Uso|Aparência|
|-|-|
|**Uso:** Raro. Somente interface do usuário com marca exclusiva.<br /><br /> **Faça:**<br /><br /> – Usar caso de frase<br />– Sempre usar Peso claro<br /><br /> **Não:**<br /><br /> – Usar para interface do usuário diferente da interface do usuário de assinatura, como Página Inicial<br />– Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em janelas de ferramentas|**Aparece como:** 34 pt Segoe UI Light<br /><br /> **Exemplo visual:**<br /><br /> *Atualmente, não é usado. Pode ser usado na página inicial Visual Studio 2017.*|

#### <a name="310-environment-font--light"></a>Fonte de ambiente de 310% + Luz

::: moniker range="vs-2017"

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> – Título maior nas caixas de diálogo de assinatura<br />– Título do relatório principal<br /><br /> **Faça:**<br /><br /> – Usar caso de frase<br />– Sempre usar Peso claro<br /><br /> **Não:**<br /><br /> – Usar para interface do usuário diferente da interface do usuário de assinatura, como Página Inicial<br />– Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em janelas de ferramentas|**Aparece como:** 28 pt Segoe UI Light<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de fonte 310% ambiente &#43; título Claro](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

::: moniker range=">=vs-2019"

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> – Título maior nas caixas de diálogo de assinatura<br />– Título do relatório principal<br /><br /> **Faça:**<br /><br /> – Usar caso de frase<br />– Sempre usar Peso claro<br /><br /> **Não:**<br /><br /> – Usar para interface do usuário diferente da interface do usuário de assinatura<br />– Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em janelas de ferramentas|**Aparece como:** 28 pt Segoe UI Light<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de fonte 310% ambiente &#43; título Claro](../../extensibility/ux-guidelines/media/0202-a_ef310.png "0202-a_EF310")|

::: moniker-end

#### <a name="200-environment-font--semilight"></a>Fonte de ambiente de 200% + Semáforo

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> - Subheadings<br />– Títulos em caixas de diálogo pequenas e médias<br /><br /> **Faça:**<br /><br /> – Usar caso de frase<br />– Sempre usar o peso do semáforo<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em janelas de ferramentas|**Aparece como:** 18 pt Segoe UI Semillight<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de fonte 200% Ambiente &#43; Semáforo](../../extensibility/ux-guidelines/media/0202-b_ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>Fonte de ambiente de 155%

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> - Títulos de seção na interface do usuário do documento bem<br />- Relatórios<br /><br /> **Faça:** Usar caso de frase<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em controles Visual Studio padrão<br />– Usar em janelas de ferramentas|**Aparece como:** 14 pt Segoe UI<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 155%](../../extensibility/ux-guidelines/media/0202-c_ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>Fonte de ambiente de 133%

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> – Subheadings menores em caixas de diálogo de assinatura<br />- Subheadings menores na interface do usuário do documento bem<br /><br /> **Faça:** Usar caso de frase<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em controles Visual Studio padrão<br />– Usar em janelas de ferramentas|**Aparece como:** 12 pt Segoe UI<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 133%](../../extensibility/ux-guidelines/media/0202-d_ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>Fonte de ambiente de 122%

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> – Títulos de seção em caixas de diálogo de assinatura<br />- Nós principais no exibição de árvore<br />– Navegação com tabulação vertical<br /><br /> **Faça:** Usar caso de frase<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em controles Visual Studio padrão<br />– Usar em janelas de ferramentas|**Aparece como:** 11 pt Segoe UI<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 122%](../../extensibility/ux-guidelines/media/0202-e_ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>Fonte do ambiente + negrito

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> - Rótulos e subheads em caixas de diálogo de assinatura<br />- Rótulos e subheads em relatórios<br />- Rótulos e subheads na interface do usuário do documento bem<br /><br /> **Faça:**<br /><br /> – Usar caso de frase<br />– Usar o peso em negrito<br /><br /> **Não:**<br /><br /> - Itálico ou negrito itálico<br />– Usar para texto do corpo<br />– Usar em controles Visual Studio padrão<br />– Usar em janelas de ferramentas|**Aparece como: 9** pt em negrito Segoe UI<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de fonte Ambiente &#43; título Negrito](../../extensibility/ux-guidelines/media/0202-f_efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>Fonte do ambiente

|Uso|Aparência|
|-|-|
|**Uso:** Todos os outros textos<br /><br /> **Faça:** Usar caso de frase<br /><br /> **Não:** Itálico ou negrito itálico|**Aparece como:** 9 pt Segoe UI<br /><br /> **Exemplo visual:**<br /><br /> ![Exemplo de fonte Environment](../../extensibility/ux-guidelines/media/0202-g_ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>Preenchimento e espaçamento
 Os títulos exigem espaço ao redor deles para dar a eles a ênfase apropriada. Esse espaço varia dependendo do tamanho do ponto e do que mais está próximo ao título, como uma regra horizontal ou uma linha de texto na fonte do ambiente.

- O preenchimento ideal para um título por si só deve ser 90% do espaço de altura do caractere capital. Por exemplo, um título light de 28 pt Segoe UI tem uma altura de limite de 26 pt e o preenchimento deve ser de aproximadamente 23 pt ou cerca de 31 pixels.

- O espaço mínimo em torno de um título deve ser de 50% da altura do caractere capital. Menos espaço pode ser usado quando um título é acompanhado por uma regra ou outro elemento de ajuste rígido.

- O texto da fonte do ambiente em negrito deve seguir o espaçamento e o preenchimento de altura da linha padrão.

## <a name="see-also"></a>Confira também

- [Fontes (Windows)](/windows/desktop/uxguide/vis-fonts)
- [Interface do Usuário texto (Windows)](/windows/desktop/uxguide/text-ui)
