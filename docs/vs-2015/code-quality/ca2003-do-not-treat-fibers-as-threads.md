---
title: 'CA2003: não tratar fibras como threads | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2003
- DoNotTreatFibersAsThreads
helpviewer_keywords:
- CA2003
- DoNotTreatFibersAsThreads
ms.assetid: 15398fb1-f384-4bcc-ad93-00e1c0fa9ddf
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a8172490b267949686dd3390c85ed6d86531b192
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521168"
---
# <a name="ca2003-do-not-treat-fibers-as-threads"></a>CA2003: Não tratar fibras como threads
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotTreatFibersAsThreads|
|CheckId|CA2003|
|Categoria|Microsoft. confiabilidade|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um thread gerenciado está sendo tratado como um Thread Win32.

## <a name="rule-description"></a>Descrição da Regra
 Não presuma que um thread gerenciado seja um Thread Win32. É uma fibra. O Common Language Runtime (CLR) executará threads gerenciados como fibras no contexto de threads reais de Propriedade do SQL. Esses threads podem ser compartilhados entre AppDomains e até mesmo bancos de dados no processo de SQL Server. O uso do armazenamento local de threads gerenciados funcionará, mas você não poderá usar o armazenamento local de thread não gerenciado ou supor que seu código será executado no thread do sistema operacional atual novamente. Não altere as configurações, como a localidade do thread. Não chame CreateCriticalSection ou CreateMutex via P/Invoke porque eles exigem que o thread que entra em um bloqueio também deva sair do bloqueio. Como esse não será o caso quando você usa fibras, as seções críticas e exclusões do Win32 serão inúteis no SQL. Você pode usar com segurança a maior parte do estado em um objeto System. thread gerenciado. Isso inclui o armazenamento local de thread gerenciado e a cultura da interface do usuário (IU) atual do thread. No entanto, para fins de modelo de programação, você não poderá alterar a cultura atual de um thread ao usar o SQL; Isso será imposto por meio de uma nova permissão.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Examine seu uso de threads e altere seu código de acordo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Você não deve suprimir essa regra.
