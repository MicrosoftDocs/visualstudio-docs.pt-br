---
title: Usando shims para isolar seu aplicativo para teste de unidade no Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: c1a6a15a5c5ba0eccfdab89461292fba484b5af3
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389063"
---
# <a name="use-shims-to-isolate-your-application-from-other-assemblies-for-unit-testing"></a>Usar shims para isolar seu aplicativo de outros assemblies para teste de unidade

**Tipos de shim** são uma das duas tecnologias que o Microsoft Fakes Framework usa para permitir que você isole componentes em teste do ambiente facilmente. Shims desviam chamadas a métodos específicos para o código que você está escrevendo como parte de seu teste. Muitos métodos retornam resultados diferentes dependendo das condições externas, mas um shim está sob controle do seu teste e pode retornar resultados consistentes em cada chamada. Isso facilita a escrita dos testes.

Use shims para isolar o código de assemblies que não fazem parte de sua solução. Para isolar os componentes da solução uns dos outros, recomendamos que você use stubs.

Para obter uma visão geral e diretrizes de início rápido, confira [Isolar o código em teste com o Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)

**Requisitos**

-   Visual Studio Enterprise
-   Um projeto do .NET Framework

> [!NOTE]
> Projetos do .NET Standard não têm suporte.

## <a name="example-the-y2k-bug"></a>Exemplo: o bug Y2K

Vamos considerar um método que gera uma exceção em 1º de janeiro de 2000:

```csharp
// code under test
public static class Y2KChecker {
    public static void Check() {
        if (DateTime.Now == new DateTime(2000, 1, 1))
            throw new ApplicationException("y2kbug!");
    }
}
```

O teste desse método é problemático porque o programa depende de `DateTime.Now`, um método que depende do relógio do computador, que não é determinístico e depende do ambiente. Além disso, a `DateTime.Now` é uma propriedade estática e, portanto, um tipo de stub não pode ser usado aqui. Esse problema é um sintoma do isolamento no teste de unidade: os programas que chamam APIs de banco de dados diretamente e se comunicam com serviços Web e afins são difíceis de testar porque sua lógica depende do ambiente.

Nesses casos é que os tipos de shim devem ser usados. Os tipos de shim oferecem um mecanismo para desviar qualquer método .NET para um representante definido pelo usuário. Os tipos de shim são gerados por código pelo gerador de Fakes e usam representantes, que chamamos de tipos de shim, para especificar as novas implementações do método.

O teste abaixo mostra como usar o tipo de shim `ShimDateTime` para fornecer uma implementação personalizada de DateTime.Now:

```csharp
//unit test code
// create a ShimsContext cleans up shims
using (ShimsContext.Create()) {
    // hook delegate to the shim method to redirect DateTime.Now
    // to return January 1st of 2000
    ShimDateTime.NowGet = () => new DateTime(2000, 1, 1);
    Y2KChecker.Check();
}
```

##  <a name="how-to-use-shims"></a>Como usar shims

###  <a name="AddFakes"></a> Adicionar assemblies do Fakes

1.  No **Gerenciador de Soluções**, expanda as **Referências** do projeto de teste de unidade.

    -   Caso esteja trabalhando no Visual Basic, selecione **Mostrar Todos os Arquivos** na barra de ferramentas do **Gerenciador de Soluções** para ver o nó **Referências**.

2.  Selecione o assembly que contém as definições de classe para as quais você deseja criar shims. Por exemplo, caso deseje usar shim em **DateTime**, selecione **System.dll**.

3.  No menu de atalhos, escolha **Adicionar Assembly do Fakes**.

###  <a name="ShimsContext"></a> Use ShimsContext

Ao usar tipos de shim em uma estrutura de teste de unidade, você deverá encapsular o código de teste em um `ShimsContext` para controlar o tempo de vida dos shims. Se não exigíssemos isso, seus shims durariam até o AppDomain ser desligado. A maneira mais fácil de criar um `ShimsContext` é usando o método estático `Create()` mostrado no código abaixo:

```csharp
//unit test code
[Test]
public void Y2kCheckerTest() {
  using(ShimsContext.Create()) {
    ...
  } // clear all shims
}
```

É fundamental dispor cada contexto de shim adequadamente. Como regra geral, chame sempre o `ShimsContext.Create` dentro de uma instrução `using` para garantir a limpeza apropriada dos shims registrados. Por exemplo, você pode registrar um shim para um método de teste que substitui o método `DateTime.Now` por um representante que sempre retorna 1º de janeiro de 2000. Se você esquecer de limpar o shim registrado no método de teste, o restante da execução do teste sempre retornará 1º de janeiro de 2000 como valor DateTime.Now. Isso pode ser surpreendente e pode causar confusão.

###  <a name="WriteShims"></a>Escrever um teste com shims

