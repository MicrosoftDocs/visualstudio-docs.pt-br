---
title: Estrutura de tópicos | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- outlining
- Visual Studio, expand/collapse code
- Visual Studio, outlining
- expand/collapse code
- code [Visual Studio], outlining
- code [Visual Studio], hiding
- outlining code
ms.assetid: d1476758-9d35-4d74-b63c-310661932ecd
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 907d075f597799edd582c9f2bae693eac92c0b2c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544957"
---
# <a name="outlining"></a>Estrutura de tópicos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode optar por ocultar a exibição de algum código recolhendo uma região de código para que ele apareça sob um sinal de adição (+). Você expande uma região recolhida clicando no sinal de adição. (Ou você pode pressionar CTRL + M + M para recolher uma região e, em seguida, CTRL + M + M para expandi-la novamente.) Você também pode recolher uma região de estrutura de tópicos clicando duas vezes em qualquer linha na região na margem da estrutura de tópicos, que aparece apenas à esquerda do código. Você pode ver o conteúdo de uma região recolhida como uma dica de ferramenta quando focaliza a região recolhida.

 As regiões na margem da estrutura de tópicos também são realçadas quando você focaliza a margem com o mouse. A cor de realce padrão pode parecer bastante esmaecida em algumas configurações de cor. Você pode alterá-la em **Ferramentas/Opções/Ambiente/Fontes e Cores/Região Recolhível**.

 Quando você trabalha no código de estrutura de tópicos, pode expandir as seções nas quais deseja trabalhar, recolhê-las quando terminar e passar para outras seções. Quando você não quiser que a estrutura de tópicos seja exibida, você pode usar o comando **Interromper Estrutura de Tópicos** para remover as informações de estrutura de tópicos sem afetar o código subjacente.

 Os comandos **Desfazer** e **Refazer** no menu **Editar** afetam essas ações. As operações de **Copiar**, **Recortar**, **Colar** e do tipo "arrastar e soltar" retêm informações de estrutura de tópico, mas não o estado da região recolhível. Por exemplo, quando você copia uma região recolhida, a operação **Colar** colará o texto copiado como uma região expandida.

> [!CAUTION]
> Quando você altera uma região de estrutura de tópicos, a estrutura de tópicos pode ser perdida. Por exemplo, exclusões ou operações de Localizar e Substituir podem apagar o fim da região.

 Os comandos a seguir podem ser encontrados no submenu **Editar/Estrutura de Tópicos**.

|Comando|Descrição|
|-|-|
|Ocultar Seleção|(CTRL + M, CTRL + H) – recolhe um bloco de código selecionado que normalmente não estaria disponível para a estrutura de tópicos, por exemplo, um bloco `if`. Para remover a região personalizada, use **Interromper Ocultação Atual** (ou CTRL + M, CTRL + U). Não disponível no Visual Basic.|
|Ativar/Desativar Expansão da Estrutura de Tópicos|– Reverte o estado atual oculto ou expandido da seção de estrutura de tópicos mais interna quando o cursor está em uma seção recolhida aninhada.|
|Ativar/Desativar Estrutura de Tópicos para Tudo|(CTRL + M, CTRL + L) – define todas as regiões para o mesmo estado recolhido ou expandido. Se algumas regiões estiverem expandidas e algumas estiverem recolhidas, as regiões recolhidas serão expandidas.|
|Interromper Estrutura de Tópicos|(CTRL + M, CTRL + P) – remove todas as informações de estrutura de tópicos para o documento inteiro.|
|Interromper Ocultação Atual|(CTRL + M, CTRL + U) – remove as informações de estrutura de tópicos para a região definida pelo usuário atualmente selecionada. Não disponível no Visual Basic.|
|Recolher para Definições|(CTRL + M, CTRL + S) – recolhe os membros de todos os tipos.|
|Recolher bloco:\<logical boundary>|(Visual C++) Recolhe uma região na função que contém o ponto de inserção. Por exemplo, se o ponto de inserção estiver dentro de um loop, o loop será ocultado.|
|Recolher tudo em:\<logical structures>|(Visual C++) Recolhe todas as estruturas de dentro da função.|

 Você também pode usar o SDK do Visual Studio para definir as regiões de texto que deseja expandir ou recolher. Consulte [Instruções passo a passo: estrutura de tópicos](../extensibility/walkthrough-outlining.md).
