---
title: Conjunto de regras de correção estendida para código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5b181f5b-6c7a-4e46-a783-360e1da427a0
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cebb3f492bb3aec873f503c2efcacb7220ec9739
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49187408"
---
# <a name="extended-correctness-rules-rule-set-for-managed-code"></a>Conjunto de regras de correção estendido para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O conjunto de regras de correção estendido Microsoft maximiza os erros de uso de lógica e do framework que são relatados pela análise de código. Ênfase extra é colocado em cenários específicos, como interoperabilidade COM e aplicativos móveis. Você deve considerar incluindo essa regra definir se um desses cenários se aplica ao seu projeto ou para localizar problemas adicionais em seu projeto.  
  
 O conjunto de regras de regras de correção estendido da Microsoft inclui as regras que estão em regras de correção básico do Microsoft conjunto. As regras básicas de correção incluem as regras que estão na regra de regras recomendadas do Microsoft mínimo definidas. Para obter mais informações, consulte [conjunto de regras de regras de correção básico para código gerenciado](../code-quality/basic-correctness-rules-rule-set-for-managed-code.md) e [gerenciados recomendado conjunto de regras para código gerenciado](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md)  
  
 A tabela a seguir descreve todas as regras no conjunto de regras de regras de correção estendido da Microsoft.  
  
