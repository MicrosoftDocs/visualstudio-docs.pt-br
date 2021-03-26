---
title: Editor de cores do VSIX | Microsoft Docs
description: Saiba mais sobre a ferramenta Editor de cores de extensão do Visual Studio, que pode criar e Editar cores personalizadas para o Visual Studio e gerar chaves de recurso de tema.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 70879c5d-e0f0-4845-993c-2f4229869706
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bfd6ff388119d829c2e5994c0fa78d01958326bc
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069277"
---
# <a name="vsix-color-editor"></a>Editor de cores do VSIX
A ferramenta Editor de cores de extensão do Visual Studio pode criar e Editar cores personalizadas para o Visual Studio. A ferramenta também pode gerar chaves de recursos de tema para que as cores possam ser usadas no código. Essa ferramenta é útil para fazer cores para uma extensão do Visual Studio que dá suporte a elas. Essa ferramenta pode abrir arquivos. pkgdef e. xml. Os temas do Visual Studio (arquivos. vstheme) podem ser usados com o editor de cores de extensão do Visual Studio, alterando a extensão de arquivo para. xml. Além disso, os arquivos. vstheme podem ser importados para um arquivo. XML atual.

 ![Herói do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-hero.png "Herói do editor de cores do VSIX")

 **Arquivos de definição de pacote**

 Os arquivos de definição de pacote (. pkgdef) são os arquivos que definem temas. As próprias cores são armazenadas em arquivos Color. XML de tema, que são compilados em um arquivo. pkgdef. Os arquivos. pkgdef são implantados em locais pesquisáveis do Visual Studio, processados em tempo de execução e mesclados juntos para definir temas.

 **Tokens de cor**

 Um token de cor é composto de quatro elementos:

- **Nome da categoria:** Um agrupamento lógico para um conjunto de cores. Use um nome de categoria existente se já houver cores específicas para o elemento de interface do usuário desejado ou para o grupo de elementos da interface do usuário.

- **Nome do token:** Um nome descritivo para o token de cor e conjuntos de tokens. Os conjuntos incluem nomes de token em segundo plano e em primeiro plano (texto), bem como todos os seus Estados, e eles devem ser nomeados para que seja fácil identificar os pares e os Estados aos quais eles se aplicam.

- **Valores de cor (ou matizes):** Necessário para cada tema colorido. Sempre crie valores de cor de texto e segundo plano em pares. As cores são emparelhadas para o plano de fundo/primeiro plano para que a cor do texto (primeiro plano) seja sempre legível em relação à cor do plano de fundo na qual ela é desenhada. Essas cores são vinculadas e serão usadas juntas na interface do usuário. Se o plano de fundo não for usado com texto, não defina uma cor de primeiro plano.

- **Nome da cor do sistema:** Para uso em monitores de alto contraste.

## <a name="how-to-use-the-tool"></a>Como usar a ferramenta
 Tanto quanto possível, e quando apropriado, as cores existentes do Visual Studio devem ser reutilizadas em vez de fazer novas. No entanto, para casos em que nenhuma cor apropriada é definida, as cores personalizadas devem ser criadas para manter uma extensão compatível com elas.

 **Criando novos tokens de cor**

 Para criar cores personalizadas usando o editor de cores de extensão do Visual Studio, siga estas etapas:

1. Determine os nomes de categoria e token para os novos tokens de cor.

2. Escolha o matiz que o elemento da interface do usuário usará para cada tema e a cor do sistema para Alto Contraste.

3. Use o editor de cores para criar novos tokens de cor.

4. Use as cores em uma extensão do Visual Studio.