No código de teste, insira um *desvio* para o método que você deseja forjar. Por exemplo:

```csharp
[TestClass]
public class TestClass1
{
        [TestMethod]
        public void TestCurrentYear()
        {
            int fixedYear = 2000;

            using (ShimsContext.Create())
            {
              // Arrange:
                // Detour DateTime.Now to return a fixed date:
                System.Fakes.ShimDateTime.NowGet =
                () =>
                { return new DateTime(fixedYear, 1, 1); };

                // Instantiate the component under test:
                var componentUnderTest = new MyComponent();

              // Act:
                int year = componentUnderTest.GetTheCurrentYear();

              // Assert:
                // This will always be true if the component is working:
                Assert.AreEqual(fixedYear, year);
            }
        }
}
```

```vb
<TestClass()> _
Public Class TestClass1
    <TestMethod()> _
    Public Sub TestCurrentYear()
        Using s = Microsoft.QualityTools.Testing.Fakes.ShimsContext.Create()
            Dim fixedYear As Integer = 2000
            ' Arrange:
            ' Detour DateTime.Now to return a fixed date:
            System.Fakes.ShimDateTime.NowGet = _
                Function() As DateTime
                    Return New DateTime(fixedYear, 1, 1)
                End Function

            ' Instantiate the component under test:
            Dim componentUnderTest = New MyComponent()
            ' Act:
            Dim year As Integer = componentUnderTest.GetTheCurrentYear
            ' Assert:
            ' This will always be true if the component is working:
            Assert.AreEqual(fixedYear, year)
        End Using
    End Sub
End Class
```

Os nomes das classes de shims são compostos pelo prefixo `Fakes.Shim` adicionado ao nome do tipo original.

Os shims funcionam inserindo *desvios* no código do aplicativo em teste. Sempre que ocorre uma chamada ao método original, o sistema de falsificações executa um desvio para que, em vez de chamar o método real, seu código de shim seja chamado.

Observe que os desvios são criados e excluídos no tempo de execução. Você sempre deve criar um desvio na vida de um `ShimsContext`. Quando descartado, os shims criados enquanto ele estava ativo são removidos. A melhor maneira de fazer isso é dentro de uma instrução `using`.

Você pode ver um erro de compilação indicando que o namespace do Fakes não existe. Às vezes, este erro ocorre quando há outros erros de compilação. Corrija os outros erros e ele desaparecerá.

##  <a name="BKMK_Shim_basics"></a> Shims para tipos de métodos diferentes

Os tipos de shim permitem que você substitua qualquer método do .NET, incluindo métodos estáticos ou não virtuais, pelos seus próprios representantes.

###  <a name="BKMK_Static_methods"></a> Métodos estáticos

As propriedades para anexar shims a métodos estáticos são colocadas em um tipo de shim. Cada propriedade tem apenas um setter que pode ser usado para anexar um representante ao método de destino. Por exemplo, dada a classe `MyClass` com um método estático `MyMethod`:

```csharp
//code under test
public static class MyClass {
    public static int MyMethod() {
        ...
    }
}
```

Podemos anexar um shim a `MyMethod` que sempre retorna 5:

```csharp
// unit test code
ShimMyClass.MyMethod = () =>5;
```

###  <a name="BKMK_Instance_methods__for_all_instances_"></a> Métodos de instância (para todas as instâncias)

Semelhantemente aos métodos estáticos, os métodos de instância podem fazer shim em todas as instâncias. As propriedades para anexar esses shims são colocadas em um tipo aninhado chamado AllInstances para evitar confusão. Por exemplo, dada a classe `MyClass` com um método de instância `MyMethod`:

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

Você pode anexar um shim a `MyMethod` que sempre retorna 5, independentemente da instância:

```csharp
// unit test code
ShimMyClass.AllInstances.MyMethod = () => 5;
```

A estrutura de tipo gerada de ShimMyClass se parece com o seguinte código:

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public static class AllInstances {
        public static Func<MyClass, int>MyMethod {
            set {
                ...
            }
        }
    }
}
```

Observe que o Fakes passa a instância de tempo de execução como o primeiro argumento do representante nesse caso.

###  <a name="BKMK_Instance_methods__for_one_instance_"></a> Métodos de instância (para uma instância de tempo de execução)

Os métodos de instância também podem sofrer shim por representantes diferentes com base no receptor da chamada. Isso permite que o mesmo método de instância tenha comportamentos diferentes por instância do tipo. As propriedades para configurar esses shims são métodos de instância do próprio tipo shim. Cada tipo de shim instanciado também está associado uma instância bruta de um tipo com shim.

Por exemplo, dada a classe `MyClass` com um método de instância `MyMethod`:

```csharp
// code under test
public class MyClass {
    public int MyMethod() {
        ...
    }
}
```

Podemos configurar dois tipos de shim MyMethod em que o primeiro sempre retorna 5 e o segundo sempre retorna 10:

```csharp
// unit test code
var myClass1 = new ShimMyClass()
{
    MyMethod = () => 5
};
var myClass2 = new ShimMyClass { MyMethod = () => 10 };
```

A estrutura de tipo gerada de ShimMyClass se parece com o seguinte código:

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public Func<int> MyMethod {
        set {
            ...
        }
    }
    public MyClass Instance {
        get {
            ...
        }
    }
}
```

