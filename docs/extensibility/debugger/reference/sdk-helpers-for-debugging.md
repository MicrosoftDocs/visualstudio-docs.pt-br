---
title: Auxiliares do SDK para depuração | Microsoft Docs
description: Saiba mais sobre as funções e declarações que são funções auxiliares globais para implementar mecanismos de depuração, avaliadores de expressão e provedores de símbolo em C++.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- dbgmetric.lib
- registry, Debugging SDK
- Debugging SDK, registry locations
- dbgmetric.h
- metrics [Debugging SDK]
ms.assetid: 80a52e93-4a04-4ab2-8adc-a7847c2dc20b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4f5a34513130ea112393ffbb4935093bcea6e797
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105061531"
---
# <a name="sdk-helpers-for-debugging"></a>Auxiliares do SDK para depuração
Essas funções e declarações são funções auxiliares globais para implementar mecanismos de depuração, avaliadores de expressão e provedores de símbolo em C++.

> [!NOTE]
> Não há versões gerenciadas dessas funções e declarações no momento.

## <a name="overview"></a>Visão geral
 Para que os mecanismos de depuração, avaliadores de expressão e provedores de símbolo sejam usados pelo Visual Studio, eles devem ser registrados. Isso é feito definindo-se as subchaves e entradas do registro, caso contrário, conhecidas como "métricas de configuração". As funções globais a seguir foram projetadas para facilitar o processo de atualização dessas métricas. Consulte a seção sobre locais de registro para descobrir o layout de cada subchave do registro que é atualizada por essas funções.

## <a name="general-metric-functions"></a>Funções de métrica geral
 Essas são funções gerais usadas pelos mecanismos de depuração. Funções especializadas para avaliadores de expressão e provedores de símbolo são detalhadas mais tarde.

### <a name="getmetric-method"></a>Método getmetric
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
|pszMachine|no Nome de um computador possivelmente remoto cujo registro será gravado ( `NULL` significa máquina local).|
|pszType|no Um dos tipos de métrica.|
|guidSection|no GUID de um mecanismo específico, avaliador, exceção, etc. Isso especifica uma subseção em um tipo de métrica para um elemento específico.|
|pszMetric|no A métrica a ser obtida. Isso corresponde a um nome de valor específico.|
|pdwValue|no O local de armazenamento do valor da métrica. Há vários tipos de getmetric que podem retornar um DWORD (como neste exemplo), um BSTR, um GUID ou uma matriz de GUIDs.|
|pszAltRoot|no Uma raiz de registro alternativa a ser usada. Defina como `NULL` para usar o padrão.|

### <a name="setmetric-method"></a>Método SETMETRIC
 Define o valor de métrica especificado no registro.

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
|pszType|no Um dos tipos de métrica.|
|guidSection|no GUID de um mecanismo específico, avaliador, exceção, etc. Isso especifica uma subseção em um tipo de métrica para um elemento específico.|
|pszMetric|no A métrica a ser obtida. Isso corresponde a um nome de valor específico.|
|dwValue|no O local de armazenamento do valor na métrica. Há vários tipos de SETMETRIC que podem armazenar um DWORD (neste exemplo), um BSTR, um GUID ou uma matriz de GUIDs.|
|fUserSpecific|no TRUE se a métrica for específica do usuário e se ela deve ser gravada no hive do usuário em vez do hive do computador local.|
|pszAltRoot|no Uma raiz de registro alternativa a ser usada. Defina como `NULL` para usar o padrão.|

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
|pszType|no Um dos tipos de métrica.|
|guidSection|no GUID de um mecanismo específico, avaliador, exceção, etc. Isso especifica uma subseção em um tipo de métrica para um elemento específico.|
|pszMetric|no A métrica a ser removida. Isso corresponde a um nome de valor específico.|
|pszAltRoot|no Uma raiz de registro alternativa a ser usada. Defina como `NULL` para usar o padrão.|

### <a name="enummetricsections-method"></a>Método EnumMetricSections
 Enumera as várias seções de métricas no registro.

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
|pszMachine|no Nome de um computador possivelmente remoto cujo registro será gravado ( `NULL` significa máquina local).|
|pszType|no Um dos tipos de métrica.|
|rgguidSections|[entrada, saída] Matriz prealocada de GUIDs a ser preenchida.|
|pdwSize|no O número máximo de GUIDs que podem ser armazenados na `rgguidSections` matriz.|
|pszAltRoot|no Uma raiz de registro alternativa a ser usada. Defina como `NULL` para usar o padrão.|

