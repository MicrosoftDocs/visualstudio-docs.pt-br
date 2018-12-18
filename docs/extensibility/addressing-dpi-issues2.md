---
title: Endereçamento DPI Problemas2 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 359184aa-f5b6-4b6c-99fe-104655b3a494
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2c4ca03c932b86ad6f9907020b037abb1308a6f7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49918526"
---
# <a name="address-dpi-issues"></a>Questões DPI
Um número crescente de dispositivos é fornecidos com telas de "alta resolução". Normalmente, essas telas têm mais de 200 pixels por polegada (ppi). Trabalhar com um aplicativo nesses computadores necessitará de conteúdo a ser escalado verticalmente para atender às necessidades de exibir o conteúdo em uma distância de exibição normal para o dispositivo. A partir de 2014, o principal alvo para monitores de alta densidade é móvel (tablets, laptops clamshell e telefones) de dispositivos de computação.  
  
 Windows 8.1 e posterior contém vários recursos para habilitar esses computadores trabalhar com exibições e ambientes em que a máquina está conectada a ambos alta densidade e densidade standard exibe ao mesmo tempo.  
  
- Windows podem permitir que você a ajustar o conteúdo para o dispositivo usando o "Tornar texto e outros itens maiores ou menores" configuração (disponível desde o Windows XP).  
  
- Windows 8.1 e posterior dimensionará automaticamente conteúdo para a maioria dos aplicativos ser consistente quando movidos entre exibições de diferentes densidades de pixels. Quando o vídeo principal é de alta densidade (200% scaling) e a exibição secundária é a densidade padrão (100%), o Windows dimensionará automaticamente o conteúdo da janela de aplicativo para baixo na exibição do secundária (1 pixel exibido para cada 4 pixels renderizados pelo aplicativo).  
  
- Windows padrão serão o direito de colocação em escala para a densidade de pixels e exibindo a distância para a exibição (Windows 7 e superior, configuráveis pelo OEM).  
  
- Windows podem dimensionar automaticamente conteúdo para cima 250% em novos dispositivos que excedem 280 ppi (a partir de S14 do Windows 8.1).  
  
  Windows tem uma maneira de lidar com o aumento da interface do usuário para tirar proveito das contagens de aumento de pixel. Um aplicativo aceita o esse sistema declarando si mesmo "sistema de reconhecimento de DPI". Aplicativos que não fazem isso são aumentados pelo sistema. Isso pode resultar em uma experiência de usuário "difusa" onde todo o aplicativo é alongado de pixel uniformemente. Por exemplo:  
  
  ![Problemas de DPI difuso](../extensibility/media/dpi-issues-fuzzy.png "DPI emite difusa")  
  
  Visual Studio aceita o que está sendo o reconhecimento de dimensionamento de DPI e, portanto, não está "virtualizado."  
  
  Windows (e o Visual Studio) aproveitam várias tecnologias de interface do usuário, que têm diferentes maneiras de lidar com definido pelo sistema de fatores de dimensionamento. Por exemplo:  
  
- WPF mede os controles de forma independente de dispositivo (unidades, não em pixels). UI WPF pode ser dimensionado automaticamente para o DPI atual.  
  
- Todos os tamanhos de texto, independentemente da estrutura de interface do usuário são expressos em pontos e, portanto, são tratados pelo sistema como independente de DPI. Texto no WPF, WinForms e Win32 já dimensionar corretamente quando desenhada para o dispositivo de vídeo.  
  
- Janelas e caixas de diálogo do Win32/WinForms tem meios para habilitar o layout é redimensionado com texto (por exemplo, por meio de grade, fluxo e painéis de layout de tabela). Eles permitem evitar locais de pixel embutido em código que não são dimensionados quando os tamanhos de fonte são aumentados.  
  
- Ícones fornecidos pelo sistema ou recursos com base nas métricas do sistema (por exemplo, SM_CXICON e SM_CXSMICON) já estão dimensionados para cima.  
  
