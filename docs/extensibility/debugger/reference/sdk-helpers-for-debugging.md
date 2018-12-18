---
title: Auxiliares do SDK para depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: d352e22b95540cfc1901eb214c2d5180b6024f27
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49821520"
---
# <a name="sdk-helpers-for-debugging"></a>Auxiliares do SDK para depuração
Essas funções e as declarações são funções auxiliares global para implementação de mecanismos de depuração, avaliadores de expressão e provedores de símbolo em C++.  
  
> [!NOTE]
>  Não há nenhum versões gerenciadas dessas funções e declarações neste momento.  
  
## <a name="overview"></a>Visão geral  
 Para que os mecanismos de depuração, avaliadores de expressão e provedores de símbolo a ser usado pelo Visual Studio, eles devem ser registrados. Isso é feito definindo sub-chaves de registro e entradas, também conhecidas como "métricas de configuração". As seguintes funções globais são criadas para facilitar o processo de atualizar essas métricas. Consulte a seção sobre locais do registro para descobrir o layout de cada subchave de registro é atualizado por essas funções.  
  
## <a name="general-metric-functions"></a>Funções de métrica gerais  
 Essas são funções gerais usadas pelos mecanismos de depuração. Funções especializadas em avaliadores de expressão e provedores de símbolo são detalhados posteriormente.  
  
### <a name="getmetric-method"></a>Método GetMetric  
 Recupera um valor de métrica do registro.  
  
```cpp  
HRESULT GetMetric(  
   LPCWSTR pszMachine,  
   LPCWSTR pszType,  
   REFGUID guidSection,  
   LPCWSTR pszMetric,  
   DWORD * pdwValue,  
   LPCWSTR pszAltRoot  
);  
```  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|pszMachine|[in] Nome de uma máquina remota, possivelmente, cujo registro será gravado (`NULL` significa que o computador local).|  
|pszType|[in] Um dos tipos de métrica.|  
|guidSection|[in] GUID de um mecanismo específico do avaliador, exceção, etc. Especifica uma subseção de um tipo de métrica para um elemento específico.|  
|pszMetric|[in] A métrica a ser obtida. Isso corresponde ao nome de um valor específico.|  
|pdwValue|[in] O local de armazenamento do valor da métrica. Há vários tipos de GetMetric que pode retornar um DWORD (como neste exemplo), um BSTR, um GUID ou uma matriz de GUIDs.|  
|pszAltRoot|[in] Uma raiz do registro alternativo para usar. Definido como `NULL` para usar o padrão.|  
  
### <a name="setmetric-method"></a>Método SetMetric  
 Define o valor da métrica especificado no registro.  
  
```cpp  
HRESULT SetMetric(  
         LPCWSTR pszType,  
         REFGUID guidSection,  
         LPCWSTR pszMetric,  
   const DWORD   dwValue,  
         bool    fUserSpecific,  
         LPCWSTR pszAltRoot  
);  
```  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|pszType|[in] Um dos tipos de métrica.|  
|guidSection|[in] GUID de um mecanismo específico do avaliador, exceção, etc. Especifica uma subseção de um tipo de métrica para um elemento específico.|  
|pszMetric|[in] A métrica a ser obtida. Isso corresponde ao nome de um valor específico.|  
|dwValue|[in] O local de armazenamento do valor na métrica. Há vários tipos de SetMetric que pode armazenar um DWORD (no exemplo), um BSTR, um GUID ou uma matriz de GUIDs.|  
|fUserSpecific|[in] TRUE se a métrica é específico do usuário e se ele deve ser escrito para o hive do usuário em vez do hive do computador local.|  
|pszAltRoot|[in] Uma raiz do registro alternativo para usar. Definido como `NULL` para usar o padrão.|  
  
### <a name="removemetric-method"></a>Método RemoveMetric  
 Remove a métrica especificada do registro.  
  
