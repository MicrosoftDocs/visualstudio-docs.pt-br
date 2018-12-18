---
title: Exportar e salvar mapas de código
ms.date: 05/16/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.workload:
- multiple
ms.openlocfilehash: abfe8d6160d023a99e9a49480baada9acb0c8243
ms.sourcegitcommit: 209c2c068ff0975994ed892b62aa9b834a7f6077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34268367"
---
# <a name="share-code-maps"></a>Mapas de códigos de compartilhamento

Você pode salvar mapas de código como parte de um projeto do Visual Studio, como uma imagem ou como um arquivo XPS.

## <a name="share-a-code-map-with-other-visual-studio-users"></a>Compartilhar um mapa de código com outros usuários do Visual Studio

Use o **arquivo** menu para salvar o mapa.

-ou-

Para salvar o mapa como parte do projeto específico, na barra de ferramentas do mapa, escolha **compartilhamento** > **mover \<CodeMapName > .dgml em**e, em seguida, escolha o projeto em que você deseja salvar o mapa.

![Mover um mapa em outro projeto](../modeling/media/codemapsmovemapmenu.png)

O Visual Studio salva o mapa como uma *.dgml* arquivo que você pode compartilhar com outros usuários do Visual Studio Enterprise e no Visual Studio Professional.

> [!NOTE]
> Antes de compartilhar um mapa com aqueles que usam o Visual Studio Professional, certifique-se expandir todos os grupos, Mostrar nós ocultos e links entre grupos e recuperar todos os nós excluídos que você deseja ver em seu mapa. Do contrário, outros usuários não poderão consultar esses itens.
>
> O seguinte erro pode ocorrer quando você salvar um mapa que está em um projeto de modelagem ou foi copiado de um projeto de modelagem para outro local:
>
> "Não é possível salvar *fileName* fora do diretório do projeto. Itens vinculados não são compatíveis."
>
> O Visual Studio mostra o erro, mas cria a versão salva de qualquer maneira. Para evitar o erro, crie o mapa fora do projeto de modelagem. Em seguida, é possível salvá-lo no local desejado. Apenas copiar o arquivo para outro local na solução e, em seguida, tentar salvá-lo não funcionará.

## <a name="export-a-code-map-as-an-image"></a>Exportar um mapa de código como uma imagem

Quando você exporta um mapa de código como uma imagem, você pode copiá-lo para outros aplicativos, como Microsoft Word ou PowerPoint.

1. Na barra de ferramentas do mapa de código, escolha **compartilhamento** > **Email como imagem** ou **Copiar imagem**.

2. Cole a imagem em outro aplicativo.

## <a name="export-the-map-as-an-xps-file"></a>Exportar o mapa como um arquivo XPS

Quando você exporta um mapa de código como um arquivo XPS, você poderá ver isso em visualizadores XML ou XAML, como o Internet Explorer.

1. Na barra de ferramentas do mapa de código, escolha **compartilhamento** > **Email como portátil XPS** ou **Salvar como XPS portátil**.

2. Navegue para onde você deseja salvar o arquivo.

3. Nome do mapa de código. Verifique se o **Salvar como tipo** caixa é definida para **arquivos XPS (\*. XPS)**. Escolha **salvar**.

## <a name="see-also"></a>Consulte também

- [Mapear as dependências com mapas de código](../modeling/map-dependencies-across-your-solutions.md)