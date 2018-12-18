---
title: Definir um manipulador de link de item de trabalho | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML API
ms.assetid: d52e0bbf-0166-4bb4-a2e3-cefed6188875
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 7ce74627d1d2d48ab02e0b124fbc38949f1f76f9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51733062"
---
# <a name="define-a-work-item-link-handler"></a>Definir um manipulador de link de item de trabalho
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode criar uma extensão de integração do Visual Studio que responde quando o usuário cria ou exclui um link entre um elemento de modelo UML e um item de trabalho. Por exemplo, quando o usuário opta por vincular um novo item de trabalho a um elemento de modelo, seu código pode inicializar os campos do item de trabalho a partir de valores no modelo.  
  
## <a name="set-up-a-uml-extension-solution"></a>Configurar uma solução de extensão UML  
 Isso permitirá que você desenvolva manipuladores e, em seguida, distribuí-los a outros usuários. Você precisa configurar dois projetos do Visual Studio:  
  
-   Um projeto de biblioteca de classes que contém o código do manipulador de link.  
  
-   Um projeto VSIX, que atua como um contêiner para instalação do comando. Se você quiser, você pode incluir outros componentes no mesmo VSIX.  
  
#### <a name="to-set-up-the-visual-studio-solution"></a>Para configurar a solução do Visual Studio  
  
1.  Crie um projeto de biblioteca de classes, adicionando-lo a uma solução existente de VSIX, ou criar uma nova solução.  
  
    1.  No menu **Arquivo**, escolha **Novo**, **Projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, na coluna do meio, clique em **biblioteca de classes**.  
  
    3.  Definir **solução** para indicar se você deseja criar uma nova solução ou adicionar um componente a uma solução VSIX que você já abriu.  
  
    4.  Defina o projeto de nome e o local e clique em Okey.  
  
2.  A menos que sua solução já contenha um, crie um projeto VSIX.  
  
    1.  Na **Gerenciador de soluções**, no menu de atalho da solução, escolha **Add**, **novo projeto**.  
  
    2.  Sob **modelos instalados**, expanda **Visual c#** ou **Visual Basic**, em seguida, selecione **extensibilidade**. Na coluna do meio, escolha **VSIX Project**.  
  
3.  Defina o projeto VSIX como o projeto de inicialização da solução.  
  
    -   No Gerenciador de soluções, no menu de atalho do projeto VSIX, escolha **definir como projeto de inicialização**.  
  
4.  Na **vsixmanifest**, em **conteúdo**, adicione o projeto de biblioteca de classe como um componente de MEF.  
  
    1.  Sobre o **metadados** guia, defina um nome para o VSIX.  
  
    2.  Sobre o **instalar destinos** guia, defina as versões do Visual Studio como os destinos.  
  
    3.  Sobre o **ativos** guia, escolha um **New**e, na caixa de diálogo, defina:  
  
         **Tipo de** = **componente MEF**  
  
         **Código-fonte** = **um projeto na solução atual**  
  
         **Projeto** = *seu projeto de biblioteca de classes*  
  
## <a name="defining-the-work-item-link-handler"></a>Definindo o manipulador de Link de Item de trabalho  
 Execute todas as tarefas a seguir no projeto de biblioteca de classes.  
  
### <a name="project-references"></a>Referências de Projeto  
 Adicione o seguinte [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)] assemblies às referências de projeto:  
  
 `Microsoft.TeamFoundation.WorkItemTracking.Client.dll`  
  
 `Microsoft.VisualStudio.TeamFoundation.WorkItemTracking.dll Microsoft.VisualStudio.Modeling.Sdk.[version]`  
  
 `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml`  
  
 `Microsoft.VisualStudio.Uml.Interfaces`  
  
 `System.ComponentModel.Composition`  
  
 `System.Drawing` -usado pelo código de exemplo  
  
 Se você não encontrar uma dessas referências sob o **.Net** guia da **adicionar referência** caixa de diálogo, use a guia Procurar para localizá-lo no \Program Files\Microsoft Visual Studio [versão] \Common7\IDE\ PrivateAssemblies\\.  
  
### <a name="import-the-work-item-namespace"></a>Importar o Namespace de Item de trabalho  
 No seu [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] project **referências**, adicione referências aos assemblies a seguir:  
  
- Microsoft  
  
- WorkItemTracking  
  
  No código do programa, importe os seguintes namespaces:  
  
```  
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;  
using System.Linq;  
```  
  
