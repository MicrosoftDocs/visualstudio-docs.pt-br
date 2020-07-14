---
title: Fontes e formatação
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3e88f314ccdf2b91215fdfe579741591c7eb724d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544203"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Fontes e formatação para Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

## <a name="the-environment-font"></a><a name="BKMK_TheEnvironmentFont"></a>A fonte do ambiente
 Todas as fontes no Visual Studio devem ser expostas ao usuário para personalização. Isso é feito principalmente por meio da página **fontes e cores** na caixa de diálogo **ferramentas > opções** . As três principais categorias de configurações de fonte são:

- **Fonte do ambiente** — a fonte principal do IDE (ambiente de desenvolvimento integrado), usada para todos os elementos da interface, incluindo caixas de diálogo, menus, janelas de ferramentas e janelas de documentos. Por padrão, a fonte do ambiente está vinculada a uma fonte do sistema que aparece como 9 pt Segoe UI nas versões atuais do Windows. O uso de uma fonte para todos os elementos de interface ajuda a garantir uma aparência de fonte consistente em todo o IDE.

- **Editor de texto** — elementos que a superfície no código e outros editores baseados em texto podem ser personalizados na página Editor de texto em **ferramentas > opções**.

- **Coleções específicas** — as janelas de designer que oferecem a personalização do usuário de seus elementos de interface podem expor fontes específicas à sua superfície de design em suas próprias páginas de configurações em **ferramentas > opções**.

### <a name="editor-font-customization-and-resizing"></a>Personalização e redimensionamento de fontes do editor
 Os usuários geralmente aumentam ou ampliam o tamanho e/ou a cor do texto no editor de acordo com sua preferência, independentemente da interface geral do usuário. Como a fonte de ambiente é usada em elementos que podem aparecer dentro ou como parte de um editor/designer, é importante observar o comportamento esperado quando uma dessas classificações de fontes é alterada.

 Ao criar elementos de interface do usuário que aparecem no editor, mas que não fazem parte do *conteúdo*, é importante usar a fonte do ambiente e não a fonte do texto para que os elementos redimensionem de forma previsível.

1. Para texto de código no editor, redimensione com a configuração fonte de texto de código e responda ao nível de zoom do texto do editor.

2. Todos os outros elementos da interface devem estar vinculados à configuração de fonte do ambiente e responder a quaisquer alterações globais no ambiente. Isso inclui (mas não se limita a):

    - Texto em menus de contexto

    - Texto em uma Adornment do editor, como texto do menu de lâmpada, painel de localização rápida e navegação para o painel

    - Texto do rótulo em caixas de diálogo, como localizar em arquivos ou refatorar

### <a name="accessing-the-environment-font"></a>Acessando a fonte do ambiente
 No código nativo ou WinForms, a fonte do ambiente pode ser acessada chamando o método **IUIHostLocale:: GetDialogFont** depois de consultar a interface do serviço de SID_SUIHostLocale.

 Para Windows Presentation Foundation (WPF), derive a classe da janela da caixa de diálogo da classe **DialogWindow** do Shell em vez da classe **Window** do WPF.

 Em XAML, o código tem esta aparência:

```
<ui:DialogWindow
    x:Class"MyNameSpace.MyWindow"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:s="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.11.0"
    ShowInTaskbar="False"
    WindowStartupLocation="CenterOwner"
    Title="My Dialog">
</ui:DialogWindow>

code behind:

internal partial class WebConfigModificationWindow : DialogWindow
{
}

```

 (Substitua `Microsoft.VisualStudio.Shell.11.0` pela versão atual da dll do MPF.)

 Para exibir a caixa de diálogo, chame "**userjanelarestrita ()**" na classe acima de **ShowDialog ()**. **Setjanelarestrita ()** define o estado modal correto no Shell, garante que a caixa de diálogo seja centralizada na janela pai e assim por diante.

 O código é o seguinte:

```
MyWindow window = new MyWindow();
window.ShowModal()

```

 **Setjanelarestrita** retorna um bool? (booliano anulável) com o **DialogResult**, que pode ser usado se necessário. O valor de retorno será true se a caixa de diálogo tiver sido fechada com **OK**.

 Se você precisar exibir alguma interface do usuário do WPF que não seja uma caixa de diálogo e esteja hospedada em seu próprio **HWND**, como uma janela pop-up ou uma janela filho do WPF de uma janela de janela pai Win32/WinForms, será necessário definir **FontFamily** e **FontSize** no elemento raiz do elemento WPF. (O Shell define as propriedades na janela principal, mas elas não serão herdadas após um HWND). O Shell fornece recursos aos quais as propriedades podem ser associadas, desta forma:

```
<Setter property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />
<Setter property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />

```