## <a name="older-win32-gdi-gdi-and-winforms-based-ui"></a>Win32 mais antigos (GDI, GDI+) e a interface do usuário baseada no WinForms  
 Embora o WPF já estiver reconhecimento de DPI alto, grande parte do nosso código baseado em Win32/GDI não foi gravado originalmente com reconhecimento de DPI em mente. Windows fornece APIs de escala de DPI. Correções para problemas de Win32 devem usá-las consistente em todo o produto. Visual Studio forneceu um auxiliar de biblioteca de classes para evitar a duplicação de funcionalidade e garantindo a consistência em todo o produto.  
  
## <a name="high-resolution-images"></a>Imagens de alta resolução  
 Esta seção é principalmente para desenvolvedores, estendendo o Visual Studio 2013. Para Visual Studio 2015, use o serviço de imagem que está incorporado ao Visual Studio. Você também pode encontrar o que você precisa de suporte/destino muitas versões do Visual Studio e, portanto, usando o serviço de imagem no 2015 não é uma opção, pois não existe nas versões anteriores. Esta seção é também, em seguida, para você.  
  
## <a name="scaling-up-images-that-are-too-small"></a>Expansão de imagens que são muito pequenas  
 Imagens que são muito pequenas podem ser expandidas e renderizadas no GDI e WPF usando alguns métodos comuns. Classes de auxiliar DPI gerenciadas estão disponíveis para integradores de Visual Studio internos e externos ao endereço dimensionamento ícones, bitmaps, imagestrips e imagelists. Baseado em Win32 nativo C / C + + auxiliares estão disponíveis para a escala HICON, HBITMAP, HIMAGELIST e VsUI::GdiplusImage. O dimensionamento de um bitmap normalmente requer apenas uma alteração de uma linha depois de incluir uma referência à biblioteca do auxiliar. Por exemplo:  
  
```cpp  
(Unmanaged)  VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
```  
  
```csharp  
(WinForms) DpiHelper.LogicalToDeviceUnits(ref image);  
```  
  
 Dimensionar um imagelist depende de imagelist for concluída no tempo de carregamento, ou é acrescentado em tempo de execução. Se for concluída no tempo de carregamento, chame `LogicalToDeviceUnits()` com imagelist como você faria um bitmap. Quando o código precisa carregar um bitmap individual antes de compor imagelist, certifique-se de dimensionar o tamanho da imagem de imagelist:  
  
```csharp  
imagelist.ImageSize = DpiHelper.LogicalToDeviceUnits(imagelist.ImageSize);  
```  
  
 No código nativo, as dimensões podem ser dimensionadas durante a criação de imagelist da seguinte maneira:  
  
```cpp  
ImageList_Create(VsUI::DpiHelper::LogicalToDeviceUnitsX(16),VsUI::DpiHelper::LogicalToDeviceUnitsY(16), ILC_COLOR32|ILC_MASK, nCount, 1);  
```  
  
 Funções na biblioteca permitem especificar o algoritmo de redimensionamento. Quando as imagens de colocação em escala a ser colocado na imagelists, certifique-se de especificar a cor do plano de fundo que é usada para a transparência ou use NearestNeighbor dimensionamento (o que fará com que as distorções em 125% e 150%).  
  
 Consulte o <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> documentação no MSDN.  
  
 A tabela a seguir mostra exemplos de como as imagens devem ser dimensionadas em PPP correspondente fatores de dimensionamento. As imagens descritas em laranja denotam nossa prática recomendada a partir do Visual Studio 2013 (100 a 200% dimensionamento DPI):  
  
 ![Problemas DPI dimensionando](../extensibility/media/dpi-issues-scaling.png "questões de DPI dimensionamento")  
  
## <a name="layout-issues"></a>Problemas de layout  
 Problemas comuns de layout podem ser evitados, principalmente por manter os pontos na interface de usuário dimensionados e a relação em vez de usar locais absolutos (especificamente, em unidades de pixel). Por exemplo:  
  
- Posições de texto do layout necessário ajustar a conta para imagens expandidos.  
  
- Colunas em grades precisam ter larguras ajustadas para o texto expandidos.  
  
- Tamanhos de embutido em código ou o espaço entre os elementos também precisará ser escalado verticalmente. Tamanhos com base apenas nas dimensões de texto são costuma funcionar bem, porque as fontes são automaticamente escaladas verticalmente.  
  
  Funções de auxiliar estão disponíveis no <xref:Microsoft.VisualStudio.PlatformUI.DpiHelper> classe para permitir o dimensionamento no eixo X e Y:  
  