A instância de tipo realmente com shim pode ser acessada por meio da propriedade Instance:

```csharp
// unit test code
var shim = new ShimMyClass();
var instance = shim.Instance;
```

O tipo de shim também tem uma conversão implícita no tipo com shim, para que se possa usar o tipo de shim simplesmente como ele é:

```csharp
// unit test code
var shim = new ShimMyClass();
MyClass instance = shim; // implicit cast retrieves the runtime
                         // instance
```

###  <a name="BKMK_Constructors"></a> Construtores

Os construtores também podem sofrer shim para anexar tipos de shim a objetos futuros. Cada construtor é exposto como um método estático Constructor no tipo de shim. Por exemplo, dada a classe `MyClass` com um construtor usando um número inteiro:

```csharp
// code under test
public class MyClass {
    public MyClass(int value) {
        this.Value = value;
    }
    ...
}
```

Configuramos o tipo de shim do construtor para que todas as instâncias futuras retornem -5 quando o getter Value é chamado, independentemente do valor no construtor:

```csharp
// unit test code
ShimMyClass.ConstructorInt32 = (@this, value) => {
    var shim = new ShimMyClass(@this) {
        ValueGet = () => -5
    };
};
```

Cada tipo de shim expõe dois construtores. O construtor padrão deve ser usado quando uma nova instância é necessária; já o construtor que usa uma instância com shim como argumento deve ser usado apenas em shims de construtor:

```csharp
// unit test code
public ShimMyClass() { }
public ShimMyClass(MyClass instance) : base(instance) { }
```

A estrutura do tipo gerado de ShimMyClass lembra o seguinte código:

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass>
{
    public static Action<MyClass, int> ConstructorInt32 {
        set {
            ...
        }
    }

    public ShimMyClass() { }
    public ShimMyClass(MyClass instance) : base(instance) { }
    ...
}
```

###  <a name="BKMK_Base_members"></a> Membros base

As propriedades de shim dos membros base podem ser acessadas com a criação de uma correção para o tipo base e a passagem da instância filha como um parâmetro ao construtor da classe de shim base.

Por exemplo, dada a classe `MyBase` com um método de instância `MyMethod` e um subtipo `MyChild`:

```csharp
public abstract class MyBase {
    public int MyMethod() {
        ...
    }
}

public class MyChild : MyBase {
}
```

Podemos configurar um shim de `MyBase` criando um novo shim `ShimMyBase`:

```csharp
// unit test code
var child = new ShimMyChild();
new ShimMyBase(child) { MyMethod = () => 5 };
```

Observe que o tipo de shim filho é implicitamente convertido para a instância filha quando passado como um parâmetro para o construtor shim base.

A estrutura do tipo gerado de ShimMyChild e ShimMyBase se parece com o seguinte código:

```csharp
// Fakes generated code
public class ShimMyChild : ShimBase<MyChild> {
    public ShimMyChild() { }
    public ShimMyChild(Child child)
        : base(child) { }
}
public class ShimMyBase : ShimBase<MyBase> {
    public ShimMyBase(Base target) { }
    public Func<int> MyMethod
    { set { ... } }
}
```

###  <a name="BKMK_Static_constructors"></a> Construtores estáticos

Os tipos de shim expõem um método estático `StaticConstructor` para fazer shim do construtor estático de um tipo. Como os construtores estáticos são executados somente uma vez, você precisa fazer com que a correção seja configurada antes de qualquer membro do tipo ser acessado.

###  <a name="BKMK_Finalizers"></a> Finalizadores

Não há suporte para os finalizadores no Fakes.

###  <a name="BKMK_Private_methods"></a> Métodos privados

O gerador de código do Fakes cria propriedades de shim para métodos particulares que têm apenas tipos visíveis na assinatura, ou seja, tipos de parâmetro e tipo de retorno visíveis.

###  <a name="BKMK_Binding_interfaces"></a>Interfaces de associação

Quando um tipo com shim implementa uma interface, o gerador de código emite um método que permite associar todos os membros da interface de uma vez.

Por exemplo, dada a classe `MyClass` que implementa `IEnumerable<int>`:

```csharp
public class MyClass : IEnumerable<int> {
    public IEnumerator<int> GetEnumerator() {
        ...
    }
    ...
}
```

Podemos fazer shim das implementações de `IEnumerable<int>` em MyClass chamando o método Bind:

```csharp
// unit test code
var shimMyClass = new ShimMyClass();
shimMyClass.Bind(new List<int> { 1, 2, 3 });
```

A estrutura do tipo gerado de ShimMyClass lembra o seguinte código:

```csharp
// Fakes generated code
public class ShimMyClass : ShimBase<MyClass> {
    public ShimMyClass Bind(IEnumerable<int> target) {
        ...
    }
}
```

##  <a name="change-the-default-behavior"></a>Alterar o comportamento padrão

Cada tipo de shim gerado contém uma instância da interface `IShimBehavior` pela propriedade `ShimBase<T>.InstanceBehavior`. O comportamento é usado sempre que um cliente chama um membro de instância que não foi sofreu shim explicitamente.

Se o comportamento não tiver sido definido explicitamente, ele usará a instância retornada pela propriedade estática `ShimsBehaviors.Current`. Por padrão, essa propriedade retorna um comportamento que gerou uma exceção `NotImplementedException`.

Esse comportamento pode ser alterado a qualquer momento definindo a propriedade `InstanceBehavior` em qualquer instância do shim. Por exemplo, o seguinte snippet altera o shim de um comportamento que não faz nada ou retorna o valor padrão do tipo de retorno, ou seja, padrão(T):

```csharp
// unit test code
var shim = new ShimMyClass();
//return default(T) or do nothing
shim.InstanceBehavior = ShimsBehaviors.DefaultValue;
```

O comportamento também pode ser alterado globalmente para todas as instâncias com shim para as quais a propriedade `InstanceBehavior` não foi definida explicitamente definindo a propriedade estática `ShimsBehaviors.Current`:

```csharp
// unit test code
// change default shim for all shim instances
// where the behavior has not been set
ShimsBehaviors.Current =
    ShimsBehaviors.DefaultValue;
