---
title: Atualizar um modelo UML de um thread em segundo plano | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42c06b0b-b681-4e19-b5f3-6116dd2a4072
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 4173b70cda9df39ce8a4500817fff199ed1a2996
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749986"
---
# <a name="update-a-uml-model-from-a-background-thread"></a>Atualizar um modelo UML por meio de um thread em segundo plano
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Às vezes, pode ser útil fazer alterações a um modelo em um thread em segundo plano. Por exemplo, se você estiver carregando informações de um recurso externo lento, você poderia usar um thread em segundo plano para supervisionar as atualizações. Isso permite que o usuário veja cada atualização assim que ele ocorre.  
  
 No entanto, você deve estar ciente de que o armazenamento de UML não é thread-safe. As seguintes precauções são importantes:  
  
-   Cada atualização de um modelo ou diagrama deve ser feita no thread da interface do usuário do usuário. O thread em segundo plano deve usar <xref:System.Windows.Forms.Control.Invoke%2A> ou `Dispatcher.` <xref:System.Windows.Threading.Dispatcher.Invoke%2A> para fazer com que o thread de interface do usuário execute as atualizações reais.  
  
-   Se você agrupar uma série de alterações em uma única transação, é recomendável que você impeça o usuário de editar o modelo, enquanto a transação está em andamento. Caso contrário, todas as edições feitas pelo usuário se tornará parte da mesma transação. Você pode impedir que o usuário faça alterações mostrando uma caixa de diálogo modal. Se você quiser, você pode fornecer um botão Cancelar na caixa de diálogo. O usuário pode ver as alterações conforme elas ocorrem.  
  
## <a name="example"></a>Exemplo  
 Este exemplo usa um thread em segundo plano para fazer várias alterações em um modelo. Uma caixa de diálogo é usada para excluir o usuário quando o thread está em execução. Neste exemplo simples, nenhum botão Cancelar é fornecido na caixa de diálogo. No entanto, seria fácil adicionar esse recurso.  
  
#### <a name="to-run-the-example"></a>Para executar o exemplo  
  
1. Crie um manipulador de comandos em um projeto c#, conforme descrito em [definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md).  
  
2. Certifique-se de que o projeto inclua referências a esses assemblies:  
  
   -   Microsoft.VisualStudio.ArchitectureTools.Extensibility  
  
   -   Microsoft.VisualStudio.Modeling.Sdk.[version]  
  
   -   Microsoft.VisualStudio.Modeling.Sdk.Diagrams.[version]  
  
   -   Microsoft.VisualStudio.Uml.Interfaces  
  
   -   System.ComponentModel.Composition  
  
   -   System.Windows.Forms  
  
3. Adicionar ao projeto um formulário do Windows chamado **ProgressForm**. Ele deve exibir uma mensagem informando que as atualizações estão em andamento. Ele não precisa ter todos os outros controles.  
  
4. Adicione um arquivo c# que contém o código mostrado após a etapa 7.  
  
5. Compile e execute o projeto.  
  
    Uma nova instância da [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] será iniciado em modo experimental.  
  
6. Crie ou abra um diagrama de classe UML na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
7. Clique com botão direito em qualquer lugar no diagrama de classe UML e, em seguida, clique em **adicionar várias Classes de UML**.  
  
   Várias novas caixas de classe serão exibida no diagrama, uma após a outra em intervalos de meio segundo.  
  