```cpp  
HRESULT RemoveMetric(  
   LPCWSTR pszType,  
   REFGUID guidSection,  
   LPCWSTR pszMetric,  
   LPCWSTR pszAltRoot  
);  
```  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|pszType|[in] Um dos tipos de métrica.|  
|guidSection|[in] GUID de um mecanismo específico do avaliador, exceção, etc. Especifica uma subseção de um tipo de métrica para um elemento específico.|  
|pszMetric|[in] A métrica a ser removido. Isso corresponde ao nome de um valor específico.|  
|pszAltRoot|[in] Uma raiz do registro alternativo para usar. Definido como `NULL` para usar o padrão.|  
  
### <a name="enummetricsections-method"></a>Método EnumMetricSections  
 Enumera as várias seções de métrica no registro.  
  
```cpp  
HRESULT EnumMetricSections(  
   LPCWSTR pszMachine,  
   LPCWSTR pszType,  
   GUID *  rgguidSections,  
   DWORD * pdwSize,  
   LPCWSTR pszAltRoot  
);  
```  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|pszMachine|[in] Nome de uma máquina remota, possivelmente, cujo registro será gravado (`NULL` significa que o computador local).|  
|pszType|[in] Um dos tipos de métrica.|  
|rgguidSections|[no, out] Matriz pré-alocado de GUIDs a serem preenchidos.|  
|pdwSize|[in] O número máximo de GUIDs que podem ser armazenadas em do `rgguidSections` matriz.|  
|pszAltRoot|[in] Uma raiz do registro alternativo para usar. Definido como `NULL` para usar o padrão.|  
  
## <a name="expression-evaluator-functions"></a>Funções do avaliador de expressão  
  
|Função|Descrição|  
|--------------|-----------------|  
|GetEEMetric|Recupera um valor de métrica do registro.|  
|SetEEMetric|Define o valor da métrica especificado no registro.|  
|RemoveEEMetric|Remove a métrica especificada do registro.|  
|GetEEMetricFile|Obtém um nome de arquivo da métrica especificada e o carrega, retornando o conteúdo do arquivo como uma cadeia de caracteres.|  
  
## <a name="exception-functions"></a>Funções de exceção  
  
|Função|Descrição|  
|--------------|-----------------|  
|GetExceptionMetric|Recupera um valor de métrica do registro.|  
|SetExceptionMetric|Define o valor da métrica especificado no registro.|  
|RemoveExceptionMetric|Remove a métrica especificada do registro.|  
|RemoveAllExceptionMetrics|Remove todas as métricas de exceção do registro.|  
  
## <a name="symbol-provider-functions"></a>Funções de símbolo do provedor  
  
|Função|Descrição|  
|--------------|-----------------|  
|GetSPMetric|Recupera um valor de métrica do registro.|  
|SetSPMetric|Define o valor da métrica especificado no registro.|  
|RemoveSPMetric|Remove a métrica especificada do registro.|  
  
## <a name="enumeration-functions"></a>Funções de enumeração  
  
|Função|Descrição|  
|--------------|-----------------|  
|EnumMetricSections|Enumera todas as métricas para um tipo de métrica especificada.|  
|EnumDebugEngine|Enumera os mecanismos de depuração registrado.|  
|EnumEEs|Enumera os avaliadores de expressão registrado.|  
|EnumExceptionMetrics|Enumera todas as métricas de exceção.|  
  
## <a name="metric-definitions"></a>Definições de métrica  
 Essas definições podem ser usadas para nomes de métrica predefinidos. Os nomes correspondem aos nomes de valor e várias chaves de registro e estão todas definidas como cadeias de caracteres largos: por exemplo, `extern LPCWSTR metrictypeEngine`.  
  
|Tipos predefinidos de métrica|Descrição: A chave de base para...|  
|-----------------------------|---------------------------------------|  
|metrictypeEngine|Todas as métricas do mecanismo de depuração.|  
|metrictypePortSupplier|Todas as métricas de fornecedor de porta.|  
|metrictypeException|Todas as métricas de exceção.|  
|metricttypeEEExtension|Todas as extensões do avaliador de expressão.|  
  
