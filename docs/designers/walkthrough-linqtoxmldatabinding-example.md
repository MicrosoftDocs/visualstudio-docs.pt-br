---
title: 'Passo a passo: Exemplo de LinqToXmlDataBinding'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: aedf42e8-896c-48fa-88df-7f7c9536aa69
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 824896a4e381a6a8d5c5e0935010b1cf224ed9b9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49839226"
---
# <a name="walkthrough-linqtoxmldatabinding-example"></a>Passo a passo: exemplo de LinqToXmlDataBinding
Este passo a passo descreve o exemplo de LinqToXmlDataBinding e explica o conteúdo mais interessante de seus dois arquivos de origem primários, *L2DBForm.xaml* e *L2DBForm.xaml.cs*.

## <a name="prerequisites"></a>Pré-requisitos
 Antes de ler este passo a passo, recomendamos que você compile e execute o programa LinqToXmlDataBinding conforme descrito em [Como compilar e executar o exemplo de LinqToXmlDataBinding](../designers/how-to-build-and-run-the-linqtoxmldatabinding-example.md).

## <a name="remarks"></a>Comentários
 O programa de LinqToXmlDataBinding é um aplicativo Windows Presentation Foundation (WPF) composto de arquivos de origem C# e XAML. Contém um documento XML inserido que define uma lista de livros, e permite que o usuário para exibir, adicionar, excluir, e editar essas entradas. É composto de dois seguintes arquivos de fonte primária:

- *L2DBForm.xaml* contém o código de declaração XAML para a interface do usuário da janela principal. Também contém uma seção de recursos da janela que define um provedor de dados e um documento XML inserido para as listagens de livro.

- *L2DBForm.xaml.cs* contém os métodos de inicialização e de manipulação de eventos associados à interface do usuário.

  A janela principal é dividida nas quatro seções verticais de interface de usuário:

- **XML** exibe o código-fonte XML bruto da listagem de livros inserida.

- **Lista de livros** exibe as entradas de livro como texto padrão e permite que o usuário selecione e exclua entradas individuais.

- **Editar Livro Selecionado** permite que o usuário edite os valores associados à entrada do livro selecionada no momento.

- **Adicionar Novo Livro** habilita a criação de uma nova entrada de livro com base nos valores inseridos pelo usuário.

## <a name="in-this-section"></a>Nesta seção

|Tópico|Descrição|
|-----------|-----------------|
|[Código-fonte de L2DBForm.xaml](../designers/l2dbform-xaml-source-code.md)|Contém o conteúdo e a descrição de código XAML no arquivo L2DBForm.xaml.|
|[Código-fonte de L2DBForm.xaml.cs](../designers/l2dbform-xaml-cs-source-code.md)|Contém o conteúdo e a descrição do código-fonte C# no arquivo L2DBForm.xaml.cs.|

## <a name="see-also"></a>Consulte também

- [Exemplo de associação de dados do WPF usando LINQ to XML](../designers/wpf-data-binding-using-linq-to-xml-example.md)
- [Como criar e executar o exemplo de LinqToXmlDataBinding](../designers/how-to-build-and-run-the-linqtoxmldatabinding-example.md)