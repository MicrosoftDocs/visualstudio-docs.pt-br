---
title: Tarefa MIDL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 345cd480cd5e34a6fe4650c9321d3ad9f90db01e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49215781"
---
# <a name="midl-task"></a>Tarefa MIDL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula a ferramenta de compilador MIDL (linguagem IDL da Microsoft), midl.exe. Para obter mais informações, consulte “MIDL Command-Line Reference” (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **MIDL**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
-   **AdditionalIncludeDirectories**  
  
     Parâmetro **String[]** opcional.  
  
     Adiciona um diretório à lista de diretórios que são pesquisados quanto a arquivos IDL importados, arquivos de cabeçalho incluídos e ACF (arquivos de configuração de aplicativo).  
  
     Para obter mais informações, consulte a opção **/I** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **AdditionalOptions**  
  
     Parâmetro **String** opcional.  
  
     Uma lista de opções de linha de comando. Por exemplo, **"**_/option1 /option2 /option#_". Use esse parâmetro para especificar opções de linha de comando não representadas por nenhum outro parâmetro da tarefa MIDL.  
  
     Para obter mais informações, consulte “MIDL Command-Line Reference” (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ApplicationConfigurationMode**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, permite que você use algumas palavras-chave ACF no arquivo IDL.  
  
     Para obter mais informações, consulte a opção **/app_config** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ClientStubFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de stub do cliente para uma interface RPC.  
  
     Para obter mais informações, consulte a opção **/cstub** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **ServerStubFile** nessa tabela.  
  
-   **CPreprocessOptions**  
  
     Parâmetro **String** opcional.  
  
     Especifica as opções para passar para o pré-processador C/C++. Especifique uma lista delimitada por espaço de opções de pré-processador.  
  
     Para obter mais informações, consulte a opção **/cpp_opt** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **DefaultCharType**  
  
     Parâmetro **String** opcional.  
  
     Especifica o tipo de caractere padrão que o compilador C usará para compilar o código gerado.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Signed**|**/char signed**|  
    |**Unsigned**|**/char unsigned**|  
    |**Ascii**|**/char ascii7**|  
  
     Para obter mais informações, consulte a opção **/char** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **DllDataFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome de arquivo para o arquivo *dlldata* gerado para um DLL de proxy.  
  
     Para obter mais informações, consulte a opção **/dlldata** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **EnableErrorChecks**  
  
     Parâmetro **String** opcional.  
  
     Especifica o tipo de verificação de erro que os stubs gerados executarão no tempo de execução.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/error none**|  
    |**EnableCustom**|**/error**|  
    |**All**|**/error all**|  
  
     Para obter mais informações, consulte a opção **/error** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ErrorCheckAllocations**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifique se há erros de memória insuficiente.  
  
     Para obter mais informações, consulte a opção **/error allocation** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ErrorCheckBounds**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifica o tamanho de variação compatível e matrizes variáveis em relação à especificação de tamanho da transmissão.  
  
     Para obter mais informações, consulte a opção **/error bounds_check** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ErrorCheckEnumRange**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifica se os valores de enumeração estão em um intervalo permitido.  
  
     Para obter mais informações, consulte a opção **/error enum** na ajuda da linha de comando (**/?**) do midl.exe.  
  
-   **ErrorCheckRefPointers**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, verifique se nenhum ponteiro de referência nula é passado para os stubs de cliente.  
  
     Para obter mais informações, consulte a opção **/error ref** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ErrorCheckStubData**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, gera um stub que captura exceções de unmarshaling no lado do servidor e as propaga para o cliente.  
  
     Para obter mais informações, consulte a opção **/error stub_data** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **GenerateClientFiles**  
  
     Parâmetro **String** opcional.  
  
     Especifica se o compilador gera arquivos de origem de C do lado do cliente para uma interface RPC.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/client none**|  
    |**Stub**|**/client stub**|  
  
     Para obter mais informações, consulte a opção **/client** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **GenerateServerFiles**  
  
     Parâmetro **String** opcional.  
  
     Especifica se o compilador gera arquivos de origem de C do lado do servidor para uma interface RPC.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    |Valor|Opção de linha de comando|  
    |-----------|--------------------------|  
    |**Nenhum**|**/server none**|  
    |**Stub**|**/server stub**|  
  
     Para obter mais informações, consulte a opção **/server** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **GenerateStublessProxies**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, gera os stubs totalmente interpretados com proxies sem stub para interfaces de objeto.  
  
     Para obter mais informações, consulte a opção **/Oicf** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **GenerateTypeLibrary**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, um arquivo de biblioteca de tipo (.tlb) não é gerado.  
  
     Para obter mais informações, consulte a opção **/notlb** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **HeaderFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de cabeçalho gerado.  
  
     Para obter mais informações, consulte a opção **/h** ou **/header** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **IgnoreStandardIncludePath**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, a tarefa MIDL pesquisa somente os diretórios especificados usando a opção **AdditionalIncludeDirectories** e ignora o diretório atual e os diretórios especificados pela variável de ambiente INCLUDE.  
  
     Para obter mais informações, consulte a opção **/no_def_idir** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **InterfaceIdentifierFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do *arquivo identificador de interface* para uma interface COM. Isso substitui o nome padrão é obtido, adicionando "_i.c" ao nome do arquivo IDL.  
  
     Para obter mais informações, consulte a opção **/iid** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **LocaleID**  
  
     Parâmetro **int** opcional.  
  
     Especifica o *identificador de localidade* que permite o uso de caracteres internacionais em arquivos de entrada, nomes de arquivo e caminhos de diretório. Especifique um identificador de localidade decimal.  
  
     Para obter mais informações, consulte a opção **/lcid** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também “IDs de localidades atribuídas pela Microsoft” no MSDN.  
  
-   **MkTypLibCompatible**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, requer que o formato do arquivo de entrada seja compatível com mktyplib.exe versão 2.03.  
  
     Para obter mais informações, consulte a opção **/mktyplib203** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Além disso, consulte "ODL File Syntax" (Sintaxe do arquivo ODL) no site do MSDN.  
  
-   **OutputDirectory**  
  
     Parâmetro **String** opcional.  
  
     Especifica o diretório padrão em que a tarefa MIDL grava os arquivos de saída.  
  
     Para obter mais informações, consulte a opção **/out** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **PreprocessorDefinitions**  
  
     Parâmetro **String[]** opcional.  
  
     Especifica um ou mais *defines*, ou seja, um nome e um valor opcional a serem passados para o pré-processador C como se por uma diretiva `#define`. A forma de cada define é *nome[=valor]*.  
  
     Para obter mais informações, consulte a opção **/D** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **UndefinePreprocessorDefinitions** nessa tabela.  
  
-   **ProxyFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de proxy da interface para uma interface COM.  
  
     Para obter mais informações, consulte a opção **/proxy** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **RedirectOutputAndErrors**  
  
     Parâmetro **String** opcional.  
  
     Redireciona a saída, como mensagens de erro e avisos, da saída padrão para o arquivo especificado.  
  
     Para obter mais informações, consulte a opção **/o** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **ServerStubFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de stub do servidor para uma interface RPC.  
  
     Para obter mais informações, consulte a opção **/sstub** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **ClientStubFile** nessa tabela.  
  
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
  
     Para obter mais informações, consulte a opção **/Zp** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). A opção **/Zp** é equivalente à opção **/pack** e à opção **/align** antiga.  
  