### <a name="define-the-linked-work-item-event-handler"></a>Definir o manipulador de eventos de Item de trabalho vinculado  
 Adicione um arquivo de classe ao projeto de biblioteca de classes e defina seu conteúdo da seguinte maneira. Altere os nomes de namespace e classe de acordo com sua preferência.  
  
```  
using System.ComponentModel.Composition;  
using Microsoft.VisualStudio.Uml.Classes;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;  
using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;  
using Microsoft.VisualStudio.TeamFoundation.WorkItemTracking;  
using System.Linq;  
  
namespace WorkItems  
{  
  [Export(typeof(ILinkedWorkItemExtension))]  
  public class MyWorkItemExtension : ILinkedWorkItemExtension  
  {  
    // Called before a new work item is edited by the user.  
    // Use this to initialize work item fields from the model element.  
    public void OnWorkItemCreated(System.Collections.Generic.IEnumerable<IElement> elementsToBeLinked, IWorkItemDocument workItemDocument)  
    {  
      INamedElement namedElement =  
            elementsToBeLinked.First() as INamedElement;  
      if (namedElement != null)  
        workItemDocument.Item.Title = namedElement.Name;  
  
    }  
  
    // Called when any work item is linked to a model element.  
    public void OnWorkItemLinked(System.Collections.Generic.IEnumerable<IElement> elements, string serverUri, int workItemId)  
    {  
      foreach (IElement element in elements)  
        foreach (IShape shape in element.Shapes())  
          shape.Color = System.Drawing.Color.Red;  
    }  
  
    // Called when a work item is unlinked from a model element.  
    public void OnWorkItemRemoved(IElement element, string serverUri, int workItemId)  
    {  
      foreach (IShape shape in element.Shapes())  
        shape.Color = System.Drawing.Color.White;  
    }  
  }  
}  
```  
  
## <a name="testing-the-link-handler"></a>Testando o manipulador de Link  
 Para fins de teste, execute o manipulador de link no modo de depuração.  
  
> [!WARNING]
>  Você já deve estar conectado ao TFS fonte de código de controle (SCC) para criar ou vincular a um item de trabalho. Se você tentar abrir uma conexão em um SCC diferentes do TFS, o Visual Studio fecha automaticamente a solução atual. Certifique-se de que você já estiver conectado ao SCC apropriado antes de tentar criar ou vincular a um item de trabalho. Em versões posteriores do Visual Studio, os comandos de menu não estão disponíveis se você não estiver conectado a um SCC.  
  
#### <a name="to-test-the-link-handler"></a>Para testar o manipulador de link  
  
1.  Pressione **F5**, ou o **depurar** menu, escolha **iniciar depuração**.  
  
     Uma instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] é iniciado.  
  
     **Solução de problemas**: se um novo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] não iniciar, certifique-se de que o projeto do VSIX está definido como o projeto de inicialização da solução.  
  
