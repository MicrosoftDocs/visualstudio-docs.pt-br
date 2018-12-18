---
title: 'CA1062: validar argumentos de métodos públicos'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
- Validate arguments of public methods
helpviewer_keywords:
- CA1062
- ValidateArgumentsOfPublicMethods
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c5894eaf321204ace98a55a3d08411d61207ff7c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857556"
---
# <a name="ca1062-validate-arguments-of-public-methods"></a>CA1062: validar argumentos de métodos públicos

|||
|-|-|
|NomeDoTipo|ValidateArgumentsOfPublicMethods|
|CheckId|CA1062|
|Categoria|Microsoft.Design|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Um método visível externamente desreferencia um de seus argumentos de referência sem verificar se esse argumento é `null` (`Nothing` no Visual Basic).

## <a name="rule-description"></a>Descrição da regra

Todos os argumentos de referência que são passados para métodos externamente visíveis devem ser verificados em relação a `null`. Se apropriado, lance uma <xref:System.ArgumentNullException> quando o argumento é `null`.

Se um método pode ser chamado de um assembly desconhecido porque está declarado como público ou protegido, você deve validar todos os parâmetros do método. Se o método foi projetado para ser chamado apenas por assemblies conhecidos, você deve tornar o método interno e aplicar o <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute> atributo ao assembly que contém o método.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Para corrigir uma violação dessa regra, validar cada argumento de referência em relação a `null`.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Se você tiver certeza de que o parâmetro deferência foi validado por outra chamada de método na função, você pode suprimir um aviso nessa regra.

## <a name="example"></a>Exemplo

O exemplo a seguir mostra um método que viola a regra e um método que satisfaz a regra.

 ```csharp
 using System;

namespace DesignLibrary
{
    public class Test
    {
        // This method violates the rule.
        public void DoNotValidate(string input)
        {
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }

        // This method satisfies the rule.
        public void Validate(string input)
        {
            if (input == null)
            {
                throw new ArgumentNullException("input");
            }
            if (input.Length != 0)
            {
                Console.WriteLine(input);
            }
        }
    }
}
```

```vb
Imports System

Namespace DesignLibrary

    Public Class Test

        ' This method violates the rule.
        Sub DoNotValidate(ByVal input As String)

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

        ' This method satisfies the rule.
        Sub Validate(ByVal input As String)

            If input Is Nothing Then
                Throw New ArgumentNullException("input")
            End If

            If input.Length <> 0 Then
                Console.WriteLine(input)
            End If

        End Sub

    End Class

End Namespace
```

## <a name="example"></a>Exemplo

Construtores de cópia que preencher campos ou propriedades que são objetos de referência também podem violar a regra de CA1062. A violação ocorre porque o objeto copiado que é passado para o construtor de cópia pode ser `null` (`Nothing` no Visual Basic). Para resolver a violação, use um método estático (compartilhado no Visual Basic) para verificar se o objeto copiado não é nulo.

A seguir `Person` exemplo de classe, o `other` objeto é passado para o `Person` construtor de cópia pode ser `null`.

```csharp
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

A seguir revisado `Person` exemplo, o `other` objeto é passado para o construtor de cópia primeiro é verificado para null no `PassThroughNonNull` método.

```csharp
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