|Propriedades do mecanismo de depuração|Descrição|  
|-----------------------------|-----------------|  
|metricAddressBP|Definida como diferente de zero para indicar o suporte para pontos de interrupção de endereço.|  
|metricAlwaysLoadLocal|Definida como diferente de zero para sempre carregar localmente o mecanismo de depuração.|  
|metricLoadInDebuggeeSession|NÃO USADO|  
|metricLoadedByDebuggee|Definida como diferente de zero para indicar que o mecanismo de depuração sempre será carregado com ou pelo programa que está sendo depurado.|  
|metricAttach|Definida como diferente de zero para indicar o suporte para o anexo a programas existentes.|  
|metricCallStackBP|Definida como diferente de zero para indicar o suporte para pontos de interrupção de pilha de chamada.|  
|metricConditionalBP|Definida como diferente de zero para indicar o suporte para a configuração de pontos de interrupção condicionais.|  
|metricDataBP|Definida como diferente de zero para indicar o suporte para a configuração de pontos de interrupção em alterações nos dados.|  
|metricDisassembly|Definido como não zero para indicar o suporte para a produção de uma listagem de desmontagem.|  
|metricDumpWriting|Definida como diferente de zero para indicar o suporte para despejo de gravação (o despejo de memória para um dispositivo de saída).|  
|metricENC|Definido como não zero para indicar o suporte para editar e continuar. **Observação:** nunca deve definir isso de um mecanismo de depuração personalizado ou deve sempre será definido como 0.|  
|metricExceptions|Definida como diferente de zero para indicar o suporte para exceções.|  
|metricFunctionBP|Definida como diferente de zero para indicar o suporte para pontos de interrupção nomeados (os pontos de interrupção que param quando um determinado nome de função é chamado).|  
|metricHitCountBP|Definida como diferente de zero para indicar o suporte para a configuração de pontos de interrupção "de acertos do ponto" (pontos de interrupção que são disparados somente depois que está sendo atingido um determinado número de vezes).|  
|metricJITDebug|Definido como não zero para indicar o suporte para depuração de just-in-time (o depurador é iniciado quando ocorre uma exceção em um processo em execução).|  
|metricMemory|NÃO USADO|  
|metricPortSupplier|Defina isso para o CLSID do fornecedor de porta, se uma estiver implementada.|  
|metricRegisters|NÃO USADO|  
|metricSetNextStatement|Definida como diferente de zero para indicar o suporte para definir a próxima instrução (que ignora a execução de instruções intermediárias).|  
|metricSuspendThread|Definida como diferente de zero para indicar o suporte para suspender a execução do thread.|  
|metricWarnIfNoSymbols|Definida como diferente de zero para indicar que o usuário será notificado se não houver nenhum símbolo.|  
|metricProgramProvider|Defina isso para o CLSID do provedor do programa.|  
|metricAlwaysLoadProgramProviderLocal|Defina isso como não zero para indicar que o provedor de programa seria sempre carregado localmente.|  
|metricEngineCanWatchProcess|Defina isso como diferente de zero para indicar que o mecanismo de depuração irá observar para processar eventos em vez do provedor do programa.|  
|metricRemoteDebugging|Defina isso como diferente de zero para indicar o suporte para depuração remota.|  
|metricEncUseNativeBuilder|Defina isso como não zero para indicar que o editar e continuar Manager devem usar encbuild.dll do mecanismo de depuração para compilar para editar e continuar. **Observação:** nunca deve definir isso de um mecanismo de depuração personalizado ou deve sempre será definido como 0.|  
|metricLoadUnderWOW64|Defina isso como diferente de zero para indicar que o mecanismo de depuração deve ser carregado no processo a ser depurado em WOW, ao depurar um processo de 64 bits; Caso contrário, o mecanismo de depuração será carregado no processo do Visual Studio (que está em execução no WOW64).|  
|metricLoadProgramProviderUnderWOW64|Defina isso como diferente de zero para indicar que o provedor do programa deve ser carregado do processo de depuração ao depurar um processo de 64 bits em WOW; Caso contrário, ele será carregado no processo do Visual Studio.|  
|metricStopOnExceptionCrossingManagedBoundary|Defina isso como diferente de zero para indicar que o processo deve ser interrompida se uma exceção não tratada é lançada em limites de código gerenciados/não gerenciados.|  
|metricAutoSelectPriority|Defina isso como uma prioridade para seleção automática do mecanismo de depuração (maior valores é igual a prioridade mais alta).|  
|metricAutoSelectIncompatibleList|Chave do registro que contém entradas que especificam os GUIDs para mecanismos de depuração a serem ignorados na seleção automática. Essas entradas são um número (0, 1, 2 e assim por diante) com um GUID, expressado como uma cadeia de caracteres.|  
|metricIncompatibleList|Chave do registro que contém entradas que especificam os GUIDs para mecanismos de depuração que são incompatíveis com este mecanismo de depuração.|  
|metricDisableJITOptimization|Defina isso como diferente de zero para indicar que as otimizações de just-in-time (para código gerenciado) devem ser desabilitadas durante a depuração.|  
  
