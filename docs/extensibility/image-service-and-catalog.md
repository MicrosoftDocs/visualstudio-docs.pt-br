---
title: Serviço de imagem e catálogo | Microsoft Docs
ms.date: 04/01/2019
ms.topic: conceptual
ms.assetid: 34990c37-ae98-4140-9b1e-a91c192220d9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 7df93a801b5ec34a433849baa41f2fd255790c86
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536325"
---
# <a name="image-service-and-catalog"></a>Serviço de imagem e catálogo
Este manual contém diretrizes e práticas recomendadas para adotar o serviço de imagem do Visual Studio e o catálogo de imagens introduzidos no Visual Studio 2015.

 O serviço de imagem introduzido no Visual Studio 2015 permite que os desenvolvedores obtenham as melhores imagens para o dispositivo e o tema escolhido pelo usuário para exibir a imagem, incluindo as correções corretas para o contexto no qual elas são exibidas. A adoção do serviço de imagem ajudará a eliminar os principais pontos problemáticos relacionados à manutenção de ativos, ao dimensionamento de HDPI e a temas.

|**Problemas hoje**|**Soluções**|
|-|-|
|Mistura de cores de plano de fundo|Mesclagem alfa interna|
|(Algumas) imagens|Metadados do tema|
|Modo de Alto Contraste|Recursos de Alto Contraste alternativos|
|Precisa de vários recursos para modos de DPI diferentes|Recursos selecionáveis com fallback baseado em vetor|
|Duplicar imagens|Um identificador por conceito de imagem|

 Por que adotar o serviço de imagem?

- Sempre obtenha a imagem mais recente de "pixel-perfeito" do Visual Studio

- Você pode enviar e usar suas próprias imagens

- Não há necessidade de testar suas imagens quando o Windows adiciona novo dimensionamento de DPI

- Resolva barreiras de arquitetura antigas em suas implementações

  A barra de ferramentas do shell do Visual Studio antes e depois de usar o serviço de imagem:

  ![Serviço de imagem antes e depois](../extensibility/media/image-service-before-and-after.png "Serviço de imagem antes e depois")

## <a name="how-it-works"></a>Como ele funciona
 O serviço de imagem pode fornecer uma imagem de bitmap adequada para qualquer estrutura de interface do usuário com suporte:

- WPF: BitmapSource

- WinForms: System. Drawing. bitmap

- Win32: HBITMAP

  Diagrama de fluxo do serviço de imagem

  ![Diagrama de fluxo do serviço de imagem](../extensibility/media/image-service-flow-diagram.png "Diagrama de fluxo do serviço de imagem")

  **Monikers de imagem**

  Um moniker de imagem (ou moniker para curto) é um par de GUID/ID que identifica exclusivamente um ativo de imagem ou ativos de lista de imagens na biblioteca de imagens.

  **Identificadores conhecidos**

  O conjunto de monikers de imagem contidos no catálogo de imagens do Visual Studio e publicamente consumível por qualquer componente ou extensão do Visual Studio.

  **Arquivos de manifesto de imagem**

  Os arquivos de manifesto de imagem (*. imagemanifest*) são arquivos XML que definem um conjunto de ativos de imagem, os monikers que representam esses ativos e a imagem real ou imagens que representam cada ativo. Os manifestos de imagem podem definir imagens autônomas ou listas de imagens para suporte de interface do usuário herdado. Além disso, há atributos que podem ser definidos no ativo ou nas imagens individuais por trás de cada ativo para alterar quando e como esses ativos são exibidos.

  **Esquema de manifesto de imagem**

  Um manifesto de imagem completo tem esta aparência:

```xml
<ImageManifest>
      <!-- zero or one Symbols elements -->
      <Symbols>
        <!-- zero or more Import, Guid, ID, or String elements -->
      </Symbols>
      <!-- zero or one Images elements -->
      <Images>
        <!-- zero or more Image elements -->
      </Images>
      <!-- zero or one ImageLists elements -->
      <ImageLists>
        <!-- zero or more ImageList elements -->
      </ImageLists>
</ImageManifest>
```

 **Símbolos**

 Como auxílio à legibilidade e à manutenção, o manifesto da imagem pode usar símbolos para valores de atributo. Os símbolos são definidos da seguinte maneira:

```xml
<Symbols>
      <Import Manifest="manifest" />
      <Guid Name="ShellCommandGuid" Value="8ee4f65d-bab4-4cde-b8e7-ac412abbda8a" />
      <ID Name="cmdidSaveAll" Value="1000" />
      <String Name="AssemblyName" Value="Microsoft.VisualStudio.Shell.UI.Internal" />
</Symbols>
```

|**Subelemento**|**Definição**|
|-|-|
|Importar|Importa os símbolos do arquivo de manifesto fornecido para uso no manifesto atual|
|Guid|O símbolo representa um GUID e deve corresponder à formatação do GUID|
|ID|O símbolo representa uma ID e deve ser um inteiro não negativo|
|String|O símbolo representa um valor de cadeia de caracteres arbitrária|

 Os símbolos diferenciam maiúsculas de minúsculas e são referenciados usando a sintaxe $ (Symbol-Name):

```xml
<Image Guid="$(ShellCommandGuid)" ID="$(cmdidSaveAll)" >
      <Source Uri="/$(AssemblyName);Component/Resources/image.xaml" />
</Image>
```

 Alguns símbolos são predefinidos para todos os manifestos. Eles podem ser usados no atributo URI do \<Source> \<Import> elemento ou para fazer referência a caminhos no computador local.

|**Símbolo**|**Descrição**|
|-|-|
|CommonProgramFiles|O valor da variável de ambiente% CommonProgramFiles%|
|LocalAppData|O valor da variável de ambiente% LocalAppData%|
|ManifestFolder|A pasta que contém o arquivo de manifesto|
|MyDocuments|O caminho completo da pasta meus documentos do usuário atual|
|ProgramFiles|O valor da variável de ambiente% ProgramFiles%|
|Sistema|A pasta *Windows\System32*|
|WinDir|O valor da variável de ambiente% WinDir%|

 **Imagem**

 O \<Image> elemento define uma imagem que pode ser referenciada por um moniker. O GUID e a ID agrupados formam o moniker da imagem. O moniker da imagem deve ser exclusivo em toda a biblioteca de imagens. Se mais de uma imagem tiver um determinado moniker, o primeiro encontrado durante a criação da biblioteca é aquele que é mantido.

 Ele deve conter pelo menos uma fonte. Fontes de tamanho neutro fornecerão os melhores resultados em uma grande variedade de tamanhos, mas eles não são obrigatórios. Se o serviço for solicitado a fornecer uma imagem de um tamanho não definido no \<Image> elemento e não houver fonte de tamanho neutro, o serviço escolherá a melhor fonte de tamanho específico e a dimensionará para o tamanho solicitado.

```xml
<Image Guid="guid" ID="int" AllowColorInversion="true/false">
      <Source ... />
      <!-- optional additional Source elements -->
</Image>
```

|**Atributo**|**Definição**|
|-|-|
|Guid|Necessária A parte GUID do moniker da imagem|
|ID|Necessária A parte de ID do moniker da imagem|
|AllowColorInversion|[Opcional, padrão verdadeiro] Indica se a imagem pode ter suas cores programaticamente invertidas quando usada em um plano de fundo escuro.|

 **Origem**

 O \<Source> elemento define um ativo de origem de imagem única (XAML e png).

