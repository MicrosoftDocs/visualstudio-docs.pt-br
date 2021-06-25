---
title: Suporte ao reconhecimento de Per-Monitor para extensores do Visual Studio
titleSuffix: ''
description: Saiba mais sobre o novo suporte de extensor para reconhecimento por monitor disponível no Visual Studio 2019.
ms.date: 04/10/2019
helpviewer_keywords:
- Visual Studio, PMA, per-monitor-awareness, extenders, Windows Forms
- Per-Monitor Awareness support for extenders
author: rub8n
ms.author: rurios
manager: anthc
monikerRange: vs-2019
ms.topic: reference
dev_langs:
- CSharp
- CPP
ms.openlocfilehash: 90ec038e8f27407ba08633bacbb5576bee2a7883
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902040"
---
# <a name="per-monitor-awareness-support-for-visual-studio-extenders"></a>Suporte ao reconhecimento de Per-Monitor para extensores do Visual Studio

As versões anteriores ao Visual Studio 2019 tinham seu contexto de reconhecimento de DPI definido como reconhecimento do sistema, em vez de reconhecimento de DPI por monitor (PMA). A execução no reconhecimento do sistema resultou em uma experiência visual degradada (por exemplo, fontes ou ícones borrados) sempre que o Visual Studio precisasse renderizar monitores com fatores de escala diferentes ou remotos em computadores com configurações de exibição diferentes (por exemplo, dimensionamento diferente do Windows).

O contexto de reconhecimento de DPI do Visual Studio 2019 é definido como PMA, quando o ambiente dá suporte a ele, permitindo que o Visual Studio seja renderizado de acordo com a configuração da exibição onde ele é hospedado, em vez de uma configuração de sistema única definida. Por fim, convertendo em uma interface do usuário sempre nítida para áreas de superfície que dão suporte ao modo PMA.

Consulte a documentação [sobre desenvolvimento de aplicativos para desktop de alto dpi no Windows](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) para obter mais informações sobre os termos e o cenário geral abordados neste documento.

## <a name="quickstart"></a>Guia de Início Rápido

- Verifique se o Visual Studio está em execução no modo de PMA (consulte **habilitando o PMA**)

- Validar se a extensão funciona corretamente em um conjunto de cenários comuns (consulte **testando suas extensões para problemas de PMA**)

- Se encontrar problemas, você poderá usar as estratégias/recomendações discutidas neste documento para diagnosticar e corrigir esses problemas. Você também precisará adicionar o novo pacote NuGet [Microsoft. VisualStudio. DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) ao seu projeto para acessar as APIs necessárias.

## <a name="enable-pma"></a>Habilitar PMA

Para habilitar o PMA no Visual Studio, os requisitos a seguir precisam ser atendidos:

- Atualização do Windows 10 de abril de 2018 (v1803, RS4) ou posterior
- .NET Framework 4,8 RTM ou superior
- Visual Studio 2019 com a opção ["otimizar renderização para telas com diferentes densidades de pixel"](../../ide/reference/general-environment-options-dialog-box.md) habilitada

Depois que esses requisitos forem atendidos, o Visual Studio habilitará automaticamente o modo PMA em todo o processo.

> [!NOTE]
> Windows Forms conteúdo no Visual Studio (por exemplo, navegador de propriedades) dá suporte a PMA somente quando você tem o Visual Studio 2019 versão 16,1 ou posterior.

## <a name="test-your-extensions-for-pma-issues"></a>Testar suas extensões para problemas de PMA

O Visual Studio dá suporte oficialmente às estruturas de interface do usuário do WPF, Windows Forms, Win32 e HTML/JS. Quando o Visual Studio é colocado no modo PMA, cada pilha da interface do usuário se comporta de forma diferente. Portanto, independentemente da estrutura da interface do usuário, é recomendável que uma aprovação de teste seja executada para garantir que toda a interface do usuário esteja em conformidade com o modo PMA.

É recomendável que você valide os seguintes cenários comuns:

- Alterar o fator de escala de um único ambiente de monitor enquanto o aplicativo está em execução.

  Esse cenário ajuda a testar se a interface do usuário está respondendo à alteração dinâmica de DPI do Windows.

- Encaixe/desencaixe de um laptop em que um monitor anexado está definido como primário e o monitor anexado tem um fator de escala diferente do laptop enquanto o aplicativo está em execução.

  Esse cenário ajuda a testar se a interface do usuário está respondendo à alteração de DPI de vídeo, bem como ao tratamento de monitores que são adicionados ou removidos dinamicamente.

- Ter vários monitores com fatores de escala diferentes e mover o aplicativo entre eles.

  Esse cenário ajuda a testar se a interface do usuário está respondendo à alteração de DPI de vídeo
    
- Comunicação remota em um computador quando as máquinas locais e remotas têm fatores de escala diferentes para o monitor primário.

  Esse cenário ajuda a testar se a interface do usuário está respondendo à alteração dinâmica de DPI do Windows.

Um bom teste preliminar para se sua interface do usuário pode ter problemas é se o código utiliza as classes *Microsoft. VisualStudio. Utilities. dpi. DpiHelper*, *Microsoft. VisualStudio. PlatformUI. DpiHelper* ou *VsUI:: CDpiHelper* . Essas classes antigas DpiHelper dão suporte apenas ao reconhecimento de DPI do sistema e nem sempre funcionarão corretamente quando o processo for PMA.

O uso típico desses DpiHelpers se parecerá com:

```cs
Point screenTopRight = logicalBounds.TopRight.LogicalToDeviceUnits();

POINT screenIntTopRight = new POINT
{
    x = (int)screenTopRIght.X,
    y = (int)screenTopRIght.Y
}

// Declared via P/Invoke
IntPtr monitor = MonitorFromPoint(screenIntTopRight, MONITOR_DEFAULTTONEARST);
```

No exemplo anterior, um retângulo que representa os limites lógicos de uma janela é convertido em unidades de dispositivo para que possa ser passado para o método nativo MonitorFromPoint que espera que as coordenadas do dispositivo retornem um ponteiro de monitor preciso.

### <a name="classes-of-issues"></a>Classes de problemas
Quando o modo PMA está habilitado para o Visual Studio, a interface do usuário pode replicar problemas de várias maneiras comuns. A maioria, se não todos, desses problemas pode ocorrer em qualquer uma das estruturas de interface do usuário com suporte do Visual Studio. Além disso, esses problemas também podem ocorrer quando uma parte da interface do usuário está sendo hospedada em cenários de dimensionamento de DPI de modo misto (consulte a [documentação](/windows/desktop/hidpi/high-dpi-desktop-application-development-on-windows) do Windows para saber mais). 

#### <a name="win32-window-creation"></a>Criação de janela do Win32
Ao criar o Windows com CreateWindow () ou CreateWindowEx (), um padrão comum é criar a janela em coordenadas (0, 0) (o canto superior/esquerdo da exibição primária) e, em seguida, movê-la para sua posição final. No entanto, isso pode fazer com que a janela dispare uma mensagem ou um evento de DPI alterado, o que pode disparar novamente outras mensagens de interface do usuário ou eventos e, eventualmente, levar a um comportamento ou renderização indesejado.

#### <a name="wpf-element-placement"></a>Posicionamento do elemento do WPF
Ao mover elementos do WPF usando o antigo Microsoft. VisualStudio. Utilities. dpi. DpiHelper, as coordenadas superior esquerda podem não ser calculadas corretamente sempre que os elementos estiverem em um DPI não primário.

#### <a name="serialization-of-ui-element-sizes-or-positions"></a>Serialização de tamanhos ou posições de elementos de interface do usuário
Quando o tamanho ou a posição da interface do usuário (se salvas como unidades do dispositivo) for restaurado em um contexto de DPI diferente daquele em que foi armazenado, ele será posicionado e dimensionado incorretamente. Isso acontece porque as unidades de dispositivo têm uma relação de DPI inerente.

