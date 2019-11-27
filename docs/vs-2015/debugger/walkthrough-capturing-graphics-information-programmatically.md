---
title: 'Walkthrough: capturando informações de gráficos programaticamente | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a5adeff9-afaf-4047-b5ce-ef0aefe710eb
caps.latest.revision: 24
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 54097420fd212ec9057f4a968e2c6d5de199e56e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2019
ms.locfileid: "74296908"
---
# <a name="walkthrough-capturing-graphics-information-programmatically"></a>Instruções passo a passo: capturando informações de gráfico de forma programática
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível usar o Diagnóstico de Gráficos do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para capturar de forma programática informações gráficas de um aplicativo Direct3D.  
  
 A captura programática é útil em cenários como:  
  
- Inicie a captura programaticamente quando seu aplicativo de gráficos não usar SwapChain presente, como quando ele é renderizado para uma textura.  
  
- Inicie a captura programaticamente quando seu aplicativo não renderizar, como quando ele usa DirectCompute para executar cálculos.  
  
- Chame `CaptureCurrentFrame`quando um problema de renderização é difícil de prever e capturar em testes manuais, mas pode ser previsto programaticamente usando informações sobre o estado do aplicativo em tempo de execução.  
  
## <a name="CaptureDX11_2"></a>Captura programática no Windows 8.1  
 Esta parte do passo a passos demonstra a captura programática em aplicativos que usam a API do DirectX 11,2 no Windows 8.1, que usa o método de captura robusto. Para obter informações sobre como usar a captura programática em aplicativos que usam versões anteriores do DirectX no Windows 8,0, consulte a [captura programática no windows 8,0 e versões anteriores](#CaptureDX11_1) , nesta explicação.  
  
 Esta seção mostra como fazer estas tarefas:  
  
- Preparando o aplicativo para usar a captura programática  
  
- Obtendo a interface IDXGraphicsAnalysis  
  
- Capturando informações de gráficos  
  
> [!NOTE]
> As implementações anteriores da captura programática se basearam em Ferramentas Remotas para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] fornecer a funcionalidade de captura, Windows 8.1 dá suporte à captura diretamente por meio do Direct3D 11,2. Como resultado, você não precisa mais instalar o Ferramentas Remotas para a captura programática no Windows 8.1.  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>Preparando o aplicativo para usar a captura programática  
 Para usar a captura programática em seu aplicativo, ele deve incluir os cabeçalhos necessários. Esses cabeçalhos fazem parte do SDK do Windows 8.1.  
  
##### <a name="to-include-programmatic-capture-headers"></a>Para incluir cabeçalhos de captura programática  
  
- Inclua estes cabeçalhos no arquivo de origem em que a interface IDXGraphicsAnalysis será definida:  
  
    ```  
    #include <DXGItype.h>  
    #include <dxgi1_2.h>  
    #include <dxgi1_3.h>  
    #include <DXProgrammableCapture.h>  
    ```  
  
    > [!IMPORTANT]
    > Não inclua o arquivo de cabeçalho vsgcapture. h — que dá suporte à captura programática no Windows 8,0 e versões anteriores — para executar a captura programática em seus aplicativos Windows 8.1. Esse cabeçalho não é compatível com o DirectX 11.2. Se esse arquivo estiver incluído depois que o cabeçalho d3d11_2. h for incluído, o compilador emitirá um aviso. Se vsgcapture. h for incluído antes de d3d11_2. h, o aplicativo não será iniciado.  
  
    > [!NOTE]
    > Se o SDK do DirectX de junho de 2010 estiver instalado em seu computador e o caminho de inclusão do seu projeto contiver `%DXSDK_DIR%includex86`, mova-o para o final do caminho de inclusão. Faça o mesmo com o caminho da biblioteca.  
  
#### <a name="windows-phone-81"></a>Windows Phone 8.1  
 Como o SDK do Windows Phone 8,1 não inclui o cabeçalho DXProgrammableCapture. h, você precisará definir a interface `IDXGraphicsAnalysis` por conta própria para poder usar os métodos `BeginCapture()` e `EndCapture()`. Inclua os outros cabeçalhos, conforme descrito na seção anterior.  
  
###### <a name="to-define-the-idxgraphicsanalysis-interface"></a>Para definir a interface IDXGraphicsAnalysis  
  
- Defina a interface IDXGraphicsAnalysis no mesmo arquivo em que você incluiu os arquivos de cabeçalho.  
  
  ```  
  interface DECLSPEC_UUID("9f251514-9d4d-4902-9d60-18988ab7d4b5") DECLSPEC_NOVTABLE  
  IDXGraphicsAnalysis : public IUnknown  
  {  
      STDMETHOD_(void, BeginCapture)() PURE;  
      STDMETHOD_(void, EndCapture)() PURE;  
  };  
  ```  
  
  Por uma questão de comodidade, é possível realizar essas etapas em um novo arquivo de cabeçalho, em seguida, incluí-lo onde for necessário no aplicativo.  
  
