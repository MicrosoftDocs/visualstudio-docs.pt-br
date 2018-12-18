---
title: Como compilar e executar o exemplo de LinqToXmlDataBinding | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3943deaf-80e2-4968-ac04-d3ef56cfad6c
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9e299000cd8477ccc36829e806072cb25e115f8f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49237907"
---
# <a name="how-to-build-and-run-the-linqtoxmldatabinding-example"></a>Como: Compilar e executar o exemplo de LinqToXmlDataBinding
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico mostra como criar e compilar o projeto de LinqToXmlDataBinding Visual Studio, e como executar o programa resultante de LinqToXmlDataBinding Windows Presentation Foundation (WPF).  
  
 Para obter mais informações sobre como usar o Visual Studio para criar projetos, consulte [Desenvolvimento de aplicativos no Visual Studio](http://msdn.microsoft.com/en-us/97490c1b-a247-41fb-8f2c-bc4c201eff68).  
  
## <a name="creating-and-populating-the-project"></a>Criando e preenchendo Projeto  
  
#### <a name="to-create-the-starting-project"></a>Para criar o projeto inicial  
  
1.  Inicie o Visual Studio e crie um LinqToXmlDataBinding WPF C# chamado aplicativo. O projeto deve usar o .NET Framework 3.5 (ou posterior).  
  
2.  Se ainda não presentes, adicione referências de projeto para os seguintes conjuntos de módulos (assemblies) .NET:  
  
    -   System.Data  
  
    -   System.Data.DataSetExtensions  
  
    -   System.Xml  
  
    -   System.Xml.Linq  
  
3.  Compile a solução pressionando **Ctnrl+Shift+B** e execute-a pressionando **F5**. O projeto deve compilar sem erros e como executar um aplicativo genérica de WPF.  
  
#### <a name="to-add-custom-code-to-the-project"></a>Para adicionar o código personalizado ao projeto  
  
1.  No Solution Explorer, renomeie o arquivo de origem Window1.xaml a L2XDBForm.xaml. O arquivo de origem dependente Window1.xaml.cs deve ser automaticamente renomeia a L2XDBForm.xaml.cs.  
  
2.  Substitua o código-fonte encontrado no arquivo L2XDBForm.xaml pela seção de código do tópico [Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md). (Use o modo de exibição XAML para trabalhar com esse arquivo.)  
  
3.  Da mesma forma, substitua a origem em L2XDBForm.xaml.cs com o código localizado em [Código-fonte L2DBForm.xaml.cs](../designers/l2dbform-xaml-cs-source-code.md).  
  
4.  No arquivo App.xaml, substitua todas as ocorrências da cadeia de caracteres “Window1.xaml” com “L2XDBForm.xaml”.  
  
5.  Compile a solução pressionando **Ctrl+Shift+B**.  
  
## <a name="running-the-program"></a>Executando o programa  
 O programa de LinqToXmlDataBinding permite que o usuário para exibir e manipular uma lista de livros que é armazenada como um elemento XML inserido.  
  
#### <a name="to-run-the-program-and-view-the-book-list"></a>Para executar o programa e exibir a lista de livros  
  
1.  Execute LinqToXmlDataBinding pressionando **F5** (**Iniciar Depuração**) ou **Ctrl+F5** (**Iniciar sem Depuração**). Uma janela de programa com o título **Vinculação de dados de WPF usando LINQ to XML** deverá ser exibida.  
  
2.  Observe a seção superior da interface do usuário, que exibe o **XML** bruto que representa a lista de livros. É exibida usando um controle de <xref:System.Windows.Controls.TextBlock> WPF, que não permite a interação por meio do mouse ou do teclado.  
  
3.  A segunda seção vertical, rotulada como **Lista de livros**, exibe os livros como uma lista ordenada de texto sem formatação. Usa um controle de <xref:System.Windows.Controls.ListBox> que permite a seleção embora o mouse ou o teclado.  
  
#### <a name="to-add-and-delete-books-from-the-list"></a>Para adicionar e excluir livros de lista  
  
1.  Para excluir um livro existente da lista, selecione-o na seção **Lista de livros** e, em seguida, clique no botão **Remover o livro selecionado**. Observe que a entrada de livro foi removida do livro e das listagens crua de código-fonte XML.  
  
2.  Para adicionar um novo livro à lista, insira valores nos controles **ID** e **Valor** <xref:System.Windows.Controls.TextBox> na última seção, **Adicionar novo livro** e, em seguida, clique no botão **Adicionar Livro**. Observe que o livro será acrescentado à lista no livro e em listagens de XML. Este programa não validar valores de entrada.  
  
#### <a name="to-edit-an-existing-book-entry"></a>Para editar uma entrada existente de livro  
  
1.  Selecione a entrada de livro na segunda seção da **Lista de livros**. Os valores atuais devem ser exibidos na terceira seção, **Editar o livro selecionado**.  
  
2.  Editar os valores usando o teclado. Assim que um ou outro controle de <xref:System.Windows.Controls.TextBox> fracamente acoplados o foco, as alterações são propagadas automaticamente as listagens de código-fonte XML e de livro.  
  
## <a name="see-also"></a>Consulte também  
 [Vinculação de dados de WPF usando o exemplo LINQ to XML](../designers/wpf-data-binding-using-linq-to-xml-example.md)   
 [Passo a passo: exemplo de LinqToXmlDataBinding](../designers/walkthrough-linqtoxmldatabinding-example.md)   
 [Desenvolvimento de aplicativos no Visual Studio](http://msdn.microsoft.com/en-us/97490c1b-a247-41fb-8f2c-bc4c201eff68)



