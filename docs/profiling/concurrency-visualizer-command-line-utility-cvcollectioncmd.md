---
title: Utilitário de linha de comando Visualização Simultânea (CVCollectionCmd) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.performance.cvcollectioncmd
ms.assetid: 476601be-1608-4014-af15-5aba6ccbed1c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a24bea13687d58d4d9b9d9dc8ecf0bec86595759
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951230"
---
# <a name="concurrency-visualizer-command-line-utility-cvcollectioncmd"></a>Utilitário de linha de comando da Visualização Simultânea (CVCollectionCmd)
É possível usar o utilitário de linha de comando do Visualização Simultânea (*CVCollectionCmd.exe*) para coletar rastreamentos na linha de comando para que seja possível exibi-los na Visualização Simultânea do Visual Studio. As ferramentas podem ser usadas em computadores que não tenham o Visual Studio instalado.  

> [!NOTE]
>  A partir do Visual Studio 2013, a Visualização Simultânea é uma extensão opcional. (Anteriormente, ela havia sido incluída no Visual Studio.) É possível baixar as [ferramentas de coleção da Visualização Simultânea para o Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=49103) do Centro de Download.  

## <a name="download-the-concurrency-visualizer-command-line-utility"></a>Baixar o utilitário de linha de comando da Visualização Simultânea  
 Para baixar e instalar o utilitário de linha de comando, vá para [Coleção de Ferramentas de Visualização Simultânea para Visual Studio 2015](http://www.microsoft.com/download/details.aspx?id=49103) e siga as instruções. Por padrão, *CVCollectionCmd.exe* é instalado em %ProgramFiles%\Microsoft Concurrency Visualizer Collection Tools\ (%ProgramFiles(x86)%\Microsoft Concurrency Visualizer Collection Tools\ em computadores x64).  

## <a name="collect-a-trace-with-cvcollectioncmd"></a>Coletar um rastreamento usando CVCollectionCmd  
 Você pode coletar um rastreamento iniciando o aplicativo com CVCollectionCmd ou se conectando a ele. Consulte a referência aos comandos abaixo para ver as opções. Por exemplo  

```cmd  
<Path>CVCollectionCmd /launch c:\myapp\myapp.exe /outdir c:\myapp\data  
```  

## <a name="commands-and-parameters"></a>Comandos e parâmetros  
 Para obter ajuda sobre os comandos e os parâmetros no utilitário de linha de comando, digite isto no prompt de comando:  

 **CvCollectionCmd /?**  

|Opção|Descrição|Parâmetros|Valores de retorno|  
|------------|-----------------|----------------|-------------------|  
|Consulta|Retorna se a coleta pode ser iniciada.|Nenhum|0 se a coleta estiver pronta para começar.<br /><br /> 1 se a coleta já estiver em andamento.<br /><br /> 2 se a coleta não estiver em andamento, mas uma ou mais sessões [ETW](/dotnet/framework/wcf/samples/etw-tracing) necessárias já estiverem habilitadas.|  
|Inicializar|Executa o processo especificado na Visualização Simultânea.|O caminho do executável.|0 se a execução foi bem-sucedida.<br /><br /> 1 se a execução falhou porque não foi possível iniciar o aplicativo de destino.<br /><br /> 13 se a execução falhou porque CVCollectionCmd não tem permissões suficientes para gravar no diretório de saída especificado.|  
|Attach|Começa coletando um rastreamento em todo o sistema. Do contrário, se conecta a um processo, se algum for especificado.|Nenhum.|0 se o anexo for bem-sucedido.<br /><br /> 1 se o anexo falhou porque o processo especificado é inválido ou ambíguo.<br /><br /> 13 se o anexo falhou porque CVCollectionCmd não tem permissões suficientes para gravar no diretório de saída especificado.|  
|Detach|Para a coleta.|nenhuma.|0 se a desanexação for bem-sucedida.<br /><br /> 1 se a desanexação falhou porque a coleta não está em andamento no momento.<br /><br /> 2 se a desanexação falhou porque a coleta não pode ser parada.|  
|Analisar|Analisa o rastreamento especificado.|O caminho completo do arquivo CVTrace.|0 se a análise for bem-sucedida.<br /><br /> 1 se a análise não puder ser iniciada porque o rastreamento especificado estava em todo o sistema, mas sem um processo de destino especificado.<br /><br /> 2 se a análise não puder ser iniciada porque o rastreamento não estava em todo o sistema e um processo foi especificado.<br /><br /> 3 se a análise falhou porque o processo especificado é inválido.<br /><br /> 4 se a análise falhou porque o arquivo CVTrace especificado é inválido.|  
|LaunchArgs|Especifica os argumentos executáveis de destino. Essa opção só se aplica ao comando Inicializar.|Os argumentos de linha de comando para o aplicativo.|nenhuma.|  
|Outdir|Especifica o diretório no qual os arquivos de rastreamento serão salvos. Aplica-se aos comandos Inicializar e Anexar.|Um caminho do diretório ou relativo.|nenhuma.|  
|Processo|Especifica o processo a ser conectado quando o comando Anexar é executado ou o processo em um rastreamento a ser analisado quando o comando Analisar é executado. Aplica-se aos comandos Anexar e Analisar.|A PID ou o nome do processo.|nenhuma.|  
|Config|Especifica o caminho do arquivo de configuração, se você quiser configurações de coleta diferentes das configurações padrão.   Aplica-se aos comandos Inicializar, Anexar e Analisar.|O caminho do diretório ou relativo do arquivo de configuração XML.|nenhuma.|  

## <a name="customize-configuration-settings"></a>Personalizar configurações  
 Se você usar CVCollectionCmd para coletar rastreamentos e quiser personalizar as configurações de coleta, use um arquivo de configuração para especificá-las.  

> [!NOTE]
>  Ao usar o Visual Studio para coletar rastreamentos, não modifique diretamente o arquivo de configuração.  Em vez disso, use a caixa de diálogo [Configurações Avançadas](../profiling/advanced-settings-dialog-box-concurrency-visualizer.md) para modificar as configurações.  

 Para modificar configurações de coleta, crie um arquivo de configuração no computador em que o utilitário CVCollectionCmd será executado. É possível criar o arquivo de configuração do zero ou copiá-lo no computador com o Visual Studio instalado e modificar isso. O arquivo se chama *UserConfig.xml* e está localizado na pasta *AppData Local*. Ao executar o utilitário, use a opção Config com o comando Inicializar, Anexar ou Analisar.  No parâmetro associado à opção Config, especifique o caminho do arquivo de configuração.  

### <a name="configuration-file-tags"></a>Marcas de arquivo de configuração  
 O arquivo de configuração se baseia em XML. Seguem as marcas e os valores válidos:  


| Marca | Descrição | Valores |
|-------------------------| - | - |
| Config | Demarca o arquivo de configuração geral. | Deve conter estes elementos:<br /><br /> –   MinorVersion<br />–   MajorVersion |
| MajorVersion | Especifica a versão principal do arquivo de configuração. | Deve ser 1 para projetos do [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)]. Se não for 1, o utilitário não funcionará. |
| MinorVersion | Especifica a versão secundária do arquivo de configuração. | Deve ser 0 para projetos do [!INCLUDE[vs_dev11_long](../data-tools/includes/vs_dev11_long_md.md)]. Se não for 0, o utilitário não funcionará. |
| IncludeEnvSymbolPath | Define um valor que determina se o caminho do símbolo de ambiente (_NT_SYMBOL_PATH) é usado. | -   Verdadeiro<br />-   Falso |
| DeleteEtlsAfterAnalysis | Define um valor que determina se os arquivos ETL são excluídos quando a análise é concluída. | -   Verdadeiro<br />-   Falso |
| SymbolPath | Especifica o caminho do servidor de símbolos. Para obter mais informações, consulte [Use the Microsoft Symbol Server to obtain debug symbol files (Usar o Servidor de Símbolos da Microsoft para obter arquivos de símbolo de depuração)](http://go.microsoft.com/fwlink/?LinkID=149389). | Um nome ou uma URL do diretório. |
| Marcadores | Contém a lista de provedores de marcadores. | Pode conter zero ou mais elementos MarkerProvider. |
| MarkerProvider | Especifica um único provedor de marcadores. | Deve conter estes elementos:<br /><br /> –   Nível<br />–   GUID<br />–   Nome<br /><br /> Pode conter estes elementos:<br /><br /> –   Categories<br />–   IsEnabled |
| Nível | Define o nível de importância de um MarkerProvider. | –   Baixa<br />–   Normal<br />–   Alta<br />–   Crítica<br />–   Todas |
| Guid | O identificador global exclusivo do provedor de marcadores ETW. | Uma GUID. |
| Nome | Especifica a descrição do provedor de marcadores. | Uma cadeia de caracteres. |
| Categorias | Especifica as categorias coletadas para o provedor de marcadores. | Uma cadeia de caracteres delimitada por vírgula de números ou intervalos de números. |
| IsEnabled | Define um valor que determina se o provedor de marcadores está habilitado para a coleção. | -   Verdadeiro<br />-   Falso |
| FilterConfig | Especifica a lista de opções de configuração dos eventos ETW filtrados da coleção. | Pode conter estes elementos:<br /><br /> -   CollectClrEvents<br />-   ClrCollectionOptions<br />-   CollectSampleEvents<br />-   CollectGpuEvents<br />-   CollectFileIO |
| CollectClrEvents | Define um valor que determina se os eventos do CLR serão coletados. | -   Verdadeiro<br />-   Falso |
| ClrCollectionOptions | Especifica se é necessário coletar eventos do CLR para aplicativos nativos e se é necessário coletar eventos de encerramento do NGEN. | Pode conter um, ambos ou nenhum destes valores:<br /><br /> -   CollectForNative<br />-   DisableNGenRundown |
| CollectSampleEvents | Define um valor que determina se os eventos de exemplo serão coletados. | -   Verdadeiro<br />-   Falso |
| CollectGpuEvents | Define um valor que determina se os eventos gerados por DX serão coletados. | -   Verdadeiro<br />-   Falso |
| CollectFileIO | Define um valor que determina se os eventos de E/S do arquivo serão coletados. | -   Verdadeiro<br />-   Falso |
| UserBufferSettings | Especifica a lista de parâmetros de configurações de buffer do usuário. | Deve conter estes elementos:<br /><br /> –   BufferFlushTimer<br />–   BufferSize<br />–   MinimumBuffers<br />–   MaximumBuffers |
| KernelBufferSettings | Especifica a lista de parâmetros de configurações de buffer do kernel. | Deve conter estes elementos:<br /><br /> –   BufferFlushTimer<br />–   BufferSize<br />–   MinimumBuffers<br />–   MaximumBuffers |
| BufferFlushTimer | Especifica o temporizador de liberação dos buffers ETW. | Um número inteiro positivo. |
| BufferSize | Quantidade de memória alocada para cada buffer de sessão de rastreamento do evento, em quilobytes. | Um número de 0 a 1.024. |
| MinimumBuffers | O número mínimo de buffers alocados para o pool de buffers da sessão de rastreamento do evento. | Um número inteiro positivo maior ou igual a duas vezes o número de núcleos lógicos. |
| MaximumBuffers | O número máximo de buffers alocados para o pool de buffers da sessão de rastreamento do evento. | Um número maior ou igual a MinimumBuffers. |
| JustMyCode | Especifica a lista de diretórios Habilitar Apenas Meu Código. | Uma lista de zero ou mais elementos MyCodeDirectory. |
| MyCodeDirectory | Especifica um diretório que contém o código. | Um caminho absoluto. |

### <a name="example"></a>Exemplo  
 Em vez de criar um arquivo de configuração desde o início, é possível copiar o exemplo a seguir e modificá-lo para atender aos requisitos.  

```xml  
<?xml version="1.0"?>  
<LocalConfig xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" MajorVersion="1" MinorVersion="0">  

  <IncludeEnvSymbolPath>true</IncludeEnvSymbolPath>  

  <DeleteEtlsAfterAnalysis>true</DeleteEtlsAfterAnalysis>  

  <TraceLocation>C:\traces</TraceLocation>  

  <SymbolPath>http://symweb</SymbolPath>  

  <Markers>  
    <MarkerProvider Name="Default" Guid="8d4925ab-505a-483b-a7e0-6f824a07a6f0" Level="Low" />  
    <MarkerProvider Name="TPL" Guid="2e5dba47-a3d2-4d16-8ee0-6671ffdcd7b5" Level="Normal" />  
    <MarkerProvider Name="TPL Dataflow" Guid="16f53577-e41d-43d4-b47e-c17025bf4025" Level="Normal" />  
    <MarkerProvider Name="TPL Synchronization" Guid="ec631d38-466b-4290-9306-834971ba0217" Level="Normal" />  
    <MarkerProvider Name="PLINQ" Guid="159eeeec-4a14-4418-a8fe-faabcd987887" Level="Normal" />  
    <MarkerProvider Name="Concurrency Runtime" Guid="f7b697a3-4db5-4d3b-be71-c4d284e6592f" Level="Normal" />  
    <MarkerProvider Name="Scenario Markers" Guid="fb9244c9-f23a-4966-8a9c-97a51f8c355b" Level="Low" />  

    <!-- The IsEnabled and Categories elements are optional -->  
    <MarkerProvider Name="myMarker1" Guid="d0dbb3a3-895c-4ce6-96d9-28f69d664dc3" Level="Critical" IsEnabled="false" Categories="0,1,3-5,8" />  
    <MarkerProvider Name="myMarker2" Guid="03452127-a617-4302-9e30-c0d10442e4ee" Level="Low" IsEnabled="false" Categories="0,1,3-5,8-10,11-13" />  
  </Markers>  

  <FilterConfig>  
    <CollectClrEvents>true</CollectClrEvents>  
    <ClrCollectionOptions>CollectForNative DisableNGenRundown</ClrCollectionOptions>  
    <CollectSampleEvents>true</CollectSampleEvents>  
    <CollectGpuEvents>true</CollectGpuEvents>  
    <CollectFileIO>true</CollectFileIO>  
  </FilterConfig>  

  <UserBufferSettings>  
    <BufferFlushTimer>0</BufferFlushTimer>  
    <BufferSize>256</BufferSize>  
    <MinimumBuffers>512</MinimumBuffers>  
    <MaximumBuffers>1024</MaximumBuffers>  
  </UserBufferSettings>  

  <KernelBufferSettings>  
    <BufferFlushTimer>0</BufferFlushTimer>  
    <BufferSize>256</BufferSize>  
    <MinimumBuffers>512</MinimumBuffers>  
    <MaximumBuffers>1024</MaximumBuffers>  
  </KernelBufferSettings>  

  <!-- List of MyCodeDirectory directories -->  
  <JustMyCode>  
    <MyCodeDirectory>C:\myBinaries1</MyCodeDirectory>  
    <MyCodeDirectory>C:\myBinaries2</MyCodeDirectory>  
  </JustMyCode>  
</LocalConfig>  

```
