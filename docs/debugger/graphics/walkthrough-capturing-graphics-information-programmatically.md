---
title: 'Walkthrough: capturando informações de gráficos programaticamente | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7533c205b95b016c43bd2eef614b4c2825596e74
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835648"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>Instruções passo a passo: capturando informações de gráfico de forma programática
É possível usar o Diagnóstico de Gráficos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para capturar de forma programática informações gráficas de um aplicativo Direct3D.

A captura programática é útil em cenários como:

- Inicie a captura programaticamente quando seu aplicativo de gráficos não usar SwapChain presente, como quando ele é renderizado para uma textura.

- Inicie a captura programaticamente quando seu aplicativo não renderizar, como quando ele usa DirectCompute para executar cálculos.

- Chame `CaptureCurrentFrame` quando um problema de renderização é difícil de prever e capturar em testes manuais, mas pode ser previsto programaticamente usando informações sobre o estado do aplicativo em tempo de execução.

## <a name="programmatic-capture-in-windows-10"></a><a name="CaptureDX11_2"></a>Captura programática no Windows 10
Esta parte do tutorial demonstra a captura programática em aplicativos que usam a API do DirectX 11,2 no Windows 10, que usa o método robusto de captura.

Esta seção mostra como fazer estas tarefas:

- Preparando o aplicativo para usar a captura programática

- Obtendo a interface IDXGraphicsAnalysis

- Capturando informações de gráficos

> [!NOTE]
> As implementações anteriores da captura programática se basearam em Ferramentas Remotas para Visual Studio para fornecer a funcionalidade de captura.

### <a name="preparing-your-app-to-use-programmatic-capture"></a>Preparando o aplicativo para usar a captura programática
Para usar a captura programática em seu aplicativo, ele deve incluir os cabeçalhos necessários. Esses cabeçalhos fazem parte do SDK do Windows 10.

##### <a name="to-include-programmatic-capture-headers"></a>Para incluir cabeçalhos de captura programática

- Inclua estes cabeçalhos no arquivo de origem em que a interface IDXGraphicsAnalysis será definida:

    ```cpp
    #include <DXGItype.h>
    #include <dxgi1_2.h>
    #include <dxgi1_3.h>
    #include <DXProgrammableCapture.h>
    ```

    > [!IMPORTANT]
    > Não inclua o arquivo de cabeçalho vsgcapture. h — que dá suporte à captura programática no Windows 8,0 e versões anteriores — para executar a captura programática em seus aplicativos do Windows 10. Esse cabeçalho não é compatível com o DirectX 11.2. Se esse arquivo estiver incluído depois que o cabeçalho d3d11_2. h for incluído, o compilador emitirá um aviso. Se vsgcapture. h for incluído antes de d3d11_2. h, o aplicativo não será iniciado.

    > [!NOTE]
    > Se o SDK do DirectX de junho de 2010 estiver instalado em seu computador e o caminho de inclusão do seu projeto contiver `%DXSDK_DIR%includex86` , mova-o para o final do caminho de inclusão. Faça o mesmo com o caminho da biblioteca.

### <a name="getting-the-idxgraphicsanalysis-interface"></a>Obtendo a interface IDXGraphicsAnalysis
Antes de capturar informações de gráficos do DirectX 11,2, você precisa obter a interface de depuração DXGI.

> [!IMPORTANT]
> Ao usar a captura programática, você ainda deve executar seu aplicativo em diagnóstico de gráficos (Alt + F5 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ) ou na [ferramenta de captura de linha de comando](command-line-capture-tool.md).

##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>Para obter a interface IDXGraphicsAnalysis

- Use o código a seguir para ligar a interface IDXGraphicsAnalysis à interface de depuração DXGI.

  ```cpp
  IDXGraphicsAnalysis* pGraphicsAnalysis;
  HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));
  ```

  Certifique-se de verificar o `HRESULT` retornado por [DXGIGetDebugInterface1](/windows/desktop/api/dxgi1_3/nf-dxgi1_3-dxgigetdebuginterface1) para garantir que você obtenha uma interface válida antes de usá-la:

  ```cpp
  if (FAILED(getAnalysis))
  {
      // Abort program or disable programmatic capture in your app.
  }
  ```

  > [!NOTE]
  > Se `DXGIGetDebugInterface1` retorna `E_NOINTERFACE` ( `error: E_NOINTERFACE No such interface supported` ), verifique se o aplicativo está sendo executado em diagnósticos de gráficos (Alt + F5 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ).

### <a name="capturing-graphics-information"></a>Capturando informações de gráficos
Agora que você tem uma interface `IDXGraphicsAnalysis` válida, é possível usar `BeginCapture` e `EndCapture` para capturar informações gráficas.

##### <a name="to-capture-graphics-information"></a>Para capturar informações gráficas

- Para iniciar a captura de informações gráficas, use `BeginCapture`:

    ```cpp
    ...
    pGraphicsAnalysis->BeginCapture();
    ...
    ```

    A captura começa assim que `BeginCapture` é chamado e não aguarda o início do próximo quadro. A captura para quando o quadro atual é apresentado ou quando você chama `EndCapture`:

    ```cpp
    ...
    pGraphicsAnalysis->EndCapture();
    ...
    ```

- Após a chamada para `EndCapture` , solte o objeto Graphics.

## <a name="next-steps"></a>Próximas etapas
Este passo a passo demonstrou como capturar informações gráficas de forma programática. Como próxima etapa, considere esta opção:

- Aprenda a analisar informações gráficas capturadas usando as ferramentas de diagnóstico de gráficos. Consulte [visão geral](overview-of-visual-studio-graphics-diagnostics.md).

## <a name="see-also"></a>Confira também
- [Passo a passo: capturando informações de gráficos](walkthrough-capturing-graphics-information.md)
- [Capturando informações de gráficos](capturing-graphics-information.md)
- [Ferramenta de captura de linha de comando](command-line-capture-tool.md)
