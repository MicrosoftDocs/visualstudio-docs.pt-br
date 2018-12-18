---
title: Refatorando classes e tipos (Designer de Classe) | Microsoft Docs
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
- vs.ClassDesigner.OverrideMembersDialog
helpviewer_keywords:
- members, overriding
- overriding members
- classes [Visual Studio], refactoring
- type members, overriding
- refactoring, types
- types [Visual Studio], refactoring
- Class Designer [Visual Studio], refactoring classes
- refactoring, classes
ms.assetid: dcf07bb4-fa3b-4224-9dec-566fd924a8ce
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 215030b511ecbddbda23073df464035887f8ef95
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49207955"
---
# <a name="refactoring-classes-and-types-class-designer"></a>Refatorando classes e tipos (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você refatora o código, ele fica mais fácil de entender, manter e mais eficiente, alterando a estrutura interna e como os seus objetos são criados, não o comportamento externo dele. Use o Designer de Classe e a janela Detalhes da Classe para reduzir o trabalho que é necessário e a possibilidade de introduzir bugs quando você refatora o código do Visual C# .NET, Visual Basic .NET ou C++ em seu projeto do Visual Studio.  
  
> [!NOTE]
>  Os arquivos de um projeto podem ser somente leitura porque o projeto está sob controle do código-fonte e não está submetido a check-out, ele é um projeto referenciado ou seus arquivos são marcados como somente leitura no disco. Quando você trabalha em um projeto em um desses estados, você tem várias maneiras de salvar o trabalho, dependendo do estado do projeto. Isso se aplica ao código de refatoração e também ao código que você altera de outra forma, como editando-o diretamente. Para obter mais informações, consulte [Exibição de informações somente leitura (Designer de Classe)](http://msdn.microsoft.com/en-us/33e2d3a9-1668-4d10-ae56-fa09b3156e0a).  
  
## <a name="common-tasks"></a>Tarefas comuns  
  
|Tarefa|Conteúdo de suporte|  
|----------|------------------------|  
|**Classes de refatoração:** você pode usar as operações de refatoração para dividir uma classe em classes parciais ou para implementar uma classe base abstrata.|-   [Como dividir uma classe em classes parciais (Designer de Classe)](../ide/how-to-split-a-class-into-partial-classes-class-designer.md)|  
|**Trabalho com interfaces:** no Designer de Classe, você pode implementar uma interface no diagrama de classe se ela for conectada a uma classe que fornece o código para os métodos de interface.|-   [Como implementar uma interface (Designer de Classe)](../ide/how-to-implement-an-interface-class-designer.md)|  
|**Refatoração de tipos, membros de tipo e parâmetros:** usando o Designer de Classe, você pode renomear tipos, substituir membros de tipo ou movê-los de um tipo para outro. Você também pode criar tipos que permitem valor nulo.|-   [Renomeando tipos e membros de tipo](../ide/refactoring-classes-and-types-class-designer.md#RenamingTypesAndMembers)<br />-   [Como mover membros de tipo de um tipo para o outro](../ide/refactoring-classes-and-types-class-designer.md#MovingTypeMembers)<br />-   [Como criar um tipo que permite valor nulo (Designer de Classe)](../ide/how-to-create-a-nullable-type-class-designer.md)|  
  
###  <a name="RenamingTypesAndMembers"></a> Renomeando tipos e membros de tipo  
 No Designer de Classe, você pode renomear um tipo ou um membro de um tipo no diagrama de classe ou na janela Propriedades. Na janela Detalhes da Classe, você pode alterar o nome de um membro, mas não um tipo. A renomeação de um tipo ou membro do tipo propaga para todas as janelas e locais de código onde o nome antigo é exibido.  
  
##### <a name="to-rename-a-name-in-the-class-designer"></a>Para renomear um nome no Designer de Classe  
  
1.  No diagrama de classe, selecione o tipo ou membro e clique no nome.  
  
     O nome do membro se torna editável.  
  
2.  Digite o novo nome do tipo ou membro do tipo  
  
##### <a name="to-rename-a-name-in-the-class-details-window"></a>Para renomear um nome na janela Detalhes da Classe  
  
1.  Para exibir a janela Detalhes da Classe, clique com o botão direito do mouse no tipo ou membro de tipo e clique em **Detalhes da Classe**.  
  
     A janela Detalhes da Classe é exibida.  
  
2.  Na coluna **Nome**, altere o nome do membro de tipo  
  
3.  Para mover o foco da célula, pressione a tecla **ENTER** ou clique fora da célula.  
  
    > [!NOTE]
    >  Na janela Detalhes da Classe, você pode alterar o nome de um membro, mas não um tipo.  
  
##### <a name="to-rename-a-name-in-the-properties-window"></a>Para mudar um nome na janela Propriedades  
  
1.  No diagrama de classe ou na janela Detalhes da Classe, clique com o botão direito do mouse no tipo ou membro e clique em **Propriedades**.  
  
     A janela Propriedades aparece e exibe as propriedades do tipo ou membro do tipo.  
  
2.  Na propriedade **Nome**, altere o nome do tipo ou do membro de tipo.  
  
     O novo nome propagada para todas as janelas e locais de código no projeto atual em que o nome antigo é exibido.  
  
###  <a name="MovingTypeMembers"></a> Movendo membros de um tipo para o outro  
 Usando o **Designer de Classe**, você poderá mover um membro de tipo de um tipo para outro, se ambos estiverem visíveis no diagrama de classe atual.  
  
##### <a name="to-move-a-type-member-from-one-type-to-another"></a>Para mover um membro de um tipo para o outro  
  
1.  Em um tipo que visível no modo de design, clique com o botão direito do mouse sobre o membro que você deseja mover para o outro tipo e clique em **Recortar**.  
  
2.  Clique com o botão direito do mouse no tipo de destino e clique em **Colar**.  
  
     A propriedade é removida do tipo de origem e aparece no tipo de destino.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Exibindo tipos e relações (Designer de Classe)](../ide/viewing-types-and-relationships-class-designer.md)||  
|[Projetando classes e tipos (Designer de Classe)](../ide/designing-classes-and-types-class-designer.md)||



