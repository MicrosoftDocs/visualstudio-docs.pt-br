---
title: Alterar o tipo de retorno de um método DataContext não pode ser desfeita | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 76b161fc-5075-4192-8d94-f15b02e199e9
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5a53bfc66c379be0d6d90d03314f84eef89bd98a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49233812"
---
# <a name="changing-the-return-type-of-a-datacontext-method-cannot-be-undone"></a>Altere o tipo de retorno de um método DataContext não pode ser desfeito
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A alteração do tipo retornado por um método DataContext não pode ser desfeita. Para reverter de volta para o tipo gerado automaticamente, você deve arraste o item do Gerenciador de Servidores/Gerenciador de Base de dados em object relational Designer de Objetos novamente. Tem certeza de que deseja alterar o tipo retornado?  
  
 O tipo de retorno de um método de <xref:System.Data.Linq.DataContext> diferem dependendo de onde você ignora o item em [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. Se você soltar um item diretamente em uma classe existente de entidade, um método de <xref:System.Data.Linq.DataContext> que tem o tipo de retorno de classe de entidade é criado. Se você soltar um item em uma área vazia de [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)], um método de <xref:System.Data.Linq.DataContext> que retorna um tipo gerado automaticamente é criado. Você pode alterar o tipo de retorno de um método de <xref:System.Data.Linq.DataContext> depois de adicioná-lo ao painel de métodos. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e clique em de **tipo de retorno** propriedade no **propriedades** janela.  
  
### <a name="to-change-the-return-type-of-a-datacontext"></a>Para alterar o tipo de retorno de um DataContext  
  
-   Clique em **Sim**.  
  
### <a name="to-exit-the-message-box-and-leave-the-return-type-unchanged"></a>Para sair da caixa de mensagem e deixar o tipo de retorno inalterado  
  
-   Clique em **Não**.  
  
### <a name="to-revert-to-the-original-return-type-after-changing-the-return-type"></a>Para reverter para o tipo de retorno original após alterar o tipo de retorno  
  
1.  Selecione o <xref:System.Data.Linq.DataContext> método no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] e excluí-lo.  
  
2.  Localize o item na **Gerenciador de banco de dados/Gerenciador de servidores** e arraste-a para o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
     Um método de <xref:System.Data.Linq.DataContext> é criado com o tipo de retorno padrão original.  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)   
 [Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (O/R Designer)](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)

