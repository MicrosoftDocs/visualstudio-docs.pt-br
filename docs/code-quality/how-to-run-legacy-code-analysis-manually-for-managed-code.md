---
title: Executar análise de código herdado manualmente (.NET)
description: Saiba como detectar possíveis defeitos no código-fonte. Veja como executar a análise de código herdada manualmente no código gerenciado no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- code analysis, running
ms.assetid: 5086d228-f92e-4515-9708-c5b89b9e9a03
author: Mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: f214ac47ad3d831432b91652c5bbe3249ce5f1c5
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223479"
---
# <a name="how-to-run-legacy-code-analysis-manually-for-managed-code"></a>Como executar a análise de código herdada manualmente para código gerenciado

A ferramenta de análise de código fornece informações sobre possíveis defeitos em seu código-fonte. Você pode executar a análise de código automaticamente com cada compilação de um projeto de código e também pode executar a análise de código manualmente. As regras que são verificadas quando a análise de código é executada são especificadas na página análise de código das páginas de propriedades do projeto. Para obter mais informações, consulte [como: configurar a análise de código para um projeto de código gerenciado](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md).

## <a name="to-run-code-analysis-manually"></a>Para executar a análise de código manualmente

1. Se você estiver no Visual Studio 2019 versão 16,5 ou posterior, execute o seguinte comando no prompt de comando antes de iniciar o Visual Studio:

```
setx EnableLegacyCodeAnalysis true
```

2. Em **Gerenciador de soluções**, clique no projeto.

3. No menu **analisar** , clique em **executar análise de código no** *nome do projeto*.
