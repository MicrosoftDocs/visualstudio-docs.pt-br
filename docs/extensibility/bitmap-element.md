---
title: Elemento bitmap | Microsoft Docs
description: O elemento bitmap define um bitmap. O bitmap é carregado a partir de um recurso ou de um arquivo. Este artigo contém um exemplo.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Bitmaps
- Bitmaps element (VSCT XML schema)
ms.assetid: edcd7891-f4e7-416d-809d-5e2eed9f17e4
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c8f3daf25a3ffe025bcdef65dbaa6def942d0fb4
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112903314"
---
# <a name="bitmap-element"></a>Elemento bitmap
Define um bitmap. O bitmap é carregado a partir de um recurso ou de um arquivo.

## <a name="syntax"></a>Sintaxe

```
<Bitmap guid="guidImages" href="images\MyImage.bmp" usedList="bmp1, bmp2, bmp3" />
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|guid|Obrigatórios. GUID do identificador de comando GUID/ID.<br /><br /> O atributo GUID de um bitmap não está associado a nenhum VSPackage ou outro grupo de comandos.  Ele deve ser exclusivo para a definição de bitmap e não deve ser usado para nenhuma outra finalidade.|
|resID|ID do identificador de comando de GUID/ID. O atributo resID ou href é necessário.<br /><br /> O atributo resID é uma ID de recurso de número inteiro que determina a faixa de bitmap a ser carregada durante a mesclagem da tabela de comandos.  Quando a tabela de comandos estiver sendo carregada, os bitmaps especificados pela ID do recurso serão carregados a partir do recurso do mesmo módulo.|
|é usado|Obrigatório se o atributo resID estiver presente. Seleciona as imagens disponíveis na faixa de bitmap.|
|href|Caminho para o bitmap. O atributo resID ou href é necessário.<br /><br /> O caminho de inclusão é procurado para o arquivo de imagem indicado, que é inserido no binário resultante.  Durante a mesclagem de tabela de comando, a imagem é copiada e nenhuma pesquisa de recurso adicional ou carga é necessária.  Se o atributo usedlist não estiver presente, todas as imagens na faixa estarão disponíveis. **Observação:**  As imagens podem ser fornecidas em um dos vários formatos que incluem *.bmp*, *.png* e *.gif*.  As versões anteriores do compilador não davam suporte a imagens de bitmap de 32 bits que tinham informações alfa para transparência parcial. A solução alternativa para essas versões é usar o formato *.png* .|
|Condição|Opcional. Consulte [atributos condicionais](../extensibility/vsct-xml-schema-conditional-attributes.md).|

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[Elemento bitmaps](../extensibility/bitmaps-element.md)|Agrupa elementos de bitmap.|

## <a name="example"></a>Exemplo

```
<Bitmap guid="guidWidgetIcons" href="WidgetToolbarIcons_32.bmp" />
<Bitmap guid="guidWidgetIcons2" resID="IDBMP_WIDGETICONS"
  usedList="1, 2, 3, 4"/>
```

## <a name="see-also"></a>Confira também
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
