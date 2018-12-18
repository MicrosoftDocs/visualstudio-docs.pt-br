---
title: Ferramenta de linha de comando de captura | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: db75b3a7-80b2-4a74-91d2-fd6e0f73b45d
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7b5de323a14bd005e10db4c17281a3b947381f26
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2018
ms.locfileid: "43775540"
---
# <a name="command-line-capture-tool"></a>Ferramenta de captura de linha de comando
O DXCap.exe é uma ferramenta de linha de comando para reprodução e captura de diagnóstico de gráficos. Ele dá suporte a Direct3D 10 através de Direct3D 12 em todos os níveis de recurso.  
  
## <a name="syntax"></a>Sintaxe  
  
```cmd  
DXCap.exe [-file filename] [-frame frames | -period periods | -manual] -c app [args...]  
DXCap.exe -p [filename] [-debug | -warp | -hw] [-config] [-rawmode]  
DXCap.exe -p [filename] -screenshot [-frame frames]  
DXCap.exe -p [filename] -toXML [xml_filename]  
DXCap.exe -v [-file filename] [-examine events] [-haltonfail | -exitonfail] [-showprogress]  
DXCap.exe -e [search_string]  
DXCap.exe -info  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `-file` `filename`  
 No modo de captura (`-c`), `filename` Especifica o nome do arquivo de log de gráficos que informações gráficas são registradas. Se `filename` não for especificado, informações gráficas são registradas em um arquivo chamado `<appname>-<date>-<time>.vsglog` por padrão.  
  
 Na validação (-v), o modo `filename` especifica o nome do arquivo de log de gráficos a ser validado. Se `filename` não for especificado, o log de gráficos que foi validado pela última vez é usado novamente.  
  
 `-frame` `frames`  
 No modo de captura, `frames` especifica os quadros que você deseja capturar. O primeiro quadro é 1. Você pode especificar vários quadros usando vírgulas e intervalos. Por exemplo, se `frames` está `2, 5, 7-9, 15`, em seguida, quadros `2`, `5`, `7`, `8`, `9`, e `15` são capturados.  

> [!TIP]
> Use `-frame` `manual` para especificar que quadros serão capturados manualmente pressionando a tecla Print Screen. Quadros poderão ser capturados quando o aplicativo é iniciado. Para parar a captura quadros, retorne para a interface de linha de comando e pressione enter.  
  
 `-period` `periods`  
 No modo de captura, `periods` especifica os intervalos de tempo, em segundos, durante o qual você deseja capturar quadros. Você pode especificar vários períodos usando vírgulas e intervalos. Por exemplo se `periods` está `2.1-5, 7.0-9.3`, em seguida, os quadros são renderizados entre `2.1` e `5` segundos e entre`7` e `9.3` são capturados.  
  
 `-c` `app` [`args...`]  
 Modo de captura. No modo de captura, `app` especifica o nome do aplicativo do qual você deseja capturar informações gráficas; `args...` especifica os parâmetros de linha de comando adicionais para que o aplicativo.  
  
 `-p` [`filename`]  
 Modo de reprodução (`-p`). No modo de reprodução `filename` especifica o nome do arquivo de log de gráfico a ser executado. Se `filename` não for especificado, o log de gráficos que foi reproduzido pela última vez é usado novamente.  
  
 `-debug`  
 No modo de reprodução, `-debug` Especifica que a reprodução deve ser reproduzida com a camada de depuração Direct3D habilitada.  
  
 `-warp`  
 No modo de reprodução, `-warp` Especifica que a reprodução deve ser reproduzida usando o renderizador de software WARP.  
  
 `-hw`  
 No modo de reprodução, `-hw` Especifica que a reprodução deve ser reproduzida usando hardware de GPU.  
  
 `-config`  
 No modo de reprodução, `-config` exibe todas as informações sobre o computador que foi usado para capturar o arquivo de log de gráficos.  
  
 `-rawmode`  
 No modo de reprodução, `-rawmode` Especifica que a reprodução deve ser executada sem modificação nos eventos registrados. Durante a operação normal, o modo de reprodução pode realizar pequenas alterações na reprodução para simplificar a depuração e acelerar a reprodução. Por exemplo, ele pode simular a saída de cadeia de troca em vez de executar comandos de cadeia de troca. Normalmente, essa reprodução não é um problema, mas talvez seja necessário reprodução ocorra de maneira mais fiel possível para o evento gravado. Por exemplo, você pode usar essa opção para restaurar o comportamento de renderização em tela inteira para um aplicativo que foi capturado durante a execução em modo de tela inteira.  
  
 `-toXML` [`xml_filename`]  
 No modo de reprodução, `xml_filename` especifica o nome do arquivo onde uma representação XML da reprodução é gravada. Se `xml_filename` não for especificado, a representação XML é gravada em um arquivo com o mesmo nome que o arquivo está sendo reproduzido, mas recebe uma extensão `.xml`.  
  
 `-v`  
 Modo de validação. No modo de validação, os quadros capturados são executados novamente no hardware e no WARP e seus resultados são comparados usando uma função de comparação de imagem. Você pode usar esse recurso para identificar rapidamente problemas de driver que afetam a renderização.  
  
 `-examine` `events`  
 No modo de validação, `events` especifica o conjunto de eventos gráficos cujos resultados imediatos são comparados. Por exemplo, `-examine present,draw,copy,clear` limita a comparação aos eventos que pertencem a essas categorias.  
  
> [!TIP]
>  É recomendável iniciar com `-examine present,draw,copy,clear` porque isso irá revelar a maioria dos problemas, mas leva muito menos tempo que um conjunto mais abrangente de eventos. Se necessário, você pode especificar um conjunto diferente ou maior de eventos para validar tais eventos e revelar outros tipos de problemas.  
  
 `-haltonfail`  
 No modo de validação, `-haltonfail` interrompe a validação quando são detectadas diferenças entre o hardware e o renderizador WARP. A validação continua após uma tecla ser pressionada.  
  
 `-exitonfail`  
 No modo de validação, `-exitonfail` sai da validação imediatamente quando são detectadas diferenças entre o hardware e o renderizador WARP. Quando o programa sai dessa forma, ele retorna `0` no ambiente; caso contrário, retornará `1`.  
  
 `-showprogress`  
 No modo de validação, `-showprogress` exibe informações de progresso sobre a sessão de validação. O andamento do WARP é exibido à esquerda, enquanto o progresso de hardware é exibido à direita.  
  
 `-e` `search_string`  
 Enumera os aplicativos UWP que são instalados. Você pode usar essas informações para executar capturas de linha de comando com aplicativos da UWP.  
  
 `-info`  
 Exibe informações sobre as DLLs de captura e do computador.  
  
## <a name="remarks"></a>Comentários  
 O DXCap.exe opera em três modos:  
  
 Modo de captura (-c)  
 Captura as informações gráficas de um aplicativo em execução e registra-as em um arquivo de log de gráficos. Os recursos de captura e o formato de arquivo são idênticos aos do Visual Studio.  
  
 Modo de reprodução (-p)  
 Reprodução de eventos de gráficos de um arquivo de log existente gráficos capturados anteriormente. Por padrão, a reprodução ocorre em uma janela, mesmo quando o arquivo de log de gráficos foi capturado de um aplicativo de tela inteira. A reprodução ocorre em tela inteira somente quando os gráficos de log arquivo foi capturado de um aplicativo de tela inteira e `-rawmode` for especificado.  
  
 Modo de validação (`-v`)  
 Valida o comportamento de renderização ao reproduzir os quadros capturados em hardware e no WARP, em seguida, comparando seus resultados usando uma função de comparação de imagem. Você pode usar esse recurso para identificar rapidamente problemas de driver que afetam a renderização.  
  
 Além desses modos, o dxcap.exe executa outras duas funções que não executam captura ou reprodução de informações de grafos.  
  
 Função de enumeração (`-e`)  
 Exibe detalhes sobre os aplicativos UWP que são instalados no computador. Esses detalhes incluem o nome do pacote e appid que identificam o arquivo executável em um aplicativo UWP. Para capturar informações de elementos gráficos de um aplicativo da Windows Store usando DXCap.exe, use o nome do pacote e appid em vez do nome do arquivo executável que é usado ao capturar um aplicativo de área de trabalho.  
  
 Info (de função`-info)`  
 Exibe os detalhes sobre as DLLs de captura e do computador.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="capture-graphics-information-from-a-desktop-app"></a>Captura as informações gráficas de um aplicativo de área de trabalho  
 Use `-c` para especificar o aplicativo do qual você deseja capturar informações gráficas.  
  
```cmd  
DXCap.exe -c BasicHLSL11.exe  
```  
  
 Por padrão, as informações gráficas são registradas em um arquivo chamado `<appname>-<date>-<time>.vsglog`. Use `-file` para especificar um arquivo diferente para o registro.  
  
```cmd  
DXCap.exe -file regression_test_12.vsglog -c BasicHLSL11.exe  
```  
  
 Especifica parâmetros adicionais de linha de comando para o aplicativo sendo capturado, incluindo-as após o nome de arquivo do aplicativo.  
  
```cmd  
DXCap.exe -c "C:\Program Files\Internet Explorer\iexplorer.exe" "www.fishgl.com"  
```  
  
 O comando no exemplo acima captura informações de gráficos da versão de área de trabalho do Internet Explorer ao exibir a página da Web localizada em www.fishgl.com que usa a API WebGL para processar conteúdo 3D.  
  
> [!NOTE]
>  Como argumentos de linha de comando que aparecem após o aplicativo são passados para ele, você deve especificar os argumentos destinados DXCap.exe antes de usar o `-c` opção.  
  
### <a name="capture-graphics-information-from-a-uwp-app"></a>Capture informações gráficas de um aplicativo UWP.  
 Você pode capturar informações gráficas de um aplicativo UWP.  
  
```cmd  
DXCap.exe -c Microsof.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe,AppexMaps  
```  
  
 Usando o DXCap.exe para capturar a partir de um aplicativo UWP é semelhante a usá-lo para capturar a partir de um aplicativo da área de trabalho do Windows, mas em vez disso, a identificação de um aplicativo da área de trabalho por seu nome de arquivo, você identificar um aplicativo UWP pelo seu nome de pacote e o nome ou ID do executável dentro do pacote que você deseja  Capture de. Para tornar mais fácil de descobrir como identificar os aplicativos UWP que são instalados em seu computador, use o `-e` opção com DXCap.exe para enumerá-los:  
  
```cmd  
DXCap.exe -e  
```  
  
 Você pode fornecer uma cadeia de caracteres de pesquisa opcional para ajudar a encontrar o aplicativo que está procurando. Quando a cadeia de caracteres de pesquisa é fornecida, DXCap.exe enumera os aplicativos UWP cujo nome do pacote, o nome do aplicativo ou IDs do aplicativo correspondem a cadeia de caracteres de pesquisa. A pesquisa diferencia maiúsculas de minúsculas.  
  
```cmd  
DXCap.exe -e map  
```  
  
 O comando acima enumera os aplicativos UWP que correspondem a "mapa"; Aqui está a saída:  
  
 **Pacote "Microsoft.BingMaps":**  
 **InstallDirectory: C:\Program Files\WindowsApps\Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe**  
 **FullName: Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe**  
 **UserSID          : S-1-5-21-2127521184-1604012920-1887927527-5603533**  
 **Nome: Microsoft.BingMaps**  
 **Publicador: CN = Microsoft Corporation, O = Microsoft Corporation, L = Redmond, S = Washington, C = US**  
 **Versão: 2.1.2914.1734**  
 **Aplicativos pode ser iniciados:**  
 **ID: AppexMaps**  
 **Exe: C:\Program Files\WindowsApps\Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe\Map.exe**  
 **IsWWA: nenhum**  
 **AppSpec (para iniciar): DXCap.exe - c Microsoft.BingMaps_2.1.2914.1734_x64__8wekyb3d8bbwe,AppexMaps** a última linha da saída de cada aplicativo enumerado exibe o comando que você pode usar para capturar informações gráficas.  
  
### <a name="capture-specific-frames-or-frames-between-specific-times"></a>Capturar quadros específicos ou quadros entre horários específicos.  
 Use `-frame` para especificar os quadros que você deseja capturar usando vírgulas e intervalos:  
  
```cmd  
DXCap.exe -frame 2,5,7-9,15 -c SimpleBezier11.exe  
```  
  
 Ou use `-period` para especificar um conjunto de intervalos de tempo durante o qual você deseja capturar quadros. Os intervalos de tempo são especificados em segundos e vários intervalos podem ser especificados:  
  
```cmd  
DXCap.exe -period 2.1-5, 7.0-9.3 -c SimpleBezier11.exe  
```  
  
### <a name="capture-frames-interactively"></a>Capturar quadros interativamente.  
 Use `-manual` para capturar quadros interativamente. Pressione a tecla Enter para iniciar a captura e pressione Enter novamente para parar.  
  
```cmd  
DXCap.exe -manual -c SimpleBezier11.exe  
```  
  
### <a name="play-back-a-graphic-log-file"></a>Reproduzir um arquivo de log de gráficos  
 Use `-p` para reproduzir um arquivo de log de gráficos capturadas anteriormente.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog  
```  
  
 Deixe o nome do arquivo para reproduzir o log de gráficos que foi capturado mais recentemente.  
  