### <a name="getting-the-idxgraphicsanalysis-interface"></a>Obtendo a interface IDXGraphicsAnalysis  
 Antes de capturar informações de gráficos do DirectX 11,2, você precisa obter a interface de depuração DXGI.  
  
> [!IMPORTANT]
> Ao usar a captura programática, você ainda deve executar seu aplicativo em diagnóstico de gráficos (Alt + F5 no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]) ou na [ferramenta de captura de linha de comando](../debugger/command-line-capture-tool.md).  
  
##### <a name="to-get-the-idxgraphicsanalysis-interface"></a>Para obter a interface IDXGraphicsAnalysis  
  
- Use o código a seguir para ligar a interface IDXGraphicsAnalysis à interface de depuração DXGI.  
  
    ```  
    IDXGraphicsAnalysis* pGraphicsAnalysis;  
    HRESULT getAnalysis = DXGIGetDebugInterface1(0, __uuidof(pGraphicsAnalysis), reinterpret_cast<void**>(&pGraphicsAnalysis));  
    ```  
  
     Não se esqueça de verificar o `HRESULT` retornado por `DXGIGetDebugInterface1` para garantir que você obtenha uma interface válida antes de usá-la:  
  
    ```  
    if (FAILED(getAnalysis))  
    {  
        // Abort program or disable programmatic capture in your app.  
    }  
    ```  
  
    > [!NOTE]
    > Se `DXGIGetDebugInterface1` retornar `E_NOINTERFACE` (`error: E_NOINTERFACE No such interface supported`), verifique se o aplicativo está sendo executado sob o diagnóstico de gráficos (Alt + F5 no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]).  
  
### <a name="capturing-graphics-information"></a>Capturando informações de gráficos  
 Agora que você tem uma interface `IDXGraphicsAnalysis` válida, é possível usar `BeginCapture` e `EndCapture` para capturar informações gráficas.  
  
##### <a name="to-capture-graphics-information"></a>Para capturar informações gráficas  
  
- Para iniciar a captura de informações gráficas, use `BeginCapture`:  
  
    ```  
    ...  
    pGraphicsAnalysis->BeginCapture();  
    ...  
    ```  
  
     A captura começa assim que `BeginCapture` é chamado e não aguarda o início do próximo quadro. A captura para quando o quadro atual é apresentado ou quando você chama `EndCapture`:  
  
    ```  
    ...  
    pGraphicsAnalysis->EndCapture();  
    ...  
    ```  
  
## <a name="CaptureDX11_1"></a>Captura programática no Windows 8,0 e versões anteriores  
 Esta parte do tutorial demonstra a captura programática em aplicativos para o Windows 8,0 e versões anteriores que usam a API do DirectX 11,1, que usa o método de captura herdado. Para obter informações sobre como usar a captura programática em aplicativos que usam o DirectX 11,2 em Windows 8.1, consulte [captura programática em Windows 8.1](#CaptureDX11_2) anteriormente neste passo a passos.  
  
 Esta parte mostra estas tarefas:  
  
- Preparando o computador para usar a captura programática  
  
- Preparando o aplicativo para usar a captura programática  
  
- Configurando o nome e o local do arquivo de log dos gráficos  
  
- Usando a API do `CaptureCurrentFrame`  
  
### <a name="preparing-your-computer-to-use-programmatic-capture"></a>Preparando o computador para usar a captura programática  
 A API de captura programática usa as Ferramentas Remotas para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para fornecer funcionalidade de captura. O computador em que o aplicativo será executado deve ter as ferramentas remotas instaladas, mesmo quando você esteja usando a captura programática no computador local. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não precisa estar em execução quando você executa a captura programática em um computador local.  
  
 Para usar as APIs de captura remota em um aplicativo que esteja em execução em um computador, primeiro, você precisa instalar as Ferramentas Remotas para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] nesse computador. Diferentes versões das ferramentas remotas dão suporte a diferentes plataformas de hardware. Para obter informações sobre como instalar as ferramentas remotas, consulte a [página de download do ferramentas remotas](https://go.microsoft.com/fwlink/p/?LinkId=246691) no site de downloads da Microsoft.  
  
 Como alternativa, o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] instala os componentes necessários para a realização de captura remota de aplicativos de 32 bits.  
  
> [!NOTE]
> Como a maioria dos aplicativos da área de trabalho do Windows, inclusive o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], não é compatível no [!INCLUDE[win8](../includes/win8-md.md)] para dispositivos ARM, o uso das Ferramentas Remotas para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] com a API de captura programática é a única maneira de capturar diagnósticos de gráfico em dispositivos ARM.  
  
