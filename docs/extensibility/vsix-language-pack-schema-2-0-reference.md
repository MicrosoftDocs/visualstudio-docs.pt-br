---
title: Referência de esquema 2.0 do VSIX Language Pack | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language pack
- localize vsix
- localize package
- localize extension
ms.assetid: 2a2932bc-cdbe-4d32-91fa-a3e0474f9098
ms.author: dagriffe
author: dgriffen
manager: douge
ms.workload:
- dagriffe
ms.openlocfilehash: 3c1dfa0e3de06bcd6c61472a085ea3c4cdeeac27
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51780783"
---
# <a name="vsix-language-pack-schema-20-reference"></a>Referência de esquema 2.0 do VSIX language pack

O esquema do pacote de idiomas do VSIX fornece informações de instalação localizado para pacotes VSIX. A versão 2.0 desse esquema dá suporte a elementos de localização adicional.

## <a name="language-pack-schema"></a>Esquema do pacote de idioma

É o elemento raiz do arquivo de pacote de idioma `<PackageLanguagePackManifest>`, com um atributo de `Version`, que é a versão do formato de pacote de idioma. Este artigo descreve a versão 2.0 do que o formato de pacote de idioma, que é especificado no manifesto, definindo o `Version` como o valor do atributo `Version="2.0.0"`. O elemento raiz contém exatamente um filho `<Metadata>` elemento.

### <a name="packagelanguagepackmanifest-element"></a>Elemento PackageLanguagePackManifest

Dentro de `<PackageLanguagePackManifest>` elemento o elemento a seguir deve existir:

|Título|Descrição|
|-----------|-----------------|
|`<Metadata>`| Elemento recipiente para todos os metadados de pacote localizado

### <a name="metadata-element"></a>Elemento de metadados

Dentro de `<Metadata>` elemento, você pode ter os seguintes elementos:

|Título|Descrição|
|-----------|-----------------|
|`<DisplayName>`|O nome localizado da extensão a ser instalado|
|`<Description>`|A descrição localizada da extensão a ser instalado|
|`<License>`| Um caminho para uma versão localizada da licença da extensão|
|`<MoreInfo>`| Um link para informações localizadas sobre a extensão|
|`<ReleaseNotes>`| Um caminho ou um link para uma versão localizada das notas de versão|
|`<Icon>`| Um caminho para uma versão localizada do ícone de extensões|

### <a name="sample-manifest"></a>Exemplo de manifesto

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageLanguagePackManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <DisplayName>Arbol de Familia</LocalizedName>
    <Description> Esta extensión pone control personalizado en la caja de herramientas por manejar información de familia.</Description>
    <MoreInfo> http://www.contoso.com/products/es/ArbolDeFamilia.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
</PackageLanguagePackManifest>
```

## <a name="see-also"></a>Consulte também

|Título|Descrição|
|-----------|-----------------|
|[Localizar pacotes VSIX](../extensibility/localizing-vsix-packages.md)|Mostra como fornecer suporte à instalação localizada para um pacote VSIX.|
|[Referência de esquema 2.0 de extensão do VSIX](../extensibility/vsix-extension-schema-2-0-reference.md)|Um manifesto do VSIX descreve o conteúdo de um *VSIX* arquivo de implantação. O arquivo de implantação permite que você instale uma extensão do Visual Studio usando o **extensões e atualizações** caixa de diálogo.|
|[Localizar e usar extensões do Visual Studio](../ide/finding-and-using-visual-studio-extensions.md)|Mostra como usar o **extensões e atualizações** caixa de diálogo para instalar, remover, ativar e desativar extensões.|