#### <a name="incorrect-scaling"></a>Dimensionamento incorreto
Os elementos da interface do usuário criados no DPI primário serão dimensionados corretamente, no entanto, quando movidos para uma exibição com um DPI diferente, eles não são redimensionados e seu conteúdo é muito grande ou muito pequeno.

#### <a name="incorrect-bounding"></a>Limite incorreto
Da mesma forma que o problema de dimensionamento, os elementos da interface do usuário calculam seus limites corretamente em seu contexto de DPI primário, no entanto, quando movido para um DPI não primário, eles não calcularão os novos limites corretamente. Assim, a janela de conteúdo é muito pequena ou muito grande em comparação com a interface do usuário de hospedagem, o que resulta em espaço vazio ou recorte.

#### <a name="drag--drop"></a>Arrastar & soltar
Sempre que dentro de cenários de DPI de modo misto (por exemplo, diferentes elementos da interface do usuário Renderizando em modos de reconhecimento de DPI diferentes), as coordenadas de arrastar e soltar podem ser calculadas incorretamente, resultando na extremidade de liberação final incorreta.

#### <a name="out-of-process-ui"></a>Interface do usuário fora do processo
Algumas interfaces do usuário são criadas fora do processo e, se a criação do processo externo estiver em um modo de reconhecimento de DPI diferente do Visual Studio, isso poderá apresentar qualquer um dos problemas de renderização anteriores.