5. Teste as alterações no Visual Studio.

   **Etapa 1: determinar os nomes de categoria e token para os novos tokens de cor.**

   O esquema de nomenclatura preferencial para um VSColor é **[categoria] [tipo de interface do usuário] [estado]**. Não use a palavra "Color" em nomes de VSColor, pois ela é redundante.

   Os nomes de categoria fornecem agrupamentos lógicos e devem ser definidos da forma mais restrita possível. Por exemplo, o nome de uma única janela de ferramenta pode ser um nome de categoria, mas o nome de uma unidade de negócios ou equipe de projeto inteira não é. O agrupamento de entradas em categorias ajuda a evitar a confusão entre as cores com o mesmo nome.

   Um nome de token deve indicar claramente o tipo de elemento e as situações, ou "estado", para os quais a cor será aplicada. Por exemplo, um **[tipo de interface do usuário]** de uma dica de dados ativa pode ser nomeado "**DataTip**" e **[state]** poderia ser denominado "**Active**", resultando em um nome de cor "**DataTipActive**". Como as dicas de dados têm texto, é necessário definir uma cor de primeiro plano e de plano de fundo. Usando um emparelhamento em segundo plano/primeiro plano, o editor de cores criará automaticamente as cores "**DataTipActive**" para o plano de fundo e "**DataTipActiveText**" para o primeiro plano.

   Se o trecho da interface do usuário tiver apenas um estado, a parte **[state]** do nome poderá ser omitida. Por exemplo, se uma caixa de pesquisa tiver uma borda e não houver nenhuma alteração de estado que afete a cor da borda, o nome do token de cor da borda poderá simplesmente ser chamado de "**SearchBoxBorder**".

   Alguns nomes de estado comuns incluem:

- Ativo

- Inativo

- MouseOver

- MouseDown

- Selecionada

- Focalizado

  Exemplos de alguns nomes de token para partes de um controle de item de lista:

- Item

- ListItemBorder

- ListItemMouseOver

- ListItemMouseOverBorder

- ListItemSelected

- ListItemSelectedBorder

- ListItemDisabled

