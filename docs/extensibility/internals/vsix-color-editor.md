---
title: Editor de Cores do VSIX | Microsoft Docs
description: Saiba mais sobre a Visual Studio editor de cores da extensão, que pode criar e editar cores personalizadas para Visual Studio e gerar chaves de recurso de tema.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 70879c5d-e0f0-4845-993c-2f4229869706
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 95fec01beabb66180089a75e772b40788a1f7f0d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898934"
---
# <a name="vsix-color-editor"></a>Editor de cores do VSIX
A Visual Studio editor de cores da extensão pode criar e editar cores personalizadas para Visual Studio. A ferramenta também pode gerar chaves de recurso de tema para que as cores possam ser usadas no código. Essa ferramenta é útil para criar cores para uma extensão Visual Studio que dá suporte a temas. Essa ferramenta pode abrir arquivos .pkgdef e .xml dados. Visual Studio temas (arquivos .vstheme) podem ser usados com o Editor de Cores da Extensão Visual Studio alterando a extensão de arquivo para .xml. Além disso, os arquivos .vstheme podem ser importados para um arquivo .xml atual.

 ![VSIX Color Editor Hero](../../extensibility/internals/media/vsix-color-editor-hero.png "VSIX Color Editor Hero")

 **Arquivos de definição de pacote**

 Arquivos de definição de pacote (.pkgdef) são os arquivos que definem temas. As cores em si são armazenadas na cor do .xml arquivos, que são compilados em um arquivo .pkgdef. Os arquivos .pkgdef são implantados Visual Studio locais pesquisáveis, processados em tempo de executar e mesclados para definir temas.

 **Tokens de cores**

 Um token de cor é feito de quatro elementos:

- **Nome da categoria:** Um grupo lógico para um conjunto de cores. Use um nome de categoria existente se já houver cores específicas para o elemento de interface do usuário desejado ou grupo de elementos da interface do usuário.

- **Nome do token:** Um nome descritivo para o token de cor e os conjuntos de tokens. Os conjuntos incluem nomes de token em segundo plano (texto), bem como todos os seus estados, e eles devem ser nomeados para que seja fácil identificar os pares e os estados aos quais eles se aplicam.

- **Valores de cor (ou matizs):** Necessário para cada tema colorido. Sempre crie valores de cor de tela de fundo e texto em pares. As cores são emparelhadas para plano de fundo/primeiro plano para que a cor do texto (primeiro plano) seja sempre acessível em relação à cor da tela de fundo na qual ela é desenhada. Essas cores são vinculadas e serão usadas juntas na interface do usuário. Se a tela de fundo não se destina ao uso com texto, não defina uma cor de primeiro plano.

- **Nome da cor do sistema:** Para uso em exibições de alto contraste.

## <a name="how-to-use-the-tool"></a>Como usar a ferramenta
 Tanto quanto possível e, quando apropriado, as cores Visual Studio existentes devem ser reutilizadas em vez de criar novas. No entanto, para casos em que nenhuma cor apropriada é definida, as cores personalizadas devem ser criadas para manter uma extensão com temas compatíveis.

 **Criando novos tokens de cores**

 Para criar cores personalizadas usando o Visual Studio de Cores da Extensão, siga estas etapas:

1. Determine os nomes de categoria e token para os novos tokens de cor.

2. Escolha os matizes que o elemento de interface do usuário usará para cada tema e a cor do sistema para Alto Contraste.

3. Use o editor de cores para criar novos tokens de cor.

4. Use as cores em uma extensão Visual Studio dados.

