---
title: Como excluir ou incluir funções curtas na instrumentação | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profiling tools, instrument events
- profiling tools, include short functions
- profiling tools, exclude short functions
ms.assetid: eaeead79-aafe-4490-86ff-6ed4cad9c15f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6c6234db781925e8c0558513cb7e8bc608b5cfea
ms.sourcegitcommit: 1b9c1e333c2f096d35cfc77e846116f8e5054557
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814678"
---
# <a name="how-to-exclude-or-include-short-functions-from-instrumentation"></a>Como excluir ou incluir funções curtas da instrumentação
Por padrão, as ferramentas de Criação de Perfil excluem *Pequenas Funções* da instrumentação. As pequenas funções são funções curtas que não fazem nenhuma chamada de função. A exclusão dessas pequenas funções fornece menor sobrecarga devido à instrumentação e, portanto, velocidade de instrumentação aprimorada. A exclusão de funções pequenas também reduz o tamanho do arquivo (.*vsp*) de dados de criação de perfil de desempenho e o tempo necessário para análise. Se as pequenas funções forem excluídas, o tempo gasto nas pequenas funções contará em relação ao tempo de exclusão e inclusão de suas funções pai. As pequenas funções podem ser excluídas ou incluídas na instrumentação, conforme descrito no procedimento a seguir.  
  
### <a name="to-exclude-or-include-short-functions-from-instrumentation"></a>Para excluir ou incluir funções curtas na instrumentação  
  
1.  No **Gerenciador de Desempenho**, selecione **Sessão de Desempenho** e, em seguida, clique com o botão direito do mouse em **Propriedades**.  
  
     A caixa de diálogo **Páginas de Propriedades** é exibida.  
  
2.  Nas **Páginas de Propriedades**, clique nas propriedades de **Instrumentação**.  
  
3.  Para excluir funções curtas da instrumentação, selecione **Excluir funções curtas da Instrumentação**. Essa é a configuração padrão.  
  
     -ou-  
  
     Para incluir funções curtas na instrumentação, desmarque **Excluir funções curtas da Instrumentação**.  
  
4.  Clique em **OK**.  
  
## <a name="see-also"></a>Consulte também  
 [Coleta de dados de controle](../profiling/controlling-data-collection.md)   
 [Propriedades da sessão de desempenho](../profiling/performance-session-properties.md)