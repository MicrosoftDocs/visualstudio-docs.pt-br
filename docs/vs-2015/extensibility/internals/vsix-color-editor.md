---
title: Editor de cores do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 70879c5d-e0f0-4845-993c-2f4229869706
caps.latest.revision: 6
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7ac81f039bf5357f9488aeba439c27814cdf7e3d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727588"
---
# <a name="vsix-color-editor"></a>Editor de cores do VSIX
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A ferramenta Editor de cores de extensão do Visual Studio pode criar e editar cores personalizadas para o Visual Studio. A ferramenta também pode gerar chaves de recurso de tema para que as cores podem ser usadas no código. Essa ferramenta é útil para fazer as cores para uma extensão do Visual Studio que dá suporte a temas. Essa ferramenta pode abrir arquivos. pkgdef e. XML. Temas do Studio Visual (arquivos .vstheme) podem ser usados com o Editor de cores do Visual Studio extensão, alterando a extensão de arquivo para. XML. Além disso, os arquivos de .vstheme podem ser importados para um arquivo. XML atual.  
  
 ![Herói de Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-hero.png "herói de Editor de cores do VSIX")  
  
 **Arquivos de definição de pacote**  
  
 Arquivos de definição (. pkgdef) do pacote são os arquivos que definem os temas. As cores em si são armazenadas em arquivos. XML cor de tema, que são compilados em um arquivo. pkgdef. Os arquivos. pkgdef são implantados em locais de pesquisa do Visual Studio, processados em tempo de execução e mesclados em conjunto para definir temas.  
  
 **Tokens de cor**  
  
 Um token de cor é composto por quatro elementos:  
  
-   **Nome da categoria:** um agrupamento lógico de um conjunto de cores. Use um nome de categoria existente se já houver cores que são específicas para o elemento desejado da interface do usuário ou grupo de elementos de interface do usuário.  
  
-   **Nome do token:** um nome descritivo para o token de cor e os conjuntos de token. Conjuntos incluem plano de fundo e nomes de token de primeiro plano (texto), bem como todos os seus estados e eles devem ser nomeados para que seja fácil identificar os pares e os estados que elas se aplicam.  
  
-   **Valores (ou matizes) de cores:** necessários para cada tema colorido. Sempre crie plano de fundo e texto cor valores em pares. As cores são combinadas para plano de fundo/primeiro plano para que a cor do texto (primeiro plano) é sempre legível em relação a cor do plano de fundo no qual ela é desenhada. Essas cores são vinculados e serão usadas juntas na interface do usuário. Se o plano de fundo não se destina para uso com o texto, não defina uma cor de primeiro plano.  
  
-   **Nome de cor do sistema:** para uso em exibições de alto contraste.  
  
## <a name="how-to-use-the-tool"></a>Como usar a ferramenta  
 Tanto quanto possível, e quando apropriado, as cores existentes do Visual Studio devem ser reutilizadas em vez de fazer novos. No entanto, para casos em que nenhuma cores apropriadas são definidas, cores personalizadas devem ser criadas para manter um tema de extensão compatível.  
  
 **Criando novos tokens de cor**  
  
 Para criar cores personalizadas usando o Editor de cores de extensão do Visual Studio, siga estas etapas:  
  
1. Determine os nomes de categoria e o token para novos tokens de cor.  
  
2. Escolha os matizes que o elemento de interface do usuário serão usados para cada tema e a cor do sistema de alto contraste.  
  
3. Use o editor de cores para criar novos tokens de cor.  
  
4. Use as cores em uma extensão do Visual Studio.  
  
5. Teste as alterações no Visual Studio.  
  
   **Etapa 1: Determine a categoria e nomes de token para os novos tokens de cor.**  
  
   Esquema de nomenclatura preferencial para um VSColor é **[Category] [tipo de interface do usuário] [estado]**. Não use a palavra "color" VSColor nomes, pois ela é redundante.  
  
   Os nomes de categoria fornecem agrupamentos lógicos e devem ser definidos como restrito quanto possível. Por exemplo, o nome de uma janela de ferramenta única pode ser um nome de categoria, mas o nome de uma equipe de unidade ou projeto de toda a empresa não é. Agrupamento de entradas em categorias ajuda a evitar confusão entre as cores com o mesmo nome.  
  
   Um nome de token claramente deve indicar o tipo de elemento e a situações ou o "estado", para o qual a cor será aplicada. Por exemplo, uma Active Directory dica de dados **[tipo de interface do usuário]** podem ser nomeados "**DataTip**" e o **[estado]** poderia ser chamado "**Active**," resultante em um nome da cor de "**DataTipActive**." Como dicas de dados que o texto, de primeiro plano e uma cor de fundo precisam ser definido. Ao usar um emparelhamento de plano de fundo/primeiro plano, o editor de cores criará automaticamente as cores "**DataTipActive**" para o plano de fundo e "**DataTipActiveText**" para o primeiro plano.  
  
   Se a parte da interface do usuário tem apenas um estado, o **[estado]** parte do nome pode ser omitido. Por exemplo, se uma caixa de pesquisa tem uma borda e nenhuma alteração de estado que possa afetar a cor da borda, em seguida, o nome de token de cor da borda pode simplesmente ser chamado "**SearchBoxBorder**."  
  
   Alguns nomes de estado comuns incluem:  
  