|Propriedades do avaliador de expressão|Descrição|  
|-------------------------------------|-----------------|  
|metricEngine|Isso mantém o número de mecanismos de depuração que suportam o avaliador de expressão especificada.|  
|metricPreloadModules|Defina isso como diferente de zero para indicar que os módulos devem ser pré-carregado quando um avaliador de expressão é iniciado em relação a um programa.|  
|metricThisObjectName|Defina isso para o nome do objeto "this".|  
  
|Propriedades de extensão do avaliador de expressão|Descrição|  
| - |-----------------|  
|metricExtensionDll|Nome da dll que oferece suporte a essa extensão.|  
|metricExtensionRegistersSupported|Lista de registros com suporte.|  
|metricExtensionRegistersEntryPoint|Ponto de entrada para acessar os registros.|  
|metricExtensionTypesSupported|Lista de tipos com suporte.|  
|metricExtensionTypesEntryPoint|Ponto de entrada para acessar tipos.|  
  
|Propriedades da porta de fornecedor|Descrição|  
|------------------------------|-----------------|  
|metricPortPickerCLSID|O CLSID do seletor de porta (uma caixa de diálogo, o usuário pode usar para selecionar as portas e adicionar portas a serem usadas para depuração).|  
|metricDisallowUserEnteredPorts|Diferente de zero se as portas inserido pelo usuário não podem ser adicionadas para o fornecedor de porta (Isso torna a caixa de diálogo do seletor de porta essencialmente somente leitura).|  
|metricPidBase|A ID de processo base usada pelo fornecedor de porta ao alocar identificadores de processo.|  
  
|Tipos de Store de SP predefinidos|Descrição|  
|-------------------------------|-----------------|  
|storetypeFile|Os símbolos são armazenados em um arquivo separado.|  
|storetypeMetadata|Os símbolos são armazenados como metadados em um assembly.|  
  
|Diversas propriedades|Descrição|  
|------------------------------|-----------------|  
|metricShowNonUserCode|Defina isso para mostrar o código de nonuser diferente de zero.|  
|metricJustMyCodeStepping|Defina isso como diferente de zero para indicar que a revisão pode ocorrer apenas no código do usuário.|  
|metricCLSID|CLSID para um objeto de um tipo específico de métrica.|  
|MetricName|Nome amigável para um objeto de um tipo específico de métrica.|  
|metricLanguage|Nome do idioma.|  
  
## <a name="registry-locations"></a>Locais do registro  
 As métricas são lida e gravadas no registro, especificamente o `VisualStudio` subchave.  
  
