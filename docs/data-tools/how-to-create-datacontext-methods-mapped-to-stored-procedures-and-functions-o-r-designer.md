---
title: 'Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (Object Relational Designer)'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 8ae5fb4b3785bde0e092f68b62a9b030069a52aa
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942693"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (O/R Designer)

Você pode adicionar procedimentos armazenados e funções para o **Relational Designer** como <xref:System.Data.Linq.DataContext> métodos. Chamar o método e passar os parâmetros necessários executa a função ou procedimento armazenado no banco de dados e retorna os dados no tipo de retorno do <xref:System.Data.Linq.DataContext> método. Para obter informações detalhadas sobre <xref:System.Data.Linq.DataContext> métodos, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).

> [!NOTE]
> Você também pode usar procedimentos armazenados para substituir o padrão [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] comportamento de tempo de execução que executa inserções, atualizações e exclusões quando alterações são salvas de classes de entidade para um banco de dados. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

## <a name="create-datacontext-methods"></a>Criar métodos DataContext

Você pode criar <xref:System.Data.Linq.DataContext> métodos arrastando procedimentos armazenados ou funções a partir <strong>Gerenciador de servidores ou * * Gerenciador de banco de dados</strong> para o **Relational Designer**.

> [!NOTE]
> O tipo de retorno de gerado <xref:System.Data.Linq.DataContext> método difere dependendo de onde você descarte o procedimento armazenado ou a função na **Relational Designer**. Soltar itens diretamente em uma classe de entidade existente cria um método <xref:System.Data.Linq.DataContext> com o tipo de retorno da classe de entidade. Soltar itens em uma área vazia do **Relational Designer** cria um <xref:System.Data.Linq.DataContext> método que retorna um tipo gerado automaticamente. Você pode alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método após adicioná-lo para o **métodos** painel. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e inspecione o **tipo de retorno** propriedade no **propriedades** janela. Para obter mais informações, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>Para criar métodos DataContext que retornam tipos gerados automaticamente

1.  Na **Gerenciador de servidores** ou **Database Explorer**, expanda o **Stored Procedures** nó do banco de dados com o qual você está trabalhando.

2.  Localize o procedimento armazenado desejado e arraste-o para uma área vazia do **Relational Designer**.

     O <xref:System.Data.Linq.DataContext> método é criado com um tipo de retorno gerado automaticamente e aparece na **métodos** painel.

### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>Para criar métodos DataContext com o tipo de retorno de uma classe de entidade

1.  Na **Gerenciador de servidores** ou **Database Explorer**, expanda o **Stored Procedures** nó do banco de dados com o qual você está trabalhando.

2.  Localize o procedimento armazenado desejado e arraste-o para uma classe de entidade existente na **Relational Designer**.

     O <xref:System.Data.Linq.DataContext> método é criado com o tipo de retorno da classe de entidade selecionada e aparece na **métodos** painel.

> [!NOTE]
> Para obter informações sobre como alterar o tipo de retorno de existentes <xref:System.Data.Linq.DataContext> métodos, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Passo a passo: Criando o LINQ para classes SQL](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Introdução ao LINQ no Visual Basic](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
- [LINQ em C#](/dotnet/csharp/linq/linq-in-csharp)