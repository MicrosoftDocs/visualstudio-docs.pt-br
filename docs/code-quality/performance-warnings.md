---
title: Avisos de desempenho
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.performancerules
helpviewer_keywords:
- warnings, performance
- performance warnings
- performance, warnings
- managed code analysis warnings, performance warnings
ms.assetid: e014ac3a-02e6-46d9-942c-3491dd63782f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a3fc631a2a99dd6090893393ee20ecec23945713
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814909"
---
# <a name="performance-warnings"></a>Avisos de desempenho
Os avisos de desempenho dão suporte a bibliotecas e aplicativos de alto desempenho.

## <a name="in-this-section"></a>Nesta seção

| Regra | Description |
| - | - |
| [CA1800: Não converta sem necessidade](../code-quality/ca1800.md) | As conversões duplicadas diminui o desempenho, especialmente quando as conversões são realizadas em instruções de iteração compactas. |
| [CA1801: Examinar parâmetros não utilizados](../code-quality/ca1801.md) | Uma assinatura de método inclui um parâmetro que não é usado no corpo do método. |
| [CA1802: Usar literais quando apropriado](../code-quality/ca1802.md) | Um campo é declarado estático e somente leitura (compartilhado e ReadOnly em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ) e é inicializado com um valor que é computáveis no momento da compilação. Como o valor atribuído ao campo de destino é computáveis em tempo de compilação, altere a declaração para um campo const (const in [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ) para que o valor seja calculado em tempo de compilação em vez de em tempo de execução. |
| [CA1804: Remover locais não utilizados](../code-quality/ca1804.md) | As variáveis locais não utilizadas e as atribuições desnecessárias aumentam o tamanho de um assembly e diminuem o desempenho. |
| [CA1805: não inicializar desnecessariamente](../code-quality/ca1805.md) | O tempo de execução do .NET inicializa todos os campos de tipos de referência para seus valores padrão antes de executar o construtor. Na maioria dos casos, a inicialização explícita de um campo para seu valor padrão é redundante, o que aumenta os custos de manutenção e pode prejudicar o desempenho (como com o maior tamanho do assembly). |
| [CA1806: Não ignorar resultados do método](../code-quality/ca1806.md) | Um novo objeto é criado, mas nunca usado, ou um método que cria e retorna uma nova cadeia de caracteres é chamado e a nova cadeia de caracteres nunca é usada ou um método Component Object Model (COM) ou P/Invoke Retorna um HRESULT ou um código de erro que nunca é usado. |
| [CA1809: Evitar locais excessivos](../code-quality/ca1809.md) | Uma otimização de desempenho comum é armazenar um valor em um registro de processador, em vez da memória, algo conhecido como "registro do valor".  Para aumentar a possibilidade de que o registro de todas as variáveis locais seja cancelado, limite o número de variáveis locais a 64. |
| [CA1810: Inicializar campos estáticos de tipo de referência em linha](../code-quality/ca1810.md) | Quando um tipo declara um construtor estático explícito, o compilador JIT (just-in-time) adiciona uma verificação a cada método estático e construtor de instância do tipo para garantir que o construtor estático tenha sido chamado anteriormente. As verificações de construtor estático podem diminuir o desempenho. |
| [CA1811: Evitar código particular não chamado](../code-quality/ca1811.md) | Um membro privado ou interno (no nível do assembly) não tem chamadores no assembly, ele não é invocado pelo Common Language Runtime e não é invocado por um delegado. |
| [CA1812: Evitar classes internas sem instâncias](../code-quality/ca1812.md) | Uma instância de um tipo no nível de assembly não é criada pelo código no assembly. |
| [CA1813: Evitar atributos não selados](../code-quality/ca1813.md) | O .NET fornece métodos para recuperar atributos personalizados. Por padrão, esses métodos pesquisam a hierarquia de herança do atributo. A validação do atributo elimina a pesquisa na hierarquia de herança e pode melhorar o desempenho. |
| [CA1814: Preferir matrizes denteadas a matrizes multidimensionais](../code-quality/ca1814.md) | Uma matriz denteada é uma matriz cujos elementos são matrizes. As matrizes que compõem os elementos podem ser de tamanhos diferentes, o que pode resultar em menos espaço desperdiçado para alguns conjuntos de dados. |
| [CA1815: Substituir equals e o operador equals em tipos de valor](../code-quality/ca1815.md) | Para tipos de valor, a implementação herdada de Equals usa a biblioteca Reflection e compara o conteúdo de todos os campos. Reflection é computacionalmente cara, e pode ser desnecessário comparar a igualdade de cada campo. Se você espera que os usuários comparem ou classifiquem instâncias, ou usem instâncias como chaves de tabela de hash, o tipo de valor deverá implementar Equals. |
| [CA1816: Chamar GC.SuppressFinalize corretamente](../code-quality/ca1816.md) | Um método que é uma implementação de Dispose não chama GC. SuppressFinalize, ou um método que não é uma implementação de Dispose chama GC. SuppressFinalize, ou um método chama GC. SuppressFinalize e passa algo diferente deste (eu em [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] ). |
| [CA1819: Propriedades não devem retornar matrizes](../code-quality/ca1819.md) | As matrizes retornadas por propriedades não são protegidas por gravação, mesmo que a propriedade seja somente leitura. Para manter a matriz à prova de adulteração, a propriedade deve retornar uma cópia da matriz. Normalmente, os usuários não compreenderão as implicações adversas no desempenho de chamar uma propriedade assim. |
| [CA1820: Testar para verificar se há cadeias de caracteres vazias usando o tamanho da cadeia de caracteres](../code-quality/ca1820.md) | A comparação de cadeias de caracteres usando-se a propriedade String.Length ou o método String.IsNullOrEmpty é significativamente mais rápida do que o uso de Equals. |
| [CA1821: Remover finalizadores vazios](../code-quality/ca1821.md) | Sempre que possível, evite finalizadores por conta da sobrecarga adicional no desempenho envolvida no acompanhamento do tempo de vida do objeto. Um finalizador vazio incorre em sobrecarga adicional sem nenhum benefício. |
| [CA1822: Marcar membros como estáticos](../code-quality/ca1822.md) | Os membros que não acessam dados da instância ou os métodos da instância de chamada podem ser marcados como estáticos (Shared no [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]). Depois que você marcar os métodos como estáticos, o compilador emitirá sites de chamada não virtuais para esses membros. Isso pode proporcionar um ganho de desempenho mensurável para o código sensível ao desempenho. |
| [CA1823: Evitar campos particulares não utilizados](../code-quality/ca1823.md) | Foram detectados campos particulares que aparentemente não são acessados no assembly. |
| [CA1824: Marque assemblies com NeutralResourcesLanguageAttribute](../code-quality/ca1824.md) | O atributo NeutralResourcesLanguage informa o ResourceManager da linguagem que foi usada para exibir os recursos de uma cultura neutra para um assembly. Isso melhora o desempenho da pesquisa para o primeiro recurso carregado e pode reduzir o conjunto de trabalho. |
| [CA1825: Evitar alocações de matriz de comprimento zero](../code-quality/ca1825.md) | A inicialização de uma matriz de comprimento zero leva à alocação de memória desnecessária. Em vez disso, use a instância de matriz vazia estaticamente alocada chamando <xref:System.Array.Empty%2A?displayProperty=nameWithType> . A alocação de memória é compartilhada entre todas as invocações desse método. |
| [CA1826: Usar a propriedade em vez do método Linq Enumerable](../code-quality/ca1826.md) | <xref:System.Linq.Enumerable>O método LINQ foi usado em um tipo que dá suporte a uma propriedade equivalente e mais eficiente. |
| [CA1827: Não usar Count/LongCount quando Any puder ser usado](../code-quality/ca1827.md) | <xref:System.Linq.Enumerable.Count%2A>o <xref:System.Linq.Enumerable.LongCount%2A> método or foi usado onde o <xref:System.Linq.Enumerable.Any%2A> método seria mais eficiente. |
| [CA1828: Não usar CountAsync/LongCountAsync quando AnyAsync puder ser usado](../code-quality/ca1828.md) | <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.CountAsync%2A>o <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.LongCountAsync%2A> método or foi usado onde o <xref:Microsoft.EntityFrameworkCore.EntityFrameworkQueryableExtensions.AnyAsync%2A> método seria mais eficiente. |
| [CA1829: Usar a propriedade Length/Count em vez do método Enumerable.Count](../code-quality/ca1829.md) | <xref:System.Linq.Enumerable.Count%2A>O método LINQ foi usado em um tipo que dá suporte a uma propriedade equivalente, mais eficiente `Length` ou `Count` . |
| [CA1830: Preferir os métodos Acrescentar e Inserir fortemente tipados provoca uma sobrecarga no StringBuilder](../code-quality/ca1830.md) | <xref:System.Text.StringBuilder.Append%2A>e <xref:System.Text.StringBuilder.Insert%2A> fornecem sobrecargas para vários tipos além de System. String.  Quando possível, prefira as sobrecargas fortemente tipadas usando ToString () e a sobrecarga baseada em cadeia de caracteres. |
| [CA1831: Usar AsSpan em vez de indexadores baseados em intervalo na cadeia de caracteres quando apropriado](../code-quality/ca1831.md) | Ao usar um indexador de intervalo em uma cadeia de caracteres e atribuir implicitamente o valor a um &lt; tipo de caractere ReadOnlySpan &gt; , o método <xref:System.String.Substring%2A?#System_String_Substring_System_Int32_System_Int32_> será usado em vez de <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> , que produz uma cópia da parte solicitada da cadeia de caracteres. |
| [CA1832: Usar AsSpan ou AsMemory em vez de indexadores baseados em intervalo para obter a parte ReadOnlySpan ou ReadOnlyMemory de uma matriz](../code-quality/ca1832.md) | Ao usar um indexador de intervalo em uma matriz e atribuir implicitamente o valor a um <xref:System.ReadOnlySpan%601> <xref:System.ReadOnlyMemory%601> tipo ou, o método <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> será usado em vez de, o <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> que produzirá uma cópia da parte solicitada da matriz. |
| [CA1833: Usar AsSpan ou AsMemory em vez de indexadores baseados em intervalo para obter a parte Span ou Memory de uma matriz](../code-quality/ca1833.md) | Ao usar um indexador de intervalo em uma matriz e atribuir implicitamente o valor a um <xref:System.Span%601> <xref:System.Memory%601> tipo ou, o método <xref:System.Runtime.CompilerServices.RuntimeHelpers.GetSubArray%2A> será usado em vez de, o <xref:System.Span%601.Slice%2A?#System_Span_1_Slice_System_Int32_System_Int32_> que produzirá uma cópia da parte solicitada da matriz. |
| [CA1835: prefira as sobrecargas baseadas em Memory' para ' ReadAsync ' e ' WriteAsync '](../code-quality/ca1835.md) | ' Stream ' tem uma sobrecarga ' ReadAsync ' que usa um ' byte de memória &lt; &gt; ' como o primeiro argumento e uma sobrecarga ' WriteAsync ' que usa um ' ReadOnlyMemory &lt; byte &gt; ' como o primeiro argumento. Prefira chamar as sobrecargas com base na memória, que são mais eficientes. |