2.  Em experimental [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra ou crie um projeto de modelagem e abra ou crie um diagrama de modelagem.  
  
3.  Crie um elemento de modelo, como a classe UML e defina seu nome.  
  
4.  O elemento com o botão direito e, em seguida, clique em **Criar Item de trabalho**.  
  
    -   Se o submenu Mostrar **abrir Conexão do Team Foundation Server**, você precisará fechar o projeto, conecte-se para o TFS apropriado e reiniciar este procedimento.  
  
    -   Se o submenu Mostrar uma lista de tipos de item de trabalho, clique em um.  
  
         Abre um novo formulário de item de trabalho.  
  
5.  Verifique se o título do item de trabalho é o mesmo que o elemento de modelo, se você tiver usado o código de exemplo na seção anterior. Isso demonstra `OnWorkItemCreated()` trabalhou.  
  
6.  Preencha o formulário, salve e feche o item de trabalho.  
  
7.  Verifique se o item de trabalho agora está em vermelho. Isso demonstra `OnWorkItemLinked()` no código de exemplo.  
  
     **Solução de problemas**: se os métodos do manipulador não executou, verifique se que:  
  
    -   O projeto de biblioteca de classes está listado como um componente MEF na **conteúdo** lista **source.extensions.manifest** no projeto VSIX.  
  
    -   Correto `Export` atributo é anexado a classe do manipulador, e a classe implementa `ILinkedWorkItemExtension`.  
  
    -   Os parâmetros de todos os `Import` e `Export` atributos são válidos.  
  
## <a name="about-the-work-item-handler-code"></a>Sobre o código de manipulador de Item de trabalho  
  
### <a name="listening-for-new-work-items"></a>Escuta para novos itens de trabalho  
 `OnWorkItemCreated` é chamado quando o usuário opta por criar um novo item de trabalho a ser vinculado aos elementos de modelo. Seu código pode inicializar os campos de item de trabalho. O item de trabalho é então apresentado ao usuário, que pode atualizar os campos e salvar o item de trabalho. O link para um elemento de modelo não é criado até que o item de trabalho foi salvo com êxito.  
  
```  
public void OnWorkItemCreated(  
    IEnumerable<IElement> elementsToBeLinked,  
    IWorkItemDocument workItem)  
{  
  INamedElement namedElement =   
         elementsToBeLinked.First() as INamedElement;  
  if (namedElement != null)  
      workItem.Item.Title = namedElement.Name;  
}  
```  
  
### <a name="listening-for-link-creation"></a>Aguardando a criação de links  
 `OnWorkItemLinked` é chamado apenas depois que um link é criado. Ele é chamado se o link é um novo item de trabalho ou um item existente. Ele é chamado uma vez para cada item de trabalho.  
  
```  
public void OnWorkItemLinked  
        (IEnumerable<IElement> elements,   
         string serverUri, // TFS server  
         int workItemId)  
{  
  foreach (IElement element in elements)  
    foreach (IShape shape in element.Shapes())  
         shape.Color = System.Drawing.Color.Red;  
}  
```  
  
> [!NOTE]
>  Para fazer com que esse exemplo funcione, você deve adicionar uma referência de projeto ao `System.Drawing.dll`e importar o namespace `Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation`. No entanto, essas adições não são necessárias para outras implementações do `OnWorkItemLinked`.  
  
### <a name="listening-for-link-removal"></a>Escutando a remoção do Link  
 `OnWorkItemRemoved` é chamado uma vez antes de cada link de item de trabalho que é excluído. Se um elemento de modelo for excluído, todos os links serão removidos.  
  
```  
public void OnWorkItemRemoved  
         (IElement element, string serverUri, int workItemId)  
{...}  
```  
  
## <a name="updating-a-work-item"></a>Atualizando um item de trabalho  
 Usando namespaces do Team Foundation, você pode manipular um item de trabalho.  
  
 Para usar o exemplo a seguir, adicione esses assemblies .NET às referências do projeto:  
  
-   DLL  
  
-   Microsoft  
  
```  
  
using Microsoft.TeamFoundation.Client;  
using Microsoft.TeamFoundation.WorkItemTracking.Client;  
...  
public void OnWorkItemLinked  
        (IEnumerable<IElement> elements,   
         string serverUri, // TFS server  
         int workItemId)  
{  
  TfsTeamProjectCollection tfs =  
        TfsTeamProjectCollectionFactory  
            .GetTeamProjectCollection(new Uri(serverUri));  
  WorkItemStore workItemStore = new WorkItemStore(tfs);  
  WorkItem item = workItemStore.GetWorkItem(workItemId);  
  item.Open();  
  item.Title = "something";  
  item.Save();  
}   
```  
  
## <a name="accessing-the-work-item-reference-links"></a>Acessando os Links de referência de Item de trabalho  
 Você pode acessar os links da seguinte maneira:  
  
```  
//Get:  
string linkString = element.GetReference(ReferenceConstants.WorkItem);  
// Set:  
element.AddReference(ReferenceConstants.WorkItem, linkString, true);  
  
```  
  
 O formato de `linkString` é:  
  
 `string.Format(@"%{0}\{1}#{1}${2}", tfServer, projectCollection, RepositoryGuid, workItem.Id);`  
  
 em que:  
  
- O URI para o servidor deve ser:  
  
   `http://tfServer:8080/tfs/projectCollection`  
  
   Caso é importante em `projectCollection`.  
  
- `RepositoryGuid` pode ser obtido da sua conexão de TFS:  
  
  ```csharp  
  TfsTeamProjectCollection tpc = TfsTeamProjectCollectionFactory...;  
  RepositoryGuid= tpc.InstanceId;  
  
  ```  
  
  Para obter mais informações sobre referências, consulte [elementos de modelo de anexar cadeias de caracteres de referência para UML](../modeling/attach-reference-strings-to-uml-model-elements.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.TeamFoundation.WorkItemTracking.Client.WorkItemStore?displayProperty=fullName>   
 [Vincular elementos de modelo e itens de trabalho](../modeling/link-model-elements-and-work-items.md)   
 [Anexar cadeias de caracteres de referência a elementos de modelo UML](../modeling/attach-reference-strings-to-uml-model-elements.md)   
 [Definir e instalar uma extensão de modelagem](../modeling/define-and-install-a-modeling-extension.md)   
 [Programando com a API UML](../modeling/programming-with-the-uml-api.md)



