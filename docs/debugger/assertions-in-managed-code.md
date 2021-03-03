---
title: Asserções em código gerenciado | Microsoft Docs
description: 'Saiba mais sobre as asserções como uma ferramenta de depuração para código gerenciado em C#, Visual Basic ou F # no Visual Studio.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], assertions in managed code
- Trace.Assert method
- debugging managed code, assertions
- Debug.Assert method
- Debug.Listeners property
- assertions, side effects
- Trace.Listeners property
- assertions, managed code
ms.assetid: 70ab2522-6486-4076-a1a9-e0f11cd0f3a1
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 626f86c2a1d370a7f31e47f86d8adafc3f905672
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684239"
---
# <a name="assertions-in-managed-code"></a>Asserções em código gerenciado
Uma asserção, ou instrução `Assert`, testa uma condição, que você especifica como um argumento para a instrução `Assert`. Se a condição for avaliada para true, nenhuma ação ocorrerá. Se a condição for avaliada como false, haverá falha de asserção. Se você estiver executando com uma compilação de depuração, o programa entrará no modo de interrupção.

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a> Neste tópico
 [Declarações no namespace System. Diagnostics](#BKMK_Asserts_in_the_System_Diagnostics_Namespace)

 [O método Debug. Assert](#BKMK_The_Debug_Assert_method)

 [Efeitos colaterais de Debug. Assert](#BKMK_Side_effects_of_Debug_Assert)

 [Requisitos de rastreamento e depuração](#BKMK_Trace_and_Debug_Requirements)

 [Argumentos Assert](#BKMK_Assert_arguments)

 [Personalizar o comportamento de asserção](#BKMK_Customizing_Assert_behavior)

 [Configurar asserções nos arquivos de configuração](#BKMK_Setting_assertions_in_configuration_files)

## <a name="asserts-in-the-systemdiagnostics-namespace"></a><a name="BKMK_Asserts_in_the_System_Diagnostics_Namespace"></a> Asserções in no namespace System.Diagnostics
 No Visual Basic e Visual C #, você pode usar o método `Assert` de <xref:System.Diagnostics.Debug> ou <xref:System.Diagnostics.Trace>, que estão no namespace <xref:System.Diagnostics>. Os métodos da classe <xref:System.Diagnostics.Debug> não estão incluídos em uma versão de lançamento do programa, portanto, não aumentam o tamanho nem reduzem a velocidade do código da versão.

 C++ não oferece suporte aos métodos da classe <xref:System.Diagnostics.Debug>. Você pode obter o mesmo efeito usando a classe <xref:System.Diagnostics.Trace> com compilação condicional, por exemplo, `#ifdef DEBUG`… `#endif`.

 [Neste tópico](#BKMK_In_this_topic)

## <a name="the-debugassert-method"></a><a name="BKMK_The_Debug_Assert_method"></a> O método Debug.Assert
 Use o método <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> livremente para testar condições que devem resultar em valores verdadeiros se seu código estiver correto. Por exemplo, suponha que você tenha escrito uma função de divisão de inteiros. Pelas regras da matemática, o divisor nunca pode ser zero. Você pode testar isso usando uma asserção:

```VB
Function IntegerDivide(ByVal dividend As Integer, ByVal divisor As Integer) As Integer
    Debug.Assert(divisor <> 0)
    Return CInt(dividend / divisor)
End Function
```

```csharp
int IntegerDivide ( int dividend , int divisor )
{
    Debug.Assert ( divisor != 0 );
    return ( dividend / divisor );
}
```

 Quando você executar esse código no depurador, a instrução de asserção será avaliada, mas, na versão lançada, a comparação não é feita, para não haver sobrecarga adicional.

 Veja a seguir outro exemplo. Você tem uma classe que implementa uma conta corrente, como segue:

```VB
Dim amount, balance As Double
balance = savingsAccount.balance
Debug.Assert(amount <= balance)
SavingsAccount.Withdraw(amount)
```

```csharp
float balance = savingsAccount.Balance;
Debug.Assert ( amount <= balance );
savingsAccount.Withdraw ( amount );
```

 Antes de retirar o dinheiro da conta, você quer garantir que o saldo seja suficiente para cobrir o valor que quer sacar. Você pode escrever uma asserção para verificar o saldo:

```VB
Dim amount, balance As Double
balance = savingsAccount.balance
Trace.Assert(amount <= balance)
SavingsAccount.Withdraw(amount)
```

```csharp
float balance = savingsAccount.Balance;
Trace.Assert ( amount <= balance );
savingsAccount.Withdraw ( amount );
```

 Observe que as chamadas para o método <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> desaparecem quando você cria uma versão de lançamento do código. Isso significa que a chamada que verifica o saldo desaparece na versão de lançamento. Para resolver esse problema, você deverá substituir <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> por <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>, que não desaparece na versão de lançamento:

 As chamadas para <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> adicionam sobrecarga para a versão de lançamento, ao contrário das chamadas para <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>.

 [Neste tópico](#BKMK_In_this_topic)

## <a name="side-effects-of-debugassert"></a><a name="BKMK_Side_effects_of_Debug_Assert"></a> Efeitos colaterais de Debug.Assert
 Quando você usar <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>, verifique se algum código `Assert` interno alterará os resultados do programa se `Assert` for removido. Caso contrário, você poderá acidentalmente introduzir um bug que aparece somente na versão de lançamento do programa. Tenha cuidado especial sobre asserções que contêm chamadas de função ou procedimento, como o exemplo a seguir:

```VB
' unsafe code
Debug.Assert (meas(i) <> 0 )
```

```csharp
// unsafe code
Debug.Assert (meas(i) != 0 );
```

 Este uso de <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> talvez pareça seguro à primeira vista, mas suponhamos que a função meas atualize um contador sempre que for chamada. Quando você compilou a versão de lançamento, essa chamada para meas é eliminada, de modo que o contador não será atualizado. Este é um exemplo de uma função com um efeito colateral. Eliminar uma chamada para uma função que tem efeitos colaterais pode resultar em um bug que aparece somente na versão de lançamento. Para evitar esses problemas, não coloque chamadas de função em uma instrução <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>. Use uma variável temporária em vez disso:

```VB
temp = meas( i )
Debug.Assert (temp <> 0)
```

```csharp
temp = meas( i );
Debug.Assert ( temp != 0 );
```

 Mesmo quando você usa <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>, talvez ainda queira evitar colocar chamadas de função em uma instrução `Assert`. Essas chamadas devem ser seguras, porque as instruções <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> não são eliminadas em uma compilação de lançamento. No entanto, se você evitar construções por uma questão de hábito, será menos provável cometer um erro quando usar <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>.

 [Neste tópico](#BKMK_In_this_topic)

## <a name="trace-and-debug-requirements"></a><a name="BKMK_Trace_and_Debug_Requirements"></a> Requisitos de rastreamento e depuração
 Se você criar seu projeto usando os assistentes do [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)], o símbolo TRACE será definido por padrão nas configurações de lançamento e depuração. O símbolo DEBUG é definido por padrão apenas na compilação de depuração.

 Caso contrário, para que os métodos <xref:System.Diagnostics.Trace> funcionem, o programa deverá ter um dos seguintes na parte superior do arquivo de origem:

- `#Const TRACE = True` no Visual Basic

- `#define TRACE` no Visual C# e C++

  Ou o programa deverá ser compilado com a opção TRACE:

- `/d:TRACE=True` no Visual Basic

- `/d:TRACE` no Visual C# e C++

  Se você precisar usar os métodos de depuração em uma compilação de lançamento do C# ou Visual Basic, deverá definir o símbolo DEBUG na configuração de lançamento.

  C++ não oferece suporte aos métodos da classe <xref:System.Diagnostics.Debug>. Você pode obter o mesmo efeito usando a classe <xref:System.Diagnostics.Trace> com compilação condicional, por exemplo, `#ifdef DEBUG`… `#endif`. Você pode definir esses símbolos na caixa de diálogo **\<Project> páginas de propriedades** . Para obter mais informações, confira [Alterando as configurações de projeto para uma configuração de depuração do Visual Basic](../debugger/project-settings-for-a-visual-basic-debug-configuration.md) ou [Alterando as configurações de projeto para uma configuração de depuração do C ou C++](../debugger/project-settings-for-a-cpp-debug-configuration.md).

## <a name="assert-arguments"></a><a name="BKMK_Assert_arguments"></a> Declarar argumentos
 <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> e <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> utilizam até três argumentos. O primeiro argumento, que é obrigatório, é a condição que você deseja verificar. Se você chamar <xref:System.Diagnostics.Trace.Assert(System.Boolean)?displayProperty=fullName> ou <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=fullName> com apenas um argumento, o método `Assert` verificará a condição e, se o resultado for false, gerará o conteúdo da pilha de chamadas para a janela de **Saída**. O exemplo a seguir mostra <xref:System.Diagnostics.Trace.Assert(System.Boolean)?displayProperty=fullName> e <xref:System.Diagnostics.Debug.Assert(System.Boolean)?displayProperty=fullName>:

```VB
Debug.Assert(stacksize > 0)
Trace.Assert(stacksize > 0)
```

```csharp
Debug.Assert ( stacksize > 0 );
Trace.Assert ( stacksize > 0 );
```

  O segundo e o terceiro argumentos, se houver, devem ser cadeias de caracteres. Se você chamar <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> ou <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName> com dois ou três argumentos, o primeiro será uma condição. O método verifica a condição e, se o resultado for false, gera a segunda e a terceira cadeias de caracteres. O exemplo a seguir mostra <xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String)?displayProperty=fullName> e <xref:System.Diagnostics.Trace.Assert(System.Boolean,System.String)?displayProperty=fullName> usados com dois argumentos:

```VB
Debug.Assert(stacksize > 0, "Out of stack space")
Trace.Assert(stacksize > 0, "Out of stack space")
```

```csharp
Debug.Assert ( stacksize > 0, "Out of stack space" );
Trace.Assert ( stacksize > 0, "Out of stack space" );
```

  O exemplo a seguir mostra <xref:System.Diagnostics.Debug.Assert(System.Boolean,System.String,System.String)?displayProperty=fullName> e é <xref:System.Diagnostics.Trace.Assert(System.Boolean,System.String,System.String)?displayProperty=fullName> usado com três argumentos:

```VB
Debug.Assert(stacksize > 0, "Out of stack space. Bytes left:" , Format(size, "G"))
Trace.Assert(stacksize > 0, "Out of stack space. Bytes left:" , Format(size, "G"))
Trace.Assert(stacksize > 0, "Out of stack space. Bytes left:", "inctemp failed on third call" )
```

```csharp
Debug.Assert ( stacksize > 100, "Out of stack space" , "Failed in inctemp" );
Trace.Assert ( stacksize > 0, "Out of stack space", "Failed in inctemp" );
```

 [Neste tópico](#BKMK_In_this_topic)

## <a name="customizing-assert-behavior"></a><a name="BKMK_Customizing_Assert_behavior"></a> Personalizando o comportamento de declaração
 Se você executar o seu aplicativo no modo de interface do usuário, o método `Assert` exibirá a caixa de diálogo **Falha de Asserção** quando a condição falhar. As ações que ocorrem quando uma asserção falha são controladas pela propriedade <xref:System.Diagnostics.Debug.Listeners%2A> ou <xref:System.Diagnostics.Trace.Listeners%2A>.

 Você pode personalizar o comportamento de saída adicionando um objeto <xref:System.Diagnostics.TraceListener> à coleção de `Listeners`, removendo <xref:System.Diagnostics.TraceListener> da coleção de `Listeners` ou substituindo o método <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName> do `TraceListener` existente para obrigá-lo a se comportar de maneira diferente.

 Por exemplo, você pode substituir o método <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName> para gravar em um log de eventos em vez de exibir a caixa de diálogo **Falha de Asserção**.

 Para personalizar a saída dessa forma, o programa deverá conter um ouvinte e você deverá herdar de <xref:System.Diagnostics.TraceListener> e substituir o método <xref:System.Diagnostics.TraceListener.Fail%2A?displayProperty=fullName>.

 Para obter mais informações, confira [Ouvintes de rastreamento](/dotnet/framework/debug-trace-profile/trace-listeners).

 [Neste tópico](#BKMK_In_this_topic)

## <a name="setting-assertions-in-configuration-files"></a><a name="BKMK_Setting_assertions_in_configuration_files"></a> Definindo asserções em arquivos de configuração
 Você pode definir asserções em seu arquivo de configuração do programa assim como em seu código. Para obter mais informações, consulte <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName> ou <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>.

## <a name="see-also"></a>Confira também

- <xref:System.Diagnostics.Debug.Assert%2A?displayProperty=fullName>
- <xref:System.Diagnostics.Trace.Assert%2A?displayProperty=fullName>
- [Segurança do depurador](../debugger/debugger-security.md)
- [Como rastrear e instrumentar aplicativos](/dotnet/framework/debug-trace-profile/tracing-and-instrumenting-applications)
- [Como: compilar condicionalmente com Trace e Debug](/dotnet/framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug)
- [Tipos de projeto do Visual Basic, C# e F#](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [Depurando código gerenciado](../debugger/debugging-managed-code.md)
