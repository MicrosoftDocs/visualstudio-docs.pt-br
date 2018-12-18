---
title: Avisos de portabilidade
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- vs.codeanalysis.PortabilityRules
helpviewer_keywords:
- portability warnings
- managed code analysis warnings, portability warnings
- warnings, portability
ms.assetid: 902e859a-2153-4970-baaa-8a5b4a11806f
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 81f463656894b9c6a9c13b28560ad310eaa6c9df
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31920438"
---
# <a name="portability-warnings"></a>Avisos de portabilidade
Avisos de portabilidade suportam a portabilidade entre diferentes sistemas operacionais.

## <a name="in-this-section"></a>Nesta seção

|Regra|Descrição|
|----------|-----------------|
|[CA1900: os campos de tipo de valor devem ser móveis](../code-quality/ca1900-value-type-fields-should-be-portable.md)|Esta regra verifica se estruturas que são declaradas usando um atributo de layout explícito serão alinhado corretamente quando passa por marshaling para código não gerenciado em sistemas operacionais de 64 bits.|
|[CA1901: Declarações P/Invoke devem ser portáteis](../code-quality/ca1901-p-invoke-declarations-should-be-portable.md)|Essa regra avalia o tamanho de cada parâmetro e o valor de retorno de um P/Invoke e verifica se o seu tamanho é correto quando passa por marshaling para código não gerenciado em sistemas operacionais de 32 bits e 64 bits.|
|[CA1903: usar apenas a API da estrutura de destino](../code-quality/ca1903-use-only-api-from-targeted-framework.md)|Um membro ou um tipo está usando um membro ou um tipo que foi introduzido em um service pack não incluído com a estrutura de destino do projeto.|