---
title: Referência do esquema 2,0 do pacote de idiomas do VSIX | Microsoft Docs
description: O esquema do pacote de idiomas do VSIX fornece informações de instalação localizadas para pacotes VSIX. A versão 2,0 dá suporte a elementos de localização adicionais.
ms.custom: SEO-VS-2020
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.openlocfilehash: 0e7107cb90a79e8cd1a052cd73706d95a782781d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062272"
---
# <a name="vsix-language-pack-schema-20-reference"></a>Referência do esquema 2,0 do pacote de idiomas do VSIX

O esquema do pacote de idiomas do VSIX fornece informações de instalação localizadas para pacotes VSIX. A versão 2,0 deste esquema oferece suporte a elementos de localização adicionais.

## <a name="language-pack-schema"></a>Esquema do pacote de idiomas

O elemento raiz do arquivo de pacote de idiomas é `<PackageLanguagePackManifest>` , com um atributo de `Version` , que é a versão do formato do pacote de idiomas. Este artigo descreve a versão 2,0 do formato do pacote de idiomas, que é especificado no manifesto, definindo o `Version` atributo para o valor `Version="2.0.0"` . O elemento raiz contém exatamente um `<Metadata>` elemento filho.

### <a name="packagelanguagepackmanifest-element"></a>Elemento PackageLanguagePackManifest

Dentro do `<PackageLanguagePackManifest>` elemento, o seguinte elemento deve existir:

|Título|Descrição|
|-----------|-----------------|
|`<Metadata>`| O elemento contentor para todos os metadados de pacote localizados

### <a name="metadata-element"></a>Elemento Metadata

Dentro do `<Metadata>` elemento, você pode ter os seguintes elementos:

|Título|Descrição|
|-----------|-----------------|
|`<DisplayName>`|O nome localizado da extensão a ser instalada|
|`<Description>`|A descrição localizada da extensão a ser instalada|
|`<License>`| Um caminho para uma versão localizada da licença da extensão|
|`<MoreInfo>`| Um link para informações localizadas sobre a extensão|
|`<ReleaseNotes>`| Um caminho ou link para uma versão localizada das notas de versão|
|`<Icon>`| Um caminho para uma versão localizada do ícone de extensões|

### <a name="sample-manifest"></a>Exemplo de manifesto

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</DisplayName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>Confira também

|Título|Descrição|
|-----------|-----------------|
|[Localizando pacotes VSIX](../extensibility/localizing-vsix-packages.md)|Mostra como fornecer suporte à instalação localizada para um pacote VSIX.|
|[Referência do esquema de extensão do VSIX 2,0](../extensibility/vsix-extension-schema-2-0-reference.md)|Um manifesto do VSIX descreve o conteúdo de um arquivo de implantação *. vsix* . O arquivo de implantação permite que você instale uma extensão do Visual Studio usando a caixa de diálogo **extensões e atualizações** .|
|[Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)|Mostra como usar a caixa de diálogo **extensões e atualizações** para instalar, remover, ativar e desativar extensões.|
