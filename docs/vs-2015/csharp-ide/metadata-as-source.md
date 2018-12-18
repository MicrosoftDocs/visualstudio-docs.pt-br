---
title: Metadados como origem | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- Go To Definition command
- Code Definition window, viewing metadata as source
- metadata as source [C#]
ms.assetid: 4945a07f-b3be-4f05-a587-fc29058aa8fa
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8bcac8071d0cc76c29a5b9d0478727fea0b59901
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49232941"
---
# <a name="metadata-as-source"></a>Metadados como origem
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Metadados como origem permite que você exiba os metadados que aparece como código-fonte c# em um buffer somente leitura. Isso permite que uma exibição das declarações de tipos e membros (sem implementações). Você pode exibir metadados como origem, executando o **ir para definição** comando para tipos ou membros cujo código-fonte não está disponível no seu projeto ou solução.  
  
> [!NOTE]
>  Quando você tenta executar o **ir para definição** de comando para tipos ou membros que são marcados como internos, o ambiente de desenvolvimento integrado (IDE) exibe seus metadados como origem, independentemente se o assembly de referência é um amigo ou não.  
  
 Você pode exibir metadados como origem em qualquer Editor de códigos ou o **definição de código** janela.  
  
## <a name="viewing-metadata-as-source-in-the-code-editor"></a>Exibindo metadados como origem no Editor de códigos  
 Quando você executa o **ir para definição** comando de um item cujo código-fonte não está disponível, um documento com guias que contém uma exibição de metadados do item, exibidos como código-fonte, é exibida no Editor de códigos. O nome do tipo, seguido por **[de metadados]**, aparece na guia do documento.  
  
 Por exemplo, se você executar o **ir para definição** comando <xref:System.Console>, metadados para <xref:System.Console> aparece no Editor de código como código-fonte c# que se parece com sua declaração, mas sem uma implementação.  
  
 ![Metadados como Origem](../csharp-ide/media/metadatasource.png "MetadataSource")  
  
## <a name="viewing-metadata-as-source-in-the-code-definition-window"></a>Exibindo metadados como origem na janela de definição de código  
 Quando o **definição de código** janela está ativa ou visível, o IDE executa automaticamente a **ir para definição** comando para itens sob o cursor no Editor de códigos e para os itens selecionados no  **Exibição de classe** ou o **Pesquisador de objetos**. Se o código-fonte não está disponível para esse item, o IDE exibirá os metadados do item como fonte na **definição de código** janela.  
  
 Por exemplo, se você colocar o cursor dentro da palavra <xref:System.Console> no Editor de código, metadados para <xref:System.Console> aparece como código-fonte na **definição de código** janela. A fonte é semelhante a <xref:System.Console> declaração, mas sem uma implementação.  
  
 Se você quiser ver a declaração de um item que aparece na **definição de código** janela, clique com o botão direito e clique em **ir para definição**.