### <a name="preparing-your-app-to-use-programmatic-capture"></a>Preparando o aplicativo para usar a captura programática  
 Para usar as ferramentas de diagnóstico de gráficos, primeiro, você precisa capturar as informações gráficas nas quais ele confia. É possível capturar de forma programática as informações usando a API do `CaptureCurrentFrame`.  
  
##### <a name="to-prepare-your-app-to-capture-graphics-information-programmatically"></a>Para preparar o aplicativo para capturar informações gráficas de forma programática  
  
1. Verifique se o cabeçalho `vsgcapture.h` está incluído no código-fonte do aplicativo. Ele pode estar incluído em apenas um local, por exemplo, no arquivo de código-fonte em que você chamará a API de captura programática, ou em um arquivo de cabeçalho pré-compilado para chamar a API de vários arquivos de código-fonte.  
  
2. No código-fonte do aplicativo, sempre que quiser capturar o restante do quadro atual, chame `g_pVsgDbg->CaptureCurrentFrame()`. Esse método não utiliza parâmetros e não retorna um valor.  
  
### <a name="configuring-the-name-and-location-of-the-graphics-log-file"></a>Configurando o nome e o local do arquivo de log dos gráficos  
 O log de gráficos é criado no local definido pelas macros `DONT_SAVE_VSGLOG_TO_TEMP` e `VSG_DEFAULT_RUN_FILENAME`.  
  
##### <a name="to-configure-the-name-and-location-of-the-graphics-log-file"></a>Para configurar o nome e o local do arquivo de log dos gráficos  
  
- Para evitar que o log de gráficos seja gravado no diretório temporário, antes da linha `#include <vsgcapture.h>`, adicione:  
  
  ```  
  #define DONT_SAVE_VSGLOG_TO_TEMP  
  ```  
  
   É possível definir esse valor para gravar o log de gráficos em um local relativo para o diretório de trabalho ou em um caminho absoluto, caso a definição de `VSG_DEFAULT_RUN_FILENAME` seja um caminho absoluto.  
  
- Para salvar o log de gráficos em um local diferente ou dar a ele um nome de arquivo diferente, antes da linha `#include <vsgcapture.h>`, adicione:  
  
  ```  
  #define VSG_DEFAULT_RUN_FILENAME <filename>  
  ```  
  
   Se você não realizar essa etapa, o nome do arquivo será default.vsglog. Se você não definiu `DONT_SAVE_VSGLOG_TO_TEMP`, o local do arquivo será relativo para o diretório temporário. Do contrário, ele será relativo para o diretório de trabalho ou em outro local, caso tenha sido especificado um nome de arquivo absoluto.  
  
  Para [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] aplicativos, o local do diretório temporário é específico para cada usuário e aplicativo e normalmente é encontrado em um local como C:\Users\\*username*\AppData\Local\Packages\\*Package family Name*\TempState\\. Para aplicativos da área de trabalho, o local do diretório temporário é específico para cada usuário e normalmente é encontrado em um local como C:\Users\\*username*\AppData\Local\Temp\\.  
  
> [!NOTE]
> Para gravar em um local específico, você deve ter permissões para gravar nesse local, ou ocorrerá um erro. Lembre-se de que os aplicativos do [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] são mais restritos do que os aplicativos da área de trabalho em relação ao local onde podem gravar dados e podem exigir configuração adicional para gravação em determinados locais.  
  
### <a name="capturing-the-graphics-information"></a>Capturando as informações gráficas  
 Depois que você tiver preparado o aplicativo para captura programática e, como opção, configurado o local e o nome do arquivo de log de gráficos, compile o aplicativo, em seguida, execute ou o depure para capturar dados. Não inicie o diagnóstico de gráficos no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] quando você usar a API de captura programática. O log de gráficos é gravado no local especificado por você. Se quiser manter essa versão do log, mova-a para outro local. Do contrário, ela será substituída quando o aplicativo for executado novamente.  
  
> [!TIP]
> Você ainda pode capturar as informações de gráficos manualmente enquanto estiver usando a captura programática — com o aplicativo em foco, basta pressionar a **tela de impressão**. Você pode usar essa técnica para capturar informações gráficas adicionais não capturadas pela API de captura programática.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo demonstrou como capturar informações gráficas de forma programática. Como próxima etapa, considere esta opção:  
  
- Aprenda a analisar informações gráficas capturadas usando as ferramentas de diagnóstico de gráficos. Consulte [visão geral](../debugger/overview-of-visual-studio-graphics-diagnostics.md).  
  
## <a name="see-also"></a>Consulte também  
 [Walkthrough: capturando informações de gráficos](../debugger/walkthrough-capturing-graphics-information.md)   
 [Como capturar informações de gráficos](../debugger/capturing-graphics-information.md)   
 [Ferramenta de captura de linha de comando](../debugger/command-line-capture-tool.md)
