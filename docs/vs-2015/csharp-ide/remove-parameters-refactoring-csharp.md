---
title: Remover parâmetros refatoração (c#) | Microsoft Docs
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
- vs.csharp.refactoring.remove
dev_langs:
- CSharp
helpviewer_keywords:
- parameters [C#], removing
- refactoring [C#], Remove Parameters
- Remove Parameters refactoring [C#]
ms.assetid: f4fc3265-0ef8-4398-a691-c338178697a6
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c9559deda5c5cdc60adc10246196fb66646cfee5
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49284382"
---
# <a name="remove-parameters-refactoring-c"></a>Refatoração Remover Parâmetros (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Remove Parameters` é uma operação de refatoração que fornece uma maneira fácil de remover parâmetros de métodos, indexadores ou delegados. Remova as alterações de parâmetros a declaração; em qualquer local em que o membro é chamado, o parâmetro é removido para refletir a nova declaração.  
  
 Você executar a operação de remover parâmetros pelo primeiro posicionando o cursor em um método, indexador ou delegado. Enquanto o cursor estiver na posição, para invocar o remova `Parameters` operação, clique em de **refatorar** menu, pressione o atalho de teclado, ou selecione o comando no menu de atalho.  
  
> [!NOTE]
>  É possível remover o primeiro parâmetro em um método de extensão.  
  
### <a name="to-remove-parameters"></a>Para remover parâmetros  
  
1.  Crie um aplicativo de console chamado `RemoveParameters`e, em seguida, substitua `Program` com o código a seguir.  
  
    ```csharp  
    class A  
    {  
        // Invoke on 'A'.  
        public A(string s, int i) { }  
    }  
  
    class B  
    {  
        void C()  
        {  
            // Invoke on 'A'.  
            A a = new A("a", 2);  
        }  
    }  
    ```  
  
2.  Coloque o cursor no método `A`, na declaração de método ou a chamada de método.  
  
3.  Dos **refatorar** menu, selecione **remover parâmetros** para exibir o **remover parâmetros** caixa de diálogo.  
  
     Você também pode digitar o atalho de teclado CTRL + R, V para exibir o **remover parâmetros** caixa de diálogo.  
  
     Você pode também com o botão direito no cursor, aponte para **refatorar**e, em seguida, clique em **remover parâmetros** para exibir o **remover parâmetros** caixa de diálogo.  
  
4.  Usando o **parâmetros** campo, posicione o cursor na `int i`e, em seguida, clique em **remover**.  
  
5.  Clique em **OK**.  
  
6.  No **visualizar alterações — remover parâmetros** caixa de diálogo, clique em **aplicar**.  
  
## <a name="remarks"></a>Comentários  
 Você pode remover os parâmetros de uma declaração de método ou uma chamada de método. Posicione o cursor no nome do método declaração ou delegado e invocar remover parâmetros.  
  
> [!CAUTION]
>  Remova habilita parâmetros que você remova um parâmetro que é referenciado no corpo de membro, mas não remove as referências para esse parâmetro no corpo do método. Isso pode introduzir erros de compilação em seu código. No entanto, você pode usar o **visualizar alterações** caixa de diálogo para revisar seu código antes de executar a operação de refatoração.  
  
 Se um parâmetro que está sendo removido é modificado durante a chamada para um método, a remoção do parâmetro também removerá a modificação. Por exemplo, se uma chamada de método é alterada de  
  
```csharp  
MyMethod(param1++, param2);  
```  
  
 para  
  
```csharp  
MyMethod(param2);  
```  
  
 Por que a operação de refatoração, `param1` não será incrementada.  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)