---
title: Conjunto de regras básicas de regras de diretrizes de Design para código gerenciado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7eb384f5-f961-400b-b151-115d92addc6a
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: ed0728eb0daa5c1ff0f322db42f66373181f3e23
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49184711"
---
# <a name="basic-design-guideline-rules-rule-set-for-managed-code"></a>Conjunto de regras de diretriz do design básico para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar as regras de diretrizes de Design básico do Microsoft conjunto de regras para se concentrar em como tornar seu código mais fácil de entender e usar. Você deve incluir essa regra definida se seu projeto incluir código de biblioteca ou se você quiser impor práticas recomendadas para o código que é fácil de manter.  
  
 As regras básicas de diretrizes de Design incluem todas as regras no conjunto de regras de regras de recomendável mínimo da Microsoft. Para obter uma lista das regras de mínima, consulte [gerenciados recomendado conjunto de regras para código gerenciado](../code-quality/managed-recommended-rules-rule-set-for-managed-code.md).  
  
 A tabela a seguir descreve todas as regras no conjunto de regras de regras de diretrizes de Design básico do Microsoft.  
  
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
|[CA1000](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)|Não declarar membros estáticos em tipos genéricos|  
|[CA1002](../code-quality/ca1002-do-not-expose-generic-lists.md)|Não expor listas genéricas|  
|[CA1003](../code-quality/ca1003-use-generic-event-handler-instances.md)|Usar instâncias do manipulador de eventos genéricos|  
|[CA1004](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)|Métodos genéricos devem fornecer o parâmetro de tipo|  
|[CA1005](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)|Evitar parâmetros excessivos em tipos genéricos|  
|[CA1006](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)|Não aninhar tipos genéricos em assinaturas de membro|  
|[CA1007](../code-quality/ca1007-use-generics-where-appropriate.md)|Usar genéricos quando apropriado|  
|[CA1008](../code-quality/ca1008-enums-should-have-zero-value.md)|Enums devem ter valor zero|  
|[CA1010](../code-quality/ca1010-collections-should-implement-generic-interface.md)|As coleções devem implementar a interface genérica|  
|[CA1011](../code-quality/ca1011-consider-passing-base-types-as-parameters.md)|Considerar passar tipos base como parâmetros|  
|[CA1012](../code-quality/ca1012-abstract-types-should-not-have-constructors.md)|Tipos abstratos não devem ter construtores|  
|[CA1013](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md)|Sobrecarregar operador equals ao sobrecarregar adicionar e subtrair|  
|[CA1014](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md)|Marcar assemblies com CLSCompliantAttribute|  
|[CA1017](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)|Marcar assemblies com ComVisibleAttribute|  
|[CA1018](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md)|Marcar atributos com AttributeUsageAttribute|  
|[CA1019](../code-quality/ca1019-define-accessors-for-attribute-arguments.md)|Definir acessadores para argumentos de atributo|  
|[CA1023](../code-quality/ca1023-indexers-should-not-be-multidimensional.md)|Indexadores não devem ser multidimensionais|  
|[CA1024](../code-quality/ca1024-use-properties-where-appropriate.md)|Usar propriedades quando apropriado|  
|[CA1025](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)|Substituir argumentos repetitivos por matriz de parâmetros|  
|[CA1026](../code-quality/ca1026-default-parameters-should-not-be-used.md)|Parâmetros padrão não devem ser usados|  
|[CA1027](../code-quality/ca1027-mark-enums-with-flagsattribute.md)|Marcar enums com FlagsAttribute|  
|[CA1028](../code-quality/ca1028-enum-storage-should-be-int32.md)|Armazenamento de enum deve ser Int32|  
|[CA1030](../code-quality/ca1030-use-events-where-appropriate.md)|Usar eventos quando apropriado|  
|[CA1031](../code-quality/ca1031-do-not-catch-general-exception-types.md)|Não capturar tipos de exceção geral|  
|[CA1032](../code-quality/ca1032-implement-standard-exception-constructors.md)|Implementar construtores de exceção padrão|  
|[CA1034](../code-quality/ca1034-nested-types-should-not-be-visible.md)|Tipos aninhados não devem ser visíveis|  
|[CA1035](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md)|As implementações de ICollection têm membros fortemente tipados|  
|[CA1036](../code-quality/ca1036-override-methods-on-comparable-types.md)|Substituir métodos em tipos comparáveis|  
|[CA1038](../code-quality/ca1038-enumerators-should-be-strongly-typed.md)|Enumeradores devem ser fortemente tipados|  
|[CA1039](../code-quality/ca1039-lists-are-strongly-typed.md)|Listas são fortemente tipadas|  
|[CA1041](../code-quality/ca1041-provide-obsoleteattribute-message.md)|Fornecer mensagem ObsoleteAttribute|  
|[CA1043](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md)|Usar argumento integral ou de cadeia de caracteres para indexadores|  
|[CA1044](../code-quality/ca1044-properties-should-not-be-write-only.md)|Propriedades não devem ser somente gravação|  
|[CA1046](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)|Não sobrecarregar operador equals em tipos de referência|  
|[CA1047](../code-quality/ca1047-do-not-declare-protected-members-in-sealed-types.md)|Não declarar membros protegidos em tipos lacrados|  
|[CA1048](../code-quality/ca1048-do-not-declare-virtual-members-in-sealed-types.md)|Não declarar membros virtuais em tipos lacrados|  
|[CA1050](../code-quality/ca1050-declare-types-in-namespaces.md)|Declarar tipos em namespaces|  
|[CA1051](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)|Não declarar campos de instância visíveis|  
|[CA1052](../code-quality/ca1052-static-holder-types-should-be-sealed.md)|Tipos de suporte estático devem ser lacrados|  
|[CA1053](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md)|Tipos de espaços reservados estáticos não devem ter construtores|  
|[CA1054](../code-quality/ca1054-uri-parameters-should-not-be-strings.md)|Parâmetros de URI não devem ser cadeias de caracteres|  
|[CA1055](../code-quality/ca1055-uri-return-values-should-not-be-strings.md)|Valores não devem ser cadeias de caracteres de retorno de URI|  
|[CA1056](../code-quality/ca1056-uri-properties-should-not-be-strings.md)|Propriedades URI não devem ser cadeias de caracteres|  
|[CA1057 AS](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md)|Cadeia de caracteres chamam sobrecargas System. URI|  
|[CA1058](../code-quality/ca1058-types-should-not-extend-certain-base-types.md)|Tipos não devem estender determinados tipos base|  
|[CA1059](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)|Os membros não devem expor certos tipos concretos|  
|[CA1064](../code-quality/ca1064-exceptions-should-be-public.md)|As exceções devem ser públicas|  
|[CA1500](../code-quality/ca1500-variable-names-should-not-match-field-names.md)|Nomes de variáveis não devem corresponder aos nomes de campo|  
|[CA1502](../code-quality/ca1502-avoid-excessive-complexity.md)|Evitar complexidade excessiva|  
|[CA1708](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)|Identificadores devem ser diferentes de maiusculas e minúsculas|  
|[CA1716](../code-quality/ca1716-identifiers-should-not-match-keywords.md)|Identificadores não devem corresponder a palavras-chave|  
|[CA1801](../code-quality/ca1801-review-unused-parameters.md)|Revisar parâmetros não utilizados|  
|[CA1804](../code-quality/ca1804-remove-unused-locals.md)|Remover locais não usados|  
|[CA1809](../code-quality/ca1809-avoid-excessive-locals.md)|Evitar locais excessivos|  
|[CA1810](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md)|Inicializar campos estáticos de tipo de referência embutido|  
|[CA1811](../code-quality/ca1811-avoid-uncalled-private-code.md)|Evitar código privado não chamado|  
|[CA1812](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)|Evite classes internas sem instâncias|  
|[CA1813](../code-quality/ca1813-avoid-unsealed-attributes.md)|Evitar atributos não lacrados|  
|[CA1814](../code-quality/ca1814-prefer-jagged-arrays-over-multidimensional.md)|Prefira matrizes denteadas multidimensional|  
|[CA1815](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md)|Substituir equals e operador equals em tipos de valor|  
|[CA1819](../code-quality/ca1819-properties-should-not-return-arrays.md)|Propriedades não devem retornar matrizes|  
|[CA1820](../code-quality/ca1820-test-for-empty-strings-using-string-length.md)|Teste para cadeias de caracteres vazias usando o comprimento da cadeia de caracteres|  
|[CA1822](../code-quality/ca1822-mark-members-as-static.md)|Marque membros como estáticos|  
|[CA1823](../code-quality/ca1823-avoid-unused-private-fields.md)|Evitar campos privados não usados|  
|[CA2201](../code-quality/ca2201-do-not-raise-reserved-exception-types.md)|Não acionar tipos de exceção reservados|  
|[CA2205](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md)|Usar equivalentes gerenciados da API do Win32|  
|[CA2208](../code-quality/ca2208-instantiate-argument-exceptions-correctly.md)|Instanciar exceções de argumento corretamente|  
|[CA2211](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md)|Campos não constantes não devem ser visíveis|  
|[CA2217](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)|Não marcar enums com FlagsAttribute|  
|[CA2219](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)|Não gerar exceções em cláusulas de exceção|  
|[CA2221](../code-quality/ca2221-finalizers-should-be-protected.md)|Os finalizadores devem ser protegidos|  
|[CA2222](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md)|Não diminuir a visibilidade de membro herdada|  
|[CA2223](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md)|Os membros devem ser diferentes por tipo de retorno|  
|[CA2224](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)|Substituir equals ao sobrecarregar operador equals|  
|[CA2225 AS](../code-quality/ca2225-operator-overloads-have-named-alternates.md)|Sobrecargas de operador possuem alternativas nomeadas|  
|[CA2226](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md)|Os operadores devem ter sobrecargas simétricas|  
|[CA2227](../code-quality/ca2227-collection-properties-should-be-read-only.md)|Propriedades de coleção devem ser somente leitura|  
|[CA2230](../code-quality/ca2230-use-params-for-variable-arguments.md)|Usar parâmetros para argumentos de variável|  
|[CA2234](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md)|Passar objetos System. URI em vez de cadeias de caracteres|  
|[CA2239](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md)|Fornecer métodos de desserialização para campos opcionais|



