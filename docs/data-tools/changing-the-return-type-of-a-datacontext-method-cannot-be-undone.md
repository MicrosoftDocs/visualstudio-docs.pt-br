---
title: Altere o tipo de retorno de um método DataContext não pode ser desfeito
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 76b161fc-5075-4192-8d94-f15b02e199e9
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 80e7407472188ef25d6fd5127179c7ddbce54318
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85536702"
---
# <a name="changing-the-return-type-of-a-datacontext-method-cannot-be-undone"></a>Altere o tipo de retorno de um método DataContext não pode ser desfeito

A alteração do tipo retornado por um método DataContext não pode ser desfeita. Para reverter de volta para o tipo gerado automaticamente, você deve arraste o item do **Gerenciador de Servidores** ou **Gerenciador de Banco de Dados** no Designer Relacional de Objetos novamente. Tem certeza de que deseja alterar o tipo retornado?

O tipo de retorno de um método de <xref:System.Data.Linq.DataContext> diferem dependendo de onde você ignora o item em [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)]. Se você soltar um item diretamente em uma classe existente de entidade, um método de <xref:System.Data.Linq.DataContext> que tem o tipo de retorno de classe de entidade é criado. Se você soltar um item em uma área vazia de [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)], um método de <xref:System.Data.Linq.DataContext> que retorna um tipo gerado automaticamente é criado. Você pode alterar o tipo de retorno de um método de <xref:System.Data.Linq.DataContext> depois de adicioná-lo ao painel de métodos. Verificar ou altere o tipo de retorno de um método de <xref:System.Data.Linq.DataContext>, selecione-o e clique na propriedade de **Tipo de Retorno** na janela **Propriedades**.

## <a name="to-change-the-return-type-of-a-datacontext"></a>Para alterar o tipo de retorno de um DataContext

- Clique em **Sim**.

## <a name="to-exit-the-message-box-and-leave-the-return-type-unchanged"></a>Para sair da caixa de mensagem e deixar o tipo de retorno inalterado

- Clique em **Não**.

## <a name="to-revert-to-the-original-return-type-after-changing-the-return-type"></a>Para reverter para o tipo de retorno original após alterar o tipo de retorno

1. Selecione o método <xref:System.Data.Linq.DataContext> em [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)] e exclua-o.

2. Localize o item em **Gerenciador de Servidores/Gerenciador de Banco de Dados** e arraste-o até [!INCLUDE[vs_ordesigner_short](../data-tools/includes/vs_ordesigner_short_md.md)].

    Um método de <xref:System.Data.Linq.DataContext> é criado com o tipo de retorno padrão original.

## <a name="see-also"></a>Confira também

- [Ferramentas do LINQ to SQL no Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md)