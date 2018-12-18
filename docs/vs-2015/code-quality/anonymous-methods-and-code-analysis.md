---
title: Métodos anônimos e análise de código | Microsoft Docs
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
- methods, anonymous
- code analysis, anonymous methods
- anonymous methods, code analysis
ms.assetid: bf0a1a9b-b954-4d46-9c0b-cee65330ad00
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 73ff8dfca29f1ed9896462725886baa87e729100
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49280157"
---
# <a name="anonymous-methods-and-code-analysis"></a>Métodos anônimos e análise de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Uma *método anônimo* é um método que não tem nome. Métodos anônimos são usados com mais frequência para passar um bloco de código como um parâmetro delegado.  
  
 Este tópico explica como a análise de código lida com os avisos e as métricas que estão associadas a métodos anônimos.  
  
## <a name="anonymous-methods-declared-in-a-member"></a>Métodos anônimos, declarados em um membro  
 Avisos e as métricas para um método anônimo que é declarada em um membro, como um método ou um acessador, são associadas com o membro que declara o método. Eles não são associados com o membro que chama o método.  
  
 Por exemplo, na classe, todos os avisos que são encontrados na declaração de **anonymousMethod** deve ser gerado em relação a **Method1** e não **Method2**.  
  
```vb  
  
      Delegate Function ADelegate(ByVal value As Integer) As Boolean  
Class AClass  
  
    Sub Method1()  
        Dim anonymousMethod As ADelegate = Function(ByVal value As Integer) value > 5  
        Method2(anonymousMethod)  
    End SubSub Method2(ByVal anonymousMethod As ADelegate)  
        anonymousMethod(10)  
    End SubEnd Class  
```  
  
```csharp  
  
      delegate void Delegate();  
class Class  
{  
    void Method1()  
    {  
        Delegate anonymousMethod = delegate()   
        {   
          Console.WriteLine("");   
        }  
        Method2(anonymousMethod);  
    }  
  
    void Method2(Delegate anonymousMethod)  
    {  
        anonymousMethod();  
    }  
}  
```  
  
## <a name="inline-anonymous-methods"></a>Métodos anônimos embutidos  
 Avisos e as métricas para um método anônimo que é declarado como uma atribuição de embutido para um campo são associadas com o construtor. Se o campo é declarado como `static` (`Shared` em [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]), os avisos e as métricas são associados com o construtor de classe; caso contrário, eles estão associados com o construtor de instância.  
  
 Por exemplo, na classe, todos os avisos que são encontrados na declaração de **anonymousMethod1** será gerado com o construtor padrão gerado implicitamente da **classe**. Por outro lado, os erros encontrados no **anonymousMethod2** serão aplicadas contra o construtor de classe gerada implicitamente.  
  
```vb  
  
  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass  
Dim anonymousMethod1 As ADelegate = Function(ByVal value As    Integer) value > 5  
Shared anonymousMethod2 As ADelegate = Function(ByVal value As     Integer) value > 5  
  
Sub Method1()  
    anonymousMethod1(10)  
    anonymousMethod2(10)  
End SubEnd Class  
```  
  
```csharp  
  
      delegate void Delegate();  
class Class  
{  
    Delegate anonymousMethod1 = delegate()   
    {   
       Console.WriteLine("");   
    }  
  
    static Delegate anonymousMethod2 = delegate()   
    {   
       Console.WriteLine("");   
    }  
  
    void Method()  
    {  
       anonymousMethod1();  
       anonymousMethod2();  
    }  
}  
```  
  
 Uma classe pode conter um método anônimo embutido que atribui um valor a um campo que tem vários construtores. Nesse caso, avisos e as métricas estão associadas a todos os construtores, a menos que esse construtor encadeia outro construtor na mesma classe.  
  
 Por exemplo, na classe, todos os avisos que são encontrados na declaração de **anonymousMethod** deve ser gerado em relação a **Class(int)** e **Class(string)** mas não em relação ao **Class ()**.  
  
```vb  
  
  Delegate Function ADelegate(ByVal value As Integer) As BooleanClass AClass  
  
Dim anonymousMethod As ADelegate = Function(ByVal value As Integer)   
value > 5  
  
SubNew()  
    New(CStr(Nothing))  
End SubSub New(ByVal a As Integer)  
End SubSub New(ByVal a As String)  
End SubEnd Class  
```  
  
```csharp  
  
      delegate void Delegate();  
class Class  
{  
    Delegate anonymousMethod = delegate()   
    {   
       Console.WriteLine("");   
    }  
  
    Class() : this((string)null)  
    {  
    }  
  
    Class(int a)  
    {  
    }  
  
    Class(string a)  
    {  
    }  
}  
```  
  
 Embora isso possa parecer inesperado, isso ocorre porque o compilador gera um método exclusivo para cada construtor que não está encadeado a outro construtor. Devido a esse comportamento, qualquer violação que isso ocorre na **anonymousMethod** deve ser suprimida separadamente. Isso também significa que, se um novo construtor é introduzida, os avisos que anteriormente eram suprimidos contra **Class(int)** e **Class(string)** também devem ser suprimidos contra o novo construtor.  
  
 Você pode contornar esse problema em uma das duas maneiras. Você poderia declarar **anonymousMethod** em um construtor comuns que todas as cadeia de construtores. Ou você pode declará-la em um método de inicialização que é chamado por todos os construtores.  
  
## <a name="see-also"></a>Consulte também  
 [Analisando a qualidade do código gerenciado](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)



