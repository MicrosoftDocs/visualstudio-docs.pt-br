---
title: Elemento PreviewImage (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento PreviewImage e como ele especifica o nome do arquivo para a imagem de visualização que será exibida na caixa de diálogo novo projeto ou adicionar novo item.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <PreviewImage> Element (Visual Studio Templates)
- PreviewImage Element (Visual Studio Templates)
ms.assetid: d1796f20-523b-4e0d-8ac3-ca87f3b5a9b6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fc7a370885d24a586262bebd4182daacd84a9b2
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090219"
---
# <a name="previewimage-element-visual-studio-templates"></a>Elemento PreviewImage (modelos do Visual Studio)
Especifica a imagem de visualização, como um nome de arquivo, para a imagem de visualização que aparecerá na caixa de diálogo **novo projeto** ou **Adicionar novo item** .

 \<VSTemplate> \<TemplateData>
 \<PreviewImage>

## <a name="syntax"></a>Sintaxe

```
<PreviewImage>"filename"</PreviewImage>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 Nenhum.

### <a name="child-elements"></a>Elementos filho
 Nenhum.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Elemento necessário.<br /><br /> Categoriza o modelo e define como ele é exibido no **novo projeto** ou na caixa de diálogo **Adicionar novo item** .|

## <a name="text-value"></a>Valor de texto
 Um valor de texto é obrigatório.

 O texto deve ser uma cadeia de caracteres que represente um nome de arquivo.

## <a name="remarks"></a>Comentários
 `PreviewImage` é um elemento opcional.

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
