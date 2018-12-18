---
title: Estruturas e uniões | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- structures [Visual Studio SDK]
ms.assetid: 9ff0a8f8-1ee6-4fdd-8b80-206436ff589b
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 33e3f5ebb4e871f98b027638f5aae47d853828a8
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31133967"
---
# <a name="structures-and-unions"></a>Estruturas e uniões
A seguir é estruturas e uniões no SDK do Visual Studio de depuração.  
  
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)  
 Especifica a ID do processo, que pode ser uma ID de sistema ou um GUID.  
  
 [BP_CONDITION](../../../extensibility/debugger/reference/bp-condition.md)  
 Descreve as condições sob as quais um ponto de interrupção será acionado.  
  
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)  
 Descreve a resolução de um ponto de interrupção de erro, inclusive local, o programa e o thread.  
  
 [BP_LOCATION](../../../extensibility/debugger/reference/bp-location.md)  
 Especifica o tipo de estrutura usada para descrever o local do ponto de interrupção.  
  
 [BP_LOCATION_CODE_ADDRESS](../../../extensibility/debugger/reference/bp-location-code-address.md)  
 Define os componentes que descrevem a localização de um ponto de interrupção em um endereço no código.  
  
 [BP_LOCATION_CODE_CONTEXT](../../../extensibility/debugger/reference/bp-location-code-context.md)  
 Descreve o local de um ponto de interrupção que está associado diretamente a um endereço no programa que está sendo depurado.  
  
 [BP_LOCATION_CODE_FILE_LINE](../../../extensibility/debugger/reference/bp-location-code-file-line.md)  
 Descreve o local de um ponto de interrupção na linha em um arquivo de origem do código.  
  
 [BP_LOCATION_CODE_FUNC_OFFSET](../../../extensibility/debugger/reference/bp-location-code-func-offset.md)  
 Descreve o local de deslocamento de um ponto de interrupção em uma função em código.  
  
 [BP_LOCATION_CODE_STRING](../../../extensibility/debugger/reference/bp-location-code-string.md)  
 Usada para definir pontos de interrupção de código com base em uma cadeia de caracteres que o usuário pode inserir a partir do IDE.  
  
 [BP_LOCATION_DATA_STRING](../../../extensibility/debugger/reference/bp-location-data-string.md)  
 Usada para definir pontos de interrupção de dados se baseiam em uma cadeia de caracteres que o usuário pode inserir a partir do IDE.  
  
 [BP_LOCATION_RESOLUTION](../../../extensibility/debugger/reference/bp-location-resolution.md)  
 Descreve a resolução de um ponto de interrupção em um local específico.  
  
 [BP_PASSCOUNT](../../../extensibility/debugger/reference/bp-passcount.md)  
 Descreve a contagem e condições no qual um ponto de interrupção será acionado depois de ter que foi passado.  
  
 [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)  
 Contém as informações necessárias para implementar um ponto de interrupção.  
  
 [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)  
 Contém as informações necessárias para implementar um ponto de interrupção (mesmo que o [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md) estrutura mas não inclui informações de GUID, restrição e tracepoint do fornecedor).  
  
 [BP_RESOLUTION_CODE](../../../extensibility/debugger/reference/bp-resolution-code.md)  
 Descreve o local de um ponto de interrupção do código.  
  
 [BP_RESOLUTION_DATA](../../../extensibility/debugger/reference/bp-resolution-data.md)  
 Descreve o resultado da associação a um ponto de interrupção de dados.  
  
 [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)  
 Descreve as informações de ponto de interrupção associado para um ponto de interrupção de código ou um ponto de interrupção de dados.  
  
 [BP_RESOLUTION_LOCATION](../../../extensibility/debugger/reference/bp-resolution-location.md)  
 Especifica a estrutura do local de resolução do ponto de interrupção.  
  
 [BSTR_ARRAY](../../../extensibility/debugger/reference/bstr-array.md)  
 Descreve uma matriz de cadeias de caracteres.  
  
 [BUILT_TYPE](../../../extensibility/debugger/reference/built-type.md)  
 Especifica informações sobre um tipo de campo obtido de metadados.  
  
 [CODE_PATH](../../../extensibility/debugger/reference/code-path.md)  
 Descreve uma chamada para uma função ou método.  
  
 [COMPUTER_INFO](../../../extensibility/debugger/reference/computer-info.md)  
 Descreve o computador no qual o depurador está em execução.  
  
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)  
 Descreve uma lista de GUIDs.  
  
 [CONTEXT_INFO](../../../extensibility/debugger/reference/context-info.md)  
 Descreve um contexto de memória ou o contexto de código.  
  
 [DEBUG_ADDRESS](../../../extensibility/debugger/reference/debug-address.md)  
 Descreve um endereço em um programa que está sendo depurado.  
  
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)  
 Representa um de um número de tipos diferentes de endereços.  
  
 [DEBUG_CUSTOM_VIEWER](../../../extensibility/debugger/reference/debug-custom-viewer.md)  
 Identifica um visualizador personalizado ou tipo de visualizador.  
  
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)  
 Descreve uma propriedade de depuração que por sua vez descreve um objeto de natureza hierárquica que tem o nome, tipo e valor.  
  
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)  
 Descreve uma referência.  
  
 [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)  
 Descreve a desmontagem ao IDE para exibição.  
  
 [EXCEPTION_INFO](../../../extensibility/debugger/reference/exception-info.md)  
 Descreve um erro de tempo de execução gerada pelo programa que está sendo depurado ou exceção.  
  
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)  
 Descreve uma variável local, parâmetro ou outro campo.  
  
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)  
 Descreve um quadro de pilha.  
  
 [GUID_ARRAY](../../../extensibility/debugger/reference/guid-array.md)  
 Descreve uma matriz de identificadores exclusivos para mecanismos de depuração disponíveis.  
  
 [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)  
 Usado para definir as informações de /justmycode para um módulo.  
  
 [MACHINE_INFO](../../../extensibility/debugger/reference/machine-info.md)  
 Descreve uma determinada máquina.  
  
 [METADATA_ADDRESS_ARRAYELEM](../../../extensibility/debugger/reference/metadata-address-arrayelem.md)  
 Descreve um elemento de matriz em uma matriz.  
  
 [METADATA_ADDRESS_FIELD](../../../extensibility/debugger/reference/metadata-address-field.md)  
 Descreve o endereço de um campo de uma classe ou estrutura.  
  
 [METADATA_ADDRESS_LOCAL](../../../extensibility/debugger/reference/metadata-address-local.md)  
 Descreve o endereço de uma variável local dentro de um escopo (geralmente uma função ou método).  
  
 [METADATA_ADDRESS_METHOD](../../../extensibility/debugger/reference/metadata-address-method.md)  
 Descreve o endereço de um método de uma classe.  
  
 [METADATA_ADDRESS_PARAM](../../../extensibility/debugger/reference/metadata-address-param.md)  
 Descreve um parâmetro de um método ou função.  
  
 [METADATA_ADDRESS_RETVAL](../../../extensibility/debugger/reference/metadata-address-retval.md)  
 Descreve o valor de retorno de uma função ou método.  
  
 [METADATA_TYPE](../../../extensibility/debugger/reference/metadata-type.md)  
 Descreve um tipo de campo obtido de metadados.  
  
 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)  
 Descreve um módulo específico (DLL, EXE ou assembly).  
  
 [MODULE_SYMBOL_SEARCH_INFO](../../../extensibility/debugger/reference/module-symbol-search-info.md)  
 Descreve as informações de status sobre os caminhos de pesquisa de símbolo que foram pesquisadas.  
  
 [NATIVE_ADDRESS](../../../extensibility/debugger/reference/native-address.md)  
 Descreve um endereço nativo.  
  
 [PDB_TYPE](../../../extensibility/debugger/reference/pdb-type.md)  
 Descreve um tipo de campo obtido um símbolo PDB.  
  
 [PENDING_BP_STATE_INFO](../../../extensibility/debugger/reference/pending-bp-state-info.md)  
 Descreve o estado de um ponto de interrupção que está pronto para vincular a um local de código.  
  
 [PROCESS_INFO](../../../extensibility/debugger/reference/process-info.md)  
 Descreve um processo.  
  
 [PROGRAM_NODE_ARRAY](../../../extensibility/debugger/reference/program-node-array.md)  
 Descreve uma lista de [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) objetos que representam nós de programa.  
  
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)  
 Descreve os processos em execução em um computador.  
  
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)  
 Descreve o local de linha e coluna no texto especificado.  
  
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)  
 Descreve as propriedades de um thread.  
  
 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)  
 Descreve o tipo do campo.  
  
 [UNMANAGED_ADDRESS_PHYSICAL](../../../extensibility/debugger/reference/unmanaged-address-physical.md)  
 Descreve um endereço físico.  
  
 [UNMANAGED_ADDRESS_THIS_RELATIVE](../../../extensibility/debugger/reference/unmanaged-address-this-relative.md)  
 Descreve um endereço relativo a um `this` ponteiro (`Me` no Visual Basic).  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: msdbg.h, sh.h ou ee.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API](../../../extensibility/debugger/reference/api-reference-visual-studio-debugging.md)