---
title: Elemento CustomDataSignature (modelos do Visual Studio) | Microsoft Docs
description: Saiba mais sobre o elemento CustomDataSignature e como ele especifica a assinatura de texto para localizar os dados personalizados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- <CustomDataSignature> Element (Visual Studio Templates)
- CustomDataSignature Element (Visual Studio Templates)
ms.assetid: 8c3db51d-7014-4484-802a-15aa1353dbdb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e5f42b3c5fe1dc5b9ab9697275876509eb0f8509
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99946053"
---
# <a name="customdatasignature-element-visual-studio-templates"></a>Elemento CustomDataSignature (modelos do Visual Studio)
Especifica a assinatura de texto para localizar os dados personalizados.

 \<VSTemplate> \<TemplateData>
 \<CustomDataSignature>

## <a name="syntax"></a>Sintaxe

```
<CustomDataSignature>"string"</CustomDataSignature>
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

 O texto é uma cadeia de caracteres que tem a assinatura de texto necessária para localizar os dados personalizados.

## <a name="remarks"></a>Comentários
 `CustomDataSignature` é um elemento opcional.

## <a name="see-also"></a>Confira também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e item](../ide/creating-project-and-item-templates.md)
