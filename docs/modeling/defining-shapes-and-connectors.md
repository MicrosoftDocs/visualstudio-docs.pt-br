---
title: Definindo formas e conectores
description: Saiba mais sobre os vários tipos básicos de formas que você pode usar para exibir informações sobre um diagrama em uma DSL (linguagem específica do domínio).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 622ff598ac2471814e51b0e268c12d40e726fb98
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385741"
---
# <a name="define-shapes-and-connectors"></a>Definir formas e conectores

Há diversos tipos básicos de formas possíveis de serem usados para exibir informações em um diagrama em uma linguagem específica do domínio (DSL).

## <a name="basic-types-of-shapes-and-connectors"></a><a name="shapeTypes"></a> Tipos básicos de formas e conectores

Um diagrama DSL mostra uma coleção de *formas* interlinkadas por linhas *ou conectores*. Geralmente, mas não sempre:

- As formas são representações visíveis dos elementos de modelo.

- Os conectores representam as relações de referência.

- O diagrama representa a instância da raiz do modelo.

- Relações de incorporações entre os elementos de modelo são mostradas por confinamento. Por exemplo, os elementos que representam portas de componentes são incorporados no componente.

Esses padrões não são impostos, mas têm melhor suporte. Quando você projetar uma DSL, tenha em mente que o design das relações de incorporação deve ser influenciado por como você deseja apresentar o modelo na tela. Por outro lado, as relações de referência devem refletir os conceitos de seu domínio dos negócios.

Os seguintes tipos de formas estão disponíveis:

|Tipo de forma|Descrição|
|-|-|
|Forma geométrica|Forma retangular ou elíptica de propósito geral. É possível exibir o texto e os decoradores de ícones em posições específicas relativas aos limites da forma. Você também pode aninhar formas dentro de formas de geometria.|
|Forma do compartimento|Retângulo contendo um cabeçalho e compartimentos, com uma classe UML. Cada compartimento pode conter uma lista de linhas de texto.<br /><br /> As linhas geralmente representam elementos incorporados sob o elemento representado pela forma. Por exemplo, criar uma DSL a partir de um modelo de solução de Diagramas de Classe.|
|Forma da imagem|Forma que exibe uma imagem.|
|Forma da porta|Um pequeno retângulo projetado para anexar o esboço de outra forma. Geralmente usado em modelos do componente.<br /><br /> O elemento de modelo representado por uma porta normalmente é incorporado sob o elemento representado pela forma pai. Por exemplo, criar uma DSL usando o modelo de solução de Componentes.<br /><br /> Por padrão, uma forma de porta pode deslizar ao longo das laterais de seu pai. É possível definir uma Regra de Associação para restringi-la a uma determinada posição.<br /><br /> Fazendo uma forma de porta muito pequena e transparente, é possível usá-la para fornecer um ponto de conexão fixo na superfície da sua forma pai.|
|Raias|Partição de raias de um diagrama em segmentos horizontais ou verticais. A raia sempre permanece abaixo de outras formas no diagrama.<br /><br /> Geralmente, os elementos de modelo da raia são criados na raiz do modelo e outros elementos são criados neles. Por exemplo, criar uma DSL a partir de um modelo de solução de Fluxo de Tarefa.|
|Conectores|As linhas desenhadas entre as formas normalmente representam relações de referência. É possível ajustar opções para tornar um conector reto ou retilíneo e para ter diferentes tipos de seta.|

## <a name="shape-inheritance"></a>Herança de forma

Uma forma pode ser herdeira de outra forma. No entanto, as formas devem ser do mesmo tipo. Por exemplo, somente uma forma geométrica pode ser herdeira de uma forma geométrica. Formas herdadas possuem os compartimentos e decoradores de sua forma de base. Os conectores podem ser herdeiros dos conectores.
