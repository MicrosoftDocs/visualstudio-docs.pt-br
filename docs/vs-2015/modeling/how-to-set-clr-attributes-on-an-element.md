---
title: 'Como: definir atributos CLR em um elemento | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.dsltools.EditAttributesDialog
helpviewer_keywords:
- Domain-Specific Language, custom attrributes
ms.assetid: b3db3c74-920c-4701-9544-6f75cbe8b7c9
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: b77e0f1f31c0f617e80a27de4e1d0ab1d0b3d2eb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49263977"
---
# <a name="how-to-set-clr-attributes-on-an-element"></a>Como definir atributos CLR em um elemento
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Atributos personalizados são atributos especiais que podem ser adicionados a diagramas, formas, conectores e elementos de domínio. Você pode adicionar qualquer atributo que herda o `System.Attribute` classe.  
  
### <a name="to-add-a-custom-attribute"></a>Para adicionar um atributo personalizado  
  
1.  No **Gerenciador de DSL**, selecione o elemento ao qual você deseja adicionar um atributo personalizado.  
  
2.  No **propriedades** janela, ao lado de **atributos personalizados** propriedade, clique no botão Procurar (**...** ) ícone.  
  
     O **editar atributos** caixa de diálogo é aberta.  
  
3.  No **nome** coluna, clique em  **\<Adicionar atributo >** e digite o nome do seu atributo. Pressione ENTER.  
  
4.  A linha sob o nome do atributo mostra parênteses. Nessa linha, digite um tipo de parâmetro para o atributo (por exemplo, `string`), e pressione ENTER.  
  
5.  No **nome da propriedade** coluna, digite um nome apropriado, por exemplo, `MyString`.  
  
6.  Clique em **OK**.  
  
     O **atributos personalizados** propriedade agora exibe o atributo no seguinte formato:  
  
     `[` *AttributeName* `(` *ParameterName* `=` *tipo* `)]`  
  
## <a name="see-also"></a>Consulte também  
 [Glossário de ferramentas de linguagem específica do domínio](http://msdn.microsoft.com/en-us/ca5e84cb-a315-465c-be24-76aa3df276aa)



