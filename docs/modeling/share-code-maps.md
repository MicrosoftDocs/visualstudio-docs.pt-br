---
title: Exportar e salvar mapas de código
description: Saiba como você pode salvar mapas de código como parte de um projeto Visual Studio, como uma imagem ou como um arquivo XPS.
ms.custom: SEO-VS-2020
ms.date: 05/16/2018
ms.topic: how-to
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: e58e06c48ed9fa3a9d459c6c615abae4d4b4823f
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385676"
---
# <a name="share-code-maps"></a>Compartilhar mapas de códigos

Você pode salvar mapas de código como parte de um projeto Visual Studio, como uma imagem ou como um arquivo XPS.

## <a name="share-a-code-map-with-other-visual-studio-users"></a>Compartilhar um mapa de código com outros Visual Studio usuários

Use **o** menu Arquivo para salvar o mapa.

– ou –

Para salvar o mapa como parte de um projeto específico, na barra de ferramentas do mapa, escolha Compartilhar Mover  >  **\<CodeMapName> .dgml para** e, em seguida, escolha o projeto no qual você deseja salvar o mapa.

![Mover um mapa para outro projeto](../modeling/media/codemapsmovemapmenu.png)

Visual Studio salva o mapa como um *arquivo .dgml* que você pode compartilhar com outros usuários de Visual Studio Enterprise e Visual Studio Professional.

> [!NOTE]
> Antes de compartilhar um mapa com aqueles que usam Visual Studio Professional, expanda todos os grupos, mostre nós ocultos e links entre grupos e recupere todos os nós excluídos que você deseja que outras pessoas vejam no mapa. Do contrário, outros usuários não poderão consultar esses itens.
>
> O seguinte erro pode ocorrer quando você salva um mapa que está em um projeto de modelagem ou que foi copiado de um projeto de modelagem para outro local:
>
> "Não é possível *salvar fileName* fora do diretório do projeto. Itens vinculados não são compatíveis."
>
> O Visual Studio mostra o erro, mas cria a versão salva de qualquer maneira. Para evitar o erro, crie o mapa fora do projeto de modelagem. Em seguida, é possível salvá-lo no local desejado. Apenas copiar o arquivo para outro local na solução e, em seguida, tentar salvá-lo não funcionará.

## <a name="export-a-code-map-as-an-image"></a>Exportar um mapa de código como uma imagem

Ao exportar um mapa de código como uma imagem, você pode copiá-lo para outros aplicativos, como o Microsoft Word ou o PowerPoint.

1. Na barra de ferramentas do mapa de código, escolha **Compartilhar**  >  **Email como Imagem** ou Copiar **Imagem.**

2. Cole a imagem em outro aplicativo.

## <a name="export-the-map-as-an-xps-file"></a>Exportar o mapa como um arquivo XPS

Ao exportar um mapa de código como um arquivo XPS, você pode vê-lo em visualizadores XML ou XAML como Internet Explorer.

1. Na barra de ferramentas do mapa de código, **escolha Compartilhar** Email  >  **como XPS** Portátil ou Salvar como **XPS Portátil.**

2. Navegue para onde você deseja salvar o arquivo.

3. Nomeia o mapa de código. Certifique-se de que **a caixa Salvar como tipo** está definida como arquivos **XPS ( \* .xps).** Selecione **Salvar**.

## <a name="see-also"></a>Confira também

- [Mapear dependências com mapas de código](../modeling/map-dependencies-across-your-solutions.md)
