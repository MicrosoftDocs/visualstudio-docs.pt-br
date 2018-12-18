---
title: 'CA2003: não tratar fibras como threads'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 3322b968266ad6fdfe1be2e5bdaac73aad32b9c7
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45551906"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003: não tratar fibras como threads

|||
|-|-|
|NomeDoTipo|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|Categoria|Microsoft.Reliability|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa

Um thread gerenciado está sendo tratado como um thread do Win32.

## <a name="rule-description"></a>Descrição da regra

Não pressuponha que um thread gerenciado é um thread do Win32. é uma fibra. O common language runtime (CLR) executa os threads gerenciados como fibras no contexto de threads reais que são de propriedade de SQL. Esses threads podem ser compartilhados entre AppDomains e até mesmo bancos de dados no processo do SQL Server. Usando gerenciado funciona o armazenamento local de thread, mas não pode usar o armazenamento local de thread não gerenciado ou supor que seu código será executado novamente no thread atual do sistema operacional. Não altere as configurações como a localidade do thread. Não chame CreateCriticalSection ou CreateMutex via P/Invoke porque eles requerem que o thread que entra em um bloqueio também deve sair do bloqueio. Porque o thread que entra em um bloqueio não sair de um bloqueio ao usar fibras, mutexes e seções críticas do Win32 são inúteis no SQL. Com segurança você pode usar a maioria do estado em um gerenciado <xref:System.Threading.Thread> objeto, incluindo o armazenamento local de thread gerenciado e a cultura de interface do usuário do usuário atual do thread. No entanto, para motivos de modelo de programação, você não poderá alterar a cultura atual de um thread quando você usa o SQL. Essa limitação será imposta por meio de uma nova permissão.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Examine o uso de threads e altere seu código adequadamente.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Não suprima essa regra.