#### <a name="windows-forms-controls-images-or-layouts-rendered-incorrectly"></a>Windows Forms controles, imagens ou layouts renderizados incorretamente
Nem todos os Windows Forms conteúdo dão suporte ao modo PMA. Como resultado, você poderá ver o problema de renderização com layouts incorretos ou dimensionamento. Uma solução possível nesse caso é processar explicitamente o conteúdo de Windows Forms no DpiAwarenessContext de "reconhecimento do sistema" (consulte [forçar um controle em um DpiAwarenessContext específico](#force-a-control-into-a-specific-dpiawarenesscontext)).

#### <a name="windows-forms-controls-or-windows-not-displaying"></a>Controles de Windows Forms ou janelas não exibidas
Uma das principais causas desse problema é que os desenvolvedores tentam redirecionar um controle ou uma janela com um DpiAwarenessContext para uma janela com um DpiAwarenessContext diferente.

As imagens a seguir mostram as restrições do sistema operacional Windows **padrão** atuais em janelas pai:

![Uma captura de tela do comportamento correto de pai](media/PMA-parenting-behavior.PNG)

> [!Note]
> Você pode alterar esse comportamento definindo o comportamento de Hospedagem de thread (consulte [Dpi_Hosting_Behavior Enumeração](/windows/desktop/api/windef/ne-windef-dpi_hosting_behavior)).

Como resultado, se você definir a relação pai-filho entre os modos sem suporte, ele falhará e o controle ou a janela poderá não ser renderizado conforme o esperado.

### <a name="diagnose-issues"></a>Diagnosticar problemas

Há muitos fatores a serem considerados ao identificar problemas relacionados ao PMA: 

- A interface do usuário ou API espera valores lógicos ou de dispositivo?
    - Interface do usuário e APIs do WPF normalmente usam valores lógicos (mas nem sempre)
    - Interface do usuário e APIs do Win32 normalmente usam valores de dispositivo

- De onde os valores são provenientes?
    - Se receber valores de outra interface do usuário ou API, ele passará por um dispositivo ou valores lógicos.
    - Se receber valores de várias fontes, todos eles usarão/esperam os mesmos tipos de valores ou as conversões precisarão ser mistas e correspondidas?

- As constantes da interface do usuário estão em uso e em qual formulário eles estão?

- O thread está no contexto de DPI correto para os valores que ele está recebendo?

  As alterações para habilitar a hospedagem de DPI mista devem geralmente colocar caminhos de código no contexto certo, no entanto, o trabalho feito fora do loop de mensagem principal ou do fluxo de eventos pode ser executado no contexto de DPI errado.

- Os valores têm limites de contexto entre DPI?

  Arraste & drop é uma situação comum em que as coordenadas podem cruzar contextos de DPI. A janela tenta fazer a coisa certa, mas, em alguns casos, a interface do usuário do host pode precisar fazer o trabalho de conversão para garantir a correspondência dos limites de contexto.

### <a name="pma-nuget-package"></a>Pacote NuGet do PMA
As novas bibliotecas DpiAwarness podem ser encontradas no pacote NuGet [Microsoft. VisualStudio. DpiAwareness](https://www.nuget.org/packages/Microsoft.VisualStudio.DpiAwareness/) .

### <a name="recommended-tools"></a>Ferramentas recomendadas
As ferramentas a seguir podem ajudar a depurar problemas relacionados ao PMA em algumas das diferentes pilhas de interface do usuário com suporte do Visual Studio.

#### <a name="snoop"></a>Intercepta
O Snoop é uma ferramenta de depuração XAML que tem alguma funcionalidade extra que as ferramentas XAML internas do Visual Studio não têm. Além disso, a Espionage não precisa depurar ativamente o Visual Studio para poder exibir e ajustar sua interface do usuário do WPF. As duas maneiras principais de rastreamento podem ser úteis para diagnosticar problemas de PMA é para validar coordenadas de posicionamento lógico ou limites de tamanho, e para validar a interface do usuário tem o DPI correto.
 
#### <a name="visual-studio-xaml-tools"></a>Ferramentas XAML do Visual Studio
Como a espionagem, as ferramentas XAML no Visual Studio podem ajudar a diagnosticar problemas de PMA. Depois que um provável culpado for encontrado, você poderá definir pontos de interrupção e usar a janela de árvore visual ao vivo, bem como as janelas de depuração, para inspecionar os limites da interface do usuário e o DPI atual.

## <a name="strategies-for-fixing-pma-issues"></a>Estratégias para corrigir problemas de PMA

### <a name="replace-dpihelper-calls"></a>Substituir chamadas DpiHelper

Na maioria dos casos, corrigir problemas de interface do usuário no modo PMA se resume a substituir chamadas em código gerenciado para as classes antigas *Microsoft. VisualStudio. Utilities. dpi. DpiHelper* e *Microsoft. VisualStudio. PlatformUI. DpiHelper* , com chamadas para a nova classe auxiliar *Microsoft. VisualStudio. Utilities. DpiAwareness* . 

```cs
// Remove this kind of use:
Point deviceTopLeft = new Point(window.Left, window.Top).LogicalToDeviceUnits();

// Replace with this use:
Point deviceTopLeft = window.LogicalToDevicePoint(new Point(window.Left, window.Top));
```

Para código nativo, ele envolverá a substituição de chamadas para a classe *VsUI:: CDpiHelper* antiga com chamadas para a nova classe *VsUI:: CDpiAwareness* . 

```cpp
// Remove this kind of use:
int cx = VsUI::DpiHelper::LogicalToDeviceUnitsX(m_cxS);
int cy = VsUI::DpiHelper::LogicalToDeviceUnitsY(m_cyS);

// Replace with this use:
int cx = m_cxS;
int cy = m_cyS;
VsUI::CDpiAwareness::LogicalToDeviceUnitsX(m_hwnd, &cx);
VsUI::CDpiAwareness::LogicalToDeviceUnitsY(m_hwnd, &cy);
```

As novas classes DpiAwareness e CDpiAwareness oferecem os mesmos auxiliares de conversão de unidade que as classes DpiHelper, mas exigem um parâmetro de entrada adicional: o elemento de interface do usuário a ser usado como uma referência para a operação de conversão. É importante observar que os auxiliares de dimensionamento de imagem não existem nos novos auxiliares DpiAwareness/CDpiAwareness e, se necessário, o [ImageService](../image-service-and-catalog.md) deve ser usado em vez disso.

A classe DpiAwareness gerenciada oferece auxiliares para visuais do WPF, controles de Windows Forms e HWNDs Win32 e HMONITORs (ambos na forma de IntPtrs), enquanto a classe CDpiAwareness nativa oferece auxiliares HWND e HMONITOR.

### <a name="windows-forms-dialogs-windows-or-controls-displayed-in-the-wrong-dpiawarenesscontext"></a>Windows Forms diálogos, janelas ou controles exibidos no DpiAwarenessContext errado
Mesmo após um pai bem-sucedido de janelas com DpiAwarenessContexts diferentes (devido ao comportamento padrão do Windows), os usuários ainda poderão ver problemas de dimensionamento como janelas com diferentes DpiAwarenessContexts dimensionando de maneira diferente. Como resultado, os usuários podem ver problemas de texto de alinhamento/desfocado ou imagem na interface do usuário.

A solução é definir o escopo DpiAwarenessContext correto para todas as janelas e controles no aplicativo.

### <a name="top-level-mixed-mode-tlmm-dialogs"></a>Caixas de diálogo de modo misto de nível superior (TLMM)
Ao criar janelas de nível superior, como caixas de diálogo modais, é importante garantir que o thread está no estado correto antes da janela (e seu handle) ser criado. O thread pode ser colocado no Reconhecimento do sistema usando o auxiliar CDpiScope em nativo ou o auxiliar DpiAwareness.EnterDpiScope em gerenciado. (O TLMM geralmente deve ser usado em caixas de diálogo/janelas não WPF.)

### <a name="child-level-mixed-mode-clmm"></a>Modo misto de nível filho (CLMM)
Por padrão, as janelas filho recebem o contexto de reconhecimento de DPI do thread atual se criados sem um pai ou o contexto de reconhecimento de DPI do pai quando criados com um pai. Para criar um filho com um contexto de reconhecimento de DPI diferente de seu pai, o thread pode ser colocado no contexto de reconhecimento de DPI desejado. Em seguida, o filho pode ser criado sem um pai e manualmente reparentado na janela pai.

#### <a name="clmm-issues"></a>Problemas do CLMM
A maioria do trabalho de cálculo da interface do usuário que acontece como parte do loop de mensagens principal ou da cadeia de eventos já deve estar em execução no contexto de reconhecimento de DPI correto. No entanto, se os cálculos de coordenadas ou de tamanho são feitos fora desses fluxos de trabalho principais (como durante uma tarefa de tempo ocioso ou fora do thread de interface do usuário, o contexto de reconhecimento de DPI atual pode estar incorreto, levando a erros de erro de tamanho ou de extração de interface do usuário. Colocar o thread no estado correto para o trabalho da interface do usuário geralmente corrige o problema.
 
#### <a name="opt-out-of-clmm"></a>Ressutar o CLMM
Se uma janela de ferramentas não WPF estiver sendo migrada para dar suporte total ao PMA, ela precisará optar pelo CLMM. Para fazer isso, uma nova interface precisa ser implementada: IVsDpiAware.

```cs
[InterfaceType(ComInterfaceType.InterfaceIsIUnknown)]
public interface IVsDpiAware
{
    [ComAliasName("Microsoft.VisualStudio.Shell.Interop.VSDPIMode")]
    uint Mode {get;}
}
```

```cpp
IVsDpiAware : public IUnknown
{
    public:
        HRRESULT STDMETHODCALLTYPE get_Mode(__RCP__out VSDPIMODE *dwMode);
};
```

Para linguagens gerenciadas, o melhor lugar para implementar essa interface é na mesma classe que deriva de *Microsoft.VisualStudio.Shell.ToolWindowPane*. Para C++, o melhor lugar para implementar essa interface é na mesma classe que implementa *IVsWindowPane* de vsshell.h.

O valor retornado pela propriedade Mode na interface é um __VSDPIMODE (e é lançado em um uint em gerenciado):

```cs
enum __VSDPIMODE
{
    VSDM_Unaware    = 0x01,
    VSDM_System     = 0x02,
    VSDM_PerMonitor = 0x03,
}
```

- Não ciente significa que a janela de ferramentas precisa lidar com 96 DPI, o Windows lidará com o dimensionamento para todas as outras DPIs. Resultando em conteúdo um pouco desfocado.
- O sistema significa que a janela de ferramentas precisa lidar com o DPI para o DPI de exibição primário. Qualquer exibição com um DPI correspondente terá uma aparência nítido, mas se o DPI for diferente ou mudar durante a sessão, o Windows manipulará o dimensionamento e ficará um pouco desfocado.
- PerMonitor significa que a janela de ferramentas precisa lidar com todas as DPIs em todas as exibições e sempre que o DPI mudar.

> [!NOTE]
> Visual Studio dá suporte apenas ao reconhecimento de PerMonitorV2, portanto, o valor de enum PerMonitor se traduz no valor do Windows de DPI_AWARENESS_CONTEXT_PER_MONITOR_AWARE_V2.

#### <a name="force-a-control-into-a-specific-dpiawarenesscontext"></a>Forçar um controle em um DpiAwarenessContext específico

A interface do usuário herdado que não está sendo atualizada para dar suporte ao modo PMA ainda pode precisar de pequenos ajustes para funcionar enquanto Visual Studio está em execução no modo PMA. Uma dessas correções envolve garantir que a interface do usuário está sendo criada no DpiAwarenessContext correto. Para forçar sua interface do usuário em um DpiAwarenessContext específico, você pode inserir um escopo de DPI com o seguinte código:

```cs
using (DpiAwareness.EnterDpiScope(DpiAwarenessContext.SystemAware))
{
    Form form = new MyForm();
    form.ShowDialog();
}
```

```cpp
void MyClass::ShowDialog()
{
    VsUI::CDpiScope dpiScope(DPI_AWARENESS_CONTEXT_SYSTEM_AWARE);
    HWND hwnd = ::CreateWindow(...);
}
```

> [!NOTE]
> Forçar o DpiAwarenessContext só funciona em caixas de diálogo WPF de nível superior e interface do usuário não WPF. Ao criar uma interface do usuário do WPF que deve ser hospedada dentro de janelas de ferramentas ou designers, assim que o conteúdo é inserido na árvore de interface do usuário do WPF, ele é convertido no processo atual DpiAwarenessContext.

## <a name="known-issues"></a>Problemas conhecidos

### <a name="windows-forms"></a>Windows Forms

Para otimizar para os novos cenários de modo misto, Windows Forms como ele cria controles e janelas sempre que seu pai não foi definido explicitamente. Anteriormente, os controles sem um pai explícito usavam uma "Janela de Estacionamento" interna como um pai temporário para o controle ou a janela que está sendo criada. 

Antes do .NET 4.8, havia uma única "Janela de Estacionamento" que obtém seu DpiAwarenessContext do contexto de reconhecimento de DPI do thread atual no momento da criação da janela. Qualquer controle não esparso herda o mesmo DpiAwarenessContext que a Janela de Estacionamento quando o controle é criado e seria reparentado para o pai final/esperado pelo desenvolvedor do aplicativo. Isso causaria falhas baseadas em tempo se a "Janela de Estacionamento" tivesse um DpiAwarenessContext maior do que a janela pai final.

A partir do .NET 4.8, agora há uma "Janela de Estacionamento" para cada DpiAwarenessContext encontrado. A outra grande diferença é que o DpiAwarenessContext usado para o controle é armazenado em cache quando o controle é criado, não quando o alça é criado. Isso significa que o comportamento de término geral é o mesmo, mas pode transformar o que costumava ser um problema baseado em tempo em um problema consistente. Ele também fornece ao desenvolvedor do aplicativo um comportamento mais determinístico para escrever seu código de interface do usuário e defini-lo de scoping corretamente.
