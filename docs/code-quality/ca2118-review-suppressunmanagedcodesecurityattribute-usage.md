---
title: 'CA2118: revisar uso de SuppressUnmanagedCodeSecurityAttribute'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2118
- ReviewSuppressUnmanagedCodeSecurityUsage
helpviewer_keywords:
- ReviewSuppressUnmanagedCodeSecurityUsage
- CA2118
ms.assetid: 4cb8d2fc-4e44-4dc3-9b74-7f5838827d41
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- cplusplus
ms.openlocfilehash: 900abe516ebd07cf5a8849f269f915623500731e
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859699"
---
# <a name="ca2118-review-suppressunmanagedcodesecurityattribute-usage"></a>CA2118: revisar uso de SuppressUnmanagedCodeSecurityAttribute

|||
|-|-|
|NomeDoTipo|ReviewSuppressUnmanagedCodeSecurityUsage|
|CheckId|CA2118|
|Categoria|Microsoft.Security|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um tipo público ou protegido ou membro tem o <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName> atributo.

## <a name="rule-description"></a>Descrição da regra
 <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute> Altera o comportamento do sistema de segurança padrão para membros que executem código não gerenciado usando invocação de plataforma ou interoperabilidade de COM. Em geral, o sistema faz uma [dados e modelagem](/dotnet/framework/data/index) para permissão de código não gerenciado. Essa demanda ocorre em tempo de execução para cada invocação do membro e verifica todos os chamadores na pilha de chamadas para a permissão. Quando o atributo estiver presente, o sistema faz uma [demandas de Link](/dotnet/framework/misc/link-demands) para a permissão: as permissões do chamador imediato são verificadas quando o chamador é compilado por JIT.

 Esse atributo é usado principalmente para aumentar o desempenho; no entanto, os ganhos de desempenho acompanham riscos de segurança significativos. Se você colocar o atributo em membros públicos que chamam métodos nativos, os chamadores na pilha de chamadas (que não seja o chamador imediato) precisa de permissão de código não gerenciado para executar código não gerenciado. Dependendo do membro público ações e manipulação de entrada, ele pode permitir que os chamadores não confiáveis para acessar a funcionalidade normalmente restringido ao código confiável.

 O .NET Framework se baseia em verificações de segurança para impedir que os chamadores tenham acesso direto ao espaço de endereço do processo atual. Como esse atributo ignora a segurança normal, seu código representa uma ameaça grave se ele pode ser usado para ler ou gravar na memória do processo. Observe que não é limitado a métodos que intencionalmente fornecem acesso para processar a memória; o risco Ele também está presente em qualquer cenário em que código mal-intencionado pode obter o acesso por qualquer meio, por exemplo, fornecendo entrada surpreendente, malformada ou inválida.

 A política de segurança padrão não concede permissão de código não gerenciado a um assembly, a menos que ele está em execução no computador local ou é um membro de um dos seguintes grupos:

- Grupo de códigos de zona Meu computador

- Grupo de códigos do Microsoft forte nome

- Grupo de códigos do ECMA forte nome

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Examine cuidadosamente o código para garantir que esse atributo é absolutamente necessário. Se você não estiver familiarizado com a segurança do código gerenciado ou não compreende as implicações de segurança de usar esse atributo, remova-o do seu código. Se o atributo for necessário, você deve garantir que os chamadores não é possível usar seu código maliciosamente. Se seu código não tem permissão para executar código não gerenciado, esse atributo não tem nenhum efeito e deve ser removido.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Para suprimir com segurança um aviso nessa regra, você deve garantir que seu código não fornece os chamadores acesso a operações nativas ou recursos que podem ser usados de forma destrutivas.

## <a name="example-1"></a>Exemplo 1
 O exemplo a seguir viola a regra.

 [!code-csharp[FxCop.Security.TypesDoNotSuppress#1](../code-quality/codesnippet/CSharp/ca2118-review-suppressunmanagedcodesecurityattribute-usage_1.cs)]

## <a name="example-2"></a>Exemplo 2
 No exemplo a seguir, o `DoWork` método fornece um caminho de código publicamente acessível para o método de invocação de plataforma `FormatHardDisk`.

 [!code-csharp[FxCop.Security.PInvokeAndSuppress#1](../code-quality/codesnippet/CSharp/ca2118-review-suppressunmanagedcodesecurityattribute-usage_2.cs)]

## <a name="example-3"></a>Exemplo 3:
 No exemplo a seguir, o método público `DoDangerousThing` faz com que uma violação. Para resolver a violação `DoDangerousThing` deve ser feito particular e acesso a ele deve ser por meio de um método público, protegido por uma exigência de segurança, conforme ilustrado pelo `DoWork` método.

 [!code-csharp[FxCop.Security.TypeInvokeAndSuppress#1](../code-quality/codesnippet/CSharp/ca2118-review-suppressunmanagedcodesecurityattribute-usage_3.cs)]

## <a name="see-also"></a>Consulte também

- <xref:System.Security.SuppressUnmanagedCodeSecurityAttribute?displayProperty=fullName>
- [Diretrizes de codificação segura](/dotnet/standard/security/secure-coding-guidelines)
- [Dados e modelagem](/dotnet/framework/data/index)
- [Demandas de link](/dotnet/framework/misc/link-demands)