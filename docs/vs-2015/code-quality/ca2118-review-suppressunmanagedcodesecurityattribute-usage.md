---
title: 'CA2118: examinar o uso do SuppressUnmanagedCodeSecurityAttribute | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2118
- ReviewSuppressUnmanagedCodeSecurityUsage
helpviewer_keywords:
- ReviewSuppressUnmanagedCodeSecurityUsage
- CA2118
ms.assetid: 4cb8d2fc-4e44-4dc3-9b74-7f5838827d41
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: bc0e88265245d795697d32a9e6a95909c0415259
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538652"
---
# <a name="ca2118-review-suppressunmanagedcodesecurityattribute-usage"></a>CA2118: Examinar o uso de SuppressUnmanagedCodeSecurityAttribute
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewSuppressUnmanagedCodeSecurityUsage|
|CheckId|CA2118|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo ou membro público ou protegido tem o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> atributo.

## <a name="rule-description"></a>Descrição da Regra
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>altera o comportamento padrão do sistema de segurança para membros que executam código não gerenciado usando a interoperabilidade de COM ou a invocação de plataforma. Geralmente, o sistema cria [dados e modelando](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) a permissão de código não gerenciado. Essa demanda ocorre em tempo de execução para cada invocação do membro e verifica a permissão de cada chamador na pilha de chamadas. Quando o atributo está presente, o sistema faz uma [demanda de link](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d) para a permissão: as permissões do chamador imediato são verificadas quando o chamador é compilado em JIT.

 Esse atributo é usado principalmente para aumentar o desempenho; no entanto, os ganhos de desempenho acompanham riscos de segurança significativos. Se você posicionar o atributo em membros públicos que chamam métodos nativos, os chamadores na pilha de chamadas (além do chamador imediato) não precisarão de permissão de código não gerenciado para executar código não gerenciado. Dependendo das ações do membro público e da manipulação de entrada, ele pode permitir que chamadores não confiáveis acessem a funcionalidade normalmente restrita ao código confiável.

 O [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] se baseia nas verificações de segurança para impedir que os chamadores obtenham acesso direto ao espaço de endereço do processo atual. Como esse atributo ignora a segurança normal, seu código representa uma ameaça séria se puder ser usado para ler ou gravar na memória do processo. Observe que o risco não está limitado aos métodos que intencionalmente fornecem acesso para processar a memória; Ele também está presente em qualquer cenário em que o código mal-intencionado possa obter acesso por qualquer meio, por exemplo, fornecendo entradas surpreendentes, malformadas ou inválidas.

 A política de segurança padrão não concede permissão de código não gerenciado a um assembly, a menos que ele esteja sendo executado do computador local ou seja membro de um dos seguintes grupos:

- Grupo de códigos de zona Meu Computador

- Grupo de códigos de nome forte da Microsoft

- Grupo de códigos de nome forte ECMA

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Examine atentamente seu código para garantir que esse atributo seja absolutamente necessário. Se você não estiver familiarizado com a segurança de código gerenciado ou não entender as implicações de segurança do uso desse atributo, remova-o do seu código. Se o atributo for necessário, você deve garantir que os chamadores não possam usar seu código de forma mal-intencionada. Se seu código não tiver permissão para executar código não gerenciado, esse atributo não terá nenhum efeito e deverá ser removido.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Para suprimir um aviso dessa regra com segurança, você deve garantir que o código não forneça acesso de chamadores a operações nativas ou recursos que possam ser usados de maneira destrutiva.

## <a name="example"></a>Exemplo
 O exemplo a seguir viola a regra.

 [!code-csharp[FxCop.Security.TypesDoNotSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypesDoNotSuppress/cs/FxCop.Security.TypesDoNotSuppress.cs#1)]

## <a name="example"></a>Exemplo
 No exemplo a seguir, o `DoWork` método fornece um caminho de código publicamente acessível para o método de invocação de plataforma `FormatHardDisk` .

 [!code-csharp[FxCop.Security.PInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PInvokeAndSuppress/cs/FxCop.Security.PInvokeAndSuppress.cs#1)]

## <a name="example"></a>Exemplo
 No exemplo a seguir, o método público `DoDangerousThing` causa uma violação. Para resolver a violação, `DoDangerousThing` deve se tornar particular, e o acesso a ela deve ser por meio de um método público protegido por uma demanda de segurança, conforme ilustrado pelo `DoWork` método.

 [!code-csharp[FxCop.Security.TypeInvokeAndSuppress#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TypeInvokeAndSuppress/cs/FxCop.Security.TypeInvokeAndSuppress.cs#1)]

## <a name="see-also"></a>Consulte Também
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>[Diretrizes de codificação seguras](https://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) [otimizações de segurança](https://msdn.microsoft.com/cf255069-d85d-4de3-914a-e4625215a7c0) [e requisitos de link de modelagem](https://msdn.microsoft.com/library/8c37635d-e2c1-4b64-a258-61d9e87405e6) [Link Demands](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
