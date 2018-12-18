---
title: Usando o atributo DebuggerTypeProxy | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- attributes [C#], debugger
- DebuggerTypeProxyAttribute class
- DebuggerTypeProxy attribute
ms.assetid: 943f3bb1-993e-4800-a47e-0af78b063014
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ab54c754fdc3b7ae773e71a96936a1c17c6bc5ce
ms.sourcegitcommit: 9571742f4a808c75b1034aa72fc24b54bc50692e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49411060"
---
# <a name="using-debuggertypeproxy-attribute"></a>Usando o atributo DebuggerTypeProxy

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> especifica um proxy, ou substituto, para um tipo e altera a maneira como o tipo é exibido nas janelas do depurador. Quando você exibe uma variável que possui um proxy, o proxy substitui o tipo original na **exibir**. A janela de variáveis do depurador exibe apenas os membros públicos do tipo de proxy. Os membros particulares não são exibidos.

Esse atributo poderá ser aplicado a:

- Estruturas
- Classes
- Assemblies

Uma classe de proxy de tipo deve ter um construtor que usa um argumento do tipo que o proxy substituirá. O depurador cria uma nova instância da classe de proxy de tipo sempre que precisa exibir uma variável do tipo de destino. Isso pode ter implicações de desempenho. Como resultado, você não deve fazer mais trabalho no construtor do que o que for absolutamente necessário.

Para minimizar penalidades de desempenho, o avaliador de expressão não examina os atributos no proxy de exibição do tipo a menos que o tipo seja expandido pelo clique do usuário no símbolo + na janela do depurador ou pelo uso de <xref:System.Diagnostics.DebuggerBrowsableAttribute>. Consequentemente, você não deverá colocar os atributos no próprio tipo de exibição. Os atributos podem e devem ser usados no corpo do tipo de exibição.

É uma boa ideia para o proxy do tipo ser uma classe aninhada particular dentro da classe a que o atributo se destina. Isso permite acessar membros internos com facilidade.

<xref:System.Diagnostics.DebuggerTypeProxyAttribute> podem ser herdadas, portanto, se um tipo proxy for especificado em uma classe base será aplicada a quaisquer classes derivadas, a menos que essas classes derivadas especifiquem seu próprio tipo proxy.

Se <xref:System.Diagnostics.DebuggerTypeProxyAttribute> for usado no nível de assembly, o parâmetro `Target` especificará o tipo que o proxy substituirá.

Para obter um exemplo de como usar esse atributo junto com <xref:System.Diagnostics.DebuggerDisplayAttribute> e <xref:System.Diagnostics.DebuggerTypeProxyAttribute>, consulte[usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md).

## <a name="using-generics-with-debuggertypeproxy"></a>Usando genéricos com DebuggerTypeProxy

O suporte para genéricos é limitado. Para C#, o `DebuggerTypeProxy` oferece suporte apenas a tipos abertos. Um tipo aberto, também chamada de um tipo não construído, é um tipo genérico que não foi instanciado com argumentos para seus parâmetros de tipo. Os tipos fechados, também chamados de tipos construídos, não têm suporte.

A sintaxe para um tipo aberto é semelhante ao seguinte:

`Namespace.TypeName<,>`

Se você usar um tipo genérico como um destino em `DebuggerTypeProxy`, deverá usar essa sintaxe. O mecanismo `DebuggerTypeProxy` infere os parâmetros de tipo para você.

Para obter mais informações sobre tipos abertos e fechados no c#, consulte a [especificação da linguagem c#](/dotnet/csharp/language-reference/language-specification), abra a seção 20.5.2 e fechado tipos.

O Visual Basic não tem sintaxe de tipo aberto; portanto, você não pode fazer a mesma coisa no Visual Basic. Em vez disso, você deverá usar uma representação de cadeia de caracteres do nome do tipo aberto.

`"Namespace.TypeName'2"`

## <a name="see-also"></a>Consulte também

- [Usando o atributo DebuggerDisplay](../debugger/using-the-debuggerdisplay-attribute.md)
- [Criar exibições personalizadas de objetos gerenciados](../debugger/create-custom-views-of-dot-managed-objects.md)
- [Aprimorando a depuração com os atributos de exibição do depurador](/dotnet/framework/debug-trace-profile/enhancing-debugging-with-the-debugger-display-attributes)