```cmd  
DXCap.exe -p  
```  
  
### <a name="play-back-in-raw-mode"></a>Reproduzir no modo bruto  
 Use `-rawmode` para reproduzir comandos capturados exatamente como eles ocorreram. Na reprodução normal, certos comandos são emulados, por exemplo, um arquivo de log de gráficos capturado em um aplicativo em tela inteira será executado em uma janela, porém com o modo bruto habilitado, o mesmo arquivo tentará ser reproduzido em tela inteira.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog -rawmode  
```  
  
### <a name="play-back-using-warp-or-a-hardware-device"></a>Reproduzir usando o WARP ou um dispositivo de hardware  
 Você pode desejar forçar a reprodução de um arquivo de log de gráficos capturado em um dispositivo de hardware para usar o WARP, ou então forçar a reprodução de um log capturado no WARP para usar um dispositivo de hardware. Use `-warp` para reproduzir usando o WARP.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog -warp  
```  
  
 Use `-hw` para reproduzir usando o hardware.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog -hw  
```  
  
### <a name="validate-a-graphics-log-file-against-warp"></a>Validar um arquivo de log de gráficos contra o WARP  
 No modo de validação, o arquivo de log de gráficos é reproduzido no hardware e no WARP, e seus resultados são comparados. Isso pode ajudá-lo a identificar erros de renderização causados pelo driver. Use - v para validar o comportamento correto do hardware de gráficos contra o WARP.  
  
```cmd  
DXCap.exe -v regression_test_12.vsglog  
```  
  
 Para reduzir a quantidade de comparações, você pode especificar um subconjunto de comandos de validação comparar e outros comandos serão ignorados. Use – examine para especificar os comandos cujos resultados você deseja comparar.  
  
```cmd  
DXCap.exe -v regression_test_12.vsglog -examine present,draw,copy,clear  
```  
  
### <a name="convert-a-graphics-log-file-to-pngs"></a>Converter um arquivo de log de gráficos para PNGs  
 Para exibir ou analisar os quadros de um arquivo de log de gráficos, o DXCap.exe pode salvar quadros capturados como arquivo de imagem .png (Portable Network Graphics). Use `-screenshot` no modo de reprodução para produzir os quadros capturados como arquivos. PNG.  
  
```cmd  
DXCap.exe -p BasicHLSL11.vsglog -screenshot  
```  
  
 Use `-frame` com `-screenshot` para especificar os quadros que você deseja gerar.  
  
```cmd  
DXCap.exe -p BasicHLSL11.vsglog -screenshot -frame 5, 7-9  
```  
  
### <a name="convert-a-graphics-log-file-to-xml"></a>Converter um arquivo de log de gráficos para XML  
 Para processar e analisar os logs de gráficos usando ferramentas conhecidas como FindStr ou XSLT, o DXCap.exe pode converter um arquivo de log de gráficos em XML. Use `-toXML` no modo de reprodução para converter o log em XML, em vez de reproduzi-lo de volta.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog -toXML  
```  
  
 Por padrão, a saída XML é gravada em um arquivo com o mesmo nome que o log de gráficos, porém com uma extensão .xml. No exemplo acima, o arquivo XML será nomeado **regression_test_12.xml**. Para fornecer o arquivo XML com um nome diferente, especifique-o após `-toXML`.  
  
