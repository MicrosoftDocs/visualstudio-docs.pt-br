---
title: Depuração usando o Visualizador de Store | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Domain-Specific Language, store viewer
- Domain-Specific Language, store
ms.assetid: 0178db2e-ae99-4ed3-9b87-8620fa9fa8e4
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 78a7cad2db2efa8057f2b95d117f93c59cc328cb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49189066"
---
# <a name="debugging-by-using-the-store-viewer"></a>Depurando por meio do Visualizador de Repositório
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Com o visualizador Store, você pode examinar o estado de um *armazenar* usado pelo [!INCLUDE[dsl](../includes/dsl-md.md)]. O Visualizador de Store exibe todos os elementos de modelo de domínio que estão em um repositório específico, juntamente com propriedades de elementos e links entre elementos.  
  
## <a name="opening-store-viewer"></a>Visualizador de Store de abertura  
 Quando você está no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] experimental build, pare seu código em um ponto de interrupção em que uma instância do repositório contém informações de modelo. Em seguida, abra o Visualizador de Store digitando o seguinte comando na **imediato** janela:  
  
```  
Microsoft.VisualStudio.Modeling.Diagnostics.StoreViewer.Show(mystore);  
```  
  
> [!NOTE]
>  Você deve substituir `mystore` com o nome da sua instância do repositório. Além disso, se você adicionar o namespace ao seu código, você pode digitar o comando para exibir o Visualizador de Store sem o namespace totalmente qualificado:  
>   
>  `using Microsoft.VisualStudio.Modeling.Diagnostics;`  
>   
>  `…`  
>   
>  `StoreViewer.Show(mystore);`  
  
 O `Show` método tem várias sobrecargas. Você pode especificar uma instância de um repositório ou uma partição como o parâmetro.  
  
 Como alternativa, você pode colocar a linha de código que exibe o Visualizador de Store em qualquer lugar em seu código em que o parâmetro que você passa para o `Show` método está no escopo. Essa ação exibe o visualizador Store quando a linha de código é executado como um instantâneo do conteúdo do repositório.  
  
### <a name="using-store-viewer"></a>Usando o Visualizador de Store  
 Quando o Visualizador de Store for aberta, uma janela não restrita do Windows Forms é exibida, como mostra a ilustração a seguir.  
  
 ![](../modeling/media/storeviewer2.png "storeviewer2")  
Visualizador de Store  
  
 O Visualizador de Store tem três painéis: o painel esquerdo, o painel superior direito e o painel inferior direito. O painel esquerdo é uma exibição de árvore dos tipos no `DomainDataDirectory` membro de um repositório. Se você expandir o nó de partição e clique em um elemento, propriedades do elemento são exibidos no painel superior direito. Se o elemento é vinculado a outros elementos, os elementos adicionais aparecem no painel inferior direito. Se você clicar duas vezes um elemento no painel inferior direito, o elemento é realçado no painel esquerdo.  
  
## <a name="see-also"></a>Consulte também  
 [Navegando por um modelo no código do programa e atualizando-o](../modeling/navigating-and-updating-a-model-in-program-code.md)



