---
title: 'Como: criar uma associação (relação) entre classes LINQ to SQL (Object Relational Designer) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 56133e65-81f3-44c3-bc28-ffdd0671a0d2
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5c739fcf11cec7eb841b99e58b01ada32cfdfd49
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49209359"
---
# <a name="how-to-create-an-association-relationship-between-linq-to-sql-classes-or-designer"></a>Como: criar uma associação (relação) entre classes LINQ to SQL (O/R Designer)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
As associações entre classes de entidade no [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] são análogas às relações entre tabelas em um banco de dados. Você pode criar associações entre classes de entidade usando o **Editor de associação** caixa de diálogo.  
  
 Você deve selecionar uma classe pai e a classe filho ao usar o **Editor de associação** caixa de diálogo para criar uma associação. A classe pai é a classe de entidade que contém a chave primária; a classe filho é a classe de entidade que contém a chave estrangeira. Por exemplo, se as classes de entidade foram criadas que mapeiam para as tabelas Customers e Orders do Northwind, a classe Customer seria a classe pai e a classe Order seria a classe filho.  
  
> [!NOTE]
>  Quando você arrasta tabelas do **Gerenciador de servidores**/**Database Explorer** até a [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]), associações são criadas automaticamente com base em existente relações de chave estrangeira no banco de dados.  
  
 Depois de criar uma associação, quando você seleciona a associação no Designer relacional de objetos, há algumas propriedades configuráveis na **propriedades** janela. (A associação é a linha entre as classes relacionadas.) A tabela a seguir fornece descrições para as propriedades de uma associação.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Cardinalidade**|Controla se a associação é de um-para-muitos ou um-para-um.|  
|**Propriedade filho**|Especifica se deve ser criada uma propriedade no pai que é uma coleção ou referência para os registros filho na parte da chave estrangeira da associação. Por exemplo, na associação entre Customer e Order, se o **propriedade filho** é definido como **verdadeiro**, uma propriedade chamada Orders é criada na classe pai.|  
|**Propriedade pai**|A propriedade na classe filho que referencia a classe pai associada. Por exemplo, na associação entre Customer e Order, uma propriedade chamada Customer que referencia o cliente associado para um pedido é criada na classe Order.|  
|**Propriedades participantes**|Exibe as propriedades de associação e fornece um **reticências** botão (...) que reabre a **Editor de associação** caixa de diálogo.|  
|**exclusivo**|Especifica se as colunas de destino estrangeiras têm uma restrição de exclusividade.|  
  
### <a name="to-create-an-association-between-entity-classes"></a>Para criar uma associação entre classes de entidade  
  
1.  A classe de entidade que representa a classe pai na associação com o botão direito, aponte para **Add**e, em seguida, clique em **associação**.  
  
2.  Verifique o correto **classe pai** está selecionado na **Editor de associação** caixa de diálogo.  
  
3.  Selecione o **classe filho** na caixa de combinação.  
  
4.  Selecione o **propriedades de associação** que relacionam as classes. Geralmente, isso mapeia para a relação de chave estrangeira definida no banco de dados. Por exemplo, na associação Customers e Orders, o **propriedades de associação** são a CustomerID para cada classe.  
  
5.  Clique em **Okey** para criar a associação.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)   
 [Como representar chaves primárias](http://msdn.microsoft.com/library/63c65289-6539-42b2-8493-891c232018fa)

