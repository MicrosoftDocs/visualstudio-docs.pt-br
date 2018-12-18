---
title: Métodos de DataContext (Object Relational Designer)
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c149f4e5-3b61-4c33-892e-3e26d47f3eeb
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 95d84442b4aba74dbc44b7aacc97d0a965162150
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924961"
---
# <a name="datacontext-methods-or-designer"></a>Métodos de DataContext (Designer de Objeto Relacional)

<xref:System.Data.Linq.DataContext> métodos (no contexto do [ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)) são métodos do <xref:System.Data.Linq.DataContext> classe que executam procedimentos armazenados e funções em um banco de dados.

A classe <xref:System.Data.Linq.DataContext> é uma classe [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] que atua como um conduto entre um banco de dados SQL Server e as classes de entidade [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] mapeadas para o banco de dados. O <xref:System.Data.Linq.DataContext> classe contém as informações de cadeia de caracteres de conexão e os métodos para se conectar a um banco de dados e manipular os dados no banco de dados. Por padrão, o <xref:System.Data.Linq.DataContext> classe contém vários métodos que você pode chamar, como o <xref:System.Data.Linq.DataContext.SubmitChanges%2A> método envia dados atualizados de [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] classes para o banco de dados. Você também pode criar adicionais <xref:System.Data.Linq.DataContext> métodos que mapeiam para procedimentos armazenados e funções. Em outras palavras, chamar esses métodos personalizados é executado o procedimento armazenado ou função no banco de dados ao qual o <xref:System.Data.Linq.DataContext> método é mapeado. Você pode adicionar novos métodos à classe <xref:System.Data.Linq.DataContext> exatamente como adiciona métodos para estender qualquer classe. No entanto, em discussões sobre <xref:System.Data.Linq.DataContext> métodos no contexto do **Relational Designer**, é o <xref:System.Data.Linq.DataContext> métodos que mapeiam para procedimentos armazenados e funções que estão sendo discutidas.

## <a name="methods-pane"></a>Painel de métodos

<xref:System.Data.Linq.DataContext> métodos que são mapeados para procedimentos armazenados e funções são exibidos na **métodos** painel da **Relational Designer**. O **métodos** painel é o painel no lado das **entidades** painel (a superfície de design principal). O **métodos** painel lista todos os <xref:System.Data.Linq.DataContext> métodos que você criou usando a **Relational Designer**. Por padrão, o **métodos** painel está vazio; arraste procedimentos armazenados ou funções de **Gerenciador de servidores** ou **Database Explorer** até o **O/R Designer**  criem <xref:System.Data.Linq.DataContext> métodos e preencher o **métodos** painel. Para obter mais informações, consulte [como: métodos de DataContext criar mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md).

> [!NOTE]
> Abrir e fechar o painel de métodos clicando com o **Relational Designer** e, em seguida, clicando em **ocultar painel de métodos** ou **Mostrar painel de métodos**, ou use o atalho de teclado  **CTRL**+**1**.

## <a name="two-types-of-datacontext-methods"></a>Dois tipos de métodos de DataContext

Os métodos de DataContext são os métodos que mapeiam para procedimentos armazenados e funções no banco de dados. Você pode criar e adicionar métodos de DataContext na **métodos** painel da **Relational Designer**. Há dois tipos distintos de <xref:System.Data.Linq.DataContext> métodos; aqueles que retornam um ou mais conjuntos de resultados e os que não:

- Os métodos de <xref:System.Data.Linq.DataContext> que retornam um ou mais conjuntos de resultados:

   Crie esse tipo de método <xref:System.Data.Linq.DataContext> quando seu aplicativo precisar apenas executar procedimentos armazenados e funções no banco de dados e retornar os resultados. Para obter mais informações, consulte [como: métodos de DataContext criar mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md), System.Data.Linq.ISingleResult\<T >, e <xref:System.Data.Linq.IMultipleResults>.

- Os métodos de <xref:System.Data.Linq.DataContext> que não retornam conjuntos de resultados: como inserções, atualizações e exclusões para uma classe de entidade específica.

   Crie esse tipo de <xref:System.Data.Linq.DataContext> quando seu aplicativo tem que executar procedimentos armazenados em vez de usar o padrão de método [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] comportamento para salvar dados modificados entre uma classe de entidade e o banco de dados. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

## <a name="return-types-of-datacontext-methods"></a>Tipos de retorno de métodos de DataContext

Quando você arrasta procedimentos armazenados e funções do **Gerenciador de servidores** ou **Database Explorer** até o **Relational Designer**, o tipo de retorno de gerado <xref:System.Data.Linq.DataContext> método difere dependendo de onde você solta o item. Soltar itens diretamente em uma classe de entidade existente cria um <xref:System.Data.Linq.DataContext> método com o tipo de retorno da classe de entidade; soltar item em uma área vazia do **Relational Designer** (em qualquer painel) cria um <xref:System.Data.Linq.DataContext> método que retorna um tipo gerado automaticamente. O tipo gerado automaticamente tem o nome que corresponda ao procedimento armazenado ou nome de função e propriedades que mapeiam para os campos retornados pelo procedimento armazenado ou função.

> [!NOTE]
> Você pode alterar o tipo de retorno de um método de <xref:System.Data.Linq.DataContext> depois de adicioná-lo ao painel de métodos. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e inspecione o **tipo de retorno** propriedade no **propriedades** janela. Para obter mais informações, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).

Você arrasta do banco de dados para a superfície do Designer relacional de objetos são nomeados automaticamente, com base no nome dos objetos no banco de dados. Se você arrastar o mesmo objeto mais de uma vez, um número é adicionado ao final do novo nome que diferencia os nomes. Quando os nomes dos objetos do banco de dados contêm espaços ou caracteres, que não são suportados no Visual Basic ou no C#, o espaço ou o caractere inválido é substituído por um sublinhado.

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Procedimentos armazenados](/dotnet/framework/data/adonet/sql/linq/stored-procedures)
- [Como criar métodos DataContext mapeados para procedimentos armazenados e funções (Designer Relacional de Objetos)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [Como atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer Relacional de Objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [Passo a passo: personalizando a inserção, a atualização e o comportamento de exclusão de classes de entidade](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [Passo a passo: Criando o LINQ para SQL classes (Object Relational Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)