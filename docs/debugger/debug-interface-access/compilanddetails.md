---
title: CompilandDetails | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b72a5ae53c336877c68cc9b164cf787017dacbe2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72745414"
---
# <a name="compilanddetails"></a>CompilandDetails
As informações de compiland são divididas entre os símbolos com uma marca de `SymTagCompiland` (baixo detalhe) e uma marca de `SymTagCompilandDetails` (alto detalhe). `SymTagCompilandDetails` requer o carregamento de símbolos adicionais. No entanto, ele fornece uma grande quantidade de informações sobre o compiland que não está disponível com um símbolo de `SymTagCompiland`.

## <a name="properties"></a>Propriedades
 A tabela a seguir mostra as propriedades que são válidas para esse tipo de símbolo.

|propriedade|Tipo de dados|Descrição|
|--------------|---------------|-----------------|
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|Número de compilação de back-end do compilador.|
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|Número de versão principal de back-end do compilador.|
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|Número de versão secundária de back-end do compilador.|
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|Nome do compilador que produziu este compiland (somente no DIA SDK V 8.0 ou posterior).|
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` se editar e continuar foram habilitados na compilação.|
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|Número de Build de front-end do compilador.|
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|Número de versão principal de front-end do compilador.|
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|Número de versão secundária de front-end do compilador.|
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|`TRUE` se esse compiland tiver informações de depuração (somente no DIA SDK V 8.0 ou posterior).|
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|`TRUE` se este compiland contiver código gerenciado (somente no DIA SDK v 8.0 ou posterior).|
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` se o compiland foi compilado com a opção de compilador [/GS (buffer Security Check)](/cpp/build/reference/gs-buffer-security-check) (somente no dia SDK v 8.0 ou posterior).|
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` se compiland foi convertido de código Common Intermediate Language (CIL) para código nativo.|
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` se os tipos definidos pelo usuário (UDT) foram alinhados a algum limite de memória especificado (somente no DIA SDK V 8.0 ou posterior).|
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` se compiland foi compilado com a opção de compilador [/hotpatch (Create Hotpatchable Image)](/cpp/build/reference/hotpatch-create-hotpatchable-image) (somente no dia SDK v 8.0 ou posterior).|
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` se compiland foi compilado com a opção de compilador [/LTCG (geração de código de tempo de vinculação)](/cpp/build/reference/ltcg-link-time-code-generation) (somente no dia SDK v 8.0 ou posterior).|
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|TRUE se compiland for um módulo MSIL (Microsoft Intermediate Language) (somente no DIA SDK v 8.0 ou posterior).|
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|Linguagem de código-fonte.|
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|Símbolo para o compiland.|
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|ID do símbolo pai léxico.|
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|Plataforma na qual o compiland foi compilado (um dos valores de [Enumeração CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md) ).|
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|ID do índice do símbolo.|
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|Retorna `SymTagCompilandDetails` (um dos valores de [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md) ).|

## <a name="remarks"></a>Comentários
 Os compiladores geralmente vêm em um formato conhecido como um compilador de duas passagens; em algumas versões do compilador, cada passagem é tratada por um programa separado. Eles são conhecidos como compiladores de front-end e back-end, respectivamente, por isso as propriedades de símbolo para números de versão de back-end e front-end.

## <a name="see-also"></a>Consulte também
- [Compiland](../../debugger/debug-interface-access/compiland.md)
- [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)