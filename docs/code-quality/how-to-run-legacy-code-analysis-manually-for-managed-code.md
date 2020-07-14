---
title: Como executar a análise de código herdada manualmente para código gerenciado
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: Mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 44190f8e828f9a971f15b57266978603dcac8139
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462056"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>Como executar a análise de código herdada manualmente para código gerenciado
A ferramenta de análise de código fornece informações sobre possíveis defeitos em seu código-fonte. Você pode executar a análise de código automaticamente com cada compilação de um projeto de código e também pode executar a análise de código manualmente. As regras que são verificadas quando a análise de código é executada são especificadas na página análise de código das páginas de propriedades do projeto. Para obter mais informações, consulte [como: configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md).

## <a name="to-run-code-analysis-manually"></a>Para executar a análise de código manualmente

1. Se você estiver no Visual Studio 2019 versão 16,5 ou posterior, execute o seguinte comando no prompt de comando antes de iniciar o Visual Studio:

```
set EnableLegacyCodeAnalysis = true
```

2. Em **Gerenciador de soluções**, clique no projeto.

3. No menu **analisar** , clique em **executar análise de código no** *nome do projeto*.

