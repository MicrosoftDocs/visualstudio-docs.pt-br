---
title: Conjunto de regras recomendadas nativo
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7aab8c5796a111d90c29e7fa656749adcdf124bd
ms.sourcegitcommit: d705e015cb525bfa87a0b93e93376c3956ec2707
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43225120"
---
# <a name="native-recommended-rules-rule-set"></a>Conjunto de regras recomendadas nativo

A regras nativas recomendadas enfocam os problemas mais críticos e comuns no seu código nativo, inclusive falhas potenciais de segurança e falhas do aplicativo. Você deve incluir este conjunto de regras em qualquer conjunto personalizado que criar para seus projetos nativos.

|Regra|Descrição|
|----------|-----------------|
|[C6001](../code-quality/c6001.md)|Uso de memória não inicializada|
|[C6011](../code-quality/c6011.md)|Desreferenciando ponteiro nulo|
|[C6029](../code-quality/c6029.md)|Uso de valores não marcados|
|[C6031](../code-quality/c6031.md)|Valor de retorno ignorado|
|[C6053](../code-quality/c6053.md)|Terminação em zero da chamada|
|[C6054](../code-quality/c6054.md)|Terminação em zero ausente|
|[C6059](../code-quality/c6059.md)|Concatenação defeituosa|
|[C6063](../code-quality/c6063.md)|Argumento da cadeia de caracteres ausente para formatar função|
|[C6064](../code-quality/c6064.md)|Argumento inteiro ausente para formatar função|
|[C6066](../code-quality/c6066.md)|Argumento de ponteiro ausente para formatar função|
|[C6067](../code-quality/c6067.md)|Argumento de ponteiro de cadeia de caracteres ausente para formatar função|
|[C6101](../code-quality/c6101.md)|Retornando a memória não inicializada|
|[C6200](../code-quality/c6200.md)|O índice excede o máximo do buffer|
|[C6201](../code-quality/c6201.md)|O índice excede o máximo do buffer da pilha|
|[C6214](../code-quality/c6214.md)|Conversão de HRESULT em BOOL inválida|
|[C6215](../code-quality/c6215.md)|Conversão de BOOL em HRESULT inválida|
|[C6216](../code-quality/c6216.md)|Conversão inserida pelo compilador inválida BOOL em HRESULT|
|[C6217](../code-quality/c6217.md)|Teste inválido de HRESULT com NOT|
|[C6220](../code-quality/c6220.md)|Comparação de HRESULT inválido como -1|
|[C6226](../code-quality/c6226.md)|Atribuição de HRESULT inválido como -1|
|[C6230](../code-quality/c6230.md)|Uso inválido de HRESULT como booleano|
|[C6235](../code-quality/c6235.md)|Constante diferente de Zero com lógica- ou|
|[C6236](../code-quality/c6236.md)|Lógica- ou com constante diferente de Zero|
|[C6237](../code-quality/c6237.md)|Zero com lógica- e perde os efeitos colaterais|
|[C6242](../code-quality/c6242.md)|Desenrolamento local forçado|
|[C6248](../code-quality/c6248.md)|Criando DACL nulo|
|[C6250](../code-quality/c6250.md)|Descritores de endereço não liberados|
|[C6255](../code-quality/c6255.md)|Uso desprotegido de Alloca|
|[C6258](../code-quality/c6258.md)|Usando encerrar o Thread|
|[C6259](../code-quality/c6259.md)|Código inativo em bit a bit- ou limitada Switch|
|[C6260](../code-quality/c6260.md)|Uso de aritmética de bytes|
|[C6262](../code-quality/c6262.md)|Uso excessivo de pilha|
|[C6263](../code-quality/c6263.md)|Usando Alloca em Loop|
|[C6268](../code-quality/c6268.md)|Parênteses ausentes em conversão|
|[C6269](../code-quality/c6269.md)|Desreferência de ponteiro ignorado|
|[C6270](../code-quality/c6270.md)|Falta argumento float para formatar a função|
|[C6271](../code-quality/c6271.md)|Argumento extra para formatar função|
|[C6272](../code-quality/c6272.md)|Argumento diferente de float para formatar a função|
|[C6273](../code-quality/c6273.md)|Argumento não inteiro para formatar função|
|[C6274](../code-quality/c6274.md)|Argumento diferente de caractere para formatar a função|
|[C6276](../code-quality/c6276.md)|Conversão de cadeia de caracteres inválida|
|[C6277](../code-quality/c6277.md)|Chamada CreateProcess inválida|
|[C6278](../code-quality/c6278.md)|Incompatibilidade de array-New Scalar-Delete|
|[C6279](../code-quality/c6279.md)|Incompatibilidade de Array-New Scalar-Delete|
|[C6280](../code-quality/c6280.md)|Incompatibilidade de alocação-desalocação de memória|
|[C6281](../code-quality/c6281.md)|Precedência de relação bit a bit|
|[C6282](../code-quality/c6282.md)|Atribuição substitui o teste|
|[C6283](../code-quality/c6283.md)|Incompatibilidade de Array-New Scalar-Delete primitiva|
|[C6284](../code-quality/c6284.md)|Argumento de objeto inválido para formatar a função|
|[C6285](../code-quality/c6285.md)|Lógica- ou de constantes|
|[C6286](../code-quality/c6286.md)|Diferente de Zero lógico- ou perdendo efeitos colaterais|
|[C6287](../code-quality/c6287.md)|Teste redundante|
|[C6288](../code-quality/c6288.md)|Inclusão mútua sobre lógico – e é False|
|[C6289](../code-quality/c6289.md)|Exclusão mútua sobre lógico- ou é verdadeiro|
|[C6290](../code-quality/c6290.md)|Precedência de NOT lógico AND bit a bit|
|[C6291](../code-quality/c6291.md)|Precedência de NOT lógico OR bit a bit|
|[C6292](../code-quality/c6292.md)|Up do máximo de contagens de loops|
|[C6293](../code-quality/c6293.md)|Contagens de loops abaixo do mínimo|
|[C6294](../code-quality/c6294.md)|Corpo do loop nunca executado|
|[C6295](../code-quality/c6295.md)|Loop infinito|
|[C6296](../code-quality/c6296.md)|Loop executado apenas uma vez|
|[C6297](../code-quality/c6297.md)|Resultado do deslocamento de conversão para tamanho maior|
|[C6299](../code-quality/c6299.md)|Campo de bits para comparação booliana|
|[C6302](../code-quality/c6302.md)|Argumento da cadeia de caracteres inválido para formatar a função|
|[C6303](../code-quality/c6303.md)|Argumento da cadeia de caracteres larga inválido para formatar a função|
|[C6305](../code-quality/c6305.md)|Uso incompatível de tamanho e contagem|
|[C6306](../code-quality/c6306.md)|Chamada de função de argumento variável incorreta|
|[C6308](../code-quality/c6308.md)|Vazamento em realocar|
|[C6310](../code-quality/c6310.md)|Constante de filtro de exceção inválida|
|[C6312](../code-quality/c6312.md)|Loop de execução de continuação da exceção|
|[C6314](../code-quality/c6314.md)|Bit a bit- ou precedência|
|[C6317](../code-quality/c6317.md)|Complemento not Not|
|[C6318](../code-quality/c6318.md)|Pesquisa de continuação da exceção|
|[C6319](../code-quality/c6319.md)|Ignorado por vírgula|
|[C6324](../code-quality/c6324.md)|Cópia de cadeia de caracteres em vez de comparação de cadeia de caracteres|
|[C6328](../code-quality/c6328.md)|Incompatibilidade potencial de tipo de argumento|
|[C6331](../code-quality/c6331.md)|Sinalizadores de VirtualFree inválido|
|[C6332](../code-quality/c6332.md)|Parâmetro VirtualFree inválido|
|[C6333](../code-quality/c6333.md)|Tamanho de VirtualFree inválido|
|[C6335](../code-quality/c6335.md)|Vazamento de identificador de processo|
|[C6381](../code-quality/c6381.md)|Informações de desligamento ausentes|
|[C6383](../code-quality/c6383.md)|Bytes de contagem de elementos-contagem de estouro de Buffer|
|[C6384](../code-quality/c6384.md)|Divisão do tamanho do ponteiro|
|[C6385](../code-quality/c6385.md)|Saturação de leitura|
|[C6386](../code-quality/c6386.md)|Saturação de gravação|
|[C6387](../code-quality/c6387.md)|Valor de parâmetro inválido|
|[C6388](../code-quality/c6388.md)|Valor de parâmetro inválido|
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
|[C6995](../code-quality/c6995.md)|Falha ao salvar o arquivo de Log XML|
|[C26100](../code-quality/c26100.md)|Condição de corrida|
|[C26101](../code-quality/c26101.md)|Falha ao usar uma operação sincronizada corretamente|
|[C26110](../code-quality/c26110.md)|Falha do chamador ao manter bloqueio|
|[C26111](../code-quality/c26111.md)|Chamador falhando ao liberar bloqueio|
|[C26112](../code-quality/c26112.md)|Chamador não pode conter qualquer bloqueio|
|[C26115](../code-quality/c26115.md)|Falha ao tentar liberar bloqueio|
|[C26116](../code-quality/c26116.md)|Falha ao adquirir ou manter bloqueio|
|[C26117](../code-quality/c26117.md)|Liberando bloqueio não mantido|
|[C26140](../code-quality/c26140.md)|Erro de anotação do SAL de simultaneidade|
|[C26441](../code-quality/c26441.md)|NO_UNNAMED_GUARDS|
|[C26444](../code-quality/c26444.md)|NO_UNNAMED_RAII_OBJECTS|
|[C26498](../code-quality/c26498.md)|USE_CONSTEXPR_FOR_FUNCTIONCALL|
|[C28020](../code-quality/c28020.md)|A expressão não é verdadeira nesta chamada|
|[C28021](../code-quality/c28021.md)|O parâmetro que está sendo anotado deve ser um ponteiro|
|[C28022](../code-quality/c28022.md)|As classes de função sobre esta função não coincidem com as classes de função no typedef usado para defini-lo.|
|[C28023](../code-quality/c28023.md)|A função que está sendo atribuída ou passada deve ter uma \_função\_classe\_ anotação para pelo menos uma das classes|
|[C28024](../code-quality/c28024.md)|O ponteiro de função que está sendo atribuído é anotado com a classe de função, que não está contida na lista de funções de classe (s).|
|[C28039](../code-quality/c28039.md)|O tipo de parâmetro real deve corresponder exatamente ao tipo|
|[C28112](../code-quality/c28112.md)|Uma variável que pode é acessada por meio de uma função Interlocked sempre deve ser acessada por meio de uma função Interlocked.|
|[C28113](../code-quality/c28113.md)|Acessando uma variável local por meio de uma função sincronizada|
|[C28125](../code-quality/c28125.md)|A função deve ser chamada de dentro de um bloco try / except bloco|
|[C28137](../code-quality/c28137.md)|O argumento variável deve ser uma constante (literal)|
|[C28138](../code-quality/c28138.md)|O argumento constante deve ser variável|
|[C28159](../code-quality/c28159.md)|Considere usar outra função.|
|[C28160](../code-quality/c28160.md)|Anotação de erro|
|[C28163](../code-quality/c28163.md)|A função nunca deve ser chamada de dentro de um bloco try / except bloco|
|[C28164](../code-quality/c28164.md)|O argumento está sendo passado para uma função que espera um ponteiro para um objeto (não um ponteiro para um ponteiro)|
|[C28182](../code-quality/c28182.md)|Desreferenciando ponteiro nulo. O ponteiro contém o mesmo valor NULO que outro ponteiro tinha.|
|[C28183](../code-quality/c28183.md)|O argumento pode ser um valor, e é uma cópia do valor encontrado no ponteiro|
|[C28193](../code-quality/c28193.md)|A variável contém um valor que deve ser examinado|
|[C28196](../code-quality/c28196.md)|O requisito não foi atendido. (A expressão não é avaliada como true.)|
|[C28202](../code-quality/c28202.md)|Referência inválida para membro não estático|
|[C28203](../code-quality/c28203.md)|Referência ambígua ao membro de classe.|
|[C28205](../code-quality/c28205.md)|\_Sucesso\_ ou \_nos\_falha\_ usado em um contexto ilegal|
|[C28206](../code-quality/c28206.md)|O operando da esquerda aponta para um struct, use '->'|
|[C28207](../code-quality/c28207.md)|O operando da esquerda é um struct, use '.'|
|[C28209](../code-quality/c28209.md)|A declaração para símbolo possui uma declaração conflitante|
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
|[C28244](../code-quality/c28244.md)|A anotação para função tem uma anotação de parâmetro/externa não analisável|
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
|[C28306](../code-quality/c28306.md)|A anotação no parâmetro é obsoleta|
|[C28307](../code-quality/c28307.md)|A anotação no parâmetro é obsoleta|
|[C28350](../code-quality/c28350.md)|A anotação descreve uma situação que não é aplicável condicionalmente.|
|[C28351](../code-quality/c28351.md)|A anotação descreve onde um valor dinâmico (uma variável) não pode ser usado na condição.|