```csharp  
using System;  
using System.ComponentModel;  
using System.ComponentModel.Composition;  
using System.Threading;  
using System.Windows.Forms;  
  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;  
using Microsoft.VisualStudio.Uml.Classes;  
  
namespace BackgroundThreadProgressUI // CHANGE TO YOUR NAMESPACE  
{  
  [Export(typeof(ICommandExtension))]  
  [ClassDesignerExtension]  
  class UmlClassAdderCommand : ICommandExtension  
  {  
  
    [Import]  
    IDiagramContext context { get; set; }  
  
    [Import]  
    ILinkedUndoContext linkedUndoContext { get; set; }  
  
    // Called when the user runs the command.  
    public void Execute(IMenuCommand command)  
    {  
      // The form that will exclude the user.  
      ProgressForm form = new ProgressForm();  
  
      // System.ComponentModel.BackgroundWorker is a  
      // convenient way to run a background thread.  
      BackgroundWorker worker = new BackgroundWorker();  
      worker.WorkerSupportsCancellation = true;  
  
      worker.DoWork += delegate(object sender, DoWorkEventArgs args)  
      {  
        // This block will be executed in a background thread.  
  
        IClassDiagram diagram = context.CurrentDiagram as IClassDiagram;  
        IModelStore store = diagram.ModelStore;  
        const int CLASSES_TO_CREATE = 15;  
  
        // Group all the changes together.  
        using (ILinkedUndoTransaction transaction = linkedUndoContext.BeginTransaction("Background Updates"))  
        {  
          for (int i = 1; i < CLASSES_TO_CREATE; i++)  
          {  
            if (worker.CancellationPending)   
               return; // No commit - undo all.  
  
            // Create model elements using the UI thread by using  
            // the Invoke method on the progress form. Always   
            // modify the model and diagrams from a UI thread.  
            form.Invoke((MethodInvoker)(delegate  
            {  
              IClass newClass = store.Root.CreateClass();  
              newClass.Name = string.Format("NewClass{0}", i);  
              diagram.Display(newClass);  
            }));  
  
            // Sleep briefly so that we can watch the updates.  
            Thread.Sleep(500);  
          }  
  
          // Commit the transaction or it will be rolled back.  
          transaction.Commit();  
        }  
      };  
  
      // Close the form when the thread completes.  
      worker.RunWorkerCompleted += delegate(object sender, RunWorkerCompletedEventArgs args)  
      {  
        form.Close();  
      };  
  
      // Start the thread before showing the modal progress dialog.  
      worker.RunWorkerAsync();  
  
      // Show the form modally, parented on VS.  
      // Prevents the user from making changes while in progress.  
      form.ShowDialog();  
    }  
  
    public void QueryStatus(IMenuCommand command)  
    {  
      command.Enabled = command.Visible = true;  
    }  
  
    public string Text  
    {  
      get { return "Add several classes"; }  
    }  
  }  
}  
```  
  
#### <a name="to-allow-the-user-to-cancel-the-thread-in-the-example"></a>Para permitir que o usuário cancele o thread no exemplo  
  
1.  Adicione um botão Cancelar na caixa de diálogo de progresso.  
  
2.  Adicione o seguinte código à caixa de diálogo de progresso:  
  
     `public event MethodInvoker Cancel;`  
  
     `private void CancelButton_Click(object sender, EventArgs e)`  
  
     `{`  
  
     `Cancel();`  
  
     `}`  
  
3.  No método Execute (), insira esta linha após a construção do formulário:  
  
     `form.Cancel += delegate() { worker.CancelAsync(); };`  
  
### <a name="other-methods-of-accessing-the-ui-thread"></a>Outros métodos para acessar o thread de interface do usuário  
 Se você não quiser criar uma caixa de diálogo, você pode acessar o controle que exibe o diagrama:  
  
 `DiagramView uiThreadHolder = context.CurrentDiagram.GetObject<Diagram>().ActiveDiagramView;`  
  
 Você pode usar `uiThreadHolder.Invoke()` para executar operações no thread da interface do usuário.  
  
## <a name="see-also"></a>Consulte também  
 [Definir um comando de menu em um diagrama de modelagem](../modeling/define-a-menu-command-on-a-modeling-diagram.md)   
 [Definir um manipulador de gestos em um diagrama de modelagem](../modeling/define-a-gesture-handler-on-a-modeling-diagram.md)



