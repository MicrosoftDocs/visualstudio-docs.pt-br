---
title: Avisos de confiabilidade
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.reliabilityrules
helpviewer_keywords:
- warnings, reliability
- reliability warnings
- managed code analysis warnings, reliability warnings
ms.assetid: 77886846-10a2-4585-968a-7eb60ebe07e8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 095631abc5678a27a4e79611433ff446337b956c
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835609"
---
# <a name="reliability-warnings"></a>Avisos de confiabilidade

Os avisos de confiabilidade dão suporte à biblioteca e confiabilidade do aplicativo, como a memória correta e o uso do thread. As regras de confiabilidade incluem:

|Regra|Descrição|
|----------|-----------------|
|[CA2000: Descartar objetos antes de perder o escopo](../code-quality/ca2000.md)|Como pode ocorrer um evento excepcional que impedirá a execução do finalizador de um objeto, o objeto deve ser explicitamente descartado antes que todas as referências a ele estejam fora do escopo.|
|[CA2001: Evitar chamar métodos problemáticos](../code-quality/ca2001.md)|Um membro chama um método potencialmente perigoso ou problemático.|
|[CA2002: Não bloquear objetos com identidade fraca](../code-quality/ca2002.md)|Diz-se que um objeto tem uma identidade fraca quando puder ser acessado diretamente em todos os limites de domínio do aplicativo. Um thread que tente adquirir um bloqueio em um objeto com uma identidade fraca pode ser bloqueado por um segundo thread em um domínio de aplicativo diferente com um bloqueio no mesmo objeto.|
|[CA2003: Não tratar fibras como threads](../code-quality/ca2003.md)|Um thread gerenciado está sendo tratado como um Thread Win32.|
|[CA2004: Remover as chamadas a GC.KeepAlive](../code-quality/ca2004.md)|Se você estiver convertendo para uso de SafeHandle, remova todas as chamadas para GC. KeepAlive (objeto). Nesse caso, as classes não devem ter que chamar GC. KeepAlive, supondo que eles não tenham um finalizador, mas dependem de SafeHandle para finalizar o identificador do sistema operacional para eles.|
|[CA2006: Usar SafeHandle para encapsular recursos nativos](../code-quality/ca2006.md)|O uso de IntPtr em código gerenciado pode indicar um problema de segurança e confiabilidade em potencial. Todos os usos de IntPtr devem ser examinados para determinar se o uso de um SafeHandle, ou tecnologia semelhante, é necessário em seu lugar.|
|[CA2007: não aguardar diretamente uma tarefa](../code-quality/ca2007.md)|Um método assíncrono [aguarda](/dotnet/csharp/language-reference/keywords/await) um <xref:System.Threading.Tasks.Task> diretamente.|
|[CA2009: Não chamar ToImmutableCollection em um valor ImmutableCollection](../code-quality/ca2009.md)|`ToImmutable`o método não era necessariamente chamado em uma coleção imutável do <xref:System.Collections.Immutable> namespace.|
|[CA2011: Não atribuir a propriedade em seu próprio setter](../code-quality/ca2011.md) | Uma propriedade recebeu acidentalmente um valor dentro de seu próprio [acessador set](/dotnet/csharp/programming-guide/classes-and-structs/using-properties#the-set-accessor). |
|[CA2012: Usar ValueTasks corretamente](../code-quality/ca2012.md) | ValueTasks retornados de invocações de membro devem ser diretamente aguardados.  Tenta consumir um ValueTask várias vezes ou para acessar diretamente um resultado antes que seja conhecido a ser concluído pode resultar em uma exceção ou corrupção.  Ignorar essa ValueTask é provavelmente uma indicação de um bug funcional e pode prejudicar o desempenho. |
|[CA2013: Não usar ReferenceEquals com tipos de valor](../code-quality/ca2013.md) | Ao comparar valores usando <xref:System.Object.ReferenceEquals%2A?displayProperty=fullName> , se objA e objB forem tipos de valor, eles estarão em caixa antes de serem passados para o <xref:System.Object.ReferenceEquals%2A> método. Isso significa que, mesmo que objA e objB representem a mesma instância de um tipo de valor, o método, no <xref:System.Object.ReferenceEquals%2A> entanto, retorna false. |
|[CA2014: não use stackalloc em loops.](../code-quality/ca2014.md) | O espaço de pilha alocado por um stackalloc é liberado apenas no final da invocação do método atual.  Usá-lo em um loop pode resultar em aumento de pilha não associado e condições de estouro de pilha eventual. |
|[CA2015: não definir finalizadores para tipos derivados de MemoryManager &lt; T&gt;](../code-quality/ca2015.md) | Adicionar um finalizador a um tipo derivado de <xref:System.Buffers.MemoryManager%601> pode permitir que a memória seja liberada enquanto ainda estiver em uso por um <xref:System.Span%601> . |
|[CA2016: encaminhe o parâmetro CancellationToken para métodos que usam um](ca2016.md) | Encaminhe o `CancellationToken` parâmetro para os métodos que usam um para garantir que as notificações de cancelamento da operação sejam propagadas corretamente ou repassem `CancellationToken.None` explicitamente para indicar, de forma intencional, não a propagação do token. |
