---
title: Avisos da análise de código para código gerenciado por CheckId
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1000
- CA1001
- CA1002
- CA1003
- CA1004
- CA1005
- CA1006
- CA1007
- CA1008
- CA1009
- CA1010
- CA1011
- CA1012
- CS1013
- CS1014
- CA1016
- CA1017
- CA1018
- CA1019
- CA1020
- CA1021
- CA1022
- CA1023
- CA1024
- CS1025
- CA1026
- CA1027
- CA1028
- CA1029
- CA1030
- CA1031
- CA1032
- CA1033
- CA1034
- CA1035
- CA1036
- CA1037
- CA1038
- CA1039
- CA1040
- CA1041
- CA1042
- CA1043
- CA1044
- CA1045
- CA1046
- CA1047
- CA1048
- CA1049
- CA1050
- CA1051
- CA1052
- CA1053
- CA1054
- CA1055
- CA1056
- CA1057
- CA1058
- CA1059
- CA1060
- CA1061
- CA1062
- CA1063
- CA1064
- CA1065
- CA1300
- CA1301
- CA1302
- CA1303
- CA1304
- CA1305
- CA1306
- CA1307
- CA1308
- CA1309
- CA1400
- CA1401
- CA1402
- CA1403
- CA1404
- CA1405
- CA1406
- CA1407
- CA1408
- CA1409
- CA1410
- CA1411
- CA1412
- CA1413
- CA1414
- CA1415
- CA1500
- CA1501
- CA1502
- CA1503
- CA1504
- CA1505
- CA1506
- CA1600
- CA1601
- CA1700
- CA1701
- CA1702
- CA1703
- CA1704
- CA1707
- CA1708
- CA1709
- CA1710
- CA1711
- CA1712
- CA1713
- CA1714
- CA1715
- VA1716
- CA1717
- CA1719
- CA1720
- CA1721
- CA1722
- CA1723
- CA1724
- CA1725
- CA1726
- CA1727
- CA1728
- CA1729
- CA1730
- CA1800
- CA1801
- CA1802
- CA1803
- CA1804
- CA1806
- CA1809
- CA1810
- CA1811
- CA1812
- CA1813
- CA1814
- CA1815
- CA1816
- CA1819
- CA1820
- CA1821
- CA1822
- CA1823
- CA1824
- CA1900
- CA1901
- CA1903
- CA2000
- CA2001
- CA2002
- CA2003
- CA2004
- CA2006
- CA2100
- CA2101
- CA2102
- CA2103
- CA2104
- CA2105
- CA2106
- CA2107
- CA2108
- CA2109
- CA2110
- CA2111
- CA2112
- CA2114
- CA2115
- CA2116
- CA2117
- CA2118
- CA2119
- CA2120
- CA2121
- CA2122
- CA2123
- CA2124
- CA2126
- CA2127
- CA2128
- CA2129
- CA2130
- CA2131
- CA2132
- CA2133
- CA2134
- CA2135
- CA2136
- CA2137
- CA2138
- CA2139
- CA2140
- CA2141
- CA2142
- CA2143
- CA2144
- CA2145
- CA2146
- CA2147
- CA2148
- CA2149
- CA2150
- CA2151
- CA2200
- CA2201
- CA2202
- CA2204
- CA2205
- CA2207
- CA2208
- CA2210
- CA2211
- CA2212
- CA2213
- CA2214
- CA2215
- CA2216
- CA2217
- CA2218
- CA2219
- CA2220
- CA2221
- CA2222
- CA2223
- CA2224
- CA2225
- CA2226
- CA2228
- CA2229
- CA2227
- CA2230
- CA2231
- CA2232
- CA2233
- CA2234
- CA2235
- CA2236
- CA2237
- CA2238
- CA2239
- CA2240
- CA2241
- CA2242
- CA2243
- CA5122
ms.assetid: 5cb221f6-dc59-4abf-9bfa-adbd6f907f96
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 87fc6bdda65bf06b344a0971fb255555914e3102
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53053030"
---
# <a name="code-analysis-warnings-for-managed-code-by-checkid"></a>Avisos da análise de código para código gerenciado por CheckId

A tabela a seguir lista avisos de análise de código para código gerenciado pelo identificador CheckId do aviso.

