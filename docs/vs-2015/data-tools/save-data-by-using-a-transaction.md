---
title: Salvar dados usando uma transação | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- saving data, using transactions
- System.Transactions namespace
- transactions, saving data
- data [Visual Studio], saving
ms.assetid: 8b835e8f-34a3-413d-9bb5-ebaeb87f1198
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: ba83cf7db6415eefcb989f678bc4149d495016e4
ms.sourcegitcommit: 53aa5a413717a1b62ca56a5983b6a50f7f0663b3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59658338"
---
# <a name="save-data-by-using-a-transaction"></a>Salvar dados usando uma transação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Salvar dados em uma transação usando o <xref:System.Transactions> namespace. Use o <xref:System.Transactions.TransactionScope> objeto participe de uma transação que é gerenciada automaticamente para você.  
  
 Projetos não são criados com uma referência ao assembly System. Transactions, portanto, você precisa adicionar manualmente uma referência a projetos que usam transações.  
  
> [!NOTE]
>  O <xref:System.Transactions> namespace tem suporte no Windows 2000 ou posterior.  
  
 A maneira mais fácil para implementar uma transação é criar uma instância de um <xref:System.Transactions.TransactionScope> do objeto em um `using` instrução. (Para obter mais informações, consulte [instrução Using](http://msdn.microsoft.com/library/665d1580-dd54-4e96-a9a9-6be2a68948f1), e [usando a instrução](http://msdn.microsoft.com/library/afc355e6-f0b9-4240-94dd-0d93f17d9fc3).) O código executado dentro de `using` instrução participa na transação.  
  
 Para confirmar a transação, chame o <xref:System.Transactions.TransactionScope.Complete%2A> bloquear o método como a última instrução em uso.  
  
 Para reverter a transação, lançar uma exceção antes de chamar o <xref:System.Transactions.TransactionScope.Complete%2A> método.  
  
 Para obter mais informações, consulte [salvar dados em uma transação](../data-tools/save-data-in-a-transaction.md).  
  
### <a name="to-add-a-reference-to-the-systemtransactions-dll"></a>Para adicionar uma referência à dll System. Transactions  
  
1.  Sobre o **Project** menu, selecione **adicionar referência**.  
  
2.  Sobre o **.NET** guia (**SQL Server** guia para projetos do SQL Server), selecione **System. Transactions**e, em seguida, selecione **Okey**.  
  
     Uma referência a Transactions é adicionada ao projeto.  
  
### <a name="to-save-data-in-a-transaction"></a>Para salvar dados em uma transação  
  
-   Adicione código para salvar os dados dentro da usando instrução que contém a transação. O código a seguir mostra como criar e instanciar um <xref:System.Transactions.TransactionScope> objeto em um usando instrução:  
  
     [!code-csharp[VbRaddataSaving#11](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#11)]
     [!code-vb[VbRaddataSaving#11](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#11)]  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
