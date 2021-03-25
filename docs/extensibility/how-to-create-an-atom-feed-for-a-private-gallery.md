---
title: 'Como: criar um Feed Atom para uma galeria privada | Microsoft Docs'
description: Você pode criar um Feed Atom (RSS) para um local de intranet que contém extensões e adicionar o feed a extensões e atualizações como uma galeria privada.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Atom feed, VSIX private galleries
- VSIX private galleries, Atom feed
ms.assetid: 5897f538-9c41-486f-97d9-a1976d20d9fd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2a83d5aa68f6f631243fbbfcad7cf28b25e7bc70
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057371"
---
# <a name="how-to-create-an-atom-feed-for-a-private-gallery"></a>Como: criar um Feed Atom para uma galeria privada
Você pode criar um Feed Atom (RSS) para um local de intranet que contém extensões e adicionar o feed a **extensões e atualizações** como uma galeria privada. Saiba mais em [Galerias privadas](../extensibility/private-galleries.md).

## <a name="create-an-atom-feed"></a>Criar um feed ATOM
 Para criar um Feed Atom como uma galeria privada, primeiro você coleta suas extensões (arquivos *. vsix* ) em uma pasta. Você pode organizá-los em subpastas, se desejar. Você também precisará dos seguintes recursos:

- Um arquivo de *atom.xml* que torna as extensões disponíveis como uma galeria privada. Para obter informações sobre como conectar o arquivo de *atom.xml* a **extensões e atualizações**, consulte [galerias particulares](../extensibility/private-galleries.md).

- Uma pasta que contém os arquivos de imagem que foram extraídos das extensões (por exemplo, capturas de tela). O arquivo de *atom.xml* contém links relativos a essas imagens para que elas estejam disponíveis em **extensões e atualizações**.

  Por exemplo, suponha que você reuniu as duas extensões a seguir em uma pasta:

- *Template_Wizard_239. vsix*, que é um modelo de projeto VSIX vazio.

- *SelectionHighlight. vsix*, que é uma ferramenta para realçar todas as instâncias de uma palavra selecionada.

  O conteúdo do arquivo de *atom.xml* seria semelhante ao exemplo a seguir:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<feed xmlns="http://www.w3.org/2005/Atom">
  <title type="text" />
  <id>uuid:bcecded5-97c8-4d24-96f1-7d9e16652433;id=1</id>
  <updated>2011-04-14T21:25:48Z</updated>
  <entry>
    <id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</id>
    <title type="text">Highlight all occurrences of selected word</title>
    <summary type="text">This extends the editor to highlight ....</summary>
    <published>2011-04-14T14:24:51-07:00</published>
    <updated>2011-04-14T14:24:22-07:00</updated>
    <author>
      <name>Microsoft</name>
    </author>
    <link rel="icon" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_Icon_SelectionHighlightIcon.jpg" />
    <link rel="previewimage" href="VSIXImages/SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa_PreviewImage_SelectionHighlight.jpg" />
    <content type="application/octet-stream" src="SelectionHighlight.vsix" />
    <Vsix xmlns="http://schemas.microsoft.com/developer/vsx-syndication-schema/2010" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Id>SelectionHighlight..a14874d2-8199-4a60-af8a-11d6447813aa</Id>
      <Version>1.31</Version>
      <References />
      <Rating xsi:nil="true" />
      <RatingCount xsi:nil="true" />
      <DownloadCount xsi:nil="true" />
    </Vsix>
  </entry>
  <entry>
    <id>Template_Wizard_239.Microsoft.3b38a7e3-5cbc-4389-a92a-d82tyc2ed592</id>
    ...
  </entry>
</feed>
```

 Observe que as duas marcas de link se referem a capturas de tela na pasta gerada de imagens.

## <a name="see-also"></a>Confira também
- [Galerias privadas](../extensibility/private-galleries.md)