> [!NOTE]
>  Na maioria das vezes, as métricas serão gravadas na chave HKEY_LOCAL_MACHINE. No entanto, às vezes, HKEY_CURRENT_USER será a chave de destino. Dbgmetric.lib lida com as duas chaves. Ao obter uma métrica, ele pesquisa HKEY_CURRENT_USER primeiro e, em seguida, HKEY_LOCAL_MACHINE. Quando ele é definir uma métrica, um parâmetro especifica qual chave de nível superior para usar.  
  
 *[chave do Registro]*\  
  
 `Software`\  
  
 `Microsoft`\  
  
 `VisualStudio`\  
  
 *[raiz de versão]*\  
  
 *[métrica root]*\  
  
 *[tipo de métrica]*\  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[chave do Registro]*|`HKEY_CURRENT_USER` ou `HKEY_LOCAL_MACHINE`.|  
|*[raiz de versão]*|A versão do Visual Studio (por exemplo, `7.0`, `7.1`, ou `8.0`). No entanto, essa raiz também pode ser modificado usando o **/rootsuffix** alternar para o **devenv.exe**. Para VSIP, esse modificador é normalmente **Exp**, portanto, a raiz da versão seria, por exemplo, 8.0Exp.|  
|*[métrica root]*|Isso ocorre `AD7Metrics` ou `AD7Metrics(Debug)`, dependendo se a versão de depuração de dbgmetric.lib é usada. **Observação:** se dbgmetric.lib for usada, essa convenção de nomenclatura deverão ser seguida se você tiver diferenças entre depuração e versão versões que devem ser refletidas no registro.|  
|*[tipo de métrica]*|O tipo de métrica a ser gravado: `Engine`, `ExpressionEvaluator`, `SymbolProvider`, etc. Eles são definidos como no dbgmetric.h como `metricTypeXXXX`, onde `XXXX` é o nome de tipo específico.|  
|*[métrica]*|O nome de uma entrada a ser atribuído um valor para definir a métrica. A organização real das métricas depende o tipo de métrica.|  
|*[valor de métrica]*|O valor atribuído para a métrica. O tipo que o valor deve ter (cadeia de caracteres), números, etc. depende a métrica.|  
  
> [!NOTE]
>  Todos os GUIDs são armazenados no formato de `{GUID}`. Por exemplo, `{123D150B-FA18-461C-B218-45B3E4589F9B}`.  
  
### <a name="debug-engines"></a>Mecanismos de depuração  
 A seguir está a organização das métricas de mecanismos de depuração no registro. `Engine` é o nome do tipo de métrica para um mecanismo de depuração e corresponde a *[tipo de métrica]* na subárvore de registro acima.  
  
 `Engine`\  
  
 *[mecanismo guid]*\  
  
 `CLSID` = *[guid de classe]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 `PortSupplier`\  
  
 `0` = *[guid do fornecedor de porta]*  
  
 `1` = *[guid do fornecedor de porta]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[mecanismo guid]*|O GUID do mecanismo de depuração.|  
|*[guid de classe]*|O GUID da classe que implementa este mecanismo de depuração.|  
|*[guid do fornecedor de porta]*|O GUID do fornecedor de porta, se houver. Muitos mecanismos de depuração usam o fornecedor de porta padrão e, portanto, não especificam seu próprio fornecedor. Nesse caso, a subchave `PortSupplier` estará ausente.|  
  
### <a name="port-suppliers"></a>Fornecedores de porta  
 A seguir está a organização das métricas de fornecedor de porta no registro. `PortSupplier` é o nome do tipo de métrica para um fornecedor de porta e corresponde a *[tipo de métrica]*.  
  
 `PortSupplier`\  
  
 *[guid do fornecedor de porta]*\  
  
 `CLSID` = *[guid de classe]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[guid do fornecedor de porta]*|O GUID do fornecedor de porta|  
|*[guid de classe]*|O GUID da classe que implementa esse fornecedor de porta|  
  
