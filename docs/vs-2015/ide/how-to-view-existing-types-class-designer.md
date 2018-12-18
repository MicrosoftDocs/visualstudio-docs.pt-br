---
title: Como exibir tipos existentes (Designer de Classe) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.classdesigner.CannotShowBaseType
helpviewer_keywords:
- types [Visual Studio], visualizing
- types [Visual Studio], class diagrams
- class diagrams, types
ms.assetid: de110a4e-5b51-4a40-9dee-615df4d8f999
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 630902cd789fb3eec0f51ed1cfede3ae54e1ac83
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49846974"
---
# <a name="how-to-view-existing-types-class-designer"></a>Como exibir tipos existentes (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para ver um tipo existente e seus membros, adicione sua forma a um diagrama de classe.  
  
 Você pode ver tipos locais e referenciados. Um tipo local existe no projeto atualmente aberto e é leitura/gravação. Um tipo referenciado existe em outro projeto ou em um assembly referenciado e é somente leitura.  
  
 Para criar novos tipos em diagramas de classe, consulte [Como criar tipos usando o Designer de Classe](../ide/how-to-create-types-by-using-class-designer.md).  
  
### <a name="to-see-types-in-a-project-on-a-class-diagram"></a>Para ver tipos de um projeto em um diagrama de classes  
  
1. Em um projeto no Gerenciador de Soluções, abra um arquivo de diagrama de classes (.cd) existente. Ou, se não houver nenhum diagrama de classes, adicione um novo ao projeto. Consulte [Como adicionar diagramas de classe a projetos (Designer de Classe)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md).  
  
2. No projeto localizado no Gerenciador de Soluções, arraste um arquivo de código-fonte para o diagrama de classes.  
  
   > [!WARNING]
   >  Se sua solução tiver um projeto que compartilha código por vários aplicativos, você poderá arrastar arquivos ou código para um diagrama de classe apenas das seguintes fontes:  
   > 
   > - Do projeto de aplicativo que contém o diagrama  
   >   -   De um projeto compartilhado que foi importado pelo projeto de aplicativo  
   >   -   De um projeto referenciado  
   >   -   De um assembly  
  
    As formas que representam os tipos definidos no arquivo de código-fonte aparecem no diagrama na posição para a qual você arrastou o arquivo.  
  
   Também é possível exibir tipos no projeto arrastando um ou mais tipos do nó do projeto no Modo de Exibição de Classe para o diagrama de classes.  
  
> [!TIP]
>  Se o Modo de Exibição de Classe não estiver aberto, abra-o no menu **Exibir**. Para obter mais informações sobre o Modo de Exibição de Classe, consulte [Exibindo classes e seus membros](http://msdn.microsoft.com/en-us/71e9e8f3-261a-4e0c-87bf-5ec48b8bf333).  
  
 Para exibir tipos em locais padrão no diagrama, selecione um ou mais tipos no Modo de Exibição de Classe, clique com o botão direito do mouse nos tipos selecionados e escolha **Exibir Diagrama de Classe**.  
  
> [!NOTE]
>  Se um diagrama de classes fechado contendo o tipo já existir no projeto, o diagrama de classes será aberto para exibir a forma do tipo. No entanto, se nenhum diagrama de classes contiver o tipo que existe no projeto, o Designer de Classe criará um novo diagrama de classes no projeto e o abrirá para exibir o tipo.  
  
 Quando você exibe um tipo no diagrama pela primeira vez, sua forma aparece recolhida por padrão. É possível expandir a forma para exibir seu conteúdo.  
  
### <a name="to-display-the-contents-of-a-project-in-a-class-diagram"></a>Para exibir o conteúdo de um projeto em um diagrama de classe  
  
1.  No Gerenciador de Soluções ou no Modo de Exibição de Classe, clique com o botão direito do mouse no projeto e escolha **Exibir** e, em seguida, **Exibir Diagrama de Classe**.  
  
     Um Diagrama de Classe populado automaticamente é criado.  
  
## <a name="see-also"></a>Consulte também  
 [Como exibir herança entre tipos (Designer de Classe)](../ide/how-to-view-inheritance-between-types-class-designer.md)   
 [Como personalizar diagramas de classe (Designer de Classe)](../ide/how-to-customize-class-diagrams-class-designer.md)   
 [Exibindo tipos e relações (Designer de Classe)](../ide/viewing-types-and-relationships-class-designer.md)