-   **SuppressCompilerWarnings**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, suprime mensagens de aviso da tarefa MIDL.  
  
     Para obter mais informações, consulte a opção **/no_warn** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **SuppressStartupBanner**  
  
     Parâmetro `Boolean` opcional.  
  
     Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.  
  
     Para obter mais informações, consulte a opção **/nologo** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
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
  
     Para obter mais informações, consulte a opção **/env** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
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
  
     Para obter mais informações, consulte as opções **/newtlb** e **/oldtlb** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **TypeLibraryName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo de biblioteca de tipos.  
  
     Para obter mais informações, consulte a opção **/tlb** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **UndefinePreprocessorDefinitions**  
  
     Parâmetro **String[]** opcional.  
  
     Remove qualquer definição anterior de um nome passando o nome para o pré-processador C como se por uma diretiva `#undefine`. Especifique um ou mais nomes definidos anteriormente.  
  
     Para obter mais informações, consulte a opção **/U** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **PreprocessorDefinitions** nessa tabela.  
  
-   **ValidateAllParameters**  
  
     Parâmetro `Boolean` opcional.  
  
     Se `true`, gera informações adicionais de verificação de erro que são usadas para executar verificações de integridade em tempo de execução. Se `false`, as informações de verificação de erro não são geradas.  
  
     Para obter mais informações, consulte as opções **/robust** e **/no_robust** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
-   **WarnAsError**  
  
     Parâmetro `Boolean` opcional.  
  
     Se for `true`, tratará todos os avisos como erros.  
  
     Se o parâmetro de tarefa MIDL **WarningLevel** não for especificado, os avisos no nível padrão, nível 1, serão tratados como erros.  
  
     Para obter mais informações, consulte as opções **/WX** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **WarningLevel** nessa tabela.  
  
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
  
     Para obter mais informações, consulte a opção **/W** em "MIDL Command-Line Reference" (Referência da linha de comando MIDL) no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737). Consulte também o parâmetro **WarnAsError** nessa tabela.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



