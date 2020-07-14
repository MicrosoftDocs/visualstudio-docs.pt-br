---
title: Mapear métodos DataContext para sprocs e Functions (O-R Designer)
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0c1545313ba6852765bc86d57f2149b4481e5f57
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282131"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>Como criar métodos DataContext mapeados para procedimentos armazenados e funções (Designer Relacional de Objetos)

Você pode adicionar procedimentos armazenados e funções ao o **/R Designer** como <xref:System.Data.Linq.DataContext> métodos. Chamar o método e passar os parâmetros necessários leva à execução do procedimento ou da função armazenada no banco de dados e ao retorno dos dados no tipo de retorno do método <xref:System.Data.Linq.DataContext>. Para obter informações detalhadas sobre <xref:System.Data.Linq.DataContext> métodos, consulte [métodos DataContext (O/R Designer)](../data-tools/datacontext-methods-o-r-designer.md).

> [!NOTE]
> Você também pode usar procedimentos armazenados para substituir o [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] comportamento de tempo de execução padrão que executa inserções, atualizações e exclusões quando as alterações são salvas de classes de entidade em um banco de dados. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (O/R Designer)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

## <a name="create-datacontext-methods"></a>Criar métodos DataContext

Você pode criar <xref:System.Data.Linq.DataContext> métodos arrastando procedimentos armazenados ou funções de <strong>Gerenciador de servidores ou * * Gerenciador de banco de dados</strong> para o o **/R Designer**.

> [!NOTE]
> O tipo de retorno do <xref:System.Data.Linq.DataContext> método gerado difere dependendo de onde você remove o procedimento armazenado ou a função no **designer o/R**. Soltar itens diretamente em uma classe de entidade existente cria um método <xref:System.Data.Linq.DataContext> com o tipo de retorno da classe de entidade. Soltar itens em uma área vazia do o **/R Designer** cria um <xref:System.Data.Linq.DataContext> método que retorna um tipo gerado automaticamente. Você pode alterar o tipo de retorno de um método <xref:System.Data.Linq.DataContext> após adicioná-lo ao painel **Métodos**. Para inspecionar ou alterar o tipo de retorno de um método <xref:System.Data.Linq.DataContext>, selecione-o e inspecione a propriedade **Tipo de Retorno** na janela **Propriedades**. Para obter mais informações, consulte [como alterar o tipo de retorno de um método DataContext (O/R Designer)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>Para criar métodos DataContext que retornam tipos gerados automaticamente

1. Em **Gerenciador de servidores** ou **Gerenciador de banco de dados**, expanda o nó **procedimentos armazenados** do banco de dados com o qual você está trabalhando.

2. Localize o procedimento armazenado desejado e arraste-o para uma área vazia do o **/R Designer**.

     O método <xref:System.Data.Linq.DataContext> é criado com um tipo de retorno gerado automaticamente e aparece no painel **Métodos**.

### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>Para criar métodos DataContext com o tipo de retorno de uma classe de entidade

1. Em **Gerenciador de servidores** ou **Gerenciador de banco de dados**, expanda o nó **procedimentos armazenados** do banco de dados com o qual você está trabalhando.

2. Localize o procedimento armazenado desejado e arraste-o para uma classe de entidade existente no o **/R Designer**.

     O método <xref:System.Data.Linq.DataContext> é criado com o tipo de retorno da classe de entidade selecionada e aparece no painel **Métodos**.

> [!NOTE]
> Para obter informações sobre como alterar o tipo de retorno de existentes <xref:System.Data.Linq.DataContext> métodos, consulte [como: Alterar o tipo de retorno de um método DataContext (Designer Relacional de Objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Métodos DataContext (Designer Relacional de Objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Walkthrough: Criando classes de LINQ to SQL](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Introdução a LINQ no Visual Basic](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
- [LINQ em C#](/dotnet/csharp/linq/linq-in-csharp)
