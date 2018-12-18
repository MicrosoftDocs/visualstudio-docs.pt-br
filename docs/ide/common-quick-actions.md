---
title: Ações Rápidas comuns
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 9c6eaa3b776e7a4c4e90795265f94af2d0df994b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894008"
---
# <a name="common-quick-actions"></a>Ações Rápidas comuns

As seções deste tópico listam algumas das **Ações Rápidas** comuns aplicáveis ao código do C# e do Visual Basic. Essas ações são *correções de código* para diagnósticos do compilador ou os [analisadores do .NET Compiler Platform](../code-quality/roslyn-analyzers-overview.md) internos do Visual Studio.

## <a name="actions-that-fix-errors"></a>Ações que corrigem erros

Nesta seção, as Ações Rápidas corrigem erros no código que podem fazer com que um build falhe. Quando as Ações Rápidas estão disponíveis para corrigir um erro em uma linha de código, o ícone exibido na margem ou abaixo do rabisco vermelho é uma lâmpada com um "x" vermelho.

![Ícone de erro e menu das Ações Rápidas](media/error-light-bulb-with-code.png)

### <a name="correct-misspelled-symbol-or-keyword"></a>Corrigir o símbolo ou a palavra-chave incorreta

Se você digitar incorretamente um tipo ou uma palavra-chave no Visual Studio acidentalmente, essa Ação Rápida corrigirá esse erro de forma automática. Você verá esses itens no menu de lâmpada como **"Alterar '*palavra digitada incorretamente*' para '*palavra correta*'**". Por exemplo:

```csharp
// Before
private viod MyMethod()
{
}

// Change 'viod' to 'void'

// After
private void MyMethod()
{
}
```

```vb
' Before
Function MyFunction as Intger
End Function

' Change 'Intger' to 'Integer'

' After
Function MyFunction as Integer
End Function
```

| ID do erro | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS0103, BC30002 | C# e Visual Basic | Visual Studio 2015 Atualização 2 |

### <a name="resolve-git-merge-conflict"></a>Resolver conflitos de mesclagem do git

Estas Ações rápidas permitem resolver conflitos de mesclagem do git "fazendo uma alteração", que remove o código e os marcadores conflitantes.

```csharp
// Before
private void MyMethod()
{
    if (false)
    {

    }
}

// Take changes from 'HEAD'

// After
private void MyMethod()
{
    if (true)
    {

    }
}
```

| ID do erro | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS8300, BC37284 | C# e Visual Basic | Visual Studio 2017 versão 15.3 |

## <a name="actions-that-remove-unnecessary-code"></a>Ações que removem código desnecessário

### <a name="remove-unnecessary-usingsimports"></a>Remover usos/importações desnecessários

A Ação Rápida **Remover Usos/Importações Desnecessários** remove todas as instruções `using` e `Import` não utilizadas do arquivo atual. Ao selecionar esse item, as importações de namespace não utilizadas são removidas.

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# e Visual Basic | Visual Studio 2015 RTW |

### <a name="remove-unnecessary-cast"></a>Remover conversão desnecessária

Se você converter um tipo em outro que não exige uma conversão, o item de Ação Rápida **Remover Conversão Desnecessária** removerá a conversão do código.

```csharp
// before
int number = (int)3;

// Remove Unnecessary Cast

// after
int number = 3;
```

```vb
' Before
Dim number as Integer = CType(3, Integer)

' Remove Unnecessary Cast

' After
Dim number as Integer = 3
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0004 | C# e Visual Basic | Visual Studio 2015 RTW |

### <a name="remove-unused-variables"></a>Remover variáveis não utilizadas

Essa Ação Rápida permite remover variáveis que foram declaradas, mas nunca foram usadas no código.

```csharp
// Before
public MyMethod()
{
    var unused = 8;
    var used = 1;
    return DoStuff(used);
}

// Remove unused variables

// After
public MyMethod()
{
    var used = 1;
    return DoStuff(used);
}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS0219, BC42024 | C# e Visual Basic | Visual Studio 2017 versão 15.3 |

### <a name="remove-type-from-default-value-expression"></a>Remover o tipo da expressão de valor padrão