### <a name="formatting-scalingbolding-reference"></a><a name="BKMK_Formatting"></a>Referência de formatação (dimensionamento/negrito)
 Algumas caixas de diálogo exigem que o texto específico seja negrito ou um tamanho diferente da fonte do ambiente. Anteriormente, as fontes maiores do que a fonte do ambiente eram codificadas como "fonte de ambiente + 2" ou semelhantes. Usar os trechos de código fornecidos dará suporte a monitores de alto DPI e garantirá que o texto de exibição sempre apareça no tamanho e peso corretos (como Light ou Semilight).

> **Observação: antes de aplicar a formatação, verifique se você está seguindo as orientações encontradas em [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).**

 Para dimensionar a fonte do ambiente, defina o estilo do TextBlock ou do rótulo, conforme indicado. Cada um desses trechos de código, usados corretamente, gerará a fonte correta, incluindo as variações de tamanho e peso apropriadas.

 Em que "vsui" é uma referência ao namespace Microsoft. VisualStudio. Shell:

```
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"

```

#### <a name="375-environment-font--light"></a>375% de fonte do ambiente + claro
 **Aparece como:** 34 pt Segoe UI Light

 **Use for:** (raro) interface do usuário com marca exclusiva, como na página inicial

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>

```

#### <a name="310-environment-font--light"></a>310% de fonte do ambiente + claro
 **Aparece como:** 28 pt Segoe UI Light

 **Use para: títulos de caixa de diálogo de** assinatura grande, título principal em relatórios

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>

```

#### <a name="200-environment-font--semilight"></a>200% de fonte de ambiente + Semilight
 **Aparece como:** 18 pt Segoe UI Semilight

 **Use for:** subtítulos, títulos em caixas de diálogo pequenas e médias

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>

```

#### <a name="155-environment-font"></a>fonte de 155% de ambiente
 **Aparece como:** 14 pt Segoe UI

 **Use para:** títulos de seção em relatórios de interface do usuário

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>

```

#### <a name="133-environment-font"></a>fonte de 133% de ambiente
 **Aparece como:** 12 pt Segoe UI

 **Use para:** subtítulos menores em caixas de diálogo de assinatura e interface do usuário bem para documentos

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>

```

#### <a name="122-environment-font"></a>fonte de 122% de ambiente
 **Aparece como:** 11 pt Segoe UI

 **Use para:** títulos de seção em caixas de diálogo de assinatura, nós principais no modo de exibição de árvore, navegação de guia vertical

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>

```

#### <a name="environment-font--bold"></a>Fonte do ambiente + negrito
 **Aparece como:** 9 pt em negrito Segoe UI

 **Use para:** rótulos e subtítulos em caixas de diálogo de assinatura, relatórios e interface do usuário bem para documentos

 **Código de procedimento:** Onde "textBlock" é um TextBlock definido anteriormente e "Label" é um rótulo definido anteriormente.

```
textBlock.SetResourceReference(TextBlock.StyleProperty,  
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey); 
label.SetResourceReference(Label.StyleProperty,  
        VsResourceKeys.LabelEnvironmentBoldStyleKey);

```

 **XAML:** Defina o estilo do TextBlock ou do rótulo, conforme mostrado.

```
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock> 
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>

```

### <a name="localizable-styles"></a>Estilos localizáveis
 Em alguns casos, os localizadores precisarão modificar estilos de fonte para localidades diferentes, como remover o texto em negrito para idiomas do leste asiático. Para tornar possível a localização de estilos de fonte, esses estilos devem estar dentro do arquivo. resx. A melhor maneira de fazer isso e ainda editar os estilos de fonte no designer de formulário do Visual Studio é definir explicitamente os estilos de fonte em tempo de design. Embora isso crie um objeto de fonte completo e pareça quebrar a herança de fontes pai, somente a Propriedade FontStyle é usada para definir a fonte.

 A solução é vincular o evento **FontChanged** do formulário de diálogo. No evento **FontChanged** , percorra todos os controles e verifique se sua fonte está definida. Se estiver definido, altere-o para uma nova fonte com base na fonte do formulário e no estilo de fonte anterior do controle. Um exemplo disso no código é:

