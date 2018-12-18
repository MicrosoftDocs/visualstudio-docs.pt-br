---
title: Tarefa Link | Microsoft Docs
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
caps.latest.revision: 16
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f2ca9c721567d89bddad4a9ee61639bd3a82f10d
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143444"
---
# <a name="link-task"></a>Tarefa Link
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula a ferramenta de vinculador do Visual C++, link.exe. A ferramenta de vinculador vincula arquivos de objeto e bibliotecas de formato COFF (Common Object File Format) para criar um arquivo executável (.exe) ou uma DLL (biblioteca de vínculo dinâmico). Para obter mais informações, consulte [Opções de Vinculador](http://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **Link**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
- **AdditionalDependencies**  
  
   Parâmetro **String[]** opcional.  
  
   Especifica uma lista de arquivos de entrada para adicionar ao comando.  
  
   Para obter mais informações, consulte [Arquivos de Entrada LINK](http://msdn.microsoft.com/library/bb26fcc5-509a-4620-bc3e-b6c6e603a412).  
  
- **AdditionalLibraryDirectories**  
  
   Parâmetro **String[]** opcional.  
  
   Substitui o caminho da biblioteca de ambiente. Especifique um nome de diretório.  
  
   Para obter mais informações, consulte [/LIBPATH (Libpath Adicional)](http://msdn.microsoft.com/library/7240af0b-9a3d-4d53-8169-2a92cd6958ba).  
  
- **AdditionalManifestDependencies**  
  
   Parâmetro **String[]** opcional.  
  
   Especifica atributos que serão colocados na seção `dependency` do arquivo de manifesto.  
  
   Para obter mais informações, consulte [/MANIFESTDEPENDENCY (Especificar Dependências de Manifesto)](http://msdn.microsoft.com/library/e4b68313-33a2-4c3e-908e-ac2b9f7d6a73). Consulte também os "Arquivos de Configuração do Distribuidor" no site do [MSDN](http://go.microsoft.com/fwlink/?LinkId=737).  
  
- **AdditionalOptions**  
  
   Parâmetro **String** opcional.  
  
   Uma lista de opções de vinculador, conforme especificado na linha de comando. Por exemplo, **"**_/option1 /option2 /option#_". Use esse parâmetro para especificar opções de vinculador que não são representadas por qualquer outro parâmetro de tarefa **Link**.  
  
   Para obter mais informações, consulte [Opções de Vinculador](http://msdn.microsoft.com/library/c1d51b8a-bd23-416d-81e4-900e02b2c129).  
  
- **AddModuleNamesToAssembly**  
  
   Parâmetro **String[]** opcional.  
  
   Adiciona uma referência de módulo a um assembly.  
  
   Para obter mais informações, consulte [/ASSEMBLYMODULE (Adicionar um Módulo MSIL ao Assembly)](http://msdn.microsoft.com/library/67357da8-e4b6-49fd-932c-329a5777f143).  
  
- **AllowIsolation**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, fará com que o sistema operacional realize pesquisas de manifesto e carregamentos. Se `false`, indicará que as DLLs serão carregadas como se não houvesse nenhum manifesto.  
  
   Para obter mais informações, consulte [/ALLOWISOLATION (Pesquisa de Manifesto)](http://msdn.microsoft.com/library/6d41851e-b3c1-4bdf-beaa-031773089d6f).  
  
- **AssemblyDebug**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, emitirá o atributo **DebuggableAttribute** junto com o acompanhamento de informações de depuração e desabilitará otimizações JIT. Se `false`, emitirá o atributo **DebuggableAttribute**, mas desabilitará o acompanhamento de informações de depuração e as otimizações JIT.  
  
   Para obter mais informações, consulte [/ASSEMBLYDEBUG (Adicionar DebuggableAttribute)](http://msdn.microsoft.com/library/94443af3-470c-41d7-83a0-7434563d7982).  
  
- **AssemblyLinkResource**  
  
   Parâmetro **String[]** opcional.  
  
   Cria um link para um recurso do .NET Framework no arquivo de saída; o arquivo de recurso não é colocado no arquivo de saída. Especifique o nome do recurso.  
  
   Para obter mais informações, consulte [/ASSEMBLYLINKRESOURCE (Link para Recurso do .NET Framework)](http://msdn.microsoft.com/library/8b6ad184-1b33-47a4-8513-4803cf915b64).  
  
- **AttributeFileTracking**  
  
   Parâmetro **Booliano** implícito.  
  
   Habilita um acompanhamento de arquivos mais profundo a fim de capturar o comportamento incremental do link. Sempre retorna `true`.  
  
- **BaseAddress**  
  
   Parâmetro **String** opcional.  
  
   Define um endereço básico para o programa ou DLL que está sendo criado. Especifique `{address[,size] | @filename,key}`.  
  
   Para obter mais informações, consulte [/BASE (Endereço Básico)](http://msdn.microsoft.com/library/00b9f6fe-0bd2-4772-a69c-7365eb199069).  
  
- **BuildingInIDE**  
  
   Parâmetro **Boolean** opcional.  
  
   Se for true, indica que o MSBuild é chamado do IDE. Caso contrário, indica que o MSBuild é chamado da linha de comando.  
  
   Esse parâmetro não tem nenhuma opção de vinculador equivalente.  
  
- **CLRImageType**  
  
   Parâmetro **String** opcional.  
  
   Define o tipo de uma imagem CLR (Common Language Runtime).  
  
   Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
  - **Default** - *\<none>*  
  
  - **ForceIJWImage** - **/CLRIMAGETYPE:IJW**  
  
  - **ForcePureILImage** - **/CLRIMAGETYPE:PURE**  
  
  - **ForceSafeILImage** - **/CLRIMAGETYPE:SAFE**  
  
    Para obter mais informações, consulte, [/CLRIMAGETYPE (Especificar Tipo de Imagem CLR)](http://msdn.microsoft.com/library/04c60ee6-9dd7-4391-bc03-6926ad0fa116).  
  
- **CLRSupportLastError**  
  
   Parâmetro **String** opcional.  
  
   Preserva o código de erro mais recente de funções chamadas por meio do mecanismo P/Invoke.  
  
   Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
  - **Enabled** - **/CLRSupportLastError**  
  
  - **Desabilitado** - **/CLRSupportLastError:NO**  
  
  - **SystemDlls** - **/CLRSupportLastError:SYSTEMDLL**  
  
    Para obter mais informações, consulte [/CLRSUPPORTLASTERROR (Preservar Último Código de Erro para Chamadas PInvoke)](http://msdn.microsoft.com/library/b7057990-4154-4b1d-9fc9-6236f7be7575).  
  
- **CLRThreadAttribute**  
  
   Parâmetro **String** opcional.  
  
   Especifica explicitamente o atributo de thread para o ponto de entrada de seu programa CLR.  
  
   Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
  - **DefaultThreadingAttribute** - **/CLRTHREADATTRIBUTE:NONE**  
  
  - **MTAThreadingAttribute** - **/CLRTHREADATTRIBUTE:MTA**  
  
  - **STAThreadingAttribute** - **/CLRTHREADATTRIBUTE:STA**  
  
    Para obter mais informações, consulte [/CLRTHREADATTRIBUTE (Definir Atributo de Thread CLR)](http://msdn.microsoft.com/library/4907e9ef-5031-446c-aecf-0a0b32fae1e8).  
  
- **CLRUnmanagedCodeCheck**  
  
   Parâmetro **Boolean** opcional.  
  
   Especifica se o vinculador aplicará o atributo **SuppressUnmanagedCodeSecurityAttribute** às chamadas P/Invoke geradas pelo vinculador do código gerenciado nas DLLs nativas.  
  
   Para obter mais informações, consulte [/CLRUNMANAGEDCODECHECK (Adicionar SuppressUnmanagedCodeSecurityAttribute)](http://msdn.microsoft.com/library/73abc426-dab0-45e2-be85-0f9a14206cc2).  
  
- **CreateHotPatchableImage**  
  
   Parâmetro **String** opcional.  
  
   Prepara uma imagem para patch instantâneo.  
  
   Especifique um dos valores a seguir, que corresponda a uma opção de vinculador.  
  
  - **Enabled** - **/FUNCTIONPADMIN**  
  
  - **X86Image** - **/FUNCTIONPADMIN:5**  
  
  - **X64Image** - **/FUNCTIONPADMIN:6**  
  
  - **ItaniumImage** - **/FUNCTIONPADMIN:16**  
  
    Para obter mais informações, consulte [/FUNCTIONPADMIN (Cria Imagem Hotpatchable)](http://msdn.microsoft.com/library/25b02c13-1add-4fbd-add9-fcb30eb2cae7).  
  
- **DataExecutionPrevention**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, indicará que um executável foi testado e considerado compatível com o recurso de Prevenção de Execução de Dados do Windows.  
  
   Para obter mais informações, consulte [/NXCOMPAT (Compatível com a Prevenção de Execução de Dados)](http://msdn.microsoft.com/library/5858e7ff-24d3-4ac3-9046-af2c9e220d9b).  
  
- **DelayLoadDLLs**  
  
   Parâmetro **String[]** opcional.  
  
   Esse parâmetro causa um *atraso no carregamento* de DLLs. Especifique o nome de uma DLL para atrasar o carregamento.  
  
   Para obter mais informações, consulte [/DELAYLOAD (Importação de Carga com Atraso)](http://msdn.microsoft.com/library/39ea0f1e-5c01-450f-9c75-2d9761ff9b28).  
  
- **DelaySign**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, assinará parcialmente um assembly. Por padrão, o valor é `false`.  
  
   Para obter mais informações, consulte [/DELAYSIGN (Assinar Parcialmente um Assembly)](http://msdn.microsoft.com/library/15244d30-3ecb-492f-a408-ffe81f38de20).  
  
- **Driver**  
  
   Parâmetro **String** opcional.  
  
   Especifique esse parâmetro para criar um driver de modo de kernel do Windows NT.  
  
   Especifique um dos valores a seguir, cada um correspondente a uma opção de vinculador.  
  
  - **NotSet** - *\<none>*  
  
  - **Driver** - **/Driver**  
  
  - **UpOnly** - **/DRIVER:UPONLY**  
  
  - **WDM** - **/DRIVER:WDM**  
  
    Para obter mais informações, consulte [/DRIVER (Driver de Modo Kernel do Windows NT)](http://msdn.microsoft.com/library/aeee8e28-5d97-40f5-ba16-9f370fe8a1b8).  
  
- **EmbedManagedResourceFile**  
  
   Parâmetro **String[]** opcional.  
  
   Insere um arquivo de recurso em um assembly. Especifique o nome do arquivo de recurso necessário. Como opção, especifique o nome lógico, usado para carregar o recurso e a opção **PRIVADO**, que indica no manifesto do assembly que o arquivo de recurso é privado.  
  
   Para obter mais informações, consulte [/ASSEMBLYRESOURCE (Inserir um Recurso Gerenciado)](http://msdn.microsoft.com/library/0ce6e1fb-921b-4b1b-a59c-d35388d789f2).  
  
- **EnableCOMDATFolding**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, habilitará a dobra COMDAT idêntica.  
  
   Para obter mais informações, consulte o argumento `ICF[= iterations]` de [/OPT (Otimizações)](http://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac).  
  
- **EnableUAC**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, especificará que as informações do UAC (Controle de Conta de Usuário) estão inseridas no manifesto do programa.  
  
   Para obter mais informações, consulte [/MANIFESTUAC (Insere informações UAC no manifesto)](http://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a).  
  
- **EntryPointSymbol**  
  
   Parâmetro **String** opcional.  
  
   Especifica uma função de ponto de entrada como o endereço de início para um arquivo .exe ou DLL. Especifique um nome de função como valor do parâmetro.  
  
   Para obter mais informações, consulte [/ENTRY (Símbolo de Ponto de Entrada)](http://msdn.microsoft.com/library/26c62ba2-4f52-4882-a7bd-7046a0abf445).  
  
- **FixedBaseAddress**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará um programa ou DLL que pode ser carregado somente em seu endereço básico preferido.  
  
   Para obter mais informações, consulte [/FIXED (Endereço Básico Fixo)](http://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5).  
  
- **ForceFileOutput**  
  
   Parâmetro **String** opcional.  
  
   Instrui o vinculador a criar um arquivo válido .exe ou DLL mesmo que um símbolo esteja referenciado, mas não definido, ou seja, definido várias vezes.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Enabled** - **/FORCE**  
  
  - **MultiplyDefinedSymbolOnly** - **/FORCE:MULTIPLE**  
  
  - **UndefinedSymbolOnly** - **/FORCE:UNRESOLVED**  
  
    Para obter mais informações, consulte [/FORCE (Forçar Saída de Arquivo)](http://msdn.microsoft.com/library/b1e9a218-a5eb-4e60-a4a4-65b4be15e5da).  
  
- **ForceSymbolReferences**  
  
   Parâmetro **String[]** opcional.  
  
   Esse parâmetro instrui o vinculador a adicionar um símbolo especificado à tabela de símbolos.  
  
   Para obter mais informações, consulte [/INCLUDE (Forçar Referências de Símbolo)](http://msdn.microsoft.com/library/4a039677-360a-480f-bd0b-448e239b449c).  
  
- **FunctionOrder**  
  
   Parâmetro **String** opcional.  
  
   Esse parâmetro otimiza seu programa colocando as funções empacotadas (COMDATs) especificadas na imagem em uma ordem predeterminada.  
  
   Para obter mais informações, consulte [/ORDER (Colocar Funções na Ordem)](http://msdn.microsoft.com/library/ecf5eb3e-e404-4e86-9a91-4e5ec157261a).  
  
- **GenerateDebugInformation**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará informações de depuração para o arquivo .exe ou DLL.  
  
   Para obter mais informações, consulte [/DEBUG (Gerar Informações de Depuração)](http://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103).  
  
- **GenerateManifest**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará um arquivo de manifesto lado a lado.  
  
   Para obter mais informações, consulte [/MANIFEST (Criar Manifesto do Assembly Lado a Lado)](http://msdn.microsoft.com/library/98c52e1e-712c-4f49-b149-4d0a3501b600).  
  
- **GenerateMapFile**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará um *arquivo de mapa*. A extensão de nome de arquivo do arquivo de mapa é .map.  
  
   Para obter mais informações, consulte [/MAP (Gerar Mapfile)](http://msdn.microsoft.com/library/9ccce53d-4e36-43da-87b0-7603ddfdea63).  
  
- **HeapCommitSize**  
  
   Parâmetro **String** opcional.  
  
   Especifica a quantidade de memória física no heap a se alocar por vez.  
  
   Para obter mais informações, consulte o argumento `commit` em [/HEAP (Definir Tamanho do Heap)](http://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da). Consulte também o parâmetro **HeapReserveSize**.  
  
- **HeapReserveSize**  
  
   Parâmetro **String** opcional.  
  
   Especifica a alocação de heap total na memória virtual.  
  
   Para obter mais informações, consulte o argumento `reserve` em [/HEAP (Definir Tamanho do Heap)](http://msdn.microsoft.com/library/a3f71927-7f1d-492c-9fdb-dfccb1a043da). Consulte também o parâmetro **HeapCommitSize** nesta tabela.  
  
- **IgnoreAllDefaultLibraries**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá o vinculador a remover uma ou mais bibliotecas padrão da lista de bibliotecas pesquisadas ao resolver referências externas.  
  
   Para obter mais informações, consulte [/NODEFAULTLIB (Ignorar Bibliotecas)](http://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e).  
  
- **IgnoreEmbeddedIDL**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, especificará que qualquer atributo IDL em código-fonte não deve ser processado em um arquivo .idl.  
  
   Para obter mais informações, consulte [/IGNOREIDL (Não Processar Atributos em MIDL)](http://msdn.microsoft.com/library/29514098-6a1c-4317-af2f-1dc268972780).  
  
- **IgnoreImportLibrary**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, especificará que a biblioteca de importações gerada por esta configuração não deve ser importada para os projetos dependentes.  
  
   Esse parâmetro não corresponde a uma opção de vinculador.  
  
- **IgnoreSpecificDefaultLibraries**  
  
   Parâmetro **String[]** opcional.  
  
   Especifica um ou mais nomes de bibliotecas padrão a serem ignoradas. Separe várias bibliotecas usando ponto e vírgula.  
  
   Para obter mais informações, consulte [/NODEFAULTLIB (Ignorar Bibliotecas)](http://msdn.microsoft.com/library/7270b673-6711-468e-97a7-c2925ac2be6e).  
  
- **ImageHasSafeExceptionHandlers**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, o vinculador produzirá uma imagem somente se também puder produzir uma tabela de manipuladores de exceção segura da imagem.  
  
   Para obter mais informações, consulte [/SAFESEH (Imagem Tem Manipuladores de Exceções Seguros)](http://msdn.microsoft.com/library/7722ff99-b833-4c65-a855-aaca902ffcb7).  
  
- **ImportLibrary**  
  
   Um nome de biblioteca de importação especificado pelo usuário que substitui o nome da biblioteca padrão.  
  
   Para obter mais informações, consulte [/IMPLIB (Nomear Biblioteca de Importações)](http://msdn.microsoft.com/library/fe8f71ab-7055-41b5-8ef8-2b97cfa4a432).  
  
- **KeyContainer**  
  
   Parâmetro **String** opcional.  
  
   Contêiner que contém a chave para um assembly assinado.  
  
   Para obter mais informações, consulte [/KEYCONTAINER (Especificar um Contêiner de Chave para Assinar um Assembly)](http://msdn.microsoft.com/library/94882d12-b77a-49c7-96d0-18a31aee001e). Consulte também o parâmetro **KeyFile** nesta tabela.  
  
- **KeyFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica um arquivo que contém a chave para um assembly assinado.  
  
   Para obter mais informações, consulte [/KEYFILE (Especificar Chave ou Par de Chaves para Assinar um Assembly)](http://msdn.microsoft.com/library/9b71f8c0-541c-4fe5-a0c7-9364f42ecb06). Consulte também o parâmetro **KeyContainer**.  
  
- **LargeAddressAware**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, o aplicativo poderá identificar endereços maiores do que 2 gigabytes.  
  
   Para obter mais informações, consulte [/LARGEADDRESSAWARE (Identificar Endereços Grandes)](http://msdn.microsoft.com/library/a29756c8-e893-47a9-9750-1f0d25359385).  
  
- **LinkDLL**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará uma DLL como o arquivo de saída principal.  
  
   Para obter mais informações, consulte [/DLL (Compilar uma DLL)](http://msdn.microsoft.com/library/c7685aec-31d0-490f-9503-fb5171a23609).  
  
- **LinkErrorReporting**  
  
   Parâmetro **String** opcional.  
  
   Permite que você forneça informações de ICE (erro interno do compilador) diretamente à Microsoft.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NoErrorReport** - **/ERRORREPORT:NONE**  
  
  - **PromptImmediately** - **/ERRORREPORT:PROMPT**  
  
  - **QueueForNextLogin** - **/ERRORREPORT:QUEUE**  
  
  - **SendErrorReport** - **/ERRORREPORT:SEND**  
  
    Para obter mais informações, consulte [/ERRORREPORT (Relatório de Erros Internos do Vinculador)](http://msdn.microsoft.com/library/f5fab595-a2f1-4eb0-ab5c-1c0fbd3d8c28).  
  
- **LinkIncremental**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, habilitará a vinculação incremental.  
  
   Para obter mais informações, consulte [/INCREMENTAL (Vincular de Maneira Incremental)](http://msdn.microsoft.com/library/135656ff-94fa-4ad4-a613-22e1a2a5d16b).  
  
- **LinkLibraryDependencies**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, especificará que as saídas de biblioteca das dependências do projeto serão vinculadas automaticamente.  
  
   Esse parâmetro não corresponde a uma opção de vinculador.  
  
- **LinkStatus**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, especificará que o vinculador deve exibir um indicador de progresso que mostrará o percentual concluído do link.  
  
   Para obter mais informações, consulte o argumento `STATUS` de [/LTCG (Geração de Código Durante o Tempo de Vinculação)](http://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2).  
  
- **LinkTimeCodeGeneration**  
  
   Parâmetro **String** opcional.  
  
   Especifica opções para a otimização guiada por perfil.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Default** - *\<none>*  
  
  - **UseLinkTimeCodeGeneration** - **/LTCG**  
  
  - **PGInstrument** - **/LTCG:PGInstrument**  
  
  - **PGOptimization** - **/LTCG:PGOptimize**  
  
  - **PGUpdate**  
  
     \- **/LTCG:PGUpdate**  
  
    Para obter mais informações, consulte [/LTCG (Geração de Código Durante o Tempo de Vinculação)](http://msdn.microsoft.com/library/788c6f52-fdb8-40c2-90af-4026ea2cf2e2).  
  
- **ManifestFile**  
  
   Parâmetro **String** opcional.  
  
   Altera o nome do arquivo de manifesto padrão para o nome de arquivo especificado.  
  
   Para obter mais informações, consulte [/MANIFESTFILE (Nomear Arquivo de Manifesto)](http://msdn.microsoft.com/library/befa5ab2-a9cf-4c9b-969a-e7b4a930f08d).  
  
- **MapExports**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá o vinculador a incluir funções exportadas em um arquivo de mapa.  
  
   Para obter mais informações, consulte o argumento `EXPORTS` de [/MAPINFO (Incluir Informações em Mapfile)](http://msdn.microsoft.com/library/533d2bce-f9b7-4fea-ae1c-0b4864c9d10b).  
  
- **MapFileName**  
  
   Parâmetro **String** opcional.  
  
   Altera o nome do arquivo de mapa padrão para o nome de arquivo especificado.  
  
- **MergedIDLBaseFileName**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nome de arquivo e a extensão de nome de arquivo .idl.  
  
   Para obter mais informações, consulte [/IDLOUT (Nomear Arquivos de Saída MIDL)](http://msdn.microsoft.com/library/10d00a6a-85b4-4de1-8732-e422c6931509).  
  
- **MergeSections**  
  
   Parâmetro **String** opcional.  
  
   Combina seções em uma imagem. Especifique `from-section=to-section`.  
  
   Para obter mais informações, consulte [/MERGE (Combinar Seções)](http://msdn.microsoft.com/library/10fb20c2-0b3f-4c8d-98a8-f69aedf03d52).  
  
- **MidlCommandFile**  
  
   Parâmetro **String** opcional.  
  
   Especifique o nome de um arquivo que contém opções de linha de comando MIDL.  
  
   Para obter mais informações, consulte [/MIDL (Especificar Opções de Linha de Comando MIDL)](http://msdn.microsoft.com/library/22dc259e-b34c-4ed3-a380-4beb734482c1).  
  
- **MinimumRequiredVersion**  
  
   Parâmetro **String** opcional.  
  
   Especifica a versão mínima necessária do subsistema. Os argumentos são números decimais no intervalo de 0 a 65535.  
  
- **ModuleDefinitionFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nome de um [arquivo de definição de módulo](http://msdn.microsoft.com/library/08c0bc28-c5d2-47aa-9624-7fc68bcaa4d8).  
  
   Para obter mais informações, consulte [/DEF (Especificar Arquivo de Definição de Módulo)](http://msdn.microsoft.com/library/6497fa68-65f0-48ca-8f66-b87166fc631a).  
  
- **MSDOSStubFileName**  
  
   Parâmetro **String** opcional.  
  
   Anexa o programa stub MS-DOS especificado a um programa Win32.  
  
   Para obter mais informações, consulte [/STUB (Nome do Arquivo Stub do MS-DOS)](http://msdn.microsoft.com/library/65221ffe-4f9a-4a14-ac69-3cfb79b40b5f).  
  
- **NoEntryPoint**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará uma DLL somente de recursos.  
  
   Para obter mais informações, consulte [/NOENTRY (Sem Ponto de Entrada)](http://msdn.microsoft.com/library/0214dd41-35ad-43ab-b892-e636e038621a).  
  
- **ObjectFiles**  
  
   Parâmetro implícito **Cadeia de Caracteres[]**.  
  
   Especifica os arquivos-objeto vinculados.  
  
- **OptimizeReferences**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, eliminará a funções e/ou dados que nunca são referenciados.  
  
   Para obter mais informações, consulte o argumento `REF` em [/OPT (Otimizações)](http://msdn.microsoft.com/library/8f229863-5f53-48a8-9478-243a647093ac).  
  
- **OutputFile**  
  
   Parâmetro **String** opcional.  
  
   Substitui o nome padrão e o local do programa que o vinculador cria.  
  
   Para obter mais informações, consulte [/OUT (Nome do Arquivo de Saída)](http://msdn.microsoft.com/library/976210a4-e51f-4cfb-af5e-c16344455834).  
  
- **PerUserRedirection**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true` e Registrar Saída estiverem habilitados, forçará as gravações de Registro para **HKEY_CLASSES_ROOT** a serem redirecionadas para **HKEY_CURRENT_USER**.  
  
- **PreprocessOutput**  
  
   Parâmetro `ITaskItem[]` opcional.  
  
   Define uma matriz de itens de saída do pré-processador que podem ser consumidos e emitidos por tarefas.  
  
- **PreventDllBinding**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, indicará ao Bind.exe que a imagem vinculada não deve ser associada.  
  
   Para obter mais informações, consulte [/ALLOWBIND (Evitar Associação de DLL)](http://msdn.microsoft.com/library/30e37e24-12e4-407e-988a-39d357403598).  
  
- **Perfil**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, produzirá um arquivo de saída que pode ser usado com o criador de perfil de **Ferramentas de Desempenho**.  
  
   Para obter mais informações, consulte [/PROFILE (Criador de Perfil das Ferramentas de Desempenho)](http://msdn.microsoft.com/library/e676baa1-5063-47a3-a357-ba0d1f0d1699).  
  
- **ProfileGuidedDatabase**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nome do arquivo .pgd que será usado para armazenar informações sobre o programa em execução  
  
   Para obter mais informações, consulte [/PGD (Especificar Banco de Dados para Otimizações Orientadas por Perfil)](http://msdn.microsoft.com/library/9f312498-493b-461f-886f-92652257e443).  
  
- **ProgramDatabaseFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica um nome para o banco de dados do programa (PDB) que o vinculador cria.  
  
   Para obter mais informações, consulte [/PDB (Usar Banco de Dados do Programa)](http://msdn.microsoft.com/library/d23db0ce-10cb-427a-bc60-d6b2a852723d).  
  
- **RandomizedBaseAddress**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, gerará uma imagem executável que pode trocar base aleatoriamente no momento do carregamento usando o recurso *ASLR* (Address Space Layout Randomization) do Windows.  
  
   Para obter mais informações, consulte [/DYNAMICBASE (Usar Aleatorização do Layout de Espaço do Endereço)](http://msdn.microsoft.com/library/6c0ced8e-fe9c-4b63-b956-eb8a55fbceb2).  
  
- **RegisterOutput**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, registrará a saída primária desse build.  
  
- **SectionAlignment**  
  
   Parâmetro opcional de **Inteiro**.  
  
   Especifica o alinhamento de cada seção dentro do espaço de endereço linear do programa. O valor do parâmetro é um número de unidade de bytes e uma potência de dois.  
  
   Para obter mais informações, consulte [/ALIGN (Alinhamento da Seção)](http://msdn.microsoft.com/library/f2f8ac24-e90e-4bea-8205-f2960a3b1740).  
  
- **SetChecksum**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, definirá a soma de verificação no cabeçalho de um arquivo .exe.  
  
   Para obter mais informações, consulte [/RELEASE (Definir a Soma de Verificação)](http://msdn.microsoft.com/library/93bcadf4-29ac-4824-914b-6997e3751d22).  
  
- **ShowProgress**  
  
   Parâmetro **String** opcional.  
  
   Especifica detalhamento de relatórios de progresso da operação de vinculação.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NotSet** - *\<none>*  
  
  - **LinkVerbose** - **/VERBOSE**  
  
  - **LinkVerboseLib** - **/VERBOSE:Lib**  
  
  - **LinkVerboseICF** - **/VERBOSE:ICF**  
  
  - **LinkVerboseREF** - **/VERBOSE:REF**  
  
  - **LinkVerboseSAFESEH** - **/VERBOSE:SAFESEH**  
  
  - **LinkVerboseCLR** - **/VERBOSE:CLR**  
  
    Para obter mais informações, consulte [/VERBOSE (Imprimir Mensagens de Progresso)](http://msdn.microsoft.com/library/9c347d98-4c37-4724-a39e-0983934693ab).  
  
- **Sources**  
  
   Parâmetro `ITaskItem[]` obrigatório.  
  
   Define uma matriz de itens de arquivo de origem do MSBuild que pode ser consumida e emitida por tarefas.  
  
- **SpecifySectionAttributes**  
  
   Parâmetro **String** opcional.  
  
   Especifica os atributos de uma seção. Isso substitui os atributos que foram definidos quando o arquivo .obj para a seção foi compilado.  
  
   Para obter mais informações, consulte [/SECTION (Especificar Atributos de Seção)](http://msdn.microsoft.com/library/92b69d81-e421-462e-b46f-7d0dff9b9d16).  
  
- **StackCommitSize**  
  
   Parâmetro **String** opcional.  
  
   Especifica a quantidade de memória física em cada alocação quando mais memória é alocada.  
  
   Para obter mais informações, consulte o argumento `commit` de [/STACK (Alocações da Pilha)](http://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c).  
  
- **StackReserveSize**  
  
   Parâmetro **String** opcional.  
  
   Especifica o tamanho de alocação de pilha total em memória virtual.  
  
   Para obter mais informações, consulte o argumento `reserve` de [/STACK (Alocações da Pilha)](http://msdn.microsoft.com/library/73283660-e4bd-47cc-b5ca-04c5d739034c).  
  
- **StripPrivateSymbols**  
  
   Parâmetro **String** opcional.  
  
   Cria um segundo arquivo de banco de dados do programa (PDB) que omite os símbolos que você não deseja distribuir aos seus clientes. Especifique o nome do segundo arquivo PDB.  
  
   Para obter mais informações, consulte [/PDBSTRIPPED (Remover Símbolos Privados)](http://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55).  
  
- **SubSystem**  
  
   Parâmetro **String** opcional.  
  
   Especifica o ambiente para o executável.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NotSet** - *\<none>*  
  
  - **Console** - **/SUBSYSTEM:CONSOLE**  
  
  - **Windows** - **/SUBSYSTEM:WINDOWS**  
  
  - **Native** - **/SUBSYSTEM:NATIVE**  
  
  - **EFI Application** - **/SUBSYSTEM:EFI_APPLICATION**  
  
  - **EFI Boot Service Driver** - **/SUBSYSTEM:EFI_BOOT_SERVICE_DRIVER**  
  
  - **EFI ROM** - **/SUBSYSTEM:EFI_ROM**  
  
  - **EFI Runtime** - **/SUBSYSTEM:EFI_RUNTIME_DRIVER**  
  
  - **WindowsCE** - **/SUBSYSTEM:WINDOWSCE**  
  
  - **POSIX** - **/SUBSYSTEM:POSIX**  
  
    Para obter mais informações, consulte [/SUBSYSTEM (Especificar Subsistema)](http://msdn.microsoft.com/library/d7b133cf-cf22-4da8-ab46-6552702c0b9b).  
  
- **SupportNobindOfDelayLoadedDLL**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá o vinculador a não incluir uma IAT (Tabela de Endereços de Importação) associável na imagem final.  
  
   Para obter mais informações, consulte o argumento `NOBIND` de [/DELAY (Configurações de Importação de Carga com Atraso)](http://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c).  
  
- **SupportUnloadOfDelayLoadedDLL**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá a função de ajuda de carregamento atrasado a dar suporte ao descarregamento explícito da DLL.  
  
   Para obter mais informações, consulte o argumento `UNLOAD` de [/DELAY (Configurações de Importação de Carga com Atraso)](http://msdn.microsoft.com/library/9334b332-cc58-4dae-b10f-a4c75972d50c).  
  
- **SuppressStartupBanner**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.  
  
   Para obter mais informações, consulte [/NOLOGO (Suprimir Faixa de Inicialização) (Vinculador)](http://msdn.microsoft.com/library/3b20dddd-eca6-4545-a331-9f70bf720197).  
  
- **SwapRunFromCD**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá o sistema operacional a copiar a saída do vinculador para um arquivo de permuta e, em seguida, executará a imagem por meio dele.  
  
   Para obter mais informações, consulte o argumento `CD` de [/SWAPRUN (Carregar Saída do Vinculador para Trocar Arquivo)](http://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683). Consulte também o parâmetro **SwapRunFromNET**.  
  
- **SwapRunFromNET**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, instruirá o sistema operacional a copiar a saída do vinculador para um arquivo de permuta e, em seguida, executará a imagem por meio dele.  
  
   Para obter mais informações, consulte o argumento `NET` de [/SWAPRUN (Carregar Saída do Vinculador para Trocar Arquivo)](http://msdn.microsoft.com/library/4a1e7f46-4399-4161-8dfc-d6a71beaf683). Consulte também o parâmetro **SwapRunFromCD** nesta tabela.  
  
- **TargetMachine**  
  
   Parâmetro **String** opcional.  
  
   Especifica a plataforma de destino para o programa ou DLL.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NotSet** - *\<none>*  
  
  - **MachineARM** - **/MACHINE:ARM**  
  
  - **MachineEBC** - **/MACHINE:EBC**  
  
  - **MachineIA64** - **/MACHINE:IA64**  
  
  - **MachineMIPS** - **/MACHINE:MIPS**  
  
  - **MachineMIPS16** - **/MACHINE:MIPS16**  
  
  - **MachineMIPSFPU** - **/MACHINE:MIPSFPU**  
  
  - **MachineMIPSFPU16** - **/MACHINE:MIPSFPU16**  
  
  - **MachineSH4** - **/MACHINE:SH4**  
  
  - **MachineTHUMB** - **/MACHINE:THUMB**  
  
  - **MachineX64** - **/MACHINE:X64**  
  
  - **MachineX86** - **/MACHINE:X86**  
  
    Para obter mais informações, consulte [/MACHINE (Especificar Plataforma de Destino)](http://msdn.microsoft.com/library/8d41bf4b-7e53-4ab9-9085-d852b08d31c2).  
  
- **TerminalServerAware**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, definirá um sinalizador no campo IMAGE_OPTIONAL_HEADER DllCharacteristics no cabeçalho opcional da imagem do programa. Quando esse sinalizador estiver definido, o servidor Host da Sessão da Área de Trabalho Remota não fará certas alterações no aplicativo.  
  
   Para obter mais informações, consulte [/TSAWARE (Criar Aplicativo com Reconhecimento do servidor Host da Sessão da Área de Trabalho Remota)](http://msdn.microsoft.com/library/fe1c1846-de5b-4839-b562-93fbfe36cd29).  
  
- **TrackerLogDirectory**  
  
   Parâmetro **String** opcional.  
  
   Especifica o diretório de log de rastreamento.  
  
- **TreatLinkerWarningAsErrors**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, fará com que nenhum arquivo de saída seja gerado caso o vinculador gere um aviso.  
  
   Para obter mais informações, consulte [/WX (Tratar Avisos do Vinculador como Erros)](http://msdn.microsoft.com/library/e4ba97c7-93f7-43ae-a4bb-d866790926c9).  
  
- **TurnOffAssemblyGeneration**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, criará uma imagem para o arquivo de saída atual sem um assembly do .NET Framework.  
  
   Para obter mais informações, consulte [/NOASSEMBLY (Criar um Módulo MSIL)](http://msdn.microsoft.com/library/3cea4e70-f451-4395-a626-1930b1b127fe).  
  
- **TypeLibraryFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nome de arquivo e a extensão de nome de arquivo .tlb. Especifique um nome de arquivo ou um caminho e nome de arquivo.  
  
   Para obter mais informações, consulte [/TLBOUT (Nomear Arquivo .TLB)](http://msdn.microsoft.com/library/0df6d078-2e48-46c9-a1a5-02674d85dce8).  
  
- **TypeLibraryResourceID**  
  
   Parâmetro opcional de **Inteiro**.  
  
   Designa um valor especificado pelo usuário para uma biblioteca de tipos criada pelo vinculador. Especifique um valor de 1 a 65535.  
  
   Para obter mais informações, consulte [/TLBID (Especificar ID do Recurso para TypeLib)](http://msdn.microsoft.com/library/434b28a2-4656-4d52-ac82-8b18bf486fb2).  
  
- **UACExecutionLevel**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nível de execução solicitado para o aplicativo quando ele é executado com Controle de Conta de Usuário.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **AsInvoker** - `level='asInvoker'`  
  
  - **HighestAvailable** - `level='highestAvailable'`  
  
  - **RequireAdministrator** - `level='requireAdministrator'`  
  
    Para obter mais informações, consulte o argumento `level` de [/MANIFESTUAC (Insere informações UAC no manifesto)](http://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a).  
  
- **UACUIAccess**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, o aplicativo ignorará os níveis de proteção da interface do usuário e direcionará a entrada para janelas de permissão superior na área de trabalho; caso contrário, `false`.  
  
   Para obter mais informações, consulte o argumento `uiAccess` de [/MANIFESTUAC (Insere informações UAC no manifesto)](http://msdn.microsoft.com/library/2d243c39-fa13-493c-b56f-d0d972a1603a).  
  
- **UseLibraryDependencyInputs**  
  
   Parâmetro **Boolean** opcional.  
  
   Se `true`, as entradas para a ferramenta de biblioteca serão usadas em vez do próprio arquivo de biblioteca ao vincular saídas de biblioteca de dependências do projeto.  
  
- **Versão**  
  
   Parâmetro **String** opcional.  
  
   Coloque um número de versão no cabeçalho do arquivo .dll ou .exe. Especifique “`major[.minor]`”. Os argumentos `major` e `minor` são números decimais de 0 a 65535.  
  
   Para obter mais informações, consulte [/VERSION (Informações de Versão)](http://msdn.microsoft.com/library/b86d0e86-dca6-4316-aee2-d863ccb9f223).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



