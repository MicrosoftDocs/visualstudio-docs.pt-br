---
title: Métodos de DataContext (Object Relational Designer) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c149f4e5-3b61-4c33-892e-3e26d47f3eeb
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 2ccf32d4af0bd16032c4601b054be6407071753f
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49200454"
---
# <a name="datacontext-methods-or-designer"></a>Métodos de DataContext (Designer de Objeto Relacional)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
DataContext] (assetId:///T:System.Data.Linq.DataContext?qualifyHint=False & autoUpgrade = True) métodos (no contexto do [ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)) são métodos do <xref:System.Data.Linq.DataContext> classe executar armazenado procedimentos e funções em um banco de dados.  
  
 A classe <xref:System.Data.Linq.DataContext> é uma classe [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] que atua como um conduto entre um banco de dados SQL Server e as classes de entidade [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] mapeadas para o banco de dados. O <xref:System.Data.Linq.DataContext> classe contém as informações de cadeia de caracteres de conexão e os métodos para se conectar a um banco de dados e manipular os dados no banco de dados. Por padrão, o <xref:System.Data.Linq.DataContext> classe contém vários métodos que você pode chamar, como o <xref:System.Data.Linq.DataContext.SubmitChanges%2A> método envia dados atualizados de [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] classes para o banco de dados. Você também pode criar adicionais <xref:System.Data.Linq.DataContext> métodos que mapeiam para procedimentos armazenados e funções. Ou seja, a chamada desses métodos personalizados executará o procedimento armazenado ou a função no banco de dados para o qual o método <xref:System.Data.Linq.DataContext> está mapeado. Você pode adicionar novos métodos à classe <xref:System.Data.Linq.DataContext> exatamente como adiciona métodos para estender qualquer classe. No entanto, em discussões sobre <xref:System.Data.Linq.DataContext> métodos no contexto do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], é o <xref:System.Data.Linq.DataContext> métodos que mapeiam para procedimentos armazenados e funções que estão sendo discutidas.  
  
## <a name="methods-pane"></a>Painel de Métodos  
 Os métodos de<xref:System.Data.Linq.DataContext> que mapeiam para procedimentos armazenados e funções são exibidos no painel dos métodos do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. O painel de métodos é o painel no lado dos **entidades** painel (a superfície de design principal). O painel de métodos lista todos os <xref:System.Data.Linq.DataContext> métodos que você criou usando o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. Por padrão, o painel de métodos está vazio. Arraste procedimentos armazenados ou funções de **Gerenciador de servidores**/**Database Explorer** até a [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] criar <xref:System.Data.Linq.DataContext> métodos e preencher o painel de métodos. Para obter mais informações, consulte [como: métodos de DataContext criar mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md).  
  
> [!NOTE]
>  Abrir e fechar o painel de métodos clicando com o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] e, em seguida, clicando em **ocultar painel de métodos** ou **Mostrar painel de métodos**, ou use o atalho de teclado CTRL + 1.  
  
## <a name="two-types-of-datacontext-methods"></a>Dois tipos de métodos de DataContext  
 Os métodos de DataContext são os métodos que mapeiam para procedimentos armazenados e funções no banco de dados. Você pode criar e adicionar métodos de DataContext no painel de métodos do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. Há dois tipos distintos de <xref:System.Data.Linq.DataContext> métodos; aqueles que retornam um ou mais conjuntos de resultados e os que não:  
  
-   Os métodos de <xref:System.Data.Linq.DataContext> que retornam um ou mais conjuntos de resultados:  
  
     Crie esse tipo de método <xref:System.Data.Linq.DataContext> quando seu aplicativo precisar apenas executar procedimentos armazenados e funções no banco de dados e retornar os resultados. Para obter mais informações, consulte [como: métodos de DataContext criar mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md), System.Data.Linq.ISingleResult\<T >, e <xref:System.Data.Linq.IMultipleResults>.  
  
-   Os métodos de <xref:System.Data.Linq.DataContext> que não retornam conjuntos de resultados: como inserções, atualizações e exclusões para uma classe de entidade específica.  
  
     Crie esse tipo de <xref:System.Data.Linq.DataContext> quando seu aplicativo tem que executar procedimentos armazenados em vez de usar o padrão de método [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] comportamento para salvar dados modificados entre uma classe de entidade e o banco de dados. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).  
  
## <a name="return-types-of-datacontext-methods"></a>Tipos de retorno de métodos de DataContext  
 Quando você arrasta procedimentos armazenados e funções do **Gerenciador de servidores**/**Database Explorer** até a [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], o tipo de retorno de gerado <xref:System.Data.Linq.DataContext> difere do método Dependendo de onde você solta o item. Soltar itens diretamente em uma classe de entidade existente cria um <xref:System.Data.Linq.DataContext> método com o tipo de retorno da classe de entidade; soltar item em uma área vazia do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] (em qualquer painel) cria um <xref:System.Data.Linq.DataContext> método que retorna um tipo gerado automaticamente. O tipo gerado automaticamente que é criado tem um nome que corresponde ao nome e às propriedades do procedimento ou da função que são mapeados para campos retornados pelo procedimento armazenado ou função.  
  
> [!NOTE]
>  Você pode alterar o tipo de retorno de um método de <xref:System.Data.Linq.DataContext> depois de adicioná-lo ao painel de métodos. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e inspecione o **tipo de retorno** propriedade no **propriedades** janela. Para obter mais informações, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).  
  
 Objetos que você arrasta do banco de dados para a superfície do Designer Relacional de Objetos serão nomeados automaticamente, com base no nome dos objetos no banco de dados. Se você arrastar o mesmo objeto mais de uma vez, um número será acrescentado ao final do novo nome para diferenciar os nomes. Quando os nomes dos objetos do banco de dados contêm espaços ou caracteres, que não são suportados no Visual Basic ou no C#, o espaço ou o caractere inválido é substituído por um sublinhado.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Procedimentos armazenados](http://msdn.microsoft.com/library/4d23dd7a-a85f-44ff-a717-af7d0950c0fc)   
 [Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)   
 [Como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)   
 [Passo a passo: Personalizando a inserção, atualização e exclusão de comportamento de classes de entidade](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)   
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)

