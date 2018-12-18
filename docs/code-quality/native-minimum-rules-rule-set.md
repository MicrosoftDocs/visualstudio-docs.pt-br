---
title: Conjunto de regras mínimas nativo
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 2d898bc4-fba5-472e-8f09-b0c6b511c5a3
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9149276064b76a08705b70883bb3c2e136e23334
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389008"
---
# <a name="native-minimum-rules-rule-set"></a>Conjunto de regras mínimas nativo
O Microsoft Native mínimo regras enfocam os problemas mais críticos do código nativo, inclusive falhas potenciais de segurança e falhas do aplicativo. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos nativos.

|Regra|Descrição|
|----------|-----------------|
|[C6001](../code-quality/c6001.md)|Uso de memória não inicializada|
|[C6011](../code-quality/c6011.md)|Desreferenciando ponteiro nulo|
|[C6029](../code-quality/c6029.md)|Uso de valores não marcados|
|[C6053](../code-quality/c6053.md)|Terminação em zero da chamada|
|[C6059](../code-quality/c6059.md)|Concatenação defeituosa|
|[C6063](../code-quality/c6063.md)|Argumento da cadeia de caracteres ausente para formatar função|
|[C6064](../code-quality/c6064.md)|Argumento inteiro ausente para formatar função|
|[C6066](../code-quality/c6066.md)|Argumento de ponteiro ausente para formatar função|
|[C6067](../code-quality/c6067.md)|Argumento de ponteiro de cadeia de caracteres ausente para formatar função|
|[C6101](../code-quality/c6101.md)|Retornando a memória não inicializada|
|[C6200](../code-quality/c6200.md)|O índice excede o máximo do buffer|
|[C6201](../code-quality/c6201.md)|O índice excede o máximo do buffer da pilha|
|[C6270](../code-quality/c6270.md)|Falta argumento float para formatar a função|
|[C6271](../code-quality/c6271.md)|Argumento extra para formatar função|
|[C6272](../code-quality/c6272.md)|Argumento diferente de float para formatar a função|
|[C6273](../code-quality/c6273.md)|Argumento não inteiro para formatar função|
|[C6274](../code-quality/c6274.md)|Argumento diferente de caractere para formatar a função|
|[C6276](../code-quality/c6276.md)|Conversão de cadeia de caracteres inválida|
|[C6277](../code-quality/c6277.md)|Chamada CreateProcess inválida|
|[C6284](../code-quality/c6284.md)|Argumento de objeto inválido para formatar a função|
|[C6290](../code-quality/c6290.md)|Precedência de NOT lógico AND bit a bit|
|[C6291](../code-quality/c6291.md)|Precedência de NOT lógico OR bit a bit|
|[C6302](../code-quality/c6302.md)|Argumento da cadeia de caracteres inválido para formatar a função|
|[C6303](../code-quality/c6303.md)|Argumento da cadeia de caracteres larga inválido para formatar a função|
|[C6305](../code-quality/c6305.md)|Uso incompatível de tamanho e contagem|
|[C6306](../code-quality/c6306.md)|Chamada de função de argumento variável incorreta|
|[C6328](../code-quality/c6328.md)|Incompatibilidade potencial de tipo de argumento|
|[C6385](../code-quality/c6385.md)|Saturação de leitura|
|[C6386](../code-quality/c6386.md)|Saturação de gravação|
|[C6387](../code-quality/c6387.md)|Valor de parâmetro inválido|
|[C6500](../code-quality/c6500.md)|Propriedade de atributo inválida|
|[C6501](../code-quality/c6501.md)|Conflito de valores de propriedades do atributo|
|[C6503](../code-quality/c6503.md)|As referências não podem ser nulas|
|[C6504](../code-quality/c6504.md)|Nulo em não ponteiro|
|[C6505](../code-quality/c6505.md)|MustCheck em nulo|
|[C6506](../code-quality/c6506.md)|Tamanho do buffer em não ponteiro ou matriz|
|[C6508](../code-quality/c6508.md)|Acesso para gravação na constante|
|[C6509](../code-quality/c6509.md)|Retorno usado em pré condição|
|[C6510](../code-quality/c6510.md)|Terminação nula em não ponteiro|
|[C6511](../code-quality/c6511.md)|MustCheck deve ser Sim ou Não|
|[C6513](../code-quality/c6513.md)|Tamanho do elemento sem tamanho do buffer|
|[C6514](../code-quality/c6514.md)|O tamanho do buffer excede o tamanho da matriz|
|[C6515](../code-quality/c6515.md)|Tamanho do buffer em não ponteiro|
|[C6516](../code-quality/c6516.md)|Nenhuma propriedade no atributo|
|[C6517](../code-quality/c6517.md)|Tamanho válido em buffer não legível|
|[C6518](../code-quality/c6518.md)|Tamanho gravável em buffer não gravável|
|[C6522](../code-quality/c6522.md)|Tipo de cadeia de caracteres de tamanho inválido|
|[C6525](../code-quality/c6525.md)|Local inatingível da cadeia de caracteres inválido|
|[C6527](../code-quality/c6527.md)|Anotação inválida: A propriedade 'NeedsRelease' não pode ser utilizada em valores de tipo void|
|[C6530](../code-quality/c6530.md)|Estilo de cadeia de caracteres de formato não reconhecido|
|[C6540](../code-quality/c6540.md)|O uso de anotações de atributo nesta função irá invalidar todas as anotações __declspec existentes na função|
|[C6551](../code-quality/c6551.md)|Especificação de tamanho inválido: expressão não analisável|
|[C6552](../code-quality/c6552.md)|Deref= ou Notref= inválidos: expressão não analisável|
|[C6701](../code-quality/c6701.md)|O valor não é um valor Sim/Não/Talvez válido|
|[C6702](../code-quality/c6702.md)|O valor não é um valor de cadeia de caracteres|
|[C6703](../code-quality/c6703.md)|O valor não é um número|
|[C6704](../code-quality/c6704.md)|Erro de Expressão de Anotação inesperada|
|[C6705](../code-quality/c6705.md)|Número esperado de argumentos para anotação não corresponde ao número de argumentos real para anotação|
|[C6706](../code-quality/c6706.md)|Erro inesperado de anotação para anotação|
|[C26450](../code-quality/c26450.md)|RESULT_OF_ARITHMETIC_OPERATION_PROVABLY_LOSSY|
|[C26451](../code-quality/c26451.md)|RESULT_OF_ARITHMETIC_OPERATION_CAST_TO_LARGER_SIZE|
|[C26452](../code-quality/c26452.md)|SHIFT_COUNT_NEGATIVE_OR_TOO_BIG|
|[C26453](../code-quality/c26453.md)|LEFTSHIFT_NEGATIVE_SIGNED_NUMBER|
|[C26454](../code-quality/c26454.md)|RESULT_OF_ARITHMETIC_OPERATION_NEGATIVE_UNSIGNED|
|[C26495](../code-quality/c26495.md)|MEMBER_UNINIT|
|[C28021](../code-quality/c28021.md)|O parâmetro que está sendo anotado deve ser um ponteiro|
|[C28182](../code-quality/c28182.md)|Desreferenciando ponteiro nulo. O ponteiro contém o mesmo valor NULO que outro ponteiro tinha.|
|[C28202](../code-quality/c28202.md)|Referência inválida para membro não estático|
|[C28203](../code-quality/c28203.md)|Referência ambígua ao membro de classe.|
|[C28205](../code-quality/c28205.md)|\_Sucesso\_ ou \_nos\_falha\_ usado em um contexto ilegal|
|[C28206](../code-quality/c28206.md)|O operando da esquerda aponta para um struct, use '->'|
|[C28207](../code-quality/c28207.md)|O operando da esquerda é um struct, use '.'|
|[C28210](../code-quality/c28210.md)|Anotações para o contexto __on_failure não devem estar no pré-contexto explícito|
|[C28211](../code-quality/c28211.md)|Nome esperado do contexto estático para SAL_context|
|[C28212](../code-quality/c28212.md)|Expressão de ponteiro esperada para anotação|
|[C28213](../code-quality/c28213.md)|O \_uso\_decl\_anotações\_ anotação deve ser usada para fazer referência, sem modificações, uma declaração prévia.|
|[C28214](../code-quality/c28214.md)|Os nomes do parâmetro de atributo devem ser p1...p9|
|[C28215](../code-quality/c28215.md)|O typefix não pode ser aplicado a um parâmetro que já tem um typefix|
|[C28216](../code-quality/c28216.md)|A anotação checkReturn se aplica apenas a pós-condições para o parâmetro da função específica.|
|[C28217](../code-quality/c28217.md)|Para função, o número de parâmetros para anotação não corresponde ao encontrado no arquivo|
|[C28218](../code-quality/c28218.md)|Para o parâmetro de função, o parâmetro da anotação não corresponde ao encontrado no arquivo|
|[C28219](../code-quality/c28219.md)|Membro de enumeração esperada para anotação do parâmetro na anotação|
|[C28220](../code-quality/c28220.md)|Expressão inteira esperada para anotação do parâmetro na anotação|
|[C28221](../code-quality/c28221.md)|Expressão de sequência de caracteres esperada para o parâmetro na anotação|
|[C28222](../code-quality/c28222.md)|__yes, \__no ou \__maybe esperados para anotação|
|[C28223](../code-quality/c28223.md)|O token/identificador esperado para anotação não encontrado, parâmetro|
|[C28224](../code-quality/c28224.md)|Anotação requer parâmetros|
|[C28225](../code-quality/c28225.md)|O número correto de parâmetros necessários na anotação não foi encontrado|
|[C28226](../code-quality/c28226.md)|Anotação não pode ser também um PrimOp (na declaração atual)|
|[C28227](../code-quality/c28227.md)|A anotação não pode ser também um PrimOp (veja a declaração anterior)|
|[C28228](../code-quality/c28228.md)|Parâmetro de anotação: não é possível usar tipo nas anotações|
|[C28229](../code-quality/c28229.md)|A anotação não tem suporte a parâmetros|
|[C28230](../code-quality/c28230.md)|O tipo de parâmetro não tem membro.|
|[C28231](../code-quality/c28231.md)|A anotação só é válida na matriz|
|[C28232](../code-quality/c28232.md)|pre, post ou deref não aplicados a qualquer anotação|
|[C28233](../code-quality/c28233.md)|pre, post ou deref aplicados a um bloco|
|[C28234](../code-quality/c28234.md)|__na expressão não se aplica à função atual|
|[C28235](../code-quality/c28235.md)|A função não pode ser autônoma como uma anotação|
|[C28236](../code-quality/c28236.md)|A anotação não pode ser usada em uma expressão|
|[C28237](../code-quality/c28237.md)|A anotação no parâmetro não é mais suportada|
|[C28238](../code-quality/c28238.md)|A anotação no parâmetro tem mais de um do valor, stringValue e longValue. Utilize paramn=xxx|
|[C28239](../code-quality/c28239.md)|A anotação no parâmetro tem os dois valores, stringValue e longValue; e paramn=xxx. Utilize apenas paramn=xxx|
|[C28240](../code-quality/c28240.md)|A anotação no parâmetro tem param2, mas não tem param1|
|[C28241](../code-quality/c28241.md)|A anotação para função no parâmetro não é reconhecida|
|[C28243](../code-quality/c28243.md)|A anotação para função no parâmetro requer mais desreferências do que o tipo real anotado permite|
|[C28245](../code-quality/c28245.md)|A anotação para função anota 'este' em uma função não membro|
|[C28246](../code-quality/c28246.md)|A anotação do parâmetro para função não corresponde ao tipo do parâmetro|
|[C28250](../code-quality/c28250.md)|Anotação inconsistente para função: a instância anterior tem um erro.|
|[C28251](../code-quality/c28251.md)|Anotação inconsistente para função: esta instância tem um erro.|
|[C28252](../code-quality/c28252.md)|Anotação inconsistente para função: o parâmetro tem outras anotações nesta instância.|
|[C28253](../code-quality/c28253.md)|Anotação inconsistente para função: o parâmetro tem outras anotações nesta instância.|
|[C28254](../code-quality/c28254.md)|dynamic_cast<>() não tem suporte nas anotações|
|[C28262](../code-quality/c28262.md)|Foi encontrado um erro de sintaxe na anotação na função, para anotação|
|[C28263](../code-quality/c28263.md)|Foi encontrado um erro de sintaxe em uma anotação condicional na anotação intrínseca|
|[C28267](../code-quality/c28267.md)|Foi encontrado um erro de sintaxe nas anotações da função.|
|[C28272](../code-quality/c28272.md)|A anotação para função, parâmetro quando examinar for inconsistente com a declaração da função|
|[C28273](../code-quality/c28273.md)|Para função, os indícios são inconsistentes com a declaração da função|
|[C28275](../code-quality/c28275.md)|O parâmetro para \_Macro\_valor\_ é nulo|
|[C28279](../code-quality/c28279.md)|Para símbolo, um 'início' foi encontrado sem um 'fim' correspondente|
|[C28280](../code-quality/c28280.md)|Para símbolo, um 'fim' foi encontrado sem um 'início' correspondente|
|[C28282](../code-quality/c28282.md)|Cadeias de caracteres de formato devem estar em pré-condições|
|[C28285](../code-quality/c28285.md)|Para função, erro de sintaxe no parâmetro|
|[C28286](../code-quality/c28286.md)|Para função, erro de sintaxe perto do fim|
|[C28287](../code-quality/c28287.md)|Para função, erro de sintaxe na \_em\_() anotação (nome de parâmetro não reconhecido)|
|[C28288](../code-quality/c28288.md)|Para função, erro de sintaxe na \_em\_() anotação (nome de parâmetro inválido)|
|[C28289](../code-quality/c28289.md)|Para função: ReadableTo ou WritableTo não tinha uma especificação de limite como parâmetro|
|[C28290](../code-quality/c28290.md)|a anotação para função contém mais Externos que o número real de parâmetros|
|[C28291](../code-quality/c28291.md)|pós null/notnull em deref nível 0 não tem sentido para a função.|
|[C28300](../code-quality/c28300.md)|Operandos da expressão de tipos incompatíveis para o operador|
|[C28301](../code-quality/c28301.md)|Não há anotações para a primeira declaração da função.|
|[C28302](../code-quality/c28302.md)|Um extra \_Deref\_ operador foi encontrado na anotação.|
|[C28303](../code-quality/c28303.md)|Um ambíguo \_Deref\_ operador foi encontrado na anotação.|
|[C28304](../code-quality/c28304.md)|Um posicionado \_Notref\_ operador foi encontrado aplicado ao token.|
|[C28305](../code-quality/c28305.md)|Foi encontrado um erro durante a análise de um token.|
|[C28350](../code-quality/c28350.md)|A anotação descreve uma situação que não é aplicável condicionalmente.|
|[C28351](../code-quality/c28351.md)|A anotação descreve onde um valor dinâmico (uma variável) não pode ser usado na condição.|