```xml
<Source Uri="uri" Background="background">
      <!-- optional NativeResource element -->
 </Source>
```

|**Atributo**|**Definição**|
|-|-|
|Uri|Necessária Um URI que define de onde a imagem pode ser carregada. Pode ser um dos seguintes:<br /><br /> -Um [pacote URI](/dotnet/framework/wpf/app-development/pack-uris-in-wpf) usando a autoridade Application:///<br />-Uma referência de recurso de componente absoluto<br />-Um caminho para um arquivo que contém um recurso nativo|
|Segundo plano|Adicional Indica em que tipo de plano de fundo a origem deve ser usada.<br /><br /> Pode ser um dos seguintes:<br /><br /> *Luz:* A origem pode ser usada em um plano de fundo claro.<br /><br /> *Escuro:* A origem pode ser usada em um plano de fundo escuro.<br /><br /> *HighContrast:* A origem pode ser usada em qualquer plano de fundo no modo de Alto Contraste.<br /><br /> *HighContrastLight:* A origem pode ser usada em um plano de fundo claro no modo de Alto Contraste.<br /><br /> *HighContrastDark:* A origem pode ser usada em um plano de fundo escuro no modo de Alto Contraste.<br /><br /> Se o atributo de plano de fundo for omitido, a origem poderá ser usada em qualquer plano de fundo.<br /><br /> Se o plano de fundo for *claro*, *escuro*, *HighContrastLight*ou *HighContrastDark*, as cores da fonte nunca serão invertidas. Se o plano de fundo for omitido ou definido como *HighContrast*, a inversão das cores da origem será controlada pelo atributo **AllowColorInversion** da imagem.|

Um \<Source> elemento pode ter exatamente um dos seguintes subelementos opcionais:

|**Elemento**|**Atributos (todos obrigatórios)**|**Definição**|
|-|-|-|
|\<Size>|Valor|A fonte será usada para imagens do tamanho determinado (em unidades do dispositivo). A imagem será quadrada.|
|\<SizeRange>|MinSize, MaxSize|A fonte será usada para imagens de MinSize para MaxSize (em unidades de dispositivo) inclusivamente. A imagem será quadrada.|
|\<Dimensions>|Largura, Altura|A fonte será usada para imagens da largura e da altura especificadas (em unidades do dispositivo).|
|\<DimensionRange>|MinWidth, MinHeight,<br /><br /> MaxWidth, MaxHeight|A fonte será usada para imagens da largura/altura mínima até a largura/altura máxima (em unidades do dispositivo), inclusive.|

 Um \<Source> elemento também pode ter um \<NativeResource> subelemento opcional, que define um \<Source> que é carregado de um assembly nativo em vez de um assembly gerenciado.

```xml
<NativeResource Type="type" ID="int" />
```

|**Atributo**|**Definição**|
|-|-|
|Type|Necessária O tipo do recurso nativo, XAML ou PNG|
|ID|Necessária A parte da ID de número inteiro do recurso nativo|

 **ImageList**

 O \<ImageList> elemento define uma coleção de imagens que podem ser retornadas em uma única faixa. A faixa é criada sob demanda, conforme necessário.

```xml
<ImageList>
      <ContainedImage Guid="guid" ID="int" External="true/false" />
      <!-- optional additional ContainedImage elements -->
 </ImageList>
```

|**Atributo**|**Definição**|
|-|-|
|Guid|Necessária A parte GUID do moniker da imagem|
|ID|Necessária A parte de ID do moniker da imagem|
|Externo|[Opcional, padrão false] Indica se o moniker da imagem faz referência a uma imagem no manifesto atual.|

 O moniker para a imagem contida não precisa fazer referência a uma imagem definida no manifesto atual. Se a imagem contida não puder ser encontrada na biblioteca de imagens, uma imagem de espaço reservado em branco será usada em seu lugar.

## <a name="using-the-image-service"></a>Usando o serviço de imagem

### <a name="first-steps-managed"></a>Primeiras etapas (gerenciadas)
 Para usar o serviço de imagem, você precisa adicionar referências a alguns ou todos os assemblies a seguir ao seu projeto:

- *Microsoft.VisualStudio.ImageCatalog.dll*

  - Necessário se você usar o **KnownMonikers**do catálogo de imagens interno.

- *Microsoft.VisualStudio.Imaging.dll*

  - Necessário se você usar **CrispImage** e **ImageThemingUtilities** em sua interface do usuário do WPF.

- *Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime.dll*

  - Necessário se você usar os tipos **ImageMoniker** e **ImageAttributes** .

  - **EmbedInteropTypes** deve ser definido como true.

- *Microsoft. VisualStudio. Shell. Interop. 14.0. designtime*

  - Necessário se você usar o tipo **IVsImageService2** .

  - **EmbedInteropTypes** deve ser definido como true.

- *Microsoft.VisualStudio.Utilities.dll*

  - Necessário se você usar o **BrushToColorConverter** para **ImageThemingUtilities. ImageBackgroundColor** em sua interface do usuário do WPF.

- *Microsoft. VisualStudio. Shell. \<VSVersion> . 0*

  - Necessário se você usar o tipo **IVsUIObject** .

- *Microsoft.VisualStudio.Shell.Interop.10.0.dll*

  - Necessário se você usar os auxiliares de interface do usuário relacionados ao WinForms.

  - **EmbedInteropTypes** deve ser definido como true

### <a name="first-steps-native"></a>Primeiras etapas (nativas)
 Para usar o serviço de imagem, você precisa incluir alguns ou todos os cabeçalhos a seguir em seu projeto:

- **KnownImageIds. h**

  - Necessário se você usar o **KnownMonikers**do catálogo de imagens interno, mas não puder usar o tipo **ImageMoniker** , como ao retornar valores de chamadas **getguidproperty** ou **GetProperty** .

- **KnownMonikers. h**

  - Necessário se você usar o **KnownMonikers**do catálogo de imagens interno.

- **ImageParameters140. h**

  - Necessário se você usar os tipos **ImageMoniker** e **ImageAttributes** .

- **VSShell140. h**

  - Necessário se você usar o tipo **IVsImageService2** .

- **ImageThemingUtilities. h**

  - Necessário se não for possível permitir que o serviço de imagem manipule-o para você.

  - Não use esse cabeçalho se o serviço de imagem puder manipular sua imagem.

::: moniker range="vs-2017"
- **VSUIDPIHelper. h**

  - Necessário se você usar os auxiliares de DPI para obter o DPI atual.

::: moniker-end

::: moniker range=">=vs-2019"
- **VsDpiAwareness. h**

  - Necessário se você usar os auxiliares de reconhecimento de DPI para obter o DPI atual.

::: moniker-end

## <a name="how-do-i-write-new-wpf-ui"></a>Como fazer escrever uma nova interface do usuário do WPF?

1. Comece adicionando as referências de assembly necessárias na seção sobre as primeiras etapas acima para o seu projeto. Você não precisa adicionar todos eles, portanto, adicione apenas as referências de que você precisa. (Observação: se você estiver usando ou tiver acesso a **cores** em vez de **pincéis**, poderá ignorar a referência a **utilitários**, já que você não precisará do conversor.)

