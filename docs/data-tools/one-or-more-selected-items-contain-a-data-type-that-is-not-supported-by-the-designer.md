---
title: Um ou mais itens selecionados contêm um tipo de dados que não é suportado pelo designer
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 71dcd4f9-2946-42c5-9ce4-99c819ea2785
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 68d8675df54e37b9a6122b853e742addc0d8060c
ms.sourcegitcommit: e9d1018a01af62c3dc5aeb6b325faba7e20bd496
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/28/2018
ms.locfileid: "37089484"
---
# <a name="one-or-more-selected-items-contain-a-data-type-that-is-not-supported-by-the-designer"></a>Um ou mais itens selecionados contêm um tipo de dados que não é suportado pelo designer

Um ou mais dos itens arrastados de **Gerenciador de servidores** ou **Gerenciador de banco de dados** para o **Relational Designer** contém um tipo de dados que não é compatível com o **s /R designer**, por exemplo, [tipos CLR definidos pelo usuário](/dotnet/framework/data/adonet/sql/clr-user-defined-types).

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Criar uma exibição que são baseadas na tabela desejada e que não inclui o tipo de dados sem suporte.

2. Arraste a exibição de **Gerenciador de servidores** ou **Database Explorer** para o designer.

## <a name="see-also"></a>Consulte também

- [Mensagens do O/R Designer](../data-tools/o-r-designer-messages.md)
- [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)