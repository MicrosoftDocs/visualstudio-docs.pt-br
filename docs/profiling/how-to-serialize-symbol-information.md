---
title: Serializar informações de símbolo | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- VS.ToolsOptionsPages.Performance.General
helpviewer_keywords:
- profiling tools, serializing symbol information
- performance tools, serializing symbol information
ms.assetid: 9e0da706-6325-4073-83d1-aeab3b7c137a
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: d644960153a8e342f6442f3750420ea68a61b38f
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851587"
---
# <a name="how-to-serialize-symbol-information"></a>Como serializar informações de símbolo
Você pode serializar os símbolos que são necessários para analisar seu aplicativo. A serialização de símbolos adiciona símbolos ao arquivo .*vsp*. Ao adicionar informações de símbolo ao arquivo .*vsp*, outras pessoas podem analisar um relatório de desempenho sem ter acesso aos símbolos originais. Se os símbolos não forem serializados, você precisará ter os arquivos originais instrumentados .*exe* e .*pdb* para analisar o arquivo .*vsp*.

### <a name="to-automatically-serialize-symbol-information"></a>Para serializar informações de símbolo automaticamente

1. No menu **Ferramentas** , clique em **Opções**.

     A caixa de diálogo **Opções** é exibida.

2. Clique em **Ferramentas de Desempenho**.

3. Em **Configuração Geral**, selecione **Serializar informações de símbolo automaticamente**.

## <a name="see-also"></a>Confira também
- [Configurar sessões de desempenho](../profiling/configuring-performance-sessions.md)
- [Como: consultar informações de símbolo do Windows](../profiling/how-to-reference-windows-symbol-information.md)
- [Como salvar arquivos de relatório analisados](/previous-versions/visualstudio/visual-studio-2010/bb763106\(v\=vs.100\))