## <a name="expression-evaluator-functions"></a>Funções do avaliador de expressão

|Função|Descrição|
|--------------|-----------------|
|GetEEMetric|Recupera um valor de métrica do registro.|
|SetEEMetric|Define o valor de métrica especificado no registro.|
|RemoveEEMetric|Remove a métrica especificada do registro.|
|GetEEMetricFile|Obtém um nome de arquivo da métrica especificada e o carrega, retornando o conteúdo do arquivo como uma cadeia de caracteres.|

## <a name="exception-functions"></a>Funções de exceção

|Função|Descrição|
|--------------|-----------------|
|GetExceptionMetric|Recupera um valor de métrica do registro.|
|SetExceptionMetric|Define o valor de métrica especificado no registro.|
|RemoveExceptionMetric|Remove a métrica especificada do registro.|
|RemoveAllExceptionMetrics|Remove todas as métricas de exceção do registro.|

## <a name="symbol-provider-functions"></a>Funções de provedor de símbolo

|Função|Descrição|
|--------------|-----------------|
|GetSPMetric|Recupera um valor de métrica do registro.|
|SetSPMetric|Define o valor de métrica especificado no registro.|
|RemoveSPMetric|Remove a métrica especificada do registro.|

## <a name="enumeration-functions"></a>Funções de enumeração

|Função|Descrição|
|--------------|-----------------|
|EnumMetricSections|Enumera todas as métricas para um tipo de métrica especificado.|
|EnumDebugEngine|Enumera os mecanismos de depuração registrados.|
|EnumEEs|Enumera os avaliadores de expressão registrados.|
|EnumExceptionMetrics|Enumera todas as métricas de exceção.|

## <a name="metric-definitions"></a>Definições de métrica
 Essas definições podem ser usadas para nomes de métrica predefinidos. Os nomes correspondem a várias chaves do registro e nomes de valor e são definidos como cadeias de caracteres largos: por exemplo, `extern LPCWSTR metrictypeEngine` .

|Tipos de métrica predefinidos|Descrição: a chave de base para...|
|-----------------------------|---------------------------------------|
|metrictypeEngine|Todas as métricas do mecanismo de depuração.|
|metrictypePortSupplier|Todas as métricas de fornecedor de porta.|
|metrictypeException|Todas as métricas de exceção.|
|metricttypeEEExtension|Todas as extensões do avaliador de expressão.|

