---
title: Criar elementos e relações em modelos UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API
ms.assetid: cae81d32-8cc7-4f7c-9f00-20119952bc51
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 5ed918bc96168196400dd34d87ec65574fdfc5b6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51785866"
---
# <a name="create-elements-and-relationships-in-uml-models"></a>Criar elementos e relações em modelos UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No código do programa para uma extensão do Visual Studio, você pode criar e excluir elementos e relações.  
  
## <a name="create-a-model-element"></a>Criar um elemento de modelo  
  
### <a name="namespace-imports"></a>Importações de Namespace  
 Você deve incluir o seguinte `using` instruções.  
  
 Os métodos de criação são definidos como métodos de extensão nesse namespace:  
  
 `using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;`  
  
### <a name="obtain-the-owner-of-the-element-you-want-to-create"></a>Obter o proprietário do elemento que você deseja criar  
 Um modelo de forma uma única árvore, para que cada item tem um proprietário, exceto para a raiz do modelo. A raiz do modelo é do tipo `IModel`, que é um tipo de `IPackage`.  
  
 Se você estiver criando um elemento que será exibido em um diagrama específico, por exemplo, diagrama de atual do usuário, você deve geralmente criá-la no pacote que está vinculado a esse diagrama. Por exemplo:  
  
```  
IPackage linkedPackage = Context.CurrentDiagram.Element as IPackage;  
```  
  
 Esta tabela resume a propriedade dos elementos de modelo comuns:  
  
|Elemento a ser criado|Proprietário|  
|---------------------------|-----------|  
|`IActor, IUseCase, IComponent, IClass, IInterface, IEnumeration`<br /><br /> `IActivity, IInteraction`|`IPackage, IModel`|  
|`IAttribute, IOperation`|`IClass, IInterface`|  
|`IPart, IPort`|`IComponent`|  
|`IAction, IObjectNode`|`IActivity`|  
|`ILifeline, IMessage, ICombinedFragment`|`IInteraction`|  
  
### <a name="invoke-the-create-method-on-the-owner"></a>Invocar o método Create no proprietário  
 O nome do método está no formato: `Create` *OwnedType*`()`. Por exemplo:  
  
```  
IUseCase usecase1 = linkedPackage.CreateUseCase();  
```  
  
 Alguns tipos têm métodos de criação mais complexos, especialmente em diagramas de sequência. Ver [diagramas de sequência UML Editar usando a API UML](../modeling/edit-uml-sequence-diagrams-by-using-the-uml-api.md).  
  
 Para alguns tipos de elemento, você pode alterar o proprietário de um elemento durante seu ciclo de vida usando `SetOwner(newOwner)`.  
  
### <a name="set-the-name-and-other-properties"></a>Definir o nome e outras propriedades  
  
```  
usecase1.Name = "user logs in";  
```  
  
### <a name="example"></a>Exemplo  
  
```  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.Uml.Extensions;  
...  
 void InstantiateObserverPattern (IPackage package, string namePrefix)  
 {    IInterface observer = package.CreateInterface();  
      observer.Name = namePrefix + "Observer";  
      IOperation operation = observer.CreateOperation();  
      operation.Name = "Update";  
      IClass subject = package.CreateClass();  
      subject.Name = namePrefix + "Subject"; ...  
```  
  
## <a name="create-an-association"></a>Criar uma associação  
  
#### <a name="to-create-an-association"></a>Para criar uma associação  
  
1.  Obter o proprietário da associação, que geralmente é o pacote ou modelo que contém o fim da origem da relação.  
  
2.  Invoca o método Create necessário no proprietário.  
  
3.  Defina as propriedades da relação, como seu nome.  
  
     Por exemplo:  
  
    ```  
    IAssociation association = subject.Package.CreateAssociation(subject, observer);  
    association .Name = "Observes";  
    ```  
  
4.  Defina as propriedades de cada extremidade da relação. Sempre há dois `MemberEnds`. Por exemplo:  
  
    ```  
    association .MemberEnds[0].Name = "subject";   // role name  
    association .MemberEnds[1].Name = "observers"; // role name  
    association .MemberEnds[1].SetBounds("0..*");           
                // multiplicity defaults to "1"  
    association.MemberEnds[0].Aggregation = AggregationKind.Composite;  
    ```  
  
## <a name="create-a-generalization"></a>Criar uma generalização  
  
```  
IGeneralization generalization =   
  subclass.CreateGeneralization(superClass);  
```  
  
## <a name="delete-an-element-relationship-or-generalization-from-the-model"></a>Excluir um elemento, relação ou generalização do modelo  
  
```  
anElement.Delete();  
```  
  
 Quando você exclui um elemento de um modelo:  
  
-   Todo relacionamento que vincula-se a ele também é excluído.  
  
-   Todas as formas que representado-lo em um diagrama também é excluída.  
  
## <a name="see-also"></a>Consulte também  
 [Estender modelos e diagramas UML](../modeling/extend-uml-models-and-diagrams.md)   
 [Exibir um modelo UML em diagramas](../modeling/display-a-uml-model-on-diagrams.md)



