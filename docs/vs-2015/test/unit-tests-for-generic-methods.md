---
title: Testes de unidade para métodos genéricos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- generics, and unit tests
- unit tests, and generics
ms.assetid: ffc89814-a7df-44fc-aef5-dd3dfeb28a9b
caps.latest.revision: 49
ms.author: gewarren
manager: douge
ms.openlocfilehash: 3657c3ea41af2aa85177ff47a28797ef7f55cc41
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49914392"
---
# <a name="unit-tests-for-generic-methods"></a>Testes de unidade para métodos genéricos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode gerar testes de unidade para métodos genéricos exatamente como faria para outros métodos, conforme descrito em [Como criar e executar um teste de unidade](http://msdn.microsoft.com/en-us/5e0f43cf-5e51-48e2-9c98-0eb9324bdc48). As seções a seguir fornecem informações e exemplos de criação de testes de unidade para métodos genéricos.  
  
## <a name="type-arguments-and-type-constraints"></a>Restrições de tipo e argumentos de tipo  
 Quando [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] gera um teste de unidade para uma classe genérica como `MyList<T>`, ela gera dois métodos: um auxiliar genérico e um método de teste. Se `MyList<T>` tem uma ou mais restrições de tipo, o argumento de tipo deve atender a todas as restrições de tipo. Para certificar-se de que o código genérico em teste funciona conforme o esperado para todas as entradas possíveis, o método de teste chama o método auxiliar genérico com todas as restrições que você deseja testar.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir ilustram testes de unidade para genéricos:  
  
