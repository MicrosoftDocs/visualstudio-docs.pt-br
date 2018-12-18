---
title: Localizar pacotes VSIX | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2017
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- localize package
- localize extension
- localized deployment
ms.assetid: 10e80b13-b39e-466c-a7c8-774a862355af
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 54de0b219eb1c86a413b7a95e87a48e7f65ac9ec
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39636968"
---
# <a name="localizing-vsix-packages"></a>Localizando pacotes do VSIX

Você pode localizar um pacote VSIX criando um *Extension.vsixlangpack* de arquivo para cada idioma de destino e, em seguida, colocando-os na pasta correta. Quando um pacote localizado estiver instalado, o nome localizado da extensão é exibido junto com uma descrição localizada. Se você fornecer um arquivo de licença localizada ou uma URL que aponta para informações localizadas, eles também são exibidos.

Se o conteúdo do seu pacote do VSIX inclui um VSPackage que adiciona os comandos de menu ou outra interface de usuário, consulte [localizar comandos de menu](../extensibility/localizing-menu-commands.md) para obter informações sobre como localizar os novos elementos de interface do usuário.

## <a name="directory-structure"></a>Estrutura do diretório

 Quando um usuário instala uma extensão **extensões e atualizações** verifica o nível superior do pacote VSIX para uma pasta cujo nome corresponde à localidade do Visual Studio do computador de destino. Se **extensões e atualizações** localiza um *.vsixlangpack* arquivo na pasta, ele substitui os valores localizados no arquivo para os valores correspondentes no *.vsixmanifest*arquivo. Esses valores são exibidos quando a extensão está sendo instalada. O exemplo a seguir mostra a estrutura de diretório para um pacote VSIX que está localizado em espanhol (es-ES) e francês (fr-FR).  

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
> Os modelos de projeto VSIX com suporte nas [!INCLUDE[vsipsdk](../extensibility/includes/vsipsdk_md.md)] gerar um manifesto do VSIX e nomeie-o *vsixmanifest*. Quando o Visual Studio compila o projeto, ele copia o conteúdo desse arquivo para vsixmanifest no pacote VSIX.

## <a name="the-extensionvsixlangpack-file"></a>O arquivo Extension.vsixlangpack

O *Extension.vsixlangpack* arquivo segue a [esquema do pacote de idiomas do VSIX 2.0](../extensibility/vsix-language-pack-schema-2-0-reference.md). Esse esquema possui um `PackageLanguagePackManifest`, que é seguido imediatamente por um `Metadata` elemento filho. O elemento de metadados pode conter até 6 elementos filho `DisplayName`, `Description`, `MoreInfo`, `License`, `ReleaseNotes`, e `Icon`. Esses elementos filho correspondem para o `DisplayName`, `Description`, `MoreInfo`, `License`, `ReleaseNotes`, e `Icon` elementos filho do `Metadata` elemento do *vsixmanifest*arquivo.

Quando você cria um arquivo vsixlangpack, você deve definir a `Include in Vsix` propriedade para `true`. Caso contrário, o texto de instalação localizado será ignorado.

### <a name="to-set-the-include-in-vsix-property"></a>Para definir a incluir no Vsix propriedade

1. Na **Gerenciador de soluções**, clique no arquivo Extension.vsixlangpack e, em seguida, clique em **propriedades**.

2.  No **grade de propriedade**, clique em **incluir em Vsix**e defina seu valor como `true`.

## <a name="example"></a>Exemplo

### <a name="description"></a>Descrição

O exemplo a seguir mostra as partes relevantes de um *vsixmanifest* arquivo. O arquivo também inclui correspondente *Extension.vsixlangpack* arquivo para espanhol. Os valores do pacote de idiomas substituem os valores do manifesto, se a localidade do Visual Studio do computador de destino é definida como Spanish.

### <a name="code"></a>Código

 [*Vsixmanifest*]

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

 [*Extension.vsixlangpack*]

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

## <a name="see-also"></a>Consulte também

|Título|Descrição|
|-----------|-----------------|
|[Referência de esquema 2.0 do pacote de idiomas do VSIX](../extensibility/vsixlanguagepack-element-vsix-language-pack-schema.md)|Um pacote de idiomas do VSIX descreve as informações de localização de um arquivo de implantação. VSIX.|
|[Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)|Descreve a estrutura e o conteúdo de um pacote vsix.|
|[Localizar os comandos de menu](../extensibility/localizing-menu-commands.md)|Mostra como localizar outros recursos de texto em uma extensão.|