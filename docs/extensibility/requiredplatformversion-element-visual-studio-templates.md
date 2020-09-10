---
title: Elemento RequiredPlatformVersion (Modelos do Visual Studio)
titleSuffix: ''
ms.date: 11/04/2016
ms.technology: vs-ide-general
ms.topic: reference
ms.assetid: 6f0e4986-3157-4bba-aed3-c28413ebe976
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6a3873a8107c60802edd07b567d65205a37dc213
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2020
ms.locfileid: "89741677"
---
# <a name="requiredplatformversion-element-visual-studio-templates"></a>Elemento RequiredPlatformVersion (modelos do Visual Studio)

Especifica a versão mínima do sistema operacional que o modelo de projeto requer para funcionar corretamente. Esse elemento é usado para modelos de projeto que criam [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativos.

 O `RequiredPlatformVersion` valor é comparado diretamente com a versão do sistema operacional. Se o `RequiredPlatformVersion` for maior que a versão do sistema operacional, o modelo não aparecerá na caixa de diálogo **novo projeto** . Para especificar um modelo para o [!INCLUDE[win8](../debugger/includes/win8_md.md)] ou superior, defina `RequiredPlatformVersion` como 6.2.0. Para especificar um modelo para o [!INCLUDE[win81](../debugger/includes/win81_md.md)] ou superior, defina `RequiredPlatformVersion` como 6.3.0.

 Modelos que especificam `RequiredPlatformVersion` = 8 são compatíveis com modelos de cliente anteriores [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] .

 TemplateData VSTemplate.... TargetPlatformName RequiredPlatformVersion

## <a name="syntax"></a>Sintaxe

```xml
<RequiredPlatformVersion> OperatingSystem </RequiredPlatformVersion>
```

## <a name="attributes-and-elements"></a>Atributos e elementos

 nenhuma.

### <a name="attributes"></a>Atributos

 nenhuma.

### <a name="child-elements"></a>Elementos filho

 nenhuma.

### <a name="parent-elements"></a>Elementos pai

|Elemento|Descrição|
|-------------|-----------------|
|[TemplatePlatformName](../extensibility/templatedata-element-visual-studio-templates.md)|Especifica a plataforma de destino do modelo de projeto.|

## <a name="text-value"></a>Valor de texto

 Um valor de texto é obrigatório.

## <a name="remarks"></a>Comentários

 Esse texto especifica a versão mínima do sistema operacional exigida pelo modelo.

## <a name="example"></a>Exemplo

 Este exemplo especifica que o modelo de projeto tem como destino [!INCLUDE[win8](../debugger/includes/win8_md.md)] ou posterior.

```xml
<VSTemplate Type="Project" Version="3.0.0"    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">
    <TemplateData>
        <TargetPlatformName>Windows</TargetPlatformName>
            <RequiredPlatformVersion>6.3.0</RequiredPlatformVersion>

    </TemplateData>
    <TemplateContent>

    </TemplateContent>
</VSTemplate>
```

## <a name="see-also"></a>Veja também

- [Elemento TargetPlatformName (modelos do Visual Studio)](../extensibility/targetplatformname-element-visual-studio-templates.md)
- [Criar modelos de projeto e de item](../ide/creating-project-and-item-templates.md)
- [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
