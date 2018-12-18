---
title: Como criar um tipo que permite valor nulo (Designer de Classe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- nullable types, Class Designer
- Class Designer [Visual Studio], nullable types
ms.assetid: 84673a89-3f6d-4668-919e-1c0f56182fe5
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ab5bfe3068f79bceb02352b47de4beb08da75c85
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49941939"
---
# <a name="how-to-create-a-nullable-type-class-designer"></a>Como criar um tipo anulável (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Alguns tipos de valor nem sempre têm (ou precisam de) um valor definido. Essa é uma prática comum em bancos de dados, em que alguns campos podem não receber nenhum valor. Por exemplo, é possível atribuir um valor nulo a um campo de banco de dados para indicar que ele ainda não recebeu um valor.  
  
 Um *tipo que permite valor nulo* é um tipo de valor que é estendido, para que ele use o intervalo de valores típico para esse tipo e também um valor nulo. Por exemplo, um tipo que permite valor nulo igual a `Int32`, também indicado como Nullable\<Int32>, pode receber qualquer valor de -2147483648 a 2147483647 ou receber um valor nulo. Um Nullable\<bool> pode receber os valores `True`, `False` ou nulo (nenhum valor).  
  
 Os tipos que permitem valor nulo são instâncias da estrutura <xref:System.Nullable%601>. Cada instância de um tipo que permite valor nulo tem duas propriedades públicas somente leitura, `HasValue` e `Value`:  
  
- `HasValue` é do tipo `bool` e indica se a variável contém um valor definido. `True` significa que a variável contém um valor não nulo. É possível testar um valor definido usando uma instrução como `if (x.HasValue)` ou `if (y != null)`.  
  
- `Value` é do mesmo tipo que o tipo subjacente. Se `HasValue` for `True`, `Value` conterá um valor significativo. Se `HasValue` for `False`, o acesso a `Value` gerará uma exceção de operação inválida.  
  
  Por padrão, ao declarar uma variável como um tipo que permite valor nulo, ela não terá nenhum valor definido (`HasValue` é `False`), além do valor padrão de seu tipo de valor subjacente.  
  
  O Designer de Classe exibe um tipo que permite valor nulo assim que ele exibe seu tipo subjacente.  
  
  Para obter mais informações sobre tipos que permitem valor nulo no Visual C#, consulte [Tipos que permitem valor nulo](http://msdn.microsoft.com/library/e473cb01-28ca-42be-9cea-f717055d72c6). Para obter mais informações sobre tipos que permitem valor nulo no Visual Basic, consulte [Tipos de valores que permitem valor nulo](http://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6).  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
### <a name="to-add-a-nullable-type-by-using-the-class-designer"></a>Para adicionar um tipo que permite valor nulo usando o Designer de Classe  
  
1.  No Diagrama de Classe, expanda uma classe existente ou crie uma nova classe.  
  
2.  Para adicionar uma classe ao projeto, no menu **Diagrama de Classe**, clique em **Adicionar** e, em seguida, em **Adicionar Classe**.  
  
3.  Para expandir a forma da classe, no menu **Diagrama de Classe**, clique em **Expandir**.  
  
4.  Selecione a forma da classe. No menu **Diagrama de Classe**, clique em **Adicionar** e, em seguida, em **Campo**. Um novo campo que tem o nome padrão **Campo** será exibido na forma da classe e também na Janela **Detalhes da Classe**.  
  
5.  Na coluna **Nome** da Janela **Detalhes da Classe** (ou na própria forma da classe), altere o nome do novo campo para um nome válido e significativo.  
  
6.  Na coluna **Tipo** da Janela **Detalhes da Classe**, declare o tipo como um tipo que permite valor nulo, conforme mostrado no seguinte código:  
  
    ```csharp  
    // Declare a nullable type in Visual C#:  
    class Test  
    {  
       int? building_number = 5;  
    }  
    ```  
  
    ```vb  
    ' Declare a nullable type in Visual Basic:  
    Class Test  
       Dim buildingNumber As Nullable(Of Integer) = 5  
    End Class  
    ```  
  
### <a name="to-add-a-nullable-type-by-using-the-code-editor"></a>Para adicionar um tipo que permite valor nulo usando o Editor de Código  
  
1.  Adicione uma classe ao projeto. Selecione o nó do projeto no **Gerenciador de Soluções** e, no menu **Projeto**, clique em **Adicionar Classe**.  
  
2.  No arquivo .cs ou .vb da nova classe, adicione um ou mais tipos que permitem valor nulo da nova classe à declaração de classe.  
  
3.  No Modo de Exibição de Classe, arraste o ícone da nova classe para a superfície de design do Designer de Classe. Uma forma de classe é exibida no diagrama de classe.  
  
4.  Expanda os detalhes da forma de classe e mova o ponteiro do mouse sobre os membros da classe. A dica de ferramenta exibe a declaração de cada membro.  
  
5.  Clique com o botão direito do mouse na forma da classe e clique em **Detalhes da Classe**. É possível exibir ou modificar as propriedades do novo tipo na Janela **Detalhes da Classe**.  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Nullable%601>   
 [Tipos que permitem valor nulo](http://msdn.microsoft.com/library/e473cb01-28ca-42be-9cea-f717055d72c6)   
 [Usando tipos que permitem valor nulo](http://msdn.microsoft.com/library/0bacbe72-ce15-4b14-83e1-9c14e6380c28)   
 [Como identificar um tipo que permite valor nulo](http://msdn.microsoft.com/library/d4b67ee2-66e8-40c1-ae9d-545d32c71387)   
 [Tipos de Valor Anulável](http://msdn.microsoft.com/library/9ac3b602-6f96-4e6d-96f7-cd4e81c468a6)



