---
title: Localizando pacotes VSIX | Microsoft Docs
description: Saiba como localizar um pacote VSIX criando um arquivo extension. vsixlangpack para cada idioma de destino e, em seguida, colocando-os na pasta correta.
ms.custom: SEO-VS-2020
ms.date: 10/26/2017
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7d2e297484e89f1ae2cfb9f2be7af25f1fe92714
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105073216"
---
# <a name="localizing-vsix-packages"></a>Localizando pacotes do VSIX

Você pode localizar um pacote VSIX criando um arquivo *extension. vsixlangpack* para cada idioma de destino e, em seguida, colocando-os na pasta correta. Quando um pacote localizado é instalado, o nome localizado da extensão é exibido junto com uma descrição localizada. Se você fornecer um arquivo de licença localizado ou uma URL que aponte para informações localizadas, eles também serão exibidos.

Se o conteúdo do seu pacote VSIX incluir um VSPackage que adiciona comandos de menu ou outra interface do usuário, consulte [Localizar comandos de menu](../extensibility/localizing-menu-commands.md) para obter informações sobre como localizar os novos elementos da interface do usuário.

## <a name="directory-structure"></a>Estrutura do diretório

 Quando um usuário instala uma extensão, **extensões e atualizações** verifica o nível superior do pacote do VSIX para uma pasta cujo nome corresponde à localidade do Visual Studio do computador de destino. Se **as extensões e atualizações** localizarem um arquivo *. vsixlangpack* na pasta, ele substituirá os valores localizados nesse arquivo pelos valores correspondentes no arquivo *. vsixmanifest* . Esses valores são exibidos quando a extensão está sendo instalada. O exemplo a seguir mostra a estrutura de diretório para um pacote VSIX localizado em espanhol (es-ES) e francês (fr-FR).

```text
.
├── MyExtension.dll
├── Extension.vsixmanifest
├── [Content_Types].xml
├── es-ES
│   └── Extension.vsixlangpack
└── fr-FR
    └── Extension.vsixlangpack
```

> [!NOTE]
> Os modelos de projeto com suporte ao VSIX em [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] gerar um manifesto do VSIX e nomeá-lo como *origem. extensão. vsixmanifest*. Quando o Visual Studio cria o projeto, ele copia o conteúdo desse arquivo em Extension. VsixManifest no pacote VSIX.

## <a name="the-extensionvsixlangpack-file"></a>O arquivo extension. vsixlangpack

O arquivo *extension. vsixlangpack* segue o [esquema de pacote de idiomas do VSIX 2,0](../extensibility/vsix-language-pack-schema-2-0-reference.md). Esse esquema tem um `PackageLanguagePackManifest` , que é seguido imediatamente por um `Metadata` elemento filho. O elemento Metadata pode conter até 6 elementos filho,,,,, `DisplayName` `Description` `MoreInfo` `License` `ReleaseNotes` e `Icon` . Esses elementos filho correspondem aos elementos filho,,, e, `DisplayName` `Description` `MoreInfo` `License` `ReleaseNotes` `Icon` do `Metadata` elemento do arquivo *extension. vsixmanifest* .

Ao criar um arquivo vsixlangpack, você deve definir a `Include in Vsix` propriedade como `true` . Caso contrário, o texto de instalação localizado será ignorado.

### <a name="to-set-the-include-in-vsix-property"></a>Para definir a propriedade include in VSIX

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo extension. vsixlangpack e clique em **Propriedades**.

2. Na **grade de propriedades**, clique em **incluir no VSIX** e defina seu valor como `true` .

## <a name="example"></a>Exemplo

### <a name="description"></a>Descrição

O exemplo a seguir mostra partes relevantes de um arquivo *extension. vsixmanifest* . O arquivo também inclui o arquivo *extension. vsixlangpack* correspondente para espanhol. Os valores do pacote de idiomas substituem os valores do manifesto se a localidade do Visual Studio do computador de destino estiver definida como espanhol.

### <a name="code"></a>Código

- [*Extensão. vsixmanifest*]

```xml
<?xml version="1.0" encoding="utf-8"?>
<PackageManifest ...>
  <Metadata ...>
    <DisplayName>Family Tree</DisplayName>
    <Description>This extension places a custom treeview control in the toolbox that is optimized for handling family tree information.</Description>
    <MoreInfo>http://www.contoso.com/products/FamilyTree.htm</MoreInfo>
    <License>Eula.rtf</License>
    <ReleaseNotes>ReleaseNotes.rtf</ReleaseNotes>
    <Icon>Icon.png</Icon>
  </Metadata>
  <Installation .../>
  <Dependencies .../>
  <Prerequisites .../>
  <Assets .../>
</PackageManifest>
```

- [*Extensão. vsixlangpack*]

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
|[Referência do esquema 2,0 do pacote de idiomas do VSIX](vsix-language-pack-schema-2-0-reference.md)|Um pacote de idiomas do VSIX descreve as informações de localização de um arquivo de implantação. vsix.|
|[Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)|Descreve a estrutura e o conteúdo de um pacote VSIX.|
|[Comandos do menu localizar](../extensibility/localizing-menu-commands.md)|Mostra como localizar outros recursos de texto em uma extensão.|
