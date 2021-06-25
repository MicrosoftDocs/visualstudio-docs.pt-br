---
title: A estrutura do arquivo [Content_types].xml arquivo | Microsoft Docs
description: Saiba mais sobre a estrutura do arquivo de tipos de conteúdo, que contém informações sobre os tipos de conteúdo em um pacote VSIX.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- content_types
- content types
- opc
- vsix
ms.assetid: 9c399598-b9fa-4da7-84b5-defbf82e9335
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 96d4d0eeea34300894674a2105d080e8a6abb607
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112900415"
---
# <a name="the-structure-of-the-content_typesxml-file"></a>A estrutura do arquivo [Content_types].xml
Contém informações sobre os tipos de conteúdo em um pacote VSIX. Visual Studio usa o arquivo [Content_Types].xml para instalar o pacote, mas ele não instala o arquivo em si.

> [!NOTE]
> Embora este tópico se aplique somente a arquivos [Content_Type].xml usados em pacotes VSIX, o tipo de arquivo [Content_Types].xml faz parte do padrão *OPC (Open Packaging Conventions).* Para obter mais informações, consulte [OPC: um novo padrão para empacotamento](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data) de dados no site do MSDN.

## <a name="attributes-and-elements"></a>Atributos e elementos
 As seções a seguir descrevem o elemento raiz e seus atributos e elementos filho.

### <a name="root-element"></a>Elemento Root

|Elemento|Descrição|
|-------------|-----------------|
|`Types`|Contém elementos filho que enumeram os tipos de arquivo no pacote VSIX.|

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`Xmlns`|(Obrigatório.) O local do esquema usado para esse arquivo [Content_Types].xml.|

### <a name="attribute-name-attribute"></a>{Nome do atributo} Atributo

| Valor | Descrição |
| - | - |
| `http://schemas.openformats.org/package/2006/content-types` | O local do esquema de tipos de conteúdo. |

### <a name="child-elements"></a>Elementos filho
 O elemento `Types` pode conter qualquer número de elementos `Default`.

|Elemento|Descrição|
|-------------|-----------------|
|`Default`|Descreve um tipo de conteúdo no pacote VSIX. Cada tipo de arquivo no pacote deve ter seu `Default` próprio elemento.|

### <a name="attributes"></a>Atributos

|Atributo|Descrição|
|---------------|-----------------|
|`Extension`|A extensão de nome de arquivo de um arquivo no pacote VSIX.|
|`ContentType`|Descreve o tipo de conteúdo associado à extensão de nome de arquivo.|

### <a name="attribute-name-attribute"></a>{Nome do atributo} Atributo
 Visual Studio reconhece os valores `ContentType` a seguir para os tipos `Extension` associados.

|Extensão|ContentType|
|---------------|-----------------|
|txt|texto/sem formatação|
|Pkgdef|texto/sem formatação|
|Xml|text/xml|
|Vsixmanifest|text/xml|
|htm ou html|texto/html|
|Rtf|application/rtf|
|pdf|application/pdf|
|GIF|image/gif|
|jpg ou jpeg|image/jpg|
|tiff|imagem/tiff|
|vsix|application/zip|
|zip|application/zip|
|dll|application/octet-stream|
|todos os outros tipos de arquivo|application/octet-stream|

## <a name="example"></a>Exemplo

### <a name="description"></a>Descrição
 O seguinte arquivo [Content_Types].xml descreve um pacote VSIX típico.

### <a name="code"></a>Código

```
<?xml version="1.0" encoding="utf-8" ?>
<Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
    <Default Extension="vsixmanifest" ContentType="text/xml" />
    <Default Extension="dll" ContentType="application/octet-stream" />
    <Default Extension="png" ContentType="application/octet-stream" />
    <Default Extension="txt" ContentType="text/plain" />
    <Default Extension="pkgdef" ContentType="text/plain" />
</Types>
```

## <a name="see-also"></a>Confira também
- [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md)
- [Referência do esquema de extensão vsix 1.0](/previous-versions/dd393700(v=vs.110))
- [OPC: um novo padrão para empacotamento de dados](/archive/msdn-magazine/2007/august/opc-a-new-standard-for-packaging-your-data)