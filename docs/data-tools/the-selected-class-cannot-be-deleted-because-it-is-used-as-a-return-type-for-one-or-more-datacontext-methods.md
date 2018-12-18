---
title: A classe selecionada não pode ser excluída porque é usada como um tipo de retorno para um ou mais métodos DataContext
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: d68254a0-f3a1-47e2-aed3-a83471e1d711
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 21ef0f86d701c899328044a03cde8035a1e7292d
ms.sourcegitcommit: f37affbc1b885dfe246d4b2c295a6538b383a0ca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37174192"
---
# <a name="the-selected-class-cannot-be-deleted-because-it-is-used-as-a-return-type-for-one-or-more-datacontext-methods"></a>A classe selecionada não pode ser excluída porque é usada como um tipo de retorno para um ou mais métodos DataContext

O tipo de retorno de um ou mais métodos de <xref:System.Data.Linq.DataContext> é a classe de entidade selecionada. Excluindo uma classe de entidade que é usada como o tipo de retorno para um <xref:System.Data.Linq.DataContext> método faz com que a compilação do projeto falhar. Para excluir a classe selecionada de entidade, identifica os métodos de <xref:System.Data.Linq.DataContext> que a usam e definem seus tipos de retorno para uma classe diferente de entidade.

Para reverter os tipos de retorno de <xref:System.Data.Linq.DataContext> métodos para seus tipos gerados automaticamente originais, primeiro exclua os <xref:System.Data.Linq.DataContext> método da **métodos** painel e, em seguida, arraste o objeto da **Server Explorer** / **Database Explorer** para o **Relational Designer** novamente.

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Identificar <xref:System.Data.Linq.DataContext> métodos que usam a classe de entidade como um tipo de retorno selecionando um <xref:System.Data.Linq.DataContext> método na **métodos** painel e inspecionando o **tipo de retorno** propriedade em que o **Propriedades** janela.

2. Defina as **tipo de retorno** para uma classe de entidade diferente ou exclua o <xref:System.Data.Linq.DataContext> método a partir do painel de métodos.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)