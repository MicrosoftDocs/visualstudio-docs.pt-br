---
title: Adicionando extensões a definições de DSL | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 07e133be-92ab-4936-a02b-45d2012bd0a6
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 9c3e74f66edc0a8b33ad1fe8205cc02cd0e80054
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49866149"
---
# <a name="adding-extensions-to-dsl-definitions"></a>Adicionando extensões a definições de DSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extensão de definição de DSL permite que você crie um pacote de extensões para uma linguagem específica de domínio (DSL). A extensão DSL, que está contida em um Visual Studio Integration VSIX (extensão), pode ser instalada no computador do usuário da mesma maneira como uma DSL. Os recursos adicionais podem ser habilitados e desabilitados em tempo de execução dinamicamente. DSLs não precisam ser explicitamente criado para a extensão e as extensões podem ser projetadas posteriormente ou por terceiros sem alterar a DSL estendida.  
  
 Os recursos adicionais podem incluir o seguinte:  
  
- Propriedades de elementos de modelo e apresentação  
  
- Decoradores de formas e conectores  
  
- Classes, relações, formas e conectores  
  
- Restrições de validação  
  
- Guias e itens de caixa de ferramentas  
  
  Um usuário de uma DSL estendido pode criar e salvar um modelo que contém as instâncias dos recursos adicionais, e eles podem ser lidos por outros usuários que tenham instalado a extensão apropriada. Os usuários que não tem instalado a extensão não é possível usar os recursos adicionais, mas eles podem atualizar e salvar um modelo sem perder os recursos adicionais.  
  
  Para código de exemplo e obter mais informações sobre esse recurso, consulte o [visualização do Visual Studio e SDK de modelagem](http://go.microsoft.com/fwlink/?LinkID=186128) site da Web.  
  
## <a name="see-also"></a>Consulte também  
 [Visualização do Visual Studio e SDK de modelagem](http://go.microsoft.com/fwlink/?LinkID=186128)



