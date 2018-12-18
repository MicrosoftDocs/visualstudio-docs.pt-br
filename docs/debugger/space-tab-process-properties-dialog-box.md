---
title: Guia de espaço, caixa de diálogo de propriedades do processo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: c4de1866-7447-48f7-aa88-28ad92c0b930
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ee4b5a416c7d3eb466498e7cf4ff727134c0f20f
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31476075"
---
# <a name="space-tab-process-properties-dialog-box"></a>Guia Espaço, Caixa de diálogo Propriedades do Processo
Use o **espaço** guia para examinar o espaço de endereço de um processo. Para exibir o [caixa de diálogo de propriedades do processo](../debugger/process-properties-dialog-box.md), mova o foco para um [exibição processos](../debugger/processes-view.md) janela. Selecione qualquer nó de processo na árvore e escolha **propriedades** do **exibição** menu.  
  
 As configurações a seguir estão disponíveis no **espaço** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Mostrar para espaço marcado como**|Use essa caixa de listagem para selecionar a categoria de espaço (imagem, mapeado, reservados ou não atribuídos).|  
|**Bytes executável**|Para a categoria selecionada, a soma de todos os espaços de endereço que esse processo está usando. Memória executável é que podem ser executadas por programas, mas podem não ser lidos ou gravados.|  
|**Bytes de EXEC-somente leitura**|Para a categoria selecionada, a soma de todos os espaços de endereço em uso com propriedades somente leitura que esse processo está usando. EXEC-memória somente leitura é a memória que pode ser executada, bem como de leitura.|  
|**Bytes de leitura de EXEC**|Para a categoria selecionada, a soma de todos os espaços de endereço em uso com as propriedades de leitura / gravação que esse processo está usando. Memória de EXEC e leitura / gravação é aquela que pode ser executada por programas, bem como ler e modificada.|  
|**Copiar Bytes de gravação de EXEC**|Para a categoria selecionada, a soma de todos os espaços de endereço que podem ser executada por programas, bem como lida e gravada. Esse tipo de proteção é usado quando a memória precisa ser compartilhada entre processos. Se os processos de compartilhamento somente leitura a memória, todos eles usarão a mesma memória. Se um processo de compartilhamento deseja acesso de gravação, será feita uma cópia da memória para o processo.|  
|**Bytes sem acesso**|Para a categoria selecionada, a soma de todos os espaços de endereço que impede que um processo de usá-lo. Tentativa de leitura ou uma violação de acesso será gerada se a gravação.|  
|**Bytes de somente leitura**|Para a categoria selecionada, a soma de todos os espaços de endereço que podem ser executado, bem como de leitura.|  
|**Bytes de leitura / gravação**|Para a categoria selecionada, a soma de todos os espaços de endereço que permite a leitura e gravação.|  
|**Bytes de gravação de cópia**|Para a categoria selecionada, a soma de todos os espaços de endereço que permite memória de compartilhamento para leitura, mas não para gravação. Quando os processos estão lendo essa memória, podem compartilhar a mesma memória. No entanto, quando um processo de compartilhamento deseja ter acesso de leitura/gravação para a memória compartilhada, é feita uma cópia de memória para gravação.|