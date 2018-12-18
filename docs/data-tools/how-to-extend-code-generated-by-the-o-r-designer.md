---
title: 'Como: estender o código gerado pelo Object Relational Designer'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 9da4dca31043104c58122c2eed7aa55ae44ef07e
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089783"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>Como: estender o código gerado pelo Designer relacional de objetos
Código gerado pelo **Relational Designer** é regenerado quando alterações são feitas para as classes de entidade e outros objetos na superfície do designer. Devido a essa regeneração de código, qualquer código que você adicionar ao código gerado seja substituído normalmente quando o código de regenerados de designer. O **Relational Designer** fornece a capacidade de gerar arquivos de classe parcial na qual você pode adicionar código que não será substituído. Um exemplo de como adicionar seu próprio código para o código gerado pelo **Relational Designer** está adicionando validação de dados a LINQ para classes SQL (entidade). Para obter mais informações, consulte [como: adicionar validação a classes de entidade](../data-tools/how-to-add-validation-to-entity-classes.md).

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>Adicione código para uma classe de entidade

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>Para criar uma classe parcial e adicione o código para uma classe de entidade

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes o **. dbml** arquivo no **Gerenciador de soluções** ou **Database Explorer**.)

2.  No **Relational Designer**, a classe para o qual você deseja adicionar validação e, em seguida, clique com o botão direito **Exibir código**.

     O editor de códigos abre com uma classe parcial para a classe de entidade selecionada.

3.  Adicione o código na declaração de classe parcial para a classe de entidade.

## <a name="add-code-to-a-datacontext"></a>Adicione código para um DataContext

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>Para criar uma classe parcial e adicione o código a um DataContext

1.  Abra ou crie um novo arquivo LINQ to SQL Classes (**dbml** arquivo) na **Relational Designer**. (Clique duas vezes o **. dbml** arquivo no **Gerenciador de soluções** ou **Database Explorer**.)

2.  No **Relational Designer**, uma área vazia no designer com o botão direito e, em seguida, clique em **Exibir código**.

     O editor de códigos abre com uma classe parcial para o DataContext.

3.  Adicione o código na declaração de classe parcial para o DataContext.

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [Passo a passo: Criando o LINQ para SQL classes (Object Relational Designer)](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)