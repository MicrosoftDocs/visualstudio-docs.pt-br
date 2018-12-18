---
title: Encapsular campo refatoração (c#) | Microsoft Docs
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
- vs.csharp.refactoring.encapsulatefield
dev_langs:
- CSharp
helpviewer_keywords:
- Encapsulate Field refactoring operation [C#]
- refactoring [C#], Encapsulate Field
ms.assetid: bf714a04-ab1e-49ce-99ce-dda1ebb1a17f
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 35d7e03e30aa5301ee65f15a8591fbccd1de3fcd
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49223531"
---
# <a name="encapsulate-field-refactoring-c"></a>Refatoração Encapsular Campo (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O **encapsular campo** operação de refatoração permite criar rapidamente uma propriedade de um campo existente e, em seguida, atualize seu código perfeitamente com as referências para a nova propriedade.  
  
 Quando um [campo](http://msdn.microsoft.com/library/3cbb2f61-75f8-4cce-b4ef-f5d1b3de0db7) é [público](http://msdn.microsoft.com/library/0ae45d16-a551-4b74-9845-57208de1328e), outros objetos têm acesso direto a esse campo e pode modificá-lo, sem ser detectado pelo objeto que possui esse campo. Usando [propriedades](http://msdn.microsoft.com/library/e295a8a2-b357-4ee7-a12e-385a44146fa8) para encapsular esse campo, você pode proibir o acesso direto aos campos.  
  
 Para criar a nova propriedade, o **encapsular campo** operação altera o modificador de acesso para o campo que você deseja encapsular a [privada](http://msdn.microsoft.com/library/654c0bb8-e6ac-4086-bf96-7474fa6aa1c8)e, em seguida, gera [obter](http://msdn.microsoft.com/library/a52de048-fbe0-41b0-82ec-8e4ac04d3a71)e [definir](http://msdn.microsoft.com/library/30d7e4e5-cc2e-4635-a597-14a724879619) acessadores para esse campo. Em alguns casos, somente um `get` acessador é gerado, como quando o campo é declarado como somente leitura.  
  
 O mecanismo de refatoração atualiza seu código com as referências para a nova propriedade nas áreas especificadas na **referências de atualização** seção o **encapsular campo** caixa de diálogo.  
  
### <a name="to-create-a-property-from-a-field"></a>Para criar uma propriedade de um campo  
  
1.  Crie um aplicativo de console chamado `EncapsulateFieldExample`e, em seguida, substitua `Program` com o código de exemplo a seguir.  
  
    ```csharp  
    class Square  
    {  
        // Select the word 'width' and then use Encapsulate Field.  
        public int width, height;  
    }  
    class MainClass  
    {  
        public static void Main()  
        {  
            Square mySquare = new Square();  
            mySquare.width = 110;  
            mySquare.height = 150;  
            // Output values for width and height.  
            Console.WriteLine("width = {0}", mySquare.width);  
            Console.WriteLine("height = {0}", mySquare.height);  
        }  
    }  
    ```  
  
2.  No [Editor de códigos](../ide/writing-code-in-the-code-and-text-editor.md), coloque o cursor na declaração, no nome do campo que você deseja encapsular. No exemplo a seguir, coloque o cursor na palavra `width`:  
  
    ```csharp  
    public int width, height;  
    ```  
  
3.  Sobre o **refatorar** menu, clique em **encapsular campo**.  
  
     O **encapsular campo** caixa de diálogo é exibida.  
  
     Você também pode digitar o atalho de teclado CTRL + R, E para exibir o **encapsular campo** caixa de diálogo.  
  
     Você pode também com o botão direito no cursor, aponte para **refatorar**e, em seguida, clique em **encapsular campo** para exibir o **encapsular campo** caixa de diálogo.  
  
4.  Especifique as configurações.  
  
5.  Pressione ENTER ou clique a **Okey** botão.  
  
6.  Se você tiver selecionado a **visualizar alterações de referência** opção, em seguida, a **visualizar alterações de referência** janela é aberta. Clique o **aplicar** botão.  
  
     O seguinte `get` e `set` código de acessador é exibido em seu arquivo de origem:  
  
    ```csharp  
    public int Width  
    {  
        get { return width; }  
        set { width = value; }  
    }  
    ```  
  
     O código a `Main` método também é atualizado para o novo `Width` nome da propriedade.  
  
    ```csharp  
    Square mySquare = new Square();  
    mySquare.Width = 110;  
    mySquare.height = 150;  
    // Output values for width and height.  
    Console.WriteLine("width = {0}", mySquare.Width);  
    ```  
  
## <a name="remarks"></a>Comentários  
 O **encapsular campo** operação só é possível quando o cursor é posicionado na mesma linha da declaração do campo.  
  
 Para as declarações que declarar vários campos, **encapsular campo** usa a vírgula como um limite entre os campos e inicia a refatoração no campo que é o mais próximo do cursor e na mesma linha do cursor. Você também pode especificar qual campo que você deseja encapsular, selecionando o nome do campo na declaração.  
  
 O código que é gerado por esta operação de refatoração é modelado pelo recurso de trechos de código de encapsular campo. Os snippets de código são modificáveis. Para obter mais informações, consulte [Snippets de Código](../ide/code-snippets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)   
 [Snippets de código do Visual C#](../ide/visual-csharp-code-snippets.md)