- Ativo  
  
- Inativo  
  
- MouseOver  
  
- MouseDown  
  
- Selecionado  
  
- Focalizado  
  
  Exemplos de alguns nomes de token para partes de um controle de item de lista:  
  
- ListItem  
  
- ListItemBorder  
  
- ListItemMouseOver  
  
- ListItemMouseOverBorder  
  
- ListItemSelected  
  
- ListItemSelectedBorder  
  
- ListItemDisabled  
  
- ListItemDisabledBorder  
  
  **Etapa 2: Escolha os matizes que o elemento de interface do usuário serão usados para cada tema e a cor do sistema de alto contraste.**  
  
  Ao escolher cores personalizadas para a interface do usuário, selecione um elemento de interface do usuário existente semelhante e use suas cores como base. As cores para elementos de interface do usuário na caixa foram submetidos a revisão e teste, para que eles serão apareça adequados e se comportam corretamente em todos os temas.  
  
  **Etapa 3: Use o editor de cores para criar novos tokens de cor.**  
  
  Inicie o editor de cores e abra ou crie um novo arquivo. XML de cores do tema personalizado. Selecione **Editar > nova cor** no menu. Isso abre uma caixa de diálogo para especificar a categoria e um ou mais nomes para as entradas de cor nessa categoria:  
  
  ![Nova cor Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-color.png "nova cor Editor de cores do VSIX")  
  
  Selecione uma categoria existente ou selecione **nova categoria** para criar uma nova categoria. Outra caixa de diálogo será aberta, criando um novo nome de categoria:  
  
  ![Nova categoria Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-category.png "nova categoria Editor de cores do VSIX")  
  
  A nova categoria, em seguida, estará disponível na **nova cor** menu suspenso de categoria. Depois de escolher uma categoria, insira um nome por linha para cada novo token de cor e selecione "Criar" quando terminar:  
  
  ![Cor do Editor de cores novo do VSIX preenchido](../../extensibility/internals/media/vsix-color-editor-new-color-filled.png "VSIX Editor de cores nova cor preenchido")  
  
  Os valores de cor são mostrados em pares de plano de fundo/primeiro plano, com "None" indicando que a cor não foi definida. Observação: se uma cor não tiver um texto cor/par de cor de fundo, em seguida, apenas o plano de fundo precisa ser definido.  
  
  ![Valores de cor de Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-color-values.png "valores de cor de Editor de cores do VSIX")  
  
  Para editar um token de cor, selecione uma entrada de cor do tema (coluna) desse token. Adicione o valor de cor digitando um valor de cor hexadecimal no formato ARGB de 8 dígitos, inserindo um nome de cor do sistema para a célula, ou usando o menu suspenso para selecionar a cor desejada por meio de um conjunto de controles deslizantes ou uma lista de cores do sistema.  
  
  ![Cor de edição de Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-edit-color.png "cor de edição de Editor de cores do VSIX")  
  
  ![Em segundo plano Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-background.png "em segundo plano Editor de cores do VSIX")  
  
  Para componentes que não é necessário para exibir o texto, insira o valor de apenas uma cor: a cor do plano de fundo. Caso contrário, insira valores para a cor de plano de fundo e texto, separado por uma barra invertida.  
  
  Ao inserir valores de alto contraste, insira nomes de cores do sistema Windows válidos. Não insira valores ARGB de embutidos em código. Você pode exibir uma lista de nomes de cores do sistema válido, selecionando "Em segundo plano: sistema" ou "em primeiro plano:" nos menus de lista suspensa de valor de cor. Durante a criação de elementos que têm componentes de texto, use o par de cor do sistema em segundo plano/texto correto ou o texto pode ser ilegível.  
  
  Quando você terminar a criação, configuração e editando os tokens de cor, salvá-los no formato. pkgdef ou. XML desejado. Cor de tokens com um plano de fundo nem nem um conjunto de primeiro plano será salvo como cores vazias no formato. XML, mas descartado no formato. pkgdef. Uma caixa de diálogo avisará da potencial perda de cor se você tentar salvar cores vazias em um arquivo. pkgdef.  
  
  **Etapa 4: Use as cores em uma extensão do Visual Studio.**  
  
  Depois de definir a nova cor tokens, inclua o. pkgdef no arquivo de projeto com "Build Action" definido como "Conteúdo" e "Incluir em VSIX" definido como "True".  
  
  ![Editor de cores do VSIX pkgdef](../../extensibility/internals/media/vsix-color-editor-pkgdef.png "pkgdef do Editor de cores do VSIX")  
  
  No Editor do Visual Studio extensão cor, escolha Arquivo > Exibir o código de recurso para exibir o código que é usado para acessar o personalizado de cores na interface do usuário baseada no WPF.  
  
  ![Visualizador de código de recurso do Editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-resource-code-viewer.png "Visualizador de código de recurso do Editor de cores do VSIX")  
  
  Inclua esse código em uma classe estática no projeto. Uma referência a **Microsoft.VisualStudio.Shell.\< VSVersion >.0.dll** precisa ser adicionada ao projeto para usar o **ThemeResourceKey** tipo.  
  
