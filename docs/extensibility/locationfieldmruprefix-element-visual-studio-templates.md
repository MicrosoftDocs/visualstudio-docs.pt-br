---
title: Elemento LocationFieldMRUPrefix (modelos do Visual Studio) | Microsoft Docs
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#LocationFieldMRUPrefix
helpviewer_keywords:
- <LocationFieldMRUPrefix> element [Visual Studio Templates]
- LocationFieldMRUPrefix element [Visual Studio Templates]
ms.assetid: 03443691-9eb5-46f4-9169-cc2552a04bcb
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c8c4c3fa4e64b302c6d1c9d0e393528d46fe072f
ms.sourcegitcommit: b0d8e61745f67bd1f7ecf7fe080a0fe73ac6a181
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/22/2019
ms.locfileid: "56680394"
---
# <a name="locationfieldmruprefix-element-visual-studio-templates"></a>Elemento LocationFieldMRUPrefix (modelos do Visual Studio)
Especifica os caminhos usados mais recentemente (MRU) a **novo projeto** e **Adicionar Novo Item** caixa de diálogo.

## <a name="syntax"></a>Sintaxe

```xml
<LocationFieldMRUPrefix> ... </LocationFieldMRUPrefix>
```

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem atributos, elementos filho e elementos pai.

### <a name="attributes"></a>Atributos
 nenhuma.

### <a name="child-elements"></a>Elementos filho
 nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplateData](../extensibility/templatedata-element-visual-studio-templates.md)|Categoriza o modelo e define como ele é exibido em qualquer um de **novo projeto** ou o **Adicionar Novo Item** caixa de diálogo.|

## <a name="remarks"></a>Comentários
 Esse elemento só deve ser usado para modelos produzidos por meio de [!INCLUDE[vsipprvsip](../extensibility/includes/vsipprvsip_md.md)].

## <a name="see-also"></a>Consulte também
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)