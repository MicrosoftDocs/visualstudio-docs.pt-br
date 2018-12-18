---
title: Reordenar parâmetros refatoração (c#) | Microsoft Docs
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
- vs.csharp.refactoring.reorder
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Reorder Parameters
- Reorder Parameters refactoring [C#]
ms.assetid: 4dabf21a-a9f0-41e9-b11b-55760cf2bd90
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 03316fba63267a4eb7fc3b59c8f6823d3678b438
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49273098"
---
# <a name="reorder-parameters-refactoring-c"></a>Refatoração Reordenar Parâmetros (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`Reorder Parameters` é um Visual C# operação de refatoração que fornece uma maneira fácil de alterar a ordem dos parâmetros para métodos, indexadores e delegados. `Reorder Parameters` Altera a declaração, e em qualquer local em que o membro é chamado, os parâmetros serão reorganizados para refletir a nova ordem.  
  
 Para executar o `Reorder Parameters` operação, coloque o cursor na ou ao lado de um método, indexador ou delegado. Quando o cursor estiver na posição, invoque o `Reorder Parameters` operação pressionando o atalho de teclado ou clicando no comando no menu de atalho.  
  
> [!NOTE]
>  Você não é possível reorganizar o primeiro parâmetro em um método de extensão.  
  
### <a name="to-reorder-parameters"></a>Para reordenar parâmetros  
  
1.  Criar uma biblioteca de classe chamada `ReorderParameters`e, em seguida, substitua `Class1` com o código de exemplo a seguir.  
  
    ```csharp  
    class ProtoClassA  
    {  
        // Invoke on 'MethodB'.  
        public void MethodB(int i, bool b) { }  
    }  
  
    class ProtoClassC  
    {  
        void D()  
        {  
            ProtoClassA MyClassA = new ProtoClassA();  
  
            // Invoke on 'MethodB'.  
            MyClassA.MethodB(0, false);  
        }  
    }  
    ```  
  
2.  Coloque o cursor em `MethodB`, na declaração de método ou a chamada de método.  
  
3.  Sobre o **refatorar** menu, clique em **reordenar parâmetros**.  
  
     O **reordenar parâmetros** caixa de diálogo é exibida.  
  
4.  No **reordenar parâmetros** caixa de diálogo, selecione `int i` no **parâmetros** lista e, em seguida, clique no botão para baixo.  
  
     Como alternativa, você pode arrastar `int i` após `bool b` na **parâmetros** lista.  
  
5.  No **reordenar parâmetros** caixa de diálogo, clique em **Okey**.  
  
     Se o **visualizar alterações de referência** opção for selecionada na **reordenar parâmetros** caixa de diálogo, o **visualizar alterações - reordenar parâmetros** caixa de diálogo será exibida. Ele fornece uma visualização das alterações na lista de parâmetros para `MethodB` na assinatura do e a chamada de método.  
  
    1.  Se o **visualizar alterações - reordenar parâmetros** caixa de diálogo for exibida, clique em **aplicar**.  
  
         Neste exemplo, a declaração do método e todas as o chamada de método sites para `MethodB` são atualizados.  
  
## <a name="remarks"></a>Comentários  
 Você pode reordenar parâmetros de uma declaração de método ou uma chamada de método. Posicione o cursor em ou próximo a declaração de método ou delegate, mas não no corpo.  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)