Esta Ação Rápida remove o tipo de valor de uma expressão de valor padrão e usa o [literal padrão](/dotnet/csharp/programming-guide/statements-expressions-operators/default-value-expressions#default-literal-and-type-inference) quando o compilador pode inferir o tipo da expressão.

```csharp
// Before
void DoWork(CancellationToken cancellationToken = default(CancellationToken)) { ... }

// Simplify default expression

// After
void DoWork(CancellationToken cancellationToken = default) { ... }
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0034 | C# 7.1+ | Visual Studio 2017 versão 15.3 |

## <a name="actions-that-add-missing-code"></a>Ações que adicionam código ausente

### <a name="add-usingsimports-for-types-in-reference-assemblies-nuget-packages-or-other-types-in-your-solution"></a>Adicionar usos/importações para tipos em assemblies de referência, pacotes NuGet ou outros tipos na solução

O uso dos tipos localizados em outros projetos da solução exibirá a Ação Rápida automaticamente. No entanto, as outras precisam ser habilitadas na guia **Ferramentas > Opções > C#** ou **Basic > Avançado**:

- Sugerir usos/importações para tipos em assemblies de referência
- Sugerir usos/importações para tipos em pacotes NuGet

Quando essa opção estiver habilitada, se você usar um tipo em um namespace que não foi importado, mas que existe em um assembly de referência ou pacote NuGet, a instrução de uso/importação será criada.

```csharp
// Before
Debug.WriteLine("Hello");

// using System.Diagnostics;

// After
using System.Diagnostics;

Debug.WriteLine("Hello");
```

```vb
' Before
Debug.WriteLine("Hello")

' Imports System.Diagnostics

// After
Imports System.Diagnostics

Debug.WriteLine("Hello")
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS0103, BC30451 | C# e Visual Basic| Visual Studio 2015 Atualização 2 |

### <a name="add-missing-casesdefault-caseboth"></a>Adicionar maiúsculas e minúsculas ausentes/maiúsculas e minúsculas padrão/ambas

Ao criar uma instrução `switch` no C# ou uma instrução `Select Case` no Visual Basic, é possível usar uma Ação de Código para adicionar automaticamente itens com maiúsculas e minúsculas ausentes, uma instrução com maiúsculas e minúsculas padrão ou ambos.

Considere a seguinte enumeração e a instrução `switch` ou `Select Case` vazia:

```csharp
enum MyEnum
{
    Item1,
    Item2,
    Item3
}

...

MyEnum myEnum = MyEnum.Item1;

switch(myEnum)
{
}
```

```vb
Enum MyEnum
    Item1
    Item2
    Item3
End Enum

...

Dim myEnum as MyEnum = MyEnum.Item1

Select Case myEnum
End Select
```

Ao usar a Ação Rápida **Adicionar Ambos**, os casos que faltam são preenchidos e um caso padrão é adicionado:

```csharp
switch(myEnum)
{
    case MyEnum.Item1:
        break;
    case MyEnum.Item2:
        break;
    case MyEnum.Item3:
        break;
    default:
        break;
}
```

```vb
Select Case myEnum
    Case MyEnum.Item1
        Exit Select
    Case MyEnum.Item2
        Exit Select
    Case Else
        Exit Select
End Select
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0010 | C# e Visual Basic| Visual Studio 2017 versão 15.3 |

### <a name="add-null-checks-for-parameters"></a>Adicionar verificações de null para parâmetros

Essa Ação Rápida permite que você adicione uma verificação ao código para determinar se um parâmetro é nulo.

```csharp
// Before
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty) // cursor inside myProperty
    {
        MyProperty = myProperty;
    }
}

// Add null check

// After
class MyClass
{
    public string MyProperty { get; set; }

    public MyClass(string myProperty)
    {
        MyProperty = myProperty ?? throw new ArgumentNullException(nameof(myProperty));
    }
}
```

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# e Visual Basic| Visual Studio 2017 versão 15.3 |

### <a name="add-argument-name"></a>Adicionar nome do argumento

```csharp
// Before
var date = new DateTime(1997, 7, 8);

// Include argument name 'year' (include trailing arguments)

// After
var date = new DateTime(year: 1997, month: 7, day: 8);
```

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# e Visual Basic| Visual Studio 2017 versão 15.3 |

### <a name="add-braces"></a>Adicionar chaves

A Ação rápida Adicionar chaves insere chaves em torno de instruções `if` de linha única.

```csharp
// Before
if (true)
    return "hello,world";

// Add braces

// After
if (true)
{
    return "hello,world";
}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0011 | C# | Visual Studio 2017 RTW |

### <a name="add-and-order-modifiers"></a>Adicionar e ordenar modificadores

