---
title: 'Como: Compilar e executar o exemplo de LinqToXmlDataBinding'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1164312d74259ad4f3a56750a487fb2578595cf0
ms.sourcegitcommit: db680e8fa8066f905e7f9240342ece7ab9259308
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2018
ms.locfileid: "37924155"
---
# <a name="how-to-build-and-run-the-linqtoxmldatabinding-example"></a>Como criar e executar o exemplo de LinqToXmlDataBinding

Este tópico mostra como criar e compilar o projeto de LinqToXmlDataBinding Visual Studio, e como executar o programa resultante de LinqToXmlDataBinding Windows Presentation Foundation (WPF).

Para obter mais informações sobre o Visual Studio, confira [Visão geral do IDE do Visual Studio](../ide/visual-studio-ide.md).

## <a name="create-and-populate-the-project"></a>Criar e popular o projeto

### <a name="to-create-the-starting-project"></a>Para criar o projeto inicial

1. Inicie o Visual Studio e crie um LinqToXmlDataBinding WPF C# chamado aplicativo. O projeto deve usar o .NET Framework 3.5 (ou posterior).

1. Se ainda não presentes, adicione referências de projeto para os seguintes conjuntos de módulos (assemblies) .NET:

    - System.Data

    - System.Data.DataSetExtensions

    - System.Xml

    - System.Xml.Linq

1. Crie a solução pressionando **Ctrl**+**Shift**+**B** e execute-a pressionando **F5**. O projeto deve compilar sem erros e como executar um aplicativo genérica de WPF.

### <a name="to-add-custom-code-to-the-project"></a>Para adicionar o código personalizado ao projeto

1. No Gerenciador de Soluções, renomeie o arquivo de origem **Window1.xaml** como **L2XDBForm.xaml**. O arquivo de origem dependente **Window1.xaml.cs** será renomeado automaticamente como **L2XDBForm.xaml.cs**.

1. Substitua o código-fonte encontrado no arquivo **L2XDBForm.xaml** pela a seção de código do tópico [código-fonte do L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md). Use o modo de exibição XAML para trabalhar com esse arquivo.

1. Da mesma forma, substitua o código-fonte no **L2XDBForm.xaml.cs** pelo código localizado em [código-fonte do L2DBForm.xaml.cs](../designers/l2dbform-xaml-cs-source-code.md).

1. No arquivo **App.xaml**, substitua todas as ocorrências da cadeia de caracteres `Window1.xaml` por `L2XDBForm.xaml`.

1. Crie a solução pressionando **Ctrl**+**Shift**+**B**.

## <a name="run-the-program"></a>Execute o programa

O programa de LinqToXmlDataBinding permite que o usuário para exibir e manipular uma lista de livros que é armazenada como um elemento XML inserido.

### <a name="to-run-the-program-and-view-the-book-list"></a>Para executar o programa e exibir a lista de livros

- Execute LinqToXmlDataBinding pressionando **F5** (**Iniciar Depuração**) ou **Ctrl**+**F5** (**Iniciar Sem Depuração**).

   É exibida uma janela de programa com o título **Associação de dados do WPF usando LINQ to XML**.

- Observe a seção superior da interface do usuário, que exibe o **XML** bruto que representa a lista de livros. É exibida usando um controle de <xref:System.Windows.Controls.TextBlock> WPF, que não permite a interação por meio do mouse ou do teclado.

- A segunda seção vertical, rotulada como **Lista de livros**, exibe os livros como uma lista ordenada de texto sem formatação. Usa um controle de <xref:System.Windows.Controls.ListBox> que permite a seleção embora o mouse ou o teclado.

### <a name="to-add-and-delete-books-from-the-list"></a>Para adicionar e excluir livros de lista

- Para adicionar um novo livro à lista, insira valores nos controles **ID** e **Valor** <xref:System.Windows.Controls.TextBox> na última seção, **Adicionar novo livro** e, em seguida, clique no botão **Adicionar Livro**. Observe que o livro será acrescentado à lista no livro e em listagens de XML. Este programa não validar valores de entrada.

- Para excluir um livro existente da lista, selecione-o na seção **Lista de livros** e, em seguida, clique no botão **Remover o livro selecionado**. Observe que a entrada de livro foi removida do livro e das listagens crua de código-fonte XML.

### <a name="to-edit-an-existing-book-entry"></a>Para editar uma entrada existente de livro

1. Selecione a entrada de livro na segunda seção da **Lista de livros**. Os valores atuais devem ser exibidos na terceira seção, **Editar o livro selecionado**.

1. Editar os valores usando o teclado. Assim que um ou outro controle de <xref:System.Windows.Controls.TextBox> fracamente acoplados o foco, as alterações são propagadas automaticamente as listagens de código-fonte XML e de livro.

## <a name="see-also"></a>Consulte também

- [Exemplo de associação de dados do WPF usando LINQ to XML](../designers/wpf-data-binding-using-linq-to-xml-example.md)
- [Passo a passo: exemplo de LinqToXmlDataBinding](../designers/walkthrough-linqtoxmldatabinding-example.md)
- [Visão geral do IDE do Visual Studio](../ide/visual-studio-ide.md)