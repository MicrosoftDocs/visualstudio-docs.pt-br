---
title: Introdução ao diagnóstico de gráficos | Microsoft Docs
ms.custom: seodec18
ms.date: 06/08/2020
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68cbd19b65eb25405dc994100baf4fddeef9479d
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350453"
---
# <a name="getting-started-with-visual-studio-graphics-diagnostics"></a>Introdução ao Diagnóstico de Gráficos do Visual Studio
Nesta seção, você se preparará para usar Diagnóstico de Gráficos pela primeira vez e, em seguida, capturará quadros de um aplicativo do Direct3D e os examinará no analisador de gráficos.

## <a name="requirements"></a>Requisitos
 Para usar Diagnóstico de Gráficos no Visual Studio, você deve usar Visual Studio Enterprise, Visual Studio Professional ou comunidade do Visual Studio.  Outras edições, incluindo Visual Studio Code, não contêm esse recurso.

 [!INCLUDE[downloadvs](../includes/downloadvs_md.md)]

### <a name="windows-10-prerequisites"></a>Pré-requisitos do Windows 10
 As *ferramentas gráficas* de recursos opcionais do Windows fornecem a infraestrutura de captura e reprodução exigida pelo diagnóstico de gráficos no Windows 10.

 Para obter informações sobre como instalar ferramentas de gráficos, consulte [instalar ferramentas de gráficos para Windows 10](#InstallGraphicsTools).

## <a name="install-graphics-tools-for-windows-10"></a><a name="InstallGraphicsTools"></a>Instalar ferramentas de gráficos para Windows 10
 No Windows 10, a infra-estrutura de Diagnóstico de Gráficos é fornecida por um recurso opcional do Windows chamado *ferramentas de gráficos*. Esse recurso é necessário para capturar e reproduzir informações de gráficos no Windows 10, independentemente de o aplicativo ser capturado ter como destino uma versão anterior do Windows ou qual versão do Direct3D ela usa. Você pode optar por instalar o recurso de ferramentas de gráficos antecipadamente; caso contrário, ele será instalado sob demanda na primeira vez que você iniciar uma sessão de Diagnóstico de Gráficos do Visual Studio.

#### <a name="to-install-graphics-tools-for-windows-10"></a>Para instalar as ferramentas de gráficos para Windows 10

1. Em pesquisa, digite **aplicativos e recursos** e, em seguida, abra os **aplicativos &** configurações de recursos.

2. No lado direito dos **aplicativos &** configurações de recursos, escolha **recursos opcionais** (em **aplicativos & recursos**).

   As configurações de **recursos opcionais** são exibidas.

3. Nas configurações de **recursos opcionais** , escolha **Adicionar um recurso**. É exibida uma lista de recursos opcionais que você pode instalar.

4. Selecione **ferramentas de gráficos** na lista de recursos e escolha **instalar**.

   O recurso ferramentas de gráficos também é instalado automaticamente quando você instala o SDK do Windows 10.

> [!TIP]
> O recurso ferramentas gráficas opcionais do Windows 10 fornece funcionalidade leve de captura e reprodução, como a **dxcap.exe**do programa de captura de linha de comando, que pode ser usado em cenários de suporte, teste e diagnóstico em computadores em que as ferramentas de desenvolvedor não estão instaladas. Para obter mais informações, consulte o tópico [ferramenta de captura de linha de comando](command-line-capture-tool.md) .

## <a name="using-graphics-diagnostics-for-the-first-time"></a>Usando Diagnóstico de Gráficos pela primeira vez
 Agora que você tem tudo o que precisa, você está pronto para começar a usar Diagnóstico de Gráficos. Basta seguir estas etapas.

### <a name="1---create-a-direct3d-app"></a>1-criar um aplicativo do Direct3D

Se você já tiver seu próprio aplicativo Direct3D para explorar Diagnóstico de Gráficos, ótimo! Caso contrário, use um dos seguintes:

::: moniker range=">=vs-2019"
Baixe um exemplo do [exemplo de jogo do Direct3D](https://docs.microsoft.com/samples/microsoft/windows-universal-samples/simple3dgamedx/).
::: moniker-end
::: moniker range="vs-2017"
- Modelos de projeto do **aplicativo DirectX 11 (universal do Windows)** ou **DirectX 12 (Universal Windows)** para Windows 10.
- [Exemplo do Direct3D 12 UAP](https://code.msdn.microsoft.com/Direct3D-12-UAP-Sample-ecb1779f) para Windows 10.
::: moniker-end

Verifique se você pode compilar e executar o aplicativo antes de prosseguir. Escolha **Compilar**compilar  >  **solução** para garantir que ela seja compilada sem erros. Em seguida, escolha **depurar**  >  **Iniciar sem depuração** (**Ctrl + F5**) para certificar-se de que ele seja executado corretamente. Dependendo de qual computador você está testando com a ferramenta, talvez seja necessário ajustar a plataforma e o destino de depuração para o exemplo. Por exemplo, para testar a plataforma x64 em seu computador host do Visual Studio, escolha **x64** como a plataforma da solução e o **computador local** como seu destino de depuração. 

### <a name="2---start-a-graphics-diagnostics-session"></a>2-iniciar uma sessão de Diagnóstico de Gráficos
 Agora você está pronto para iniciar sua primeira sessão de diagnóstico de gráficos. No Visual Studio, no menu principal, escolha **depurar, gráficos, iniciar depuração de gráficos**ou apenas pressione **ALT + F5**. Isso inicia seu aplicativo em Diagnóstico de Gráficos e exibe as janelas de sessão de diagnóstico no Visual Studio.

> [!IMPORTANT]
> Se você estiver executando seu aplicativo no Windows 10 e ainda não tiver instalado o recurso de ferramentas gráficas opcionais, você será solicitado a fazer isso agora. Você deve instalá-lo antes de poder usar Diagnóstico de Gráficos no Windows 10.

### <a name="3---capture-frames"></a>3-capturar quadros
 Você está pronto para capturar quadros assim que seu aplicativo é iniciado.

#### <a name="to-capture-single-frames"></a>Para capturar quadros únicos

- No Visual Studio, escolha o botão **capturar quadro** na barra de ferramentas de gráficos ou na janela sessão de diagnóstico. Ou, se o seu aplicativo tiver foco, basta pressionar a tecla **Print Screen** no teclado.

#### <a name="to-capture-a-sequence-of-frames"></a>Para capturar uma sequência de quadros

- No Visual Studio, na janela sessão de diagnóstico, defina os **quadros a serem capturados** para o número de quadros que você deseja capturar em sequência e, em seguida, Capture a sequência usando qualquer um dos métodos descritos acima para capturar quadros únicos.

   Para capturar quadros únicos novamente, defina os **quadros a serem capturados** como *1*.

  Quando você terminar de capturar quadros, basta sair do aplicativo ou escolher o botão **parar** na barra de ferramentas de gráficos ou na janela sessão de diagnóstico.

### <a name="4---examine-captured-frames-in-the-graphics-analyzer"></a>4-examinar os quadros capturados no analisador de gráficos
 Agora você está pronto para examinar os quadros que acabou de capturar. Para começar a analisar um quadro, escolha o número do quadro que você deseja examinar na janela sessão de diagnóstico. Isso abre o quadro no **analisador de gráficos**, no qual você pode usar as ferramentas de diagnóstico de gráficos para examinar como seu aplicativo usa o Direct3D para rastrear problemas de renderização ou usar a ferramenta de **análise de quadros** para entender seu desempenho.

 Se você selecionou o quadro incorreto na janela sessão de diagnóstico ou deseja examinar um quadro diferente, poderá selecionar um novo no analisador de gráficos. Na guia **destino de renderização** da janela de log de gráficos, sob a imagem de destino de renderização, expanda a **lista de quadros** e escolha um quadro diferente para examinar.

 Para saber mais sobre como usar as ferramentas do analisador de gráficos juntas, consulte os [exemplos](graphics-diagnostics-examples.md).

## <a name="see-also"></a>Veja também
- [Elementos gráficos do Direct3D 12](/windows/desktop/direct3d12/direct3d-12-graphics)