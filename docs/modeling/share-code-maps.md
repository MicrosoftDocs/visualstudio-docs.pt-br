---
title: Exportar e salvar mapas de código
ms.date: 05/16/2018
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ef7f72010623d20e79a327877a512f0b7352bac5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542565"
---
# <a name="share-code-maps"></a>Compartilhar mapas de códigos

Você pode salvar mapas de código como parte de um projeto do Visual Studio, como uma imagem ou como um arquivo XPS.

## <a name="share-a-code-map-with-other-visual-studio-users"></a>Compartilhar um mapa de código com outros usuários do Visual Studio

Use o menu **arquivo** para salvar o mapa.

-ou-

Para salvar o mapa como parte do projeto específico, na barra de ferramentas do mapa, escolha **compartilhar**  >  **mover \<CodeMapName> . dgml em**e, em seguida, escolha o projeto no qual você deseja salvar o mapa.

![Mover um mapa para outro projeto](../modeling/media/codemapsmovemapmenu.png)

O Visual Studio salva o mapa como um arquivo *. dgml* que você pode compartilhar com outros usuários de Visual Studio Enterprise e Visual Studio Professional.

> [!NOTE]
> Antes de compartilhar um mapa com aqueles que usam Visual Studio Professional, certifique-se de expandir todos os grupos, mostrar nós ocultos e links entre grupos e recuperar os nós excluídos que você deseja que outras pessoas vejam no mapa. Do contrário, outros usuários não poderão consultar esses itens.
>
> O erro a seguir pode ocorrer quando você salva um mapa que está em um projeto de modelagem ou foi copiado de um projeto de modelagem para outro local:
>
> "Não é possível salvar o *nome de arquivo* fora do diretório do projeto. Itens vinculados não são compatíveis."
>
> O Visual Studio mostra o erro, mas cria a versão salva de qualquer maneira. Para evitar o erro, crie o mapa fora do projeto de modelagem. Em seguida, é possível salvá-lo no local desejado. Apenas copiar o arquivo para outro local na solução e, em seguida, tentar salvá-lo não funcionará.

## <a name="export-a-code-map-as-an-image"></a>Exportar um mapa de código como uma imagem

Ao exportar um mapa de código como uma imagem, você pode copiá-lo em outros aplicativos, como o Microsoft Word ou o PowerPoint.

1. Na barra de ferramentas do mapa de códigos, escolha **compartilhar**  >  **email como imagem** ou **copiar imagem**.

2. Cole a imagem em outro aplicativo.

## <a name="export-the-map-as-an-xps-file"></a>Exportar o mapa como um arquivo XPS

Ao exportar um mapa de código como um arquivo XPS, você pode vê-lo em visualizadores XML ou XAML como o Internet Explorer.

1. Na barra de ferramentas do mapa de códigos, escolha **compartilhar**  >  **email como XPS portátil** ou **salvar como XPS portátil**.

2. Navegue para onde você deseja salvar o arquivo.

3. Nomeie o mapa de código. Verifique se a caixa **salvar como tipo** está definida como **arquivos XPS ( \* . XPS)**. Selecione **Salvar**.

## <a name="see-also"></a>Consulte também

- [Mapear dependências com mapas de código](../modeling/map-dependencies-across-your-solutions.md)
