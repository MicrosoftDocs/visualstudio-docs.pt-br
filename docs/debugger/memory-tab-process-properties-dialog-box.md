---
title: Guia de memória, a caixa de diálogo de propriedades do processo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: reference
helpviewer_keywords:
- Process properties for Windows NT
ms.assetid: a70785f2-5997-40ec-a90f-80a52449768b
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b43dd047e4ebdb145092dc3b9f37098b8db6322e
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31474613"
---
# <a name="memory-tab-process-properties-dialog-box"></a>Guia Memória, Caixa de diálogo Propriedades do Processo
Use o **memória** guia para mostrar como um processo usa a memória. Para exibir o [caixa de diálogo de propriedades do processo](../debugger/process-properties-dialog-box.md), mova o foco para um [exibição processos](../debugger/processes-view.md) janela. Selecione qualquer nó de processo na árvore e escolha **propriedades** do **exibição** menu.  
  
 As configurações a seguir estão disponíveis no **memória** guia:  
  
|Entrada|Descrição|  
|-----------|-----------------|  
|**Bytes virtuais**|O tamanho atual (em bytes) de espaço de endereço virtual que o processo está usando. O uso do espaço de endereço virtual não implica necessariamente o uso correspondente de disco ou páginas de memória principal. No entanto, o espaço virtual é finito e muito usando pode limitar a capacidade do processo de carregar bibliotecas.|  
|**Máximo de Bytes virtuais**|O número máximo de bytes de espaço de endereço virtual do processo usou a qualquer momento.|  
|**Conjunto de trabalho**|O conjunto de páginas de memória utilizadas recentemente pelos threads no processo. Se a memória livre no computador estiver acima de um limite, páginas são deixadas no conjunto de trabalho de um processo mesmo que não estejam em uso. Quando a memória livre fica abaixo do limite, páginas são excluídas do conjunto de trabalho. Se forem necessários, eles serão reinseridas no conjunto de trabalho por falha de software antes de sair da memória principal.|  
|**Conjunto de trabalho de pico**|O número máximo de páginas no conjunto de trabalho desse processo a qualquer momento.|  
|**Bytes de Pool paginável**|A quantidade atual de pool paginável que o processo alocou. Pool paginado é uma área de memória do sistema em que os componentes de sistema operacional adquirem espaço conforme eles realizar suas tarefas indicadas. Páginas de pool paginável podem ser paginadas para o arquivo de paginação quando não são acessados pelo sistema prolongada períodos de tempo.|  
|**Bytes de Pool não-paginável**|O número atual de bytes de pool não paginável alocada pelo processo. O pool não-paginável é uma área de memória do sistema onde o espaço é adquirido por componentes do sistema operacional conforme eles realizar suas tarefas indicadas. Páginas de pool não-paginável não podem ser paginadas para o arquivo de paginação; eles permanecem na memória principal, enquanto estiverem alocados.|  
|**Bytes particulares**|O número atual de bytes que o processo alocou que não pode ser compartilhado com outros processos.|  
|**Bytes livres**|O espaço total de endereço virtual não utilizado do processo.|  
|**Bytes reservados**|A quantidade total de memória virtual reservada para uso futuro por esse processo.|  
|**Bytes de imagem livres**|A quantidade de espaço de endereço virtual que não está em uso ou reservado por imagens no processo.|  
|**Bytes de imagem reservados**|A soma de toda a memória virtual reservada por imagens executadas no processo.|