Estas Ações rápidas ajudam a organizar os modificadores, permitindo que você classifique modificadores de acessibilidade existentes e adicione os que estão ausentes.

```csharp
// Before
enum Color
{
    Red, White, Blue
}

// Add accessibility modifiers

// After
internal enum Color
{
    Red, White, Blue
}
```

```csharp
// Before
static private int thisFieldIsPublic;

// Order modifiers

// After
private static int thisFieldIsPublic;
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0036 | C# e Visual Basic| Visual Studio 2017 versão 15.5 |
| IDE0040 | C# e Visual Basic| Visual Studio 2017 versão 15.5 |

## <a name="code-transformations"></a>Transformações de código

### <a name="convert-if-construct-to-switch"></a>Converter construtor 'if' em 'switch'

Essa Ação Rápida permite que você converta um construtor **if-then-else** em um construtor **switch**.

```csharp
// Before
if (obj is string s)
{
  Console.WriteLine("obj is a string: " + s);
}

else if (obj is int i && i > 10)
{
  Console.WriteLine("obj is an int greater than 10");
}

// Convert to switch

// After
switch (obj)
{
  case string s:
    Console.WriteLine("Obj is a string: " + s);
    break;
  case int i when i > 10:
    Console.WriteLine("obj is an int greater than 10");
    break;
}
```

```vb
' Before
If TypeOf obj Is String s Then
    Console.WriteLine("obj is a string: " + s)
Else If TypeOf obj Is Integer i And i > 10 Then
    Console.WriteLine("obj is an int greater than 10")
End If

' Convert to switch

' After
Select Case obj
  Case String s
    Console.WriteLine("Obj is a string: " + s)
    Exit Sub
  Case Integer i when i > 10
    Console.WriteLine("obj is an int greater than 10")
    Exit Sub
End Select
```

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# e Visual Basic| Visual Studio 2017 versão 15.3 |

### <a name="convert-to-interpolated-string"></a>Converter em cadeia de caracteres interpolada

[Cadeias de caracteres interpoladas](/dotnet/csharp/language-reference/keywords/interpolated-strings) são uma maneira fácil de expressar cadeias de caracteres com variáveis inseridas, semelhante ao método **[String.Format](/dotnet/api/system.string.format#overloads)**.  Essa Ação Rápida reconhece maiúsculas e minúsculas nas quais as cadeias de caracteres são concatenadas ou que usam **String.Format** e altera o uso de uma cadeia de caracteres interpolada.

```csharp
// Before
int num = 3;
string s = string.Format("My string with {0} in the middle", num);

// Convert to interpolated string

// After
int num = 3;
string s = $"My string with {num} in the middle";
```

```vb
' Before
Dim num as Integer = 3
Dim s as String = String.Format("My string with {0} in the middle", num)

' Convert to interpolated string

' After
Dim num as Integer = 3
Dim s As String = $"My string with {num} in the middle"
```

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# 6.0+ e Visual Basic 14+ | Visual Studio 2017 RTW |

### <a name="use-object-initializers"></a>Usar inicializadores de objeto

Esta Ação Rápida permite usar [inicializadores de objeto](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers) em vez de invocar o construtor e ter linhas adicionais de instruções de atribuição.

```csharp
// Before
var c = new Customer();
c.Age = 21;

// Object initialization can be simplified

// After
var c = new Customer() { Age = 21 };
```

```vb
' Before
Dim c = New Customer()
c.Age = 21

' Object initialization can be simplified

' After
Dim c = New Customer() With {.Age = 21}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0017 | C# e Visual Basic | Visual Studio 2017 RTW |

### <a name="use-collection-initializers"></a>Usar inicializadores de coleção

Esta Ação rápida permite usar [inicializadores de coleção](/dotnet/csharp/programming-guide/classes-and-structs/object-and-collection-initializers) em vez de múltiplas chamadas ao método `Add` da sua classe.

```csharp
// Before
var list = new List<int>();
list.Add(1);
list.Add(2);
list.Add(3);

// Collection initialization can be simplified

// After
var list = new List<int> { 1, 2, 3 };
```

```vb
' Before
Dim list = New List(Of Integer)
list.Add(1)
list.Add(2)
list.Add(3)

' Collection initialization can be simplified

' After
Dim list = New List(Of Integer) From {1, 2, 3}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0028 | C# e Visual Basic | Visual Studio 2017 RTW |

### <a name="convert-auto-property-to-full-property"></a>Converter a propriedade automática em propriedade completa

Esta Ação rápida permite converter uma propriedade automática em uma propriedade completa e vice-versa.

```csharp
// Before
private int MyProperty { get; set; }

