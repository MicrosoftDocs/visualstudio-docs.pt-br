---
title: Interfaces (debug interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 902a3d361eb06288a0e50e9f384b67a2a8c61aa1
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461269"
---
# <a name="interfaces-debug-interface-access-sdk"></a>Interfaces (SDK de Acesso à Interface de Depuração)
Os métodos são listados em ordem alfabética em cada interface no sumário e na página de interface em ordem vtable.

## <a name="in-this-section"></a>Nesta seção

[IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)

Fornece controle sobre como o DIA SDK computa os endereços virtuais e virtuais relativos para objetos de depuração.

[IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)

Inicia o acesso a uma fonte de símbolos de depuração.

[IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)

Fornece acesso aos registros em um fluxo de dados de depuração.

[IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)

Enumera os vários fluxos de depuração contidos na fonte de dados.

[IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)

Enumera os vários elementos de dados de quadro contidos na fonte de dados.

[IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)

Enumere as várias fontes injetadas contidas na fonte de dados.

[IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)

Enumera os vários números de linha contidos na fonte de dados.

[IDiaEnumSectionContribs](../../debugger/debug-interface-access/idiaenumsectioncontribs.md)

Enumera as várias contribuições de seção contidas na fonte de dados.

[IDiaEnumSegments](../../debugger/debug-interface-access/idiaenumsegments.md)

Enumera os vários segmentos contidos na fonte de dados.

[IDiaEnumSourceFiles](../../debugger/debug-interface-access/idiaenumsourcefiles.md)

Enumera os vários arquivos de origem contidos na fonte de dados.

[IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md)

Enumera os vários quadros de pilhas disponíveis.

[IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)

Enumera os vários símbolos contidos na fonte de dados.

[IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)

Enumera por endereço os vários símbolos contidos na fonte de dados.

[IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)

Enumera as várias tabelas contidas na fonte de dados.

[IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)

Expõe os detalhes de um quadro de pilha.

[IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)

Expõe os detalhes do local de base e dos deslocamentos de memória do módulo ou da imagem.

[IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)

Acessa o código-fonte do programa armazenado na fonte de dados DIA.

[IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)

Acessa informações que descrevem o processo de mapeamento a partir de um bloco de bytes de texto de imagem para um número de linha de arquivo de origem.

[IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)

Recebe retornos de chamada do procedimento de localização de símbolo de DIA, permitindo assim que uma interface do usuário relate o progresso da tentativa de localização.

[IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)

Recebe retornos de chamada do procedimento de localização de símbolo de DIA, permitindo que as restrições sejam impostas no processo de localização.

[IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)

Permite que você leia as propriedades persistentes de um conjunto de propriedades de DIA.

[IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)

Permite que um aplicativo cliente forneça bytes de um arquivo executável, conforme especificado pela posição do arquivo.

[IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)

Permite que um aplicativo cliente forneça bytes de um arquivo executável, conforme especificado por um endereço virtual relativo.

[IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)

Recupera dados que descrevem uma contribuição de seção, ou seja, um bloco contíguo de memória contribuído para a imagem por um compiland.

[IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)

Mapeia dados do número da seção para segmentos de espaço de endereço.

[IDiaSession](../../debugger/debug-interface-access/idiasession.md)

Fornece um contexto de consulta para símbolos de depuração.

[IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)

Representa um arquivo de origem.

[IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)

Expõe as propriedades de um quadro de pilha.

[IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)

Fornece métodos para fazer uma movimentação de pilha usando o arquivo PDB.

[IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)

Mantém o contexto de pilha entre invocações do método [IDiaFrameData:: execute](../../debugger/debug-interface-access/idiaframedata-execute.md) .

[IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)

Facilita a movimentação da pilha usando o arquivo PDB (banco de dados de depuração do programa).

[IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)

Descreve as propriedades de uma instância de símbolo.

[IDiaTable](../../debugger/debug-interface-access/idiatable.md)

Enumera uma tabela de fonte de dados de DIA.

## <a name="related-sections"></a>Seções relacionadas
[Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)

Descreve as enumerações e estruturas usadas pelas várias interfaces do DIA SDK.

[Constantes (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)

Descreve as constantes disponíveis no DIA SDK.

## <a name="see-also"></a>Veja também

- [Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)