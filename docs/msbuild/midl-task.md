---
title: Tarefa MIDL | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCMidlTool.ServerStubFile
- VC.Project.VCMidlTool.ApplicationConfigurationMode
- VC.Project.VCMidlTool.GenerateServerFiles
- VC.Project.VCMidlTool.ClientStubFile
- VC.Project.VCMidlTool.LocaleID
- VC.Project.VCMidlTool.GenerateClientFiles
- VC.Project.VCMidlTool.SuppressCompilerWarnings
- VC.Project.VCMidlTool.TypeLibFormat
- vc.task.midl
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), MIDL task
- MIDL task (MSBuild (Visual C++))
ms.assetid: 727efa8c-3336-40b8-8bef-ae6cbd77a422
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1affc4d84b8ea44cbaed51f656c8a3e97e04f97a
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219803"
---
# <a name="midl-task"></a>tarefa MIDL
Encapsula a ferramenta do compilador da MIDL (linguagem IDL) da Microsoft, *midl.exe*. Para obter mais informações, confira [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
## <a name="parameters"></a>Parâmetros  
 Veja a seguir a descrição dos parâmetros da tarefa **MIDL**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
-   **AdditionalIncludeDirectories**  
  
     Parâmetro **String[]** opcional.  
  
     Adiciona um diretório à lista de diretórios que são pesquisados quanto a arquivos IDL importados, arquivos de cabeçalho incluídos e ACF (arquivos de configuração de aplicativo).  
  
     Para obter mais informações, confira a opção **/I** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **AdditionalOptions**  
  
     Parâmetro **String** opcional.  
  
     Uma lista de opções de linha de comando. Por exemplo, /\<option1> /\<option2> /\<option#>. Use esse parâmetro para especificar opções de linha de comando não representadas por nenhum outro parâmetro da tarefa MIDL.  
  
     Para obter mais informações, confira [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ApplicationConfigurationMode**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, permite que você use algumas palavras-chave ACF no arquivo IDL.  
  
     Para obter mais informações, confira a opção **/app_config** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ClientStubFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de stub do cliente para uma interface RPC.  
  
     Para obter mais informações, confira a opção **/cstub** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **ServerStubFile** nessa tabela.  
  
-   **CPreprocessOptions**  
  
     Parâmetro **String** opcional.  
  
     Especifica as opções para passar para o pré-processador C/C++. Especifique uma lista delimitada por espaço de opções de pré-processador.  
  
     Para obter mais informações, confira a opção **/cpp_opt** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **DefaultCharType**  
  
     Parâmetro **String** opcional.  
  
     Especifica o tipo de caractere padrão que o compilador C usará para compilar o código gerado.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Signed**|**/char signed**|  
    |**Unsigned**|**/char unsigned**|  
    |**Ascii**|**/char ascii7**|  
  
     Para obter mais informações, confira a opção **/char** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **DllDataFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome de arquivo para o arquivo *dlldata* gerado para um DLL de proxy.  
  
     Para obter mais informações, confira a opção **/dlldata** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **EnableErrorChecks**  
  
     Parâmetro **String** opcional.  
  
     Especifica o tipo de verificação de erro que os stubs gerados executarão no tempo de execução.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/error none**|  
    |**EnableCustom**|**/error**|  
    |**All**|**/error all**|  
  
     Para obter mais informações, confira a opção **/error** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ErrorCheckAllocations**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifique se há erros de memória insuficiente.  
  
     Para obter mais informações, confira a opção **/error allocation** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ErrorCheckBounds**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifica o tamanho de variação compatível e matrizes variáveis em relação à especificação de tamanho da transmissão.  
  
     Para obter mais informações, confira a opção **/error bounds_check** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ErrorCheckEnumRange**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifica se os valores de enumeração estão em um intervalo permitido.  
  
     Para obter mais informações, confira a opção **/error enum** na ajuda da linha de comando (**/?**) do *midl.exe*.  
  
-   **ErrorCheckRefPointers**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifique se nenhum ponteiro de referência nula é passado para os stubs de cliente.  
  
     Para obter mais informações, confira a opção **/error ref** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ErrorCheckStubData**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, gera um stub que captura exceções de unmarshaling no lado do servidor e as propaga para o cliente.  
  
     Para obter mais informações, confira a opção **/error stub_data** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **GenerateClientFiles**  
  
     Parâmetro **String** opcional.  
  
     Especifica se o compilador gera arquivos de origem de C do lado do cliente para uma interface RPC.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/client none**|  
    |**Stub**|**/client stub**|  
  
     Para obter mais informações, confira a opção **/client** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **GenerateServerFiles**  
  
     Parâmetro **String** opcional.  
  
     Especifica se o compilador gera arquivos de origem de C do lado do servidor para uma interface RPC.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/server none**|  
    |**Stub**|**/server stub**|  
  
     Para obter mais informações, confira a opção **/server** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **GenerateStublessProxies**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, gera os stubs totalmente interpretados com proxies sem stub para interfaces de objeto.  
  
     Para obter mais informações, confira a opção **/Oicf** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **GenerateTypeLibrary**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, um arquivo de biblioteca de tipos (*.tlb*) não será gerado.  
  
     Para obter mais informações, confira a opção **/notlb** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **HeaderFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de cabeçalho gerado.  
  
     Para obter mais informações, confira a opção **/h** ou **/header** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **IgnoreStandardIncludePath**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, a tarefa MIDL pesquisa somente os diretórios especificados usando a opção **AdditionalIncludeDirectories** e ignora o diretório atual e os diretórios especificados pela variável de ambiente INCLUDE.  
  
     Para obter mais informações, confira a opção **/no_def_idir** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **InterfaceIdentifierFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do *arquivo identificador de interface* para uma interface COM. Isso substitui o nome padrão é obtido, adicionando "_i.c" ao nome do arquivo IDL.  
  
     Para obter mais informações, confira a opção **/iid** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **LocaleID**  
  
     Parâmetro **int** opcional.  
  
     Especifica o *identificador de localidade* que permite o uso de caracteres internacionais em arquivos de entrada, nomes de arquivo e caminhos de diretório. Especifique um identificador de localidade decimal.  
  
     Para obter mais informações, confira a opção **/lcid** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Confira também [Identificadores de localidade](https://docs.microsoft.com/windows/desktop/intl/locale-identifiers).  
  
-   **MkTypLibCompatible**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, exigirá que o formato do arquivo de entrada seja compatível com o *mktyplib.exe* versão 2.03.  
  
     Para obter mais informações, confira a opção **/mktyplib203** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Além disso, confira [Sintaxe do arquivo ODL](/previous-versions/windows/desktop/automat/odl-file-syntax) no site do MSDN.  
  
-   **OutputDirectory**  
  
     Parâmetro **String** opcional.  
  
     Especifica o diretório padrão em que a tarefa MIDL grava os arquivos de saída.  
  
     Para obter mais informações, confira a opção **/out** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **PreprocessorDefinitions**  
  
     Parâmetro **String[]** opcional.  
  
     Especifica um ou mais *defines*, ou seja, um nome e um valor opcional a serem passados para o pré-processador C como se por uma diretiva `#define`. A forma de cada define é *nome[=valor]*.  
  
     Para obter mais informações, confira a opção **/D** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **UndefinePreprocessorDefinitions** nessa tabela.  
  
-   **ProxyFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de proxy da interface para uma interface COM.  
  
     Para obter mais informações, confira a opção **/proxy** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **RedirectOutputAndErrors**  
  
     Parâmetro **String** opcional.  
  
     Redireciona a saída, como mensagens de erro e avisos, da saída padrão para o arquivo especificado.  
  
     Para obter mais informações, confira a opção **/o** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **ServerStubFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de stub do servidor para uma interface RPC.  
  
     Para obter mais informações, confira a opção **/sstub** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **ClientStubFile** nessa tabela.  
  
-   **Source**  
  
     Parâmetro `ITaskItem[]` obrigatório.  
  
     Especifica uma lista de arquivos de origem separados por espaços.  
  
-   **StructMemberAlignment**  
  
     Parâmetro **String** opcional.  
  
     Especifica o alinhamento (*nível de empacotamento*) de estruturas no sistema de destino.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**1**|**/Zp1**|  
    |**2**|**/Zp2**|  
    |**4**|**/Zp4**|  
    |**8**|**/Zp8**|  
  
     Para obter mais informações, confira a opção **/Zp** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). A opção **/Zp** é equivalente à opção **/pack** e à opção **/align** antiga.  
  
-   **SuppressCompilerWarnings**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, suprime mensagens de aviso da tarefa MIDL.  
  
     Para obter mais informações, confira a opção **/no_warn** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **SuppressStartupBanner**  
  
     Parâmetro `Boolean` opcional.  
  
     Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.  
  
     Para obter mais informações, confira a opção **/nologo** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **TargetEnvironment**  
  
     Parâmetro **String** opcional.  
  
     Especifica o ambiente no qual o aplicativo é executado.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**NotSet**|*\<none>*|  
    |**Win32**|**/env win32**|  
    |**Itanium**|**/env ia64**|  
    |**X64**|**/env x64**|  
  
     Para obter mais informações, confira a opção **/env** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **TrackerLogDirectory**  
  
     Parâmetro `String` opcional.  
  
     Especifica o diretório intermediário em que os logs de rastreamento para essa tarefa são armazenados.  
  
-   **TypeLibFormat**  
  
     Parâmetro **String** opcional.  
  
     Especifica o formato do arquivo de biblioteca de tipos.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**NewFormat**|**/newtlb**|  
    |**OldFormat**|**/oldtlb**|  
  
     Para obter mais informações, confira as opções **/newtlb** e **/oldtlb** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **TypeLibraryName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de biblioteca de tipos.  
  
     Para obter mais informações, confira a opção **/tlb** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **UndefinePreprocessorDefinitions**  
  
     Parâmetro **String[]** opcional.  
  
     Remove qualquer definição anterior de um nome passando o nome para o pré-processador C como se por uma diretiva `#undefine`. Especifique um ou mais nomes definidos anteriormente.  
  
     Para obter mais informações, confira a opção **/U** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **PreprocessorDefinitions** nessa tabela.  
  
-   **ValidateAllParameters**  
  
     Parâmetro `Boolean` opcional.  
  
     Se `true`, gera informações adicionais de verificação de erro que são usadas para executar verificações de integridade em tempo de execução. Se `false`, as informações de verificação de erro não são geradas.  
  
     Para obter mais informações, confira as opções **/robust** e **/no_robust** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference).  
  
-   **WarnAsError**  
  
     Parâmetro `Boolean` opcional.  
  
     Se for `true`, tratará todos os avisos como erros.  
  
     Se o parâmetro de tarefa MIDL **WarningLevel** não for especificado, os avisos no nível padrão, nível 1, serão tratados como erros.  
  
     Para obter mais informações, confira as opções **/WX** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **WarningLevel** nessa tabela.  
  
-   **WarningLevel**  
  
     Parâmetro **String** opcional.  
  
     Especifica a gravidade (*nível de aviso*) de avisos a serem emitidos. Nenhum aviso é emitido para um valor de 0. Caso contrário, um aviso será emitido se seu nível de aviso for numericamente menor ou igual ao valor especificado.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**0**|**/W0**|  
    |**1**|**/W1**|  
    |**2**|**/W2**|  
    |**3**|**/W3**|  
    |**4**|**/W4**|  
  
     Para obter mais informações, confira a opção **/W** em [Referência da linha de comando MIDL](https://docs.microsoft.com/windows/desktop/Midl/midl-command-line-reference). Consulte também o parâmetro **WarnAsError** nessa tabela.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)