2. Selecione a imagem desejada e obtenha seu moniker. Use um **KnownMoniker**ou use seu próprio se você tiver suas próprias imagens e monikers personalizados.

3. Adicione **CrispImages** ao seu XAML. (Veja o exemplo abaixo.)

4. Defina a propriedade **ImageThemingUtilities. ImageBackgroundColor** em sua hierarquia de interface do usuário. (Isso deve ser definido no local onde a cor do plano de fundo é conhecida, não necessariamente no **CrispImage**.) (Veja o exemplo abaixo.)

```xaml
<Window
  x:Class="WpfApplication.MainWindow"
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  xmlns:imaging="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:theming="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:utilities="clr-namespace:Microsoft.Internal.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.Imaging"
  xmlns:catalog="clr-namespace:Microsoft.VisualStudio.Imaging;assembly=Microsoft.VisualStudio.ImageCatalog"
  Title="MainWindow" Height="350" Width="525" UseLayoutRounding="True">
  <Window.Resources>
    <utilities:BrushToColorConverter x:Key="BrushToColorConverter"/>
  </Window.Resources>
  <StackPanel Background="White" VerticalAlignment="Center"
    theming:ImageThemingUtilities.ImageBackgroundColor="{Binding Background, RelativeSource={RelativeSource Self}, Converter={StaticResource BrushToColorConverter}}">
    <imaging:CrispImage Width="16" Height="16" Moniker="{x:Static catalog:KnownMonikers.MoveUp}" />
  </StackPanel>
</Window>
```

 **Como fazer atualizar a interface do usuário existente do WPF?**

 A atualização da interface do usuário existente do WPF é um processo relativamente simples, que consiste em três etapas básicas:

1. Substitua todos os \<Image> elementos em sua interface do usuário por \<CrispImage> elementos.

2. Altere todos os atributos de origem para atributos de moniker.

    - Se a imagem nunca for alterada e você estiver usando **KnownMonikers**, então, associe estaticamente essa propriedade ao **KnownMoniker**. (Consulte o exemplo acima.)

    - Se a imagem nunca for alterada e você estiver usando sua própria imagem personalizada, então associe-se estaticamente ao seu próprio moniker.

    - Se a imagem puder ser alterada, associe o atributo moniker a uma propriedade de código que notifique as alterações de propriedade.

3. Em algum lugar na hierarquia da interface do usuário, defina **ImageThemingUtilities. ImageBackgroundColor** para verificar se a inversão de cores funciona corretamente.

    - Isso pode exigir o uso da classe **BrushToColorConverter** . (Consulte o exemplo acima.)

## <a name="how-do-i-update-win32-ui"></a>Como fazer atualizar a interface do usuário do Win32?
 Adicione o seguinte ao seu código sempre que apropriado para substituir o carregamento bruto de imagens. Alterne valores para retornar HBITMAPs versus HICONs versus HIMAGELIST, conforme necessário.

 **Obter o serviço de imagem**

```cpp
CComPtr<IVsImageService2> spImgSvc;
CGlobalServiceProvider::HrQueryService(SID_SVsImageService, &spImgSvc);
```

 **Solicitando a imagem**

::: moniker range="vs-2017"

```cpp
ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = VsUI::DpiHelper::GetDeviceDpiX();
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

::: moniker range=">=vs-2019"

```cpp
UINT dpiX, dpiY;
HWND hwnd = // get the HWND where the image will be displayed
VsUI::CDpiAwareness::GetDpiForWindow(hwnd, &dpiX, &dpiY);

ImageAttributes attr = { 0 };
attr.StructSize      = sizeof(attributes);
attr.Format          = DF_Win32;
// IT_Bitmap for HBITMAP, IT_Icon for HICON, IT_ImageList for HIMAGELIST
attr.ImageType       = IT_Bitmap;
attr.LogicalWidth    = 16;
attr.LogicalHeight   = 16;
attr.Dpi             = dpiX;
// Desired RGBA color, if you don't use this, don't set IAF_Background below
attr.Background      = 0xFFFFFFFF;
attr.Flags           = IAF_RequiredFlags | IAF_Background;

CComPtr<IVsUIObject> spImg;
// Replace this KnownMoniker with your desired ImageMoniker
spImgSvc->GetImage(KnownMonikers::Blank, attributes, &spImg);
```

::: moniker-end

## <a name="how-do-i-update-winforms-ui"></a>Como fazer atualizar a interface do usuário WinForms?
 Adicione o seguinte ao seu código sempre que apropriado para substituir o carregamento bruto de imagens. Alterne valores para retornar bitmaps versus ícones conforme necessário.

 **Útil usando a instrução**

```csharp
using GelUtilities = Microsoft.Internal.VisualStudio.PlatformUI.Utilities;
```

 **Obter o serviço de imagem**

```csharp
// This or your preferred way of querying for Visual Studio services
IVsImageService2 imageService = (IVsImageService2)Package.GetGlobalService(typeof(SVsImageService));

```

 **Solicitar a imagem**

::: moniker range="vs-2017"

```csharp
ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiHelper.DeviceDpiX;
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

::: moniker range=">=vs-2019"

```csharp
Control control = // get the control where the image will be displayed

ImageAttributes attributes = new ImageAttributes
{
    StructSize    = Marshal.SizeOf(typeof(ImageAttributes)),
    // IT_Bitmap for Bitmap, IT_Icon for Icon, IT_ImageList for ImageList
    ImageType     = (uint)_UIImageType.IT_Bitmap,
    Format        = (uint)_UIDataFormat.DF_WinForms,
    LogicalWidth  = 16,
    LogicalHeight = 16,
    Dpi           = (int)DpiAwareness.GetWindowDpi(control.Handle);
    // Desired RGBA color, if you don't use this, don't set IAF_Background below
    Background    = 0xFFFFFFFF,
    Flags         = unchecked((uint)_ImageAttributesFlags.IAF_RequiredFlags | _ImageAttributesFlags.IAF_Background),
};

// Replace this KnownMoniker with your desired ImageMoniker
IVsUIObject uIObj = imageService.GetImage(KnownMonikers.Blank, attributes);

Bitmap bitmap = (Bitmap)GelUtilities.GetObjectData(uiObj); // Use this if you need a bitmap
// Icon icon = (Icon)GelUtilities.GetObjectData(uiObj);    // Use this if you need an icon
```

::: moniker-end

## <a name="how-do-i-use-image-monikers-in-a-new-tool-window"></a>Como fazer usar monikers de imagem em uma nova janela de ferramenta?
 O modelo de projeto do pacote VSIX foi atualizado para o Visual Studio 2015. Para criar uma nova janela de ferramenta, clique com o botão direito do mouse no projeto VSIX e selecione **Adicionar**  >  **novo item** (**Ctrl** + **Shift** + **a**). No nó extensibilidade para a linguagem do projeto, selecione **janela de ferramenta personalizada**, dê um nome à janela de ferramentas e pressione o botão **Adicionar** .

 Esses são os principais locais para usar monikers em uma janela de ferramentas. Siga as instruções para cada um:

