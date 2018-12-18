---
title: 'Como: alterar o tipo de retorno de um método DataContext (Object Relational Designer)'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c5b66bff-6dbb-43c0-bffa-317133ca5b9e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 5c67d6dea4c64e858acdab25ecc4a6cede6bf262
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089351"
---
# <a name="how-to-change-the-return-type-of-a-datacontext-method-or-designer"></a>Como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)
O tipo de retorno de um <xref:System.Data.Linq.DataContext> (criado com base em um procedimento armazenado ou função) do método difere dependendo de onde você descarte o procedimento armazenado ou função em de **Relational Designer**. Se você soltar um item diretamente em uma classe existente de entidade, um método de <xref:System.Data.Linq.DataContext> que tem o tipo de retorno de classe de entidade é criado (se o esquema dos dados retornados por correspondências armazenadas do procedimento ou função a forma de classe de entidade). Se você soltar um item em uma área vazia do **Relational Designer**, um <xref:System.Data.Linq.DataContext> método que retorna um tipo gerado automaticamente é criado. Você pode alterar o tipo de retorno de um método de <xref:System.Data.Linq.DataContext> depois de adicioná-lo ao painel de métodos. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e clique em de **tipo de retorno** propriedade no **propriedades** janela.

> [!NOTE]
>  Você não pode reverter <xref:System.Data.Linq.DataContext> métodos que têm um tipo de retorno definido como uma classe de entidade para retornar o tipo gerado automaticamente usando o **propriedades** janela. Para reverter uma <xref:System.Data.Linq.DataContext> método para retornar um tipo gerado automaticamente, você deve arrastar o objeto de banco de dados original para o **Relational Designer** novamente.

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-change-the-return-type-of-a-datacontext-method-from-the-auto-generated-type-to-an-entity-class"></a>Para alterar o tipo de retorno de um método DataContext do tipo gerado automaticamente a uma entidade

1.  Selecione o método de <xref:System.Data.Linq.DataContext> no painel de métodos.

2.  Selecione **tipo de retorno** na **propriedades** classe de janela e, em seguida, selecione uma entidade disponível na **tipo de retorno** lista. Se a classe de entidade desejada não estiver na lista, adicioná-lo ou criá-lo na **Relational Designer** para adicioná-lo à lista.

3.  Salvar a *dbml* arquivo.

## <a name="to-change-the-return-type-of-a-datacontext-method-from-an-entity-class-back-to-the-auto-generated-type"></a>Para alterar o tipo de retorno de um método DataContext de uma classe de entidade de volta para o tipo gerado automaticamente

1.  Selecione o <xref:System.Data.Linq.DataContext> método na **métodos** painel e excluí-lo.

2.  Arraste o objeto de banco de dados da **Gerenciador de servidores** ou **Database Explorer** em uma área vazia do **Relational Designer**.

3.  Salvar a *dbml* arquivo.

## <a name="see-also"></a>Consulte também

- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)
- [Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)