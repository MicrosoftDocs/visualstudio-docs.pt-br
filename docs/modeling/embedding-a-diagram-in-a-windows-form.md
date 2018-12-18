---
title: Inserindo um diagrama em um formulário do Windows Forms
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 7afd12aa6277983f8b50eb1d7adfdd8396f8f960
ms.sourcegitcommit: ef828606e9758c7a42a2f0f777c57b2d39041ac3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39567263"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>Inserir um diagrama em um Windows Form

Você pode inserir um diagrama DSL em um controle do Windows, que aparece na janela do Visual Studio.

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>Inserir um diagrama DSL em um controle do Windows

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
    private MyDSLDocView docView;
    ```

4.  Adicione um novo arquivo ao projeto DslPackage, com o seguinte conteúdo:

    ```csharp
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

5.  Para testar o DSL, pressione **F5** e abrir um arquivo de modelo de exemplo. O diagrama é exibido dentro do controle. A caixa de ferramentas e outros recursos funcionam normalmente.

## <a name="update-the-form-using-store-events"></a>Atualizar o formulário usando o repositório de eventos

1.  No designer de formulários, adicione uma **ListBox** denominado `listBox1`. Isso exibirá uma lista dos elementos no modelo. Ele é sincronizado com o modelo usando *armazenar eventos*. Para obter mais informações, consulte [manipuladores de propagar alterações fora o modelo de evento](../modeling/event-handlers-propagate-changes-outside-the-model.md).

2.  No arquivo de código personalizado, ainda mais substitua métodos à classe DocView:

    ```csharp
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

    ```csharp
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

4.  Para testar o DSL, pressione **F5** e na instância experimental do Visual Studio, abra um arquivo de modelo de exemplo.

     Observe que a caixa de listagem mostra uma lista dos elementos no modelo, e se ele está correto depois de qualquer adição ou exclusão e desfazer e refazer.

## <a name="see-also"></a>Consulte também

- [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
