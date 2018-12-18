---
title: Tarefa Link | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: reference
f1_keywords:
- VC.Project.VCLinkerTool.ForceFileOutput
- VC.Project.VCLinkerTool.LinkStatus
- VC.Project.VCLinkerTool.CLRUnmanagedCodeCheck
- VC.Project.VCLinkerTool.SpecifySectionAttributes
- VC.Project.VCLinkerTool.SupportNobindOfDelayLoadedDLL
- VC.Project.VCLinkerTool.MinimumRequiredVersion
- VC.Project.VCLinkerTool.PerUserRedirection
- VC.Project.VCLinkerTool.CreateHotPatchableImage
- VC.Project.VCLinkerTool.DataExecutionPrevention
- VC.Project.VCLinkerTool.TreatLinkerWarningsAsErrors
- vc.task.link
- VC.Project.VCLinkerTool.ImageHasSafeExceptionHandlers
- VC.Project.VCLinkerTool.CLRSupportLastError
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), Link task
- Link task (MSBuild (Visual C++))
ms.assetid: 0a61f168-3113-4fa7-83a3-d9142e2a33f8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5cd79db9b5bfc2e68dea2ff711b2da6ce55c9bc0
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220115"
---
# <a name="link-task"></a>tarefa de vinculação
Encapsula a ferramenta de vinculador do Visual C++, *link.exe*. A ferramenta de vinculador vincula arquivos-objeto e bibliotecas de formato COFF para criar um arquivo *.exe* (executável) ou uma DLL (biblioteca de vínculo dinâmico). Para obter mais informações, confira [Opções do vinculador](/cpp/build/reference/linker-options).  
  
## <a name="parameters"></a>Parâmetros  
 Veja a seguir uma descrição dos parâmetros da tarefa **Link**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
-   **AdditionalDependencies**  
  
     Parâmetro **String[]** opcional.  
  
     Especifica uma lista de arquivos de entrada para adicionar ao comando.  
  
     Para obter mais informações, confira [Arquivos de entrada LINK](/cpp/build/reference/link-input-files).  
  
-   **AdditionalLibraryDirectories**  
  
     Parâmetro **String[]** opcional.  
  
     Substitui o caminho da biblioteca de ambiente. Especifique um nome de diretório.  
  
     Para obter mais informações, consulte [/LIBPATH (Libpath Adicional)](/cpp/build/reference/libpath-additional-libpath).  
  