- ListItemDisabledBorder

  **Etapa 2: escolha o matiz que o elemento da interface do usuário usará para cada tema e a cor do sistema para Alto Contraste.**

  Ao escolher cores personalizadas para a interface do usuário, selecione um elemento de interface do usuário existente semelhante e use suas cores como base. As cores dos elementos da interface do usuário na caixa têm passou na revisão e no teste. portanto, eles terão a aparência apropriada e se comportarão corretamente em todos os temas.

  **Etapa 3: Use o editor de cores para criar novos tokens de cor.**

  Inicie o editor de cores e abra ou crie um novo arquivo Colors. XML do tema personalizado. Selecione **editar > nova cor** no menu. Isso abre uma caixa de diálogo para especificar a categoria e um ou mais nomes para entradas de cor dentro dessa categoria:

  ![Nova cor do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-color.png "Nova cor do editor de cores do VSIX")

  Selecione uma categoria existente ou selecione **nova categoria** para criar uma nova categoria. Outra caixa de diálogo será aberta, criando um novo nome de categoria:

  ![Nova categoria do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-new-category.png "Nova categoria do editor de cores do VSIX")

  A nova categoria ficará disponível no menu suspenso nova categoria de **cor** . Depois de escolher uma categoria, insira um nome por linha para cada novo token de cor e selecione "criar" quando terminar:

  ![Nova cor do editor de cores do VSIX preenchida](../../extensibility/internals/media/vsix-color-editor-new-color-filled.png "Nova cor do editor de cores do VSIX preenchida")

  Os valores de cor são mostrados em pares de plano de fundo/primeiro plano, com "nenhum" indicando que a cor não foi definida. Observação: se uma cor não tiver um par de cores de texto/cor do plano de fundo, somente o plano de fundo precisará ser definido.

  ![Valores de cor do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-color-values.png "Valores de cor do editor de cores do VSIX")

  Para editar um token de cor, selecione uma entrada de cor para o tema (coluna) desse token. Adicione o valor de cor digitando um valor de cor hexadecimal no formato ARGB de 8 dígitos, inserindo um nome de cor do sistema na célula ou usando o menu suspenso para selecionar a cor desejada por meio de um conjunto de controles deslizantes de cor ou uma lista de cores do sistema.

  ![Cor de edição do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-edit-color.png "Cor de edição do editor de cores do VSIX")

  ![Plano de fundo do editor de cores do VSIX](../../extensibility/internals/media/vsix-color-editor-background.png "Plano de fundo do editor de cores do VSIX")

  Para componentes que não precisam exibir texto, insira apenas um valor de cor: a cor da tela de fundo. Caso contrário, insira valores para a cor do texto e do plano de fundo, separados por uma barra.

  Ao inserir valores para Alto Contraste, insira nomes de cor de sistema do Windows válidos. Não insira valores ARGB codificados. Você pode exibir uma lista de nomes de cores do sistema válidos selecionando "plano de fundo: sistema" ou "primeiro plano: sistema" nos menus suspensos de valor de cor. Ao criar elementos que têm componentes de texto, use o par de cores do sistema de texto/plano de fundo correto ou o texto pode ser ilegível.

  Quando você terminar de criar, configurar e editar os tokens de cor, salve-os no formato. xml ou. pkgdef desejado. Os tokens de cor sem nenhum plano de fundo nem um conjunto de primeiro plano serão salvos como cores vazias no formato. xml, mas descartados no formato. pkgdef. Uma caixa de diálogo avisará sobre possíveis perdas de cores se você tentar salvar cores vazias em um arquivo. pkgdef.

  **Etapa 4: usar as cores em uma extensão do Visual Studio.**

  Depois de definir os novos tokens de cor, inclua o. pkgdef no arquivo de projeto com a "ação de compilação" definida como "conteúdo" e "incluir no VSIX" definido como "verdadeiro".

  ![Editor de cores do VSIX pkgdef](../../extensibility/internals/media/vsix-color-editor-pkgdef.png "Editor de cores do VSIX pkgdef")

  No editor de cores de extensão do Visual Studio, escolha Arquivo > exibir código de recurso para exibir o código usado para acessar as cores personalizadas na interface do usuário baseada no WPF.

  ![Visualizador de código de recurso do editor de cores VSIX](../../extensibility/internals/media/vsix-color-editor-resource-code-viewer.png "Visualizador de código de recurso do editor de cores VSIX")

  Inclua esse código em uma classe estática no projeto. Uma referência a **Microsoft. VisualStudio. Shell. \<VSVersion>.0.dll** precisa ser adicionada ao projeto para usar o tipo **a themeresourcekey** .

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

 Isso permite o acesso às cores no código XAML e permite que a interface do usuário responda às alterações do tema.

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

 **Etapa 5: testar as alterações no Visual Studio.**

 O editor de cores pode aplicar temporariamente os tokens de cor às instâncias em execução do Visual Studio para exibir alterações dinâmicas em cores sem recriar o pacote de extensão. Para fazer isso, clique no botão "aplicar este tema ao Windows executando o Visual Studio" localizado no cabeçalho de cada coluna de tema. Esse tema temporário desaparece quando o editor de cores VSIX é fechado.

 ![Editor de cores do VSIX aplicar](../../extensibility/internals/media/vsix-color-editor-apply.png "Editor de cores do VSIX aplicar")

 Para tornar as alterações permanentes, recompile e reimplante a extensão do Visual Studio depois de adicionar as novas cores ao arquivo. pkgdef e gravar o código que usará essas cores. A recriação da extensão do Visual Studio mesclará os valores do registro para as novas cores no restante dos temas. Em seguida, reinicie o Visual Studio, exiba a interface do usuário e verifique se as novas cores aparecem conforme o esperado.

## <a name="notes"></a>Anotações
 Essa ferramenta deve ser usada para criar cores personalizadas para os temas preexistentes do Visual Studio ou para editar as cores de um tema personalizado do Visual Studio. Para criar temas personalizados do Visual Studio, baixe a [extensão do editor de tema de cores do Visual Studio](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.VisualStudio2015ColorThemeEditor) na Galeria de extensões do Visual Studio.

## <a name="sample-output"></a>Saída de exemplo
 **Saída de cor XML**

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

 **Saída de cor do PKGDEF**

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

 **Wrapper de chaves de recurso do C#**

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

 **Invólucro do dicionário de recursos do WPF**

 As chaves de **ResourceDictionary** de cores geradas pela ferramenta serão semelhantes a esta:

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
