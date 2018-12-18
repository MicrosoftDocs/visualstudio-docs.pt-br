---
title: Inserindo um diagrama em um formulário do Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fa6cd040-7c88-4329-b9c3-2a80b312610f
caps.latest.revision: 3
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 04ecf5bd7bfc91e03f48e624d208a5b4f29b10b7
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49292520"
---
# <a name="embedding-a-diagram-in-a-windows-form"></a>Inserindo um diagrama em um formulário do Windows Forms
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode inserir um diagrama DSL em um controle do Windows, que aparece no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] janela.  
  
## <a name="embedding-a-diagram"></a>Inserindo um diagrama  
  
#### <a name="to-embed-a-dsl-diagram-in-a-windows-control"></a>Para inserir um diagrama DSL em um controle do Windows  
  
1.  Adicione um novo **controle de usuário** arquivo ao projeto DslPackage.  
  
2.  Adicione um painel de controle para o controle de usuário. Este painel contém o diagrama de DSL.  
  
     Adicione outros controles que você precisa.  
  
     Defina as propriedades de ancoragem de controles.  
  
3.  No Gerenciador de soluções, clique no arquivo de controle de usuário e clique em **Exibir código**. Adicione este construtor e a variável no código:  
  
    ```csharp  
  
    internal UserControl1(MyDSLDocView docView, Control content)  
      : this()  
    {  
      panel1.Controls.Add(content);  
      this.docView = docView;  
    }  
    private MyDSLDSLDocView docView;  
  
    ```  
  
4.  Adicione um novo arquivo ao projeto DslPackage, com o seguinte conteúdo:  
  
    ```  
    using System.Windows.Forms;  
    namespace Company.MyDSL  
    {  
      partial class MyDSLDocView  
      {  
        private UserControl1 container;  
        public override IWin32Window Window  
        {  
          get  
          {  
            if (container == null)  
            {  
              // Put our own form inside the DSL window:  
              container = new UserControl1(this,  
                (Control)base.Window);  
            }  
            return container;  
    } } } }  
  
    ```  
  
5.  Para testar o DSL, pressione F5 e abrir um arquivo de modelo de exemplo. O diagrama é exibido dentro do controle. A caixa de ferramentas e outros recursos funcionam normalmente.  
  
#### <a name="updating-the-form-using-store-events"></a>Atualizando o formulário usando eventos Store  
  
1.  No designer de formulários, adicione uma **ListBox** denominado `listBox1`. Isso exibirá uma lista dos elementos no modelo. Ele será mantido no synchronism com o modelo usando *armazenar eventos*. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).  
  
2.  No arquivo de código personalizado, ainda mais substitua métodos à classe DocView:  
  
    ```  
  
    partial class MyDSLDocView  
    {  
     /// <summary>  
     /// Register store event listeners.  
     /// This method is called when the model and diagram    
     /// have completed loading.   
     /// </summary>  
     protected override bool LoadView()  
      {  
        bool result = base.LoadView();  
        Store store = this.DocData.Store;  
        EventManagerDirectory emd = store.EventManagerDirectory;  
        DomainClassInfo componentClass = store.DomainDataDirectory.FindDomainClass(typeof(ExampleElement));  
        emd.ElementAdded.Add(componentClass, new EventHandler<ElementAddedEventArgs>(AddElement));  
        emd.ElementDeleted.Add(componentClass, new EventHandler<ElementDeletedEventArgs>(RemoveElement));  
  
        // Do the initial parts list:  
        container.SetUpFormFromModel();  
        return result;  
      }  
     /// <summary>  
     /// Listener method called on creation of each instance of   
     /// the ExampleElement class or its subclasses.  
     /// </summary>  
     private void AddElement(object sender, ElementAddedEventArgs e)  
     {  
       container.Add(e.ModelElement as ExampleElement);  
     }  
     /// <summary>  
     /// Listener method called after deletion of each instance of   
     /// the ExampleElement class or its subclasses.  
     /// </summary>  
     private void RemoveElement(object sender, ElementDeletedEventArgs e)  
     {  
       container.Remove(e.ModelElement as ExampleElement);  
     }  
  
    ```  
  
3.  No code-behind do controle de usuário, inserir métodos para escutar os elementos adicionados e removidos:  
  
    ```  
  
          public partial class UserControl1 : UserControl { ...  
  
    private ExampleModel modelRoot;  
  
    internal void Add(ExampleElement e) { UpdatePartsList(); }  
    internal void Remove(ExampleElement e) { UpdatePartsList(); }  
  
    internal void SetUpFormFromModel()  
    {  
      modelRoot = this.docView.CurrentDiagram.ModelElement as ExampleModel;  
      UpdatePartsList();  
    }  
  
    private void UpdatePartsList()  
    {  
      StringBuilder builder = new StringBuilder();  
      listBox1.Items.Clear();  
      foreach (ExampleElement c in modelRoot.Elements)  
      {  
        listBox1.Items.Add(c.Name);  
      }  
    }  
  
    ```  
  
4.  Para testar o DSL, pressione F5 e na instância experimental do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], abra um arquivo de modelo de exemplo.  
  
     Observe que a caixa de listagem mostra uma lista dos elementos no modelo, e se ele está correto depois de qualquer adição ou exclusão e desfazer e refazer.  
  
## <a name="see-also"></a>Consulte também  
 [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)   
 [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)

