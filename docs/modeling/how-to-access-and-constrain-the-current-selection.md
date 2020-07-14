---
title: Como acessar e restringir a seleção atual
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Domain-Specific Language, accessing the current selection
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b1f5aaa106e00f9b10eb88892bcc978b92a01c79
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545685"
---
# <a name="how-to-access-and-constrain-the-current-selection"></a>Como acessar e restringir a seleção atual

Ao escrever um comando ou manipulador de gestos para sua linguagem específica de domínio, você pode determinar em qual elemento o usuário clicou com o botão direito do mouse. Você também pode impedir que algumas formas ou campos sejam selecionados. Por exemplo, você pode organizar isso quando o usuário clica em um decorador de ícone, a forma que o contém é selecionada. Restringir a seleção dessa maneira reduz o número de manipuladores que você precisa escrever. Ele também torna mais fácil para o usuário, quem pode clicar em qualquer lugar na forma sem precisar evitar o decorador.

## <a name="access-the-current-selection-from-a-command-handler"></a>Acessar a seleção atual de um manipulador de comandos

A classe do conjunto de comandos para uma linguagem específica de domínio contém os manipuladores de comando para seus comandos personalizados. A <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> classe, da qual a classe do conjunto de comandos para uma linguagem específica de domínio deriva, fornece alguns membros para acessar a seleção atual.

Dependendo do comando, o manipulador de comandos pode precisar da seleção no designer de modelos, no Gerenciador de modelos ou na janela ativa.

### <a name="to-access-selection-information"></a>Para acessar informações de seleção

1. A <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> classe define os membros a seguir que podem ser usados para acessar a seleção atual.

    |Membro|Descrição|
    |-|-|
    |Método <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsAnyDocumentSelectionCompartment%2A>|Retorna `true` se qualquer um dos elementos selecionados no designer de modelo for uma forma de compartimento; caso contrário, `false` .|
    |Método <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsDiagramSelected%2A>|Retorna `true` se o diagrama está selecionado no designer de modelo; caso contrário, `false` .|
    |Método <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleDocumentSelection%2A>|Retorna `true` se exatamente um elemento for selecionado no designer de modelo; caso contrário, `false` .|
    |Método <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.IsSingleSelection%2A>|Retorna `true` se exatamente um elemento for selecionado na janela ativa; caso contrário, `false` .|
    |Propriedade <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentDocumentSelection%2A>|Obtém uma coleção somente leitura dos elementos selecionados no designer de modelo.|
    |Propriedade <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.CurrentSelection%2A>|Obtém uma coleção somente leitura dos elementos selecionados na janela ativa.|
    |Propriedade <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleDocumentSelection%2A>|Obtém o elemento principal da seleção no designer de modelo.|
    |Propriedade <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.SingleSelection%2A>|Obtém o elemento principal da seleção na janela ativa.|

2. A <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet.CurrentDocView%2A> propriedade da <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> classe fornece acesso ao <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView> objeto que representa a janela do designer de modelo e fornece acesso adicional aos elementos selecionados no designer de modelo.

3. Além disso, o código gerado define uma propriedade de janela de ferramenta do Explorer e uma propriedade de seleção do Explorer na classe do conjunto de comandos para a linguagem específica do domínio.

    - A propriedade janela de ferramentas do Gerenciador retorna uma instância da classe da janela de ferramentas do Explorer para a linguagem específica do domínio. A classe da janela de ferramentas do Explorer deriva da <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow> classe e representa o Gerenciador de modelos para a linguagem específica do domínio.

    - A `ExplorerSelection` propriedade retorna o elemento selecionado na janela Gerenciador de modelos para a linguagem específica do domínio.

## <a name="determine-which-window-is-active"></a>Determinar qual janela está ativa

A <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> interface contém membros que fornecem acesso ao estado de seleção atual no Shell. Você pode obter um <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> objeto da classe Package ou da classe set de comando para a linguagem específica do domínio por meio da `MonitorSelection` propriedade definida na classe base de cada. A classe de pacote deriva da <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage> classe e a classe de conjunto de comandos deriva da <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> classe.

### <a name="to-determine-from-a-command-handler-what-type-of-window-is-active"></a>Para determinar a partir de um manipulador de comandos que tipo de janela está ativo

1. A <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSetLibrary.MonitorSelection%2A> propriedade da <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet> classe retorna um <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> objeto que fornece acesso ao estado de seleção atual no Shell.

2. A <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService.CurrentSelectionContainer%2A> propriedade da <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService> interface Obtém o contêiner de seleção ativa, que pode ser diferente da janela ativa.