```cmd  
DXCap.exe -p regression_test_12.vsglog -toXML temp.xml  
```  
  
 O arquivo resultante conterá um XML semelhante a este:  
  
```xml  
<Moment value="67"/>  
<Method name="CreateDXGIFactory1" >  
    <Return type="HRESULT" value="S_OK" />  
    <Parameter name="riid" type="IID" value="770AAE78-F26F-4DBA-A829-253C83D1B387" />  
    <Parameter name="ppFactory" type="void" handle="1" isOutput="true" />  
</Method>  
  
<Moment value="167"/>  
<Method name="D3D11CreateDevice" >  
    <Return type="HRESULT" value="S_OK" />  
    <Parameter name="pAdapter" type="IDXGIAdapter" handle="34" />  
    <Parameter name="DriverType" type="D3D_DRIVER_TYPE" value="D3D_DRIVER_TYPE_UNKNOWN" />  
    <Parameter name="Software" type="HMODULE" value="pointer" />  
    <Parameter name="Flags" type="UINT" value="0" />  
    <Parameter name="pFeatureLevels" type="D3D_FEATURE_LEVEL" arrSize="1" >  
        <Element value="D3D_FEATURE_LEVEL_11_0" />  
    </Parameter>  
    <Parameter name="FeatureLevels" type="UINT" value="1" />  
    <Parameter name="SDKVersion" type="UINT" value="7" />  
    <Parameter name="ppDevice" type="ID3D11Device" handle="35" isOutput="true" />  
    <Parameter name="pFeatureLevel" type="D3D_FEATURE_LEVEL" value="D3D_FEATURE_LEVEL_11_0" isOutput="true" />  
    <Parameter name="ppImmediateContext" type="ID3D11DeviceContext" value="nullptr" isOutput="true" />  
</Method>  
```  
  
## <a name="requirements"></a>Requisitos