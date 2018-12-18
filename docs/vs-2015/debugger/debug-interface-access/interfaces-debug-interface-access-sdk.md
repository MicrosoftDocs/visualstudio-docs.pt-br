---
title: Interfaces (SDK de acesso à Interface de depuração) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- interfaces [DIA SDK]
- DIA SDK, interfaces
ms.assetid: 62aee7c3-d314-4272-a32b-b2818f32fab8
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d74f42008a76fb9b3f5ac6966ec01721bcb32cac
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809331"
---
# <a name="interfaces-debug-interface-access-sdk"></a>Interfaces (SDK de Acesso à Interface de Depuração)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Métodos estão listados em ordem alfabética em cada interface na tabela de conteúdo e na página de interface na ordem de Vtable.  
  
## <a name="in-this-section"></a>Nesta seção  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)  
 Fornece controle sobre como o DIA SDK calcula relativos e virtuais endereços virtuais para objetos de depuração.  
  
 [IDiaDataSource](../../debugger/debug-interface-access/idiadatasource.md)  
 Inicia o acesso a uma fonte de símbolos de depuração.  
  
 [IDiaEnumDebugStreamData](../../debugger/debug-interface-access/idiaenumdebugstreamdata.md)  
 Fornece acesso aos registros em um fluxo de dados de depuração.  
  
 [IDiaEnumDebugStreams](../../debugger/debug-interface-access/idiaenumdebugstreams.md)  
 Enumera os vários fluxos de depuração contidos na fonte de dados.  
  
 [IDiaEnumFrameData](../../debugger/debug-interface-access/idiaenumframedata.md)  
 Enumera os vários elementos de dados do quadro contidos na fonte de dados.  
  
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
 Enumera os vários quadros de pilha disponível.  
  
 [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)  
 Enumera os vários símbolos contidos na fonte de dados.  
  
 [IDiaEnumSymbolsByAddr](../../debugger/debug-interface-access/idiaenumsymbolsbyaddr.md)  
 Enumera os vários símbolos contidos na fonte de dados por endereço.  
  
 [IDiaEnumTables](../../debugger/debug-interface-access/idiaenumtables.md)  
 Enumera as várias tabelas contidas na fonte de dados.  
  
 [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)  
 Expõe os detalhes de um quadro de pilha.  
  
 [IDiaImageData](../../debugger/debug-interface-access/idiaimagedata.md)  
 Expõe os detalhes da base deslocamentos da memória e o local do módulo ou da imagem.  
  
 [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)  
 Acessa o código-fonte armazenado na fonte de dados do DIA.  
  
 [IDiaLineNumber](../../debugger/debug-interface-access/idialinenumber.md)  
 Acessa as informações que descreve o processo de mapeamento de um bloco de bytes de texto da imagem para um número de linha do arquivo de origem.  
  
 [IDiaLoadCallback](../../debugger/debug-interface-access/idialoadcallback.md)  
 Receber retornos de chamada do símbolo de DIA de localizar o procedimento, permitindo que uma interface do usuário relatar o progresso da tentativa de local.  
  
 [IDiaLoadCallback2](../../debugger/debug-interface-access/idialoadcallback2.md)  
 Receber retornos de chamada do símbolo de DIA de localizar o procedimento, permitindo que as restrições a serem impostas sobre o processo de localização.  
  
 [IDiaPropertyStorage](../../debugger/debug-interface-access/idiapropertystorage.md)  
 Permite que você leia as propriedades persistentes de um conjunto de propriedades do DIA.  
  
 [IDiaReadExeAtRVACallback](../../debugger/debug-interface-access/idiareadexeatrvacallback.md)  
 Permite que um aplicativo cliente para fornecer os bytes de um arquivo executável, conforme especificado pela posição do arquivo.  
  
 [IDiaReadExeAtOffsetCallback](../../debugger/debug-interface-access/idiareadexeatoffsetcallback.md)  
 Permite que um aplicativo cliente para fornecer os bytes de um arquivo executável, conforme especificado por um endereço virtual relativo.  
  
 [IDiaSectionContrib](../../debugger/debug-interface-access/idiasectioncontrib.md)  
 Recupera os dados que descrevem uma contribuição de seção, ou seja, um bloco contíguo de memória contribuição para a imagem de um compiland.  
  
 [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)  
 Mapeia dados de número de seção para segmentos de espaço de endereço.  
  
 [IDiaSession](../../debugger/debug-interface-access/idiasession.md)  
 Fornece um contexto de consulta para símbolos de depuração.  
  
 [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)  
 Representa um arquivo de origem.  
  
 [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)  
 Expõe as propriedades de um quadro de pilha.  
  
 [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)  
 Fornece métodos para fazer uma pilha de percorrer usando o arquivo PDB.  
  
 [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)  
 Mantém o contexto de pilha entre invocações da [idiaframedata:: execute](../../debugger/debug-interface-access/idiaframedata-execute.md) método.  
  
 [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)  
 Facilita a movimentar a pilha usando o arquivo de banco de dados (PDB) de depuração do programa.  
  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)  
 Descreve as propriedades de uma instância de símbolo.  
  
 [IDiaTable](../../debugger/debug-interface-access/idiatable.md)  
 Enumera uma tabela de fonte de dados do DIA.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)  
 Descreve as enumerações e estruturas usadas por várias interfaces do SDK do DIA.  
  
 [Constantes (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/constants-debug-interface-access-sdk.md)  
 Descreve as constantes disponíveis no SDK do DIA.  
  
## <a name="see-also"></a>Consulte também  
 [Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)



