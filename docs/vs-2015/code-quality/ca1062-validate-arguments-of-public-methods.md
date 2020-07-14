---
title: 'CA1062: validar argumentos de métodos públicos | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
ms.assetid: db1f69ca-68f7-477e-94f3-d135cc5dfcbc
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 377906675d70a712f8ca72b0b6e4d8a6864c1fbc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533231"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062: Validar argumentos de métodos públicos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|Categoria|Microsoft. Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método visível externamente faz referência a um de seus argumentos de referência sem verificar se esse argumento é `null` ( `Nothing` em Visual Basic).

## <a name="rule-description"></a>Descrição da Regra
 Todos os argumentos de referência que são passados para métodos externos visíveis devem ser verificados em relação a `null` . Se apropriado, acione um <xref:System.ArgumentNullException> quando o argumento for `null` .

 Se um método puder ser chamado de um assembly desconhecido porque é declarado público ou protegido, você deve validar todos os parâmetros do método. Se o método for projetado para ser chamado somente por assemblies conhecidos, você deverá tornar o método interno e aplicar o <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> atributo ao assembly que contém o método.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, valide cada argumento de referência em relação a `null` .

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você pode suprimir um aviso dessa regra se tiver certeza de que o parâmetro de referência foi validado por outra chamada de método na função.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método que viola a regra e um método que satisfaz a regra.

 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#1)]
 [!code-csharp[FxCop.Design.ValidateArguments#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#1)]
 [!code-vb[FxCop.Design.ValidateArguments#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#1)]

## <a name="example"></a>Exemplo
 No [!INCLUDE[vsprvslong](../includes/vsprvslong-md.md)] , essa regra não detecta que os parâmetros estão sendo passados para outro método que faz a validação.

 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/fxcop.design.validatearguments.copyctors.cs#2)]
 [!code-csharp[FxCop.Design.ValidateArguments#2](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/cs/FxCop.Design.ValidateArguments.cs#2)]
 [!code-vb[FxCop.Design.ValidateArguments#2](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ValidateArguments/vb/FxCop.Design.ValidateArguments.vb#2)]

## <a name="example"></a>Exemplo
 Os construtores de cópia que populam campos ou propriedades que são objetos de referência também podem violar a regra CA1062. A violação ocorre porque o objeto copiado que é passado para o construtor de cópia pode ser `null` ( `Nothing` em Visual Basic). Para resolver a violação, use um método estático (compartilhado no Visual Basic) para verificar se o objeto copiado não é nulo.

 No exemplo de `Person` classe a seguir, o `other` objeto que é passado para o `Person` Construtor de cópia pode ser `null` .

```

public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor CA1062 fires because other is dereferenced
    // without being checked for null
    public Person(Person other)
        : this(other.Name, other.Age)
    {
    }
}
```

## <a name="example"></a>Exemplo
 No exemplo revisado a seguir `Person` , o `other` objeto que é passado para o construtor de cópia é verificado primeiro para nulo no `PassThroughNonNull` método.

```
public class Person
{
    public string Name { get; private set; }
    public int Age { get; private set; }

    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }

    // Copy constructor
    public Person(Person other)
        : this(PassThroughNonNull(other).Name,
          PassThroughNonNull(other).Age)
    {
    }

    // Null check method
    private static Person PassThroughNonNull(Person person)
    {
        if (person == null)
            throw new ArgumentNullException("person");
        return person;
    }
}
```
