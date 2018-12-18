---
title: Tarefa CL | Microsoft Docs
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
- VC.Project.VCCLCompilerTool.UseUnicodeForAssemblerListing
- vc.task.cl
- VC.Project.VCCLCompilerTool.TreatSpecificWarningsAsErrors
- VC.Project.VCCLCompilerTool.CreateHotpatchableImage
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- MSBuild (Visual C++), CL task
- CL task (MSBuild (Visual C++))
ms.assetid: 651ba971-b755-4f03-a549-4816beb3cc0d
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fb9b6924f5d11e3d857308e3a1bcf1e1644f78bc
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50220242"
---
# <a name="cl-task"></a>Tarefa CL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Encapsula a ferramenta do compilador Visual C++, cl.exe. O compilador produz arquivos executáveis (.exe), arquivos de biblioteca de vínculo dinâmico (.dll) ou arquivos de módulo de código (.netmodule). Para obter mais informações, consulte [Opções do compilador](http://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c).  
  
## <a name="parameters"></a>Parâmetros  
 A tabela a seguir descreve os parâmetros da tarefa **CL**. A maioria dos parâmetros de tarefa e alguns conjuntos de parâmetros correspondem a uma opção de linha de comando.  
  
- **AdditionalIncludeDirectories**  
  
   Parâmetro String[] opcional.  
  
   Adiciona um diretório à lista de diretórios que são pesquisados para arquivos de inclusão.  
  
   Para obter mais informações, consulte [/I (diretórios de inclusão adicionais)](http://msdn.microsoft.com/library/3e9add2a-5ed8-4d15-ad79-5b411e313a49).  
  
- **AdditionalOptions**  
  
   Parâmetro String opcional.  
  
   Uma lista de opções de linha de comando. Por exemplo, "/*option1* /*option2* /*option#*". Use esse parâmetro para especificar opções de linha de comando não representadas por nenhum outro parâmetro da tarefa.  
  
   Para obter mais informações, consulte [Opções do compilador](http://msdn.microsoft.com/library/ed3376c8-bef4-4c9a-80e9-3b5da232644c).  
  
- **AdditionalUsingDirectories** parâmetro opcional String [].  
  
   Especifica um diretório em que o compilador pesquisará para resolver referências de arquivo passadas para diretiva **#using**.  
  
   Para obter mais informações, consulte [/AI (Especificar Diretórios de Metadados)](http://msdn.microsoft.com/library/fb9c1846-504c-4a3b-bb39-c8696de32f6f).  
  
- **AlwaysAppend**  
  
   Parâmetro String opcional.  
  
   Uma cadeia de caracteres sempre é emitida na linha de comando. Seu valor padrão é "**/c**".  
  
- **AssemblerListingLocation**  
  
   Cria um arquivo de listagem que contém o código do assembly.  
  
   Para obter mais informações, consulte a opção **/Fa** em [/FA, /Fa (Arquivo de Listagem)](http://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402).  
  
- **AssemblerOutput**  
  
   Parâmetro String opcional.  
  
   Cria um arquivo de listagem que contém o código do assembly.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NoListing** - *\<none>*  
  
  - **AssemblyCode** - **/FA**  
  
  - **AssemblyAndMachineCode** - **/FAc**  
  
  - **AssemblyAndSourceCode** - **/FAs**  
  
  - **All** - **/FAcs**  
  
    Para obter mais informações, consulte as opções **/FA**, **/FAc**, **/FAs** e **/FAcs** opções em [/FA, /Fa (Arquivo de Listagem)](http://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402).  
  
- **BasicRuntimeChecks**  
  
   Parâmetro String opcional.  
  
   Habilita e desabilita o recurso de verificações de erro em tempo de execução, em conjunto com o pragma [runtime_checks](http://msdn.microsoft.com/library/ae50b43f-f88d-47ad-a2db-3389e9e7df5b).  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Default** -                          *\<none>*  
  
  - **StackFrameRuntimeCheck** - **/RTCs**  
  
  - **UninitializedLocalUsageCheck** - **/RTCu**  
  
  - **EnableFastChecks** -                          **/RTC1**  
  
    Para obter mais informações, consulte [/RTC (verificações de erro em tempo de execução)](http://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368).  
  
- **BrowseInformation**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, criará um arquivo de informações de procura.  
  
   Para obter mais informações, consulte a opção **/FR** em [/FR, /Fr (criar Arquivo .Sbr)](http://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896).  
  
- **BrowseInformationFile**  
  
   Parâmetro String opcional.  
  
   Especifica um nome de arquivo para o arquivo de informações de procura.  
  
   Para obter mais informações, consulte o parâmetro **BrowseInformation** nessa tabela e também consulte [/FR, /Fr (criar Arquivo .Sbr)](http://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896).  
  
- **BufferSecurityCheck**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, detectará alguns estouros de buffer que substituem o endereço de retorno, uma técnica comum para explorar o código que não impõe restrições de tamanho do buffer.  
  
   Para obter mais informações, consulte [/GS (verificação de segurança do buffer)](http://msdn.microsoft.com/library/8d8a5ea1-cd5e-42e1-bc36-66e1cd7e731e).  
  
- **BuildingInIDE**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, indicará que **MSBuild** é invocado pelo IDE. Caso contrário, **MSBuild** será invocado na linha de comando.  
  
- **CallingConvention**  
  
   Parâmetro String opcional.  
  
   Especifica a convenção de chamada, que determina a ordem na qual os argumentos de função são colocados na pilha, se a função do chamador ou a função chamada remove os argumentos da pilha no final da chamada e a convenção de decoração de nome que o compilador usa para identificar funções individuais.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Cdecl** - **/Gd**  
  
  - **FastCall** -                          **/Gr**  
  
  - **StdCall** -                          **/Gz**  
  
    Para obter mais informações, consulte [/Gd, /Gr, /Gv, /Gz (convenção de chamada)](http://msdn.microsoft.com/library/fd3110cb-2d77-49f2-99cf-a03f9ead00a3).  
  
- **CompileAs**  
  
   Parâmetro String opcional.  
  
   Especifica se o arquivo de entrada deve ser compilado como um arquivo de origem C ou C++.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Default** - *\<none>*  
  
  - **CompileAsC** - **/TC**  
  
  - **CompileAsCpp** - **/TP**  
  
    Para obter mais informações, consulte [/Tc, /Tp, /TC, /TP (especificar o tipo de arquivo de origem)](http://msdn.microsoft.com/library/7d9d0a65-338b-427c-8b48-fff30e2f9d2b).  
  
- **CompileAsManaged**  
  
   Parâmetro String opcional.  
  
   Permite que aplicativos e componentes usem recursos do CLR (Common Language Runtime).  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **false** - *\<none>*  
  
  - **true** - **/clr**  
  
  - **Pure** - **/clr:pure**  
  
  - **Safe** - **/clr:safe**  
  
  - **OldSyntax** - **/clr:oldSyntax**  
  
    Para obter mais informações, consulte [/clr (compilação de Common Language Runtime)](http://msdn.microsoft.com/library/fec5a8c0-40ec-484c-a213-8dec918c1d6c).  
  
- **CreateHotpatchableImage**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, informará ao compilador para preparar uma imagem para *aplicação de patch sob demanda*. Esse parâmetro garante que a primeira instrução de cada função tenha dois bytes, o que é necessário para aplicação de patch sob demanda.  
  
   Para obter mais informações, consulte [/hotpatch (criar imagem capaz de aplicar patches sob demanda)](http://msdn.microsoft.com/library/aad539b6-c053-4c78-8682-853d98327798).  
  
- **DebugInformationFormat**  
  
   Parâmetro String opcional.  
  
   Selecione o tipo de informações de depuração criadas para seu programa e se essas informações são mantidas em arquivos de objeto (.obj) ou em um banco de dados de programa (PDB).  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **OldStyle** - **/Z7**  
  
  - **ProgramDatabase** - **/Zi**  
  
  - **EditAndContinue** - **/ZI**  
  
    Para obter mais informações, consulte [/Z7, /Zd, /Zi, /ZI (formato de informação de depuração)](http://msdn.microsoft.com/library/ce9fa7e1-0c9b-47e3-98ea-26d1a16257c8).  
  
- **DisableLanguageExtensions**  
  
   Parâmetro Boolean opcional.  
  
   Se **true**, dirá ao compilador para emitir um erro para construções de linguagem que não sejam compatíveis com ANSI C ou ANSI C++.  
  
   Para obter mais informações, consulte a opção **/Za** em [/Za, /Ze (Desabilitar Extensões de Idioma)](http://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2).  
  
- **DisableSpecificWarnings**  
  
   Parâmetro String[] opcional.  
  
   Desabilita os números de aviso especificados em uma lista delimitada por ponto e vírgula.  
  
   Para obter mais informações, consulte a opção `/wd` em [/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Nível de Aviso)](http://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f).  
  
- **EnableEnhancedInstructionSet**  
  
   Parâmetro String opcional.  
  
   Especifica a arquitetura para a geração de código que usa as instruções SSE (Streaming SIMD Extensions) e SSE2 (Streaming SIMD Extensions 2).  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **StreamingSIMDExtensions** - **/arch:SSE**  
  
  - **StreamingSIMDExtensions2** - **/arch:SSE2**  
  
    Para obter mais informações, consulte [/arch (x86)](http://msdn.microsoft.com/library/9dd5a75d-06e4-4674-aade-33228486078d).  
  
- **EnableFiberSafeOptimizations**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, dê suporte a segurança de fibra para dados alocados usando armazenamento local de thread estático, ou seja, dados alocados usando `__declspec(thread)`.  
  
   Para obter mais informações, consulte [/GT (suporte para armazenamento em fibra-thread safe-local)](http://msdn.microsoft.com/library/071fec79-c701-432b-9970-457344133159).  
  
- **EnablePREfast**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, habilitará análise de código.  
  
   Para obter mais informações, consulte [/analyze (Análise de Código)](http://msdn.microsoft.com/library/81da536a-e030-4bd4-be18-383927597d08).  
  
- **ErrorReporting**  
  
   Parâmetro String opcional.  
  
   Permite que você forneça informações de ICE (erro interno do compilador) diretamente à Microsoft. Por padrão, a configuração em compilações do IDE é **Aviso** e a configuração em compilações de linha de comando é **Fila**.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **None** - **/errorReport:none**  
  
  - **Prompt** - **/errorReport:prompt**  
  
  - **Queue** - **/errorReport:queue**  
  
  - **Send** - **/errorReport:send**  
  
    Para obter mais informações, consulte [/errorReport (relatório de erros internos do compilador)](http://msdn.microsoft.com/library/819828f8-b0a5-412c-9c57-bf822f17e667).  
  
- **ExceptionHandling**  
  
   Parâmetro String opcional.  
  
   Especifica o modelo de tratamento de exceções a ser utilizado pelo compilador.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **false** - *\<none>*  
  
  - **Async** - **/EHa**  
  
  - **Sync** - **/EHsc**  
  
  - **SyncCThrow** - **/EHs**  
  
    Para obter mais informações, consulte [/EH (modelo de tratamento de exceção)](http://msdn.microsoft.com/library/754b916f-d206-4472-b55a-b6f1b0f2cb4d).  
  
- **ExpandAttributedSource**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, criará um arquivo de listagem com atributos expandidos injetados no arquivo de origem.  
  
   Para obter mais informações, consulte [/Fx (mesclar código injetado)](http://msdn.microsoft.com/library/14f0e301-3bab-45a3-bbdf-e7ce66f20560).  
  
- **FavorSizeOrSpeed**  
  
   Parâmetro String opcional.  
  
   Especifica se tamanho ou velocidade do código deve ser favorecido.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Neither** - *\<none>*  
  
  - **Size** - **/Os**  
  
  - **Speed** - **/Ot**  
  
    Para obter mais informações, consulte [/Os, /Ot (favorecer código pequeno, favorecer código rápido)](http://msdn.microsoft.com/library/9a340806-fa15-4308-892c-355d83cac0f2).  
  
- **FloatingPointExceptions**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, habilitará o modelo de exceção de ponto flutuante confiável. As exceções serão geradas imediatamente depois de serem disparadas.  
  
   Para obter mais informações, consulte a opção o /**fp:except** em [/fp (Especificar Comportamento de Ponto Flutuante)](http://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e).  
  
- **FloatingPointModel**  
  
   Parâmetro String opcional.  
  
   Define o modelo de ponto flutuante.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Precise** - **/fp:precise**  
  
  - **Strict** - **/fp:strict**  
  
  - **Fast** - **/fp:fast**  
  
    Para obter mais informações, consulte [/fp (especificar comportamento de ponto flutuante)](http://msdn.microsoft.com/library/10469d6b-e68b-4268-8075-d073f4f5d57e).  
  
- **ForceConformanceInForLoopScope**  
  
   Parâmetro Boolean opcional.  
  
   Se `true`, implementará o comportamento padrão do C++ em loops [for](http://msdn.microsoft.com/library/6c7d01b3-c4c1-4c6a-aa58-e2d198f33d4a) que usem extensões da Microsoft ([/Ze](http://msdn.microsoft.com/library/65e49258-7161-4289-a176-7c5c0656b1a2)).  
  
   Para obter mais informações, consulte [/Zc:forScope (forçar conformidade para escopo de loop)](http://msdn.microsoft.com/library/3031f02d-3b14-4ad0-869e-22b0110c3aed).  
  
- **ForcedIncludeFiles**  
  
   Parâmetro `String[]` opcional.  
  
   Faz o pré-processador processar um ou mais arquivos de cabeçalho especificados.  
  
   Para obter mais informações, consulte [/FI (nomear arquivo de include forçado)](http://msdn.microsoft.com/library/07e79577-8152-4df9-a64c-aae08c603397).  
  
- **ForcedUsingFiles**  
  
   Parâmetro **String[]** opcional.  
  
   Faz o pré-processador processar um ou mais arquivos **#using** especificados.  
  
   Para obter mais informações, consulte [/FU (nome forçado #usando arquivo)](http://msdn.microsoft.com/library/698f8603-457f-435a-baff-5ac9243d6ca1).  
  
- **FunctionLevelLinking**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, permitirá que o compilador empacote funções individuais na forma de funções empacotadas (COMDATs).  
  
   Para obter mais informações, consulte [/Gy (habilitar vinculação em nível de função)](http://msdn.microsoft.com/library/0d3cf14c-ed7d-4ad3-b4b6-104e56f61046).  
  
- **GenerateXMLDocumentationFiles**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, fará o compilador processar comentários da documentação em arquivos de código-fonte e criará um arquivo .xdc para cada arquivo de código-fonte que tenha comentários de documentação.  
  
   Para obter mais informações, consulte [/doc (processar comentários da documentação) (C/C++)](http://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63). Consulte também o parâmetro **XMLDocumentationFileName** nesta tabela.  
  
- **IgnoreStandardIncludePath**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, evitará que o compilador pesquise os arquivos de inclusão em diretórios especificados nas variáveis de ambiente PATH e INCLUDE.  
  
   Para obter mais informações, consulte [/X (ignorar caminhos de inclusão padrão)](http://msdn.microsoft.com/library/16bdf2cc-c8dc-46e4-bdcc-f3caeba5e1ef).  
  
- **InlineFunctionExpansion**  
  
   Parâmetro **String** opcional.  
  
   Especifica o nível de expansão de função embutida para o build.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Default** - *\<none>*  
  
  - **Disabled** - **/Ob0**  
  
  - **OnlyExplicitInline** - **/Ob1**  
  
  - **AnySuitable** - **/Ob2**  
  
    Para obter mais informações, consulte [/Ob (expansão de função embutida)](http://msdn.microsoft.com/library/f134e6df-e939-4980-a01d-47425dbc562a).  
  
- **IntrinsicFunctions**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, substituirá algumas chamadas de função com formas da função intrínsecas ou especiais de outra maneira que ajudem o aplicativo a ser executado mais rapidamente.  
  
   Para obter mais informações, consulte [/Oi (gerar funções intrínsecas)](http://msdn.microsoft.com/library/fa4a3bf6-0ed8-481b-91c0-add7636132b4).  
  
- **MinimalRebuild**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, habilitará recompilação mínima, que determina se os arquivos de origem C++ que incluem definições de classe C++ alteradas (armazenadas nos arquivos de cabeçalho (.h)) devem ser recompilados.  
  
   Para obter mais informações, consulte [/Gm (habilitar recompilação mínima)](http://msdn.microsoft.com/library/d8869ce0-d2ea-40eb-8dae-6d2cdb61dd59).  
  
- **MultiProcessorCompilation**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, use vários processadores para compilar. Esse parâmetro cria um processo para cada processador efetivo no seu computador.  
  
   Para obter mais informações, consulte [/MP (compilar com vários processos)](http://msdn.microsoft.com/library/a932b14a-74fe-4b45-84e4-6bf53f0f5e07). Consulte também o parâmetro **ProcessorNumber** nesta tabela.  
  
- **ObjectFileName**  
  
   Parâmetro **String** opcional.  
  
   Especifica um nome de arquivo de objeto (.obj) ou diretório a ser usado no lugar do padrão.  
  
   Para obter mais informações, consulte [/Fo (nome do arquivo-objeto)](http://msdn.microsoft.com/library/0e6d593e-4e7f-4990-9e6e-92e1dcbcf6e6).  
  
- **ObjectFiles**  
  
   Parâmetro **String[]** opcional.  
  
   Uma lista de arquivos de objeto.  
  
- **OmitDefaultLibName**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, omitirá o nome da biblioteca em tempo de execução C padrão do arquivo de objeto (.obj). Por padrão, o compilador coloca o nome da biblioteca no arquivo .obj para direcionar o vinculador à biblioteca correta.  
  
   Para obter mais informações, consulte [/Zl (omitir o nome da biblioteca padrão)](http://msdn.microsoft.com/library/b27d39d0-44d6-498c-84ae-27c1326fee59).  
  
- **OmitFramePointers**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, suprimirá a criação de ponteiros de quadro na pilha de chamadas.  
  
   Para obter mais informações, consulte [/Oy (omissão do ponteiro de quadro)](http://msdn.microsoft.com/library/c451da86-5297-4c5a-92bc-561d41379853).  
  
- **OpenMPSupport**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, fará o compilador processar cláusulas e diretivas OpenMP.  
  
   Para obter mais informações, consulte [/openmp (habilitar suporte a OpenMP 2.0)](http://msdn.microsoft.com/library/9082b175-18d3-4378-86a7-c0eb95664e13).  
  
- **Optimization**  
  
   Parâmetro **String** opcional.  
  
   Especifica várias otimizações de código para velocidade e tamanho.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Disabled** - **/Od**  
  
  - **MinSpace** - **/O1**  
  
  - **MaxSpeed** - **/O2**  
  
  - **Full** - **/Ox**  
  
    Para obter mais informações, consulte Opções de [/S (otimizar código)](http://msdn.microsoft.com/library/77997af9-5555-4b3d-aa57-6615b27d4d5d).  
  
- **PrecompiledHeader**  
  
   Parâmetro **String** opcional.  
  
   Crie ou use um arquivo de cabeçalho pré-compilado (.pch) durante o build.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **NotUsing** - *\<none>*  
  
  - **Create** - **/Yc**  
  
  - **Use** - **/Yu**  
  
    Para obter mais informações, consulte [/Yc (Criar arquivo de cabeçalho pré-compilado)](http://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678) e [/Yu (Usar arquivo de cabeçalho pré-compilado)](http://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f). Consulte também os parâmetros **PrecompiledHeaderFile** e **PrecompiledHeaderOutputFile** nessa tabela.  
  
- **PrecompiledHeaderFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica um nome de arquivo de cabeçalho pré-compilado para criar ou usar.  
  
   Para obter mais informações, consulte [/Yc (Criar arquivo de cabeçalho pré-compilado)](http://msdn.microsoft.com/library/47c2e555-b4f5-46e6-906e-ab5cf21f0678) e [/Yu (Usar arquivo de cabeçalho pré-compilado)](http://msdn.microsoft.com/library/24f1bd0e-b624-4296-a17e-d4b53e374e1f).  
  
- **PrecompiledHeaderOutputFile**  
  
   Parâmetro **String** opcional.  
  
   Especifica um nome de caminho para um cabeçalho pré-compilado em vez de usar o nome do caminho padrão.  
  
   Para obter mais informações, consulte [/Fp (arquivo .Pch de nome)](http://msdn.microsoft.com/library/0fcd9cbd-e09f-44d3-9715-b41efb5d0be2).  
  
- **PreprocessKeepComments**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, preservará comentários durante o pré-processamento.  
  
   Para obter mais informações, consulte [/C (Preservar Comentários Durante o Pré-Processamento)](http://msdn.microsoft.com/library/944567ca-16bc-4728-befe-d414a7787f26).  
  
- **PreprocessorDefinitions**  
  
   Parâmetro `String[]` opcional.  
  
   Define um símbolo de pré-processamento para seu arquivo de origem.  
  
   Para obter mais informações, consulte [/D (definições de pré-processador)](http://msdn.microsoft.com/library/b53fdda7-8da1-474f-8811-ba7cdcc66dba).  
  
- **PreprocessOutput**  
  
   Parâmetro `ITaskItem[]` opcional.  
  
   Define uma matriz de itens de saída do pré-processador que podem ser consumidos e emitidos por tarefas.  
  
- **PreprocessOutputPath**  
  
   Parâmetro `String` opcional.  
  
   Especifica o nome do arquivo de saída para o qual o parâmetro **PreprocessToFile** grava a saída pré-processada.  
  
   Para obter mais informações, consulte [/Fi (pré-processar nome de arquivo de saída)](http://msdn.microsoft.com/library/6d0ba983-a8b7-41ec-84f5-b4688ef8efee).  
  
- **PreprocessSuppressLineNumbers**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, pré-processará arquivos de origem em C e C++ e copiará os arquivos pré-processados para o dispositivo de saída padrão.  
  
   Para obter mais informações, consulte [/EP (pré-processar para stdout Sem Diretivas #line)](http://msdn.microsoft.com/library/6ec411ae-e33d-4ef5-956e-0054635eabea).  
  
- **PreprocessToFile**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, pré-processará arquivos de origem em C e C++ e gravará a saída pré-processada em um arquivo.  
  
   Para obter mais informações, consulte [/P (pré-processar para um arquivo)](http://msdn.microsoft.com/library/123ee54f-8219-4a6f-9876-4227023d83fc).  
  
- **ProcessorNumber**  
  
   Parâmetro `Integer` opcional.  
  
   Especifica o número máximo de processadores a serem usados em uma compilação multiprocessador. Use esse parâmetro em combinação com o parâmetro **MultiProcessorCompilation**.  
  
- **ProgramDataBaseFileName**  
  
   Parâmetro `String` opcional.  
  
   Especifica um nome de arquivo para o arquivo PDB (banco de dados do programa).  
  
   Para obter mais informações, consulte [/Fd (nome de arquivo de banco de dados do programa)](http://msdn.microsoft.com/library/3977a9ed-f0ac-45df-bf06-01cedd2ba85a).  
  
- **RuntimeLibrary**  
  
   Parâmetro `String` opcional.  
  
   Indica se um módulo com multithread é uma DLL e seleciona versões de varejo ou de depuração da biblioteca em tempo de execução.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **MultiThreaded** - **/MT**  
  
  - **MultiThreadedDebug** - **/MTd**  
  
  - **MultiThreadedDLL** - **/MD**  
  
  - **MultiThreadedDebugDLL** - **/MDd**  
  
    Para obter mais informações, consulte [/MD, /MT, /LD (usar biblioteca em tempo de execução)](http://msdn.microsoft.com/library/cf7ed652-dc3a-49b3-aab9-ad60e5395579).  
  
- **RuntimeTypeInfo**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, adicionará código para verificar os tipos de objeto C++ no tempo de execução (informações de tipo de tempo de execução).  
  
   Para obter mais informações, consulte [/GR (habilitar informações de tipo de tempo de execução)](http://msdn.microsoft.com/library/d1f9f850-dcec-49fd-96ef-e72d01148906).  
  
- **ShowIncludes**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, fará o compilador gerar uma lista dos arquivos de inclusão.  
  
   Para obter mais informações, consulte [/showIncludes (listar arquivos de inclusão)](http://msdn.microsoft.com/library/0b74b052-f594-45a6-a7c7-09e1a319547d).  
  
- **SmallerTypeCheck**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, relatará um erro em tempo de execução se um valor for atribuído a um tipo de dados menor e provocará perda de dados.  
  
   Para obter mais informações, consulte a opção **/RTCc** em [/RTC (Verificações de Erro em Tempo de Execução)](http://msdn.microsoft.com/library/9702c558-412c-4004-acd5-80761f589368).  
  
- **Sources**  
  
   Parâmetro `ITaskItem[]` obrigatório.  
  
   Especifica uma lista de arquivos de origem separados por espaços.  
  
- **StringPooling**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, permitirá que o compilador crie uma cópia de cadeias de caracteres idênticas na imagem do programa.  
  
   Para obter mais informações, consulte [/GF (eliminar cadeias de caracteres duplicadas)](http://msdn.microsoft.com/library/bb7b5d1c-8e1f-453b-9298-8fcebf37d16c).  
  
- **StructMemberAlignment**  
  
   Parâmetro `String` opcional.  
  
   Especifica o alinhamento de byte para todos os membros em uma estrutura.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **Default** - **/Zp1**  
  
  - **1Byte** - **/Zp1**  
  
  - **2Bytes** - **/Zp2**  
  
  - **4Bytes** - **/Zp4**  
  
  - **8Bytes** - **/Zp8**  
  
  - **16Bytes** - **/Zp16**  
  
    Para obter mais informações, consulte [/Zp (Alinhamento de Membro de Struct)](http://msdn.microsoft.com/library/5242f656-ed9b-48a3-bc73-cfcf3ed2520f).  
  
- **SuppressStartupBanner**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, impedirá a exibição da mensagem de direitos autorais e de número de versão quando a tarefa for iniciada.  
  
   Para obter mais informações, consulte [/nologo (suprimir faixa de inicialização) (C/C++)](http://msdn.microsoft.com/library/75930d8b-b11c-4db8-99e5-b52f97da0693).  
  
- **TrackerLogDirectory**  
  
   Parâmetro `String` opcional.  
  
   Especifica o diretório intermediário em que os logs de rastreamento para essa tarefa são armazenados.  
  
   Para obter mais informações, consulte os parâmetros **TLogReadFiles** e **TLogWriteFiles** nesta tabela.  
  
- **TreatSpecificWarningsAsErrors**  
  
   Parâmetro **String[]** opcional.  
  
   Trata a lista especificada de avisos do compilador como erros.  
  
   Para obter mais informações, consulte a opção **/we**`n` em [/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Nível de Aviso)](http://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f).  
  
- **TreatWarningAsError**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, tratará todos os avisos do compilador como erros.  
  
   Para obter mais informações, consulte a opção **/WX** em [/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (nível de aviso)](http://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f).  
  
- **TreatWChar_tAsBuiltInType**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, trate o tipo `wchar_t` como um tipo nativo.  
  
   Para obter mais informações, consulte [/Zc:wchar_t (wchar_t é o tipo nativo)](http://msdn.microsoft.com/library/b0de5a84-da72-4e5a-9a4e-541099f939e0).  
  
- **UndefineAllPreprocessorDefinitions**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, cancelará a definição de símbolos específicos da Microsoft que o compilador definir.  
  
   Para obter mais informações, consulte a opção **/u** em [/U, /u (Excluir Símbolos)](http://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a).  
  
- **UndefinePreprocessorDefinitions**  
  
   Parâmetro `String[]` opcional.  
  
   Especifica uma lista de um ou mais símbolos de pré-processador a excluir.  
  
   Para obter mais informações, consulte a opção **/U** em [/U, /u (excluir símbolos)](http://msdn.microsoft.com/library/7bc0474f-6d1f-419b-807d-0d8816763b2a).  
  
- **UseFullPaths**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, exibirá o caminho completo dos arquivos de código-fonte passados para o compilador no diagnóstico.  
  
   Para obter mais informações, consulte [/FC (caminho completo do arquivo de código-fonte no diagnóstico)](http://msdn.microsoft.com/library/1f11414e-cb42-421b-be68-9d369aab036b).  
  
- **UseUnicodeForAssemblerListing**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, fará o arquivo de saída ser criado em formato UTF-8.  
  
   Para obter mais informações, consulte a opção **/FAu** em [/FA, /Fa (Arquivo de Listagem)](http://msdn.microsoft.com/library/c7507d0e-c69d-44f9-b8e2-d2c398697402).  
  
- **WarningLevel**  
  
   Parâmetro `String` opcional.  
  
   Especifica o nível mais alto de aviso que deverá ser gerado pelo compilador.  
  
   Especifique um dos valores a seguir, cada um correspondendo a uma opção de linha de comando.  
  
  - **TurnOffAllWarnings** - **/W0**  
  
  - **Level1** - **/W1**  
  
  - **Level2** - **/W2**  
  
  - **Level3** - **/W3**  
  
  - **Level4** - **/W4**  
  
  - **EnableAllWarnings** - **/Wall**  
  
    Para obter mais informações, consulte a opção **/W**_n_ em [/w, /W0, /W1, /W2, /W3, /W4, /w1, /w2, /w3, /w4, /Wall, /wd, /we, /wo, /Wv, /WX (Nível de Aviso)](http://msdn.microsoft.com/library/d6bc7bf5-c754-4879-909c-8e3a67e2629f).  
  
- **WholeProgramOptimization**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, habilitará a otimização de todo o programa.  
  
   Para obter mais informações, consulte [/GL (otimização de programa inteiro)](http://msdn.microsoft.com/library/09d51e2d-9728-4bd0-b5dc-3b8284aca1d1).  
  
- **XMLDocumentationFileName**  
  
   Parâmetro `String` opcional.  
  
   Especifica o nome dos arquivos de documentação XML gerados. Esse parâmetro pode ser um nome de arquivo ou de diretório.  
  
   Para obter mais informações, consulte o argumento `name` em [/doc ( Comentários da Documentação do Processo) (C/C++)](http://msdn.microsoft.com/library/b54f7e2c-f28f-4f46-9ed6-0db09be2cc63). Consulte também o parâmetro **GenerateXMLDocumentationFiles** nesta tabela.  
  
- **MinimalRebuildFromTracking**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, um build incremental controlada será executada; se `false`, será executada uma recompilação.  
  
- **TLogReadFiles**  
  
   Parâmetro `ITaskItem[]` opcional.  
  
   Especifica uma matriz de itens que representam os *logs de acompanhamento do arquivo de leitura*.  
  
   Um log de acompanhamento do arquivo de leitura (.tlog) contém os nomes dos arquivos de entrada lidos por uma tarefa e é usado pelo sistema de build do projeto para dar suporte a compilações incrementais. Para obter mais informações, consulte os parâmetros **TrackerLogDirectory** e **TrackFileAccess** nesta tabela.  
  
- **TLogWriteFiles**  
  
   Parâmetro `ITaskItem[]` opcional.  
  
   Especifica uma matriz de itens que representam os *logs de acompanhamento do arquivo de gravação*.  
  
   Um log de acompanhamento de arquivo de gravação (.tlog) contém os nomes dos arquivos de saída gravados por uma tarefa e é usado pelo sistema de build do projeto para dar suporte a compilações incrementais. Para obter mais informações, consulte os parâmetros **TrackerLogDirectory** e **TrackFileAccess** nesta tabela.  
  
- **TrackFileAccess**  
  
   Parâmetro `Boolean` opcional.  
  
   Se `true`, controlará os padrões de acesso de arquivo.  
  
   Para obter mais informações, consulte os parâmetros **TLogReadFiles** e **TLogWriteFiles** nesta tabela.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Referência de tarefas](../msbuild/msbuild-task-reference.md)