|Propriedades do mecanismo de depuração|Descrição|
|-----------------------------|-----------------|
|metricAddressBP|Defina como diferente de zero para indicar suporte para pontos de interrupção de endereço.|
|metricAlwaysLoadLocal|Defina como diferente de zero para sempre carregar o mecanismo de depuração localmente.|
|metricLoadInDebuggeeSession|NÃO USADO|
|metricLoadedByDebuggee|Defina como diferente de zero para indicar que o mecanismo de depuração sempre será carregado com ou pelo programa que está sendo depurado.|
|metricAttach|Defina como diferente de zero para indicar suporte para anexo a programas existentes.|
|metricCallStackBP|Defina como diferente de zero para indicar suporte para pontos de interrupção de pilha de chamadas.|
|metricConditionalBP|Defina como diferente de zero para indicar suporte para a configuração de pontos de interrupção condicionais.|
|metricDataBP|Defina como diferente de zero para indicar suporte para a configuração de pontos de interrupção nas alterações nos dados.|
|metricDisassembly|Defina como diferente de zero para indicar suporte para a produção de uma listagem de desmontagem.|
|metricDumpWriting|Defina como diferente de zero para indicar suporte para gravação de despejo (o despejo de memória para um dispositivo de saída).|
|metricENC|Defina como diferente de zero para indicar suporte para editar e continuar. **Observação:**  Um mecanismo de depuração personalizado nunca deve definir isso ou deve sempre defini-lo como 0.|
|metricExceptions|Defina como diferente de zero para indicar suporte para exceções.|
|metricFunctionBP|Defina como diferente de zero para indicar suporte para pontos de interrupção nomeados (pontos de interrupção que são interrompidos quando um determinado nome de função é chamado).|
|metricHitCountBP|Defina como diferente de zero para indicar suporte para a configuração de pontos de interrupção "ponto de acesso" (pontos de interrupção que são disparados somente depois de serem atingidos um determinado número de vezes).|
|metricJITDebug|Defina como diferente de zero para indicar suporte para depuração Just-in-time (o depurador é iniciado quando ocorre uma exceção em um processo em execução).|
|metricMemory|NÃO USADO|
|metricPortSupplier|Defina isso para o CLSID do fornecedor da porta se um for implementado.|
|metricRegisters|NÃO USADO|
|metricSetNextStatement|Defina como diferente de zero para indicar suporte para definir a próxima instrução (que ignora a execução de instruções intermediárias).|
|metricSuspendThread|Defina como diferente de zero para indicar suporte para suspender a execução do thread.|
|metricWarnIfNoSymbols|Defina como diferente de zero para indicar que o usuário deve ser notificado se não houver nenhum símbolo.|
|metricProgramProvider|Defina isso para o CLSID do provedor de programa.|
|metricAlwaysLoadProgramProviderLocal|Defina como diferente de zero para indicar que o provedor do programa sempre deve ser carregado localmente.|
|metricEngineCanWatchProcess|Defina isso como diferente de zero para indicar que o mecanismo de depuração observará eventos de processo em vez do provedor de programa.|
|metricRemoteDebugging|Defina isso como diferente de zero para indicar suporte para depuração remota.|
|metricEncUseNativeBuilder|Defina isso como diferente de zero para indicar que o Gerenciador de edição e continuação deve usar o encbuild.dll do mecanismo de depuração para compilar para editar e continuar. **Observação:**  Um mecanismo de depuração personalizado nunca deve definir isso ou deve sempre defini-lo como 0.|
|metricLoadUnderWOW64|Defina isso como diferente de zero para indicar que o mecanismo de depuração deve ser carregado no processo depurado em WOW durante a depuração de um processo de 64 bits; caso contrário, o mecanismo de depuração será carregado no processo do Visual Studio (que está sendo executado no WOW64).|
|metricLoadProgramProviderUnderWOW64|Defina isso como diferente de zero para indicar que o provedor do programa deve ser carregado no processo de depuração ao depurar um processo de 64 bits em WOW; caso contrário, ele será carregado no processo do Visual Studio.|
|metricStopOnExceptionCrossingManagedBoundary|Defina isso como diferente de zero para indicar que o processo deve parar se uma exceção sem tratamento for lançada entre limites de código gerenciados/não gerenciados.|
|metricAutoSelectPriority|Defina isso para uma prioridade para a seleção automática do mecanismo de depuração (valores mais altos são iguais à prioridade mais alta).|
|metricAutoSelectIncompatibleList|Chave do registro contendo entradas que especificam GUIDs para que os mecanismos de depuração sejam ignorados na seleção automática. Essas entradas são um número (0, 1, 2 e assim por diante) com um GUID expresso como uma cadeia de caracteres.|
|metricIncompatibleList|Chave do registro contendo entradas que especificam GUIDs para mecanismos de depuração que são incompatíveis com esse mecanismo de depuração.|
|metricDisableJITOptimization|Defina isso como diferente de zero para indicar que otimizações just-in-time (para código gerenciado) devem ser desabilitadas durante a depuração.|

|Propriedades do avaliador de expressão|Descrição|
|-------------------------------------|-----------------|
|metricEngine|Isso contém o número de mecanismos de depuração que dão suporte ao avaliador de expressão especificado.|
|metricPreloadModules|Defina como diferente de zero para indicar que os módulos devem ser pré-carregados quando um avaliador de expressão for iniciado em um programa.|
|metricThisObjectName|Defina isso para o nome do objeto "This".|

|Propriedades de extensão do avaliador de expressão|Descrição|
| - |-----------------|
|metricExtensionDll|Nome da dll que dá suporte a essa extensão.|
|metricExtensionRegistersSupported|Lista de registros com suporte.|
|metricExtensionRegistersEntryPoint|Ponto de entrada para acessar os registros.|
|metricExtensionTypesSupported|Lista de tipos com suporte.|
|metricExtensionTypesEntryPoint|Ponto de entrada para acessar tipos.|

|Propriedades do fornecedor da porta|Descrição|
|------------------------------|-----------------|
|metricPortPickerCLSID|O CLSID do seletor de porta (uma caixa de diálogo que o usuário pode usar para selecionar portas e adicionar portas a serem usadas para depuração).|
|metricDisallowUserEnteredPorts|Diferente de zero se as portas inseridas pelo usuário não puderem ser adicionadas ao fornecedor da porta (isso torna a caixa de diálogo Seletor de porta essencialmente somente leitura).|
|metricPidBase|A ID do processo base usada pelo fornecedor da porta ao alocar IDs de processo.|

