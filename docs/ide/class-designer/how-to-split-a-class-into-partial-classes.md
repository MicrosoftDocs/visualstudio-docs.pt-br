---
title: Como dividir uma classe em classes parciais (Designer de Classe)
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Class Designer, partial classes
- partial classes, Class Designer
ms.assetid: 6f6b0b30-3996-4569-9200-20482b3adf90
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 623ac5269b78faee9f68580f0803576ad56c1233
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85770035"
---
# <a name="how-to-split-a-class-into-partial-classes-in-class-designer"></a>Como dividir uma classe em classes parciais no Designer de Classe

Você pode usar a palavra-chave `partial` (`Partial` em Visual Basic) para dividir a declaração de uma classe ou estrutura entre várias declarações. Você pode usar quantas declarações parciais desejar.

As declarações podem estar em um ou em vários arquivos de origem. Todas as declarações precisam estar no mesmo assembly e no mesmo namespace.

Classes parciais são úteis em várias situações. Em um projeto grande, por exemplo, a separação de uma classe em vários arquivos permite que mais de um programador trabalhe no projeto ao mesmo tempo. Quando você está trabalhando com o código que o Visual Studio gera, é possível alterar a classe sem precisar recriar o arquivo de origem. (Exemplos de código que o Visual Studio gera incluem Windows Forms e o código do wrapper do serviço Web.) Portanto, você pode criar código que usa classes geradas automaticamente sem precisar modificar o arquivo criado pelo Visual Studio.

Existem dois tipos de métodos parciais. No C#, eles são chamados de declarar e implementar. No Visual Basic, são chamados de declaração e implementação.

**Designer de classe** dá suporte a classes e métodos parciais. A forma de tipo no diagrama de classe se refere a um único local de declaração para a classe parcial. Se a classe parcial for definida em vários arquivos, você poderá especificar qual local de Declaração **Designer de classe** será usado definindo a propriedade **novo local do membro** na janela **Propriedades** . Ou seja, quando você clica duas vezes em uma forma de classe, **Designer de classe** vai para o arquivo de origem que contém a declaração de classe identificada pela propriedade **local do novo membro** . Quando você clica duas vezes em um método parcial em uma forma de classe, **Designer de classe** vai para a declaração de método parcial. Além disso, na janela **Propriedades**, a propriedade **Nome de Arquivo** aponta para o local da declaração. Para classes parciais, **Nome de Arquivo** lista todos os arquivos que contêm código de implementação e declaração dessa classe. No entanto, para métodos parciais, **Nome de Arquivo** lista apenas o arquivo que contém a declaração de método parcial.

Os exemplos a seguir dividem a definição da classe `Employee` em duas declarações, cada uma das quais define um procedimento diferente. As duas definições parciais nos exemplos podem estar em um arquivo de origem ou em dois arquivos de origem diferentes.

> [!NOTE]
> O Visual Basic usa definições de classe parcial para separar o código gerado pelo Visual Studio do código de autoria do usuário. O código é separado em arquivos de origem distintos. Por exemplo, o **Windows Form Designer** define classes parciais para controles, como `Form`. Você não deve modificar o código gerado nesses controles.

Para obter mais informações sobre tipos parciais no Visual Basic, consulte [Parcial](/dotnet/visual-basic/language-reference/modifiers/partial).

## <a name="example"></a>Exemplo

Para dividir uma definição de classe, use a palavra-chave `partial` (`Partial` no Visual Basic), conforme mostrado no exemplo a seguir:

```csharp
// First part of class definition.
public partial class Employee
{
    public void CalculateWorkHours()
    {
    }
}

// Second part of class definition.
public partial class Employee
{
    public void CalculateTaxes()
    {
    }
}
```

```vb
' First part of class definition.
Partial Public Class Employee
    Public Sub CalculateWorkHours()
    End Sub
End Class

' Second part of class definition.
Partial Public Class Employee
    Public Sub CalculateTaxes()
    End Sub
End Class
```

## <a name="see-also"></a>Confira também

- [Classes e métodos parciais](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)
- [partial (tipo) (Referência de C#)](/dotnet/csharp/language-reference/keywords/partial-type)
- [partial (método) (Referência do C#)](/dotnet/csharp/language-reference/keywords/partial-method)
- [Parcial (Visual Basic)](/dotnet/visual-basic/language-reference/modifiers/partial)