```csharp  
namespace MyCustomColors  
{  
    public static class MyCategory  
    {  
        #region Autogenerated resource keys  
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.  
        public static readonly Guid Category = new Guid("faf7f3f9-9fe5-4dd3-9350-59679617dfbe");  
  
        private static ThemeResourceKey _MyColor1ColorKey;  
        private static ThemeResourceKey _MyColor1BrushKey;  
        private static ThemeResourceKey _MyColor1TextColorKey;  
        private static ThemeResourceKey _MyColor1TextBrushKey;  
        public static ThemeResourceKey MyColor1ColorKey { get { return _MyColor1ColorKey ?? (_MyColor1ColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundColor)); } }  
        public static ThemeResourceKey MyColor1BrushKey { get { return _MyColor1BrushKey ?? (_MyColor1BrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.BackgroundBrush)); } }  
        public static ThemeResourceKey MyColor1TextColorKey { get { return _MyColor1TextColorKey ?? (_MyColor1TextColorKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundColor)); } }  
        public static ThemeResourceKey MyColor1TextBrushKey { get { return _MyColor1TextBrushKey ?? (_MyColor1TextBrushKey = new ThemeResourceKey(Category, "MyColor1", ThemeResourceKeyType.ForegroundBrush)); } }  
        #endregion  
    }  
}  
```  
  
 Isso permite que o acesso para as cores no código XAML e a interface do usuário responder a alterações de tema.  
  
```xaml  
<UserControl x:Class="NewTestProject.TestPackageControl" Name="MyToolWindow"  
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
             xmlns:ns="clr-namespace:MyCustomColors">  
  <Grid>  
    <TextBlock Background="{DynamicResource {x:Static ns:MyCategory.MyColor1BrushKey}}"  
               Foreground="{DynamicResource {x:Static ns:MyCategory.MyColor1TextBrushKey}}"  
      >Sample Text</TextBlock>  
  
  </Grid>  
</UserControl>  
```  
  
 **Etapa 5: Teste as alterações no Visual Studio.**  
  
 O editor de cores pode temporariamente aplicar tokens de cor para as instâncias em execução do Visual Studio para exibir as alterações em tempo real para cores sem recompilar o pacote de extensão. Para fazer isso, clique no botão "Aplicar este tema à execução de janelas do Visual Studio", localizado no cabeçalho da coluna de cada tema. Este tema temporário desaparecerá quando o Editor de cores do VSIX está fechado.  
  
 ![Editor de cores do VSIX se aplicam](../../extensibility/internals/media/vsix-color-editor-apply.png "aplicar do Editor de cores do VSIX")  
  
 Para tornar as alterações permanentes, recompile e reimplante a extensão do Visual Studio depois de adicionar as novas cores para o arquivo. pkgdef e escrever o código que usará essas cores. Recriando a extensão do Visual Studio, você mesclará os valores do registro para as novas cores para o restante dos temas. Em seguida, reinicie o Visual Studio, exibir a interface do usuário e verifique se as novas cores aparecem conforme o esperado.  
  
