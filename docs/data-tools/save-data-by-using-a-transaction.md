---
title: Como salvar dados usando uma transação
description: Examine como salvar dados usando uma transação com ferramentas de conjunto de dados no Visual Studio. Você salva dados em uma transação usando o namespace System. Transactions.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: c633ed01821f500e958d3c7549febc23cf33c09d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99858482"
---
# <a name="how-to-save-data-by-using-a-transaction"></a>Como salvar dados usando uma transação

Você salva dados em uma transação usando o <xref:System.Transactions> namespace. Use o <xref:System.Transactions.TransactionScope> objeto para participar de uma transação que é gerenciada automaticamente para você.

Os projetos não são criados com uma referência ao assembly *System. Transactions* , portanto, você precisa adicionar manualmente uma referência a projetos que usam transações.

A maneira mais fácil de implementar uma transação é criar uma instância de um <xref:System.Transactions.TransactionScope> objeto em uma `using` instrução. (Para obter mais informações, consulte [instrução using](/dotnet/visual-basic/language-reference/statements/using-statement)e [instrução using](/dotnet/csharp/language-reference/keywords/using-statement).) O código que é executado dentro da `using` instrução participa da transação.

Para confirmar a transação, chame o <xref:System.Transactions.TransactionScope.Complete%2A> método como a última instrução no bloco Using.

Para reverter a transação, acione uma exceção antes de chamar o <xref:System.Transactions.TransactionScope.Complete%2A> método.

## <a name="to-add-a-reference-to-the-systemtransactionsdll"></a>Para adicionar uma referência ao System.Transactions.dll

1. No menu **Projeto**, selecione **Adicionar Referência**.

2. Na guia **.net** (**SQL Server** guia para projetos SQL Server), selecione **System. Transactions** e, em seguida, selecione **OK**.

     Uma referência a *System.Transactions.dll* é adicionada ao projeto.

## <a name="to-save-data-in-a-transaction"></a>Para salvar dados em uma transação

- Adicione código para salvar dados dentro da instrução using que contém a transação. O código a seguir mostra como criar e instanciar um <xref:System.Transactions.TransactionScope> objeto em uma instrução Using:

     [!code-vb[VbRaddataSaving#11](../data-tools/codesnippet/VisualBasic/save-data-by-using-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#11](../data-tools/codesnippet/CSharp/save-data-by-using-a-transaction_1.cs)]

## <a name="see-also"></a>Confira também

- [Salvar dados novamente no banco de dados](../data-tools/save-data-back-to-the-database.md)
- [Passo a passo: salvar dados em uma transação](../data-tools/save-data-in-a-transaction.md)
