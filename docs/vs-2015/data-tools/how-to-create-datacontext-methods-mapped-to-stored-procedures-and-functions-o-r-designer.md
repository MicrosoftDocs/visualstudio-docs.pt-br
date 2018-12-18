---
title: 'Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (Object Relational Designer) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8b1864fa87867d2f48179c5215a18f2897d9883c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49196190"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>Como: criar métodos DataContext mapeados para procedimentos armazenados e funções (O/R Designer)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Procedimentos armazenados e funções podem ser adicionadas para o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] como <xref:System.Data.Linq.DataContext> métodos. Chamar o método e passar os parâmetros necessários executa a função ou procedimento armazenado no banco de dados e retorna os dados no tipo de retorno do <xref:System.Data.Linq.DataContext> método. Para obter informações detalhadas sobre <xref:System.Data.Linq.DataContext> métodos, consulte [métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md).  
  
> [!NOTE]
>  Os procedimentos armazenados também podem ser usados para substituir o comportamento padrão em tempo de execução de [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] que executa inserções, atualizações e exclusões quando alterações são salvas de classes de entidade para um banco de dados. Para obter mais informações, consulte [como: atribuir procedimentos armazenados para executar atualizações, inserções e exclusões (Designer relacional de objetos)](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md).  
  
## <a name="creating-datacontext-methods"></a>Criando métodos DataContext  
 Você pode criar <xref:System.Data.Linq.DataContext> métodos arrastando procedimentos armazenados ou funções a partir **Server Explorer/Database Explorer** até o [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
> [!NOTE]
>  O tipo de retorno do método <xref:System.Data.Linq.DataContext> gerado varia de acordo com o local onde você solta o procedimento armazenado ou a função no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. Soltar itens diretamente em uma classe de entidade existente cria um método <xref:System.Data.Linq.DataContext> com o tipo de retorno da classe de entidade. Soltar itens em uma área vazia do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] cria um método <xref:System.Data.Linq.DataContext> que retorna um tipo gerado automaticamente. Você pode alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método após adicioná-lo ao painel de métodos. Para inspecionar ou alterar o tipo de retorno de um <xref:System.Data.Linq.DataContext> método, selecione-o e inspecione o **tipo de retorno** propriedade no **propriedades** janela. Para obter mais informações, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>Para criar métodos DataContext que retornam tipos gerados automaticamente  
  
1.  No **Gerenciador de servidores**/**Gerenciador de banco de dados**, expanda o **procedimentos armazenados** nó do banco de dados que você está trabalhando.  
  
2.  Localize o procedimento armazenado desejado e arraste-o para uma área vazia do [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
     O <xref:System.Data.Linq.DataContext> método é criado com um tipo de retorno gerado automaticamente e aparece na **métodos** painel.  
  
#### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>Para criar métodos DataContext com o tipo de retorno de uma classe de entidade  
  
1.  No **Gerenciador de servidores**/**Gerenciador de banco de dados**, expanda o **procedimentos armazenados** nó do banco de dados que você está trabalhando.  
  
2.  Localize o procedimento armazenado desejado e arraste-o para uma classe de entidade existente no [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)].  
  
     O <xref:System.Data.Linq.DataContext> método é criado com o tipo de retorno da classe de entidade selecionada e aparece na **métodos** painel.  
  
> [!NOTE]
>  Para obter informações sobre como alterar o tipo de retorno de existentes <xref:System.Data.Linq.DataContext> métodos, consulte [como: alterar o tipo de retorno de um método DataContext (Designer relacional de objetos)](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md).  
  
## <a name="see-also"></a>Consulte também  
 [Ferramentas LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)   
 [Métodos de DataContext (Designer relacional de objetos)](../data-tools/datacontext-methods-o-r-designer.md)   
 [Passo a passo: Criando Classes LINQ to SQL (Object Relational Designer)](http://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233)   
 [LINQ to SQL](http://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)   
 [Introdução ao LINQ no Visual Basic](http://msdn.microsoft.com/library/3047d86e-0d49-40e2-928b-dc02e46c7984)   
 [Como escrever consultas LINQ em C#](http://msdn.microsoft.com/library/45e47fcc-cfa1-4b72-b161-d038ae87bd23)

