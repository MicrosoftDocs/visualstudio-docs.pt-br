---
title: Propriedades de decoradores
description: Saiba que decoradores são ícones, texto ou divisas de expansão/ressalvação que podem aparecer em formas ou conectores no diagrama.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 2f3436bb800142e7c85594f4b05cef6fb45c4489
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112390796"
---
# <a name="properties-of-decorators"></a>Propriedades de decoradores
Decoradores são ícones, texto ou divisas de expansão/redação que podem aparecer em formas ou conectores no diagrama. As tabelas a seguir mostram as propriedades dos três tipos de decorador. Algumas das propriedades aparecem apenas em decoradores de forma ou somente em decoradores de conector.

 Para obter mais informações, [consulte How to Define a Domain-Specific Language](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [Personalização](../modeling/customizing-and-extending-a-domain-specific-language.md)e extensão de uma linguagem Domain-Specific .

## <a name="expandcollapse-decorator"></a>Expanda/resvale o decorador

|Propriedade|Descrição|Padrão|
|-|-|-|
|DisplayName|O nome do decorador que será exibido no designer gerado.|Expandir o Decorador de Ressuleção|
|Name|O nome do decorador.|ExpandCollapseDecorator|
|Observações|Observações informais associadas a esse decorador.|\<none>|
|Horizontaloffset|O deslocamento horizontal, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|Verticaloffset|O deslocamento vertical, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|Posição|A posição padrão do decorador.|SourceTop|

## <a name="icon-decorator"></a>Decorador de ícone

|Propriedade|Descrição|Padrão|
|-|-|-|
|Defaulticon|O caminho do ícone ou arquivo de imagem a ser exibido.|\<none>|
|DisplayName|O nome do decorador a ser exibido no designer gerado.|Decorador de ícone|
|Name|O nome do decorador.|IconDecorator|
|Observações|Observações informais associadas ao decorador.|\<none>|
|Horizontaloffset|O deslocamento horizontal, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|Verticaloffset|O deslocamento vertical, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|Posição|A posição padrão do decorador.|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|Propriedade|Descrição|Padrão|
|-|-|-|
|DefaultText|O texto padrão a ser exibido.|Rótulo|
|DisplayName|O nome do decorador a ser exibido no designer gerado.|Rótulo|
|FontSize|O tamanho da fonte para o texto exibido no decorador.|8|
|FontStyle|O estilo da fonte para o texto exibido no decorador.|Regular|
|Name|O nome do decorador.|Rótulo|
|Observações|Observações informais associadas ao decorador.|\<none>|
|Horizontaloffset|O deslocamento horizontal, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|Verticaloffset|O deslocamento vertical, relativo à posição padrão do decorador, em polegadas. (Somente em formas.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, em relação à sua posição padrão, em polegadas. (Somente em conectores.)|0|
|Posição|A posição padrão do decorador.|TargetBottom|

## <a name="see-also"></a>Confira também

- [Glossário das Ferramentas de Linguagem Específica de Domínio](/previous-versions/bb126564(v=vs.100))