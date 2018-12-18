---
title: Vincular atualizações de modelo UML usando transações | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API, transactions
ms.assetid: a1df6c38-a3d1-4a3f-82bc-c8f363ab916e
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: fb8bb5dfd5238871324b786f120d618d70f14b43
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51800400"
---
# <a name="link-uml-model-updates-by-using-transactions"></a>Vincular atualizações de modelo UML usando transações
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você define uma extensão para os designers UML no Visual Studio, você pode agrupar várias alterações em uma única transação chamada um *contexto de desfazer vinculado*. Para ver quais versões do Visual Studio dão suporte a modelos UML, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
 Por padrão, cada modificação que seu código faz em um modelo pode ser desfeita separadamente pelo usuário. Por exemplo, se você definir um comando de menu que alterna os nomes de duas classes UML, um usuário pode invocar o comando e, em seguida, execute um Desfazer. Isso desfaria a alteração para um nome, mas não em outro, deixando seu modelo em um estado não intencional.  
  
 Para evitar isso, seu código pode executar uma série de alterações em uma transação. Isso faz com que as alterações se parecer com uma única alteração para o usuário. Um comando subsequente desfazer desfazerá a série inteira.  
  
 Um benefício adicional é que seu código pode desfazer um conjunto parcial / completamente de alterações, lançando uma exceção ou anulando a transação.  
  
## <a name="to-group-changes-into-a-single-transaction"></a>Para agrupar alterações em uma única transação  
 Certifique-se de que as referências do projeto incluam esse assembly do .NET:  
  
 **Microsoft.VisualStudio.Modeling.Sdk. . dll de [versão]**  
  
 Dentro de sua classe, declare uma propriedade importada que tem o tipo <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ILinkedUndoContext>:  
  
 `using Microsoft.VisualStudio.Modeling.ExtensionEnablement;`  
  
 `...`  
  
 `class … {`  
  
 `[Import]`  
  
 `public ILinkedUndoContext LinkedUndoContext { get; set; }`  
  
 Em um método que altera o modelo, inclua suas alterações em uma transação:  
  
 `using (ILinkedUndoTransaction transaction =`  
  
 `LinkedUndoContext.BeginTransaction("my updates"))`  
  
 `{`  
  
 `// code to update model elements or shapes goes here`  
  
 `transaction.Commit();`  
  
 `}`  
  
 Observe o seguinte:  
  
-   Você sempre deve incluir `Commit()` no final da transação. Se uma transação for descartada sem ser confirmada, a transação será revertida. Ou seja, o modelo será restaurado ao estado no início da transação.  
  
-   Se ocorrer uma exceção que não é capturada dentro da transação, a transação será revertida. É um padrão frequente para incluir a `using` bloco de transação dentro um `try…catch` bloco.  
  
-   Você pode aninhar transações.  
  
-   Você pode fornecer qualquer nome não em branco para `BeginTransaction()`.  
  
-   Somente o Store de modelo UML é afetado por essas transações. Modelagem de transações não afeta: variáveis, armazenamentos externos, como arquivos e bancos de dados, diagramas de camada e modelos de código.  
  
## <a name="example"></a>Exemplo  
  
```  
    using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
    using Microsoft.VisualStudio.Uml.Interfaces;  
    using Microsoft.VisualStudio.Uml.Classes;  
    using Microsoft.VisualStudio.Uml.Extensions;  
    using System.Linq;  
    using System.ComponentModel.Composition;  
 ...  
  [Import]  
  public ILinkedUndoContext LinkedUndoContext { get; set; }  
  
  /// <summary>  
  /// Swap the names of the currently selected elements.  
  /// </summary>  
  public void Execute(IMenuCommand command)  
  {  
    var selectedShapes =  
      Context.CurrentDiagram.GetSelectedShapes<IClassifier>();  
    if (selectedShapes.Count() < 2) return;  
    IClassifier firstElement = selectedShapes.First().Element;  
    IClassifier lastElement = selectedShapes.Last().Element;  
    string firstName = firstElement.Name;  
    // Perform changes inside a transaction so that undo  
    // works as a single change.  
    using (ILinkedUndoTransaction transaction =   
      LinkedUndoContext.BeginTransaction("Swap names"))  
    {  
        firstElement.Name = lastElement.Name;  
        lastElement.Name = firstName;  
        transaction.Commit();  
    }  
 }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)   
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)