1. A guia da janela de ferramentas quando as guias ficam pequenas o suficiente (também é usado no seletor de janela **Ctrl** + **Tab** ).

    Adicione essa linha ao construtor para a classe que deriva do tipo **ToolWindowPane** :

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   this.BitmapImageMoniker = KnownMonikers.Blank;
   ```

2. O comando para abrir a janela de ferramentas.

    No arquivo *. vsct* do pacote, edite o botão de comando da janela de ferramentas:

   ```xml
   <Button guid="guidPackageCmdSet" id="CommandId" priority="0x0100" type="Button">
     <Parent guid="guidSHLMainMenu" id="IDG_VS_WNDO_OTRWNDWS1"/>
     <!-- Replace this KnownMoniker with your desired ImageMoniker -->
     <Icon guid="ImageCatalogGuid" id="Blank" />
     <!-- Add this -->
     <CommandFlag>IconIsMoniker</CommandFlag>
     <Strings>
       <ButtonText>MyToolWindow</ButtonText>
     </Strings>
   </Button>
   ```

   **Como fazer usar monikers de imagem em uma janela de ferramentas existente?**

   A atualização de uma janela de ferramentas existente para usar monikers de imagem é semelhante às etapas para criar uma nova janela de ferramenta.

   Esses são os principais locais para usar monikers em uma janela de ferramentas. Siga as instruções para cada um:

3. A guia da janela de ferramentas quando as guias ficam pequenas o suficiente (também é usado no seletor de janela **Ctrl** + **Tab** ).

   1. Remova essas linhas (se existirem) no construtor para a classe que deriva do tipo **ToolWindowPane** :

       ```csharp
       this.BitmapResourceID = <Value>;
       this.BitmapIndex = <Value>;
       ```

   2. Consulte a etapa #1 da "Como fazer usar moniker de imagem em uma nova janela de ferramenta?" seção acima.

4. O comando para abrir a janela de ferramentas.

   - Consulte a etapa #2 da "Como fazer usar moniker de imagem em uma nova janela de ferramenta?" seção acima.

## <a name="how-do-i-use-image-monikers-in-a-vsct-file"></a>Como fazer usar monikers de imagem em um arquivo. vsct?
 Atualize seu arquivo *. vsct* conforme indicado pelas linhas comentadas abaixo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <!--  Include the definitions for images included in the VS image catalog -->
  <Include href="KnownImageIds.vsct"/>
  <Commands package="guidMyPackage">
    <Buttons>
      <Button guid="guidMyCommandSet" id="cmdidMyCommand" priority="0x0000" type="Button">
        <!-- Add an Icon element, changing the attributes to match the image moniker you want to use.
             In this case, we're using the Guid for the VS image catalog.
             Change the id attribute to be the ID of the desired image moniker. -->
        <Icon guid="ImageCatalogGuid" id="OpenFolder" />
        <CommandFlag>DynamicVisibility</CommandFlag>
        <CommandFlag>DefaultInvisible</CommandFlag>
        <CommandFlag>DefaultDisabled</CommandFlag>
        <CommandFlag>CommandWellOnly</CommandFlag>
        <CommandFlag>IconAndText</CommandFlag>
        <!-- Add the IconIsMoniker CommandFlag -->
        <CommandFlag>IconIsMoniker</CommandFlag>
        <Strings>
          <ButtonText>Quick Fixes...</ButtonText>
          <CommandName>Show Quick Fixes</CommandName>
          <CanonicalName>ShowQuickFixes</CanonicalName>
          <LocCanonicalName>ShowQuickFixes</LocCanonicalName>
        </Strings>
      </Button>
    </Buttons>
  </Commands>
  <!-- It is recommended that you remove <Bitmap> elements that are no longer used in the vsct file -->
  <Symbols>
    <GuidSymbol name="guidMyPackage"    value="{1491e936-6ffe-474e-8371-30e5920d8fdd}" />
    <GuidSymbol name="guidMyCommandSet" value="{10347de4-69a9-47f4-a950-d3301f6d2bc7}">
      <IDSymbol name="cmdidMyCommand" value="0x9437" />
    </GuidSymbol>
  </Symbols>
</CommandTable>
```

 **E se meu arquivo. vsct também precisar ser lido por versões mais antigas do Visual Studio?**

 As versões mais antigas do Visual Studio não reconhecem o sinalizador de comando **IconIsMoniker** . Você pode usar imagens do serviço de imagem em versões do Visual Studio que dão suporte a ela, mas continuar usando imagens de estilo antigo em versões mais antigas do Visual Studio. Para fazer isso, deixe o arquivo *. vsct* inalterado (e, portanto, compatível com versões anteriores do Visual Studio) e crie um arquivo CSV (valores separados por vírgula) que mapeia de pares GUID/ID definidos no elemento do arquivo *. vsct* para os \<Bitmaps> pares GUID/ID do moniker da imagem.

 O formato do arquivo CSV de mapeamento é:

```
Icon guid, Icon id, Moniker guid, Moniker id
b714fcf7-855e-4e4c-802a-1fd87144ccad,1,fda30684-682d-421c-8be4-650a2967058e,100
b714fcf7-855e-4e4c-802a-1fd87144ccad,2,fda30684-682d-421c-8be4-650a2967058e,200
```

 O arquivo CSV é implantado com o pacote e seu local é especificado pela propriedade **IconMappingFilename** do atributo de pacote **ProvideMenuResource** :

```csharp
[ProvideMenuResource("MyPackage.ctmenu", 1, IconMappingFilename="IconMappings.csv")]
```

 O **IconMappingFilename** é um caminho relativo com raiz implícita em $PackageFolder $ (como no exemplo acima) ou um caminho absoluto com raiz explícita em um diretório definido por uma variável de ambiente, como *@ "% USERPROFILE% \dir1\dir2\MyMappingFile.csv"*.

## <a name="how-do-i-port-a-project-system"></a>Como fazer portar um sistema de projeto?
 **Como fornecer ImageMonikers para um projeto**

1. Implemente **VSHPROPID_SupportsIconMonikers** no **IVsHierarchy**do projeto e retorne true.

2. Implemente qualquer **VSHPROPID_IconMonikerImageList** (se o projeto original usado **VSHPROPID_IconImgList**) ou **VSHPROPID_IconMonikerGuid**, **VSHPROPID_IconMonikerId**, **VSHPROPID_OpenFolderIconMonikerGuid**, VSHPROPID_OpenFolderIconMonikerId (se o projeto original usado **VSHPROPID_IconHandle** e **VSHPROPID_OpenFolderIconHandle**). **VSHPROPID_OpenFolderIconMonikerId**

