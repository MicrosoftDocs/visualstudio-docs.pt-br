---
title: Endereçando DPI Issues2 | Microsoft Docs
description: Saiba mais sobre os problemas envolvidos na programação para telas de alta resolução, como escalar verticalmente o conteúdo, os problemas de layout e o uso de APIs de dimensionamento de DPI.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9cf7b4fe19cdefe11b77de1418b16454089f45c6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097507"
---
# <a name="address-dpi-issues"></a>Problemas de endereço de DPI
Um número cada vez maior de dispositivos é enviado com telas de "alta resolução". Essas telas normalmente têm mais de 200 pixels por polegada (ppi). Trabalhar com um aplicativo nesses computadores exigirá que o conteúdo seja dimensionado para atender às necessidades de exibição do conteúdo em uma distância de exibição normal do dispositivo. A partir de 2014, o destino principal para monitores de alta densidade é dispositivos de computação móvel (tablets, laptops Clamshell e telefones).

O Windows 8.1 e superior contém vários recursos para permitir que esses computadores trabalhem com monitores e ambientes em que a máquina está anexada a monitores de alta densidade e densidade padrão ao mesmo tempo.

- O Windows pode permitir que você dimensione o conteúdo para o dispositivo usando a configuração "criar texto e outros itens maiores ou menores" (disponível desde o Windows XP).

- Windows 8.1 e superior dimensionarão automaticamente o conteúdo para a maioria dos aplicativos serem consistentes quando movidos entre telas de diferentes densidades de pixel. Quando a exibição primária é de alta densidade (200% de dimensionamento) e a exibição secundária é a densidade padrão (100%), o Windows dimensiona automaticamente o conteúdo da janela do aplicativo para baixo na exibição secundária (1 pixel exibido para cada 4 pixels processados pelo aplicativo).

- O Windows usará como padrão o dimensionamento correto para a densidade de pixel e a distância de exibição da exibição (Windows 7 e superior, OEM-configurável).

- O Windows pode dimensionar automaticamente o conteúdo em até 250% em novos dispositivos que excedem 280 PPI (a partir de Windows 8.1 S14).

  O Windows tem uma maneira de lidar com a expansão da interface do usuário para aproveitar as maiores contagens de pixels. Um aplicativo opta por este sistema, declarando-se "reconhecimento de DPI do sistema". Os aplicativos que não fazem isso são escalados verticalmente pelo sistema. Isso pode resultar em uma experiência de usuário "difusa", em que todo o aplicativo é uniformemente alongado em pixels. Por exemplo:

  ![Difusão de problemas de DPI](../extensibility/media/dpi-issues-fuzzy.png "Difusão de problemas de DPI")

  O Visual Studio opta por ser compatível com o dimensionamento de DPI e, portanto, não é "virtualizado".

  O Windows (e o Visual Studio) aproveitam várias tecnologias de interface do usuário, que têm maneiras diferentes de lidar com fatores de dimensionamento definidos pelo sistema. Por exemplo:

- O WPF mede controles de forma independente de dispositivo (unidades, não pixels). A interface do usuário do WPF é dimensionada automaticamente para o DPI atual.

- Todos os tamanhos de texto, independentemente da estrutura da interface do usuário, são expressos em pontos e, portanto, são tratados pelo sistema como independentes de DPI. O texto no Win32, WinForms e WPF já são dimensionados corretamente quando desenhado para o dispositivo de vídeo.

- As caixas de diálogo do Win32/WinForms e o Windows têm meios para habilitar o layout que é redimensionado com texto (por exemplo, por meio de painéis de layout de grade, de fluxo e de tabela). Isso permite evitar locais de pixel embutidos em código que não são dimensionados quando os tamanhos das fontes são aumentados.

- Os ícones fornecidos pelo sistema ou recursos com base nas métricas do sistema (por exemplo, SM_CXICON e SM_CXSMICON) já estão escalados verticalmente.

## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>Interface do usuário com base no Win32 (GDI, GDI+) e WinForms mais antigas
Embora o WPF já tenha alto reconhecimento de DPI, grande parte do nosso código baseado em Win32/GDI não foi escrito originalmente com reconhecimento de DPI em mente. O Windows forneceu APIs de dimensionamento de DPI. Correções para problemas do Win32 devem usá-las consistentemente em todo o produto. O Visual Studio forneceu uma biblioteca de classes auxiliar para evitar a duplicação da funcionalidade e garantir a consistência em todo o produto.

