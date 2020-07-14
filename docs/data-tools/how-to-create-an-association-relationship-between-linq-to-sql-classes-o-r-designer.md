---
title: Relações entre classes de LINQ to SQL (O/R Designer)
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 56133e65-81f3-44c3-bc28-ffdd0671a0d2
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b081e989932ea03a3aaf3203bdc7383f90b9b7ed
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282144"
---
# <a name="how-to-create-an-association-between-linq-to-sql-classes-or-designer"></a>Como: criar uma associação entre classes de LINQ to SQL (O/R Designer)
As associações entre classes de entidade no [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] são análogas às relações entre tabelas em um banco de dados. Você pode criar associações entre classes de entidade usando a caixa de diálogo **Editor de Associação**.

Você deve selecionar uma classe pai e uma classe filho ao usar a caixa de diálogo **Editor de Associação** para criar uma associação. A classe pai é a classe de entidade que contém a chave primária; a classe filho é a classe de entidade que contém a chave estrangeira. Por exemplo, se classes de entidade foram criadas e mapeadas para as `Northwind Customers` `Orders` tabelas e, a classe `Customer` seria a classe pai e a classe seria `Order` a classe filho.

> [!NOTE]
> Quando você arrasta tabelas de **Gerenciador de servidores** ou **Gerenciador de Banco de Dados** para a **Object Relational Designer** (**o/R Designer**), as associações são criadas automaticamente com base nas relações de chave estrangeira existentes no banco de dados.

## <a name="association-properties"></a>Propriedades de associação
Depois de criar uma associação, quando você seleciona a associação no **Designer Relacional de Objetos**, há algumas propriedades configuráveis na janela **Propriedades**. (A associação é a linha entre as classes relacionadas.) A tabela a seguir fornece descrições para as propriedades de uma associação.

|Propriedade|Descrição|
|--------------|-----------------|
|**Cardinalidade**|Controla se a associação é de um-para-muitos ou um-para-um.|
|**Propriedade Filho**|Especifica se deve ser criada uma propriedade no pai que é uma coleção ou referência para os registros filho na parte da chave estrangeira da associação. Por exemplo, na associação entre `Customer` e `Order` , se a **Propriedade Child** for definida como **true**, uma propriedade chamada `Orders` será criada na classe pai.|
|**Propriedade pai**|A propriedade na classe filho que referencia a classe pai associada. Por exemplo, na associação entre `Customer` e `Order` , uma propriedade chamada `Customer` que faz referência ao cliente associado para um pedido é criada na `Order` classe.|
|**Propriedades participantes**|Exibe as propriedades de associação e fornece um botão de **reticências** (...) que reabre a caixa de diálogo **Editor de Associação**.|
|**Exclusivo**|Especifica se as colunas de destino estrangeiras têm uma restrição de exclusividade.|

## <a name="to-create-an-association-between-entity-classes"></a>Para criar uma associação entre classes de entidade

1. Clique com o botão direito do mouse na classe de entidade que representa a classe pai na associação, aponte-a para **Adicionar** e clique em **Associação**.

2. Verifique se a **Classe Pai** correta está selecionada na caixa de diálogo **Editor de Associação**.

3. Selecione a **Classe Filho** na caixa de combinação.

4. Selecione as **Propriedades de Associação** que relacionam as classes. Geralmente, isso mapeia para a relação de chave estrangeira definida no banco de dados. Por exemplo, na `Customers` associação e `Orders` , as **Propriedades de associação** são as de `CustomerID` cada classe.

5. Clique em **OK** para criar a associação.

## <a name="see-also"></a>Veja também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Walkthrough: Criando classes de LINQ to SQL](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Métodos DataContext (Designer Relacional de Objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Como: representar chaves primárias](/dotnet/framework/data/adonet/sql/linq/how-to-represent-primary-keys)
