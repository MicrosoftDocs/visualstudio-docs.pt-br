---
title: Guia espaço, caixa de diálogo de propriedades do processo | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: c4de1866-7447-48f7-aa88-28ad92c0b930
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: de5df4c55feba8c9aaba0def7585029cc71426b5
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58929414"
---
# <a name="space-tab-process-properties-dialog-box"></a>Guia Espaço, Caixa de diálogo Propriedades do Processo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o **espaço** guia para examinar o espaço de endereço de um processo. Para exibir o [caixa de diálogo de propriedades do processo](../debugger/process-properties-dialog-box.md), mova o foco para um [exibição de processos](../debugger/processes-view.md) janela. Selecione qualquer nó de processo na árvore e escolha **propriedades** da **exibição** menu.  
  
 As seguintes configurações estão disponíveis sobre o **espaço** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Exibir para espaço marcado como**|Use essa caixa de listagem para selecionar a categoria de espaço (imagem, mapeada, reservados ou não atribuídos).|  
|**Bytes Executáveis**|Para a categoria selecionada, a soma de todos os espaços de endereço que esse processo está usando. Memória executável é que podem ser executados por programas, mas pode não ser lidos ou gravados.|  
|**Bytes de Execução-Somente Leitura**|Para a categoria selecionada, a soma de todos os espaços de endereço em uso com as propriedades somente leitura que esse processo está usando. EXEC-memória somente leitura é a memória que pode ser executada, bem como de leitura.|  
|**Bytes de Execução-Leitura-Gravação**|Para a categoria selecionada, a soma de todos os espaços de endereço em uso com as propriedades de leitura / gravação que esse processo está usando. Memória de EXEC e leitura / gravação é aquela que pode ser executada por programas, bem como ler e modificado.|  
|**Cópia de Bytes de gravação de EXEC**|Para a categoria selecionada, a soma de todos os espaços de endereço que podem ser executada por programas, bem como lida e gravada. Esse tipo de proteção é usado quando a memória precisa ser compartilhado entre processos. Se os processos de compartilhamento apenas lerem a memória, todos eles usarão a mesma memória. Se um processo de compartilhamento deseja acesso de gravação, será feita uma cópia da memória para o processo.|  
|**Bytes Não Acessíveis**|Para a categoria selecionada, a soma de todos os espaços de endereço que impede que um processo de usá-lo. Tentativa de leitura ou uma violação de acesso é gerada se a gravação.|  
|**Bytes Somente Leitura**|Para a categoria selecionada, a soma de todos os espaços de endereço que podem ser executado, bem como de leitura.|  
|**Bytes de Leitura-Gravação**|Para a categoria selecionada, a soma de todos os espaços de endereço que permite a leitura e gravação.|  
|**Bytes de Gravação-Cópia**|Para a categoria selecionada, a soma de todos os espaços de endereço que permite o compartilhamento de memória para leitura, mas não para gravação. Quando os processos estão lendo essa memória, eles podem compartilhar a mesma memória. No entanto, quando um processo de compartilhamento deseja ter acesso de leitura/gravação a essa memória compartilhada, é feita uma cópia do que a memória para gravação.|