```

##  <a name="detect-environment-accesses"></a>Detectar acessos ao ambiente

É possível anexar um comportamento a todos os membros, incluindo métodos estáticos, de um tipo específico atribuindo o comportamento `ShimsBehaviors.NotImplemented` à propriedade estática `Behavior` do tipo de shim correspondente:

```csharp
// unit test code
// assigning the not implemented behavior
ShimMyClass.Behavior = ShimsBehaviors.NotImplemented;
// shorthand
ShimMyClass.BehaveAsNotImplemented();
```

##  <a name="BKMK_Concurrency"></a> Simultaneidade

Os tipos de shim se aplicam a todos os threads no AppDomain e não têm afinidade de thread. Isso é importante se você planeja usar um executor de teste que dá suporte à simultaneidade: testes que envolvem tipos de shim não podem ser executados simultaneamente. Essa propriedade não é imposta pelo tempo de execução do Fakes.

##  <a name="call-the-original-method-from-the-shim-method"></a>Chamar o método original por meio do método shim

Imagine que gostaríamos realmente de escrever o texto no sistema de arquivos depois de validar o nome do arquivo passado para o método. Nesse caso, quereríamos chamar o método original no meio do método shim.

A primeira abordagem para resolver esse problema é encapsular uma chamada ao método original usando um representante e `ShimsContext.ExecuteWithoutShims()`, como no código abaixo:

```csharp
// unit test code
ShimFile.WriteAllTextStringString = (fileName, content) => {
  ShimsContext.ExecuteWithoutShims(() => {

      Console.WriteLine("enter");
      File.WriteAllText(fileName, content);
      Console.WriteLine("leave");
  });
};
```

Outra abordagem é definir o shim como null, chamar o método original e restaurar o shim.

```csharp
// unit test code
ShimsDelegates.Action<string, string> shim = null;
shim = (fileName, content) => {
  try {
    Console.WriteLine("enter");
    // remove shim in order to call original method
    ShimFile.WriteAllTextStringString = null;
    File.WriteAllText(fileName, content);
  }
  finally
  {
    // restore shim
    ShimFile.WriteAllTextStringString = shim;
    Console.WriteLine("leave");
  }
};
// initialize the shim
ShimFile.WriteAllTextStringString = shim;
```

##  <a name="BKMK_Limitations"></a> Limitações

Os shims não podem ser usados em todos os tipos da biblioteca de classes base do .NET **mscorlib** e **System**.

## <a name="see-also"></a>Consulte também

- [Isolar o código em teste com o Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md)
- [Blog de Peter Provost: Visual Studio 2012 shims](http://www.peterprovost.org/blog/2012/04/25/visual-studio-11-fakes-part-2) (Shims do Visual Studio 2012)
- [Vídeo (1h16): testando códigos que não podem ser testados com elementos fictícios no Visual Studio 2012](http://go.microsoft.com/fwlink/?LinkId=261837)