5. Teste as alterações no Visual Studio.

   **Etapa 1: Determinar os nomes de categoria e token para os novos tokens de cor.**

   O esquema de nomenlização preferencial para um VSColor **é [Categoria] [tipo de interface do usuário] [Estado]**. Não use a palavra "cor" em nomes VSColor, pois ela é redundante.

   Os nomes de categoria fornecem agrupamentos lógicos e devem ser definidos o mais restrito possível. Por exemplo, o nome de uma única janela de ferramentas pode ser um nome de categoria, mas o nome de uma unidade de negócios inteira ou equipe de projeto não é. Agrupar entradas em categorias ajuda a evitar confusão entre cores com o mesmo nome.

   Um nome de token deve indicar claramente o tipo de elemento e as situações, ou "estado", para o qual a cor será aplicada. Por exemplo, o [tipo de interface do **usuário]** de uma dica de dados ativa pode ser chamado de "**DataTip**" e **o [Estado]** pode ser chamado de "**Ativo**", resultando em um nome de cor de "**DataTipActive**." Como as dicas de dados têm texto, um primeiro plano e uma cor da tela de fundo precisam ser definidos. Usando um emparelhamento em segundo plano/plano de fundo, o editor de cores criará automaticamente as cores "**DataTipActive**" para a tela de fundo e "**DataTipActiveText**" para o primeiro plano.

   Se a parte da interface do usuário tiver apenas um estado, a parte **[Estado]** do nome poderá ser omitida. Por exemplo, se uma caixa de pesquisa tiver uma borda e não houver nenhuma alteração de estado que afete a cor da borda, o nome do token de cor da borda poderá simplesmente ser chamado de "**SearchBoxBorder**."

   Alguns nomes de estado comuns incluem:

- Ativo

- Inativo

- MouseOver

- Mousedown

- Selecionada

- Focalizado

  Exemplos de alguns nomes de token para partes de um controle de item de lista:

- Listitem

- ListItemBorder

- ListItemMouseOver

- ListItemMouseOverBorder

- ListItemSelected

- ListItemSelectedBorder

- ListItemDisabled