// Convert to full property

// After
private int MyProperty
{
    get { return _myProperty; }
    set { _myProperty = value; }
}
```

```vb
' Before
Public Property Name As String

' Convert to full property

' After
Private _Name As String

Public Property Name As String
    Get
        Return _Name
    End Get
    Set
        _Name = Value
    End Set
End Property
```

| Linguagens Aplicáveis | Versão compatível |
| -------------------- | ---------------- |
| C# e Visual Basic | Visual Studio 2017 versão 15.5 |

### <a name="convert-block-body-to-expression-bodied-member"></a>Converter o corpo do bloco em membro apto para expressão

Esta Ação rápida permite converter corpos do bloco em membros aptos para expressão para métodos, construtores, operadores, propriedades, indexadores e acessadores.

```csharp
//Before
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get { return _myProperty; }
        set
        {
            _myProperty = value;
        }
    }

    public MyClass4(int myProperty)
    {
        MyProperty = myProperty;
    }

    public void PrintProperty()
    {
        Console.WriteLine(MyProperty);
    }
}

// Use expression body for accessors/constructors/methods

// After
class MyClass4
{
    private int _myProperty;

    public int MyProperty
    {
        get => _myProperty;
        set => _myProperty = value;
    }

    public MyClass4(int myProperty) => MyProperty = myProperty;

    public void PrintProperty() => Console.WriteLine(MyProperty);
}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0021-27 | C# 6.0+ | Visual Studio 2017 RTW |

### <a name="convert-anonymous-function-to-local-function"></a>Converter função anônima em função local

Esta Ação rápida converte funções anônimas em funções locais.

```csharp
// Before
Func<int, int> fibonacci = null;
fibonacci = (int n) =>
{
    return n <= 1 ? 1 : fibonacci(n - 1) + fibonacci(n - 2);
};

// Use local function

// After
int fibonacci(int n)
{
    return n <= 1 ? 1 : fibonacci(n-1) + fibonacci(n-2);
}
```

### <a name="convert-referenceequals-to-is-null"></a>Converter 'ReferenceEquals' em 'is null'

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0041 | C# 7.0+ | Visual Studio 2017 versão 15.5 |

Esta Ação rápida sugere o uso de [correspondência de padrões](/dotnet/csharp/pattern-matching) em vez do padrão de codificação ```ReferenceEquals```, sempre que possível.

```csharp
// Before
var value = "someString";
if (object.ReferenceEquals(value, null))
{
    return;
}

// Use 'is null' check

// After
var value = "someString";
if (value is null)
{
    return;
}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0039 | C# 7.0+ | Visual Studio 2017 versão 15.5 |

### <a name="introduce-pattern-matching"></a>Introduzir a correspondência de padrões

Esta Ação rápida sugere o uso da [correspondência de padrões](/dotnet/csharp/pattern-matching) com conversões e verificações nulas em C#.

```csharp
// Before
if (o is int)
{
    var i = (int)o;
    ...
}

// Use pattern matching

// After
if (o is int i)
{
    ...
}
```

```csharp
// Before
var s = o as string;
if (s != null)
{
    ...
}

// Use pattern matching

// After
if (o is string s)
{
    ...
}
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0020 | C# 7.0+ | Visual Studio 2017 RTW |
| IDE0019 | C# 7.0+ | Visual Studio 2017 RTW |

### <a name="change-base-for-numeric-literals"></a>Alterar base para literais numéricas

Essa Ação Rápida permite que você converta um literal numérico de um sistema numérico base para outro. Por exemplo, você pode alterar um número para hexadecimal ou formato binário.

```csharp
// Before
int countdown = 2097152;

// Convert to hex

// After
int countdown = 0x200000;
```

```vb
' Before
Dim countdown As Integer = 2097152

' Convert to hex

' After
Dim countdown As Integer = &H200000
```

| Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| C# 7.0+ e Visual Basic 14+ | Visual Studio 2017 versão 15.3 |

### <a name="insert-digit-separators-into-literals"></a>Inserir separadores de dígitos em literais

Essa Ação Rápida permite que você adicione caracteres separadores em valores literais.

```csharp
// Before
int countdown = 1000000;

// Separate thousands

// After
int countdown = 1_000_000;
```