## <a name="notes"></a>Observações  
 Essa ferramenta destina-se a ser usado para criar cores personalizadas para os temas do Visual Studio preexistentes, ou para editar as cores de um tema personalizado do Visual Studio. Para criar temas personalizados do Visual Studio completos, baixe o [extensão do Visual Studio Color Theme Editor](http://visualstudiogallery.msdn.microsoft.com/6f4b51b6-5c6b-4a81-9cb5-f2daa560430b) da Galeria de extensões do Visual Studio.  
  
## <a name="sample-output"></a>Saída de Exemplo  
 **Cor de saída XML**  
  
 O arquivo. XML gerado pela ferramenta será semelhante a este:  
  
```xml  
<Themes>  
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">  
    <Category Name="CategoryName" GUID="{eee9d521-dac2-48d9-9a5e-5c625ba2040c}">  
      <Color Name="ColorName1">  
        <Background Type="CT_RAW" Source="FFFFFFFF" />  
      </Color>  
      <Color Name="ColorName2">  
        <Background Type="CT_RAW" Source="FFFFFFFF" />  
        <Foreground Type="CT_RAW" Source="FF000000" />  
      </Color>  
      <Color Name="ColorName3">  
        <Background Type="CT_RAW" Source="FFFF0000" />  
      </Color>  
      <Color Name="ColorName4">  
        <Background Type="CT_RAW" Source="FF000088" />  
        <Foreground Type="CT_RAW" Source="FFFFFFFF" />  
      </Color>  
    </Category>  
  </Theme>  
  <Theme Name="Dark" GUID="{1ded0138-47ce-435e-84ef-9ec1f439b749}">...</Theme>  
  <Theme Name="Blue" GUID="{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}">...</Theme>  
  <Theme Name="HighContrast" GUID="{a5c004b4-2d4b-494e-bf01-45fc492522c7}">...</Theme>  
</Themes>  
  
```  
  
 **Saída de cor PKGDEF**  
  
 O arquivo. pkgdef gerado pela ferramenta será semelhante a este:  
  
```  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\CategoryName]  
"Data"=hex:78,00,00,00,0b,00,00,00,01,00,00,00,21,d5,e9,ee,c2,da,d9,48,9a,5e,5c,62,5b,a2,04,0c,04,00,00,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,31,01,ff,ff,ff,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,32,01,ff,ff,ff,ff,01,00,00,00,ff,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,33,01,ff,00,00,ff,00,0a,00,00,00,43,6f,6c,6f,72,4e,61,6d,65,34,01,00,00,88,ff,01,ff,ff,ff,ff  
[$RootKey$\Themes\{1ded0138-47ce-435e-84ef-9ec1f439b749}\CategoryName]  
"Data"=hex:...  
[$RootKey$\Themes\{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}\CategoryName]  
"Data"=hex:...  
[$RootKey$\Themes\{a5c004b4-2d4b-494e-bf01-45fc492522c7}\CategoryName]  
"Data"=hex:...  
  
```  
  
 **Wrapper de chaves de recurso em C#**  
  
 As chaves de recurso de cor geradas pela ferramenta será semelhantes a este:  
  
```csharp  
namespace MyNamespace  
{  
    public static class MyColors  
    {  
        #region Autogenerated resource keys  
        // These resource keys are generated by Visual Studio Extension Color Editor, and should be replaced when new colors are added to this category.  
  
        public static string ColorName1ColorKey { get { return "ColorName1ColorKey"; } }  
        public static string ColorName1BrushKey { get { return "ColorName1BrushKey"; } }  
  
        public static string ColorName2ColorKey { get { return "ColorName2ColorKey"; } }  
        public static string ColorName2BrushKey { get { return "ColorName2BrushKey"; } }  
        public static string ColorName2TextColorKey { get { return "ColorName2TextColorKey"; } }  
        public static string ColorName2TextBrushKey { get { return "ColorName2TextBrushKey"; } }  
  
        public static string ColorName3ColorKey { get { return "ColorName4ColorKey"; } }  
        public static string ColorName3BrushKey { get { return "ColorName4BrushKey"; } }  
        public static string ColorName3TextColorKey { get { return "ColorName4TextColorKey"; } }  
        public static string ColorName3TextBrushKey { get { return "ColorName4TextBrushKey"; } }  
        #endregion  
    }  
}  
```  
  
 **Wrapper de dicionário de recursos do WPF**  
  
 A cor **ResourceDictionary** chaves geradas pela ferramenta será semelhantes a este:  
  
```xaml  
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"  
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"  
        xmlns:colors="clr-namespace:MyNamespace">  
  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName1BrushKey}" Color="#FFFFFFFF" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName1ColorKey}" A="255" R="255" G="255" B="255" />  
  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2BrushKey}" Color="#FFFFFFFF" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName2ColorKey}" A="255" R="255" G="255" B="255" />  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName2TextBrushKey}" Color="#FF000000" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName2TextColorKey}" A="255" R="0" G="0" B="0" />  
  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName3BrushKey}" Color="#FFFF0000" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName3ColorKey}" A="255" R="255" G="0" B="0" />  
  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4BrushKey}" Color="#FF000088" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName4ColorKey}" A="255" R="0" G="0" B="136" />  
  <SolidColorBrush x:Key="{x:Static colors:MyColors.ColorName4TextBrushKey}" Color="#FFFFFFFF" />  
  <Color x:Key="{x:Static colors:MyColors.ColorName4TextColorKey}" A="255" R="255" G="255" B="255" />  
</ResourceDictionary>  
```

