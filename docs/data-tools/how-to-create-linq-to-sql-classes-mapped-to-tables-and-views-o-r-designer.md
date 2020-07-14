---
title: Mapear classes de LINQ to SQL para tabelas/exibições (O-R Designer)
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0fb78bbc-7a78-4ab4-b32f-85ece912e660
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 19b634973e555fd037d20c3ad359ccbb1465c894
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282118"
---
# <a name="how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-or-designer"></a>Como criar classes LINQ to SQL mapeadas para tabelas e exibições (Designer Relacional de Objetos)

[!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)]as classes mapeadas para tabelas e exibições de banco de dados são chamadas de *classes de entidade*. A classe de entidade é mapeada para um registro, enquanto as propriedades individuais de uma classe de entidade são mapeadas para as colunas individuais que compõem um registro. Crie classes de entidade baseadas em tabelas ou exibições de banco de dados arrastando tabelas ou exibições de **Gerenciador de servidores** ou **Gerenciador de banco de dados** para as [ferramentas de LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md). O o **/R Designer** gera as classes e aplica os [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] atributos específicos para habilitar a [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] funcionalidade (os recursos de edição e de comunicação de dados do <xref:System.Data.Linq.DataContext> ). Para obter informações detalhadas sobre [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] classes, consulte [o modelo de objeto LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model).

> [!NOTE]
> O o **/R Designer** é um mapeador relacional de objeto simples, pois dá suporte apenas a relações de mapeamento 1:1. Em outras palavras, uma classe de entidade pode ter apenas uma relação de mapeamento de 1:1 com uma tabela ou exibição de banco de dados. O mapeamento complexo, como o mapeamento de uma classe de entidade para várias tabelas, não tem suporte. No entanto, você pode mapear uma classe de entidade para uma exibição que une várias tabelas relacionadas.

## <a name="create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>Criar classes LINQ to SQL que são mapeadas para tabelas ou exibições de banco de dados

Arrastar tabelas ou exibições de **Gerenciador de servidores** ou **Gerenciador de banco de dados** para o o **/R Designer** cria classes de entidade além dos <xref:System.Data.Linq.DataContext> métodos que são usados para executar atualizações.

Por padrão, o runtime do [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] cria a lógica para salvar alterações de uma classe de entidade atualizável de volta para o banco de dados. Essa lógica é baseada no esquema da tabela (as definições de coluna e informações de chave primária). Se você não quiser esse comportamento, poderá configurar uma classe de entidade para usar procedimentos armazenados para executar inserções, atualizações e exclusões em vez de usar o [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] comportamento de tempo de execução padrão. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (O/R Designer)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-linq-to-sql-classes-that-are-mapped-to-database-tables-or-views"></a>Para criar classes LINQ to SQL que são mapeadas para tabelas ou exibições de banco de dados

1. No **Servidor**/**Gerenciador de Banco de Dados**, expanda **Tabelas** ou **Modos de exibição** e localize a tabela ou exibição de banco de dados que você quer usar em seu aplicativo.

2. Arraste a tabela ou exibição para o o **/R Designer**.

     Uma classe de entidade é criada e aparece na superfície de design. A classe de entidade tem propriedades que mapeiam para as colunas na tabela ou exibição selecionada.

## <a name="create-an-object-data-source-and-display-the-data-on-a-form"></a>Crie um objeto de fonte de dados e exiba os dados em um formulário

Depois de criar classes de entidade usando o o **/R Designer**, você pode criar uma fonte de dados de objeto e popular a [janela de fontes de dados](add-new-data-sources.md#data-sources-window) com as classes de entidade.

### <a name="to-create-an-object-data-source-based-on-linq-to-sql-entity-classes"></a>Para criar uma fonte de dados de objeto com base nas classes de entidade do LINQ to SQL

1. No menu **Compilar**, clique em **Compilar Solução** para criar o seu projeto.

2. Para abrir a janela **fontes de dados** , no menu **dados** , clique em **mostrar fontes de dados**.

3. Na janela **Fontes de Dados**, clique em **Adicionar Nova Fonte de Dados**.

4. Clique em **Objeto** na página **Escolher um Tipo de Fonte de Dados** e clique em **Avançar**.

5. Expanda os nós e localize e selecione sua classe.

    > [!NOTE]
    > Se a classe **Customer** não estiver disponível, cancele o assistente, compile o projeto e execute o assistente novamente.

6. Clique em **Concluir** para criar a fonte de dados e adicionar a classe de entidade **Customer** à janela **Fontes de Dados**.

7. Arraste itens da janela de **Fontes de Dados** para um formulário.

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: criando classes LINQ to SQL (Designer Relacional de Objetos)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [Métodos DataContext (Designer Relacional de Objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Como criar métodos DataContext mapeados para procedimentos armazenados e funções (Designer Relacional de Objetos)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [O modelo de objeto LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/the-linq-to-sql-object-model)
- [Passo a passo: personalizando a inserção, a atualização e o comportamento de exclusão de classes de entidade](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [Como criar uma associação (relação) entre classes LINQ to SQL (Designer Relacional de Objetos)](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)