- LogicalToDeviceUnitsX/LogicalToDeviceUnitsY (funções permitem o dimensionamento em X / eixo Y)  
  
- espaço de int = DpiHelper.LogicalToDeviceUnitsX (10);  
  
- int altura = VsUI::DpiHelper::LogicalToDeviceUnitsY(5);  
  
  Há sobrecargas de LogicalToDeviceUnits para permitir o dimensionamento de objetos, como Rect, ponto e tamanho.  
  
## <a name="using-the-dpihelper-libraryclass-to-scale-images-and-layout"></a>Usando a biblioteca DPIHelper/classe para dimensionar imagens e o layout  
 A biblioteca do auxiliar de DPI do Visual Studio está disponível em formulários nativos e gerenciados e pode ser usada por outros aplicativos fora do shell do Visual Studio.  
  
 Para usar a biblioteca, vá para o [exemplos de extensibilidade de VSSDK do Visual Studio](https://github.com/Microsoft/VSSDK-Extensibility-Samples) e clonar o exemplo DPI_Images_Icons alta.  
  
 Nos arquivos de origem, inclua *VsUIDpiHelper.h* e chamar as funções estáticas de `VsUI::DpiHelper` classe:  
  
```cpp  
#include "VsUIDpiHelper.h"  
  
int cxScaled = VsUI::DpiHelper::LogicalToDeviceUnitsX(cx);  
VsUI::DpiHelper::LogicalToDeviceUnits(&hBitmap);  
  
```  
  
> [!NOTE]
>  Não use as funções auxiliares em nível de módulo ou classe variáveis estáticas. A biblioteca também usa estatísticas para sincronização de threads e você pode ter problemas de inicialização de ordem. Converta essas estatísticas para variáveis de membro não estáticos, ou encapsulá-los em uma função (de modo que eles obterem construídos no primeiro acesso).  
  
 Para acessar as funções do auxiliar DPI do código gerenciado que será executado dentro do ambiente do Visual Studio:  
  
-   O projeto consumidor deve fazer referência a versão mais recente do MPF de Shell. Por exemplo:  
  
    ```csharp  
    <Reference Include="Microsoft.VisualStudio.Shell.14.0.dll" />  
    ```  
  
-   Verifique se o projeto tem referências aos **Forms**, **PresentationCore**, e **PresentationUI**.  
  
-   No código, use o **Microsoft.VisualStudio.PlatformUI** namespace e chame funções estáticas da classe DpiHelper. Para tipos com suporte (pontos, tamanhos, retângulos e assim por diante), existem desde dimensionado de funções de extensão que retornam novos objetos. Por exemplo:  
  
    ```csharp  
    using Microsoft.VisualStudio.PlatformUI;  
    double x = DpiHelper.LogicalToDeviceUnitsX(posX);  
    Point ptScaled = ptOriginal.LogicalToDeviceUnits();  
    DpiHelper.LogicalToDeviceUnits(ref bitmap);  
  
    ```  
  
## <a name="dealing-with-wpf-image-fuzziness-in-zoomable-ui"></a>Lidando com grau de seleção de imagem WPF no cartaz da interface do usuário  
 No WPF, bitmaps são redimensionados automaticamente pelo WPF para o nível de zoom atual do DPI usando um algoritmo de bicúbica de alta qualidade (padrão), que funciona bem para imagens ou capturas de tela grandes, mas não é apropriado para os ícones de item de menu porque ela introduz o grau de seleção percebido .  
  
 Recomendações:  
  
- Para a arte de imagem e faixas de logotipo, o padrão <xref:System.Windows.Media.BitmapScalingMode> modo de redimensionamento pode ser usado.  
  
- Para itens de menu e imagens de iconografia, o <xref:System.Windows.Media.BitmapScalingMode> deve ser usado quando ele não faz com que outros artefatos de distorção eliminar o grau de seleção (no % 200 e 300%).  
  
- Para os níveis de zoom grande não múltiplos de 100% (por exemplo, 250% ou % 350), dimensionando imagens iconografia com bicúbica resulta em difusa e Desbotado da interface do usuário. Um resultado melhor é obtido ao dimensionar a imagem com NearestNeighbor para o múltiplo de maior de 100% (por exemplo, 200% ou 300%) primeiro e o dimensionamento com bicúbica a partir daí. Consulte o caso especial: prescaling imagens do WPF para grande DPI níveis para obter mais informações.  
  
  A classe DpiHelper no namespace Microsoft.VisualStudio.PlatformUI fornece um membro <xref:System.Windows.Media.BitmapScalingMode> que pode ser usado para associação. Isso permitirá que o shell do Visual Studio controlar o modo de dimensionamento em todo o produto uniformemente, dependendo do fator de escala de DPI de bitmap.  
  
  Para usá-lo em XAML, adicione:  
  
```xaml  
xmlns:vsui="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"  
  
<Setter Property="RenderOptions.BitmapScalingMode" Value="{x:Static vs:DpiHelper.BitmapScalingMode}" />  
  
```  
  
 Já o shell do Visual Studio define essa propriedade em caixas de diálogo e janelas de nível superior. Interface de usuário baseada no WPF em execução no Visual Studio já será herdá-la. Se a configuração não se propaga às suas partes específicas da interface do usuário, ele pode ser definido no elemento raiz da interface do usuário XAML/WPF. Os locais em que isso ocorre incluem pop-ups em elementos com os pais do Win32, e janelas de designer que são executados fora do processam, como o Blend.  
  
 Algumas interfaces do usuário podem ser dimensionados independentemente do nível de zoom DPI conjunto do sistema, como o editor de texto do Visual Studio e os designers com base em WPF (área de trabalho do WPF e Windows Store). Nesses casos, DpiHelper.BitmapScalingMode não deve ser usado. Para corrigir esse problema no editor, a equipe IDE criada uma propriedade personalizada denominada RenderOptions.BitmapScalingMode. Defina o valor da propriedade HighQuality ou NearestNeighbor dependendo do nível de zoom combinado do sistema e a interface do usuário.  
  
## <a name="special-case-prescaling-wpf-images-for-large-dpi-levels"></a>Caso especial: prescaling imagens do WPF para níveis DPI grandes  
 Para os níveis de zoom muito grandes que não são múltiplos de 100% (por exemplo, 250%, % 350 e assim por diante), dimensionando imagens de iconografia com resultados bicúbica na interface do usuário difusa e Desbotado. A impressão dessas imagens junto com textos quase é semelhante à de uma ilusão ótica. As imagens parecem ser mais próximo ao olho e fora de foco em relação ao texto. O resultado de colocação em escala nesse tamanho ampliada pode ser melhorado, dimensionar a imagem com NearestNeighbor para o múltiplo de maior de 100% (por exemplo, 200% ou 300%) primeiro e o dimensionamento com bicúbica ao restante (um adicional 50%).  
  
 A seguir está um exemplo das diferenças nos resultados, em que a primeira imagem é dimensionada com o algoritmo de dimensionamento dupla aprimorado 100% -> 200% -> 250%, e o segundo é apenas com bicúbica 100% -> 250%.  
  
 ![DPI emite o exemplo de dimensionamento duplo](../extensibility/media/dpi-issues-double-scaling-example.png "DPI emite duplo exemplo de dimensionamento")  
  
 Para habilitar a interface do usuário usar esse dimensionamento duplo, a marcação XAML para exibir cada elemento de imagem precisará ser modificado. Os exemplos a seguir demonstram como usar o dimensionamento dupla no WPF no Visual Studio usando a biblioteca de DpiHelper e Shell.12/14.  
  
 Etapa 1: Prescale a imagem para 200%, 300% e assim por diante usando NearestNeighbor.  
  
 Prescale a imagem usando qualquer um conversor de aplicado em uma associação ou com uma extensão de marcação XAML. Por exemplo:  
  
```xaml  
<vsui:DpiPrescaleImageSourceConverter x:Key="DpiPrescaleImageSourceConverter" />  
  
<Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
  
<Image Source="{vsui:DpiPrescaledImage Images/Help.png}" Width="16" Height="16" />  
  
```  
  
 Se a imagem também precisa ser o tema (a maioria, se não todos, deve), a marcação pode usar um conversor de diferente que primeiro faz o tema da imagem e, em seguida, o dimensionamento previamente. A marcação pode usar o <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageConverter> ou <xref:Microsoft.VisualStudio.PlatformUI.DpiPrescaleThemedImageSourceConverter>, dependendo da saída de conversão desejada.  
  
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
  
 Etapa 2: Verifique se que o tamanho final está correto para o DPI atual.  
  
 Porque o WPF dimensionará a interface do usuário para o DPI atual usando a propriedade de BitmapScalingMode definida no UIElement, deve ser um controle de imagem usando uma imagem prescaled como sua fonte aparecerá duas ou três vezes maior do que ele. A seguir estão algumas maneiras de combater esse efeito:  
  
-   Se você souber a dimensão da imagem original em 100%, você pode especificar o tamanho exato do controle de imagem. Esses tamanhos refletirá que o tamanho da interface do usuário antes do dimensionamento é aplicado.  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" Width="16" Height="16" />  
    ```  
  
-   Se o tamanho da imagem original não for conhecido, um LayoutTransform pode ser usado para reduzir verticalmente o objeto de imagem final. Por exemplo:  
  
    ```xaml  
    <Image Source="{Binding Path=SelectedImage, Converter={StaticResource DpiPrescaleImageSourceConverter}}" >  
        <Image.LayoutTransform>  
         <ScaleTransform  
             ScaleX="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}"  
             ScaleY="{x:Static vsui:DpiHelper.PreScaledImageLayoutTransformScale}" />  
        </Image.LayoutTransform>  
    </Image>  
    ```  
  
## <a name="enabling-hdpi-support-to-the-weboc"></a>Habilitando o suporte HDPI para o WebOC  
 Por padrão, os controles de WebOC (como o controle WebBrowser no WPF, ou a interface IWebBrowser2) não habilitam a detecção de HDPI e suporte. O resultado será um controle inserido com o conteúdo de exibição é muito pequeno em uma exibição de alta resolução. A seguir descreve como habilitar o suporte a DPI alto em uma instância de WebOC web específico.  
  
 Implementar a interface IDocHostUIHandler (consulte o artigo do MSDN sobre o [IDocHostUIHandler](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753260(v=vs.85)):  
  
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
  
 Opcionalmente, implemente a interface ICustomDoc (consulte o artigo do MSDN sobre o [ICustomDoc](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa753272(v=vs.85)):  
  
```idl  
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown),  
 Guid("3050F3F0-98B5-11CF-BB82-00AA00BDCE0B")]  
