---
title: Fontes e formatação para o Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 04/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: c3c3df69-83b4-4fd0-b5b1-e18c33f39376
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1a758c1e44f9f78f7dc2a225e641d91f97db72cc
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942823"
---
# <a name="fonts-and-formatting-for-visual-studio"></a>Fontes e formatação para o Visual Studio
##  <a name="BKMK_TheEnvironmentFont"></a> A fonte de ambiente
 Todas as fontes no Visual Studio devem ser expostas ao usuário para personalização. Isso é feito principalmente através de **fontes e cores** página na **Ferramentas > Opções** caixa de diálogo. As três principais categorias de configurações de fonte são:  
  
-   **Fonte de ambiente** -fonte primária para o IDE (ambiente de desenvolvimento integrado), usada para todos os elementos de interface, incluindo caixas de diálogo, menus, janelas de ferramentas e janelas de documento. Por padrão, a fonte de ambiente é vinculada a uma fonte de sistema que é exibido como 9 pt Segoe da interface do usuário em versões atuais do Windows. Usando uma fonte para todos os elementos de interface ajuda a garantir uma aparência consistente fonte por meio do IDE.  
  
-   **Editor de texto** -página de elementos que superfície no código e outros editores baseados em texto podem ser personalizadas no Editor de texto no **Ferramentas > Opções**.  
  
-   **Coleções específicas** -as janelas de designer que oferecem a personalização de seus elementos de interface do usuário pode expor fontes específicas para seu design de superfície na própria página de configurações na **Ferramentas > Opções**.  
  
### <a name="editor-font-customization-and-resizing"></a>Personalização do Editor de fonte e redimensionamento  
 Os usuários geralmente serão ampliar ou reduzir o tamanho e/ou a cor do texto no editor de acordo com suas preferências, independente da interface do usuário geral. Como a fonte de ambiente é usada em elementos que podem aparecer dentro ou como parte de um designer/editor, é importante observar o comportamento esperado quando uma destas classificações de fonte é alterada.  
  
 Ao criar elementos de interface do usuário que aparecem no editor, mas são não fazem parte dos *conteúdo*, é importante usar a fonte de ambiente e não a fonte do texto, para que elementos redimensionar de forma previsível.  
  
1.  Para o texto do código no editor, redimensionada com a configuração de fonte do texto de código e responder a nível de zoom do texto do editor.  
  
2.  Todos os outros elementos da interface devem ser vinculados à configuração de fonte de ambiente e respondem às alterações no ambiente globais. Isso inclui (mas não está limitado a):  
  
    -   Texto em menus de contexto  
  
    -   Texto em um adorno de editor, como o texto do menu de lâmpada, painel do editor de localização rápida e navegue até o painel  
  
    -   Rótulo de texto nas caixas de diálogo, como **localizar nos arquivos** ou **Refatorar**  
  
### <a name="accessing-the-environment-font"></a>Acessar a fonte de ambiente  
 No código nativo ou WinForms, a fonte de ambiente pode ser acessada, chamando o método `IUIHostLocale::GetDialogFont` depois de consultar a interface do `SID_SUIHostLocale` service.  
  
 Para o Windows Presentation Foundation (WPF), derivar a classe de janela de caixa de diálogo do shell `DialogWindow` classe, em vez do WPF `Window` classe.  
  
 No XAML, o código tem esta aparência:
  
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

code-behind:

```csharp
internal partial class WebConfigModificationWindow : DialogWindow  
{  
}  
```
  
 (Substitua `Microsoft.VisualStudio.Shell.11.0` com a versão atual da dll MPF.)  
  
 Para exibir a caixa de diálogo, chame "`ShowModal()`" na classe sobre `ShowDialog()`. `ShowModal()` Define o estado modal correto no shell, garante que a caixa de diálogo é centralizada na janela pai e assim por diante.  
  
 O código é da seguinte maneira:  
  