### <a name="symbol-providers"></a>Provedores de símbolo  
 A seguir está a organização das métricas de fornecedor de símbolo no registro. `SymbolProvider` é o nome do tipo de métrica para o provedor de símbolo e corresponde ao *[tipo de métrica]*.  
  
 `SymbolProvider`\  
  
 *[guid do provedor de símbolo]*\  
  
 `file`\  
  
 `CLSID` = *[guid de classe]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 `metadata`\  
  
 `CLSID` = *[guid de classe]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[guid do provedor de símbolo]*|O GUID do provedor de símbolo|  
|*[guid de classe]*|O GUID da classe que implementa esse provedor de símbolo|  
  
### <a name="expression-evaluators"></a>Avaliadores de expressão  
 A seguir está a organização das métricas do avaliador de expressão no registro. `ExpressionEvaluator` é o nome do tipo de métrica para o avaliador de expressão e corresponde a *[tipo de métrica]*.  
  
> [!NOTE]
>  O tipo de métrica para `ExpressionEvaluator` não está definido no dbgmetric.h, pois ele é considerado que todas as alterações de métricas para os avaliadores de expressão percorrer as funções de métrica de avaliador de expressão apropriada (o layout do `ExpressionEvaluator` subchave é um pouco complicado, portanto, os detalhes estão ocultos dentro de dbgmetric.lib).  
  
 `ExpressionEvaluator`\  
  
 *[guid do idioma]*\  
  
 *[guid do fornecedor]*\  
  
 `CLSID` = *[guid de classe]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 `Engine`\  
  
 `0` = *[guid do mecanismo de depuração]*  
  
 `1` = *[guid do mecanismo de depuração]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[guid do idioma]*|O GUID de um idioma|  
|*[guid do fornecedor]*|O GUID de um fornecedor|  
|*[guid de classe]*|O GUID da classe que implementa essa avaliador de expressão|  
|*[guid do mecanismo de depuração]*|O GUID de um mecanismo de depuração que este avaliador de expressão funciona com|  
  
### <a name="expression-evaluator-extensions"></a>Extensões do avaliador de expressão  
 A seguir está a organização das métricas de extensão do avaliador de expressão no registro. `EEExtensions` é o nome de tipo de métrica para a expressão de extensões do avaliador e corresponde ao *[tipo de métrica]*.  
  
 `EEExtensions`\  
  
 *[extensão guid]*\  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[extensão guid]*|O GUID de uma extensão do avaliador de expressão|  
  
### <a name="exceptions"></a>Exceções  
 A seguir está a organização das métricas de exceções no registro. `Exception` é o nome do tipo de métrica para as exceções e corresponde ao *[tipo de métrica]*.  
  
 `Exception`\  
  
 *[guid do mecanismo de depuração]*\  
  
 *[tipos de exceção]*\  
  
 *[exceção]*\  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
 *[exceção]*\  
  
 *[métrica] = [valor de métrica]*  
  
 *[métrica] = [valor de métrica]*  
  
|Espaço reservado|Descrição|  
|-----------------|-----------------|  
|*[guid do mecanismo de depuração]*|O GUID de um mecanismo de depuração que dá suporte a exceções.|  
|*[tipos de exceção]*|Um título geral para a subchave identifica a classe de exceções que podem ser manipulados. São nomes típicos **exceções do C++**, **exceções Win32**, **exceções do Common Language Runtime**, e **verificações de tempo de execução nativo**. Esses nomes também são usados para identificar uma determinada classe de exceção para o usuário.|  
|*[exceção]*|Um nome para uma exceção: por exemplo, **com_error** ou **Control-Break**. Esses nomes também são usados para identificar uma exceção específica ao usuário.|  
  
## <a name="requirements"></a>Requisitos  
 Esses arquivos estão localizados na [!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)] diretório de instalação do SDK (por padrão, *[unidade]* \Program Files\Microsoft SDK do Visual Studio 2010\\).  
  
 Cabeçalho: includes\dbgmetric.h  
  
 Biblioteca: libs\ad2de.lib, libs\dbgmetric.lib  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)