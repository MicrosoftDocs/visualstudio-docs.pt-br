---
title: 'CA1030: Usar eventos quando apropriado'
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UseEventsWhereAppropriate
- CA1030
helpviewer_keywords:
- CA1030
- UseEventsWhereAppropriate
ms.assetid: ea051367-deeb-40f9-9b65-eb818f1e133a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ad0659241e75c862b3d82c64a7e8b2ad3ccada21
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547669"
---
# <a name="ca1030-use-events-where-appropriate"></a>CA1030: Usar eventos quando apropriado

|||
|-|-|
|NomeDoTipo|UseEventsWhereAppropriate|
|CheckId|CA1030|
|Categoria|Microsoft.Design|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa

Um nome de método começa com um dos seguintes:

- AddOn
- RemoveOn
- Ativar
- Gera

Por padrão, essa regra só examina os métodos visíveis externamente, mas isso é [configurável](#configurability).

## <a name="rule-description"></a>Descrição da regra

Essa regra detecta métodos que têm nomes que seriam usados normalmente em eventos. Eventos seguem o observador ou o padrão de design de publicação/assinatura; Eles são usados quando uma alteração de estado em um objeto deve ser comunicada a outros objetos. Se um método é chamado em resposta a uma alteração de estado claramente definida, o método deve ser invocado por um manipulador de eventos. Os objetos que chamam o método devem acionar eventos, em vez de chamar o método diretamente.

Alguns exemplos comuns de eventos são encontrados em aplicativos de interface do usuário em que uma ação do usuário, como clicar em um botão, faz com que um segmento de código seja executado. O modelo de evento do .NET não está limitado às interfaces do usuário. Ele deve ser usado em qualquer lugar em que você deve comunicar alterações de estado em um ou mais objetos.

## <a name="how-to-fix-violations"></a>Como corrigir violações

Se o método for chamado quando o estado de um objeto for alterado, considere alterar o design para usar o modelo de evento do .NET.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

Suprimir um aviso dessa regra se o método não funcionar com o modelo de evento do .NET.

## <a name="configurability"></a>Configurabilidade

Se você estiver executando essa regra por meio de analisadores do [FxCop](install-fxcop-analyzers.md) (e não com a análise herdada), poderá configurar em quais partes de sua base de código executar essa regra, com base em sua acessibilidade. Por exemplo, para especificar que a regra deve ser executada somente na superfície da API não pública, adicione o seguinte par chave-valor a um arquivo. editorconfig em seu projeto:

```ini
dotnet_code_quality.ca1030.api_surface = private, internal
```

Você pode configurar essa opção apenas para essa regra, para todas as regras ou para todas as regras nesta categoria (Design). Para obter mais informações, consulte [Configurar analisadores de FxCop](configure-fxcop-analyzers.md).