```
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

 O uso desse código garante que quando a fonte do formulário for atualizada, as fontes de controles também serão atualizadas. Esse método também deve ser chamado a partir do construtor do formulário, porque a caixa de diálogo pode falhar ao obter uma instância de **IUIService** e o evento **FontChanged** nunca será acionado. A conexão do **FontChanged** permitirá que as caixas de diálogo selecionem a nova fonte dinamicamente, mesmo que a caixa de diálogo já esteja aberta.

### <a name="testing-the-environment-font"></a>Testando a fonte do ambiente
 Para garantir que sua interface do usuário esteja usando a fonte do ambiente e respeita as configurações de tamanho, abra **ferramentas > opções > ambiente > fontes e cores** e selecione "fonte do ambiente" no menu suspenso "Mostrar configurações para:".

 ![Página fontes e cores na caixa de diálogo ferramentas &#62; opções](../../extensibility/ux-guidelines/media/0201-a-optionsfonts.png "0201-a_OptionsFonts")

 **Configurações de fontes e cores na caixa de diálogo ferramentas > opções**

 Defina a fonte como algo muito diferente do padrão. Para tornar claro que a interface do usuário não é atualizada, escolha uma fonte com serifas (como "Times New Roman") e defina um tamanho muito grande. Em seguida, teste sua interface do usuário para garantir que ela respeita o ambiente. Veja um exemplo de como usar a caixa de diálogo de licença:

 ![Exemplo de caixa de diálogo que não usa a fonte do ambiente](../../extensibility/ux-guidelines/media/0201-b-wrongfontdialog.png "0201-b_WrongFontDialog")

 **Exemplo de texto da interface do usuário que não respeita a fonte do ambiente**

 Nesse caso, "informações do usuário" e "informações do produto" não estão respeitando a fonte. Em alguns casos, essa pode ser uma opção de design explícita, mas pode ser um bug se a fonte explícita não for especificada como parte das especificações de Redline.

 Para redefinir a fonte, clique em "usar padrões" em **ferramentas > opções > ambiente > fontes e cores**.

## <a name="text-style"></a><a name="BKMK_TextStyle"></a>Estilo de texto
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

|Letras Maiúsculas|Comentários e exemplos|
|---------------|---------------------------|
|Todos os substantivos||
|Todos os verbos|Incluindo "is" e outras formas de "a ser"|
|Todos os advérbios|Incluindo "de" e "quando"|
|Todos os adjetivos|Incluindo "This" e "que"|
|Todos os substantivos|Incluindo o Possessive "seu", bem como "é", uma contratação do pronoun "It" e o verbo "is"|
|Primeira e última palavras, independentemente de partes da fala||
|Preposições que fazem parte de uma frase verbal|"Fechar todas as janelas" ou "desligar o sistema"|
|Todas as letras de um acrônimo|HTML, XML, URL, IDE, RGB|
|A segunda palavra em uma palavra composta, se for um substantivo ou um adjetivo apropriado, ou se as palavras tiverem um peso igual|Referência cruzada, software anterior da Microsoft, acesso de leitura/gravação, tempo de execução|

|Letras minúsculas|Exemplos|
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
 A formatação de texto padrão no Visual Studio 2013 é controlada por uma [fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont). Esse serviço ajuda a garantir uma aparência de fonte consistente em todo o IDE (ambiente de desenvolvimento integrado) e você deve usá-la para garantir uma experiência consistente para seus usuários.

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

- Ao usar cores em títulos, você deve aderir às [diretrizes de cores do Windows](https://msdn.microsoft.com/library/dn742482.aspx), incluindo a taxa de contraste e outras considerações sobre acessibilidade.

### <a name="font-size"></a>Tamanho da fonte
 O design da interface do usuário do Visual Studio apresenta uma aparência mais clara com mais espaço em branco. Sempre que possível, as barras Chrome e title foram reduzidas ou removidas. Embora a densidade das informações seja um requisito no Visual Studio, a tipografia continua sendo importante, com ênfase em mais espaçamento de linha aberta e uma variação de tamanhos e pesos de fontes.

 As tabelas a seguir incluem detalhes de design e exemplos visuais para as fontes de exibição usadas no Visual Studio. Algumas variações de fonte de vídeo têm o tamanho e o peso, como Semilight ou Light, codificados em sua aparência.

 Trechos de código de implementação para todas as fontes de exibição podem ser encontrados na [referência de formatação (dimensionamento/negrito)](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting).

#### <a name="375-environment-font--light"></a>375% de fonte do ambiente + claro

|Uso|Aparência|
|-|-|
|**Uso:** Encontrar. Somente interface do usuário com marca exclusiva.<br /><br /> **Coincide**<br /><br /> -Usar caso de sentença<br />-Sempre usar peso leve<br /><br /> **Não:**<br /><br /> -Use para a interface do usuário que não seja a interface do usuário da assinatura, como página inicial<br />– Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nas janelas de ferramentas|**Aparece como:** 34 pt Segoe UI Light<br /><br /> **Exemplo de Visual:**<br /><br /> *Não usado no momento. Pode ser usado na página inicial.*|

#### <a name="310-environment-font--light"></a>310% de fonte do ambiente + claro

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Título maior em caixas de diálogo de assinatura<br />-Título do relatório principal<br /><br /> **Coincide**<br /><br /> -Usar caso de sentença<br />-Sempre usar peso leve<br /><br /> **Não:**<br /><br /> -Use para a interface do usuário que não seja a interface do usuário da assinatura, como página inicial<br />– Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nas janelas de ferramentas|**Aparece como:** 28 pt Segoe UI Light<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente de 310% &#43; título da luz](../../extensibility/ux-guidelines/media/0202-a-ef310.png "0202-a_EF310")|

#### <a name="200-environment-font--semilight"></a>200% de fonte de ambiente + Semilight

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Subtítulos<br />-Títulos em caixas de diálogo pequenas e médias<br /><br /> **Coincide**<br /><br /> -Usar caso de sentença<br />-Sempre usar peso Semilight<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nas janelas de ferramentas|**Aparece como:** 18 pt Segoe UI Semillight<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente de 200% &#43; Semilight](../../extensibility/ux-guidelines/media/0202-b-ef200.png "0202-b_EF200")|

#### <a name="155-environment-font"></a>fonte de 155% de ambiente

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Títulos de seção na interface do usuário bem-documentação<br />-Relatórios<br /><br /> **Fazer:** Usar caso de sentença<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nos controles padrão do Visual Studio<br />-Usar nas janelas de ferramentas|**Aparece como:** 14 pt Segoe UI<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 155%](../../extensibility/ux-guidelines/media/0202-c-ef155.png "0202-c_EF155")|

#### <a name="133-environment-font"></a>fonte de 133% de ambiente

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Subtítulos menores em caixas de diálogo de assinatura<br />-Subtítulos menores na interface do usuário bem de documentos<br /><br /> **Fazer:** Usar caso de sentença<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nos controles padrão do Visual Studio<br />-Usar nas janelas de ferramentas|**Aparece como:** 12 pt Segoe UI<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 133%](../../extensibility/ux-guidelines/media/0202-d-ef133.png "0202-d_EF133")|

#### <a name="122-environment-font"></a>fonte de 122% de ambiente

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Títulos de seção em caixas de diálogo de assinatura<br />-Nós principais no modo de exibição de árvore<br />-Navegação de guia vertical<br /><br /> **Fazer:** Usar caso de sentença<br /><br /> **Não:**<br /><br /> – Negrito, itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nos controles padrão do Visual Studio<br />-Usar nas janelas de ferramentas|**Aparece como:** 11 pt Segoe UI<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente de 122%](../../extensibility/ux-guidelines/media/0202-e-ef122.png "0202-e_EF122")|

#### <a name="environment-font--bold"></a>Fonte do ambiente + negrito

|Uso|Aparência|
|-|-|
|**Uso:**<br /><br /> -Rótulos e subtítulos em caixas de diálogo de assinatura<br />-Rótulos e subtítulos em relatórios<br />-Rótulos e subtítulos na interface do usuário bem-sudirecionada<br /><br /> **Coincide**<br /><br /> -Usar caso de sentença<br />-Usar peso em negrito<br /><br /> **Não:**<br /><br /> -Itálico ou negrito itálico<br />-Use para corpo de texto<br />-Usar nos controles padrão do Visual Studio<br />-Usar nas janelas de ferramentas|**Aparece como:** 9 pt em negrito Segoe UI<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente &#43; título em negrito](../../extensibility/ux-guidelines/media/0202-f-efb.png "0202-f_EFB")|

#### <a name="environment-font"></a>Fonte do ambiente

|Uso|Aparência|
|-|-|
|**Uso:** Todos os outros textos<br /><br /> **Fazer:** Usar caso de sentença<br /><br /> Não **:** Itálico ou negrito itálico|**Aparece como:** 9 pt Segoe UI<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente](../../extensibility/ux-guidelines/media/0202-g-ef.png "0202-g_EF")|

### <a name="padding-and-spacing"></a>Enchimento e espaçamento
 Os títulos exigem espaço em relação a eles para dar a eles a ênfase apropriada. Esse espaço varia dependendo do tamanho do ponto e do que mais está próximo ao título, como uma regra horizontal ou uma linha de texto na fonte do ambiente.

- O preenchimento ideal para um título por si só deve ser de 90% do espaço de altura de caractere maiúsculo. Por exemplo, um título de Segoe UI de 28 pt tem uma altura de 26 pt e o preenchimento deve ser de aproximadamente 23 pt ou cerca de 31 pixels.

- O espaço mínimo em volta de um cabeçalho deve ser 50% da altura do caractere maiúsculo. Menos espaço pode ser usado quando um título é acompanhado por uma regra ou outro elemento de ajuste rígido.

- O texto da fonte do ambiente em negrito deve seguir o espaçamento e o preenchimento da altura de linha padrão.

## <a name="see-also"></a>Consulte Também
 [Msdn: fonts (Windows)](https://msdn.microsoft.com/library/windows/desktop/dn742483\(v=vs.85\).aspx) [msdn: texto da interface do usuário (Windows)](https://msdn.microsoft.com/library/windows/desktop/dn742478\(v=vs.85\).aspx)
