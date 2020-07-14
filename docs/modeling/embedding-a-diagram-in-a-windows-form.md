---
title: Inserindo um diagrama em um formulário do Windows Forms
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3e81a5ff10cd6e309ffbf17e40ffbaa9ec88f185
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547622"
---
# <a name="embed-a-diagram-in-a-windows-form"></a>Inserir um diagrama em um Windows Form

Você pode inserir um diagrama de DSL em um controle do Windows, que aparece na janela do Visual Studio.

## <a name="embed-a-dsl-diagram-in-a-windows-control"></a>Inserir um diagrama de DSL em um controle do Windows

1. Adicione um novo arquivo de **controle de usuário** ao projeto DslPackage.

2. Adicione um controle de painel ao controle de usuário. Esse painel conterá o diagrama DSL.

     Adicione outros controles que você precisa.

     Defina as propriedades de âncora dos controles.

3. Em Gerenciador de Soluções, clique com o botão direito do mouse no arquivo de controle de usuário e clique em **Exibir código**. Adicione este construtor e a variável ao código:

    ```csharp
    internal UserControl1(MyDSLDocView docView, Control content)
      : this()
    {
      panel1.Controls.Add(content);
      this.docView = docView;
    }
    private MyDSLDocView docView;
    ```

4. Adicione um novo arquivo ao projeto DslPackage, com o seguinte conteúdo:

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

5. Para testar a DSL, pressione **F5** e abra um arquivo de modelo de exemplo. O diagrama aparece dentro do controle. A caixa de ferramentas e outros recursos funcionam normalmente.

## <a name="update-the-form-using-store-events"></a>Atualizar o formulário usando os eventos da loja

1. No designer de formulário, adicione uma caixa de **listagem** chamada `listBox1` . Isso exibirá uma lista dos elementos no modelo. Ele é sincronizado com o modelo usando *eventos de armazenamento*. Para obter mais informações, consulte [manipuladores de eventos propagar alterações fora do modelo](../modeling/event-handlers-propagate-changes-outside-the-model.md).

2. No arquivo de código personalizado, substitua os métodos adicionais para a classe DocView:

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

3. No código por trás do controle de usuário, insira métodos para escutar elementos adicionados e removidos:

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

4. Para testar a DSL, pressione **F5** e, na instância experimental do Visual Studio, abra um arquivo de modelo de exemplo.

     Observe que a caixa de listagem mostra uma lista dos elementos no modelo e que ele está correto após qualquer adição ou exclusão, e após desfazer e refazer.

## <a name="see-also"></a>Confira também

- [Navegando e atualizando um modelo no código do programa](../modeling/navigating-and-updating-a-model-in-program-code.md)
- [Escrevendo código para personalizar uma linguagem específica de domínio](../modeling/writing-code-to-customise-a-domain-specific-language.md)