```csharp
MyWindow window = new MyWindow();  
window.ShowModal()  
```
  
 `ShowModal` Retorna um bool? (booliano anulável) com o `DialogResult`, que pode ser usado se necessário. O valor retornado será true se a caixa de diálogo foi fechada com **Okey**.  
  
 Se você precisar exibir algumas UI WPF que não é uma caixa de diálogo e é hospedado em seu próprio `HwndSource`, como uma janela pop-up ou uma janela do WPF filho de uma janela do Win32/WinForms pai, você precisará definir o `FontFamily` e `FontSize` no elemento raiz do elemento do WPF. (O shell define as propriedades na janela principal, mas eles não serão herdados após um `HWND`). O shell fornece recursos para o qual as propriedades podem ser associadas, como este:  
  
```xaml
<Setter Property="FontFamily" Value="{DynamicResource VsFont.EnvironmentFontFamily}" />  
<Setter Property="FontSize" Value="{DynamicResource VsFont.EnvironmentFontSize}" />  
```
  
###  <a name="BKMK_Formatting"></a> Formatação de referência (dimensionamento/negrito)  
 Algumas caixas de diálogo exigem um determinado texto em negrito ou um tamanho diferente de fonte de ambiente. Anteriormente, as fontes maiores do que a fonte de ambiente tivesse sido codificadas como "`environment font +2`" ou semelhantes. Usar os trechos de código fornecido, dar suporte a monitores com alto DPI e certifique-se de que o texto de exibição sempre aparece no peso (como Light ou Semilight) e no tamanho correto.  
  
> **Observação: Antes de aplicar formatação, verifique se você estiver seguindo as diretrizes encontradas nas [estilo de texto](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TextStyle).**  
  
 Para dimensionar a fonte de ambiente, defina o estilo do TextBlock ou rótulo conforme indicado. Cada um desses trechos de código, quando usados corretamente, irá gerar a fonte correta, incluindo as variações de tamanho e peso apropriadas.  
  
 Onde "`vsui`" é uma referência ao namespace `Microsoft.VisualStudio.Shell`:  

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0" 
```
  
#### <a name="375-environment-font--light"></a>Fonte de ambiente % 375 + luz  
 **Aparece como:** pt 34 Segoe UI Light  
 **Use para:** (raro) exclusivo com a marca da interface do usuário, como na página inicial

 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey);  
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado.  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment375PercentFontSizeStyleKey}}">TextBlock: 375 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment375PercentFontSizeStyleKey}}">Label: 375 Percent Scaling</Label>  
```
  
#### <a name="310-environment-font--light"></a>Fonte de ambiente % 310 + luz  
 **Aparece como:** pt 28 Segoe UI Light   
 **Use para:** títulos de caixa de diálogo assinatura grandes, principais de cabeçalho em relatórios  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado.  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment310PercentFontSizeStyleKey}}">TextBlock: 310 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment310PercentFontSizeStyleKey}}">Label: 310 Percent Scaling</Label>     
```
  
#### <a name="200-environment-font--semilight"></a>Fonte do ambiente de 200% + Semilight  
 **Aparece como:** 18 pt Segoe UI Semilight    
 **Use para:** subtítulos, títulos de caixas de diálogo de pequenas e médias  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente: 
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado:  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment200PercentFontSizeStyleKey}}">TextBlock: 200 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment200PercentFontSizeStyleKey}}">Label: 200 Percent Scaling</Label>    
```
  
#### <a name="155-environment-font"></a>Fonte de ambiente % 155  
 **Aparece como:** Segoe 14 pt da interface do usuário    
 **Use para:** títulos de seção no documento bem relatórios ou interface do usuário  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado:  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment155PercentFontSizeStyleKey}}">TextBlock: 155 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment155PercentFontSizeStyleKey}}">Label: 155 Percent Scaling</Label>  