-   [Edição do código de teste gerado](#EditingGeneratedTestCode). Este exemplo tem duas seções, Código de teste gerado e Código de teste editado. Ele mostra como editar o código de teste bruto gerado de um método genérico em um método de teste útil.  
  
-   [Usando uma restrição de tipo](#TypeConstraintNotSatisfied). Este exemplo mostra um teste de unidade para um método genérico que usa uma restrição de tipo. Neste exemplo, a restrição de tipo não for atendida.  
  
###  <a name="EditingGeneratedTestCode"></a> Exemplo 1: edição do código de teste gerado  
 O código de teste nesta seção testa um método de código em teste chamado `SizeOfLinkedList()`. Esse método retorna um inteiro que especifica o número de nós na lista vinculada.  
  
 O primeiro exemplo de código, na seção Código de teste gerado, mostra o código de teste não editado como ele foi gerado pelo Visual Studio Enterprise. O segundo exemplo, na seção Código de teste editado, mostra como você poderia fazê-lo testar o funcionamento do método SizeOfLinkedList para dois tipos de dados diferentes, `int` e `char`.  
  
 Este código ilustra dois métodos:  
  
-   um método auxiliar de teste, `SizeOfLinkedListTestHelper<T>()`. Por padrão, um método auxiliar de teste tem "TestHelper" em seu nome.  
  
-   um método de teste, `SizeOfLinkedListTest()`. Cada método de teste é marcado com o atributo TestMethod.  
  
#### <a name="generated-test-code"></a>Código de teste gerado  
 O código de teste a seguir foi gerado por meio do método `SizeOfLinkedList()`. Como esse é o teste gerado não editado, ele deve ser modificado para testar corretamente o método SizeOfLinkedList.  
  
```  
public void SizeOfLinkedListTestHelper<T>()  
{  
    T val = default(T); // TODO: Initialize to an appropriate value  
    MyLinkedList<T> target = new MyLinkedList<T>(val); // TODO: Initialize to an appropriate value  
    int expected = 0; // TODO: Initialize to an appropriate value  
    int actual;  
    actual = target.SizeOfLinkedList();  
    Assert.AreEqual(expected, actual);  
    Assert.Inconclusive("Verify the correctness of this test method.");  
}  
  
[TestMethod()]  
public void SizeOfLinkedListTest()  
{  
   SizeOfLinkedListTestHelper<GenericParameterHelper>();  
}  
```  
  
 No código anterior, o parâmetro de tipo genérico é `GenericParameterHelper`. Considerando que você pode editá-lo para fornecer tipos de dados específicos, conforme mostrado no exemplo a seguir, você poderia executar o teste sem editar essa instrução.  
  
#### <a name="edited-test-code"></a>Código de teste editado  
 No código a seguir, o método de teste e o método auxiliar de teste foram editados para fazer com que eles testem com êxito o método de código em teste `SizeOfLinkedList()`.  
  
##### <a name="test-helper-method"></a>Método auxiliar de teste  
 O método auxiliar de teste executa as etapas a seguir, que correspondem às linhas de código rotuladas como etapas 1 a 5.  
  
1.  Crie uma lista vinculada genérica.  
  
2.  Acrescente quatro nós à lista vinculada. O tipo de dados do conteúdo desses nós é desconhecido.  
  
3.  Atribua o tamanho esperado da lista vinculada à variável `expected`.  
  
4.  Compute o tamanho real da lista vinculada e atribua-a à variável `actual`.  
  
5.  Compare `actual` com `expected` em uma instrução Assert. Se o valor real não for igual ao esperado, o teste falhará.  
  
##### <a name="test-method"></a>Método de Teste  
 O método de teste é compilado para o código que é chamado quando você executa o teste chamado SizeOfLinkedListTest. Ele executa as etapas a seguir, que correspondem às linhas de código rotuladas como etapas 6 e 7.  
  
1.  Especifique `<int>` quando você chama o método auxiliar de teste, para verificar se o teste funciona para variáveis `integer`.  
  
2.  Especifique `<char>` quando você chama o método auxiliar de teste, para verificar se o teste funciona para variáveis `char`.  
  
```  
  
public void SizeOfLinkedListTestHelper<T>()  
{  
    T val = default(T);   
    MyLinkedList<T> target = new MyLinkedList<T>(val); // step 1  
    for (int i = 0; i < 4; i++) // step 2  
    {  
        MyLinkedList<T> newNode = new MyLinkedList<T>(val);  
        target.Append(newNode);  
    }  
    int expected = 5; // step 3  
    int actual;  
    actual = target.SizeOfLinkedList(); // step 4  
    Assert.AreEqual(expected, actual); // step 5  
}  
  
[TestMethod()]  
public void SizeOfLinkedListTest()   
{  
    SizeOfLinkedListTestHelper<int>();  // step 6  
    SizeOfLinkedListTestHelper<char>(); // step 7  
}  
```  
  
> [!NOTE]
>  Cada vez que o teste SizeOfLinkedListTest é executado, o método TestHelper é chamado duas vezes. A instrução assert deve ser sempre avaliada como true para que o teste seja aprovado. Se o teste falhar, talvez não fique claro se foi a chamada que especificou `<int>` ou a chamada que especificou `<char>` que causou a falha. Para encontrar a resposta, você pode examinar a pilha de chamadas ou definir pontos de interrupção em seu método de teste e, em seguida, depurar durante a execução do teste. Para obter mais informações, consulte [Como depurar durante a execução de um teste em uma solução do ASP.NET](http://msdn.microsoft.com/library/de4d7aa1-4a1e-467e-a19b-4a85ec245b8b).  
  
###  <a name="TypeConstraintNotSatisfied"></a> Exemplo 2: usando uma restrição de tipo  
 Este exemplo mostra um teste de unidade para um método genérico que usa uma restrição de tipo não atendida. A primeira seção mostra código do projeto de código em teste. A restrição de tipo está realçada.  
  
 A segunda seção mostra código do projeto de teste.  
  
#### <a name="code-under-test-project"></a>Projeto de código em teste  
  
```  
using System;  
using System.Linq;  
using System.Collections.Generic;  
using System.Text;  
  
namespace ClassLibrary2  
{  
    public class Employee  
    {  
        public Employee(string s, int i)  
        {  
        }  
    }  
  
    public class GenericList<T> where T : Employee  
    {  
        private class Node  
        {  
            private T data;  
            public T Data  
            {  
                get { return data; }  
                set { data = value; }  
            }  
        }  
    }  
}  
```  
  
#### <a name="test-project"></a>Projeto de Teste  
 Assim como acontece com todos os testes de unidade recém-gerados, você deve adicionar instruções Assert não inconclusivas a esse teste de unidade para fazê-lo retornar resultados úteis. Você não os adiciona ao método marcado com o atributo TestMethod, mas sim ao método "TestHelper", que neste teste é chamado de `DataTestHelper<T>()`.  
  
 Neste exemplo, o parâmetro de tipo genérico `T` tem a restrição `where T : Employee`. Essa restrição não foi atendida no método de teste. Portanto, o método `DataTest()` contém uma instrução Assert que alerta você para a necessidade de fornecer a restrição de tipo que foi colocada em `T`. A mensagem desta instrução Assert diz o seguinte: `("No appropriate type parameter is found to satisfies the type constraint(s) of T. " + "Please call DataTestHelper<T>() with appropriate type parameters.");`  
  
 Em outras palavras, quando você chama o método `DataTestHelper<T>()` do método de teste, `DataTest()`, você deve passar um parâmetro do tipo `Employee` ou uma classe derivada de `Employee`.  
  
 `using ClassLibrary2;`  
  
 `using Microsoft.VisualStudio.TestTools.UnitTesting;`  
  
 `namespace TestProject1`  
  
```  
{  
    [TestClass()]  
    public class GenericList_NodeTest  
    {  
  
        public void DataTestHelper<T>()  
            where T : Employee  
        {  
            GenericList_Shadow<T>.Node target = new GenericList_Shadow<T>.Node(); // TODO: Initialize to an appropriate value  
            T expected = default(T); // TODO: Initialize to an appropriate value  
            T actual;  
            target.Data = expected;  
            actual = target.Data;  
            Assert.AreEqual(expected, actual);  
            Assert.Inconclusive("Verify the correctness of this test method.");  
        }  
  
        [TestMethod()]  
        public void DataTest()  
        {  
            Assert.Inconclusive("No appropriate type parameter is found to satisfies the type constraint(s) of T. " +  
            "Please call DataTestHelper<T>() with appropriate type parameters.");  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Anatomia de um teste de unidade](http://msdn.microsoft.com/en-us/a03d1ee7-9999-4e7c-85df-7d9073976144)   
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)