-   **AdditionalManifestDependencies**  
  
     Parâmetro **String[]** opcional.  
  
     Especifica atributos que serão colocados na seção `dependency` do arquivo de manifesto.  
  
     Para obter mais informações, confira [/MANIFESTDEPENDENCY (Especificar dependências de manifesto)](/cpp/build/reference/manifestdependency-specify-manifest-dependencies). Confira também [Arquivos de configuração de editor](https://docs.microsoft.com/windows/desktop/SbsCs/publisher-configuration-files).  
  
-   **AdditionalOptions**  
  
     Parâmetro **String** opcional.  
  
     Uma lista de opções de vinculador, conforme especificado na linha de comando. Por exemplo, /\<option1> /\<option2> /\<option#>. Use esse parâmetro para especificar opções de vinculador que não são representadas por qualquer outro parâmetro de tarefa **Link**.  
  
     Para obter mais informações, confira [Opções do vinculador](/cpp/build/reference/linker-options).  
  
-   **AddModuleNamesToAssembly**  
  
     Parâmetro **String[]** opcional.  
  
     Adiciona uma referência de módulo a um assembly.  
  
     Para obter mais informações, confira [/ASSEMBLYMODULE (Adicionar um módulo MSIL ao assembly)](/cpp/build/reference/assemblymodule-add-a-msil-module-to-the-assembly).  
  
-   **AllowIsolation**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, fará com que o sistema operacional realize pesquisas de manifesto e carregamentos. Se `false`, indicará que as DLLs serão carregadas como se não houvesse nenhum manifesto.  
  
     Para obter mais informações, confira [/ALLOWISOLATION (Pesquisa de manifesto)](/cpp/build/reference/allowisolation-manifest-lookup).  
  
-   **AssemblyDebug**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, emitirá o atributo **DebuggableAttribute** junto com o acompanhamento de informações de depuração e desabilitará otimizações JIT. Se `false`, emitirá o atributo **DebuggableAttribute**, mas desabilitará o acompanhamento de informações de depuração e as otimizações JIT.  
  
     Para obter mais informações, consulte [/ASSEMBLYDEBUG (Adicionar DebuggableAttribute)](/cpp/build/reference/assemblydebug-add-debuggableattribute).  
  
-   **AssemblyLinkResource**  
  
     Parâmetro **String[]** opcional.  
  
     Cria um link para um recurso do .NET Framework no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída. Especifique o nome do recurso.  
  
     Para obter mais informações, confira [/ASSEMBLYLINKRESOURCE (Link para recurso do .NET Framework)](/cpp/build/reference/assemblylinkresource-link-to-dotnet-framework-resource).  
  
-   **AttributeFileTracking**  
  
     Parâmetro **Booliano** implícito.  
  
     Habilita um acompanhamento de arquivos mais profundo a fim de capturar o comportamento incremental do link. Sempre retorna `true`.  
  
-   **BaseAddress**  
  
     Parâmetro **String** opcional.  
  
     Define um endereço básico para o programa ou DLL que está sendo criado. Especifique `{address[,size] | @filename,key}`.  
  
     Para obter mais informações, confira [/BASE (Endereço básico)](/cpp/build/reference/base-base-address).  
  
-   **BuildingInIDE**  
  
     Parâmetro **Boolean** opcional.  
  
     Se for true, indica que o MSBuild é chamado do IDE. Caso contrário, indica que o MSBuild é chamado da linha de comando.  
  
     Esse parâmetro não tem nenhuma opção de vinculador equivalente.  
  
-   **CLRImageType**  
  
     Parâmetro **String** opcional.  
  
     Define o tipo de uma imagem CLR (Common Language Runtime).  
  
     Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
    -   **Default** - *\<none>*  
  
    -   **ForceIJWImage** - **/CLRIMAGETYPE:IJW**  
  
    -   **ForcePureILImage** - **/CLRIMAGETYPE:PURE**  
  
    -   **ForceSafeILImage** - **/CLRIMAGETYPE:SAFE**  
  
    Para obter mais informações, confira, [/CLRIMAGETYPE (Especificar tipo de imagem CLR)](/cpp/build/reference/clrimagetype-specify-type-of-clr-image).  
  
-   **CLRSupportLastError**  
  
     Parâmetro **String** opcional.  
  
     Preserva o código de erro mais recente de funções chamadas por meio do mecanismo P/Invoke.  
  
     Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
    -   **Enabled** - **/CLRSupportLastError**  
  
    -   **Desabilitado** - **/CLRSupportLastError:NO**  
  
    -   **SystemDlls** - **/CLRSupportLastError:SYSTEMDLL**  
  
    Para obter mais informações, confira [/CLRSUPPORTLASTERROR (Preservar último código de erro para chamadas PInvoke)](/cpp/build/reference/clrsupportlasterror-preserve-last-error-code-for-pinvoke-calls).  
  
-   **CLRThreadAttribute**  
  
     Parâmetro **String** opcional.  
  
     Especifica explicitamente o atributo de thread para o ponto de entrada de seu programa CLR.  
  
     Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
    -   **DefaultThreadingAttribute** - **/CLRTHREADATTRIBUTE:NONE**  
  
    -   **MTAThreadingAttribute** - **/CLRTHREADATTRIBUTE:MTA**  
  
    -   **STAThreadingAttribute** - **/CLRTHREADATTRIBUTE:STA**  
  
    Para obter mais informações, confira [/CLRTHREADATTRIBUTE (Definir atributo de thread CLR)](/cpp/build/reference/clrthreadattribute-set-clr-thread-attribute).  
  
-   **CLRUnmanagedCodeCheck**  
  
     Parâmetro **Boolean** opcional.  
  
     Especifica se o vinculador aplicará o atributo **SuppressUnmanagedCodeSecurityAttribute** às chamadas P/Invoke geradas pelo vinculador do código gerenciado nas DLLs nativas.  
  
    Para obter mais informações, confira [/CLRUNMANAGEDCODECHECK (Adicionar o SuppressUnmanagedCodeSecurityAttribute)](/cpp/build/reference/clrunmanagedcodecheck-add-suppressunmanagedcodesecurityattribute).  
  
-   **CreateHotPatchableImage**  
  
     Parâmetro **String** opcional.  
  
     Prepara uma imagem para patch instantâneo.  
  
     Especifique um dos valores a seguir, que corresponda a uma opção de vinculador.  
  
    -   **Enabled** - **/FUNCTIONPADMIN**  
  
    -   **X86Image** - **/FUNCTIONPADMIN:5**  
  
    -   **X64Image** - **/FUNCTIONPADMIN:6**  
  
    -   **ItaniumImage** - **/FUNCTIONPADMIN:16**  
  
    Para obter mais informações, confira [/FUNCTIONPADMIN (Criar imagem para patch instantâneo)](/cpp/build/reference/functionpadmin-create-hotpatchable-image).  
  
-   **DataExecutionPrevention**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, indicará que um executável foi testado e considerado compatível com o recurso de Prevenção de Execução de Dados do Windows.  
  
     Para obter mais informações, consulte [/NXCOMPAT (Compatível com a Prevenção de Execução de Dados)](/cpp/build/reference/nxcompat-compatible-with-data-execution-prevention).  
  
-   **DelayLoadDLLs**  
  
     Parâmetro **String[]** opcional.  
  
     Esse parâmetro causa um *atraso no carregamento* de DLLs. Especifique o nome de uma DLL para atrasar o carregamento.  
  
     Para obter mais informações, confira [/DELAYLOAD (Importação de carga com atraso)](/cpp/build/reference/delayload-delay-load-import).  
  
-   **DelaySign**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, assinará parcialmente um assembly. Por padrão, o valor é `false`.  
  
     Para obter mais informações, confira [/DELAYSIGN (Assinar parcialmente um assembly)](/cpp/build/reference/delaysign-partially-sign-an-assembly).  
  
-   **Driver**  
  
     Parâmetro **String** opcional.  
  
     Especifique esse parâmetro para criar um driver de modo de kernel do Windows NT.  
  
     Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
    -   **NotSet** - *\<none>*  
  
    -   **Driver** - **/Driver**  
  
    -   **UpOnly** - **/DRIVER:UPONLY**  
  
    -   **WDM** - **/DRIVER:WDM**  
  
    Para obter mais informações, confira [/DRIVER (Driver de modo kernel do Windows NT)](/cpp/build/reference/driver-windows-nt-kernel-mode-driver).  
  
-   **EmbedManagedResourceFile**  
  
     Parâmetro **String[]** opcional.  
  
     Insere um arquivo de recurso em um assembly. Especifique o nome do arquivo de recurso necessário. Como opção, especifique o nome lógico, usado para carregar o recurso e a opção **PRIVADO**, que indica no manifesto do assembly que o arquivo de recurso é privado.  
  
     Para obter mais informações, confira [/ASSEMBLYRESOURCE (Inserir um recurso gerenciado)](/cpp/build/reference/assemblyresource-embed-a-managed-resource).  
  
-   **EnableCOMDATFolding**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, habilitará a dobra COMDAT idêntica.  
  
     Para obter mais informações, consulte o argumento `ICF[= iterations]` de [/OPT (Otimizações)](/cpp/build/reference/opt-optimizations).  
  
-   **EnableUAC**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, especificará que as informações do UAC (Controle de Conta de Usuário) estão inseridas no manifesto do programa.  
  
     Para obter mais informações, consulte [/MANIFESTUAC (Insere informações UAC no manifesto)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest).  
  
-   **EntryPointSymbol**  
  
     Parâmetro **String** opcional.  
  
     Especifica uma função de ponto de entrada como o endereço inicial para um arquivo *.exe* ou uma DLL. Especifique um nome de função como valor do parâmetro.  
  
     Para obter mais informações, confira [/ENTRY (Símbolo de ponto de entrada)](/cpp/build/reference/entry-entry-point-symbol).  
  
-   **FixedBaseAddress**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará um programa ou DLL que pode ser carregado somente em seu endereço básico preferido.  
  
     Para obter mais informações, confira [/FIXED (Endereço básico fixo)](/cpp/build/reference/fixed-fixed-base-address).  
  
-   **ForceFileOutput**  
  
     Parâmetro **String** opcional.  
  
     Instrui o vinculador a criar uma DLL ou um arquivo *.exe* válido mesmo que um símbolo esteja referenciado, mas não definido, ou esteja definido várias vezes.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **Enabled** - **/FORCE**  
  
    -   **MultiplyDefinedSymbolOnly** - **/FORCE:MULTIPLE**  
  
    -   **UndefinedSymbolOnly** - **/FORCE:UNRESOLVED**  
  
    Para obter mais informações, confira [/FORCE (Forçar saída de arquivo)](/cpp/build/reference/force-force-file-output).  
  
-   **ForceSymbolReferences**  
  
     Parâmetro **String[]** opcional.  
  
     Esse parâmetro instrui o vinculador a adicionar um símbolo especificado à tabela de símbolos.  
  
     Para obter mais informações, confira [/INCLUDE (Forçar referências de símbolo)](/cpp/build/reference/include-force-symbol-references).  
  
-   **FunctionOrder**  
  
     Parâmetro **String** opcional.  
  
     Esse parâmetro otimiza seu programa colocando as funções empacotadas (COMDATs) especificadas na imagem em uma ordem predeterminada.  
  
     Para obter mais informações, confira [/ORDER (Colocar funções na ordem)](/cpp/build/reference/order-put-functions-in-order).  
  
-   **GenerateDebugInformation**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, criará informações de depuração para o arquivo *.exe* ou a DLL.  
  
     Para obter mais informações, confira [/DEBUG (Gerar informações de depuração)](/cpp/build/reference/debug-generate-debug-info).  
  
-   **GenerateManifest**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará um arquivo de manifesto lado a lado.  
  
     Para obter mais informações, confira [/MANIFEST (Criar manifesto do assembly lado a lado)](/cpp/build/reference/manifest-create-side-by-side-assembly-manifest).  
  
-   **GenerateMapFile**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará um *arquivo de mapa*. A extensão de nome do arquivo de mapa é *.map*.  
  
     Para obter mais informações, confira [/MAP (Gerar arquivo de mapa)](/cpp/build/reference/map-generate-mapfile).  
  
-   **HeapCommitSize**  
  
     Parâmetro **String** opcional.  
  
     Especifica a quantidade de memória física no heap a se alocar por vez.  
  
     Para obter mais informações, confira o argumento `commit` em [/HEAP (Definir tamanho do heap)](/cpp/build/reference/heap-set-heap-size). Consulte também o parâmetro **HeapReserveSize**.  
  
-   **HeapReserveSize**  
  
     Parâmetro **String** opcional.  
  
     Especifica a alocação de heap total na memória virtual.  
  
     Para obter mais informações, confira o argumento `reserve` em [/HEAP (Definir tamanho do heap)](/cpp/build/reference/heap-set-heap-size). Consulte também o parâmetro **HeapCommitSize** nesta tabela.  
  
-   **IgnoreAllDefaultLibraries**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá o vinculador a remover uma ou mais bibliotecas padrão da lista de bibliotecas pesquisadas ao resolver referências externas.  
  
     Para obter mais informações, confira [/NODEFAULTLIB (Ignorar bibliotecas)](/cpp/build/reference/nodefaultlib-ignore-libraries).  
  
-   **IgnoreEmbeddedIDL**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, especificará que qualquer atributo IDL no código-fonte não deve ser processado em um arquivo *.idl*.  
  
     Para obter mais informações, confira [/IGNOREIDL (Não processar atributos em MIDL)](/cpp/build/reference/ignoreidl-don-t-process-attributes-into-midl).  
  
-   **IgnoreImportLibrary**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, especificará que a biblioteca de importações gerada por esta configuração não deve ser importada para os projetos dependentes.  
  
     Esse parâmetro não corresponde a uma opção de vinculador.  
  
-   **IgnoreSpecificDefaultLibraries**  
  
     Parâmetro **String[]** opcional.  
  
     Especifica um ou mais nomes de bibliotecas padrão a serem ignoradas. Separe várias bibliotecas usando ponto e vírgula.  
  
     Para obter mais informações, confira [/NODEFAULTLIB (Ignorar bibliotecas)](/cpp/build/reference/nodefaultlib-ignore-libraries).  
  
-   **ImageHasSafeExceptionHandlers**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, o vinculador produzirá uma imagem somente se também puder produzir uma tabela de manipuladores de exceção segura da imagem.  
  
     Para obter mais informações, confira [/SAFESEH (A imagem tem manipuladores de exceção seguros)](/cpp/build/reference/safeseh-image-has-safe-exception-handlers).  
  
-   **ImportLibrary**  
  
     Um nome de biblioteca de importação especificado pelo usuário que substitui o nome da biblioteca padrão.  
  
     Para obter mais informações, confira [/IMPLIB (Nomear biblioteca de importações)](/cpp/build/reference/implib-name-import-library).  
  
-   **KeyContainer**  
  
     Parâmetro **String** opcional.  
  
     Contêiner que contém a chave para um assembly assinado.  
  
     Para obter mais informações, confira [/KEYCONTAINER (Especificar um contêiner de chave para assinar um assembly)](/cpp/build/reference/keycontainer-specify-a-key-container-to-sign-an-assembly). Consulte também o parâmetro **KeyFile** nesta tabela.  
  
-   **KeyFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica um arquivo que contém a chave para um assembly assinado.  
  
     Para obter mais informações, confira [/KEYFILE (Especificar chave ou par de chaves para assinar um assembly)](/cpp/build/reference/keyfile-specify-key-or-key-pair-to-sign-an-assembly). Consulte também o parâmetro **KeyContainer**.  
  
-   **LargeAddressAware**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, o aplicativo poderá identificar endereços maiores do que 2 gigabytes.  
  
     Para obter mais informações, confira [/LARGEADDRESSAWARE (Identificar endereços grandes)](/cpp/build/reference/largeaddressaware-handle-large-addresses).  
  
-   **LinkDLL**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará uma DLL como o arquivo de saída principal.  
  
     Para obter mais informações, consulte [/DLL (Compilar uma DLL)](/cpp/build/reference/dll-build-a-dll).  
  
-   **LinkErrorReporting**  
  
     Parâmetro **String** opcional.  
  
     Permite que você forneça informações de ICE (erro interno do compilador) diretamente à Microsoft.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **NoErrorReport** - **/ERRORREPORT:NONE**  
  
    -   **PromptImmediately** - **/ERRORREPORT:PROMPT**  
  
    -   **QueueForNextLogin** - **/ERRORREPORT:QUEUE**  
  
    -   **SendErrorReport** - **/ERRORREPORT:SEND**  
  
    Para obter mais informações, confira [/ERRORREPORT (Relatar erros internos do vinculador)](/cpp/build/reference/errorreport-report-internal-linker-errors).  
  
-   **LinkIncremental**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, habilitará a vinculação incremental.  
  
     Para obter mais informações, confira [/INCREMENTAL (Vincular de forma incremental)](/cpp/build/reference/incremental-link-incrementally).  
  
-   **LinkLibraryDependencies**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, especificará que as saídas de biblioteca das dependências do projeto serão vinculadas automaticamente.  
  
     Esse parâmetro não corresponde a uma opção de vinculador.  
  
-   **LinkStatus**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, especificará que o vinculador deve exibir um indicador de progresso que mostrará o percentual concluído do link.  
  
     Para obter mais informações, confira o argumento `STATUS` de [/LTCG (Geração de código durante o tempo de vinculação)](/cpp/build/reference/ltcg-link-time-code-generation).  
  
-   **LinkTimeCodeGeneration**  
  
     Parâmetro **String** opcional.  
  
     Especifica opções para a otimização guiada por perfil.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **Default** - *\<none>*  
  
    -   **UseLinkTimeCodeGeneration** - **/LTCG**  
  
    -   **PGInstrument** - **/LTCG:PGInstrument**  
  
    -   **PGOptimization** - **/LTCG:PGOptimize**  
  
    -   **PGUpdate**  
  
         \- **/LTCG:PGUpdate**  
  
    Para obter mais informações, confira [/LTCG (Geração de código durante o tempo de vinculação)](/cpp/build/reference/ltcg-link-time-code-generation).  
  
-   **ManifestFile**  
  
     Parâmetro **String** opcional.  
  
     Altera o nome do arquivo de manifesto padrão para o nome de arquivo especificado.  
  
     Para obter mais informações, confira [/MANIFESTFILE (Nomear arquivo de manifesto)](/cpp/build/reference/manifestfile-name-manifest-file).  
  
-   **MapExports**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá o vinculador a incluir funções exportadas em um arquivo de mapa.  
  
     Para obter mais informações, confira o argumento `EXPORTS` de [/MAPINFO (Incluir informações no arquivo de mapa)](/cpp/build/reference/mapinfo-include-information-in-mapfile).  
  
-   **MapFileName**  
  
     Parâmetro **String** opcional.  
  
     Altera o nome do arquivo de mapa padrão para o nome de arquivo especificado.  
  
-   **MergedIDLBaseFileName**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome e a extensão de nome do arquivo *.idl*.  
  
     Para obter mais informações, confira [/IDLOUT (Nomear arquivos de saída MIDL)](/cpp/build/reference/idlout-name-midl-output-files).  
  
-   **MergeSections**  
  
     Parâmetro **String** opcional.  
  
     Combina seções em uma imagem. Especifique `from-section=to-section`.  
  
     Para obter mais informações, confira [/MERGE (Combinar seções)](/cpp/build/reference/merge-combine-sections).  
  
-   **MidlCommandFile**  
  
     Parâmetro **String** opcional.  
  
     Especifique o nome de um arquivo que contém opções de linha de comando MIDL.  
  
     Para obter mais informações, confira [/MIDL (Especificar opções de linha de comando MIDL)](/cpp/build/reference/midl-specify-midl-command-line-options).  
  
-   **MinimumRequiredVersion**  
  
     Parâmetro **String** opcional.  
  
     Especifica a versão mínima necessária do subsistema. Os argumentos são números decimais no intervalo de 0 a 65535.  
  
-   **ModuleDefinitionFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome de um [arquivo de definição de módulo](/cpp/build/reference/module-definition-dot-def-files).  
  
     Para obter mais informações, confira [/DEF (Especificar arquivo de definição de módulo)](/cpp/build/reference/def-specify-module-definition-file).  
  
-   **MSDOSStubFileName**  
  
     Parâmetro **String** opcional.  
  
     Anexa o programa stub MS-DOS especificado a um programa Win32.  
  
     Para obter mais informações, confira [/STUB (Nome do arquivo stub do MS-DOS)](/cpp/build/reference/stub-ms-dos-stub-file-name).  
  
-   **NoEntryPoint**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará uma DLL somente de recursos.  
  
     Para obter mais informações, confira [/NOENTRY (Sem ponto de entrada)](/cpp/build/reference/noentry-no-entry-point).  
  
-   **ObjectFiles**  
  
     Parâmetro implícito **Cadeia de Caracteres[]**.  
  
     Especifica os arquivos-objeto vinculados.  
  
-   **OptimizeReferences**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, eliminará a funções e/ou dados que nunca são referenciados.  
  
     Para obter mais informações, consulte o argumento `REF` em [/OPT (Otimizações)](/cpp/build/reference/opt-optimizations).  
  
-   **OutputFile**  
  
     Parâmetro **String** opcional.  
  
     Substitui o nome padrão e o local do programa que o vinculador cria.  
  
     Para obter mais informações, confira [/OUT (Nome do arquivo de saída)](/cpp/build/reference/out-output-file-name).  
  
-   **PerUserRedirection**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true` e Registrar Saída estiverem habilitados, forçará as gravações de Registro para **HKEY_CLASSES_ROOT** a serem redirecionadas para **HKEY_CURRENT_USER**.  
  
-   **PreprocessOutput**  
  
     Parâmetro `ITaskItem[]` opcional.  
  
     Define uma matriz de itens de saída do pré-processador que podem ser consumidos e emitidos por tarefas.  
  
-   **PreventDllBinding**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, indicará ao *Bind.exe* que a imagem vinculada não deve ser associada.  
  
     Para obter mais informações, confira [/ALLOWBIND (Prevenir associação de DLL)](/cpp/build/reference/allowbind-prevent-dll-binding).  
  
-   **Perfil**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, produzirá um arquivo de saída que pode ser usado com o criador de perfil de **Ferramentas de Desempenho**.  
  
     Para obter mais informações, confira [/PROFILE (Criador de perfil das ferramentas de desempenho)](/cpp/build/reference/profile-performance-tools-profiler).  
  
-   **ProfileGuidedDatabase**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome do arquivo *.pgd* que será usado para armazenar informações sobre o programa em execução  
  
     Para obter mais informações, confira [/PGD (Especificar banco de dados para otimizações guiadas por perfil)](/cpp/build/reference/pgd-specify-database-for-profile-guided-optimizations).  
  
-   **ProgramDatabaseFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica um nome para o banco de dados do programa (PDB) que o vinculador cria.  
  
     Para obter mais informações, confira [/PDB (Usar banco de dados de programa)](/cpp/build/reference/pdb-use-program-database).  
  
-   **RandomizedBaseAddress**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, gerará uma imagem executável que pode trocar base aleatoriamente no momento do carregamento usando o recurso *ASLR* (Address Space Layout Randomization) do Windows.  
  
     Para obter mais informações, consulte [/DYNAMICBASE (Usar Aleatorização do Layout de Espaço do Endereço)](/cpp/build/reference/dynamicbase-use-address-space-layout-randomization).  
  
-   **RegisterOutput**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, registrará a saída primária desse build.  
  
-   **SectionAlignment**  
  
     Parâmetro opcional de **Inteiro**.  
  
     Especifica o alinhamento de cada seção dentro do espaço de endereço linear do programa. O valor do parâmetro é um número de unidade de bytes e uma potência de dois.  
  
     Para obter mais informações, confira [/ALIGN (Alinhamento da seção)](/cpp/build/reference/align-section-alignment).  
  
-   **SetChecksum**  
  
     Parâmetro **Boolean** opcional.  
  
     Se ele for `true`, definirá a soma de verificação no cabeçalho de um arquivo *.exe*.  
  
     Para obter mais informações, confira [/RELEASE (Definir a soma de verificação)](/cpp/build/reference/release-set-the-checksum).  
  
-   **ShowProgress**  
  
     Parâmetro **String** opcional.  
  
     Especifica detalhamento de relatórios de progresso da operação de vinculação.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **NotSet** - *\<none>*  
  
    -   **LinkVerbose** - **/VERBOSE**  
  
    -   **LinkVerboseLib** - **/VERBOSE:Lib**  
  
    -   **LinkVerboseICF** - **/VERBOSE:ICF**  
  
    -   **LinkVerboseREF** - **/VERBOSE:REF**  
  
    -   **LinkVerboseSAFESEH** - **/VERBOSE:SAFESEH**  
  
    -   **LinkVerboseCLR** - **/VERBOSE:CLR**  
  
    Para obter mais informações, confira [/VERBOSE (Imprimir mensagens de progresso)](/cpp/build/reference/verbose-print-progress-messages).  
  
-   **Sources**  
  
     Parâmetro `ITaskItem[]` obrigatório.  
  
     Define uma matriz de itens de arquivo de origem do MSBuild que pode ser consumida e emitida por tarefas.  
  
-   **SpecifySectionAttributes**  
  
     Parâmetro **String** opcional.  
  
     Especifica os atributos de uma seção. Isso substitui os atributos que foram definidos quando o arquivo *.obj* da seção foi compilado.  
  
     Para obter mais informações, confira [/SECTION (Especificar atributos de seção)](/cpp/build/reference/section-specify-section-attributes).  
  
-   **StackCommitSize**  
  
     Parâmetro **String** opcional.  
  
     Especifica a quantidade de memória física em cada alocação quando mais memória é alocada.  
  
     Para obter mais informações, confira o argumento `commit` de [/STACK (Alocações da pilha)](/cpp/build/reference/stack-stack-allocations).  
  
-   **StackReserveSize**  
  
     Parâmetro **String** opcional.  
  
     Especifica o tamanho de alocação de pilha total em memória virtual.  
  
     Para obter mais informações, confira o argumento `reserve` de [/STACK (Alocações da pilha)](/cpp/build/reference/stack-stack-allocations).  
  
-   **StripPrivateSymbols**  
  
     Parâmetro **String** opcional.  
  
     Cria um segundo arquivo de banco de dados do programa (PDB) que omite os símbolos que você não deseja distribuir aos seus clientes. Especifique o nome do segundo arquivo PDB.  
  
     Para obter mais informações, confira [/PDBSTRIPPED (Remover símbolos privados)](/cpp/build/reference/pdbstripped-strip-private-symbols).  
  
-   **SubSystem**  
  
     Parâmetro **String** opcional.  
  
     Especifica o ambiente para o executável.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **NotSet** - *\<none>*  
  
    -   **Console** - **/SUBSYSTEM:CONSOLE**  
  
    -   **Windows** - **/SUBSYSTEM:WINDOWS**  
  
    -   **Native** - **/SUBSYSTEM:NATIVE**  
  
    -   **EFI Application** - **/SUBSYSTEM:EFI_APPLICATION**  
  
    -   **EFI Boot Service Driver** - **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**  
  
    -   **EFI ROM** - **/SUBSYSTEM:EFI_ROM**  
  
    -   **EFI Runtime** - **/SUBSYSTEM:EFI_RUNTIME_DRIVER**  
  
    -   **WindowsCE** - **/SUBSYSTEM:WINDOWSCE**  
  
    -   **POSIX** - **/SUBSYSTEM:POSIX**  
  
    Para obter mais informações, confira [/SUBSYSTEM (Especificar subsistema)](/cpp/build/reference/subsystem-specify-subsystem).  
  
-   **SupportNobindOfDelayLoadedDLL**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá o vinculador a não incluir uma IAT (Tabela de Endereços de Importação) associável na imagem final.  
  
     Para obter mais informações, confira o argumento `NOBIND` de [/DELAY (Configurações de importação de carga com atraso)](/cpp/build/reference/delay-delay-load-import-settings).  
  
-   **SupportUnloadOfDelayLoadedDLL**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá a função de ajuda de carregamento atrasado a dar suporte ao descarregamento explícito da DLL.  
  
     Para obter mais informações, confira o argumento `UNLOAD` de [/DELAY (Configurações de importação de carga com atraso)](/cpp/build/reference/delay-delay-load-import-settings).  
  
-   **SuppressStartupBanner**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.  
  
     Para obter mais informações, confira [/NOLOGO (Suprimir faixa de inicialização) (vinculador)](/cpp/build/reference/nologo-suppress-startup-banner-linker).  
  
-   **SwapRunFromCD**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá o sistema operacional a copiar a saída do vinculador para um arquivo de permuta e, em seguida, executará a imagem por meio dele.  
  
     Para obter mais informações, confira o argumento `CD` de [/SWAPRUN (Carregar saída do vinculador no arquivo de permuta)](/cpp/build/reference/swaprun-load-linker-output-to-swap-file). Consulte também o parâmetro **SwapRunFromNET**.  
  
-   **SwapRunFromNET**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, instruirá o sistema operacional a copiar a saída do vinculador para um arquivo de permuta e, em seguida, executará a imagem por meio dele.  
  
     Para obter mais informações, confira o argumento `NET` de [/SWAPRUN (Carregar saída do vinculador no arquivo de permuta)](/cpp/build/reference/swaprun-load-linker-output-to-swap-file). Consulte também o parâmetro **SwapRunFromCD** nesta tabela.  
  
-   **TargetMachine**  
  
     Parâmetro **String** opcional.  
  
     Especifica a plataforma de destino para o programa ou DLL.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **NotSet** - *\<none>*  
  
    -   **MachineARM** - **/MACHINE:ARM**  
  
    -   **MachineEBC** - **/MACHINE:EBC**  
  
    -   **MachineIA64** - **/MACHINE:IA64**  
  
    -   **MachineMIPS** - **/MACHINE:MIPS**  
  
    -   **MachineMIPS16** - **/MACHINE:MIPS16**  
  
    -   **MachineMIPSFPU** - **/MACHINE:MIPSFPU**  
  
    -   **MachineMIPSFPU16** - **/MACHINE:MIPSFPU16**  
  
    -   **MachineSH4** - **/MACHINE:SH4**  
  
    -   **MachineTHUMB** - **/MACHINE:THUMB**  
  
    -   **MachineX64** - **/MACHINE:X64**  
  
    -   **MachineX86** - **/MACHINE:X86**  
  
    Para obter mais informações, confira [/MACHINE (Especificar plataforma de destino)](/cpp/build/reference/machine-specify-target-platform).  
  
-   **TerminalServerAware**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, definirá um sinalizador no campo IMAGE_OPTIONAL_HEADER DllCharacteristics no cabeçalho opcional da imagem do programa. Quando esse sinalizador estiver definido, o servidor Host da Sessão da Área de Trabalho Remota não fará certas alterações no aplicativo.  
  
     Para obter mais informações, confira [/TSAWARE (Criar aplicativo com reconhecimento do servidor Host da Sessão da Área de Trabalho Remota)](/cpp/build/reference/tsaware-create-terminal-server-aware-application).  
  
-   **TrackerLogDirectory**  
  
     Parâmetro **String** opcional.  
  
     Especifica o diretório de log de rastreamento.  
  
-   **TreatLinkerWarningAsErrors**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, fará com que nenhum arquivo de saída seja gerado caso o vinculador gere um aviso.  
  
     Para obter mais informações, confira [/WX (Tratar avisos do vinculador como erros)](/cpp/build/reference/wx-treat-linker-warnings-as-errors).  
  
-   **TurnOffAssemblyGeneration**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, criará uma imagem para o arquivo de saída atual sem um assembly do .NET Framework.  
  
     Para obter mais informações, confira [/NOASSEMBLY (Criar um módulo MSIL)](/cpp/build/reference/noassembly-create-a-msil-module).  
  
-   **TypeLibraryFile**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nome e a extensão de nome do arquivo *.tlb*. Especifique um nome de arquivo ou um caminho e nome de arquivo.  
  
     Para obter mais informações, confira [/TLBOUT (Nomear arquivo .tlb)](/cpp/build/reference/tlbout-name-dot-tlb-file).  
  
-   **TypeLibraryResourceID**  
  
     Parâmetro opcional de **Inteiro**.  
  
     Designa um valor especificado pelo usuário para uma biblioteca de tipos criada pelo vinculador. Especifique um valor de 1 a 65535.  
  
     Para obter mais informações, confira [/TLBID (Especificar ID do recurso para TypeLib)](/cpp/build/reference/tlbid-specify-resource-id-for-typelib).  
  
-   **UACExecutionLevel**  
  
     Parâmetro **String** opcional.  
  
     Especifica o nível de execução solicitado para o aplicativo quando ele é executado com Controle de Conta de Usuário.  
  
     Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
    -   **AsInvoker** - `level='asInvoker'`  
  
    -   **HighestAvailable** - `level='highestAvailable'`  
  
    -   **RequireAdministrator** - `level='requireAdministrator'`  
  
    Para obter mais informações, consulte o argumento `level` de [/MANIFESTUAC (Insere informações UAC no manifesto)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest).  
  
-   **UACUIAccess**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, o aplicativo ignorará os níveis de proteção da interface do usuário e direcionará a entrada para janelas de permissão superior na área de trabalho; caso contrário, `false`.  
  
     Para obter mais informações, consulte o argumento `uiAccess` de [/MANIFESTUAC (Insere informações UAC no manifesto)](/cpp/build/reference/manifestuac-embeds-uac-information-in-manifest).  
  
-   **UseLibraryDependencyInputs**  
  
     Parâmetro **Boolean** opcional.  
  
     Se `true`, as entradas para a ferramenta de biblioteca serão usadas em vez do próprio arquivo de biblioteca ao vincular saídas de biblioteca de dependências do projeto.  
  
-   **Versão**  
  
     Parâmetro **String** opcional.  
  
     Coloque um número de versão no cabeçalho do arquivo *.exe* ou *.dll*. Especifique “`major[.minor]`”. Os argumentos `major` e `minor` são números decimais de 0 a 65535.  
  
     Para obter mais informações, confira [/VERSION (Informações de versão)](/cpp/build/reference/version-version-information).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)