3. Adicione as propriedades a seguir à classe do conjunto de comandos para a linguagem específica do domínio para determinar qual tipo de janela está ativo.

    ```csharp
    // using Microsoft.VisualStudio.Modeling.Shell;

    // Returns true if the model designer is the active selection container;
    // otherwise, false.
    protected bool IsDesignerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is DiagramDocView);
        }
    }

    // Returns true if the model explorer is the active selection container;
    // otherwise, false.
    protected bool IsExplorerActive
    {
        get
        {
            return (this.MonitorSelection.CurrentSelectionContainer
                is ModelExplorerToolWindow);
        }
    }
    ```

## <a name="constrain-the-selection"></a>Restringir a seleção

Ao adicionar regras de seleção, você pode controlar quais elementos são selecionados quando o usuário seleciona um elemento no modelo. Por exemplo, para permitir que o usuário trate um número de elementos como uma única unidade, você pode usar uma regra de seleção.

### <a name="to-create-a-selection-rule"></a>Para criar uma regra de seleção

1. Criar um arquivo de código personalizado no projeto DSL

2. Defina uma classe de regra de seleção que seja derivada da <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules> classe.

3. Substitua o <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules.GetCompliantSelection%2A> método da classe de regra de seleção para aplicar os critérios de seleção.

4. Adicione uma definição de classe parcial para a classe ClassDiagram ao seu arquivo de código personalizado.

     A `ClassDiagram` classe deriva da <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram> classe e é definida no arquivo de código gerado, Diagram.cs, no projeto DSL.

5. Substitua a <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> propriedade da `ClassDiagram` classe para retornar a regra de seleção personalizada.

     A implementação padrão da <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.SelectionRules%2A> propriedade Obtém um objeto de regra de seleção que não modifica a seleção.

### <a name="example"></a>Exemplo

O arquivo de código a seguir cria uma regra de seleção que expande a seleção para incluir todas as instâncias de cada uma das formas de domínio inicialmente selecionadas.

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;

namespace CompanyName.ProductName.GroupingDsl
{
    public class CustomSelectionRules : DiagramSelectionRules
    {
        protected Diagram diagram;
        protected IElementDirectory elementDirectory;

        public CustomSelectionRules(Diagram diagram)
        {
            if (diagram == null) throw new ArgumentNullException();

            this.diagram = diagram;
            this.elementDirectory = diagram.Store.ElementDirectory;
        }

        /// <summary>Called by the design surface to allow selection filtering.
        /// </summary>
        /// <param name="currentSelection">[in] The current selection before any
        /// ShapeElements are added or removed.</param>
        /// <param name="proposedItemsToAdd">[in/out] The proposed DiagramItems to
        /// be added to the selection.</param>
        /// <param name="proposedItemsToRemove">[in/out] The proposed DiagramItems
        /// to be removed from the selection.</param>
        /// <param name="primaryItem">[in/out] The proposed DiagramItem to become
        /// the primary DiagramItem of the selection. A null value signifies that
        /// the last DiagramItem in the resultant selection should be assumed as
        /// the primary DiagramItem.</param>
        /// <returns>true if some or all of the selection was accepted; false if
        /// the entire selection proposal was rejected. If false, appropriate
        /// feedback will be given to the user to indicate that the selection was
        /// rejected.</returns>
        public override bool GetCompliantSelection(
            SelectedShapesCollection currentSelection,
            DiagramItemCollection proposedItemsToAdd,
            DiagramItemCollection proposedItemsToRemove,
            DiagramItem primaryItem)
        {
            if (currentSelection.Count == 0 && proposedItemsToAdd.Count == 0) return true;

            HashSet<DomainClassInfo> itemsToAdd = new HashSet<DomainClassInfo>();

            foreach (DiagramItem item in proposedItemsToAdd)
            {
                if (item.Shape != null)
                    itemsToAdd.Add(item.Shape.GetDomainClass());
            }
            proposedItemsToAdd.Clear();
            foreach (DomainClassInfo classInfo in itemsToAdd)
            {
                foreach (ModelElement element
                    in this.elementDirectory.FindElements(classInfo, false))
                {
                    if (element is ShapeElement)
                    {
                        proposedItemsToAdd.Add(
                            new DiagramItem((ShapeElement)element));
                    }
                }
            }

            return true;
        }
    }

    public partial class ClassDiagram
    {
        protected CustomSelectionRules customSelectionRules = null;

        protected bool multipleSelectionMode = true;

        public override DiagramSelectionRules SelectionRules
        {
            get
            {
                if (multipleSelectionMode)
                {
                    if (customSelectionRules == null)
                    {
                        customSelectionRules = new CustomSelectionRules(this);
                    }
                    return customSelectionRules;
                }
                else
                {
                    return base.SelectionRules;
                }
            }
        }
    }
}
```

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelingPackage>
- <xref:Microsoft.VisualStudio.Modeling.Shell.DiagramDocView>
- <xref:Microsoft.VisualStudio.Modeling.Shell.ModelExplorerToolWindow>
- <xref:Microsoft.VisualStudio.Modeling.Shell.IMonitorSelectionService>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.DiagramSelectionRules>
- <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>