| CheckId | Aviso | Descrição |
|---------| - | - |
| CA1000 | [CA1000: não declarar membros estáticos em tipos genéricos](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md) | Quando um membro estático de um tipo genérico é chamado, o argumento de tipo deve ser especificado para o tipo. Quando um membro de instância genérico que não dá suporte à inferência é chamado, o argumento de tipo deve ser especificado para o membro. Nesses dois casos, a sintaxe para especificar o argumento de tipo é diferente e facilmente confundida. |
| CA1001 | [CA1001: tipos que têm campos descartáveis devem ser descartáveis](../code-quality/ca1001-types-that-own-disposable-fields-should-be-disposable.md) | Uma classe declara e implementa um campo de instância que é um tipo System.IDisposable, e a classe não implementa IDisposable. Uma classe que declara um campo IDisposable indiretamente possui um recurso não gerenciado e deve implementar a interface IDisposable. |
| CA1002 | [CA1002: não expor listas genéricas](../code-quality/ca1002-do-not-expose-generic-lists.md) | Generic < (de \<(T >) >) é uma coleção genérica que foi projetada para desempenho, não a herança. Por isso, List não contém membros virtuais. As coleções genéricas projetadas para herança devem ser expostas em seu lugar. |
| CA1003 | [CA1003: usar instâncias do manipulador de eventos genéricos](../code-quality/ca1003-use-generic-event-handler-instances.md) |Um tipo contém um delegado que retorna void, cuja assinatura contém dois parâmetros (o primeiro um objeto e o segundo um tipo atribuível a EventArgs), e o assembly que contém tem como alvo o Microsoft .NET Framework 2.0. |
| CA1004 | [CA1004: os métodos genéricos devem fornecer o parâmetro de tipo](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md) | Inferência é como o argumento de tipo de um método genérico é determinado pelo tipo de argumento passado para o método, em vez da especificação explícita do argumento de tipo. Para habilitar a inferência, a assinatura do parâmetro de um método genérico deve incluir um parâmetro que seja do mesmo tipo do parâmetro de tipo para o método. Nesse caso, o argumento de tipo não precisa ser especificado. Durante o uso da inferência para todos os parâmetros de tipo, a sintaxe para chamar métodos de instância genéricos e não genéricos é idêntica; isso simplifica a usabilidade de métodos genéricos. |
| CA1005 | [CA1005: evitar parâmetros excessivos em tipos genéricos](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md) | Quanto mais parâmetros de tipo um tipo genérico contiver, mais difícil será saber e lembrar-se do que cada parâmetro de tipo representa. É normalmente óbvio com um parâmetro de tipo, como na lista\<T > e, em certos casos que têm dois parâmetros de tipo, como em Dictionary\<TKey, TValue >. No entanto, se houver mais de dois parâmetros de tipo, a dificuldade ficará muito grande para a maioria dos usuários. |
| CA1006 | [CA1006: não aninhar tipos genéricos em assinaturas de membro](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md) | Um argumento de tipo aninhado é um argumento de tipo que também é um tipo genérico. Para chamar um membro cuja assinatura contenha um argumento de tipo aninhado, o usuário deve criar uma instância de um tipo genérico e passar esse tipo para o construtor de um segundo tipo genérico. O procedimento e a sintaxe obrigatórios são complexos e devem ser evitados. |
| CA1007 |[CA1007: usar genéricos quando apropriado](../code-quality/ca1007-use-generics-where-appropriate.md) | Um método visível externamente contém um parâmetro de referência do tipo System.Object. O uso de um método genérico permite que todos os tipos, sujeitos a restrições, sejam passados para o método sem primeiramente converter o tipo no tipo de parâmetro de referência. |
| CA1008 | [CA1008: as enums devem ter valor zero](../code-quality/ca1008-enums-should-have-zero-value.md) | O valor padrão de uma enumeração não inicializada, assim como o de outros tipos de valor, é zero. Uma enumeração atribuída por nonflags deve definir um membro usando o valor de zero de forma que o valor padrão seja um valor válido da enumeração. Se uma enumeração que tem o atributo FlagsAttribute aplicado definir um membro com valor, seu nome deverá ser “None” para indicar que nenhum valor foi definido na enumeração. |
| CA1009 | [CA1009: declarar manipuladores de eventos corretamente](../code-quality/ca1009-declare-event-handlers-correctly.md) | Os métodos de manipulador de eventos utilizam dois parâmetros. O primeiro é do tipo System.Object e é chamado de "sender". Este é o objeto que acionou o evento. O segundo parâmetro é do tipo System.EventArgs e é chamado de "e". Esses são os dados associados ao evento. Os métodos do manipulador de eventos não devem retornar um valor; na linguagem de programação C#, isso é indicado pelo tipo de retorno nulo. |
| CA1010 | [CA1010: as coleções devem implementar a interface genérica](../code-quality/ca1010-collections-should-implement-generic-interface.md) | Para ampliar a usabilidade de uma coleção, implemente uma das interfaces da coleção genéricas. Em seguida, a coleção pode ser usada para popular tipos de coleção genéricos. |
| CA1011 |[CA1011: considere passar os tipos base como parâmetros](../code-quality/ca1011-consider-passing-base-types-as-parameters.md) | Quando um tipo de base é especificado como um parâmetro em uma declaração de método, qualquer tipo derivado do tipo de base pode ser passado como o argumento correspondente ao método. Se a funcionalidade adicional fornecida pelo tipo de parâmetro derivado não for necessária, o uso do tipo de base permitirá um uso mais amplo do método. |
| CA1012 | [CA1012: tipos abstratos não devem ter construtores](../code-quality/ca1012-abstract-types-should-not-have-constructors.md) | Construtores em tipos abstratos só podem ser chamados por tipos derivados. Como construtores públicos criam instâncias de um tipo e não é possível criar instâncias de um tipo abstrato, um tipo abstrato com um construtor público é projetado incorretamente. |
| CA1013 | [CA1013: sobrecarregar operador Equals ao sobrecarregar adicionar e subtrair](../code-quality/ca1013-overload-operator-equals-on-overloading-add-and-subtract.md) | Um tipo público ou protegido implementa os operadores de adição ou subtração sem implementar o operador de igualdade. |
| CA1014 | [CA1014: marcar assemblies com CLSCompliantAttribute](../code-quality/ca1014-mark-assemblies-with-clscompliantattribute.md) | A CLS (Common Language Specification) define restrições de nomenclatura, tipos de dados e regras que assemblies deverão respeitar se forem usados em todas as linguagens de programação. Um bom design determina que todos os assemblies indiquem explicitamente a conformidade com CLS usando-se <xref:System.CLSCompliantAttribute>. Se esse atributo não estiver presente em um assembly, o assembly não será compatível. |
| CA1016 | [CA1016: marcar assemblies com AssemblyVersionAttribute](../code-quality/ca1016-mark-assemblies-with-assemblyversionattribute.md) | O .NET Framework usa o número de versão para identificar exclusivamente um assembly e associar a tipos em assemblies fortemente nomeados. O número de versão é usado com a versão e a política do publicador. Por padrão, os aplicativos só são executados com a versão do assembly com que foram criados. |
| CA1017 | [CA1017: marcar assemblies com ComVisibleAttribute](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md) |ComVisibleAttribute determina como clientes COM acessam código gerenciado. Um bom design determina que os assemblies indiquem explicitamente a visibilidade de COM. A visibilidade de COM pode ser definida para todo o assembly e, em seguida, substituída por tipos individuais e membros de tipo. Caso esse atributo não esteja presente, o conteúdo do assembly permanece visível aos clientes COM. |
| CA1018 | [CA1018: marcar atributos com AttributeUsageAttribute](../code-quality/ca1018-mark-attributes-with-attributeusageattribute.md) | Ao definir um atributo personalizado, você o marca usando AttributeUsageAttribute para indicar onde o atributo personalizado pode ser aplicado no código-fonte. O significado e o uso desejado de um atributo determinarão seus locais válidos no código. |
| CA1019 | [CA1019: definir acessadores para argumentos de atributo](../code-quality/ca1019-define-accessors-for-attribute-arguments.md) | Os atributos podem definir argumentos obrigatórios que devem ser especificados quando você aplica o atributo a um destino. Eles também são conhecidos como argumentos posicionais porque são fornecidos a construtores de atributos como parâmetros posicionais. Para cada argumento obrigatório, o atributo também deve fornecer uma propriedade somente leitura correspondente de forma que o valor do argumento possa ser recuperado no tempo de execução. Os atributos também podem definir argumentos opcionais, que também são conhecidos como argumentos nomeados. Esses argumentos são fornecidos a construtores de atributo por nome e devem ter uma propriedade de leitura/gravação correspondente. |
| CA1020 | [CA1020: evitar namespaces com poucos tipos](../code-quality/ca1020-avoid-namespaces-with-few-types.md) | Verifique se cada um dos namespaces tem uma organização lógica e se há um motivo válido para colocar tipos em um namespace populado de maneira esparsa. |
| CA1021 | [CA1021: evitar parâmetros de saída](../code-quality/ca1021-avoid-out-parameters.md) | A passagem de tipos por referência (usando out ou ref) requer experiência com ponteiros, compreensão das diferenças entre tipos de valor e tipos de referência e os métodos de tratamento com vários valores de retorno. Além disso, a diferença entre parâmetros out e ref não é amplamente compreendida. |
| CA1023 | [CA1023: os indexadores não devem ser multidimensionais](../code-quality/ca1023-indexers-should-not-be-multidimensional.md) | Os indicadores (ou seja, propriedades indexadas) devem usar um único índice. Os indicadores multidimensionais podem reduzir significativamente a usabilidade da biblioteca. |
| CA1024 | [CA1024: usar propriedades quando apropriado](../code-quality/ca1024-use-properties-where-appropriate.md) | Um método público ou protegido tem um nome que começa com "Get", não utiliza parâmetros e retorna um valor que não é uma matriz. O método pode ser um bom candidato a se tornar uma propriedade. |
| CA1025 | [CA1025: substituir argumentos repetitivos por matriz de parâmetros](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md) | Use uma matriz de parâmetros, em vez de argumentos repetidos, quando o número exato de argumentos for desconhecido e quando os argumentos variáveis forem do mesmo tipo ou puderem ser passados como o mesmo tipo. |
| CA1026 | [CA1026: parâmetros padrão não devem ser usados](../code-quality/ca1026-default-parameters-should-not-be-used.md) | Métodos que usam parâmetros padrão são permitidos na CLS; no entanto, a CLS permite que os compiladores ignorem os valores que são atribuídos a esses parâmetros. Para manter o comportamento desejado em todas as linguagens de programação, os métodos que usam parâmetros padrão devem ser substituídos por sobrecargas de método que forneçam os parâmetros padrão. |
| CA1027 |[CA1027: marcar enums com FlagsAttribute](../code-quality/ca1027-mark-enums-with-flagsattribute.md) | Uma enumeração é um tipo de valor que define um conjunto de constantes nomeadas relacionadas. Aplique FlagsAttribute a uma enumeração quando suas constantes nomeadas puderem ser combinadas de maneira significativa. |
| CA1028 | [CA1028: o armazenamento de enum deve ser Int32](../code-quality/ca1028-enum-storage-should-be-int32.md) | Uma enumeração é um tipo de valor que define um conjunto de constantes nomeadas relacionadas. Por padrão, o tipo de dados System.Int32 é usado para armazenar o valor constante. Embora seja possível alterar esse tipo subjacente, isso não é necessário ou recomendado na maioria dos cenários. |
| CA1030 | [CA1030: usar eventos quando apropriado](../code-quality/ca1030-use-events-where-appropriate.md) |Essa regra detecta métodos que têm nomes que seriam usados normalmente em eventos. Se um método for chamado em resposta a uma alteração de estado claramente definida, o método deverá ser invocado por um manipulador de eventos. Os objetos que chamam o método devem acionar eventos, em vez de chamar o método diretamente. |
| CA1031 | [CA1031: não capturar tipos de exceção gerais](../code-quality/ca1031-do-not-catch-general-exception-types.md) | As exceções gerais não devem ser capturadas. Capture uma exceção mais específica ou relance a exceção geral como a última instrução no bloco de captura. |
| CA1032 |[CA1032: implementar construtores de exceção padrão](../code-quality/ca1032-implement-standard-exception-constructors.md) | Deixar de fornecer o conjunto completo de construtores pode dificultar o tratamento correto das exceções. |
| CA1033 | [CA1033: os métodos de interface devem ser chamáveis por tipos filho](../code-quality/ca1033-interface-methods-should-be-callable-by-child-types.md) | Um tipo visível externamente sem lacre fornece uma implementação de método explícita de uma interface pública e não fornece um método visível externamente alternativo com o mesmo nome. |
| CA1034 | [CA1034: os tipos aninhados não devem ser visíveis](../code-quality/ca1034-nested-types-should-not-be-visible.md) | Um tipo aninhado é um tipo declarado no escopo de outro tipo. Os tipos aninhados são úteis para encapsular detalhes de implementação privados do tipo de contenção. Usados para essa finalidade, os tipos aninhados não devem ser visíveis externamente. |
| CA1035 | [CA1035: as implementações de ICollection têm membros fortemente tipados](../code-quality/ca1035-icollection-implementations-have-strongly-typed-members.md) | Essa regra exige que implementações de ICollection forneçam membros fortemente tipados de forma que usuários não sejam obrigados a converter argumentos no tipo Object quando usarem a funcionalidade fornecida pela interface. Essa regra pressupõe que o tipo que implementa ICollection faça isso para gerenciar uma coleção de instâncias de um tipo mais forte que Object. |
| CA1036 | [CA1036: substituir métodos em tipos comparáveis](../code-quality/ca1036-override-methods-on-comparable-types.md) |Um público ou um tipo protegido implementa a interface System.IComparable. Ele não substitui Object.Equals nem sobrecarrega o operador específico da linguagem para igualdade, desigualdade, menor que ou maior que. |
| CA1038 | [CA1038: os enumeradores devem ser fortemente tipados](../code-quality/ca1038-enumerators-should-be-strongly-typed.md) | Essa regra exige que implementações de IEnumerator também forneçam uma versão fortemente tipada da propriedade Current de forma que usuários não sejam obrigados a converter o valor de retorno no tipo forte quando usarem a funcionalidade fornecida pela interface. |
| CA1039 | [CA1039: as listas são fortemente tipadas](../code-quality/ca1039-lists-are-strongly-typed.md) | Essa regra exige que implementações de IList forneçam membros fortemente tipados de forma que usuários não sejam obrigados a converter argumentos no tipo System.Object quando usarem a funcionalidade fornecida pela interface. |
| CA1040 |[CA1040: evitar interfaces vazias](../code-quality/ca1040-avoid-empty-interfaces.md) | As interfaces definem os membros que fornecem um contrato de comportamento ou de uso. A funcionalidade descrita pela interface pode ser adotada por qualquer tipo, independentemente de onde o tipo seja exibido na hierarquia de herança. Um tipo implementa uma interface fornecendo implementações para os membros da interface. Uma interface vazia não define membros; por isso, ela não define um contrato que pode ser implementado. |
| CA1041 | [CA1041: fornecer mensagem ObsoleteAttribute](../code-quality/ca1041-provide-obsoleteattribute-message.md) | Um tipo ou um membro é marcado usando-se um atributo System.ObsoleteAttribute que não tem sua propriedade ObsoleteAttribute.Message especificada. Quando um tipo ou um membro marcado usando-se ObsoleteAttribute é compilado, a propriedade Message do atributo é exibida. Isso dá ao usuário informações sobre o tipo ou o membro obsoleto. |
| CA1043 | [CA1043: usar argumento integral ou de cadeia de caracteres para indexadores](../code-quality/ca1043-use-integral-or-string-argument-for-indexers.md) | Os indicadores (ou seja, propriedades indexadas) devem usar tipos integrais ou de cadeia de caracteres no índice. Esses tipos normalmente são usados na indexação de estruturas de dados e aumentam a usabilidade da biblioteca. O uso do tipo Object deve ser restrito a esses casos em que o tipo integral ou de cadeia de caracteres específico não pode ser especificado no tempo de design. |
| CA1044 | [CA1044: as propriedades não devem ser somente leitura](../code-quality/ca1044-properties-should-not-be-write-only.md) | Embora seja aceitável e normalmente necessário ter uma propriedade somente leitura, as diretrizes de design proíbem o uso de propriedades somente gravação. Isso é porque a permissão para que um usuário defina um valor e o impedimento posterior para ele exiba esse valor não dão nenhuma segurança. Além disso, sem acesso de leitura, o estado de objetos compartilhados não pode ser exibido, o que limita sua utilidade. |
| CA1045 |[CA1045: não passar tipos por referência](../code-quality/ca1045-do-not-pass-types-by-reference.md) | A passagem de tipos por referência (usando out ou ref) requer experiência com ponteiros, compreensão das diferenças entre tipos de valor e tipos de referência e os métodos de tratamento que têm vários valores de retorno. Os arquitetos de bibliotecas que projetam para um público em geral não devem esperar que os usuários dominem o trabalho com parâmetros out ou ref. |
| CA1046 | [CA1046: não sobrecarregar operador Equals em tipos de referência](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md) | Para tipos de referência, a implementação padrão do operador de igualdade está quase sempre correta. Por padrão, duas referências só serão iguais se apontarem para o mesmo objeto. |
| CA1047 |[CA1047: não declarar membros protegidos em tipos lacrados](../code-quality/ca1047-do-not-declare-protected-members-in-sealed-types.md) | Os tipos declaram membros protegidos de forma que a herança de tipos possa acessar ou substituir o membro. Por definição, os tipos vedados não podem ser lacrados, o que significa que os métodos protegidos em tipos lacrados não podem ser chamados. |
| CA1048 | [CA1048: não declarar membros virtuais em tipos lacrados](../code-quality/ca1048-do-not-declare-virtual-members-in-sealed-types.md) | Os tipos declaram métodos como virtuais de forma que a herança de tipos possa substituir a implementação do método virtual. Por definição, um tipo lacrado não pode ser herdado. Isso torna um método virtual em um tipo lacrado sem sentido. |
| CA1049 | [CA1049: tipos que tenham recursos nativos devem ser descartáveis](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md) | Tipos que alocam recursos não gerenciados devem implementar IDisposable para permitir que os chamadores liberem esses recursos sob demanda e reduzir o tempo de vida dos objetos que contêm os recursos. |
| CA1050 | [CA1050: declarar tipos em namespaces](../code-quality/ca1050-declare-types-in-namespaces.md) | Tipos são declarados em namespaces para evitar conflitos de nome e são uma maneira de organizar tipos relacionados em uma hierarquia de objetos. |
| CA1051 | [CA1051: não declarar campos de instância visíveis](../code-quality/ca1051-do-not-declare-visible-instance-fields.md) | O principal uso de um campo deve ser um como um detalhe da implementação. Os campos devem ser privados ou internos e devem ser expostos usando-se propriedades. |
| CA1052 | [CA1052: os tipos de suporte estático devem ser lacrados](../code-quality/ca1052-static-holder-types-should-be-sealed.md) | Um tipo público ou protegido contém apenas membros estáticos e não é declarado usando-se o modificador (Reference do C#) (NotInheritable). Um tipo que não é deve ser herdado deve ser marcado usando-se o modificador lacrado para evitar seu uso como um tipo de base. |
| CA1053 |[CA1053: os tipos de suporte estático não devem ter construtores](../code-quality/ca1053-static-holder-types-should-not-have-constructors.md) | Um tipo público ou público aninhado declara apenas membros estáticos e tem um construtor padrão público ou protegido. O construtor é desnecessário porque chamar membros estáticos não exige uma instância do tipo. A sobrecarga de cadeia de caracteres deve chamar a sobrecarga do URI (Uniform Resource Identifier) usando-se o argumento de cadeia de caracteres por questões de segurança. |
| CA1054 | [CA1054: os parâmetros de URI não devem ser cadeias de caracteres](../code-quality/ca1054-uri-parameters-should-not-be-strings.md) | Se um método utilizar uma representação de cadeia de caracteres de um URI, uma sobrecarga correspondente deverá ser fornecida utilizando uma instância da classe do URI, que oferece esses serviços de maneira segura e protegida. |
| CA1055 | [CA1055: os valores de retorno de URI não devem ser cadeias de caracteres](../code-quality/ca1055-uri-return-values-should-not-be-strings.md) | Esta regra pressupõe que o método retorne um URI. Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. A classe System.Uri fornece esses serviços de maneira segura. |
| CA1056 | [CA1056: as propriedades de URI não devem ser cadeias de caracteres](../code-quality/ca1056-uri-properties-should-not-be-strings.md) | Esta regra pressupõe que a propriedade represente o URI. Uma representação de cadeia de caracteres de um URI está propensa a erros de análise e de codificação, e pode resultar em vulnerabilidades de segurança. A classe System.Uri fornece esses serviços de maneira segura. |
| CA1057 | [CA1057: as sobrecargas de URI da cadeia de caracteres chamam sobrecargas System.Uri](../code-quality/ca1057-string-uri-overloads-call-system-uri-overloads.md) | Um tipo declara sobrecargas de método que diferem apenas pela substituição de um parâmetro de cadeia de caracteres com um parâmetro System.Uri. A sobrecarga que utiliza o parâmetro de cadeia de caracteres não chama a sobrecarga que utiliza o parâmetro do URI. |
| CA1058 | [CA1058: os tipos não devem estender determinados tipos base](../code-quality/ca1058-types-should-not-extend-certain-base-types.md) | Um tipo visível externamente estende determinados tipos de base. Use uma das alternativas. |
| CA1059 |[CA1059: os membros não devem expor determinados tipos concretos](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md) | Um tipo concreto é um tipo que tem uma implementação completa e, por isso, uma instância pode ser criada. Para permitir o uso difundido do membro, substitua o tipo concreto usando-se a interface sugerida. |
| CA1060 | [CA1060: mover P/Invokes para a classe NativeMethods](../code-quality/ca1060-move-p-invokes-to-nativemethods-class.md) | Métodos de invocação da plataforma, como os marcados usando-se o atributo System.Runtime.InteropServices.DllImportAttribute, ou métodos definidos usando-se a palavra-chave Declare em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)], acessam um código não gerenciado. Esses métodos devem ser da classe NativeMethods, SafeNativeMethods ou UnsafeNativeMethods. |
| CA1061 |[CA1061: não ocultar métodos de classe base](../code-quality/ca1061-do-not-hide-base-class-methods.md) | Um método em um tipo de base permanece oculto por um método nomeado identicamente em um tipo derivado, quando a assinatura do parâmetro do método derivado difere apenas pelos tipos derivados de maneira mais fraca do que os tipos correspondentes na assinatura do parâmetro do método de base. |
| CA1062 | [CA1062: validar argumentos de métodos públicos](../code-quality/ca1062-validate-arguments-of-public-methods.md) | Todos os argumentos de referência passados para os métodos visíveis externamente devem ser verificados em relação que serão nulos. |
| CA1063 | [CA1063: implementar IDisposable corretamente](../code-quality/ca1063-implement-idisposable-correctly.md) | Todos os tipos IDisposable devem implementar o padrão Dispose corretamente. |
| CA1064 | [CA1064: as exceções devem ser públicas](../code-quality/ca1064-exceptions-should-be-public.md) | Uma exceção interna só permanece visível dentro do próprio escopo interno. Depois que a exceção falha fora do escopo interno, somente a exceção de base pode ser usada para capturar a exceção. Se a exceção interna for herdada de <xref:System.Exception>, <xref:System.SystemException>, ou <xref:System.ApplicationException>, o código externo não terá informações suficientes para saber o que fazer com a exceção. |
| CA1065 | [CA1065: não acionar exceções em locais inesperados](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md) | Um método que não deve acionar exceções aciona uma exceção. |
| CA1300 | [CA1300: especificar MessageBoxOptions](../code-quality/ca1300-specify-messageboxoptions.md) | Para exibir corretamente uma caixa de mensagem para as culturas que usam uma ordem de leitura da direita para a esquerda, os membros RightAlign e RtlReading da enumeração MessageBoxOptions devem ser passados para o método Show. |
| CA1301 | [CA1301: evitar aceleradores duplicados](../code-quality/ca1301-avoid-duplicate-accelerators.md) | Uma tecla de acesso, também conhecida como acelerador, dá ao teclado acesso a um controle usando-se a tecla ALT. Quando vários controles têm teclas de acesso duplicadas, o comportamento da tecla de acesso não é bem definido. |
| CA1302 | [CA1302: não codificar cadeias de caracteres específicas da localidade](../code-quality/ca1302-do-not-hardcode-locale-specific-strings.md) | A enumeração System.Environment.SpecialFolder contém membros que fazem referência às pastas especiais do sistema. Os locais dessas pastas podem ter valores diferentes em diferentes sistemas operacionais; o usuário pode alterar alguns dos locais; e os locais são diferentes para cada linguagem. O método Environment.GetFolderPath retorna os locais associados à enumeração Environment.SpecialFolder, localizada e apropriada para o computador atualmente em execução. |
| CA1303 | [CA1303: não passar literais como parâmetros localizados](../code-quality/ca1303-do-not-pass-literals-as-localized-parameters.md) | Um método visível externamente passa uma cadeia de caracteres literal como um parâmetro para um construtor ou método na biblioteca de classes do .NET Framework, e essa cadeia de caracteres deve ser localizável. |
| CA1304 | [CA1304: especificar CultureInfo](../code-quality/ca1304-specify-cultureinfo.md) | Um método ou um construtor chama um membro que tem uma sobrecarga que aceita um parâmetro System.Globalization.CultureInfo, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro CultureInfo. Quando um objeto CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades. |
| CA1305 | [CA1305: especificar IFormatProvider](../code-quality/ca1305-specify-iformatprovider.md) | Um método ou um construtor chama um ou mais membros que têm sobrecargas que aceitam um parâmetro System.IFormatProvider, e o método ou o construtor não chama a sobrecarga que utiliza o parâmetro IFormatProvider. Quando um objeto System.Globalization.CultureInfo ou System.IFormatProvider não for fornecido, o valor padrão fornecido pelo membro sobrecarregado poderá não ter o efeito desejado em todas as localidades. |
| CA1306 | [CA1306: definir localidade para tipos de dados](../code-quality/ca1306-set-locale-for-data-types.md) | A localidade determina os elementos de apresentação específicos da cultura para dados, como a formatação usada para valores numéricos, símbolos de moeda e ordem de classificação. Ao criar um DataTable ou um DataSet, você deve definir explicitamente a localidade. |
| CA1307 | [CA1307: especificar StringComparison](../code-quality/ca1307-specify-stringcomparison.md) | Uma operação de comparação de cadeia de caracteres usa uma sobrecarga de método que não define um parâmetro StringComparison. |
| CA1308 |[CA1308: normalizar cadeias de caracteres para maiúsculas](../code-quality/ca1308-normalize-strings-to-uppercase.md) | As cadeias de caracteres devem ser normalizadas em maiúsculas. Um pequeno grupo de caracteres não pode fazer uma viagem de ida e volta quando são convertidos em minúsculas. |
| CA1309 | [CA1309: usar StringComparison ordinal](../code-quality/ca1309-use-ordinal-stringcomparison.md) | Uma operação de comparação de cadeia de caracteres não linguística não define o parâmetro StringComparison como Ordinal ou OrdinalIgnoreCase. Definindo-se explicitamente o parâmetro como StringComparison.Ordinal ou StringComparison.OrdinalIgnoreCase, o código normalmente ganha velocidade, fica mais correto e se torna mais confiável. |
| CA1400 | [CA1400: os pontos de entrada de P-Invoke devem existir](../code-quality/ca1400-p-invoke-entry-points-should-exist.md) |Um método público ou protegido é marcado usando-se o atributo System.Runtime.InteropServices.DllImportAttribute. Não foi possível localizar a biblioteca não gerenciada ou não foi possível comparar o método a uma função na biblioteca. |
| CA1401 | [CA1401: os P/Invokes não devem estar visíveis](../code-quality/ca1401-p-invokes-should-not-be-visible.md) | Um método público ou protegido em um tipo público tem o atributo System.Runtime.InteropServices.DllImportAttribute (também implementado pela palavra-chave Declare em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]). Esses métodos não devem ser expostos. |
| CA1402 |[CA1402: evitar sobrecargas em interfaces visíveis em COM](../code-quality/ca1402-avoid-overloads-in-com-visible-interfaces.md) | Quando os métodos sobrecarregados são expostos a clientes COM, apenas a primeira sobrecarga do método mantém seu nome. As sobrecargas subsequentes são renomeadas com exclusividade acrescentando-se ao nome um caractere de sublinhado (_) e um inteiro correspondente à ordem de declaração da sobrecarga. |
| CA1403 | [CA1403: os tipos de layout automático não devem ser visíveis em COM](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md) | Um tipo de valor visível por COM é marcado usando-se o atributo System.Runtime.InteropServices.StructLayoutAttribute definido como LayoutKind.Auto. O layout desses tipos pode ser alterados entre versões do .NET Framework, o que interromperá clientes COM que esperam um layout específico. |
| CA1404 | [CA1404: chamar GetLastError logo depois de P/Invoke](../code-quality/ca1404-call-getlasterror-immediately-after-p-invoke.md) | É feita uma chamada para o método Marshal.GetLastWin32Error ou o equivalente [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] função GetLastError e a chamada imediatamente anterior não é para um sistema operacional invocar o método. |
| CA1405 | [CA1405: os tipos base de tipo visível em COM devem ser visíveis em COM](../code-quality/ca1405-com-visible-type-base-types-should-be-com-visible.md) | Um tipo visível por COM deriva de um tipo que não é visível por COM. |
| CA1406 |[CA1406: evitar argumentos Int64 para clientes do Visual Basic 6](../code-quality/ca1406-avoid-int64-arguments-for-visual-basic-6-clients.md) | Os clientes COM do Visual Basic 6 não podem acessar inteiros de 64 bits. |
| CA1407 |[CA1407: evitar membros estáticos em tipos visíveis em COM](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md) | COM não dá suporte para métodos estáticos. |
| CA1408 | [CA1408: não usar AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md) | Tipos que usam uma interface dupla permitem que clientes sejam associados a um layout de interface específico. Todas as alterações feitas em uma versão futura do layout do tipo ou de qualquer tipo de base interromperão clientes COM associados à interface. Por padrão, se o atributo ClassInterfaceAttribute não for especificado, será usada uma interface somente de expedição. |
| CA1409 | [CA1409: os tipos visíveis em Com devem ser criáveis](../code-quality/ca1409-com-visible-types-should-be-creatable.md) |Um tipo de referência marcado especificamente como visível para COM contém um construtor parametrizado público, mas não contém um construtor padrão público (sem parâmetros). Um tipo sem um construtor padrão público não pode ser criado por clientes COM. |
| CA1410 | [CA1410: os métodos de registro COM devem ser correspondentes](../code-quality/ca1410-com-registration-methods-should-be-matched.md) | Um tipo declara um método marcado usando o atributo System.Runtime.InteropServices.ComRegisterFunctionAttribute, mas não declara um método marcado usando o atributo System.Runtime.InteropServices.ComUnregisterFunctionAttribute, ou vice-versa. |
| CA1411 | [CA1411: os métodos de registro COM não devem estar visíveis](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md) | Um método marcado usando-se o atributo System.Runtime.InteropServices.ComRegisterFunctionAttribute ou o atributo System.Runtime.InteropServices.ComUnregisterFunctionAttribute permanece visível externamente. |
| CA1412 | [CA1412: marcar interfaces ComSource como IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md) | Um tipo é marcado usando-se o atributo System.Runtime.InteropServices.ComSourceInterfacesAttribute, e pelo menos uma das interfaces especificadas não está marcada usando-se o atributo System.Runtime.InteropServices.InterfaceTypeAttribute definido como ComInterfaceType.InterfaceIsIDispatch. |
| CA1413 | [CA1413: evitar campos não públicos em tipos de valor visíveis em COM](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md) | Os campos de instância não pública dos tipos de valor visíveis por COM permanecem visíveis para clientes COM. Revise o conteúdo dos campos em busca de informações que não devem ser expostas, ou isso terá efeitos não intencionais sobre o design ou a segurança. |
| CA1414 | [CA1414: marcar argumentos P/Invoke boolianos com MarshalAs](../code-quality/ca1414-mark-boolean-p-invoke-arguments-with-marshalas.md) | O tipo de dados Booliano tem várias representações em código não gerenciado. |
| CA1415 | [CA1415: declarar P/Invokes corretamente](../code-quality/ca1415-declare-p-invokes-correctly.md) | Esta regra procura declarações do método de invocação do sistema operacional com funções [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)] como destino que tenham um ponteiro para um parâmetro de estrutura OVERLAPPED e o parâmetro gerenciado correspondente não seja um ponteiro para uma estrutura System.Threading.NativeOverlapped. |
| CA1500 | [CA1500: os nomes de variável não devem corresponder aos nomes de campo](../code-quality/ca1500-variable-names-should-not-match-field-names.md) | Um método de instância declara um parâmetro ou uma variável local cujo nome corresponde a um campo da instância do tipo declarante, o que leva a erros. |
| CA1501 | [CA1501: evitar herança excessiva](../code-quality/ca1501-avoid-excessive-inheritance.md) | Um tipo está mais de quatro níveis abaixo na hierarquia de herança. As hierarquias de tipo profundamente aninhado podem ser difíceis de seguir, compreender e manter. |
| CA1502 | [CA1502: evitar complexidade excessiva](../code-quality/ca1502-avoid-excessive-complexity.md) | Esta regra mede o número de caminhos linearmente independentes por meio do método, o que é determinado pelo número e pela complexidade das ramificações condicionais. |
| CA1504 | [CA1504: examinar nomes de campo confusos](../code-quality/ca1504-review-misleading-field-names.md) | O nome de um campo de instância começa com "s _", ou o nome do campo estático (compartilhado no Visual Basic) começa com "m _". |
| CA1505 | [CA1505: evitar código que não possa ser mantido](../code-quality/ca1505-avoid-unmaintainable-code.md) | Um tipo ou um método tem um baixo valor de índice de facilidade de manutenção. Um baixo índice de facilidade de manutenção indica que um tipo ou um método é provavelmente difícil de manter e seria um bom candidato para um novo design. |
| CA1506 |[CA1506: evitar acoplamento de classes excessivo](../code-quality/ca1506-avoid-excessive-class-coupling.md) | Esta regra mede o acoplamento de classes contando o número de referências de tipo exclusivas que um tipo ou um método contém. |
| CA1600 | [CA1600: não usar a prioridade de processo ociosa](../code-quality/ca1600-do-not-use-idle-process-priority.md) | Não defina a prioridade do processo como Ocioso. Os processos que têm System.Diagnostics.ProcessPriorityClass.Idle ocuparão a CPU quando estariam ociosos e, assim, bloquearão a espera. |
| CA1601 | [CA1601: não usar temporizadores que impeçam alterações no estado de energia](../code-quality/ca1601-do-not-use-timers-that-prevent-power-state-changes.md) | A atividade periódica de alta frequência manterá a CPU ocupada e interferirá nos temporizadores ociosos que economizam energia e desligam monitores e discos rígidos. |
| CA1700 | [CA1700: não nomear valores de enum como 'Reservados'](../code-quality/ca1700-do-not-name-enum-values-reserved.md) | Esta regra pressupõe que um membro da enumeração que tenha um nome que contém "reserved" não é usado atualmente, mas é um espaço reservado a ser renomeado ou removido em uma versão futura. Renomear ou remover um membro é uma alteração drástica. |
| CA1701 | [CA1701: as palavras compostas da cadeia de caracteres de recurso devem ter maiúsculas e minúsculas corretas](../code-quality/ca1701-resource-string-compound-words-should-be-cased-correctly.md) | Cada palavra na cadeia de caracteres de recurso é dividida em tokens com base em maiúsculas. Cada combinação contígua de dois tokens é verificada pela biblioteca do verificador ortográfico da Microsoft. Se reconhecidas, as palavras produzirão uma violação da regra. |
| CA1702 | [CA1702: palavras compostas devem ter maiúsculas e minúsculas corretas](../code-quality/ca1702-compound-words-should-be-cased-correctly.md) | O nome de um identificador contém várias palavras e pelo menos uma das palavras parece ser uma palavra composta que não tem maiúsculas corretas. |
| CA1703 | [CA1703: as cadeias de caracteres do recurso devem ter a ortografia correta](../code-quality/ca1703-resource-strings-should-be-spelled-correctly.md) | Uma cadeia de caracteres de recurso contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft. |
| CA1704 | [CA1704: os identificadores devem ter a ortografia correta](../code-quality/ca1704-identifiers-should-be-spelled-correctly.md) | O nome de um identificador visível externamente contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft. |
| CA1707 | [CA1707: os identificadores não devem conter sublinhados](../code-quality/ca1707-identifiers-should-not-contain-underscores.md) | Por convenção, os nomes de identificador não contêm o caractere de sublinhado (_). Esta regra verifica namespaces, tipos, membros e parâmetros. |
| CA1708 | [CA1708: os identificadores devem ser diferentes além de maiúsculas de minúsculas](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md) | Os identificadores de namespaces, tipos, membros e parâmetros não podem se diferenciar apenas por maiúsculas porque linguagens com o Common Language Runtime como destino não precisam diferenciar maiúsculas e minúsculas. |
| CA1709 | [CA1709: os identificadores devem ter maiúsculas e minúsculas corretas](../code-quality/ca1709-identifiers-should-be-cased-correctly.md) | Por convenção, nomes de parâmetro usam maiúsculas, namespace e tipo, e nomes de membro usam maiúsculas Pascal. |
| CA1710 | [CA1710: os identificadores devem ter o sufixo correto](../code-quality/ca1710-identifiers-should-have-correct-suffix.md) |Por convenção, os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, têm um sufixo associado ao tipo de base ou à interface. |
| CA1711 | [CA1711: os identificadores não devem ter sufixo incorreto](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md) | Por convenção, apenas os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, devem terminar com sufixos reservados específicos. Outros nomes de tipo não devem usar esses sufixos reservados. |
| CA1712 | [CA1712: não usar valores de enum como prefixo com o nome do tipo](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md) | Os nomes dos membros de enumeração não são prefixados usando-se o nome de tipo porque as ferramentas de desenvolvimento devem fornecer informações de tipo. |
| CA1713 | [CA1713: os eventos não devem ter um prefixo anterior ou posterior](../code-quality/ca1713-events-should-not-have-before-or-after-prefix.md) | O nome de um evento começa com "Before" ou "After". Para nomear eventos relacionados acionados em uma sequência específica, use o presente ou o pretérito para indicar a posição relativa na sequência de ações. |
| CA1714 | [CA1714: enums de sinalizadores devem ter nomes plurais](../code-quality/ca1714-flags-enums-should-have-plural-names.md) | Uma enumeração pública tem o atributo System.FlagsAttribute, e seu nome não termina com "s". Tipos marcados usando FlagsAttribute têm nomes que estão no plural porque o atributo indica que mais de um valor pode ser especificado. |
| CA1715 | [CA1715: os identificadores devem ter o prefixo correto](../code-quality/ca1715-identifiers-should-have-correct-prefix.md) | O nome de uma interface visível externamente não começa com "I" em maiúsculas. O nome de um parâmetro de tipo genérico em um tipo visível externamente ou método não começa com um "T" em maiúsculas. |
| CA1716 | [CA1716: os identificadores não devem corresponder a palavras-chave](../code-quality/ca1716-identifiers-should-not-match-keywords.md) | Um nome de namespace ou um nome de tipo corresponde a uma palavra-chave reservada em uma linguagem de programação. Os identificadores de namespaces e tipos não devem corresponder a palavras-chave definidas por com o Common Language Runtime como destino. |
| CA1717 | [CA1717: apenas enums FlagsAttribute devem ter nomes plurais](../code-quality/ca1717-only-flagsattribute-enums-should-have-plural-names.md) | As convenções de nomenclatura determinam que um nome no plural para uma enumeração indica que mais de um valor de enumeração pode ser especificado ao mesmo tempo. |
| CA1719 | [CA1719: os nomes de parâmetro não devem corresponder aos nomes de membro](../code-quality/ca1719-parameter-names-should-not-match-member-names.md) | Um nome de parâmetro deve informar o significado de um parâmetro e um nome de membro deve informar o significado de um membro. Seria um design raro se eles fossem iguais. A nomenclatura de um parâmetro com o mesmo nome do membro não é intuitiva e dificulta o uso da biblioteca. |
| CA1720 |[CA1720: os identificadores não devem conter nomes de tipo](../code-quality/ca1720-identifiers-should-not-contain-type-names.md) | O nome de um parâmetro em um membro visível externamente contém um nome de tipo de dados, ou o nome de um membro visível externamente contém um nome de tipo de dados específico da linguagem. |
| CA1721 | [CA1721: nomes de propriedade não devem corresponder a métodos get](../code-quality/ca1721-property-names-should-not-match-get-methods.md) |O nome de um membro público ou protegido começa com "Get" e, de outra forma, corresponde ao nome de uma propriedade pública ou protegida. Métodos "Get" e propriedades devem ter nomes que diferenciem claramente a função. |
| CA1722 | [CA1722: os identificadores não devem ter prefixo incorreto](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md) | Por convenção, somente determinados elementos de programação têm nomes que começam com um prefixo específico. |
| CA1724 | [CA1724: os nomes de tipo não devem corresponder a namespaces](../code-quality/ca1724-type-names-should-not-match-namespaces.md) | Nomes de tipo não devem corresponder a nomes de namespaces que são definidos na biblioteca de classes do .NET Framework. A violação dessa regra pode reduzir a usabilidade da biblioteca. |
| CA1725 | [CA1725: os nomes de parâmetro devem corresponder à declaração base](../code-quality/ca1725-parameter-names-should-match-base-declaration.md) | A nomenclatura consistente dos parâmetros em uma hierarquia de substituição aumenta a usabilidade das substituições de método. Um nome de parâmetro em um método derivado diferente do nome na declaração de base pode causar confusão em relação à possibilidade do método ser uma substituição do método de base ou de uma nova sobrecarga do método. |
| CA1726 | [CA1726: usar termos preferenciais](../code-quality/ca1726-use-preferred-terms.md) | O nome de um identificador visível externamente inclui um termo para o qual existe um termo preferido, alternativo. Como alternativa, o nome inclui o termo "Flag" ou "Flags". |
| CA1800 | [CA1800: não converter desnecessariamente](../code-quality/ca1800-do-not-cast-unnecessarily.md) | As conversões duplicadas diminui o desempenho, especialmente quando as conversões são realizadas em instruções de iteração compactas. |
| CA1801 | [CA1801: examinar parâmetros não usados](../code-quality/ca1801-review-unused-parameters.md) | Uma assinatura de método inclui um parâmetro que não é usado no corpo do método. |
| CA1802 |[CA1802: usar literais quando apropriado](../code-quality/ca1802-use-literals-where-appropriate.md) |Um campo é declarado estático e somente leitura (Shared e ReadOnly no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]), e é inicializado usando-se um valor computável no tempo de compilação. Como o valor que é atribuído ao campo de destino é computável no tempo de compilação, altere a declaração para const (Const em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) para que o valor é calculado em tempo de compilação em vez de em tempo de execução de campo. |
| CA1804 | [CA1804: remover locais não usados](../code-quality/ca1804-remove-unused-locals.md) | As variáveis locais não utilizadas e as atribuições desnecessárias aumentam o tamanho de um assembly e diminuem o desempenho. |
| CA1806 | [CA1806: não ignorar resultados do método](../code-quality/ca1806-do-not-ignore-method-results.md) | Um novo objeto é criado, mas nunca é usado; ou um método que cria e retorna uma nova cadeia de caracteres é chamado e a nova cadeia de caracteres jamais é usada; um método ou COM ou P/Invoke retorna um HRESULT ou um código de erro que nunca é usado. |
| CA1809 |[CA1809: evitar locais excessivos](../code-quality/ca1809-avoid-excessive-locals.md) | Uma otimização de desempenho comum é armazenar um valor em um registro de processador, em vez da memória, algo conhecido como "registro do valor". Para aumentar a chance de que todas as variáveis locais sejam cancelado, limite o número de variáveis locais a 64. |
| CA1810 | [CA1810: inicializar campos estáticos de tipo de referência embutido](../code-quality/ca1810-initialize-reference-type-static-fields-inline.md) | Quando um tipo declara um construtor estático explícito, o compilador JIT (just-in-time) adiciona uma verificação a cada método estático e construtor de instância do tipo para garantir que o construtor estático tenha sido chamado anteriormente. As verificações de construtor estático podem diminuir o desempenho. |
| CA1811 | [CA1811: evitar código privado não chamado](../code-quality/ca1811-avoid-uncalled-private-code.md) | Um membro particular ou interno (no nível de assembly) não tem chamadores no assembly; ele não é invocado pelo Common Language Runtime e não é invocado por um representante. |
| CA1812 | [CA1812: evitar classes internas sem instâncias](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md) | Uma instância de um tipo no nível de assembly não é criada pelo código no assembly. |
| CA1813 | [CA1813: evitar atributos não lacrados](../code-quality/ca1813-avoid-unsealed-attributes.md) | A biblioteca de classes do .NET Framework fornece métodos para recuperar atributos personalizados. Por padrão, esses métodos pesquisam a hierarquia de herança do atributo. A validação do atributo elimina a pesquisa na hierarquia de herança e pode melhorar o desempenho. |
| CA1814 | [CA1814: preferir matrizes denteadas em relação às multidimensionais](../code-quality/ca1814-prefer-jagged-arrays-over-multidimensional.md) | Uma matriz denteada é uma matriz cujos elementos são matrizes. As matrizes que constituem os elementos podem ter tamanhos diferentes, o que leva a menos espaço desperdiçado para alguns conjuntos de dados. |
| CA1815 | [CA1815: substituir Equals e operador Equals em tipos de valor](../code-quality/ca1815-override-equals-and-operator-equals-on-value-types.md) | Para tipos de valor, a implementação herdada de Equals usa a biblioteca Reflection e compara o conteúdo de todos os campos. Reflection é computacionalmente cara, e pode ser desnecessário comparar a igualdade de cada campo. Se você espera que os usuários comparem ou classifiquem instâncias, ou usem instâncias como chaves de tabela de hash, o tipo de valor deverá implementar Equals. |
| CA1816 | [CA1816: chamar GC.SuppressFinalize corretamente](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md) | Um método que é uma implementação de Dispose não chama GC. SuppressFinalize; ou um método que não é uma implementação de Dispose chama GC. SuppressFinalize; ou um método chama GC. SuppressFinalize e passa algo que não seja isso (Me no Visual Basic). |
| CA1819 | [CA1819: as propriedades não devem retornar matrizes](../code-quality/ca1819-properties-should-not-return-arrays.md) | As matrizes retornadas por propriedades não estão protegidas contra a gravação, mesmo quando a propriedade é somente leitura. Para manter a matriz à prova de adulteração, a propriedade deve retornar uma cópia da matriz. Normalmente, os usuários não compreenderão as implicações adversas no desempenho de chamar uma propriedade assim. |
| CA1820 | [CA1820: testar se há cadeias de caracteres vazias usando o comprimento da cadeia de caracteres](../code-quality/ca1820-test-for-empty-strings-using-string-length.md) | A comparação de cadeias de caracteres usando-se a propriedade String.Length ou o método String.IsNullOrEmpty é significativamente mais rápida do que o uso de Equals. |
| CA1821 | [CA1821: remover finalizadores vazios](../code-quality/ca1821-remove-empty-finalizers.md) | Sempre que possível, evite finalizadores por conta da sobrecarga adicional no desempenho envolvida no acompanhamento do tempo de vida do objeto. Um finalizador vazio incorre na sobrecarga adicionada e não oferece benefícios. |
| CA1822 |[CA1822: marcar membros como estáticos](../code-quality/ca1822-mark-members-as-static.md) | Os membros que não acessam dados da instância ou os métodos da instância de chamada podem ser marcados como estáticos (Shared no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]). Depois que você marcar os métodos como estáticos, o compilador emitirá sites de chamada não virtuais para esses membros. Isso pode proporcionar um ganho de desempenho mensurável para o código sensível ao desempenho. |
| CA1823 | [CA1823: evitar campos privados não usados](../code-quality/ca1823-avoid-unused-private-fields.md) | Foram detectados campos particulares que aparentemente não são acessados no assembly. |
| CA1824 |[CA1824: marcar assemblies com NeutralResourcesLanguageAttribute](../code-quality/ca1824-mark-assemblies-with-neutralresourceslanguageattribute.md) | O atributo NeutralResourcesLanguage informa o ResourceManager da linguagem que foi usada para exibir os recursos de uma cultura neutra para um assembly. Isso melhora o desempenho da pesquisa para o primeiro recurso carregado e pode reduzir o conjunto de trabalho. |
| CA1900 | [CA1900: os campos de tipo de valor devem ser móveis](../code-quality/ca1900-value-type-fields-should-be-portable.md) | Essa regra verifica se as estruturas declaradas usando-se o layout explícito serão alinhadas corretamente durante a realização de marshaling para o código não gerenciado em sistemas operacionais de 64 bits. |
| CA1901 | [CA1901: as declarações P/Invoke devem ser portáteis](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md) | Essa regra avalia o tamanho de cada parâmetro e o valor de retorno de um P/Invoke, além de verificar se o tamanho do parâmetro está correto durante a realização de marshaling para código não gerenciado em sistemas operacionais 32 e 64 bits. |
| CA1903 | [CA1903: usar apenas a API da estrutura de destino](../code-quality/ca1903-use-only-api-from-targeted-framework.md) | Um membro ou um tipo está usando um membro ou um tipo que foi introduzido em um service pack não incluído com a estrutura de destino do projeto. |
| CA2000 | [CA2000: descartar objetos antes de perder o escopo](../code-quality/ca2000-dispose-objects-before-losing-scope.md) | Como pode ocorrer um evento excepcional que impedirá a execução do finalizador de um objeto, o objeto deve ser explicitamente descartado antes que todas as referências a ele estejam fora do escopo. |
| CA2001 | [CA2001: evitar chamar métodos problemáticos](../code-quality/ca2001-avoid-calling-problematic-methods.md) | Um membro chama um método potencialmente perigoso ou problemático. |
| CA2002 |[CA2002: não bloquear objetos com identidade fraca](../code-quality/ca2002-do-not-lock-on-objects-with-weak-identity.md) |Diz-se que um objeto tem uma identidade fraca quando puder ser acessado diretamente em todos os limites de domínio do aplicativo. Um thread que tente adquirir um bloqueio em um objeto com uma identidade fraca pode ser bloqueado por um segundo thread em um domínio de aplicativo diferente com um bloqueio no mesmo objeto. |
| CA2003 |[CA2003: não tratar fibras como threads](../code-quality/ca2003-do-not-treat-fibers-as-threads.md) | Um thread gerenciado está sendo tratado como um thread do [!INCLUDE[TLA2#tla_win32](../code-quality/includes/tla2sharptla_win32_md.md)]. |
| CA2004 | [CA2004: remover chamadas para GC.KeepAlive](../code-quality/ca2004-remove-calls-to-gc-keepalive.md) | Se você converter no uso de SafeHandle, remova todas as chamadas para GC.KeepAlive (objeto). Nesse caso, as classes não precisarão chamar GC.KeepAlive. Isso pressupõe que elas não tenham um finalizador, mas dependam de SafeHandle para finalizar o identificador do sistema operacional para elas. |
| CA2006 | [CA2006: use SafeHandle para encapsular recursos nativos](../code-quality/ca2006-use-safehandle-to-encapsulate-native-resources.md) | O uso de IntPtr em código gerenciado pode indicar um problema de segurança e confiabilidade em potencial. Todos os usos de IntPtr devem ser examinados para determinar se o uso de um SafeHandle, ou tecnologia semelhante, é necessário em seu lugar. |
| CA2100 | [CA2100: examinar consultas SQL para vulnerabilidades de segurança](../code-quality/ca2100-review-sql-queries-for-security-vulnerabilities.md) | Um método define a propriedade System.Data.IDbCommand.CommandText usando uma cadeia de caracteres criada com base em um argumento da cadeia de caracteres para o método. Esta regra pressupõe que o argumento da cadeia de caracteres contenha a entrada do usuário. Uma cadeia de caracteres de comando SQL criada com base na entrada do usuário é vulnerável a ataques de injeção SQL. |
| CA2101 |[CA2101: especificar marshaling para argumentos de cadeia de caracteres P/Invoke](../code-quality/ca2101-specify-marshaling-for-p-invoke-string-arguments.md) | Um membro de invocação da plataforma permite chamadores parcialmente confiáveis, tem um parâmetro de cadeia de caracteres e não realiza marshaling da cadeia de caracteres explicitamente. Isso pode causar uma vulnerabilidade de segurança em potencial. |
| CA2102 | [CA2102: capturar exceções que não sejam CLSCompliant em manipuladores gerais](../code-quality/ca2102-catch-non-clscompliant-exceptions-in-general-handlers.md) | Um membro em um assembly que não é marcado usando-se o RuntimeCompatibilityAttribute ou que é marcado como RuntimeCompatibility (WrapNonExceptionThrows = false) contém um bloco de captura que trata System.Exception e não contém um bloco de captura geral imediatamente posterior. |
| CA2103 | [CA2103: examinar segurança obrigatória](../code-quality/ca2103-review-imperative-security.md) |Um método usa segurança obrigatória e pode construir a permissão usando as informações de estado ou os valores de retorno que podem ser alterados desde que a demanda esteja ativa. Use a segurança declarativa sempre que possível. |
| CA2104 |[CA2104: não declarar tipos de referência mutáveis somente leitura](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md) | Um tipo visível externamente contém um campo somente leitura visível externamente que é um tipo de referência mutável. Um tipo mutável é um tipo cujos dados da instância podem ser modificados. |
| CA2105 | [CA2105: campos de matriz não devem ser somente leitura](../code-quality/ca2105-array-fields-should-not-be-read-only.md) |Quando você aplica o modificador somente leitura (ReadOnly in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) a um campo que contém uma matriz, o campo não pode ser alterado para fazer referência a uma matriz diferente. No entanto, os elementos da matriz que são armazenados em um campo somente leitura podem ser alterados. |
| CA2106 | [CA2106: declarações seguras](../code-quality/ca2106-secure-asserts.md) | Um método declara uma permissão e nenhuma verificação de segurança é realizada no chamador. A declaração de uma permissão de segurança sem realizar verificações de segurança pode deixar uma fraqueza de segurança explorável no código. |
| CA2107 | [CA2107: examinar o uso de deny e permit only](../code-quality/ca2107-review-deny-and-permit-only-usage.md) |O método PermitOnly e as ações de segurança CodeAccessPermission devem ser usadas apenas por aqueles que tenham um conhecimento avançado de segurança do .NET Framework. O código que usa essas ações de segurança deve passar por uma revisão de segurança. |
| CA2108 | [CA2108: examinar segurança declarativa em tipos de valor](../code-quality/ca2108-review-declarative-security-on-value-types.md) | Um tipo de valor público ou protegido é resguardado por acesso a dados ou exigências de vínculo. |
| CA2109 | [CA2109: examinar manipuladores de eventos visíveis](../code-quality/ca2109-review-visible-event-handlers.md) | Um método público ou protegido de tratamento de eventos foi detectado. Os métodos de tratamento de eventos não devem ser expostos, a menos que seja absolutamente necessário. |
| CA2111 |[CA2111: os ponteiros não devem estar visíveis](../code-quality/ca2111-pointers-should-not-be-visible.md) | Um ponteiro não é privado, interno ou somente leitura. Um código mal-intencionado pode alterar o valor do ponteiro, o que pode dar acesso a locais arbitrários na memória ou causar falhas no aplicativo ou no sistema. |
| CA2112 | [CA2112: os tipos seguros não devem expor campos](../code-quality/ca2112-secured-types-should-not-expose-fields.md) | Um tipo público ou protegido contém campos públicos e é protegido por exigências de vínculo. Se tiver acesso a uma instância de um tipo protegido por uma exigência de vínculo, o código não precisará atender à exigência de vínculo para acessar os campos do tipo. |
| CA2114 | [CA2114: a segurança de método deve ser um superconjunto de tipo](../code-quality/ca2114-method-security-should-be-a-superset-of-type.md) | Um método não deve ter segurança declarativa no nível do método e no nível do tipo para a mesma ação. |
| CA2115 | [CA2115: chamar GC.KeepAlive durante o uso de recursos nativos](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md) | Esta regra detecta erros que podem ocorrer porque um recurso não gerenciado está sendo finalizado, enquanto ainda está sendo usado em código não gerenciado. |
| CA2116 | [CA2116: os métodos APTCA só devem chamar métodos APTCA](../code-quality/ca2116-aptca-methods-should-only-call-aptca-methods.md) |Quando APTCA AllowPartiallyTrustedCallersAttribute () estiver presente em um assembly totalmente confiável e o assembly executar código em outro assembly que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. |
| CA2117 | [CA2117: os tipos APTCA só devem estender tipos base APTCA](../code-quality/ca2117-aptca-types-should-only-extend-aptca-base-types.md) | Quando APTCA estiver presente em um assembly totalmente confiável e um tipo no assembly for herdado de um tipo que não permita chamadores parcialmente confiáveis, será possível uma exploração de segurança. |
| CA2118 | [CA2118: examinar uso de SuppressUnmanagedCodeSecurityAttribute](../code-quality/ca2118-review-suppressunmanagedcodesecurityattribute-usage.md) |SuppressUnmanagedCodeSecurityAttribute altera o comportamento do sistema de segurança padrão para membros que executem código não gerenciado que usa interoperabilidade COM ou invocação do sistema operacional. Esse atributo é usado principalmente para aumentar o desempenho; no entanto, os ganhos de desempenho acompanham riscos de segurança significativos. |
| CA2119 | [CA2119: métodos para lacrar que atendam a interfaces privadas](../code-quality/ca2119-seal-methods-that-satisfy-private-interfaces.md) | Um tipo público herdável fornece uma implementação de método substituível de uma interface (Friend no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) interna. Para corrigir uma violação dessa regra, evite que o método seja substituído fora do assembly. |
| CA2120 | [CA2120: proteger construtores de serialização](../code-quality/ca2120-secure-serialization-constructors.md) | Esse tipo tem um construtor que utiliza um objeto System.Runtime.Serialization.SerializationInfo e um objeto System.Runtime.Serialization.StreamingContext (a assinatura do construtor de serialização). Esse construtor não é protegido por uma verificação de segurança, mas um ou mais dos construtores regulares no tipo são protegidos. |
| CA2121 | [CA2121: os construtores estáticos devem ser privados](../code-quality/ca2121-static-constructors-should-be-private.md) | O sistema chama o construtor estático antes que a primeira instância do tipo seja criada ou que outros membros estáticos sejam referenciados. Se não for privado, um construtor estático poderá ser chamado por um código diferente do sistema. Dependendo das operações realizadas no construtor, isso pode causar um comportamento inesperado. |
| CA2122 | [CA2122: não expor indiretamente métodos com demandas de link](../code-quality/ca2122-do-not-indirectly-expose-methods-with-link-demands.md) | Um membro público ou protegido tem exigências de vínculo e é chamado por um membro que não realiza nenhuma verificação de segurança. Uma exigência de vínculo verifica as permissões apenas do chamador imediato. |
| CA2123 | [CA2123: as demandas de link de substituição devem ser idênticas à base](../code-quality/ca2123-override-link-demands-should-be-identical-to-base.md) | Esta regra compara um método ao método de base, que é uma interface ou um método virtual em outro tipo e, em seguida, compara as exigências de vínculo em cada um. Se essa regra for violada, um chamador mal-intencionado poderá ignorar a exigência de vínculo apenas chamando o método não seguro. |
| CA2124 | [CA2124: encapsular cláusulas finalmente vulneráveis em tentativa externa](../code-quality/ca2124-wrap-vulnerable-finally-clauses-in-outer-try.md) | Um método público ou protegido contém um bloco try/finally. O bloco finally aparentemente redefine o estado de segurança não está incluído em um bloco finally. |
| CA2126 | [CA2126: demandas do link de tipo exigem demandas de herança](../code-quality/ca2126-type-link-demands-require-inheritance-demands.md) | Um tipo sem lacre público é protegido usando-se uma exigência de link e tem um método substituível. Nem o tipo nem o método é protegido usando-se uma exigência de herança. |
| CA2127 | [CA2136: os membros não devem ter anotações de transparência conflitantes](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md) | Código crítico não pode ocorrer em um assembly 100 por cento transparente. Esta regra analisa assemblies 100 por cento transparente para todas as anotações de SecurityCritical no tipo, campo e os níveis de método. |
| CA2128 |[CA2147: os métodos transparentes talvez não usem declarações de segurança](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md) | Esta regra analisa todos os métodos e tipos em um assembly que é 100 por cento transparente ou misto transparente/crítico e sinaliza o uso declarativo ou obrigatório de Assert. |
| CA2129 | [CA2140: código transparente não deve fazer referência a itens críticos de segurança](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md) | Métodos que são marcados por SecurityTransparentAttribute chamam membros públicos marcados como SecurityCritical. Esta regra analisa todos os métodos e tipos em um assembly que seja transparente/crítico misto, e sinaliza todas as chamadas de código transparente para o código crítico não público que não estejam marcadas como SecurityTreatAsSafe. |
| CA2130 | [CA2130: as constantes críticas de segurança devem ser transparentes](../code-quality/ca2130-security-critical-constants-should-be-transparent.md) | A imposição de transparência não é imposta para valores constantes porque compiladores têm valores constantes internos de modo que nenhuma pesquisa seja necessária no tempo de execução. Os campos constantes devem ter segurança transparente de forma que os revisores de código não pressuponham que o código transparente não pode acessar a constante. |
| CA2131 | [CA2131: os tipos críticos de segurança podem não participar da equivalência de tipo](../code-quality/ca2131-security-critical-types-may-not-participate-in-type-equivalence.md) | Um tipo participa da equivalência do tipo e o próprio tipo, ou um membro ou campo do tipo, é marcado usando-se o atributo SecurityCriticalAttribute. Esta regra ocorre em qualquer tipo crítico ou em tipos que contenham métodos críticos ou campos que estejam participando da equivalência do tipo. Ao detectar um tipo assim, o CLR não o carrega com um TypeLoadException em tempo de execução. Normalmente, essa regra só é acionada quando usuários implementam equivalência de tipo manualmente, em vez de depender de tlbimp e dos compiladores para fazer a equivalência do tipo. |
| CA2132 | [CA2132: os construtores padrão devem ser pelo menos tão críticos quanto construtores padrão do tipo base](../code-quality/ca2132-default-constructors-must-be-at-least-as-critical-as-base-type-default-constructors.md) |Os tipos e os membros que têm o SecurityCriticalAttribute não podem ser usados pelo código de aplicativo do Silverlight. Os tipos de segurança crítica e os membros só podem ser usados por código confiável no .NET Framework para a biblioteca de classes do Silverlight. Como uma construção pública ou protegida em uma classe derivada deve ter a mesma transparência maior que sua classe base, uma classe em um aplicativo não pode ser derivada de uma classe marcada como SecurityCritical. |
| CA2133 | [CA2133: os representantes devem ser associados a métodos com transparência consistente](../code-quality/ca2133-delegates-must-bind-to-methods-with-consistent-transparency.md) | Esse aviso é acionado em um método que associa um representante que foi marcado usando-se o SecurityCriticalAttribute para um método transparente ou marcado usando-se SecuritySafeCriticalAttribute. O aviso também é acionado em um método que associa um representante transparente ou de segurança crítica a um método crítico. |
| CA2134 | [CA2134: os métodos devem manter uma transparência consistente durante a substituição dos métodos base](../code-quality/ca2134-methods-must-keep-consistent-transparency-when-overriding-base-methods.md) |Essa regra é acionada quando um método marcado usando-se o SecurityCriticalAttribute substitui um método transparente ou marcado usando-se SecuritySafeCriticalAttribute. A regra também é acionada quando um método transparente ou marcado usando-se SecuritySafeCriticalAttribute substitui um método marcado usando-se um SecurityCriticalAttribute. A regra é aplicada durante a substituição de um método virtual ou a implementação de uma interface. |
| CA2135 | [CA2135: os assemblies de nível 2 não devem conter LinkDemands](../code-quality/ca2135-level-2-assemblies-should-not-contain-linkdemands.md) | LinkDemands são preteridos no conjunto de regras de segurança nível 2. Em vez de usar LinkDemands para impor a segurança em tempo de compilação JIT, marque os métodos, os tipos e os campos usando o atributo SecurityCriticalAttribute. |
| CA2136 | [CA2136: os membros não devem ter anotações de transparência conflitantes](../code-quality/ca2136-members-should-not-have-conflicting-transparency-annotations.md) | Os atributos de transparência são aplicados com base nos elementos de código de escopo maior a elementos de escopo menor. Os atributos de transparência dos elementos de código que têm escopo maior têm precedência sobre atributos de transparência dos elementos de código contidos no primeiro elemento. Por exemplo, uma classe marcada usando-se o atributo SecurityCriticalAttribute não pode conter um método marcado usando-se o atributo SecuritySafeCriticalAttribute. |
| CA2137 | [CA2137: os métodos transparentes só devem conter o nível de integridade verificável](../code-quality/ca2137-transparent-methods-must-contain-only-verifiable-il.md) | Um método contém código não verificável ou retorna um tipo por referência. Esta regra é acionada em tentativas por código transparente de segurança para executar MISL (Microsoft Intermediate Language) não verificável. Entretanto, a regra não contém um verificador de IL completo e, em vez disso, usa heurística para capturar a maioria das violações de verificação de MSIL. |
| CA2138 | [CA2138: os métodos transparentes não devem chamar métodos com o atributo SuppressUnmanagedCodeSecurity](../code-quality/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute.md) | Um método de segurança transparente chama um método marcado usando-se o atributo SuppressUnmanagedCodeSecurityAttribute. |
| CA2139 | [CA2139: os métodos transparentes talvez não usem o atributo HandleProcessCorruptingExceptions](../code-quality/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute.md) | Esta regra é acionada por qualquer método que seja transparente e tenta tratar uma exceção de corrompimento de processo usando o atributo HandleProcessCorruptedStateExceptionsAttribute. Uma exceção de corrompimento de processo é uma classificação de exceção do CLR versão 4.0 de exceções, como AccessViolationException. O atributo HandleProcessCorruptedStateExceptionsAttribute só pode ser usado por métodos de segurança crítica e será ignorado se for aplicado a um método transparente. |
| CA2140 | [CA2140: código transparente não deve fazer referência a itens críticos de segurança](../code-quality/ca2140-transparent-code-must-not-reference-security-critical-items.md) | Um elemento de código marcado usando-se o atributo SecurityCriticalAttribute é crítico para segurança. Um método transparente não pode usar um elemento crítico para segurança. Se um tipo transparente tentar usar um tipo crítico de segurança, um TypeAccessException, um MethodAccessException ou um FieldAccessException será acionado. |
| CA2141 |[CA2141: métodos transparentes não devem atender a LinkDemands](../code-quality/ca2141-transparent-methods-must-not-satisfy-linkdemands.md) | Um método transparente de segurança chama um método em um assembly que não foi marcado usando-se o APTCA ou um método transparente de segurança atende a um LinkDemand para um tipo ou um método. |
| CA2142 | [CA2142: código transparente não deve ser protegido com LinkDemands](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md) | Esta regra é acionada em métodos transparentes que exigem LinkDemands para serem acessados. O código transparente de segurança não deve ser responsável por verificar a segurança de uma operação e, assim, não deve exigir permissões. |
| CA2143 | [CA2143: métodos transparentes não devem usar demandas de segurança](../code-quality/ca2143-transparent-methods-should-not-use-security-demands.md) | O código transparente de segurança não deve ser responsável por verificar a segurança de uma operação e, assim, não deve exigir permissões. O código transparente de segurança deve usar demandas completas para tomar decisões de segurança e o código crítico de segurança não deve confiar no código transparente para fazer a demanda completa. |
| CA2144 | [CA2144: o código transparente não deve carregar assemblies de matrizes de bytes](../code-quality/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays.md) | A revisão de segurança para o código transparente não é tão completo quanto a revisão de segurança para o código crítico porque o código transparente não pode realizar ações confidenciais de segurança. Os assemblies carregados a partir de uma matriz de bytes podem não ser observados no código transparente e essa matriz de bytes pode conter código crítico ou código crítico de segurança mais importante, que precisa ser auditado. |
| CA2145 | [CA2145: os métodos transparentes não devem ser decorados com o SuppressUnmanagedCodeSecurityAttribute](../code-quality/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute.md) | Os métodos decorados pelo atributo SuppressUnmanagedCodeSecurityAttribute têm um LinkDemand implícito colocado em qualquer método que o chame. Este LinkDemand requer que o código de chamada seja crítico de segurança. A marcação do método que usa SuppressUnmanagedCodeSecurity usando o atributo SecurityCriticalAttribute torna esse requisito mais óbvio para chamadores do método. |
| CA2146 | [CA2146: tipos devem ser pelo menos tão críticos quanto seus tipos base e interfaces](../code-quality/ca2146-types-must-be-at-least-as-critical-as-their-base-types-and-interfaces.md) | Esta regra é acionada quando um tipo derivado tem um atributo de transparência de segurança que não é tão crítico quanto seu tipo de base ou interface implementada. Apenas os tipos críticos podem derivar os tipos de base críticos ou implementar interfaces críticos, e apenas os tipos críticos ou de segurança crítica podem derivar dos tipos de base críticos de segurança ou implementar interfaces críticas de segurança. |
| CA2147 |[CA2147: os métodos transparentes talvez não usem declarações de segurança](../code-quality/ca2147-transparent-methods-may-not-use-security-asserts.md) | O código que é marcado como SecurityTransparentAttribute não recebe permissões suficientes para declarar. |
| CA2149 | [CA2149: métodos transparentes não devem chamar código nativo](../code-quality/ca2149-transparent-methods-must-not-call-into-native-code.md) | Esta regra é aciona em qualquer método transparente chamado diretamente no código nativo (por exemplo, por meio de um P/Invoke). As violações dessa regra resultam em um MethodAccessException no modelo de transparência de nível 2 e uma demanda completa para UnmanagedCode no modelo de transparência de nível 1. |
| CA2151 |[CA2151: campos com tipos críticos devem ser críticos para segurança](../code-quality/ca2151-fields-with-critical-types-should-be-security-critical.md) | Para usar tipos de segurança crítica, o código que faz referência ao tipo deve ser de segurança crítica ou de segurança crítica segura. Isso será verdadeiro mesmo que a referência seja indireta. Por isso, ter um campo de segurança transparente ou de segurança crítica é enganoso porque o código transparente continuará incapaz de acessar o campo. |
| CA2200 | [CA2200: relançar para preservar detalhes da pilha](../code-quality/ca2200-rethrow-to-preserve-stack-details.md) | Uma exceção é lançada novamente e a exceção é especificada explicitamente na instrução throw. Se uma exceção for lançada novamente pela especificação da exceção na instrução throw, a lista de chamadas de método entre o método original que lançou a exceção e o método atual será perdida. |
| CA2201 | [CA2201: não acionar tipos de exceção reservados](../code-quality/ca2201-do-not-raise-reserved-exception-types.md) | Isso torna o erro original difícil de detectar e depurar. |
| CA2202 | [CA2202: não descartar objetos várias vezes](../code-quality/ca2202-do-not-dispose-objects-multiple-times.md) |Uma implementação do método contém caminhos de código que poderiam causar várias chamadas para System.IDisposable.Dispose ou para um equivalente a Dispose (como um método Close() em alguns tipos) no mesmo objeto. |
| CA2204 | [CA2204: os literais devem ter a ortografia correta](../code-quality/ca2204-literals-should-be-spelled-correctly.md) | Uma cadeia de caracteres literal em um corpo de método contém uma ou mais palavras não reconhecidas pela biblioteca do verificador ortográfico da Microsoft. |
| CA2205 | [CA2205: usar equivalentes gerenciados da API do Win32](../code-quality/ca2205-use-managed-equivalents-of-win32-api.md) | Um sistema operacional invocar o método é definido e um método que tem a funcionalidade equivalente está localizado na biblioteca de classes do .NET Framework. |
| CA2207 | [CA2207: inicializar campos estáticos de tipo de valor embutido](../code-quality/ca2207-initialize-value-type-static-fields-inline.md) | Um tipo de valor declara um construtor estático explícito. Para corrigir uma violação dessa regra, inicialize todos os dados estáticos quando declarados e remova o construtor estático. |
| CA2208 |[CA2208: instanciar exceções de argumento corretamente](../code-quality/ca2208-instantiate-argument-exceptions-correctly.md) | For feita uma chamada para o construtor padrão (sem parâmetros) de um tipo de exceção que seja ou derive de ArgumentException, ou um argumento de cadeia de caracteres incorreto é passado para um construtor com parâmetros de um tipo de exceção que seja ou derive de ArgumentException. |
| CA2210 |[CA2210: os assemblies devem ter nomes fortes válidos](../code-quality/ca2210-assemblies-should-have-valid-strong-names.md) | O nome forte protege clientes do carregamento desconhecido de um assembly adulterado. Os assemblies sem nomes fortes não devem ser implantados fora de cenários muito limitados. Se você compartilhar ou distribuir assemblies não assinados corretamente, o assembly poderá ser adulterado, o Common Language Runtime poderá não carregar o assembly ou o usuário talvez precise desabilitar a verificação em seu computador. |
| CA2211 |[CA2211: os campos não constantes não devem estar visíveis](../code-quality/ca2211-non-constant-fields-should-not-be-visible.md) | Os campos estáticos que não são constantes nem somente leitura não são thread-safe. O acesso a esse campo deve ser controlado cuidadosamente e exige técnicas de programação avançadas para sincronizar o acesso ao objeto da classe. |
| CA2212 | [CA2212: não marcar componentes atendidos com WebMethod](../code-quality/ca2212-do-not-mark-serviced-components-with-webmethod.md) |Um método em um tipo herdado de System.EnterpriseServices.ServicedComponent é marcado usando-se System.Web.Services.WebMethodAttribute. Como WebMethodAttribute e um método ServicedComponent têm comportamento e requisitos conflitantes para o contexto e o fluxo de transações, o comportamento do método estará incorreto em alguns cenários. |
| CA2213 | [CA2213: os campos descartáveis devem ser descartados](../code-quality/ca2213-disposable-fields-should-be-disposed.md) | Um tipo que implementa System.IDisposable declara campos que são de tipos que também implementam IDisposable. O método Dispose do campo não é chamado pelo método Dispose do tipo declarante. |
| CA2214 | [CA2214: não chamar métodos substituíveis em construtores](../code-quality/ca2214-do-not-call-overridable-methods-in-constructors.md) | Ao chamar um método virtual, o construtor da instância que invoca o método pode não ter sido executado. |
| CA2215 | [CA2215: métodos Dispose devem chamar o descarte da classe base](../code-quality/ca2215-dispose-methods-should-call-base-class-dispose.md) | Se for herdado de um tipo descartável, um tipo deverá chamar o método Dispose do tipo de base em seu próprio método Dispose. |
| CA2216 |[CA2216: os tipos descartáveis devem declarar o finalizador](../code-quality/ca2216-disposable-types-should-declare-finalizer.md) | Um tipo que implementa System.IDisposable e tem campos que sugerem o uso de recursos não gerenciados não implementa um finalizador, conforme descrito por Object.Finalize. |
| CA2217 | [CA2217: não marcar enums com FlagsAttribute](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md) |Uma enumeração visível externamente é marcada usando-se FlagsAttribute e tem um ou mais valores que não são potências de dois ou uma combinação dos outros valores definidos na enumeração. |
| CA2218 |[CA2218: substituir GetHashCode em igualdades de substituição](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md) | GetHashCode retorna um valor, com base na instância atual, adequado para algoritmos de hash e estruturas de dados como uma tabela de hash. Dois objetos que tenham o mesmo tipo e sejam iguais devem retornar o mesmo código hash. |
| CA2219 | [CA2219: não acionar exceções em cláusulas de exceção](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md) | Quando uma exceção é acionada em uma cláusula finally ou fault, a nova exceção oculta a exceção ativa. Quando uma exceção é acionada em uma cláusula de filtro, o tempo de execução captura silenciosamente a exceção. Isso torna o erro original difícil de detectar e depurar. |
| CA2220 | [CA2220: finalizadores devem chamar o finalizador da classe base](../code-quality/ca2220-finalizers-should-call-base-class-finalizer.md) | A finalização deve ser propagada em toda a hierarquia de herança. Para garantir isso, os tipos devem chamar o método Finalize de classe base em seu próprio método Finalize. |
| CA2221 |[CA2221: os finalizadores devem ser protegidos](../code-quality/ca2221-finalizers-should-be-protected.md) | Os finalizadores deve usar o modificador de acesso da família. |
| CA2222 | [CA2222: não diminuir a visibilidade de membro herdada](../code-quality/ca2222-do-not-decrease-inherited-member-visibility.md) |Você não deve alterar o modificador de acesso para membros herdados. A alteração de um membro herdado para particular não impede que os chamadores acessem a implementação da classe base do método. |
| CA2223 | [CA2223: os membros devem ser diferentes em algo além do tipo de retorno](../code-quality/ca2223-members-should-differ-by-more-than-return-type.md) | Embora o Common Language Runtime permita o uso de tipos de retorno na diferenciação de membros outrora idênticos, este recurso não está na CLS nem é um recurso comum das linguagens de programação do .NET. |
| CA2224 | [CA2224: substituir Equals ao sobrecarregar o operador Equals](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md) | Um tipo público implementa o operador de igualdade, mas não substitui Object.Equals. |
| CA2225 | [CA2225: as sobrecargas do operador têm alternativos nomeados](../code-quality/ca2225-operator-overloads-have-named-alternates.md) |Uma sobrecarga de operador foi detectada, e o método alternativo nomeado esperado não foi encontrado. O membro alternativo nomeado fornece acesso à mesma funcionalidade que o operador, e é fornecido para desenvolvedores que programem em linguagens que não dão suporte a operadores sobrecarregados. |
| CA2226 | [CA2226: os operadores devem ter sobrecargas simétricas](../code-quality/ca2226-operators-should-have-symmetrical-overloads.md) | Um tipo implementa o operador de igualdade ou de desigualdade e não implementa o operador oposto. |
| CA2227 |[CA2227: propriedades de coleção devem ser somente leitura](../code-quality/ca2227-collection-properties-should-be-read-only.md) |Uma propriedade collection gravável permite que um usuário substitua a coleção por uma coleção diferente. Uma propriedade somente leitura evita que a coleção seja substituída, mas ainda permite que membros individuais sejam definidos. |
| CA2228 | [CA2228: não remeter formatos de recurso não lançados](../code-quality/ca2228-do-not-ship-unreleased-resource-formats.md) | Arquivos de recursos que foram compilados usando versões de pré-lançamento do .NET Framework não podem ser usados por versões com suporte do .NET Framework. |
| CA2229 | [CA2229: implementar construtores de serialização](../code-quality/ca2229-implement-serialization-constructors.md) | Para corrigir uma violação dessa regra, implemente o construtor de serialização. Para uma classe lacrada, torne o construtor particular; do contrário, deixe-o protegido. |
| CA2230 | [CA2230: usar parâmetros para argumentos variáveis](../code-quality/ca2230-use-params-for-variable-arguments.md) | Um tipo público ou protegido contém um método público ou protegido que usa a convenção de chamada VarArgs, em vez da palavra-chave params. |
| CA2231 | [CA2231: sobrecarregar operador Equals ao substituir ValueType.Equals](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md) | Um tipo de valor substitui Object.Equals, mas não implementa o operador de igualdade. |
| CA2232 | [CA2232: marcar pontos de entrada do Windows Forms com STAThread](../code-quality/ca2232-mark-windows-forms-entry-points-with-stathread.md) | STAThreadAttribute indica que o modelo de threading COM para o aplicativo é um single-threaded apartment. Esse atributo deve estar presente no ponto de entrada de qualquer aplicativo que use o Windows Forms; se ele for omitido, os componentes do Windows poderão não funcionar corretamente. |
| CA2233 |[CA2233: as operações não devem estourar](../code-quality/ca2233-operations-should-not-overflow.md) | Você não deve realizar operações aritméticas sem primeiro validar os operandos. Isso garante que o resultado da operação não esteja fora do intervalo de valores possíveis para os tipos de dados que estão envolvidos. |
| CA2234 | [CA2234: passar objetos System.Uri em vez de cadeias de caracteres](../code-quality/ca2234-pass-system-uri-objects-instead-of-strings.md) | Foi feita uma chamada para um método com um parâmetro de cadeia de caracteres cujo nome contém "uri", "URI", "urn", "URN", "url" ou "URL". O tipo declarante do método contém uma sobrecarga do método correspondente que possui um parâmetro System.Uri. |
| CA2235 | [CA2235: marcar todos os campos não serializáveis](../code-quality/ca2235-mark-all-non-serializable-fields.md) | Um campo de instância de um tipo que não seja serializável é declarado em um tipo que é serializável. |
| CA2236 | [CA2236: chamar métodos de classe base em tipos ISerializable](../code-quality/ca2236-call-base-class-methods-on-iserializable-types.md) | Para corrigir uma violação dessa regra, chame o método GetObjectData de tipo base ou o construtor de serialização do método de tipo derivado correspondente ou do construtor. |
| CA2237 | [CA2237: marcar tipos ISerializable com SerializableAttribute](../code-quality/ca2237-mark-iserializable-types-with-serializableattribute.md) | Para serem reconhecidos pelo Common Language Runtime como serializáveis, os tipos devem ser marcados usando-se o atributo SerializableAttribute, mesmo quando o tipo usa uma rotina de serialização personalizada por meio da implementação da interface ISerializable. |
| CA2238 |[CA2238: implementar métodos de serialização corretamente](../code-quality/ca2238-implement-serialization-methods-correctly.md) | Um método que trata um evento de serialização não tem a assinatura, o tipo de retorno ou a visibilidade corretos. |
| CA2239 | [CA2239: fornecer métodos de desserialização para campos opcionais](../code-quality/ca2239-provide-deserialization-methods-for-optional-fields.md) | Um tipo tem um campo que foi marcado usando-se o atributo System.Runtime.Serialization.OptionalFieldAttribute, e o tipo não fornece métodos de tratamento de eventos de desserialização. |
| CA2240 | [CA2240: implementar ISerializable corretamente](../code-quality/ca2240-implement-iserializable-correctly.md) | Para corrigir uma violação dessa regra, deixe o método GetObjectData visível e substituível e verifique se todos os campos de instância estão incluídos no processo de serialização ou marcados explicitamente usando-se o atributo NonSerializedAttribute. |
| CA2241 | [CA2241: fornecer argumentos corretos para métodos de formatação](../code-quality/ca2241-provide-correct-arguments-to-formatting-methods.md) | O argumento format passado para System.String.Format não contém um item de formato correspondente a cada argumento do objeto ou vice-versa. |
| CA2242 |[CA2242: testar para NaN corretamente](../code-quality/ca2242-test-for-nan-correctly.md) | Essa expressão testa um valor em Single.Nan ou Double.Nan. Use Single.IsNan (único) ou Double.IsNan (duplo) para testar o valor. |
| CA2243 |[CA2243: os literais de cadeia de caracteres de atributo devem ser analisados corretamente](../code-quality/ca2243-attribute-string-literals-should-parse-correctly.md) | O parâmetro literal da cadeia de caracteres de um atributo não é analisado corretamente para uma URL, um GUID ou uma versão. |
| CA5122 | [CA5122: as declarações de P-Invoke não devem ser críticas para segurança](../code-quality/ca5122-p-invoke-declarations-should-not-be-safe-critical.md) | Os métodos são marcados como SecuritySafeCritical quando executam uma operação confidencial de segurança, mas também são seguros para serem usados pelo código transparente. O código transparente jamais pode chamar diretamente o código nativo por meio de um P/Invoke. Por isso, a marcação de um P/Invoke como crítico de segurança não permitirá que o código transparente o chame, e é enganosa na análise de segurança. |