## <a name="high-resolution-images"></a>Imagens de alta resolução
Esta seção destina-se principalmente a desenvolvedores que estendem Visual Studio 2013. Para o Visual Studio 2015, use o serviço de imagem que é incorporado ao Visual Studio. Você também pode descobrir que precisa dar suporte/destino a várias versões do Visual Studio e, portanto, usar o serviço de imagem no 2015 não é uma opção, pois ela não existe em versões anteriores. Esta seção também é para você.

## <a name="scaling-up-images-that-are-too-small"></a>Dimensionamento de imagens muito pequenas
Imagens muito pequenas podem ser escaladas verticalmente e renderizadas em GDI e WPF usando alguns métodos comuns. As classes auxiliares de DPI gerenciado estão disponíveis para integradores internos e externos do Visual Studio para abordar ícones de dimensionamento, bitmaps, imagestrips e imagelists. Os auxiliares C/C + + nativos baseados em Win32 estão disponíveis para dimensionar HICON, HBITMAP, HIMAGELIST e VsUI:: GdiplusImage. O dimensionamento de um bitmap normalmente requer apenas uma alteração de uma linha depois de incluir uma referência à biblioteca auxiliar. Por exemplo:

```cpp
(Unmanaged) VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);
```

```csharp
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);
```

Dimensionar um ImageList depende se ImageList está completa no tempo de carregamento ou é anexado em tempo de execução. Se for concluído no tempo de carregamento, chame `LogicalToDeviceUnits()` com ImageList como você faria com um bitmap. Quando o código precisar carregar um bitmap individual antes de compor ImageList, certifique-se de dimensionar o tamanho da imagem de ImageList:

```csharp
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);
```

No código nativo, as dimensões podem ser dimensionadas ao criar ImageList da seguinte maneira:

```cpp
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);
```

As funções na biblioteca permitem especificar o algoritmo de redimensionamento. Ao dimensionar imagens a serem colocadas em imagelists, especifique a cor do plano de fundo usada para transparência ou use o dimensionamento de NearestNeighbor (que causará distorções em 125% e 150%).

Consulte a <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> documentação no msdn.

A tabela a seguir mostra exemplos de como as imagens devem ser dimensionadas em fatores de dimensionamento de DPI correspondentes. As imagens descritas em laranja indicam nossa prática recomendada a partir de Visual Studio 2013 (100%-200% de dimensionamento de DPI):

![Escala de problemas de DPI](../extensibility/media/dpi-issues-scaling.png "Escala de problemas de DPI")

## <a name="layout-issues"></a>Problemas de layout
Problemas de layout comuns podem ser evitados principalmente por manter os pontos na interface do usuário dimensionados e relativos entre si, em vez de usar locais absolutos (especificamente, em unidades de pixel). Por exemplo:

- As posições de layout/texto precisam ser ajustadas para considerar as imagens escaladas.

- As colunas nas grades precisam ter larguras ajustadas para o texto escalonado.

- Tamanhos embutidos em código ou espaço entre elementos também precisarão ser escalados verticalmente. Os tamanhos baseados apenas em dimensões de texto normalmente são bem, pois as fontes são dimensionadas automaticamente.

  As funções auxiliares estão disponíveis na <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> classe para permitir o dimensionamento nos eixos X e Y:

- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (as funções permitem o dimensionamento no eixo X/Y)

- espaço int = DpiHelper. LogicalToDeviceUnitsX (10);

- altura int = VsUI::D piHelper:: LogicalToDeviceUnitsY (5);

  Há sobrecargas LogicalToDeviceUnits para permitir o dimensionamento de objetos como Rect, Point e size.

## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>Usando a biblioteca/classe DPIHelper para dimensionar imagens e layout
A biblioteca do Visual Studio DPI Helper está disponível em formulários nativos e gerenciados e pode ser usada fora do shell do Visual Studio por outros aplicativos.

