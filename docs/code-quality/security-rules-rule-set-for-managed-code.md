---
title: Conjunto de regras de segurança para código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 564aeac6-03fa-41b0-b655-88179f0ab01b
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 6712454fad2acaf57b3cb4d8f1740366a396ec6e
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31925036"
---
# <a name="security-rules-rule-set-for-managed-code"></a>Conjunto de regras de segurança para código gerenciado
Você deve incluir o Microsoft Security conjunto de regras para maximizar o número de possíveis problemas de segurança que são relatados.

|Regra|Descrição|
|----------|-----------------|
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|Revisar as consultas SQL para vulnerabilidades de segurança|
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|Capturar exceções não CLSCompliant em manipuladores gerais|
|[CA2103](../code-quality/ca2103-review-imperative-security.md)|Revisar segurança obrigatória|
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|Não declarar tipos de referência mutáveis somente leitura|
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|Campos de matriz não devem ser somente leitura|
|[CA2106](../code-quality/ca2106-secure-asserts.md)|Declarações seguras|
|[CA2107](../code-quality/ca2107-review-deny-and-permit-only-usage.md)|Revisar deny e permit uso somente|
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|Revisar segurança declarativa em tipos de valor|
|[CA2109](../code-quality/ca2109-review-visible-event-handlers.md)|Revise os manipuladores de eventos visíveis|
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|Ponteiros não devem ser visíveis|
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|Tipos protegidos não devem expor campos|
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|Segurança do método deve ser um superconjunto de tipo|
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|Chame GC. KeepAlive ao usar recursos nativos|
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|Métodos APTCA só devem chamar métodos APTCA|
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|Os tipos APTCA só devem estender tipos base APTCA|
|[CA2118](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md)|Revise o uso de SuppressUnmanagedCodeSecurityAttribute|
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|Métodos de lacre que satisfazem interfaces privadas|
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|Proteger construtores de serialização|
|[CA2121 OS](../code-quality/ca2121-static-constructors-should-be-private.md)|Construtores estáticos devem ser privados|
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|Não exponha indiretamente métodos com demandas de link|
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|Demandas de link de substituição devem ser idênticas de base|
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|Wrap vulnerável finalmente tente cláusulas externa|
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|Demandas de link do tipo exigem demandas de herança|
|[CA2130](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|Constantes críticas de segurança devem ser transparentes|
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|Tipos críticos de segurança não podem participar de equivalência de tipo|
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|Construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base|
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|Delegados devem ligar a métodos com transparência consistente|
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|Métodos devem manter uma transparência consistente quando os métodos base|
|[CA2135](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|Assemblies de nível 2 não devem conter LinkDemands|
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|Membros não devem ter anotações de transparência conflitantes|
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|Os métodos transparentes devem conter apenas IL verificável|
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|Os métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity|
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|Os métodos transparentes não podem usar o atributo HandleProcessCorruptingExceptions|
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|Código transparente não deve fazer referência a itens críticos de segurança|
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|Os métodos transparentes não devem atender a LinkDemands|
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|Código transparente não deve ser protegido com LinkDemands|
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|Os métodos transparentes não devem usar demandas de segurança|
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|Código transparente não deve carregar assemblies de matrizes de bytes|
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|Os métodos transparentes não devem ser decorados com o SuppressUnmanagedCodeSecurityAttribute|
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|Os tipos devem ser pelo menos críticos como seus tipos base e interfaces|
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|Os métodos transparentes não podem usar segurança declarações|
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|Os métodos transparentes não devem chamar código nativo|
|[CA2210](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md)|Assemblies devem ter nomes fortes válidos|