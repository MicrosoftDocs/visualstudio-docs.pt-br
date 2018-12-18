---
title: Código de L2DBForm.xaml.cs
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: sample
ms.assetid: 5a40dad3-6763-4576-b3ad-874df3f2c8d9
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2d996d5cd6c6856c5e348d362c442e7c6471ceba
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49915159"
---
# <a name="l2dbformxamlcs-source-code"></a>Código-fonte de L2DBForm.xaml.cs

Este tópico inclui o conteúdo e a descrição do código-fonte C# no arquivo *L2DBForm.xaml.cs*. A classe parcial de L2XDBForm contida neste arquivo pode ser dividida em três seções lógicas: membros de dados e o botão de `OnRemove` e de `OnAddBook` clique manipuladores de eventos.

## <a name="data-members"></a>Membros de dados

Dois membros de dados particulares são usados para associar essa classe aos recursos de janela usados em *L2DBForm.xaml*.

-   O namespace `myBooks` variável é inicializada a `"http://www.mybooks.com"`.

-   O membro `bookList` é inicializado no construtor para a cadeia de caracteres CDATA em *L2DBForm.xaml* com a seguinte linha:

    ```csharp
    bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
    ```

## <a name="onaddbook-event-handler"></a>Manipulador de eventos OnAddBook

Este método contém as três declarações:

-   A primeira declaração condicional é usada para validação de entrada.

-   A segunda instrução cria um novo <xref:System.Xml.Linq.XElement> de valores de cadeia de caracteres que o usuário inseriu na seção de UI (interface do usuário) **Adicionar Novo Livro**.

-   A última instrução adiciona esse novo elemento de livro ao provedor de dados em *L2DBForm.xaml*. Portanto, a associação de dados dinâmicos atualizará automaticamente interface do usuário com esse novo item; nenhum código de acrescentar fornecido é necessário.

## <a name="onremove-event-handler"></a>Manipulador de eventos OnRemove

O manipulador de `OnRemove` é mais complicado que o manipulador de `OnAddBook` por dois motivos. Primeiro, como o XML brutos contém o espaço em branco preservada, as novas linhas correspondentes também devem ser removidos com a entrada de livro. Segundo, como uma conveniência, a seleção, que estava no item excluído, é reiniciada a anterior na lista.

No entanto, o trabalho principal da remoção do item de livro selecionado é feito por apenas duas instruções:

-   Primeiro, o elemento de livro associado com o item atualmente selecionado na caixa de listagem é recuperado:

    ```csharp
    XElement selBook = (XElement)lbBooks.SelectedItem;
    ```

-   Em seguida, esse elemento é excluído do provedor de dados:

    ```csharp
    selBook.Remove();
    ```

Além disso, a associação de dados dinâmicos garante que interface do usuário do programa é atualizado automaticamente.

## <a name="example"></a>Exemplo

### <a name="code"></a>Código

```csharp
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;
using System.Diagnostics;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Input;
using System.Xml;
using System.Xml.Linq;

namespace LinqToXmlDataBinding {
    /// <summary>
    /// Interaction logic for L2XDBForm.xaml
    /// </summary>

    public partial class L2XDBForm : System.Windows.Window
    {
        XNamespace mybooks = "http://www.mybooks.com";
        XElement bookList;

        public L2XDBForm()
        {
            InitializeComponent();
            bookList = (XElement)((ObjectDataProvider)Resources["LoadedBooks"]).Data;
        }

        void OnRemoveBook(object sender, EventArgs e)
        {
            int index = lbBooks.SelectedIndex;
            if (index < 0) return;

            XElement selBook = (XElement)lbBooks.SelectedItem;
            //Get next node before removing element.
            XNode nextNode = selBook.NextNode;
            selBook.Remove();

            //Remove any matching newline node.
            if (nextNode != null && nextNode.ToString().Trim().Equals(""))
            { nextNode.Remove(); }

            //Set selected item.
            if (lbBooks.Items.Count > 0)
            {  lbBooks.SelectedItem = lbBooks.Items[index > 0 ? index - 1 : 0]; }
        }

        void OnAddBook(object sender, EventArgs e)
        {
            if (String.IsNullOrEmpty(tbAddID.Text) ||
                String.IsNullOrEmpty(tbAddValue.Text))
            {
                MessageBox.Show("Please supply both a Book ID and a Value!", "Entry Error!");
                return;
            }
            XElement newBook = new XElement(
                                mybooks + "book",
                                new XAttribute("id", tbAddID.Text),
                                tbAddValue.Text);
            bookList.Add("  ", newBook, "\r\n");
        }
    }
}
```

### <a name="comments"></a>Comentários

Para obter o código-fonte XAML associado a esses manipuladores, confira [Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md).

## <a name="see-also"></a>Consulte também

- [Passo a passo: exemplo de LinqToXmlDataBinding](../designers/walkthrough-linqtoxmldatabinding-example.md)
- [Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md)