public interface ICustomDoc  
{  
    void SetUIHandler(IDocHostUIHandler pUIHandler);  
}   
```  
  
 Associe a classe que implementa IDocHostUIHandler com o documento do WebOC. Se você tiver implementado a interface ICustomDoc acima, assim que a propriedade de documento do WebOC for válida, convertê-lo para um ICustomDoc e chame o método SetUIHandler, passando a classe que implementa IDocHostUIHandler.  
  
```csharp  
// "this" references that class that owns the WebOC control and in this case also implements the IDocHostUIHandler interface  
ICustomDoc customDoc = (ICustomDoc)webBrowser.Document;  
customDoc.SetUIHandler(this);  
  
```  
  
 Se você não implementou a interface ICustomDoc, assim que a propriedade de documento do WebOC for válida, você precisará convertê-lo para uma IOleObject e chame o `SetClientSite` método, passando a classe que implementa IDocHostUIHandler. Definir o sinalizador DOCHOSTUIFLAG_DPI_AWARE no DOCHOSTUIINFO passado para o `GetHostInfo` chamada de método:  
  
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
  
 Isso deve ser tudo o que você precisa obter seu controle WebOC para dar suporte a HPDI.  
  
## <a name="tips"></a>Dicas  
  
1.  Se a propriedade de documento no controle WebOC for alterado, você precisa reassociar o documento com a classe IDocHostUIHandler.  
  
2.  Se as opções acima não funcionar, há um problema conhecido com o WebOC não escolher a mudança para o sinalizador DPI. A maneira mais confiável de corrigir isso é ativar/desativar o zoom ótico de WebOC, duas chamadas de significado com dois valores diferentes para o percentual de zoom. Além disso, se essa solução alternativa é necessária, pode ser necessário para executá-lo em cada chamada de navegar.  
  
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
