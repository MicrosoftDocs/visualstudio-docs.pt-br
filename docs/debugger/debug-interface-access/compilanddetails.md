---
title: CompilandDetails | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- CompilandDetails symbol
ms.assetid: ddc7d794-c622-4c63-b2a6-72f8b2d0022a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8b1288a3bde1a8d17f40971744298adb1e1ecffb
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31468802"
---
# <a name="compilanddetails"></a>CompilandDetails
Informações Compiland são divididas entre os símbolos com um `SymTagCompiland` marca (nível baixo de detalhe) e um `SymTagCompilandDetails` marca (alta detalhes). `SymTagCompilandDetails` requer o carregamento de símbolos adicionais. No entanto, ele fornece uma grande quantidade de informações sobre o compiland não está disponível com um `SymTagCompiland` símbolo.  
  
## <a name="properties"></a>Propriedades  
 A tabela a seguir mostra as propriedades que são válidas para este tipo de símbolo.  
  
|Propriedade|Tipo de dados|Descrição|  
|--------------|---------------|-----------------|  
|[IDiaSymbol::get_backEndBuild](../../debugger/debug-interface-access/idiasymbol-get-backendbuild.md)|`DWORD`|Número de compilação de back-end do compilador.|  
|[IDiaSymbol::get_backEndMajor](../../debugger/debug-interface-access/idiasymbol-get-backendmajor.md)|`DWORD`|Número de versão principal do back-end do compilador.|  
|[IDiaSymbol::get_backEndMinor](../../debugger/debug-interface-access/idiasymbol-get-backendminor.md)|`DWORD`|Número de versão secundária do back-end do compilador.|  
|[IDiaSymbol::get_compilerName](../../debugger/debug-interface-access/idiasymbol-get-compilername.md)|`BSTR`|Nome do compilador que gerou este compiland (somente no v 8.0 do SDK do DIA ou posterior).|  
|[IDiaSymbol::get_editAndContinueEnabled](../../debugger/debug-interface-access/idiasymbol-get-editandcontinueenabled.md)|`BOOL`|`TRUE` Se editar e continuar foram habilitados na compilação.|  
|[IDiaSymbol::get_frontEndBuild](../../debugger/debug-interface-access/idiasymbol-get-frontendbuild.md)|`DWORD`|Número de compilação de front-end do compilador.|  
|[IDiaSymbol::get_frontEndMajor](../../debugger/debug-interface-access/idiasymbol-get-frontendmajor.md)|`DWORD`|Número de versão principal de front-end do compilador.|  
|[IDiaSymbol::get_frontEndMinor](../../debugger/debug-interface-access/idiasymbol-get-frontendminor.md)|`DWORD`|Número de versão secundária front-end do compilador.|  
|[IDiaSymbol::get_hasDebugInfo](../../debugger/debug-interface-access/idiasymbol-get-hasdebuginfo.md)|`BOOL`|`TRUE` Se este compiland tem informações de depuração (somente no v 8.0 do SDK do DIA ou posterior).|  
|[IDiaSymbol::get_hasManagedCode](../../debugger/debug-interface-access/idiasymbol-get-hasmanagedcode.md)|`BOOL`|`TRUE` Se este compiland contém código gerenciado (somente no v DIA SDK 8.0 ou posterior).|  
|[IDiaSymbol::get_hasSecurityChecks](../../debugger/debug-interface-access/idiasymbol-get-hassecuritychecks.md)|`BOOL`|`TRUE` Se o compiland foi compilado com o [/GS (verificação de segurança do Buffer)](/cpp/build/reference/gs-buffer-security-check) opção de compilador (somente no v 8.0 do SDK do DIA ou posterior).|  
|[IDiaSymbol::get_isCVTCIL](../../debugger/debug-interface-access/idiasymbol-get-iscvtcil.md)|`BOOL`|`TRUE` Se compiland foi convertido de código de idioma intermediário comum (CIL) em código nativo.|  
|[IDiaSymbol::get_isDataAligned](../../debugger/debug-interface-access/idiasymbol-get-isdataaligned.md)|`BOOL`|`TRUE` Se os tipos definidos pelo usuário (UDT) tiveram sido alinhados com alguns especificado limites de memória (somente no v 8.0 do SDK do DIA ou posterior).|  
|[IDiaSymbol::get_isHotpatchable](../../debugger/debug-interface-access/idiasymbol-get-ishotpatchable.md)|`BOOL`|`TRUE` Se compiland foi compilado com o [/hotpatch (Criar imagem de Hotpatchable)](/cpp/build/reference/hotpatch-create-hotpatchable-image) opção de compilador (somente no v DIA SDK 8.0 ou posterior).|  
|[IDiaSymbol::get_isLTCG](../../debugger/debug-interface-access/idiasymbol-get-isltcg.md)|`BOOL`|`TRUE` Se compiland foi compilado com o [/LTCG (geração de código Link-time)](/cpp/build/reference/ltcg-link-time-code-generation) opção de compilador (somente no v 8.0 do SDK do DIA ou posterior).|  
|[IDiaSymbol::get_isMSILNetmodule](../../debugger/debug-interface-access/idiasymbol-get-ismsilnetmodule.md)|`BOOL`|TRUE se compiland é um módulo do Microsoft Intermediate Language (MSIL) (somente no v DIA SDK 8.0 ou posterior).|  
|[IDiaSymbol::get_language](../../debugger/debug-interface-access/idiasymbol-get-language.md)|`DWORD`|Linguagem de código fonte.|  
|[IDiaSymbol::get_lexicalParent](../../debugger/debug-interface-access/idiasymbol-get-lexicalparent.md)|`IDiaSymbol*`|Símbolo para o compiland.|  
|[IDiaSymbol::get_lexicalParentId](../../debugger/debug-interface-access/idiasymbol-get-lexicalparentid.md)|`DWORD`|ID do símbolo lexical pai.|  
|[IDiaSymbol::get_platform](../../debugger/debug-interface-access/idiasymbol-get-platform.md)|`DWORD`|Plataforma na qual o compiland foi compilado (um do [enumeração CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md) valores).|  
|[IDiaSymbol::get_symIndexId](../../debugger/debug-interface-access/idiasymbol-get-symindexid.md)|`DWORD`|ID de índice de símbolo.|  
|[IDiaSymbol::get_symTag](../../debugger/debug-interface-access/idiasymbol-get-symtag.md)|`DWORD`|Retorna `SymTagCompilandDetails` (um do [SymTagEnum enumeração](../../debugger/debug-interface-access/symtagenum.md) valores).|  
  
## <a name="remarks"></a>Comentários  
 Compiladores geralmente vêm em um formato conhecido como um compilador dois passos; em algumas versões do compilador, cada fase é tratada por um programa separado. Eles são conhecidos como compiladores de front-end e back-end, respectivamente, portanto, as propriedades de símbolo para números de versão de front-end e back-end.  
  
## <a name="see-also"></a>Consulte também  
 [Compiland](../../debugger/debug-interface-access/compiland.md)   
 [Hierarquia lexical de tipos de símbolo](../../debugger/debug-interface-access/lexical-hierarchy-of-symbol-types.md)