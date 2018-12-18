---
title: Extrair Interface refatoração (c#) | Microsoft Docs
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
- vs.csharp.refactoring.extractinterface
dev_langs:
- CSharp
helpviewer_keywords:
- refactoring [C#], Extract Interface
- Extract Interface refactoring operation [C#]
ms.assetid: 7d0aa225-3b33-4331-9652-5a67cac6f3d0
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: e7c3af675155cf3d47d82457aadbfb6327895d4f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49279897"
---
# <a name="extract-interface-refactoring-c"></a>Refatoração Extrair Interface (C#)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extrair Interface é uma operação de refatoração que fornece uma maneira fácil de criar uma nova interface com os membros que se originam em uma classe existente, struct ou interface.  
  
 Quando vários clientes usam o mesmo subconjunto de membros de uma classe, struct ou interface, ou várias classes, structs ou interfaces têm um subconjunto de membros em comum, pode ser útil incorporar o subconjunto de membros em uma interface. Para obter mais informações sobre como usar interfaces, consulte [Interfaces](http://msdn.microsoft.com/library/2feda177-ce11-432d-81b4-d50f5f35fd37).  
  
 Extrair Interface gera uma interface em um novo arquivo e posiciona o cursor no início do novo arquivo. Você pode especificar quais membros para extrair para a nova interface, o nome da nova interface e o nome do arquivo gerado usando o **extrair Interface** caixa de diálogo.  
  
### <a name="to-use-extract-interface"></a>Usar extrair Interface  
  
1.  Crie um aplicativo de console chamado `ExtractInterface`e, em seguida, substitua `Program` com o código a seguir  
  
    ```csharp  
    // Invoke Extract Interface on ProtoA.  
    // Note:  the extracted interface will be created in a new file.  
    class ProtoA  
    {  
        public void MethodB(string s) { }  
    }  
    ```  
  
2.  Com o cursor posicionado no `MethodB`e clique em **extrair Interface** sobre o **refatorar** menu.  
  
     O **extrair Interface** caixa de diálogo é exibida.  
  
     Você também pode digitar o atalho de teclado CTRL + R, posso exibir o **extrair Interface** caixa de diálogo.  
  
     Você pode também com o botão direito do mouse, aponte para **refatorar**e, em seguida, clique em **extrair Interface** para exibir o **extrair Interface** caixa de diálogo.  
  
3.  Clique em **Selecionar tudo**.  
  
4.  Clique em **OK**.  
  
     Você verá o novo arquivo, IProtoA.cs e o código a seguir:  
  
    ```csharp  
    using System;  
    namespace TopThreeRefactorings  
    {  
        interface IProtoA  
        {  
            void MethodB(string s);  
        }  
    }  
    ```  
  
## <a name="remarks"></a>Comentários  
 Esse recurso só é acessível quando o cursor é posicionado na classe, struct ou interface que contém os membros que você deseja extrair. Quando o cursor está nessa posição, invocar a operação de refatoração Extrair Interface.  
  
 Quando você invoca extrair interface em uma classe ou em um struct, a lista de bases e interfaces é modificada para incluir o nome da nova interface. Quando você invoca extrair interface em uma interface, a lista de bases e interfaces não é modificada.  
  
## <a name="see-also"></a>Consulte também  
 [Refatoração (C#)](../csharp-ide/refactoring-csharp.md)