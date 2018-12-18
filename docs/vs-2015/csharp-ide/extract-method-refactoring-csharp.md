---
title: Extrair método refatoração (c#) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.csharp.refactoring.extractmethod
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Method
- Extract Method refactoring operation [C#]
ms.assetid: eeba11df-a815-4bec-9c21-8a831891b783
caps.latest.revision: 29
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: cc05da79676beed5fa698f11843a6b7485280e71
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49228053"
---
# <a name="extract-method-refactoring-c"></a>Refatoração Extrair Método (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**Extrair método** é uma operação de refatoração que fornece uma maneira fácil de criar um novo método de um fragmento de código em um membro existente.  
  
 Usando o **extrair método**, você pode criar um novo método extraindo uma seleção de código de dentro do bloco de código de um membro existente. O método extraído, novo contém o código selecionado e o código selecionado no membro existente é substituído por uma chamada para o novo método. Transformar um fragmento de código em seu próprio método permite que você rapidamente e com precisão reorganizar o código para melhorar a legibilidade e reutilização.  
  
 **Extrair método** tem os seguintes benefícios:  
  
-   Incentiva práticas de codificação melhor, enfatizando métodos discretos e reutilizáveis.  
  
-   Incentiva a autodocumentação em código por meio de boa organização.  
  
     Quando nomes descritivos são os métodos usados e de alto nível, podem ler mais como uma série de comentários.  
  
-   Incentiva a criação de métodos mais refinados para simplificar a substituição.  
  
-   Reduz a duplicação de código.  
  
### <a name="to-use-extract-method"></a>Usar extrair método  
  
1.  Crie um aplicativo de console chamado `ExtractMethod`e, em seguida, substitua `Program` com o código de exemplo a seguir.  
  
    ```csharp  
    class A  
    {  
        const double PI = 3.141592;  
  
        double CalculatePaintNeeded(double paintPerUnit, double radius)  
        {  
            // Select any of the following:  
            // 1. The entire next line of code.  
            // 2. The right-hand side of the next line of code.  
            // 3. Just "PI *" of the right-hand side of the next line  
            //    of code (to see the prompt for selection expansion).  
            // 4.  All code within the method body.  
            // ...Then invoke Extract Method.  
  
            double area = PI * radius * radius;  
  
            return area / paintPerUnit;  
        }  
    }  
    ```  
  
2.  Selecione o fragmento de código que você deseja extrair:  
  
    ```csharp  
    double area = PI * radius * radius;  
    ```  
  
3.  Sobre o **refatorar** menu, clique em **extrair método**.  
  
     O **extrair método** caixa de diálogo é exibida.  
  
     Como alternativa, você também pode digitar o atalho de teclado CTRL + R, M para exibir o **extrair método** caixa de diálogo.  
  
     Você pode também com o botão direito selecionado de código, aponte para **refatorar**e, em seguida, clique em **extrair método** para exibir o **extrair método** caixa de diálogo.  
  
4.  Especifique um nome para o novo método, como `CircleArea`, no **nome do novo método** caixa.  
  
     Uma visualização da nova assinatura de método exibe sob **Visualizar assinatura do método**.  
  
5.  Clique em **OK**.  
  
## <a name="remarks"></a>Comentários  
 Quando você usa o **extrair método** de comando, o novo método é inserido após o membro de origem na mesma classe.  
  
## <a name="partial-types"></a>Tipos parciais  
 Se a classe for um tipo parcial, em seguida **extrair método** gera o novo método imediatamente após o membro de origem. **Extrair método** determina a assinatura do novo método, criando um método estático quando nenhum dado de instância é referenciado pelo código no novo método.  
  
## <a name="generic-type-parameters"></a>Parâmetros de tipo genérico  
 Quando você extrair um método que tem um parâmetro de tipo genérico sem restrição, o código gerado não adicionará o `ref` modificador para esse parâmetro, a menos que um valor é atribuído a ele. Se o método extraído dará suporte a tipos de referência como o argumento de tipo genérico e, em seguida, você deve adicionar manualmente o `ref` modificador para o parâmetro na assinatura do método.  
  
## <a name="anonymous-methods"></a>Métodos anônimos  
 Se você tentar extrair parte de um método anônimo que inclui uma referência a uma variável local que é declarada ou referenciada fora do método anônimo, em seguida, o Visual Studio avisará sobre possíveis alterações semânticas.  
  
 Quando um método anônimo usa o valor de uma variável local, o valor é obtido no momento em que o método anônimo é executado. Quando um método anônimo é extraído para outro método, o valor da variável local é obtido no momento da chamada para o método extraído.  
  
 O exemplo a seguir ilustra essa alteração semântica. Se esse código é executado, em seguida **11** será impressa no console. Se você usar **extrair método** para extrair a região de código que está marcado com comentários de código em seu próprio método e, em seguida, executar o código refatorado, em seguida, **10** será impressa no console.  
  
```csharp  
class Program  
{  
    delegate void D();  
    D d;  
    static void Main(string[] args)  
    {  
        Program p = new Program();  
        int i = 10;  
        /*begin extraction*/  
            p.d = delegate { Console.WriteLine(i++); };  
        /*end extraction*/  
        i++;  
        p.d();  
    }  
}  
```  
  
 Para contornar essa situação, verifique as variáveis locais que são usadas nos campos da classe de método anônimo.  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)