```
  
#### <a name="133-environment-font"></a>Fonte de ambiente % 133  
 **Aparece como:** 12 pt Segoe da interface do usuário    
 **Use para:** subtítulos menores no documento e caixas de diálogo de assinatura bem da interface do usuário  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado:  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment133PercentFontSizeStyleKey}}">TextBlock: 133 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment133PercentFontSizeStyleKey}}">Label: 133 Percent Scaling</Label>    
```
  
#### <a name="122-environment-font"></a>Fonte de ambiente % 122  
 **Aparece como:** 11 pt Segoe da interface do usuário    
 **Use para:** seção títulos em caixas de diálogo de assinatura, superior nós na exibição de árvore, navegação de tabulação vertical  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado:  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironment122PercentFontSizeStyleKey}}">TextBlock: 122 Percent Scaling</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironment122PercentFontSizeStyleKey}}">Label: 122 Percent Scaling</Label>    
```
  
#### <a name="environment-font--bold"></a>Fonte de ambiente + em negrito  
 **Aparece como:** em negrito 9 pt Segoe da interface do usuário    
 **Use para:** rótulos e subtítulos em caixas de diálogo de assinatura, relatórios e documentos bem da interface do usuário  
  
 **Código procedural:** onde `textBlock` é um TextBlock definido anteriormente e `label` é um rótulo definido anteriormente:  
  
```csharp
textBlock.SetResourceReference(TextBlock.StyleProperty,    
        VsResourceKeys.TextBlockEnvironmentBoldStyleKey);   
label.SetResourceReference(Label.StyleProperty,    
        VsResourceKeys.LabelEnvironmentBoldStyleKey);    
