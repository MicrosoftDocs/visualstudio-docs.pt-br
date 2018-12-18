---
title: Propriedades de decoradores
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, decorators
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 0265146f5b8d03c7b3ac5f2b08b0cb384c3e45a5
ms.sourcegitcommit: 768d7877fe826737bafdac6c94c43ef70bf45076
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50967097"
---
# <a name="properties-of-decorators"></a>Propriedades de decoradores
Os decoradores são ícones, texto ou expandir/recolher divisas que podem aparecer em formas ou conectores no diagrama. As tabelas a seguir mostram as propriedades para os três tipos de decorador. Algumas das propriedades aparecem somente em decoradores de forma ou somente em decoradores do conector.

 Para obter mais informações, consulte [como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md). Para obter mais informações sobre como usar essas propriedades, consulte [personalizando e estendendo uma linguagem específica do domínio](../modeling/customizing-and-extending-a-domain-specific-language.md).

## <a name="expandcollapse-decorator"></a>Expandir/recolher decorador

|Propriedade|Descrição|Padrão|
|-|-|-|
|DisplayName|O nome do decorador que será exibido no designer gerado.|Expandir recolher decorador|
|Nome|O nome do decorador.|ExpandCollapseDecorator|
|Observações|Observações informais associadas esse decorador.|\<Nenhum >|
|HorizontalOffset|O deslocamento horizontal, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|VerticalOffset|O deslocamento vertical, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, relativo à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|Posição|A posição padrão do decorador.|SourceTop|

## <a name="icon-decorator"></a>Ícone de decorador

|Propriedade|Descrição|Padrão|
|-|-|-|
|DefaultIcon|O caminho do arquivo de imagem ou ícone a ser exibido.|\<Nenhum >|
|DisplayName|O nome do decorador a ser exibido no designer gerado.|Ícone de decorador|
|Nome|O nome do decorador.|IconDecorator|
|Observações|Observações informais que estão associadas com o decorador.|\<Nenhum >|
|HorizontalOffset|O deslocamento horizontal, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|VerticalOffset|O deslocamento vertical, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, relativo à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|Posição|A posição padrão do decorador.|SourceTop|

## <a name="textdecorator"></a>TextDecorator

|Propriedade|Descrição|Padrão|
|-|-|-|
|DefaultText|O texto padrão a ser exibido.|Rotular|
|DisplayName|O nome do decorador a ser exibido no designer gerado.|Rotular|
|FontSize|O tamanho da fonte para o texto que é exibido no decorador.|8|
|fontStyle|O estilo da fonte para o texto que é exibido no decorador.|Normal|
|Nome|O nome do decorador.|Rotular|
|Observações|Observações informais que estão associadas com o decorador.|\<Nenhum >|
|HorizontalOffset|O deslocamento horizontal, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|VerticalOffset|O deslocamento vertical, em relação à posição padrão do decorador, em polegadas. (Nas formas somente.)|0|
|OffsetFromLine|O deslocamento do decorador da linha, em relação à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|OffsetFromShape|O deslocamento do decorador da forma, relativo à sua posição padrão, em polegadas. (Nos conectores somente.)|0|
|Posição|A posição padrão do decorador.|TargetBottom|

## <a name="see-also"></a>Consulte também

- [Glossário de ferramentas de linguagem específica do domínio](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)