3. Altere a implementação do VSHPROPIDs original para ícones para criar versões "herdadas" dos ícones se os pontos de extensão os solicitarem. O **IVsImageService2** fornece a funcionalidade necessária para obter esses ícones

   **Requisitos extras para tipos de projeto VB/C#**

   Só implemente **VSHPROPID_SupportsIconMonikers** se você detectar que o seu projeto é o **tipo mais externo**. Caso contrário, o tipo real mais externo pode não dar suporte a monikers de imagem na realidade, e seu tipo base pode efetivamente "Ocultar" imagens personalizadas.

   **Como fazer usar monikers de imagem no CPS?**

   A configuração de imagens personalizadas no CPS (sistema de projeto comum) pode ser feita manualmente ou por meio de um modelo de item que acompanha o SDK de extensibilidade do sistema do projeto.

   **Usando o SDK de extensibilidade do sistema do projeto**

   Siga as instruções em [fornecer ícones personalizados para tipo de projeto/tipo de item](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/scenario/provide_custom_icons_for_the_project_or_item_type.md) para personalizar suas imagens do CPS. Mais informações sobre o CPS podem ser encontradas em [documentação de extensibilidade do sistema de projetos do Visual Studio](https://github.com/Microsoft/VSProjectSystem)

   **Usar ImageMonikers manualmente**

4. Implemente e exporte a interface **IProjectTreeModifier** em seu sistema de projeto.

5. Determine qual **KnownMoniker** ou moniker de imagem personalizada você deseja usar.

6. No método **ApplyModifications** , faça o seguinte em algum lugar no método antes de retornar a nova árvore, semelhante ao exemplo abaixo:

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   tree = tree.SetIcon(KnownMonikers.Blank.ToProjectSystemType());
   ```

7. Se você estiver criando uma nova árvore, poderá definir as imagens personalizadas passando os monikers desejados para o método NewTree, semelhante ao exemplo abaixo:

   ```csharp
   // Replace this KnownMoniker with your desired ImageMoniker
   ProjectImageMoniker icon         = KnownMonikers.FolderClosed.ToProjectSystemType();
   ProjectImageMoniker expandedIcon = KnownMonikers.FolderOpened.ToProjectSystemType();

   return this.ProjectTreeFactory.Value.NewTree(/*caption*/<value>,
                                                /*filePath*/<value>,
                                                /*browseObjectProperties*/<value>,
                                                icon,
                                                expandedIcon);
   ```

## <a name="how-do-i-convert-from-a-real-image-strip-to-a-moniker-based-image-strip"></a>Como fazer converter de uma faixa de imagem real em uma faixa de imagens baseada em moniker?
 **Preciso dar suporte a HIMAGELISTs**

 Se houver uma faixa de imagens já existente para o seu código que você deseja atualizar para usar o serviço de imagem, mas estiver restrito por APIs que exigem a passagem de listas de imagens, você ainda poderá obter os benefícios do serviço de imagem. Para criar uma faixa de imagens baseada em moniker, siga as etapas abaixo para criar um manifesto a partir de monikers existentes.

1. Execute a ferramenta **ManifestFromResources** , passando-a para a faixa de imagens. Isso irá gerar um manifesto para a faixa.

   - Recomendado: forneça um nome não padrão para o manifesto se adequar ao seu uso.

2. Se você estiver usando apenas **KnownMonikers**, faça o seguinte:

   - Substitua a \<Images> seção do manifesto por \<Images/> .

   - Remova todas as IDs de subimagem (qualquer coisa com \<imagestrip name> _ # #).

   - Recomendado: renomeie o símbolo AssetsGuid e o símbolo da faixa de imagem para se adequar ao seu uso.

   - Substitua o GUID de cada **ContainedImage**por $ (ImageCatalogGuid), substitua cada ID de **ContainedImage**por $ ( \<moniker> ) e adicione o atributo external = "true" a cada **ContainedImage**

       - \<moniker>deve ser substituído pelo **KnownMoniker** que corresponde à imagem, mas com o "KnownMonikers". removido do nome.

   - Adicione <importar manifesto = "$ (ManifestFolder) \\<caminho dir de instalação relativa a * \> \Microsoft.VisualStudio.ImageCatalog.imagemanifest"/ \*> na parte superior da \<Symbols> seção.

       - O caminho relativo é determinado pelo local de implantação definido na criação da instalação para o manifesto.

3. Execute a ferramenta **ManifestToCode** para gerar wrappers para que o código existente tenha um moniker que possa ser usado para consultar o serviço de imagem para a faixa de imagens.

   - Recomendado: forneça nomes não padrão para os wrappers e namespaces para atender ao seu uso.

4. Faça todas as adições, criação de instalação/implantação e outras alterações de código para trabalhar com o serviço de imagem e os novos arquivos.

   Manifesto de exemplo incluindo imagens internas e externas para ver como deve ser:

```xml
<?xml version="1.0"?>
<ImageManifest
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns="http://schemas.microsoft.com/VisualStudio/ImageManifestSchema/2014">

  <Symbols>
    <!-- This needs to be the relative path from your manifest to the ImageCatalog's manifest
         where $(ManifestFolder) is the deployed location of this manifest. -->
    <Import Manifest="$(ManifestFolder)\<RelPath>\Microsoft.VisualStudio.ImageCatalog.imagemanifest" />

    <String Name="Resources" Value="/My.Assembly.Name;Component/Resources/ImageStrip" />
    <Guid Name="ImageGuid" Value="{fb41b7ef-6587-480c-aa27-5b559d42cfc9}" />
    <Guid Name="ImageStripGuid" Value="{9c84a570-d9a7-4052-a340-188fb276f973}" />
    <ID Name="MyImage_0" Value="100" />
    <ID Name="MyImage_1" Value="101" />
    <ID Name="InternalList" Value="1001" />
    <ID Name="ExternalList" Value="1002" />
  </Symbols>

  <Images>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_0)">
      <Source Uri="$(Resources)/MyImage_0.png">
        <Size Value="16" />
      </Source>
    </Image>
    <Image Guid="$(ImageGuid)" ID="$(MyImage_1)">
      <Source Uri="$(Resources)/MyImage_1.png">
        <Size Value="16" />
      </Source>
    </Image>
  </Images>

  <ImageLists>
    <ImageList Guid="$(ImageStripGuid)" ID="$(InternalList)">
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_0)" />
      <ContainedImage Guid="$(ImageGuid)" ID="$(MyImage_1)" />
    </ImageList>
    <ImageList Guid="$(ImageStripGuid)" ID="$(ExternalList)">
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusError)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusWarning)" External="true" />
      <ContainedImage Guid="$(ImageCatalogGuid)" ID="$(StatusInformation)" External="true" />
    </ImageList>
  </ImageLists>