Para usar a biblioteca, vá para os [exemplos de extensibilidade do Visual Studio VSSDK](https://github.com/Microsoft/VSSDK-Extensibility-Samples) e clone o exemplo de High-DPI_Images_Icons.

Em arquivos de origem, inclua *VsUIDpiHelper. h* e chame as funções estáticas da `VsUI::DpiHelper` classe:

```cpp
#include "VsUIDpiHelper.h"

int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);

```

> [!NOTE]
> Não use as funções auxiliares em variáveis estáticas em nível de módulo ou de classe. A biblioteca também usa estáticos para sincronização de threads e você pode ter problemas de inicialização de pedidos. Converta os estáticos em variáveis de membro não estáticos ou coloque-os em uma função (para que eles sejam construídos no primeiro acesso).

Para acessar as funções auxiliares de DPI do código gerenciado que será executado dentro do ambiente do Visual Studio:

- O projeto de consumo deve fazer referência à versão mais recente do Shell MPF. Por exemplo:

    ```csharp
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />
    ```

- Verifique se o projeto tem referências a **System. Windows. Forms**, **PresentationCore** e **PresentationUI**.

- No código, use o namespace **Microsoft. VisualStudio. PlatformUI** e chame funções estáticas da classe DpiHelper. Para tipos com suporte (pontos, tamanhos, retângulos e assim por diante), há funções de extensão fornecidas que retornam novos objetos dimensionados. Por exemplo:

    ```csharp
    using Microsoft.VisualStudio.PlatformUI;
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();
    DpiHelper.LogicalToDeviceUnits(ref bitmap);

    ```

## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>Lidando com a difusão da imagem do WPF na interface do usuário com zoom
No WPF, os bitmaps são redimensionados automaticamente pelo WPF para o nível de zoom atual de DPI usando um algoritmo Bicúbico de alta qualidade (padrão), que funciona bem para imagens ou capturas de tela grandes, mas é inadequado para ícones de item de menu porque ele introduz a fuzzização percebida.

Recomendações:

- Para imagens de logotipo e faixas de arte, o <xref:System.Windows.Media.BitmapScalingMode> modo de redimensionamento padrão pode ser usado.

- Para itens de menu e imagens iconografia, o <xref:System.Windows.Media.BitmapScalingMode> deve ser usado quando não faz com que outros artefatos de distorção eliminem a fuzzização (às 200% e 300%).

- Para níveis de zoom grandes que não são múltiplos de 100% (por exemplo, 250% ou 350%), dimensionar imagens iconografia com Bicúbico resulta em uma interface do usuário difusa e desbotada. Um resultado melhor é obtido primeiro dimensionando a imagem com NearestNeighbor para o maior múltiplo de 100% (por exemplo, 200% ou 300%) e dimensionando com o Bicúbico a partir daí. Veja o caso especial: predimensionar imagens do WPF para níveis de DPI grandes para obter mais informações.

  A classe DpiHelper no namespace Microsoft. VisualStudio. PlatformUI fornece um membro <xref:System.Windows.Media.BitmapScalingMode> que pode ser usado para associação. Ele permitirá que o Shell do Visual Studio controle o modo de dimensionamento de bitmap no produto uniformemente, dependendo do fator de dimensionamento de DPI.

  Para usá-lo em XAML, adicione:

```xaml
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"

<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />

```

O Shell do Visual Studio já define essa propriedade em janelas de nível superior e caixas de diálogo. A interface do usuário baseada no WPF em execução no Visual Studio já a herdará. Se a configuração não for propagada para suas partes específicas da interface do usuário, ela poderá ser definida no elemento raiz da interface do usuário XAML/WPF. Os locais em que isso acontece incluem pop-ups, em elementos com pais do Win32 e janelas de designer que ficam fora do processo, como Blend.

Algumas interfaces do usuário podem ser dimensionadas independentemente do nível de zoom do DPI definido pelo sistema, como o editor de texto do Visual Studio e designers baseados no WPF (área de trabalho do WPF e Windows Store). Nesses casos, DpiHelper. BitmapScalingMode não deve ser usado. Para corrigir esse problema no editor, a equipe do IDE criou uma propriedade personalizada chamada RenderOptions. BitmapScalingMode. Defina esse valor de propriedade como HighQuality ou NearestNeighbor dependendo do nível de zoom combinado do sistema e da sua interface do usuário.

## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>Caso especial: predimensionar imagens do WPF para grandes níveis de DPI
Para níveis de zoom muito grandes que não são múltiplos de 100% (por exemplo, 250%, 350% e assim por diante), o dimensionamento de imagens iconografia com Bicúbico resulta em uma interface de usuário desbotada e sem interrupções. A impressão dessas imagens junto com o texto nítido é quase parecida com a de uma ilusão ótica. As imagens parecem ficar mais próximas do olho e fora do foco em relação ao texto. O resultado de dimensionamento nesse tamanho ampliado pode ser melhorado ao dimensionar primeiro a imagem com NearestNeighbor para o maior múltiplo de 100% (por exemplo, 200% ou 300%) e dimensionamento com Bicúbico para o resto (um 50%) adicional.

Veja a seguir um exemplo das diferenças nos resultados, em que a primeira imagem é dimensionada com o algoritmo de dimensionamento duplo melhorado 100%->200%->250% e a segunda apenas com Bicúbico 100%->250%.

![Exemplo de dimensionamento duplo de problemas de DPI](../extensibility/media/dpi-issues-double-scaling-example.png "Exemplo de dimensionamento duplo de problemas de DPI")

Para permitir que a interface do usuário use esse dimensionamento duplo, a marcação XAML para exibir cada elemento de imagem precisará ser modificada. Os exemplos a seguir demonstram como usar o dimensionamento duplo no WPF no Visual Studio usando a biblioteca DpiHelper e o Shell. 12/14.

Etapa 1: predimensionar a imagem para 200%, 300% e assim por diante usando NearestNeighbor.

Predimensionar a imagem usando um conversor aplicado em uma associação ou com uma extensão de marcação XAML. Por exemplo:

```xaml
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />

<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />

<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />

```

Se a imagem também precisa ser contornada (a maioria, se não todas, deveria), a marcação pode usar um conversor diferente que primeiro faz a imagem e, em seguida, o dimensionamento antecipado. A marcação pode usar <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> ou <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter> , dependendo da saída de conversão desejada.

```xaml
<vsui:DpiPrescaleThemedImageSourceConverter x:Key="DpiPrescaleThemedImageSourceConverter" />

<Image Width="16" Height="16">
  <Image.Source>
    <MultiBinding Converter="{StaticResource DpiPrescaleThemedImageSourceConverter}">
      <Binding Path="Icon" />
      <Binding Path="(vsui:ImageThemingUtilities.ImageBackgroundColor)"
               RelativeSource="{RelativeSource Self}" />
      <Binding Source="{x:Static vsui:Boxes.BooleanTrue}" />
    </MultiBinding>
  </Image.Source>
</Image>
```

Etapa 2: Verifique se o tamanho final está correto para o DPI atual.

Como o WPF dimensionará a interface do usuário para o DPI atual usando a propriedade BitmapScalingMode definida no UIElement, um controle de imagem usando uma imagem em escala como sua fonte terá uma aparência de duas ou três vezes maior do que deveria. A seguir estão algumas maneiras de combater esse efeito:

- Se você souber a dimensão da imagem original em 100%, poderá especificar o tamanho exato do controle de imagem. Esses tamanhos refletirão o tamanho da interface do usuário antes da aplicação do dimensionamento.

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />
    ```

- Se o tamanho da imagem original não for conhecido, um LayoutTransform poderá ser usado para reduzir verticalmente o objeto de imagem final. Por exemplo:

    ```xaml
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >
        <Image.LayoutTransform>
            <ScaleTransform
                ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"
                ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />
        </Image.LayoutTransform>
    </Image>
    ```

## <a name="enabling-hdpi-support-to-the-weboc"></a>Habilitando o suporte do HDPI ao WebOC
Por padrão, os controles WebOC (como o controle WebBrowser no WPF ou a interface IWebBrowser2) não habilitam a detecção e o suporte do HDPI. O resultado será um controle incorporado com conteúdo de exibição muito pequeno em uma exibição de alta resolução. O exemplo a seguir descreve como habilitar o suporte a alto DPI em uma instância de WebOC da Web específica.

Implemente a interface IDocHostUIHandler (consulte o artigo do MSDN na [IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85)):

```idl
[ComImport, InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("BD3F23C0-D43E-11CF-893B-00AA00BDCE1A")]
public interface IDocHostUIHandler
{
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowContextMenu(
        [In, MarshalAs(UnmanagedType.U4)] int dwID,
        [In] POINT pt,
        [In, MarshalAs(UnmanagedType.Interface)] object pcmdtReserved,
        [In, MarshalAs(UnmanagedType.IDispatch)] object pdispReserved);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetHostInfo([In, Out] DOCHOSTUIINFO info);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ShowUI(
        [In, MarshalAs(UnmanagedType.I4)] int dwID,
        [In, MarshalAs(UnmanagedType.Interface)] object activeObject,
        [In, MarshalAs(UnmanagedType.Interface)] object commandTarget,
        [In, MarshalAs(UnmanagedType.Interface)] object frame,
        [In, MarshalAs(UnmanagedType.Interface)] object doc);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int HideUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int UpdateUI();
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int EnableModeless([In, MarshalAs(UnmanagedType.Bool)] bool fEnable);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnDocWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int OnFrameWindowActivate([In, MarshalAs(UnmanagedType.Bool)] bool fActivate);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int ResizeBorder(
        [In] COMRECT rect,
        [In, MarshalAs(UnmanagedType.Interface)] object doc,
        bool fFrameWindow);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateAccelerator(
        [In] ref MSG msg,
        [In] ref Guid group,
        [In, MarshalAs(UnmanagedType.I4)] int nCmdID);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetOptionKeyPath(
        [Out, MarshalAs(UnmanagedType.LPArray)] string[] pbstrKey,
        [In, MarshalAs(UnmanagedType.U4)] int dw);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetDropTarget(
        [In, MarshalAs(UnmanagedType.Interface)] IOleDropTarget pDropTarget,
        [MarshalAs(UnmanagedType.Interface)] out IOleDropTarget ppDropTarget);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int GetExternal([MarshalAs(UnmanagedType.IDispatch)] out object ppDispatch);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int TranslateUrl(
        [In, MarshalAs(UnmanagedType.U4)] int dwTranslate,
        [In, MarshalAs(UnmanagedType.LPWStr)] string strURLIn,
        [MarshalAs(UnmanagedType.LPWStr)] out string pstrURLOut);
    [return: MarshalAs(UnmanagedType.I4)]
    [PreserveSig]
    int FilterDataObject(
        IDataObject pDO,
        out IDataObject ppDORet);
    }
```

Opcionalmente, implemente a interface ICustomDoc (consulte o artigo do MSDN no [ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85)):

```idl
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]
public interface ICustomDoc
{
    void SetUIHandler(IDocHostUIHandler pUIHandler);
}
```

Associe a classe que implementa IDocHostUIHandler ao documento do WebOC. Se você implementou a interface ICustomDoc acima, assim que a propriedade de documento do WebOC for válida, converta-a em um ICustomDoc e chame o método SetUIHandler, passando a classe que implementa IDocHostUIHandler.

```csharp
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;
customDoc.SetUIHandler(this);