- ListItemDisabledBorder

  **Etapa 2: escolha os matizes que o elemento de interface do usuário usará para cada tema e a cor do sistema para Alto Contraste.**

  Ao escolher cores personalizadas para a interface do usuário, selecione um elemento de interface do usuário existente semelhante e use suas cores como base. As cores dos elementos de interface do usuário in-the-box passaram por revisão e teste, portanto, eles terão a aparência apropriada e se comportarão corretamente em todos os temas.

  **Etapa 3: usar o editor de cores para criar novos tokens de cor.**

  Iniciar o editor de cores e abrir ou criar um novo arquivo de cores .xml tema personalizado. Selecione **Editar > Nova Cor** no menu. Isso abre uma caixa de diálogo para especificar a categoria e um ou mais nomes para entradas de cores dentro dessa categoria:

  ![Nova cor do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-color.png "Nova cor do Editor de Cores do VSIX")

  Selecione uma categoria existente ou selecione **Nova Categoria** para criar uma nova categoria. Outra caixa de diálogo será aberta, criando um novo nome de categoria:

  ![Nova categoria do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-category.png "Nova categoria do Editor de Cores do VSIX")

  A nova categoria ficará disponível no menu suspenso categoria **Nova** Cor. Depois de escolher uma categoria, insira um nome por linha para cada novo token de cor e selecione "Criar" quando terminar:

  ![Nova cor preenchida do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-color-filled.png "Nova cor preenchida do Editor de Cores do VSIX")

  Os valores de cor são mostrados em pares de plano de fundo/primeiro plano, com "Nenhum" indicando que a cor não foi definida. Observação: se uma cor não tiver um par de cores de texto/cor da tela de fundo, somente a tela de fundo precisará ser definida.

  ![Valores de cor do editor de cores vsix](../../extensibility/internals/media/vsix-color-editor-color-values.png "Valores de cor do editor de cores vsix")

  Para editar um token de cor, selecione uma entrada de cor para o tema (coluna) desse token. Adicione o valor de cor digitando um valor de cor hexatória no formato ARGB de 8 dígitos, inserindo um nome de cor do sistema na célula ou usando o menu suspenso para selecionar a cor desejada por meio de um conjunto de controles deslizantes de cores ou uma lista de cores do sistema.

  ![Cor da edição do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-edit-color.png "Cor da edição do Editor de Cores do VSIX")

  ![Tela de fundo do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-background.png "Tela de fundo do Editor de Cores do VSIX")

  Para componentes que não precisam exibir texto, insira apenas um valor de cor: a cor da tela de fundo. Caso contrário, insira valores para a tela de fundo e a cor do texto, separados por uma barra.

  Ao inserir valores para Alto Contraste, insira nomes de cores válidos do sistema Windows. Não insira valores ARGB em código. Você pode exibir uma lista de nomes de cores do sistema válidos selecionando "Tela de fundo: Sistema" ou "Primeiro plano: Sistema" nos menus suspensos do valor de cor. Ao criar elementos que têm componentes de texto, use o par de cores do sistema de texto/tela de fundo correto ou o texto poderá ser ilegível.

  Quando terminar de criar, definir e editar os tokens de cor, salve-os no formato .xml ou .pkgdef desejado. Tokens de cores sem uma tela de fundo nem um conjunto de primeiro plano serão salvos como cores vazias no formato .xml, mas descartados no formato .pkgdef. Uma caixa de diálogo avisará você sobre a possível perda de cores se você tentar salvar cores vazias em um arquivo .pkgdef.

  **Etapa 4: use as cores em uma extensão Visual Studio dados.**

  Depois de definir os novos tokens de cor, inclua o .pkgdef no arquivo de projeto com "Ação de Build" definida como "Conteúdo" e "Incluir no VSIX" definido como "True".

  ![Pkgdef do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-pkgdef.png "Pkgdef do Editor de Cores do VSIX")

  No Editor de Cores Visual Studio Extensão, escolha Arquivo > Exibir Código do Recurso para exibir o código usado para acessar as cores personalizadas na interface do usuário baseada em WPF.

  ![Visualizador de Código de Recurso do Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-resource-code-viewer.png "Visualizador de Código de Recurso do Editor de Cores do VSIX")

  Inclua esse código em uma classe estática no projeto. Uma referência a **Microsoft.VisualStudio.Shell. \<VSVersion>.0.dll** precisa ser adicionada ao projeto para usar o tipo **ThemeResourceKey.**

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

 Isso permite o acesso às cores no código XAML e permite que a interface do usuário responda às alterações de tema.

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

 **Etapa 5: Testar as alterações no Visual Studio.**

 O editor de cores pode aplicar temporariamente tokens de cor às instâncias em execução do Visual Studio para exibir alterações ao vivo nas cores sem recriar o pacote de extensão. Para fazer isso, clique no botão "Aplicar este tema Visual Studio janelas" localizado no header de cada coluna de tema. Esse tema temporário desaparecerá quando o Editor de Cores do VSIX for fechado.

 ![Aplicar Editor de Cores do VSIX](../../extensibility/internals/media/vsix-color-editor-apply.png "Aplicar Editor de Cores do VSIX")

 Para tornar as alterações permanentes, reimplante e reimplante a extensão Visual Studio depois de adicionar as novas cores ao arquivo .pkgdef e escrever o código que usará essas cores. A recriação Visual Studio extensão de Visual Studio mescla os valores do Registro para as novas cores no restante dos temas. Em seguida, relançar Visual Studio, exibir a interface do usuário e verificar se as novas cores aparecem conforme o esperado.

## <a name="notes"></a>Observações
 Essa ferramenta destina-se a ser usada para criar cores personalizadas para os temas Visual Studio pré-Visual Studio ou para editar as cores de um tema Visual Studio personalizado. Para criar temas Visual Studio personalizados completos, baixe Visual Studio extensão [do Editor](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.VisualStudio2015ColorThemeEditor) de Tema de Cores da Visual Studio Extensões.

## <a name="sample-output"></a>Saída de exemplo
 **Saída de cor XML**

 O .xml gerado pela ferramenta será semelhante a este:

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

 O arquivo .pkgdef gerado pela ferramenta será semelhante a este:

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

 **Wrapper de chaves de recurso C#**

 As chaves de recurso de cor geradas pela ferramenta serão semelhantes a esta:

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

 A cor **das chaves ResourceDictionary** geradas pela ferramenta será semelhante a esta:

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
