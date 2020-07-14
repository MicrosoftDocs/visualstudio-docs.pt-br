---
title: IDiaSymbol | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol interface
ms.assetid: 01ad328a-736c-4933-a9f8-c2ded19ddd8c
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0214d3e8d097efa31b3f8b02e67f419226a093a4
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461339"
---
# <a name="idiasymbol"></a>IDiaSymbol
Descreve as propriedades de uma instância de símbolo.

## <a name="syntax"></a>Syntax

```
IDiaSymbol : IUnknown
```

## <a name="methods-in-alphabetical-order"></a>Métodos em ordem alfabética
A tabela a seguir mostra os métodos de `IDiaSymbol` .

> [!NOTE]
> Os símbolos retornarão dados significativos apenas para alguns desses métodos, dependendo do tipo de símbolo. Se um método retornar `S_OK` , esse método retornará dados significativos.

|Método|Descrição|
|------------|-----------------|
|[IDiaSymbol::findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md)|Recupera todos os filhos do símbolo.|
|[IDiaSymbol::findChildrenEx](../../debugger/debug-interface-access/idiasymbol-findchildrenex.md)|Recupera os filhos do símbolo. Este método é a versão estendida de [IDiaSymbol:: findChildren](../../debugger/debug-interface-access/idiasymbol-findchildren.md).|
|[IDiaSymbol::findChildrenExByAddr](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyaddr.md)|Recupera os filhos do símbolo que são válidos em um endereço especificado.|
|[IDiaSymbol::findChildrenExByRVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyrva.md)|Recupera os filhos do símbolo que são válidos em um endereço virtual relativo (RVA) específico.|
|[IDiaSymbol::findChildrenExByVA](../../debugger/debug-interface-access/idiasymbol-findchildrenexbyva.md)|Recupera os filhos do símbolo que são válidos em um endereço virtual especificado.|
|[IDiaSymbol::findInlineFramesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyaddr.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um determinado endereço.|
|[IDiaSymbol::findInlineFramesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyrva.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual relativo (RVA) específico.|
|[IDiaSymbol::findInlineFramesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineframesbyva.md)|Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual especificado (VA).|
|[IDiaSymbol::findInlineeLines](../../debugger/debug-interface-access/idiasymbol-findinlineelines.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, neste símbolo.|
|[IDiaSymbol::findInlineeLinesByAddr](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyaddr.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, neste símbolo dentro do intervalo de endereços especificado.|
|[IDiaSymbol::findInlineeLinesByRVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyrva.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, neste símbolo dentro do RVA (endereço virtual relativo) especificado.|
|[IDiaSymbol::findInlineeLinesByVA](../../debugger/debug-interface-access/idiasymbol-findinlineelinesbyva.md)|Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, neste símbolo dentro do endereço virtual especificado (VA).|
|[IDiaSymbol::findSymbolsByRVAForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsbyrvaforacceleratorpointertag.md)|Dado um valor de marca correspondente, esse método retorna uma enumeração de símbolos que estão contidos nessa função de stub em um endereço virtual relativo especificado.|
|[IDiaSymbol::findSymbolsForAcceleratorPointerTag](../../debugger/debug-interface-access/idiasymbol-findsymbolsforacceleratorpointertag.md)|Retorna o número de marcas do ponteiro do acelerador em uma C++ AMP função de stub.|
|[IDiaSymbol::get_acceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-acceleratorpointertags.md)|Retorna todos os valores de marca do ponteiro de aceleração que correspondem a uma função de stub de C++ AMP Accelerator.|
|[IDiaSymbol::get_access](../../debugger/debug-interface-access/idiasymbol-get-access.md)|Recupera o modificador de acesso de um membro de classe.|
|[IDiaSymbol::get_addressOffset](../../debugger/debug-interface-access/idiasymbol-get-addressoffset.md)|Recupera a parte de deslocamento de um local de endereço.|
|[IDiaSymbol::get_addressSection](../../debugger/debug-interface-access/idiasymbol-get-addresssection.md)|Recupera a parte da seção de um local de endereço.|
|[IDiaSymbol::get_addressTaken](../../debugger/debug-interface-access/idiasymbol-get-addresstaken.md)|Recupera um sinalizador que indica se outro símbolo faz referência a esse endereço.|
|[IDiaSymbol::get_age](../../debugger/debug-interface-access/idiasymbol-get-age.md)|Recupera o valor de idade de um banco de dados do programa.|
|[IDiaSymbol::get_arrayIndexType](../../debugger/debug-interface-access/idiasymbol-get-arrayindextype.md)|Recupera o identificador de símbolo do tipo de índice da matriz.|
|[IDiaSymbol::get_arrayIndexTypeId](../../debugger/debug-interface-access/idiasymbol-get-arrayindextypeid.md)|Recupera o identificador do tipo de índice de matriz do símbolo.|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|Recupera o número de versão principal de back-end.|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|Recupera o número de versão secundária de back-end.|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|Recupera o número da compilação de back-end.|
|[IDiaSymbol::get_baseDataOffset](../../debugger/debug-interface-access/idiasymbol-get-basedataoffset.md)|Recupera o deslocamento de dados base.|
|[IDiaSymbol::get_baseDataSlot](../../debugger/debug-interface-access/idiasymbol-get-basedataslot.md)|Recupera o slot de dados base.|
|[IDiaSymbol::get_baseSymbol](../../debugger/debug-interface-access/idiasymbol-get-basesymbol.md)|Recupera o símbolo do qual o ponteiro se baseia.|
|[IDiaSymbol::get_baseSymbolId](../../debugger/debug-interface-access/idiasymbol-get-basesymbolid.md)|Recupera a ID do símbolo do qual o ponteiro se baseia.|
|[IDiaSymbol::get_baseType](../../debugger/debug-interface-access/idiasymbol-get-basetype.md)|Recupera a marca de tipo de um tipo simples.|
|[IDiaSymbol::get_bitPosition](../../debugger/debug-interface-access/idiasymbol-get-bitposition.md)|Recupera a posição de bits de um local.|
|[IDiaSymbol::get_builtInKind](../../debugger/debug-interface-access/idiasymbol-get-builtinkind.md)|Recupera um tipo interno do tipo HLSL.|
|[IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)|Retorna um indicador da Convenção de chamada de um método.|
|[IDiaSymbol::get_classParent](../../debugger/debug-interface-access/idiasymbol-get-classparent.md)|Recupera uma referência para a classe pai do símbolo.|
|[IDiaSymbol::get_classParentId](../../debugger/debug-interface-access/idiasymbol-get-classparentid.md)|Recupera o identificador pai de classe do símbolo.|
|[IDiaSymbol::get_code](../../debugger/debug-interface-access/idiasymbol-get-code.md)|Recupera um sinalizador que indica se o símbolo se refere a um endereço de código.|
|[IDiaSymbol::get_compilerGenerated](../../debugger/debug-interface-access/idiasymbol-get-compilergenerated.md)|Recupera um sinalizador que indica se o símbolo foi gerado pelo compilador.|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|Recupera o nome do compilador usado para criar o [compiland](../../debugger/debug-interface-access/compiland.md).|
|[IDiaSymbol::get_constructor](../../debugger/debug-interface-access/idiasymbol-get-constructor.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário tem um construtor.|
|[IDiaSymbol::get_container](../../debugger/debug-interface-access/idiasymbol-get-container.md)|Recupera o símbolo de contenção deste símbolo.|
|[IDiaSymbol::get_constType](../../debugger/debug-interface-access/idiasymbol-get-consttype.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário é constante.|
|[IDiaSymbol::get_count](../../debugger/debug-interface-access/idiasymbol-get-count.md)|Recupera o número de itens em uma lista ou matriz.|
|[IDiaSymbol::get_countLiveRanges](../../debugger/debug-interface-access/idiasymbol-get-countliveranges.md)|Recupera o número de intervalos de endereços válidos associados ao símbolo local.|
|[IDiaSymbol::get_customCallingConvention](../../debugger/debug-interface-access/idiasymbol-get-customcallingconvention.md)|Recupera um sinalizador que indica se a função usa uma Convenção de chamada personalizada.|
|[IDiaSymbol::get_dataBytes](../../debugger/debug-interface-access/idiasymbol-get-databytes.md)|Recupera os bytes de dados de um símbolo OEM.|
|[IDiaSymbol::get_dataKind](../../debugger/debug-interface-access/idiasymbol-get-datakind.md)|Recupera a classificação de variável de um símbolo de dados.|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|Recupera o sinalizador que descreve os recursos de editar e continuar do programa ou da unidade compilada.|
|[IDiaSymbol::get_farReturn](../../debugger/debug-interface-access/idiasymbol-get-farreturn.md)|Recupera um sinalizador que indica se a função usa um retorno distante.|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|Recupera o número de versão principal de front-end.|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|Recupera o número de versão secundária de front-end.|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|Recupera o número da compilação de front-end.|
|[IDiaSymbol::get_function](../../debugger/debug-interface-access/idiasymbol-get-function.md)|Recupera um sinalizador que indica se o símbolo público se refere a uma função.|
|[IDiaSymbol::get_guid](../../debugger/debug-interface-access/idiasymbol-get-guid.md)|Recupera o GUID do símbolo.|
|[IDiaSymbol::get_hasAlloca](../../debugger/debug-interface-access/idiasymbol-get-hasalloca.md)|Recupera um sinalizador que indica se a função contém uma chamada para `alloca` .|
|[IDiaSymbol::get_hasAssignmentOperator](../../debugger/debug-interface-access/idiasymbol-get-hasassignmentoperator.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário tem quaisquer operadores de atribuição definidos.|
|[IDiaSymbol::get_hasCastOperator](../../debugger/debug-interface-access/idiasymbol-get-hascastoperator.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário tem quaisquer operadores de conversão definidos.|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|Recupera um sinalizador que indica se o compiland contém informações de depuração.|
|[IDiaSymbol::get_hasEH](../../debugger/debug-interface-access/idiasymbol-get-haseh.md)|Recupera um sinalizador que indica se a função tem um manipulador de exceção em estilo C++.|
|[IDiaSymbol::get_hasEHa](../../debugger/debug-interface-access/idiasymbol-get-haseha.md)|Recupera um sinalizador que indica se a função tem um manipulador de exceção assíncrona.|
|[IDiaSymbol::get_hasInlAsm](../../debugger/debug-interface-access/idiasymbol-get-hasinlasm.md)|Recupera um sinalizador que indica se a função tem assembly embutido.|
|[IDiaSymbol::get_hasLongJump](../../debugger/debug-interface-access/idiasymbol-get-haslongjump.md)|Recupera um sinalizador que indica se a função contém um comando longjmp (parte da manipulação de exceção em estilo C).|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|Recupera um sinalizador que indica se o módulo contém código gerenciado.|
|[IDiaSymbol::get_hasNestedTypes](../../debugger/debug-interface-access/idiasymbol-get-hasnestedtypes.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário tem definições de tipo aninhado.|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|Recupera um sinalizador que indica se a função ou compiland tem verificações de segurança compiladas em (por meio da opção de compilador [/GS (verificação de segurança de buffer)](/cpp/build/reference/gs-buffer-security-check) ).|
|[IDiaSymbol::get_hasSEH](../../debugger/debug-interface-access/idiasymbol-get-hasseh.md)|Recupera um sinalizador que indica se a função tem manipulação de exceção estruturada no estilo Win32.|
|[IDiaSymbol::get_hasSetJump](../../debugger/debug-interface-access/idiasymbol-get-hassetjump.md)|Recupera um sinalizador que indica se a função contém um comando setjmp.|
|[IDiaSymbol::get_indirectVirtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-indirectvirtualbaseclass.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário é uma classe base virtual indireta.|
|[IDiaSymbol::get_InlSpec](../../debugger/debug-interface-access/idiasymbol-get-inlspec.md)|Recupera um sinalizador que indica se a função foi marcada com o atributo embutido.|
|[IDiaSymbol::get_interruptReturn](../../debugger/debug-interface-access/idiasymbol-get-interruptreturn.md)|Recupera um sinalizador que indica se a função tem um retorno da instrução de interrupção.|
|[IDiaSymbol::get_intro](../../debugger/debug-interface-access/idiasymbol-get-intro.md)|Recupera um sinalizador que indica se a função é a função virtual da classe base.|
|[IDiaSymbol::get_isAcceleratorGroupSharedLocal](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorgroupsharedlocal.md)|Recupera um sinalizador que indica se o símbolo corresponde a uma variável local compartilhada de grupo no código compilado para um acelerador de C++ AMP.|
|[IDiaSymbol::get_isAcceleratorPointerTagLiveRange](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorpointertagliverange.md)|Recupera um sinalizador que indica se o símbolo corresponde ao *símbolo de intervalo de definição* para o componente de marca de uma variável de ponteiro no código compilado para um acelerador de C++ amp. O símbolo de intervalo de definição é o local de uma variável para um intervalo de endereços.|
|[IDiaSymbol::get_isAcceleratorStubFunction](../../debugger/debug-interface-access/idiasymbol-get-isacceleratorstubfunction.md)|Indica se o símbolo corresponde a um símbolo de função de nível superior para um sombreador compilado para um acelerador que corresponde a uma `parallel_for_each` chamada.|
|[IDiaSymbol::get_isAggregated](../../debugger/debug-interface-access/idiasymbol-get-isaggregated.md)|Recupera um sinalizador que indica se os dados fazem parte de um agregado de muitos símbolos.|
|[IDiaSymbol::get_isCTypes](../../debugger/debug-interface-access/idiasymbol-get-isctypes.md)|Recupera um sinalizador que indica se o arquivo de símbolo contém tipos C.|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|Recupera um sinalizador que indica se o módulo foi convertido de Common Intermediate Language (CIL) para código nativo.|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|Recupera um sinalizador que indica se os elementos de um tipo de dados definidos pelo usuário estão alinhados a um limite específico.|
|[IDiaSymbol::get_isHLSLData](../../debugger/debug-interface-access/idiasymbol-get-ishlsldata.md)|Especifica se este símbolo representa dados de HLSL (linguagem de sombreamento de alto nível).|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|Recupera um sinalizador que indica se o módulo foi compilado com a opção de compilador [/hotpatch (Create Hotpatchable Image)](/cpp/build/reference/hotpatch-create-hotpatchable-image) .|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|Recupera um sinalizador que indica se o compiland gerenciado foi vinculado com o LTCG do vinculador.|
|[IDiaSymbol::get_isMatrixRowMajor](../../debugger/debug-interface-access/idiasymbol-get-ismatrixrowmajor.md)|Especifica se a matriz é a linha principal.|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|Recupera um sinalizador que indica se o compiland gerenciado é um. netmodule (contendo somente metadados).|
|[IDiaSymbol::get_isMultipleInheritance](../../debugger/debug-interface-access/idiasymbol-get-ismultipleinheritance.md)|Especifica se o `this` ponteiro aponta para um membro de dados com várias heranças.|
|[IDiaSymbol::get_isNaked](../../debugger/debug-interface-access/idiasymbol-get-isnaked.md)|Recupera um sinalizador que indica se a função tem o atributo [Naked](/cpp/cpp/naked-cpp) .|
|[IDiaSymbol::get_isOptimizedAway](../../debugger/debug-interface-access/idiasymbol-get-isoptimizedaway.md)|Especifica se a variável é otimizada para fora.|
|[IDiaSymbol::get_isPointerBasedOnSymbolValue](../../debugger/debug-interface-access/idiasymbol-get-ispointerbasedonsymbolvalue.md)|Especifica se o `this` ponteiro é baseado em um valor de símbolo.|
|[IDiaSymbol::get_isPointerToDataMember](../../debugger/debug-interface-access/idiasymbol-get-ispointertodatamember.md)|Especifica se este símbolo é um ponteiro para um membro de dados.|
|[IDiaSymbol::get_isPointerToMemberFunction](../../debugger/debug-interface-access/idiasymbol-get-ispointertomemberfunction.md)|Especifica se este símbolo é um ponteiro para uma função membro.|
|[IDiaSymbol::get_isReturnValue](../../debugger/debug-interface-access/idiasymbol-get-isreturnvalue.md)|Especifica se a variável contém um valor de retorno.|
|[IDiaSymbol::get_isSdl](../../debugger/debug-interface-access/idiasymbol-get-issdl.md)|Especifica se o módulo é compilado com a opção/SDL.|
|[IDiaSymbol::get_isSingleInheritance](../../debugger/debug-interface-access/idiasymbol-get-issingleinheritance.md)|Especifica se o `this` ponteiro aponta para um membro de dados com herança única.|
|[IDiaSymbol::get_isSplitted](../../debugger/debug-interface-access/idiasymbol-get-issplitted.md)|Recupera um sinalizador que indica se os dados foram divididos em uma agregação de símbolos separados.|
|[IDiaSymbol::get_isStatic](../../debugger/debug-interface-access/idiasymbol-get-isstatic.md)|Recupera um sinalizador que indica se uma função ou camada de conversão é estática.|
|[IDiaSymbol::get_isStripped](../../debugger/debug-interface-access/idiasymbol-get-isstripped.md)|Recupera um sinalizador que indica se os símbolos privados foram removidos do arquivo de símbolo.|
|[IDiaSymbol::get_isVirtualInheritance](../../debugger/debug-interface-access/idiasymbol-get-isvirtualinheritance.md)|Especifica se o `this` ponteiro aponta para um membro de dados com herança virtual.|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|Recupera o idioma da origem.|
|[IDiaSymbol::get_length](../../debugger/debug-interface-access/idiasymbol-get-length.md)|Recupera o número de bytes de memória usados pelo objeto representado por este símbolo.|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|Recupera uma referência ao pai léxico do símbolo.|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|Recupera o identificador pai léxico do símbolo.|
|[IDiaSymbol::get_libraryName](../../debugger/debug-interface-access/idiasymbol-get-libraryname.md)|Recupera o nome do arquivo da biblioteca ou do arquivo de objeto do qual o objeto foi carregado.|
|[IDiaSymbol::get_liveRangeLength](../../debugger/debug-interface-access/idiasymbol-get-liverangelength.md)|Retorna o comprimento do intervalo de endereços no qual o símbolo local é válido.|
|[IDiaSymbol::get_liveRangeStartAddressSection](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddresssection.md)|Retorna a parte da seção do intervalo de endereços inicial no qual o símbolo local é válido.|
|[IDiaSymbol::get_liveRangeStartAddressOffset](../../debugger/debug-interface-access/idiasymbol-get-liverangestartaddressoffset.md)|Retorna a parte de deslocamento do intervalo de endereços inicial no qual o símbolo local é válido.|
|[IDiaSymbol::get_liveRangeStartRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-liverangestartrelativevirtualaddress.md)|Retorna o início do intervalo de endereços no qual o símbolo local é válido.|
|[IDiaSymbol::get_locationType](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)|Recupera o tipo de local de um símbolo de dados.|
|[IDiaSymbol::get_lowerBound](../../debugger/debug-interface-access/idiasymbol-get-lowerbound.md)|Recupera o limite inferior de uma dimensão de matriz FORTRAN.|
|[IDiaSymbol::get_lowerBoundId](../../debugger/debug-interface-access/idiasymbol-get-lowerboundid.md)|Recupera o identificador de símbolo do limite inferior de uma dimensão de matriz FORTRAN.|
|[IDiaSymbol::get_machineType](../../debugger/debug-interface-access/idiasymbol-get-machinetype.md)|Recupera o tipo da CPU de destino.|
|[IDiaSymbol::get_managed](../../debugger/debug-interface-access/idiasymbol-get-managed.md)|Recupera um sinalizador que indica se o símbolo refere-se ao código gerenciado.|
|[IDiaSymbol::get_memorySpaceKind](../../debugger/debug-interface-access/idiasymbol-get-memoryspacekind.md)|Recupera o tipo de espaço de memória.|
|[IDiaSymbol::get_msil](../../debugger/debug-interface-access/idiasymbol-get-msil.md)|Recupera um sinalizador que indica se o símbolo refere-se ao código MSIL (Microsoft Intermediate Language).|
|[IDiaSymbol::get_name](../../debugger/debug-interface-access/idiasymbol-get-name.md)|Recupera o nome do símbolo.|
|[IDiaSymbol::get_nested](../../debugger/debug-interface-access/idiasymbol-get-nested.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário está aninhado.|
|[IDiaSymbol::get_noInline](../../debugger/debug-interface-access/idiasymbol-get-noinline.md)|Recupera um sinalizador que indica se a função está marcada com o atributo [noinline](/cpp/cpp/noinline) .|
|[IDiaSymbol::get_noReturn](../../debugger/debug-interface-access/idiasymbol-get-noreturn.md)|Recupera um sinalizador que indica se a função foi declarada com o atributo [noreturn](/cpp/cpp/noreturn) .|
|[IDiaSymbol::get_noStackOrdering](../../debugger/debug-interface-access/idiasymbol-get-nostackordering.md)|Recupera um sinalizador que indica se nenhuma ordem de pilha pode ser feita como parte da verificação do buffer de pilha.|
|[IDiaSymbol::get_notReached](../../debugger/debug-interface-access/idiasymbol-get-notreached.md)|Recupera um sinalizador que indica se a função ou o rótulo nunca é alcançado.|
|[IDiaSymbol::get_numberOfAcceleratorPointerTags](../../debugger/debug-interface-access/idiasymbol-get-numberofacceleratorpointertags.md)|Retorna o número de marcas do ponteiro do acelerador em uma C++ AMP função de stub.|
|[IDiaSymbol::get_numberOfModifiers](../../debugger/debug-interface-access/idiasymbol-get-numberofmodifiers.md)|Recupera o número de modificadores que são aplicados ao tipo original.|
|[IDiaSymbol::get_numberOfRegisterIndices](../../debugger/debug-interface-access/idiasymbol-get-numberofregisterindices.md)|Recupera o número de índices de registro.|
|[IDiaSymbol::get_numberOfRows](../../debugger/debug-interface-access/idiasymbol-get-numberofrows.md)|Recupera o número de linhas na matriz.|
|[IDiaSymbol::get_numberOfColumns](../../debugger/debug-interface-access/idiasymbol-get-numberofcolumns.md)|Recupera o número de colunas na matriz.|
|[IDiaSymbol::get_objectFileName](../../debugger/debug-interface-access/idiasymbol-get-objectfilename.md)|Recupera o nome do arquivo de objeto.|
|[IDiaSymbol::get_objectPointerType](../../debugger/debug-interface-access/idiasymbol-get-objectpointertype.md)|Recupera o tipo do ponteiro de objeto para um método de classe.|
|[IDiaSymbol::get_oemId](../../debugger/debug-interface-access/idiasymbol-get-oemid.md)|Recupera o valor do símbolo `oemId` .|
|[IDiaSymbol::get_oemSymbolId](../../debugger/debug-interface-access/idiasymbol-get-oemsymbolid.md)|Recupera o valor do símbolo `oemSymbolId` .|
|[IDiaSymbol::get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md)|Recupera o deslocamento do local do símbolo.|
|[IDiaSymbol::get_optimizedCodeDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-optimizedcodedebuginfo.md)|Recupera um sinalizador que indica se a função ou o rótulo contém código otimizado, bem como informações de depuração.|
|[IDiaSymbol::get_overloadedOperator](../../debugger/debug-interface-access/idiasymbol-get-overloadedoperator.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário tem operadores sobrecarregados.|
|[IDiaSymbol::get_packed](../../debugger/debug-interface-access/idiasymbol-get-packed.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário está embalado.|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|Recupera o tipo de plataforma para o qual o programa ou o compiland foi compilado.|
|[IDiaSymbol::get_pure](../../debugger/debug-interface-access/idiasymbol-get-pure.md)|Recupera um sinalizador que indica se a função é virtual puro.|
|[IDiaSymbol::get_rank](../../debugger/debug-interface-access/idiasymbol-get-rank.md)|Recupera a classificação de uma matriz multidimensional FORTRAN.|
|[IDiaSymbol::get_reference](../../debugger/debug-interface-access/idiasymbol-get-reference.md)|Recupera um sinalizador que indica se um tipo de ponteiro é uma referência.|
|[IDiaSymbol::get_registerId](../../debugger/debug-interface-access/idiasymbol-get-registerid.md)|Recupera o designador de registro do local.|
|[IDiaSymbol::get_registerType](../../debugger/debug-interface-access/idiasymbol-get-registertype.md)|Recupera o tipo de registro.|
|[IDiaSymbol::get_relativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-relativevirtualaddress.md)|Recupera o endereço virtual relativo (RVA) do local.|
|[IDiaSymbol::get_restrictedType](../../debugger/debug-interface-access/idiasymbol-get-restrictedtype.md)|Especifica se o `this` ponteiro está sinalizado como restrito.|
|[IDiaSymbol::get_samplerSlot](../../debugger/debug-interface-access/idiasymbol-get-samplerslot.md)|Recupera o slot de amostra.|
|[IDiaSymbol::get_scoped](../../debugger/debug-interface-access/idiasymbol-get-scoped.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário aparece em um escopo léxico não global.|
|[IDiaSymbol::get_signature](../../debugger/debug-interface-access/idiasymbol-get-signature.md)|Recupera o valor de assinatura do símbolo.|
|[IDiaSymbol::get_sizeInUdt](../../debugger/debug-interface-access/idiasymbol-get-sizeinudt.md)|Recupera o tamanho de um membro de um tipo definido pelo usuário.|
|[IDiaSymbol::get_slot](../../debugger/debug-interface-access/idiasymbol-get-slot.md)|Recupera o número de slot do local.|
|[IDiaSymbol::get_sourceFileName](../../debugger/debug-interface-access/idiasymbol-get-sourcefilename.md)|Recupera o nome de arquivo do arquivo de origem.|
|[IDiaSymbol::getSrcLineOnTypeDefn](../../debugger/debug-interface-access/idiasymbol-getsrclineontypedefn.md)|Recupera o arquivo de origem e o número de linha que indicam onde um tipo definido pelo usuário especificado é definido.|
|[IDiaSymbol::get_stride](../../debugger/debug-interface-access/idiasymbol-get-stride.md)|Recupera o stride da matriz ou da matriz substituída.|
|[IDiaSymbol::get_subType](../../debugger/debug-interface-access/idiasymbol-get-subtype.md)|Recupera o subtipo.|
|[IDiaSymbol::get_subTypeId](../../debugger/debug-interface-access/idiasymbol-get-subtypeid.md)|Recupera a ID do subtipo.|
|[IDiaSymbol::get_symbolsFileName](../../debugger/debug-interface-access/idiasymbol-get-symbolsfilename.md)|Recupera o nome do arquivo do qual os símbolos foram carregados.|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|Recupera o identificador de símbolo exclusivo.|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|Recupera o classificador de tipo de símbolo.|
|[IDiaSymbol::get_targetOffset](../../debugger/debug-interface-access/idiasymbol-get-targetoffset.md)|Recupera a seção de deslocamento de um destino de conversão.|
|[IDiaSymbol::get_targetRelativeVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetrelativevirtualaddress.md)|Recupera o endereço virtual relativo (RVA) de um destino de conversão.|
|[IDiaSymbol::get_targetSection](../../debugger/debug-interface-access/idiasymbol-get-targetsection.md)|Recupera a seção de endereço de um destino de conversão.|
|[IDiaSymbol::get_targetVirtualAddress](../../debugger/debug-interface-access/idiasymbol-get-targetvirtualaddress.md)|Recupera o endereço virtual (VA) de um destino de conversão.|
|[IDiaSymbol::get_textureSlot](../../debugger/debug-interface-access/idiasymbol-get-textureslot.md)|Recupera o slot de textura.|
|[IDiaSymbol::get_thisAdjust](../../debugger/debug-interface-access/idiasymbol-get-thisadjust.md)|Recupera o `this` ajustador lógico para o método.|
|[IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)|Recupera o tipo de conversão de uma função.|
|[IDiaSymbol::get_timeStamp](../../debugger/debug-interface-access/idiasymbol-get-timestamp.md)|Recupera o carimbo de data/hora do arquivo executável subjacente.|
|[IDiaSymbol::get_token](../../debugger/debug-interface-access/idiasymbol-get-token.md)|Recupera o token de metadados de uma função ou variável gerenciada.|
|[IDiaSymbol::get_type](../../debugger/debug-interface-access/idiasymbol-get-type.md)|Recupera uma referência à assinatura da função.|
|[IDiaSymbol::get_typeId](../../debugger/debug-interface-access/idiasymbol-get-typeid.md)|Recupera o identificador de tipo do símbolo.|
|[IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)|Recupera uma matriz de valores de tipo específicos do compilador para este símbolo.|
|[IDiaSymbol::get_typeIds](../../debugger/debug-interface-access/idiasymbol-get-typeids.md)|Recupera uma matriz de valores de identificador de tipo específicos do compilador para este símbolo.|
|[IDiaSymbol::get_uavSlot](../../debugger/debug-interface-access/idiasymbol-get-uavslot.md)|Recupera o slot UAV.|
|[IDiaSymbol::get_udtKind](../../debugger/debug-interface-access/idiasymbol-get-udtkind.md)|Recupera a variedade de um tipo definido pelo usuário (UDT).|
|[IDiaSymbol::get_unalignedType](../../debugger/debug-interface-access/idiasymbol-get-unalignedtype.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário está desalinhado.|
|[IDiaSymbol::get_undecoratedName](../../debugger/debug-interface-access/idiasymbol-get-undecoratedname.md)|Recupera o nome não decorado para um nome de C++ decorado ou de vinculação.|
|[IDiaSymbol::get_undecoratedNameEx](../../debugger/debug-interface-access/idiasymbol-get-undecoratednameex.md)|Extensão do `get_undecoratedName` método que recupera o nome não decorado com base no valor de um campo de extensão.|
|[IDiaSymbol::get_unmodifiedTypeId](../../debugger/debug-interface-access/idiasymbol-get-unmodifiedtypeid.md)|Recupera a ID do tipo original (não modificado).|
|[IDiaSymbol::get_upperBound](../../debugger/debug-interface-access/idiasymbol-get-upperbound.md)|Recupera o limite superior de uma dimensão de matriz FORTRAN.|
|[IDiaSymbol::get_upperBoundId](../../debugger/debug-interface-access/idiasymbol-get-upperboundid.md)|Recupera o identificador de símbolo do limite superior de uma dimensão de matriz FORTRAN.|
|[IDiaSymbol::get_value](../../debugger/debug-interface-access/idiasymbol-get-value.md)|Recupera o valor de uma constante.|
|[IDiaSymbol::get_virtual](../../debugger/debug-interface-access/idiasymbol-get-virtual.md)|Recupera um sinalizador que indica se a função é virtual.|
|[IDiaSymbol::get_virtualAddress](../../debugger/debug-interface-access/idiasymbol-get-virtualaddress.md)|Recupera o endereço virtual (VA) do local.|
|[IDiaSymbol::get_virtualBaseClass](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseclass.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário é uma classe base virtual.|
|[IDiaSymbol::get_virtualBaseDispIndex](../../debugger/debug-interface-access/idiasymbol-get-virtualbasedispindex.md)|Recupera o índice para a tabela de deslocamento de base virtual.|
|[IDiaSymbol::get_virtualBaseOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbaseoffset.md)|Recupera o deslocamento na tabela de funções virtuais de uma função virtual.|
|[IDiaSymbol::get_virtualBasePointerOffset](../../debugger/debug-interface-access/idiasymbol-get-virtualbasepointeroffset.md)|Recupera o deslocamento do ponteiro de base virtual.|
|[IDiaSymbol::get_virtualBaseTableType](../../debugger/debug-interface-access/idiasymbol-get-virtualbasetabletype.md)|Recupera o tipo de um ponteiro de tabela base virtual.|
|[IDiaSymbol::get_virtualTableShape](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshape.md)|Recupera a interface de símbolo do tipo da tabela virtual para um tipo definido pelo usuário.|
|[IDiaSymbol::get_virtualTableShapeId](../../debugger/debug-interface-access/idiasymbol-get-virtualtableshapeid.md)|Recupera o identificador da forma da tabela virtual do símbolo.|
|[IDiaSymbol::get_volatileType](../../debugger/debug-interface-access/idiasymbol-get-volatiletype.md)|Recupera um sinalizador que indica se o tipo de dados definido pelo usuário é volátil.|

## <a name="remarks"></a>Comentários

## <a name="notes-for-callers"></a>Observações para chamadores
Obtenha essa interface chamando um dos seguintes métodos:

- [IDiaEnumSymbols::Item](../../debugger/debug-interface-access/idiaenumsymbols-item.md)

- [IDiaEnumSymbols::Next](../../debugger/debug-interface-access/idiaenumsymbols-next.md)

- [IDiaEnumSymbolsByAddr::Next](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-next.md)

- [IDiaEnumSymbolsByAddr::Prev](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-prev.md)

- [IDiaEnumSymbolsByAddr::symbolByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyaddr.md)

- [IDiaEnumSymbolsByAddr::symbolByRVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyrva.md)

- [IDiaEnumSymbolsByAddr::symbolByVA](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr-symbolbyva.md)

- [IDiaSession::findSymbolByAddr](../../debugger/debug-interface-access/idiasession-findsymbolbyaddr.md)

- [IDiaSession::findSymbolByRVA](../../debugger/debug-interface-access/idiasession-findsymbolbyrva.md)

- [IDiaSession::findSymbolByRVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyrvaex.md)

- [IDiaSession::findSymbolByVA](../../debugger/debug-interface-access/idiasession-findsymbolbyva.md)

- [IDiaSession::findSymbolByVAEx](../../debugger/debug-interface-access/idiasession-findsymbolbyvaex.md)

- [IDiaSession::findSymbolByToken](../../debugger/debug-interface-access/idiasession-findsymbolbytoken.md)

- [IDiaSession::symbolById](../../debugger/debug-interface-access/idiasession-symbolbyid.md)

- [IDiaStackWalkHelper::symbolForVA](../../debugger/debug-interface-access/idiastackwalkhelper-symbolforva.md)

- [IDiaSymbol::get_types](../../debugger/debug-interface-access/idiasymbol-get-types.md)

## <a name="example"></a>Exemplo
Este exemplo mostra como exibir as variáveis locais para uma função em um determinado endereço virtual relativo. Ele também mostra como os símbolos de tipos diferentes estão relacionados entre si.

> [!NOTE]
> `CDiaBSTR`é uma classe que encapsula um `BSTR` e automaticamente trata a liberação da cadeia de caracteres quando a instanciação sai do escopo.

```C++
void DumpLocalVars( DWORD rva, IDiaSession *pSession )
{
    CComPtr< IDiaSymbol > pBlock;
    if ( FAILED( psession->findSymbolByRVA( rva, SymTagBlock, &pBlock ) ) )
    {
        Fatal( "Failed to find symbols by RVA" );
    }
    CComPtr< IDiaSymbol > pscope;
    for ( ; pBlock != NULL; )
    {
        CComPtr< IDiaEnumSymbols > pEnum;
        // local data search
        if ( FAILED( pBlock->findChildren( SymTagNull, NULL, nsNone, &pEnum ) ) )
        {
            Fatal( "Local scope findChildren failed" );
        }
        CComPtr< IDiaSymbol > pSymbol;
        DWORD tag;
        DWORD celt;
        while ( pEnum != NULL &&
                SUCCEEDED( pEnum->Next( 1, &pSymbol, &celt ) ) &&
                celt == 1)
        {
            pSymbol->get_symTag( &tag );
            if ( tag == SymTagData )
            {
                CDiaBSTR name;
                DWORD    kind;
                pSymbol->get_name( &name );
                pSymbol->get_dataKind( &kind );
                if ( name != NULL )
                    wprintf_s( L"\t%s (%s)\n", name, szDataKinds[ kind ] );
            }
            else if ( tag == SymTagAnnotation )
            {
                CComPtr< IDiaEnumSymbols > pValues;
                // local data search
                wprintf_s( L"\tAnnotation:\n" );
                if ( FAILED( pSymbol->findChildren( SymTagNull, NULL, nsNone, &pValues ) ) )
                    Fatal( "Annotation findChildren failed" );
                pSymbol = NULL;
                while ( pValues != NULL &&
                        SUCCEEDED( pValues->Next( 1, &pSymbol, &celt ) ) &&
                        celt == 1 )
                {
                    CComVariant value;
                    if ( pSymbol->get_value( &value ) != S_OK )
                        Fatal( "No value for annotation data." );
                    wprintf_s( L"\t\t%ws\n", value.bstrVal );
                    pSymbol = NULL;
                }
            }
            pSymbol = NULL;
        }
        pBlock->get_symTag( &tag );
        if ( tag == SymTagFunction )    // stop when at function scope
            break;
        // move to lexical parent
        CComPtr< IDiaSymbol > pParent;
        if ( SUCCEEDED( pBlock->get_lexicalParent( &pParent ) )
            && pParent != NULL ) {
            pBlock = pParent;
        }
        else
        {
            Fatal( "Finding lexical parent failed." );
        }
    };
}
```

## <a name="requirements"></a>Requisitos
`Header:` Dia2.h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [Hierarquia de classes de tipos de símbolo](../../debugger/debug-interface-access/class-hierarchy-of-symbol-types.md)
- [Símbolos e marcas de símbolos](../../debugger/debug-interface-access/symbols-and-symbol-tags.md)
- [Compiland](../../debugger/debug-interface-access/compiland.md)