```

Se você não implementou a interface ICustomDoc, assim que a propriedade de documento do WebOC for válida, você precisará convertê-la em um IOleObject e chamar o `SetClientSite` método, passando a classe que implementa IDocHostUIHandler. Defina o sinalizador DOCHOSTUIFLAG_DPI_AWARE no DOCHOSTUIINFO passado para a `GetHostInfo` chamada do método:

```csharp
public int GetHostInfo(DOCHOSTUIINFO info)
{
    // This is what the default site provides.
    info.dwFlags = (DOCHOSTUIFLAG)0x5a74012;
    // Add the DPI flag to the defaults
    info.dwFlags |=.DOCHOSTUIFLAG.DOCHOSTUIFLAG_DPI_AWARE;
    return S_OK;
}
```

Deve ser tudo o que você precisa para obter o controle WebOC para dar suporte ao HPDI.

## <a name="tips"></a>Dicas

1. Se a propriedade Document no controle WebOC for alterada, talvez seja necessário reassociar o documento à classe IDocHostUIHandler.

2. Se o mostrado acima não funcionar, há um problema conhecido com o WebOC que não está selecionando a alteração para o sinalizador de DPI. A maneira mais confiável de corrigir isso é alternar o zoom óptico do WebOC, o que significa que duas chamadas com dois valores diferentes para a porcentagem de zoom. Além disso, se essa solução alternativa for necessária, talvez seja necessário executá-la em cada chamada de navegação.

    ```csharp
    // browser2 is a SHDocVw.IWebBrowser2 in this case
    // EX: Call the Exec twice with DPI%-1 and then DPI% as the zoomPercent values
    IOleCommandTarget cmdTarget = browser2.Document as IOleCommandTarget;
    if (cmdTarget != null)
    {
        object commandInput = zoomPercent;
        cmdTarget.Exec(IntPtr.Zero,
                       OLECMDID_OPTICAL_ZOOM,
                       OLECMDEXECOPT_DONTPROMPTUSER,
                       ref commandInput,
                       ref commandOutput);
    }
    ```
