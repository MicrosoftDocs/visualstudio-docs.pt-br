---
title: Como adicionar diagramas de classes a projetos (Designer de Classe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- class diagrams, creating
- Class Designer [Visual Studio], opening
ms.assetid: 0eac1b54-2711-4e4b-9654-a0c429c08c8f
caps.latest.revision: 43
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f1a0d10dabdace7ef7ab3805a59b892548cf6556
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "72645527"
---
# <a name="how-to-add-class-diagrams-to-projects-class-designer"></a>Como adicionar diagramas de classe a projetos (Designer de Classe)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Para projetar, editar e refatorar classes e outros tipos, adicione um diagrama de classe ao seu projeto Visual C# .NET, Visual Basic .NET ou C++. Para visualizar diferentes partes do código em um projeto, adicione vários diagramas de classes ao projeto.

 Não é possível criar diagramas de classes a partir de projetos que compartilham o código por meio de diversos aplicativos. Para criar diagramas de classe UML, consulte [Criar diagramas e projetos de modelagem UML](../modeling/create-uml-modeling-projects-and-diagrams.md).

### <a name="to-add-a-blank-class-diagram-to-a-project"></a>Para adicionar um diagrama de classes em branco a um projeto

1. No Gerenciador de Solução, clique no nome do projeto. Escolha **Adicionar Novo Item** ou **Adicionar**, **Novo Item**.

2. Na lista de modelos, escolha o **Diagrama de Classe**. Para projetos do Visual C++, procure em **Modelos** e em **Utilitário** para localizar esse modelo.

     O diagrama de classes é aberto no Designer de Classe e aparece como um arquivo que possui uma extensão .cd no Gerenciador de Soluções na hierarquia do projeto. Use a caixa de ferramentas Designer da Classe para arrastar formas e linhas até o diagrama.

3. Para adicionar vários diagramas de classes, repita as etapas deste procedimento.

### <a name="to-add-a-class-diagram-based-on-existing-types"></a>Para adicionar um diagrama de classes com base em tipos existentes

1. No Gerenciador de Soluções, abra o menu de contexto do arquivo de classe e escolha **Exibir em Diagrama de Classe**.

     - ou -

     Em **Modo de Exibição de Classe**, abra o namespace ou o menu de contexto de tipo e escolha **Exibir em Diagrama de Classe**.

### <a name="to-display-the-contents-of-a-complete-project-in-a-class-diagram"></a>Para exibir o conteúdo de um projeto completo em um diagrama de classe

1. No Gerenciador de Soluções ou no Modo de Exibição de Classe, clique com o botão direito do mouse no projeto e escolha **Exibir** e, em seguida, **Exibir Diagrama de Classe**.

     Um Diagrama de Classe populado automaticamente é criado.

## <a name="see-also"></a>Consulte Também
 [Como: criar tipos usando Designer de classe](../ide/how-to-create-types-by-using-class-designer.md) [como exibir tipos existentes (Designer de classe)](../ide/how-to-view-existing-types-class-designer.md) [criando classes e tipos (Designer de classe)](../ide/designing-classes-and-types-class-designer.md) [exibindo tipos e relações (Designer de classe)](../ide/viewing-types-and-relationships-class-designer.md) que [trabalham com diagramas de classe (Designer de classe)](../ide/working-with-class-diagrams-class-designer.md)