|Tipos de armazenamento de SP predefinido|Descrição|
|-------------------------------|-----------------|
|storetypeFile|Os símbolos são armazenados em um arquivo separado.|
|storetypeMetadata|Os símbolos são armazenados como metadados em um assembly.|

|Propriedades diversas|Descrição|
|------------------------------|-----------------|
|metricShowNonUserCode|Defina isso como diferente de zero para mostrar o código que não é do usuário.|
|metricJustMyCodeStepping|Defina isso como diferente de zero para indicar que a depuração pode ocorrer somente no código do usuário.|
|metricCLSID|CLSID para um objeto de um tipo de métrica específico.|
|metricName|Nome amigável para um objeto de um tipo de métrica específico.|
|metricLanguage|Nome do idioma.|

## <a name="registry-locations"></a>Locais do registro
 As métricas são lidas e gravadas no registro, especificamente na `VisualStudio` subchave.

> [!NOTE]
> Na maioria das vezes, as métricas serão gravadas na chave de HKEY_LOCAL_MACHINE. No entanto, às vezes HKEY_CURRENT_USER será a chave de destino. Dbgmetric. lib manipula ambas as chaves. Ao obter uma métrica, ele pesquisa HKEY_CURRENT_USER primeiro e, em seguida, HKEY_LOCAL_MACHINE. Quando ele está definindo uma métrica, um parâmetro especifica qual chave de nível superior deve ser usada.

 *[chave do registro]*\

 `Software`\

 `Microsoft`\

 `VisualStudio`\

 *[raiz da versão]*\

 *[raiz da métrica]*\

 *[tipo de métrica]*\

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[chave do registro]*|`HKEY_CURRENT_USER` ou `HKEY_LOCAL_MACHINE`.|
|*[raiz da versão]*|A versão do Visual Studio (por exemplo, `7.0` , `7.1` ou `8.0` ). No entanto, essa raiz também pode ser modificada usando a opção **/rootsuffix** para **devenv.exe**. Para o VSIP, esse modificador normalmente é **exp**, portanto, a raiz da versão seria, por exemplo, 8.0 Exp.|
|*[raiz da métrica]*|Isso é `AD7Metrics` ou `AD7Metrics(Debug)` , dependendo se a versão de depuração de dbgmetric. lib é usada. **Observação:**  Se dbgmetric. lib for usado, essa Convenção de nomenclatura deverá ser atendida se você tiver diferenças entre as versões de depuração e de lançamento que devem ser refletidas no registro.|
|*[tipo de métrica]*|O tipo de métrica a ser gravado: `Engine` , `ExpressionEvaluator` , `SymbolProvider` etc. Todos eles são definidos como em dbgmetric. h como `metricTypeXXXX` , em que `XXXX` é o nome do tipo específico.|
|*medidas*|O nome de uma entrada à qual um valor será atribuído para definir a métrica. A organização real das métricas depende do tipo de métrica.|
|*[valor da métrica]*|O valor atribuído à métrica. O tipo que o valor deve ter (cadeia de caracteres, número etc.) depende da métrica.|

> [!NOTE]
> Todos os GUIDs são armazenados no formato de `{GUID}` . Por exemplo, `{123D150B-FA18-461C-B218-45B3E4589F9B}`.

### <a name="debug-engines"></a>Mecanismos de depuração
 A seguir está a organização das métricas de mecanismos de depuração no registro. `Engine` é o nome do tipo de métrica para um mecanismo de depuração e corresponde a *[tipo de métrica]* na subárvore do registro acima.

 `Engine`\

 *[GUID do mecanismo]*\

 `CLSID` = *[GUID de classe]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 `PortSupplier`\

 `0` = *[GUID do fornecedor da porta]*

 `1` = *[GUID do fornecedor da porta]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID do mecanismo]*|O GUID do mecanismo de depuração.|
|*[GUID de classe]*|O GUID da classe que implementa esse mecanismo de depuração.|
|*[GUID do fornecedor da porta]*|O GUID do fornecedor da porta, se houver. Muitos mecanismos de depuração usam o fornecedor de porta padrão e, portanto, não especificam seu próprio fornecedor. Nesse caso, a subchave `PortSupplier` estará ausente.|