|Regra|Descrição|  
|----------|-----------------|  
|[CA1001](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md)|Tipos que possuem campos descartáveis devem ser descartáveis|  
|[CA1009](../code-quality/ca1009-declare-event-handlers-correctly.md)|Declarar manipuladores de eventos corretamente|  
|[CA1016](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md)|Marcar assemblies com AssemblyVersionAttribute|  
|[CA1033](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md)|Métodos de interface devem ser chamáveis por tipos filho|  
|[CA1049](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)|Tipos que tenham recursos nativos devem ser descartáveis|  
|[CA1060](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md)|Mover P/Invokes para a classe NativeMethods|  
|[CA1061](../code-quality/ca1061-do-not-hide-base-class-methods.md)|Não ocultar métodos de classe base|  
|[CA1063](../code-quality/ca1063-implement-idisposable-correctly.md)|Implementar IDisposable corretamente|  
|[CA1065](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)|Não gerar exceções em locais inesperados|  
|[CA1301](../code-quality/ca1301-avoid-duplicate-accelerators.md)|Evitar aceleradores duplicados|  
|[CA1400](../code-quality/ca1400-p-invoke-entry-points-should-exist.md)|Pontos de entrada P/Invoke devem existir|  
|[CA1401](../code-quality/ca1401-p-invokes-should-not-be-visible.md)|P/Invokes não devem ser visíveis|  
|[CA1403](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)|Tipos de layout automático não devem ser visíveis em COM|  
|[CA1404](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md)|Chamar GetLastError logo depois de P/Invoke|  
|[CA1405](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md)|Tipos de base de tipo visível COM devem ser visíveis em COM|  
|[CA1410](../code-quality/ca1410-com-registration-methods-should-be-matched.md)|OS métodos de registro devem ser correspondidos.|  
|[CA1415](../code-quality/ca1415-declare-p-invokes-correctly.md)|Declarar P/Invokes corretamente|  
|[CA1821](../code-quality/ca1821-remove-empty-finalizers.md)|Remova finalizadores vazios|  
|[CA1900](../code-quality/ca1900-value-type-fields-should-be-portable.md)|Campos de tipo de valor devem ser portáteis|  
|[CA1901](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|Declarações P/Invoke devem ser portáteis|  
|[CA2002](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md)|Não bloquear objetos com identidade fraca|  
|[CA2100](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md)|Revisar as consultas SQL para vulnerabilidades de segurança|  
|[CA2101](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md)|Especificar marshaling para argumentos de cadeia de caracteres P/Invoke|  
|[CA2108](../code-quality/ca2108-review-declarative-security-on-value-types.md)|Revisar segurança declarativa em tipos de valor|  
|[CA2111](../code-quality/ca2111-pointers-should-not-be-visible.md)|Ponteiros não devem ser visíveis|  
|[CA2112](../code-quality/ca2112-secured-types-should-not-expose-fields.md)|Tipos seguros não devem expor campos|  
|[CA2114](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md)|Segurança de método deve ser um superconjunto de tipo|  
|[CA2116](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md)|Os métodos APTCA só devem chamar métodos APTCA|  
|[CA2117](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md)|Os tipos APTCA só devem estender tipos base APTCA|  
|[CA2122](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md)|Não expor indiretamente métodos com demandas de link|  
|[CA2123](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md)|As demandas de link de substituição devem ser idênticas à base|  
|[CA2124](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md)|Encapsulamento vulnerável, por fim, cláusulas em tentativa externa|  
|[CA2126](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md)|Demandas de link de tipo exigem demandas de herança|  
|[CA2131](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md)|Tipos críticos de segurança não podem participar da equivalência de tipo|  
|[CA2132](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md)|Construtores padrão devem ser pelo menos críticos como construtores padrão do tipo base|  
|[CA2133](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md)|Delegados devem associar a métodos com transparência consistente|  
|[CA2134](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md)|Os métodos devem manter uma transparência consistente durante a substituição de métodos base|  
|[CA2137](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md)|Métodos transparentes devem conter apenas IL verificável|  
|[CA2138](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md)|Métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity|  
|[CA2140](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md)|O código transparente não deve fazer referência a itens críticos de segurança|  
|[CA2141](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md)|Métodos transparentes não devem atender a LinkDemands|  
|[CA2146](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md)|Tipos devem ser pelo menos tão críticos quanto seus tipos base e interfaces|  
|[CA2147](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md)|Métodos transparentes não podem usar a segurança declara|  
|[CA2149](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md)|Métodos transparentes não devem chamar código nativo|  
|[CA2200](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)|Relançar para preservar detalhes da pilha|  
|[CA2202](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md)|Não descartar objetos várias vezes|  
|[CA2207](../code-quality/ca2207-initialize-value-type-static-fields-inline.md)|Inicializar campos estáticos de tipo de valor embutido|  
|[CA2212](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md)|Não marcar componentes atendidos com WebMethod|  
|[CA2213](../code-quality/ca2213-disposable-fields-should-be-disposed.md)|Campos descartáveis devem ser descartados|  
|[CA2214](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md)|Não chamar métodos substituíveis em construtores|  
|[CA2216](../code-quality/ca2216-disposable-types-should-declare-finalizer.md)|Os tipos descartáveis devem declarar o finalizador|  
|[CA2220](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md)|Os finalizadores devem chamar o finalizador da classe base|  
|[CA2229](../code-quality/ca2229-implement-serialization-constructors.md)|Implementar construtores de serialização|  
|[CA2231](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)|Sobrecarregar operador equals ao substituir ValueType.Equals&lt;2}&lt;1}|  
|[CA2232](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md)|Pontos de entrada de marca Windows Forms com STAThread|  
|[CA2235](../code-quality/ca2235-mark-all-non-serializable-fields.md)|Marcar todos os campos não serializáveis|  
|[CA2236](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md)|Chamar métodos da classe base em tipos ISerializable|  
|[CA2237](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md)|Marcar tipos ISerializable com SerializableAttribute|  
|[CA2238](../code-quality/ca2238-implement-serialization-methods-correctly.md)|Implementar métodos de serialização corretamente|  
|[CA2240](../code-quality/ca2240-implement-iserializable-correctly.md)|Implementar ISerializable corretamente|  
|[CA2241](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md)|Fornecer argumentos corretos para métodos de formatação|  
|[CA2242](../code-quality/ca2242-test-for-nan-correctly.md)|Testar para NaN corretamente|  
|[CA1008](../code-quality/ca1008-enums-should-have-zero-value.md)|Enums devem ter valor zero|  
|[CA1013](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|Sobrecarregar operador equals ao sobrecarregar adicionar e subtrair|  
|[CA1303](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md)|Não passar literais como parâmetros localizados|  
|[CA1308](../code-quality/ca1308-normalize-strings-to-uppercase.md)|Normalizar cadeias de caracteres em maiusculas|  
|[CA1806](../code-quality/ca1806-do-not-ignore-method-results.md)|Não ignore resultados do método|  
|[CA1816](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)|Chame GC. SuppressFinalize corretamente|  
|[CA1819](../code-quality/ca1819-properties-should-not-return-arrays.md)|Propriedades não devem retornar matrizes|  
|[CA1820](../code-quality/ca1820-test-for-empty-strings-using-string-length.md)|Teste para cadeias de caracteres vazias usando o comprimento da cadeia de caracteres|  
|[CA1903](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|Usar apenas a API da estrutura de destino|  
|[CA2004](../code-quality/ca2004-remove-calls-to-gc-keepalive.md)|Remova chamadas para GC. KeepAlive|  
|[CA2006](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md)|Use SafeHandle para encapsular recursos nativos|  
|[CA2102](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md)|Capturar exceções não CLSCompliant em manipuladores gerais|  
|[CA2104](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)|Não declarar tipos de referência mutáveis somente leitura|  
|[CA2105](../code-quality/ca2105-array-fields-should-not-be-read-only.md)|Campos de matriz não devem ser somente leitura|  
|[CA2106](../code-quality/ca2106-secure-asserts.md)|Declarações seguras|  
|[CA2115](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)|Chame GC. KeepAlive ao usar recursos nativos|  
|[CA2119](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md)|Métodos para lacrar que atendam a interfaces privadas|  
|[CA2120](../code-quality/ca2120-secure-serialization-constructors.md)|Construtores de serialização segura|  
|[CA2121 OS](../code-quality/ca2121-static-constructors-should-be-private.md)|Construtores estáticos devem ser privados|  
|[CA2130 AS](../code-quality/ca2130-security-critical-constants-should-be-transparent.md)|Constantes críticas de segurança devem ser transparentes|  
|[CA2205](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|Usar equivalentes gerenciados da API do Win32|  
|[CA2215](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md)|Métodos Dispose devem chamar o descarte da classe base|  
|[CA2221](../code-quality/ca2221-finalizers-should-be-protected.md)|Os finalizadores devem ser protegidos|  
|[CA2222](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|Não diminuir a visibilidade de membro herdada|  
|[CA2223](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|Os membros devem ser diferentes por tipo de retorno|  
|[CA2224](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|Substituir equals ao sobrecarregar operador equals|  
|[CA2226](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|Os operadores devem ter sobrecargas simétricas|  
|[CA2227](../code-quality/ca2227-collection-properties-should-be-read-only.md)|Propriedades de coleção devem ser somente leitura|  
|[CA2239](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|Fornecer métodos de desserialização para campos opcionais|  
|[CA1032](../code-quality/ca1032-implement-standard-exception-constructors.md)|Implementar construtores de exceção padrão|  
|[CA1054](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|Parâmetros de URI não devem ser cadeias de caracteres|  
|[CA1055](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|Valores não devem ser cadeias de caracteres de retorno de URI|  
|[CA1056](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|Propriedades URI não devem ser cadeias de caracteres|  
|[CA1057 AS](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|Cadeia de caracteres chamam sobrecargas System. URI|  
|[CA1402](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md)|Evitar sobrecargas em interfaces visíveis COM|  
|[CA1406](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md)|Evitar argumentos Int64 para clientes Visual Basic 6|  
|[CA1407](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)|Evitar membros estáticos em tipos visíveis COM|  
|[CA1408](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)|Não usar AutoDual ClassInterfaceType|  
|[CA1409](../code-quality/ca1409-com-visible-types-should-be-creatable.md)|Tipos visíveis com devem ser criáveis|  
|[CA1411](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)|OS métodos de registro não devem ser visíveis|  
|[CA1412](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)|Marcar Interfaces ComSource como IDispatch|  
|[CA1413](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)|Evitar campos não públicos em tipos de valor visíveis COM|  
|[CA1414](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md)|Marcar argumentos P/Invoke boolianos com MarshalAs|  
|[CA1600](../code-quality/ca1600-do-not-use-idle-process-priority.md)|Não use prioridade de processo ociosa|  
|[CA1601](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md)|Não usar temporizadores que impeçam alterações no estado de energia|  
|[CA1824](../code-quality/ca1824-mark-assemblies-with-neutralresourceslanguageattribute.md)|Marcar assemblies com NeutralResourcesLanguageAttribute|  
|[CA2001](../code-quality/ca2001-avoid-calling-problematic-methods.md)|Evite chamar métodos problemáticos|  
|[CA2003](../code-quality/ca2003-do-not-treat-fibers-as-threads.md)|Não trate fibras como threads|  
|[CA2135 OS](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md)|Assemblies de nível 2 não devem conter LinkDemands|  
|[CA2136](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md)|Os membros não devem ter anotações de transparência conflitantes|  
|[CA2139](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md)|Métodos transparentes talvez não usem o atributo HandleProcessCorruptingExceptions|  
|[CA2142](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)|O código transparente não deve ser protegido com LinkDemands|  
|[CA2143](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md)|Métodos transparentes não devem usar demandas de segurança|  
|[CA2144](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md)|O código transparente não deve carregar assemblies de matrizes de bytes|  
|[CA2145](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md)|Métodos transparentes não devem ser decorados com o SuppressUnmanagedCodeSecurityAttribute|  
|[CA2204](../code-quality/ca2204-literals-should-be-spelled-correctly.md)|Literais devem ter grafia correta|  
|[CA2211](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md)|Campos não constantes não devem ser visíveis|  
|[CA2217](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)|Não marcar enums com FlagsAttribute|  
|[CA2218](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)|Substituir GetHashCode em igualdades de substituição|  
|[CA2219](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)|Não gerar exceções em cláusulas de exceção|  
|[CA2225 AS](../code-quality/ca2225-operator-overloads-have-named-alternates.md)|Sobrecargas de operador possuem alternativas nomeadas|  
|[CA2228](../code-quality/ca2228-do-not-ship-unreleased-resource-formats.md)|Não remeter formatos de recurso não lançados|  
|[CA2230](../code-quality/ca2230-use-params-for-variable-arguments.md)|Usar parâmetros para argumentos de variável|  
|[CA2233](../code-quality/ca2233-operations-should-not-overflow.md)|Operações não devem estourar|  
|[CA2234](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)|Passar objetos System. URI em vez de cadeias de caracteres|  
|[CA2243](../code-quality/ca2243-attribute-string-literals-should-parse-correctly.md)|Literais de cadeia de caracteres de atributo devem ser analisados corretamente|



