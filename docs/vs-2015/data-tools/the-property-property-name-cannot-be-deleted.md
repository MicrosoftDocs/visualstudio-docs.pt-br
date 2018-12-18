---
title: A propriedade &lt;nome da propriedade&gt; não pode ser excluída | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 55873f74-7834-4ec1-8815-eeeb65618d87
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 98b065500c9c881a7190b59c4d70a0433eb8864c
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49186518"
---
# <a name="the-property-ltproperty-namegt-cannot-be-deleted"></a>A propriedade &lt;nome da propriedade&gt; não pode ser excluído
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A propriedade \<nome da propriedade > não pode ser excluído porque ele está definido como a propriedade de discriminador para herança entre \<nome da classe > e \<nome de classe >  
  
 A propriedade selecionada é definida como o **propriedade discriminatória** para herança entre as classes mencionadas na mensagem de erro. Propriedades não podem ser excluídas estão participando na configuração de herança entre classes de dados.  
  
 Defina as **propriedade discriminatória** a uma propriedade diferente da classe de dados para permitir a exclusão de bem-sucedida da propriedade desejada.  
  
### <a name="to-correct-this-error"></a>Para corrigir este erro  
  
1.  Em object relational Designer de Objetos, selecione a linha de herança que conecta as classes de dados mencionadas na mensagem de erro.  
  
2.  Defina as **discriminador** propriedade a uma propriedade diferente.  
  
3.  Tente excluir novamente a propriedade.  
  
## <a name="see-also"></a>Consulte também  
 [Como: configurar a herança usando o Designer relacional de objetos](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)   
 [Herança de classe de dados (O/R Designer)](../data-tools/data-class-inheritance-o-r-designer.md)   
 [Passo a passo: criando classes LINQ to SQL usando a herança de tabela única (Designer Relacional de Objetos)](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)