</ImageManifest>
```

 **Não preciso dar suporte a HIMAGELISTs**

1. Determine o conjunto de **KnownMonikers** que correspondem às imagens em sua faixa de imagens ou crie seus próprios monikers para as imagens em sua faixa de imagens.

2. Atualize qualquer mapeamento que você usou para obter a imagem no índice necessário na faixa de imagens para usar os moniker em vez disso.

3. Atualize seu código para usar o serviço de imagem para solicitar monikers por meio do mapeamento atualizado. (Isso pode significar a atualização para **CrispImages** para código gerenciado, ou solicitar HBITMAPs ou HICONs do serviço de imagem e passá-los para código nativo.)

## <a name="testing-your-images"></a>Testando suas imagens
 Você pode usar a ferramenta Image Library Viewer para testar seus manifestos de imagem para garantir que tudo esteja criado corretamente. Você pode encontrar a ferramenta no [SDK do Visual Studio 2015](visual-studio-sdk.md). A documentação para essa ferramenta e outras podem ser encontradas [aqui](/visualstudio/extensibility/internals/vssdk-utilities?view=vs-2015).

## <a name="additional-resources"></a>Recursos adicionais

### <a name="samples"></a>Exemplos
 Vários dos exemplos do Visual Studio no GitHub foram atualizados para mostrar como usar o serviço de imagem como parte de vários pontos de extensibilidade do Visual Studio.

 Verifique [http://github.com/Microsoft/VSSDK-Extensibility-Samples](https://github.com/Microsoft/VSSDK-Extensibility-Samples) os exemplos mais recentes.

### <a name="tooling"></a>Ferramentas
 Um conjunto de ferramentas de suporte para o serviço de imagem foi criado para auxiliar na criação/atualização da interface do usuário que funciona com o serviço de imagem. Para obter mais informações sobre cada ferramenta, consulte a documentação que acompanha as ferramentas. As ferramentas são incluídas como parte do [SDK do Visual Studio 2015](visual-studio-sdk.md).

 **ManifestFromResources**

 A ferramenta de Manifest from Resources usa uma lista de recursos de imagem (PNG ou XAML) e gera um arquivo de manifesto de imagem para usar essas imagens com o serviço de imagem.

 **ManifestToCode**

 A ferramenta de Manifest to Code usa um arquivo de manifesto de imagem e gera um arquivo de wrapper para referenciar os valores de manifesto nos arquivos de código (C++, C# ou VB) ou *. vsct* .

 **ImageLibraryViewer**

 A ferramenta Visualizador de biblioteca de imagens pode carregar manifestos de imagem e permite que o usuário manipule-os da mesma maneira que o Visual Studio faria para ter certeza de que o manifesto foi criado corretamente. O usuário pode alterar o plano de fundo, tamanhos, configuração de DPI, Alto Contraste e outras configurações. Ele também exibe informações de carregamento para localizar erros nos manifestos e exibe informações de origem para cada imagem no manifesto.

## <a name="faq"></a>Perguntas frequentes

- Há alguma dependência que você deve incluir ao carregar \<Reference Include="Microsoft.VisualStudio.*.Interop.14.0.DesignTime" /> ?

  - Defina EmbedInteropTypes = "true" em todas as DLLs de interoperabilidade.

- Como fazer implantar um manifesto de imagem com minha extensão?

  - Adicione o arquivo *. imagemanifest* ao seu projeto.

  - Defina "incluir no VSIX" como true.

- Estou atualizando meu sistema de projeto do CPS. O que aconteceu com **ImageName** e **StockIconService**?

  - Elas foram removidas quando o CPS foi atualizado para usar monikers. Você não precisa mais chamar o **StockIconService**, basta passar o **KnownMoniker** desejado para o método ou a propriedade usando o método de extensão **ToProjectSystemType ()** nos utilitários do CPS. Você pode encontrar um mapeamento de **ImageName** para **KnownMonikers** abaixo:

    |**ImageName**|**KnownMoniker**|
    |-|-|
    |ImageName. OfflineWebApp|KnownImageIds. Web|
    |ImageName. WebReferencesFolder|KnownImageIds. Web|
    |ImageName. OpenReferenceFolder|KnownImageIds.FolderOpened|
    |ImageName. ReferenceFolder|KnownImageIds. Reference|
    |ImageName. Reference|KnownImageIds. Reference|
    |ImageName. SdlWebReference|KnownImageIds.WebReferenceFolder|
    |ImageName. DiscoWebReference|KnownImageIds.DynamicDiscoveryDocument|
    |ImageName. Folder|KnownImageIds.FolderClosed|
    |ImageName. OpenFolder|KnownImageIds.FolderOpened|
    |ImageName. ExcludedFolder|KnownImageIds.HiddenFolderClosed|
    |ImageName. OpenExcludedFolder|KnownImageIds.HiddenFolderOpened|
    |ImageName. excludefile|KnownImageIds. Hiddenfile|
    |ImageName. Dependentfile|KnownImageIds. Gerarfile|
    |ImageName. Missingfile|KnownImageIds.DocumentWarning|
    |ImageName. WindowsForm|KnownImageIds.WindowsForm|
    |ImageName. WindowsUserControl|KnownImageIds. UserControl|
    |ImageName. WindowsComponent|KnownImageIds. Componentfile|
    |Esquema de ImageName.Xml|Esquema de KnownImageIds.XML|
    |Arquivo de ImageName.Xml|Arquivo de KnownImageIds.XML|
    |ImageName. WebForms|KnownImageIds. Web|
    |ImageName. WebService|KnownImageIds. WebService|
    |ImageName. webusercontrol|KnownImageIds. webusercontrol|
    |ImageName. WebCustomUserControl|KnownImageIds.WebCustomControl|
    |ImageName. AspPage|KnownImageIds.ASPFile|
    |ImageName. GlobalApplicationClass|KnownImageIds. SettingsFile|
    |ImageName. WebConfig|KnownImageIds.ConfigurationFile|
    |ImageName.HtmlPage|KnownImageIds.HTMLFile|
    |ImageName. StyleSheet|KnownImageIds. StyleSheet|
    |ImageName. scriptfile|KnownImageIds.JSscript|
    |ImageName. textfile|KnownImageIds.Document|
    |ImageName. SettingsFile|KnownImageIds. Settings|
    |ImageName. Resources|KnownImageIds.DocumentGroup|
    |ImageName. bitmap|KnownImageIds. Image|
    |ImageName. Icon|KnownImageIds. IconFile|
    |ImageName. Image|KnownImageIds. Image|
    |ImageName. ImageMap|KnownImageIds. ImageMapfile|
    |ImageName. XWorld|KnownImageIds.XWorldFile|
    |ImageName. Audio|KnownImageIds. Sound|
    |ImageName. Video|KnownImageIds. Media|
    |ImageName.Cab|KnownImageIds.CABprojeto|
    |ImageName. jar|KnownImageIds. JARFile|
    |ImageName. DataEnvironment|KnownImageIds. DataTable|
    |ImageName. previewfile|KnownImageIds. Report|
    |ImageName. DanglingReference|KnownImageIds.ReferenceWarning|
    |ImageName. xsltfile|KnownImageIds. XSLTransform|
    |ImageName. cursor|KnownImageIds. cursorFile|
    |ImageName. AppDesignerFolder|KnownImageIds. Property|
    |ImageName. Data|KnownImageIds. Database|
    |ImageName. Application|KnownImageIds. Application|
    |ImageName. DataSet|KnownImageIds. Database|
    |ImageName. pfx|KnownImageIds. Certificate|
    |ImageName. SNK|KnownImageIds. Rule|
    |ImageName. VisualBasicProject|KnownImageIds.VBProjectNode|
    |ImageName. CSharpProject|KnownImageIds.CSProjectNode|
    |ImageName. Empty|KnownImageIds. Blank|
    |ImageName. MissingFolder|KnownImageIds.FolderOffline|
    |ImageName. SharedImportReference|KnownImageIds.SharedProject|
    |ImageName. SharedProjectCs|KnownImageIds.CSSharedProject|
    |ImageName. SharedProjectVc|KnownImageIds.CPPSharedProject|
    |ImageName. SharedProjectJs|KnownImageIds.JSSharedProject|
    |ImageName. CSharpCodeFile|KnownImageIds.CSFileNode|
    |ImageName. VisualBasicCodeFile|KnownImageIds.VBFileNode|

  - Estou atualizando meu provedor de lista de conclusão. Que **KnownMonikers** corresponde aos valores antigos de **StandardGlyphGroup** e **StandardGlyph** ?

    |Nome|Nome|Nome|
    |-|-|-|
    |GlyphGroupClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupConstant|GlyphItemPublic|ConstantPublic|
    |GlyphGroupConstant|GlyphItemInternal|ConstantInternal|
    |GlyphGroupConstant|GlyphItemFriend|ConstantInternal|
    |GlyphGroupConstant|GlyphItemProtected|ConstantProtected|
    |GlyphGroupConstant|GlyphItemPrivate|ConstantPrivate|
    |GlyphGroupConstant|GlyphItemShortcut|ConstantShortcut|
    |GlyphGroupDelegate|GlyphItemPublic|DelegatePublic|
    |GlyphGroupDelegate|GlyphItemInternal|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemFriend|DelegateInternal|
    |GlyphGroupDelegate|GlyphItemProtected|DelegateProtected|
    |GlyphGroupDelegate|GlyphItemPrivate|DelegatePrivate|
    |GlyphGroupDelegate|GlyphItemShortcut|DelegateShortcut|
    |GlyphGroupEnum|GlyphItemPublic|EnumerationPublic|
    |GlyphGroupEnum|GlyphItemInternal|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemFriend|EnumerationInternal|
    |GlyphGroupEnum|GlyphItemProtected|EnumerationProtected|
    |GlyphGroupEnum|GlyphItemPrivate|EnumerationPrivate|
    |GlyphGroupEnum|GlyphItemShortcut|EnumerationShortcut|
    |GlyphGroupEnumMember|GlyphItemPublic|EnumerationItemPublic|
    |GlyphGroupEnumMember|GlyphItemInternal|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemFriend|EnumerationItemInternal|
    |GlyphGroupEnumMember|GlyphItemProtected|EnumerationItemProtected|
    |GlyphGroupEnumMember|GlyphItemPrivate|EnumerationItemPrivate|
    |GlyphGroupEnumMember|GlyphItemShortcut|EnumerationItemShortcut|
    |GlyphGroupEvent|GlyphItemPublic|EventPublic|
    |GlyphGroupEvent|GlyphItemInternal|EventInternal|
    |GlyphGroupEvent|GlyphItemFriend|EventInternal|
    |GlyphGroupEvent|GlyphItemProtected|EventProtected|
    |GlyphGroupEvent|GlyphItemPrivate|EventPrivate|
    |GlyphGroupEvent|GlyphItemShortcut|EventShortcut|
    |GlyphGroupException|GlyphItemPublic|ExceptionPublic|
    |GlyphGroupException|GlyphItemInternal|ExceptionInternal|
    |GlyphGroupException|GlyphItemFriend|ExceptionInternal|
    |GlyphGroupException|GlyphItemProtected|ExceptionProtected|
    |GlyphGroupException|GlyphItemPrivate|ExceptionPrivate|
    |GlyphGroupException|GlyphItemShortcut|ExceptionShortcut|
    |GlyphGroupField|GlyphItemPublic|FieldPublic|
    |GlyphGroupField|GlyphItemInternal|FieldInternal|
    |GlyphGroupField|GlyphItemFriend|FieldInternal|
    |GlyphGroupField|GlyphItemProtected|FieldProtected|
    |GlyphGroupField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupMacro|GlyphItemPublic|MacroPublic|
    |GlyphGroupMacro|GlyphItemInternal|MacroInternal|
    |GlyphGroupMacro|GlyphItemFriend|MacroInternal|
    |GlyphGroupMacro|GlyphItemProtected|MacroProtected|
    |GlyphGroupMacro|GlyphItemPrivate|MacroPrivate|
    |GlyphGroupMacro|GlyphItemShortcut|MacroShortcut|
    |GlyphGroupMap|GlyphItemPublic|MapPublic|
    |GlyphGroupMap|GlyphItemInternal|MapInternal|
    |GlyphGroupMap|GlyphItemFriend|MapInternal|
    |GlyphGroupMap|GlyphItemProtected|MapProtected|
    |GlyphGroupMap|GlyphItemPrivate|MapPrivate|
    |GlyphGroupMap|GlyphItemShortcut|MapShortcut|
    |GlyphGroupMapItem|GlyphItemPublic|MapItemPublic|
    |GlyphGroupMapItem|GlyphItemInternal|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemFriend|MapItemInternal|
    |GlyphGroupMapItem|GlyphItemProtected|MapItemProtected|
    |GlyphGroupMapItem|GlyphItemPrivate|MapItemPrivate|
    |GlyphGroupMapItem|GlyphItemShortcut|MapItemShortcut|
    |GlyphGroupMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupOverload|GlyphItemPublic|MethodPublic|
    |GlyphGroupOverload|GlyphItemInternal|MethodInternal|
    |GlyphGroupOverload|GlyphItemFriend|MethodInternal|
    |GlyphGroupOverload|GlyphItemProtected|MethodProtected|
    |GlyphGroupOverload|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupOverload|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupModule|GlyphItemPublic|ModulePublic|
    |GlyphGroupModule|GlyphItemInternal|ModuleInternal|
    |GlyphGroupModule|GlyphItemFriend|ModuleInternal|
    |GlyphGroupModule|GlyphItemProtected|ModuleProtected|
    |GlyphGroupModule|GlyphItemPrivate|ModulePrivate|
    |GlyphGroupModule|GlyphItemShortcut|ModuleShortcut|
    |GlyphGroupNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupOperator|GlyphItemPublic|OperatorPublic|
    |GlyphGroupOperator|GlyphItemInternal|OperatorInternal|
    |GlyphGroupOperator|GlyphItemFriend|OperatorInternal|
    |GlyphGroupOperator|GlyphItemProtected|OperatorProtected|
    |GlyphGroupOperator|GlyphItemPrivate|OperatorPrivate|
    |GlyphGroupOperator|GlyphItemShortcut|OperatorShortcut|
    |GlyphGroupProperty|GlyphItemPublic|PropertyPublic|
    |GlyphGroupProperty|GlyphItemInternal|PropertyInternal|
    |GlyphGroupProperty|GlyphItemFriend|PropertyInternal|
    |GlyphGroupProperty|GlyphItemProtected|PropertyProtected|
    |GlyphGroupProperty|GlyphItemPrivate|PropertyPrivate|
    |GlyphGroupProperty|GlyphItemShortcut|PropertyShortcut|
    |GlyphGroupStruct|GlyphItemPublic|StructurePublic|
    |GlyphGroupStruct|GlyphItemInternal|StructureInternal|
    |GlyphGroupStruct|GlyphItemFriend|StructureInternal|
    |GlyphGroupStruct|GlyphItemProtected|StructureProtected|
    |GlyphGroupStruct|GlyphItemPrivate|StructurePrivate|
    |GlyphGroupStruct|GlyphItemShortcut|StructureShortcut|
    |GlyphGroupTemplate|GlyphItemPublic|TemplatePublic|
    |GlyphGroupTemplate|GlyphItemInternal|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemFriend|TemplateInternal|
    |GlyphGroupTemplate|GlyphItemProtected|TemplateProtected|
    |GlyphGroupTemplate|GlyphItemPrivate|TemplatePrivate|
    |GlyphGroupTemplate|GlyphItemShortcut|TemplateShortcut|
    |GlyphGroupTypedef|GlyphItemPublic|TypeDefinitionPublic|
    |GlyphGroupTypedef|GlyphItemInternal|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemFriend|TypeDefinitionInternal|
    |GlyphGroupTypedef|GlyphItemProtected|TypeDefinitionProtected|
    |GlyphGroupTypedef|GlyphItemPrivate|TypeDefinitionPrivate|
    |GlyphGroupTypedef|GlyphItemShortcut|TypeDefinitionShortcut|
    |GlyphGroupType|GlyphItemPublic|TypePublic|
    |GlyphGroupType|GlyphItemInternal|TypeInternal|
    |GlyphGroupType|GlyphItemFriend|TypeInternal|
    |GlyphGroupType|GlyphItemProtected|TypeProtected|
    |GlyphGroupType|GlyphItemPrivate|TypePrivate|
    |GlyphGroupType|GlyphItemShortcut|TypeShortcut|
    |GlyphGroupUnion|GlyphItemPublic|UnionPublic|
    |GlyphGroupUnion|GlyphItemInternal|UnionInternal|
    |GlyphGroupUnion|GlyphItemFriend|UnionInternal|
    |GlyphGroupUnion|GlyphItemProtected|UnionProtected|
    |GlyphGroupUnion|GlyphItemPrivate|UnionPrivate|
    |GlyphGroupUnion|GlyphItemShortcut|UnionShortcut|
    |GlyphGroupVariable|GlyphItemPublic|FieldPublic|
    |GlyphGroupVariable|GlyphItemInternal|FieldInternal|
    |GlyphGroupVariable|GlyphItemFriend|FieldInternal|
    |GlyphGroupVariable|GlyphItemProtected|FieldProtected|
    |GlyphGroupVariable|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupVariable|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupValueType|GlyphItemPublic|ValueTypePublic|
    |GlyphGroupValueType|GlyphItemInternal|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemFriend|ValueTypeInternal|
    |GlyphGroupValueType|GlyphItemProtected|ValueTypeProtected|
    |GlyphGroupValueType|GlyphItemPrivate|ValueTypePrivate|
    |GlyphGroupValueType|GlyphItemShortcut|ValueTypeShortcut|
    |GlyphGroupIntrinsic|GlyphItemPublic|Objectpúblico|
    |GlyphGroupIntrinsic|GlyphItemInternal|Objectinterna|
    |GlyphGroupIntrinsic|GlyphItemFriend|Objectinterna|
    |GlyphGroupIntrinsic|GlyphItemProtected|Objectprotect|
    |GlyphGroupIntrinsic|GlyphItemPrivate|Objectprivate|
    |GlyphGroupIntrinsic|GlyphItemShortcut|Objectshortcut|
    |GlyphGroupJSharpMethod|GlyphItemPublic|MethodPublic|
    |GlyphGroupJSharpMethod|GlyphItemInternal|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemFriend|MethodInternal|
    |GlyphGroupJSharpMethod|GlyphItemProtected|MethodProtected|
    |GlyphGroupJSharpMethod|GlyphItemPrivate|MethodPrivate|
    |GlyphGroupJSharpMethod|GlyphItemShortcut|MethodShortcut|
    |GlyphGroupJSharpField|GlyphItemPublic|FieldPublic|
    |GlyphGroupJSharpField|GlyphItemInternal|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemFriend|FieldInternal|
    |GlyphGroupJSharpField|GlyphItemProtected|FieldProtected|
    |GlyphGroupJSharpField|GlyphItemPrivate|FieldPrivate|
    |GlyphGroupJSharpField|GlyphItemShortcut|FieldShortcut|
    |GlyphGroupJSharpClass|GlyphItemPublic|ClassPublic|
    |GlyphGroupJSharpClass|GlyphItemInternal|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemFriend|ClassInternal|
    |GlyphGroupJSharpClass|GlyphItemProtected|ClassProtected|
    |GlyphGroupJSharpClass|GlyphItemPrivate|ClassPrivate|
    |GlyphGroupJSharpClass|GlyphItemShortcut|ClassShortcut|
    |GlyphGroupJSharpNamespace|GlyphItemPublic|NamespacePublic|
    |GlyphGroupJSharpNamespace|GlyphItemInternal|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemFriend|NamespaceInternal|
    |GlyphGroupJSharpNamespace|GlyphItemProtected|NamespaceProtected|
    |GlyphGroupJSharpNamespace|GlyphItemPrivate|NamespacePrivate|
    |GlyphGroupJSharpNamespace|GlyphItemShortcut|NamespaceShortcut|
    |GlyphGroupJSharpInterface|GlyphItemPublic|InterfacePublic|
    |GlyphGroupJSharpInterface|GlyphItemInternal|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemFriend|InterfaceInternal|
    |GlyphGroupJSharpInterface|GlyphItemProtected|InterfaceProtected|
    |GlyphGroupJSharpInterface|GlyphItemPrivate|InterfacePrivate|
    |GlyphGroupJSharpInterface|GlyphItemShortcut|InterfaceShortcut|
    |GlyphGroupError||StatusError|
    |GlyphBscFile||Classe de|
    |GlyphAssembly||Referência|
    |GlyphLibrary||Biblioteca|
    |GlyphVBProject||VBProjectNode|
    |GlyphCoolProject||CSProjectNode|
    |GlyphCppProject||CPPProjectNode|
    |GlyphDialogId||caixa de diálogo|
    |GlyphOpenFolder||FolderOpened|
    |GlyphClosedFolder||FolderClosed|
    |GlyphArrow||GoToNext|
    |GlyphCSharpFile||CSFileNode|
    |GlyphCSharpExpansion||Snippet|
    |GlyphKeyword||IntellisenseKeyword|
    |GlyphInformation||StatusInformation|
    |GlyphReference||ClassMethodReference|
    |GlyphRecursion||Recursão|
    |GlyphXmlItem||Marca|
    |GlyphJSharpProject||DocumentCollection|
    |GlyphJSharpDocument||Document|
    |GlyphForwardType||GoToNext|
    |GlyphCallersGraph||Chamar|
    |GlyphCallGraph||CallFrom|
    |GlyphWarning||StatusWarning|
    |GlyphMaybeReference||QuestionMark|
    |GlyphMaybeCaller||Chamar|
    |GlyphMaybeCall||CallFrom|
    |GlyphExtensionMethod||ExtensionMethod|
    |GlyphExtensionMethodInternal||ExtensionMethod|
    |GlyphExtensionMethodFriend||ExtensionMethod|
    |GlyphExtensionMethodProtected||ExtensionMethod|
    |GlyphExtensionMethodPrivate||ExtensionMethod|
    |GlyphExtensionMethodShortcut||ExtensionMethod|
    |GlyphXmlAttribute||XmlAttribute|
    |GlyphXmlChild||XmlElement|
    |GlyphXmlDescendant||Xmldescendant|
    |GlyphXmlNamespace||XmlNamespace|
    |GlyphXmlAttributeQuestion||XmlAttributeLowConfidence|
    |GlyphXmlAttributeCheck||XmlAttributeHighConfidence|
    |GlyphXmlChildQuestion||XmlElementLowConfidence|
    |GlyphXmlChildCheck||XmlElementHighConfidence|
    |GlyphXmlDescendantQuestion||XmlDescendantLowConfidence|
    |GlyphXmlDescendantCheck||XmlDescendantHighConfidence|
    |GlyphCompletionWarning||IntellisenseWarning|
