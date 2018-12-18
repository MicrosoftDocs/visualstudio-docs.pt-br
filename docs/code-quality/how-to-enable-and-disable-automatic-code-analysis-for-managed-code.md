---
title: Habilitar ou desabilitar análise de código
ms.date: 10/25/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: 71a1c44ee775060a25946f79d7c23194e19f0ae9
ms.sourcegitcommit: 1abb9cf4c3ccb90e3481ea8079272c98aad12875
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50143392"
---
# <a name="how-to-enable-and-disable-automatic-code-analysis-for-managed-code"></a>Como: habilitar e desabilitar análise de código automática para código gerenciado

Você pode configurar a análise de código (estático) a ser executado após cada compilação de um projeto de código gerenciado. Você pode definir propriedades de análise para cada configuração de compilação de código diferente, por exemplo, debug e release.

Este artigo se aplica a análise de código apenas como estático e análise de código não em tempo real usando [analisadores de código do Roslyn](roslyn-analyzers-overview.md).

## <a name="to-enable-or-disable-automatic-code-analysis"></a>Para habilitar ou desabilitar análise de código automática

1. Na **Gerenciador de soluções**, clique com botão direito no projeto e, em seguida, escolha **propriedades**.

1. Na caixa de diálogo Propriedades do projeto, escolha o **análise de código** guia.

   > [!TIP]
   > Tipos de projetos mais recentes, como aplicativos .NET Core e .NET Standard não têm uma **análise de código** guia. Análise de código estático não está disponível para esses tipos de projeto, mas você ainda pode obter a análise de código ao vivo usando [analisadores de código do Roslyn](roslyn-analyzers-overview.md). Para suprimir avisos de analisadores de código do Roslyn, consulte a observação no final deste artigo.

1. Especifique o tipo de compilação na **Configuration** e a plataforma de destino na **plataforma**.

1. Para habilitar ou desabilitar a análise de código automática, marque ou desmarque a **habilitar a análise de código no Build** caixa de seleção.

> [!NOTE]
> O **habilitar a análise de código no Build** caixa de seleção afeta somente a análise de código estático. Ele não afeta [analisadores de código do Roslyn](roslyn-analyzers-overview.md), que sempre é executado em compilação se você instalou-los como um pacote do NuGet. Se você quiser limpar erros do analisador do **lista de erros**, você pode suprimir todas as violações atuais, escolhendo **analisar** > **executar análise de código e suprimir Active Directory Problemas** na barra de menus. Para obter mais informações, consulte [suprimir violações](use-roslyn-analyzers.md#suppress-violations).