```
  
 **XAML:** definir o estilo de TextBlock ou o rótulo, conforme mostrado:  
  
```xaml
<TextBlock Style="{DynamicResource {x:Static vsui:VsResourceKeys.TextBlockEnvironmentBoldStyleKey}}"> Bold TextBlock</TextBlock>   
<Label Style="{DynamicResource {x:Static vsui:VsResourceKeys.LabelEnvironmentBoldStyleKey}}"> Bold Label</Label>    
```
  
### <a name="localizable-styles"></a>Estilos de localizáveis  
 Em alguns casos, os localizadores precisará modificar os estilos de fonte para localidades diferentes, como a remoção de negrito do texto para idiomas do Leste Asiático. Para possibilitar a localização dos estilos de fonte, esses estilos devem ser dentro do arquivo. resx. É a melhor maneira de fazer isso e ainda Editar estilos de fonte no designer de formulários do Visual Studio definir explicitamente os estilos de fonte em tempo de design. Embora isso cria um objeto de fonte completa e pode parecer que quebrem a herança de fontes do pai, apenas a propriedade FontStyle é usada para definir a fonte.  
  
 A solução é vincular o formulário de caixa de diálogo `FontChanged` eventos. No `FontChanged` percorrer todos os controles de evento e verifique se a fonte está definida. Se ele for definido, você deve alterá-lo para uma nova fonte com base na fonte do formulário e estilo de fonte do controle anterior. Um exemplo no código é:  
  
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
  
 Usar esse código garante que quando a fonte do formulário é atualizada, as fontes dos controles também atualizará. Esse método também deve ser chamado do construtor do formulário, porque a caixa de diálogo pode não conseguir obter uma instância de `IUIService` e o `FontChanged` evento nunca será acionado. Vinculando `FontChanged` permitirá que as caixas de diálogo Selecionar a nova fonte dinamicamente, mesmo se a caixa de diálogo já está aberta.  
  
### <a name="testing-the-environment-font"></a>Teste a fonte de ambiente  
 Para garantir que sua interface do usuário está usando a fonte de ambiente e respeita as configurações de tamanho, abra **Ferramentas > Opções > ambiente > fontes e cores** e selecione "Fonte de ambiente" sob a "Mostrar configurações de:" menu suspenso.  
  
 ![Configurações de fontes e cores nas ferramentas do &gt; caixa de diálogo Opções](../../extensibility/ux-guidelines/media/0201-a_optionsfonts.png "a_OptionsFonts 0201")<br />Configurações de fontes e cores nas ferramentas de &gt; caixa de diálogo Opções
  
 Defina a fonte para algo muito diferente do padrão. Para tornar óbvio que não atualiza a interface do usuário, escolha uma fonte com serifas (como "Times New Roman") e defina um tamanho muito grande. Em seguida, teste sua interface do usuário para garantir que ele respeita o ambiente. Aqui está um exemplo usando a caixa de diálogo de licença:  
  
 ![Exemplo de texto de interface do usuário que não respeita a fonte de ambiente](../../extensibility/ux-guidelines/media/0201-b_wrongfontdialog.png "b_WrongFontDialog 0201")<br />Exemplo de texto de interface do usuário que não respeita a fonte de ambiente
  
 Nesse caso, "Informações de usuário" e "Informações do produto" são não respeitam a fonte. Em alguns casos, isso pode ser uma escolha de design explícita, mas ele pode ser um bug, se a fonte explícita não for especificada como parte das especificações redline.  
  
 Para redefinir a fonte, clique em "Padrões de uso" em **Ferramentas > Opções > ambiente > fontes e cores**.  
  
##  <a name="BKMK_TextStyle"></a> Estilo de texto  
 Estilo de texto se refere ao uso de maiusculas, peso e tamanho da fonte. Para obter diretrizes de implementação, consulte [a fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).  
  
### <a name="text-casing"></a>Uso de maiusculas e minúsculas do texto  
  
#### <a name="all-caps"></a>Todas em maiusculas  
 Não use todas em maiusculas para títulos ou rótulos no Visual Studio.  
  
#### <a name="all-lowercase"></a>Tudo em minúsculas  
 Não use todas as letras minúsculas para títulos ou rótulos no Visual Studio.  
  
#### <a name="sentence-and-title-case"></a>Caso de frase e título  
 Texto do Visual Studio deve usar a capitalização de título ou diferenciam maiusculas de minúsculas, dependendo da situação.  
  
|Use a capitalização de título para:|Use diferenciam maiusculas de minúsculas para:|  
|-------------------------|----------------------------|  
|Títulos de caixa de diálogo|Rótulos|  
|Caixas de grupo|Caixas de seleção|  
|Itens de menu|Botões de opção|  
|Itens de menu de contexto|Itens de caixa de lista|  
|Botões|Barras de status|  
|Rótulos de tabela||  
|Cabeçalhos de coluna||  
|Dicas de ferramenta||  
  
##### <a name="title-case"></a>Capitalização de título  
 Capitalização de título é um estilo no qual as primeiras letras da maioria ou todas as palavras dentro de uma frase estão em maiusculas. No Visual Studio, capitalização de título é usada para vários itens, incluindo:  
  
- **Dicas de ferramenta.** Exemplo: "Visualizar itens selecionados"  
  
- **Cabeçalhos de coluna.** Exemplo: "resposta do sistema"  
  
- **Itens de menu.** Exemplo: "Salvar tudo"  
  
  Ao usar a capitalização de título, estas são as diretrizes para quando colocar em maiuscula palavras e deixá-los em minúsculas:  
  
|Maiúsculas|Comentários e exemplos|  
|---------------|---------------------------|  
|Todos os substantivos||  
|Todos os verbos|Incluindo "Is" e outras formas de "ser"|  
|Todos os advérbios|Incluindo "Que" e "Quando"|  
|Todos os adjetivos|Incluindo "This" e "Que"|  
|Todos os pronomes|Incluindo o caso seja "Seu", bem como "É," uma contração dos pronomes "it" e o verbo "é"|  
|Primeira e última palavras, independentemente de partes da fala||  
|Preposições que fazem parte de uma frase verbal|"Fechando-Out de todos os Windows" ou "Desligamento do sistema"|  
|Todas as letras de um acrônimo|HTML, XML, URL, IDE, RGB|  
|O segundo word em uma palavra composta, caso se trate de um substantivo ou um adjetivo adequada, ou se as palavras têm o mesmo peso|Acesso de leitura/gravação de referência cruzada, Software de pré-Microsoft, tempo de execução|  
  
|Minúsculas|Exemplos|  
|---------------|--------------|  
|A segunda palavra em uma palavra composta, se for um particípio modificando a primeira palavra ou outra parte da fala|Instruções, fora Take|  
|Artigos, a menos que um é a primeira palavra no título|um, uma,|  
|Associações de coordenadas|e, mas, para, nem, ou|  
|Preposições com palavras de quatro ou menos letras fora de uma frase verbal|em, no, como para fora da, na parte superior do|  
|"Para" quando usado em uma frase infinita|"Como formatar o disco rígido"|  
  
##### <a name="sentence-case"></a>Diferenciam maiusculas de minúsculas  
 Diferenciam maiusculas de minúsculas é o método padrão de maiusculas e minúsculas para gravação no qual apenas a primeira palavra da sentença está em maiusculas, junto com qualquer substantivos e os pronomes "I". Em geral, diferenciam maiusculas de minúsculas é mais fácil para um público mundial ler, especialmente quando o conteúdo será convertido por uma máquina. Use diferenciam maiusculas de minúsculas para:  
  
1.  **Mensagens da barra de status.** Esses são simples, resumo e fornecem apenas informações de status. Exemplo: "carregamento de arquivo de projeto"  
  
2.  **Todos os outros elementos de interface do usuário**, incluindo rótulos, caixas de seleção, botões de opção e listar itens de caixa. Exemplo: "Selecionar todos os itens na lista"  
  
### <a name="text-formatting"></a>Formatação de texto  
 Texto do padrão de formatação no Visual Studio 2013 é controlado pela [a fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont). Esse serviço ajuda a garantir uma aparência consistente fonte por meio do IDE (ambiente de desenvolvimento integrado), e você deve usá-lo para garantir uma experiência consistente para seus usuários.  
  
 O tamanho padrão usado pelo serviço da fonte do Visual Studio vem do Windows e é exibido como 9 pt.  
  
 Você pode aplicar a formatação para a fonte de ambiente. Este tópico aborda como e onde usar estilos. Para obter informações de implementação, consulte [a fonte de ambiente](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_TheEnvironmentFont).  
  
#### <a name="bold-text"></a>Texto em negrito  
 Texto em negrito é usado com moderação no Visual Studio e deve ser reservado para:  
  
-   rótulos de pergunta em assistentes  
  
-   designando o projeto ativo no Gerenciador de soluções  
  
-   valores substituídos na janela da ferramenta propriedades  
  
-   determinados eventos nas listas de lista suspensa de editor do Visual Basic  
  
-   conteúdo gerado pelo servidor na estrutura de tópicos de documento para páginas da web  
  
-   cabeçalhos de seção na caixa de diálogo complexa ou designer de interface do usuário  
  
#### <a name="italics"></a>Itálico  
 Visual Studio não usa o texto em itálico itálico ou negrito.  
  
#### <a name="color"></a>Cor  
  
-   Azul é reservado para hiperlinks (navegação e comandos) e nunca deve ser usado para a orientação.  
  
-   Títulos maiores (fonte de ambiente x 155% ou maior) podem ser coloridos para essas finalidades:  
  
    -   Para fornecer o apelo visual a assinatura de IU do Visual Studio  
  
    -   Para chamar a atenção para uma área específica  
  
    -   Para oferecer alívio de cor do texto padrão ambiente/preto a cinza-escuro  
  
-   Cor nos títulos deve utilizar o Visual Studio marca cores existentes, principalmente a principal roxa, #FF68217A.  
  
-   Ao usar cor em títulos, você deve seguir a [diretrizes de cores do Windows](/windows/desktop/uxguide/vis-color), incluindo a taxa de contraste e outras considerações de acessibilidade.  
  
### <a name="font-size"></a>Tamanho da fonte  
 Design do Visual Studio da interface do usuário apresenta uma aparência mais clara com mais espaço em branco. Sempre que possível, as barras de título e chrome foram reduzidas ou removidas. Enquanto a densidade de informações é um requisito no Visual Studio, tipografia continua sendo importante, com ênfase em mais aberto de espaçamento entre linhas e uma variação de tamanhos de fonte e pesos.  
  
 As tabelas a seguir inclui detalhes de design e exemplos visuais para as fontes de exibição usados no Visual Studio. Algumas variações de fonte de exibição tem o tamanho e o peso, como Semilight ou luz, codificados em sua aparência.  
  
 Trechos de código de implementação para todas as fontes de exibição podem ser encontrados na [formatação (dimensionamento/negrito) referência](../../extensibility/ux-guidelines/fonts-and-formatting-for-visual-studio.md#BKMK_Formatting).  
  
#### <a name="375-environment-font--light"></a>Fonte de ambiente % 375 + luz  
  
|||  
|-|-|  
|**Uso:** raros. Exclusivo com marca somente interface do usuário.<br /><br /> **Faça:**<br /><br /> -Use diferenciam maiusculas de minúsculas<br />-Sempre use leve<br /><br /> **Não:**<br /><br /> -Use para interface do usuário que não seja da interface do usuário, como página inicial de assinatura<br />-Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Use nas janelas de ferramentas|**Aparece como:** pt 34 Segoe UI Light<br /><br /> **Exemplo de Visual:**<br /><br /> *Não usado atualmente. Pode ser usada na página inicial.*|  
  
#### <a name="310-environment-font--light"></a>Fonte de ambiente % 310 + luz  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Título maior em caixas de diálogo de assinatura<br />-Título do relatório principal<br /><br /> **Faça:**<br /><br /> -Use diferenciam maiusculas de minúsculas<br />-Sempre use leve<br /><br /> **Não:**<br /><br /> -Use para interface do usuário que não seja da interface do usuário, como página inicial de assinatura<br />-Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Use nas janelas de ferramentas|**Aparece como:** pt 28 Segoe UI Light<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente % 310 &#43; título claro](../../extensibility/ux-guidelines/media/0202-a_ef310.png "a_EF310 0202")|  
  
#### <a name="200-environment-font--semilight"></a>Fonte do ambiente de 200% + Semilight  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Subtítulos<br />-Títulos de caixas de diálogo de pequenas e médias<br /><br /> **Faça:**<br /><br /> -Use diferenciam maiusculas de minúsculas<br />-Sempre use Semilight peso<br /><br /> **Não:**<br /><br /> -Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Use nas janelas de ferramentas|**Aparece como:** Semillight de interface do usuário do Segoe 18 pt<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente de 200% &#43; Semilight](../../extensibility/ux-guidelines/media/0202-b_ef200.png "b_EF200 0202")|  
  
#### <a name="155-environment-font"></a>Fonte de ambiente % 155  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Os títulos de seção documento bem da interface do usuário<br />-Relatórios<br /><br /> **Tarefas pendentes:** usar diferenciam maiusculas de minúsculas<br /><br /> **Não:**<br /><br /> -Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Usar em controles padrão do Visual Studio<br />-Use nas janelas de ferramentas|**Aparece como:** Segoe 14 pt da interface do usuário<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente % 155](../../extensibility/ux-guidelines/media/0202-c_ef155.png "c_EF155 0202")|  
  
#### <a name="133-environment-font"></a>Fonte de ambiente % 133  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Subtítulos menores nas caixas de diálogo de assinatura<br />-Subtítulos menores no documento bem da interface do usuário<br /><br /> **Tarefas pendentes:** usar diferenciam maiusculas de minúsculas<br /><br /> **Não:**<br /><br /> -Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Usar em controles padrão do Visual Studio<br />-Use nas janelas de ferramentas|**Aparece como:** 12 pt Segoe da interface do usuário<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente % 133](../../extensibility/ux-guidelines/media/0202-d_ef133.png "d_EF133 0202")|  
  
#### <a name="122-environment-font"></a>Fonte de ambiente % 122  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Títulos de seção nas caixas de diálogo de assinatura<br />-Nós superior no modo de exibição de árvore<br />-Navegação pela tecla tab vertical<br /><br /> **Tarefas pendentes:** usar diferenciam maiusculas de minúsculas<br /><br /> **Não:**<br /><br /> -Em negrito, itálico ou negrito, itálico<br />-Use para o corpo de texto<br />-Usar em controles padrão do Visual Studio<br />-Use nas janelas de ferramentas|**Aparece como:** 11 pt Segoe da interface do usuário<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de título de fonte de ambiente % 122](../../extensibility/ux-guidelines/media/0202-e_ef122.png "e_EF122 0202")|  
  
#### <a name="environment-font--bold"></a>Fonte de ambiente + em negrito  
  
|||  
|-|-|  
|**Uso:**<br /><br /> -Rótulos e subtítulos nas caixas de diálogo de assinatura<br />-Rótulos e subtítulos em relatórios<br />-Rótulos e subtítulos no documento da interface do usuário<br /><br /> **Faça:**<br /><br /> -Use diferenciam maiusculas de minúsculas<br />– Use o peso de negrito<br /><br /> **Não:**<br /><br /> -Itálico ou negrito itálico<br />-Use para o corpo de texto<br />-Usar em controles padrão do Visual Studio<br />-Use nas janelas de ferramentas|**Aparece como:** em negrito 9 pt Segoe da interface do usuário<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente &#43; cabeçalho em negrito](../../extensibility/ux-guidelines/media/0202-f_efb.png "f_EFB 0202")|  
  
#### <a name="environment-font"></a>Fonte de ambiente  
  
|||  
|-|-|  
|**Uso:** todos os outros tipos de texto<br /><br /> **Tarefas pendentes:** usar diferenciam maiusculas de minúsculas<br /><br /> **Não:** itálico ou negrito e itálico|**Aparece como:** Segoe 9 pt da interface do usuário<br /><br /> **Exemplo de Visual:**<br /><br /> ![Exemplo de fonte de ambiente](../../extensibility/ux-guidelines/media/0202-g_ef.png "g_EF 0202")|  
  
### <a name="padding-and-spacing"></a>Preenchimento e espaçamento  
 Títulos exigem espaço em torno deles para fornecer-lhes a ênfase apropriada. Esse espaço varia dependendo do tamanho do ponto e o que mais é quase o título, como uma régua horizontal ou uma linha de texto na fonte de ambiente.  
  
-   O preenchimento ideal para um título por si só deve ser 90% do espaço de altura de capital de caractere. Por exemplo, um título de Segoe UI Light pt 28 possui uma altura de limite de 26 pt, e o preenchimento deve ser aproximadamente 23 pt ou aproximadamente 31 pixels.  
  
-   O espaço mínimo em torno de um título deve ser 50% da altura do caractere de capital. Menos espaço pode ser usado quando um cabeçalho é acompanhado por uma regra ou outro elemento de ajuste uma forte.  
  
-   Texto de fonte de ambiente em negrito deve seguir o preenchimento e o espaçamento de altura de linha padrão.  
  
## <a name="see-also"></a>Consulte também  
 [MSDN: Fontes (Windows)](/windows/desktop/uxguide/vis-fonts)   
 [MSDN: Texto da Interface do usuário (Windows)](/windows/desktop/uxguide/text-ui)