### <a name="port-suppliers"></a>Fornecedores de porta
 A seguir está a organização das métricas de fornecedor de porta no registro. `PortSupplier` é o nome do tipo de métrica para um fornecedor de porta e corresponde a *[tipo de métrica]*.

 `PortSupplier`\

 *[GUID do fornecedor da porta]*\

 `CLSID` = *[GUID de classe]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID do fornecedor da porta]*|O GUID do fornecedor da porta|
|*[GUID de classe]*|O GUID da classe que implementa este fornecedor de porta|

### <a name="symbol-providers"></a>Provedores de símbolos
 A seguir está a organização das métricas de fornecedor do símbolo no registro. `SymbolProvider` é o nome do tipo de métrica para o provedor de símbolo e corresponde a *[tipo de métrica]*.

 `SymbolProvider`\

 *[GUID do provedor de símbolos]*\

 `file`\

 `CLSID` = *[GUID de classe]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 `metadata`\

 `CLSID` = *[GUID de classe]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID do provedor de símbolos]*|O GUID do provedor de símbolos|
|*[GUID de classe]*|O GUID da classe que implementa este provedor de símbolos|

### <a name="expression-evaluators"></a>Avaliadores de expressão
 A seguir está a organização das métricas do avaliador de expressão no registro. `ExpressionEvaluator` é o nome do tipo de métrica para o avaliador de expressão e corresponde a *[tipo de métrica]*.

> [!NOTE]
> O tipo de métrica para `ExpressionEvaluator` não é definido em dbgmetric. h, pois supõe-se que todas as alterações de métrica para avaliadores de expressão percorrerão as funções de métrica do avaliador de expressão apropriadas (o layout da `ExpressionEvaluator` subchave é um pouco complicado, portanto os detalhes estão ocultos em dbgmetric. lib).

 `ExpressionEvaluator`\

 *[GUID de idioma]*\

 *[GUID do fornecedor]*\

 `CLSID` = *[GUID de classe]*

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 `Engine`\

 `0` = *[GUID do mecanismo de depuração]*

 `1` = *[GUID do mecanismo de depuração]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID de idioma]*|O GUID de um idioma|
|*[GUID do fornecedor]*|O GUID de um fornecedor|
|*[GUID de classe]*|O GUID da classe que implementa este avaliador de expressão|
|*[GUID do mecanismo de depuração]*|O GUID de um mecanismo de depuração com o qual este avaliador de expressão funciona|

### <a name="expression-evaluator-extensions"></a>Extensões do avaliador de expressão
 A seguir está a organização das métricas de extensão do avaliador de expressão no registro. `EEExtensions` é o nome do tipo de métrica para as extensões do avaliador de expressão e corresponde a *[tipo de métrica]*.

 `EEExtensions`\

 *[GUID de extensão]*\

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID de extensão]*|O GUID de uma extensão do avaliador de expressão|

### <a name="exceptions"></a>Exceções
 A seguir está a organização das métricas de exceções no registro. `Exception` é o nome do tipo de métrica para as exceções e corresponde a *[tipo de métrica]*.

 `Exception`\

 *[GUID do mecanismo de depuração]*\

 *[tipos de exceção]*\

 *Exception*\

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

 *Exception*\

 *[metric] = [valor da métrica]*

 *[metric] = [valor da métrica]*

|Espaço reservado|Descrição|
|-----------------|-----------------|
|*[GUID do mecanismo de depuração]*|O GUID de um mecanismo de depuração que oferece suporte a exceções.|
|*[tipos de exceção]*|Um título geral para a subchave que identifica a classe de exceções que pode ser tratada. Nomes típicos são **exceções do C++**, exceções do **Win32**, **exceções do Common Language Runtime** e **verificações de Run-Time nativas**. Esses nomes também são usados para identificar uma classe de exceção específica para o usuário.|
|*Exception*|Um nome para uma exceção: por exemplo, **_com_error** ou **controle-Break**. Esses nomes também são usados para identificar uma exceção específica ao usuário.|

## <a name="requirements"></a>Requisitos
 Esses arquivos estão localizados no [!INCLUDE[vs_dev10_ext](../../../extensibility/debugger/reference/includes/vs_dev10_ext_md.md)] diretório de instalação do SDK (por padrão, *[unidade]* \Arquivos de programas\microsoft Visual Studio 2010 SDK \\ ).

 Cabeçalho: includes\dbgmetric.h

 Biblioteca: libs\ad2de.lib, libs\dbgmetric.lib

## <a name="see-also"></a>Confira também
- [Referência da API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)