```vb
' Before
Dim countdown As Integer = 1000000

' Separate thousands

' After
Dim countdown As Integer = 1_000_000
```

| Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| C# 7.0+ e Visual Basic 14+ | Visual Studio 2017 versão 15.3 |

### <a name="use-explicit-tuple-names"></a>Usar nomes de tupla explícita

Esta Ação rápida identifica áreas em que o nome da tupla explícita pode ser usado em vez de Item1, Item2, etc.

```csharp
// Before
(string name, int age) customer = GetCustomer();
var name = customer.Item1;

// Use explicit tuple name

// After
(string name, int age) customer = GetCustomer();
var name = customer.name;
```

```vb
' Before
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.Item1

' Use explicit tuple name

' After
Dim customer As (name As String, age As Integer) = GetCustomer()
Dim name = customer.name
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0033 | C# 7.0+ e Visual Basic 15+ | Visual Studio 2017 RTW |

### <a name="use-inferred-names"></a>Usar nomes inferidos

Esta Ação Rápida destaca quando o código pode ser simplificado para usar nomes de membros inferidos em tipos anônimos ou nomes de elemento inferidos em tuplas.

```csharp
// Before
var anon = new { age = age, name = name };

// Use inferred member name

// After
var anon = new { age, name };
```

```csharp
// Before
var tuple = (age: age, name: name);

// Use inferred tuple element name

// After
var tuple = (age, name);
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0037 | C# | Visual Studio 2017 v. 15.5 |
| IDE0037 | C# 7.1+ | Visual Studio 2017 v. 15.5 |

### <a name="deconstruct-tuple-declaration"></a>Desconstruir declaração de tupla

Esta Ação Rápida permite desconstruir declarações de variável de tupla.

```csharp
// Before
var person = GetPersonTuple();
Console.WriteLine($"{person.name} {person.age}");

(int x, int y) point = GetPointTuple();
Console.WriteLine($"{point.x} {point.y}");

//Deconstruct variable declaration

// After
var (name, age) = GetPersonTuple();
Console.WriteLine($"{name} {age}");

(int x, int y) = GetPointTuple();
Console.WriteLine($"{x} {y}");
```

| ID do diagnóstico | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| IDE0042 | C# 7.0+ | Visual Studio 2017 v. 15.5 |

### <a name="make-method-synchronous"></a>Tornar o método síncrono

Ao usar a palavra-chave `async` ou `Async` em um método, espera-se que, dentro desse método a palavra-chave `await` ou `Await` também seja usada. No entanto, se esse não é o caso, é exibida uma Ação Rápida que torna o método síncrono removendo a palavra-chave `async` ou `Async` e alterando o tipo de retorno. Use a opção **Tornar o método síncrono** do menu Ações Rápidas.

```csharp
// Before
async Task<int> MyAsyncMethod()
{
    return 3;
}

// Make method synchronous

// After
int MyAsyncMethod()
{
    return 3;
}
```

```vb
' Before
Async Function MyAsyncMethod() As Task(Of Integer)
    Return 3
End Function

' Make method synchronous

' After
Function MyAsyncMethod() As Integer
    Return 3
End Function
```

| ID do erro | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS1998, BC42356 | C# e Visual Basic | Visual Studio 2015 Atualização 2 |

### <a name="make-method-asynchronous"></a>Tornar o método assíncrono

Ao usar a palavra-chave `await` ou `Await` em um método, espera-se que o próprio método seja marcado com a palavra-chave `async` ou `Async`. No entanto, se esse não for o caso, é exibida uma Ação Rápida que torna o método assíncrono. Use a opção **Tornar o método ou a função síncrona** do menu Ações Rápidas.

```csharp
// Before
int MyAsyncMethod()
{
    return await Task.Run(...);
}

// Make method asynchronous

// After
async Task<int> MyAsyncMethod()
{
    return await Task.Run(...);
}
```

```vb
' Before
Function MyAsyncMethod() as Integer
    Return  Await Task.Run(...)
End Function

' Make method asynchronous

' After
Async Function MyAsyncMethod() As Task(Of Integer)
    Return Await Task.Run(...)
End Function
```

| ID do erro | Linguagens Aplicáveis | Versão compatível |
| ------- | -------------------- | ---------------- |
| CS4032, BC37057 | C# e Visual Basic | Visual Studio 2017 |

## <a name="see-also"></a>Consulte também

- [Ações rápidas](../ide/quick-actions.md)
