---
title: Anatomia de um pacote VSIX | Microsoft Docs
description: Saiba mais sobre o conteúdo de um pacote VSIX no Visual Studio, um arquivo que contém uma ou mais extensões do Visual Studio e um arquivo de manifesto de metadados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- visual studio extension
- vsix
- packages
ms.assetid: 8b86d62f-c274-4e91-82e0-38cdb9a423d5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 67b3775509e330ad55a2531a9e42a7cca93c50a6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097494"
---
# <a name="anatomy-of-a-vsix-package"></a>Anatomia de um pacote VSIX
Um pacote VSIX é um arquivo *. vsix* que contém uma ou mais extensões do Visual Studio, junto com os metadados que o Visual Studio usa para classificar e instalar as extensões. Esses metadados estão contidos no manifesto do VSIX e no arquivo *[Content_Types]. xml* . Um pacote VSIX também pode conter um ou mais arquivos *extension. vsixlangpack* para fornecer texto de instalação localizado e pode conter pacotes VSIX adicionais para instalar dependências.

 O formato do pacote VSIX segue o padrão OPC (Open Packaging Conventions). O pacote contém binários e arquivos de suporte, juntamente com um arquivo *[Content_Types]. xml* e um arquivo de manifesto *. vsix* . Um pacote VSIX pode conter a saída de vários projetos ou até mesmo vários pacotes que têm seus próprios manifestos.

> [!NOTE]
> Os nomes dos arquivos incluídos nos pacotes VSIX não devem incluir espaços, nem caracteres reservados em identificadores de recursos uniformes (URI), conforme definido em [ \[ rfc2396 \] ](https://www.rfc-editor.org/rfc/rfc2396.txt).

## <a name="the-vsix-manifest"></a>O manifesto do VSIX
 O manifesto do VSIX contém informações sobre a extensão a ser instalada e segue o esquema VSX. Para obter mais informações, consulte [referência do esquema de extensão do VSIX 1,0](/previous-versions/dd393700(v=vs.110)). Para obter um exemplo de manifesto do VSIX, consulte [elemento PackageManifest (elemento raiz, esquema VSX)](/previous-versions/dd393754(v=vs.110)).

 O manifesto do VSIX deve ser nomeado `extension.vsixmanifest` quando é incluído em um arquivo ^. vsix *.

## <a name="the-content"></a>O conteúdo
 Um pacote VSIX pode conter modelos, itens de caixa de ferramentas, VSPackages ou qualquer outro tipo de extensão com suporte no Visual Studio.

## <a name="language-packs"></a>Pacotes de idiomas
 Um pacote VSIX pode conter uma ou mais arquivos *extension. vsixlangpack* para fornecer texto localizado durante a instalação. Para obter mais informações, consulte [localizando pacotes VSIX](../extensibility/localizing-vsix-packages.md).

## <a name="dependencies-and-references"></a>Dependências e referências
 Um pacote VSIX pode conter outros pacotes VSIX como referências. Cada um desses outros pacotes deve incluir seu próprio manifesto do VSIX.

 Se um usuário tentar instalar uma extensão que tenha dependências, o instalador verificará se os assemblies necessários estão instalados no sistema do usuário. Se os assemblies necessários não forem encontrados, **as extensões e as atualizações** exibirão uma lista dos assemblies ausentes.

 Se o manifesto de extensão incluir um ou mais elementos de [referência](/previous-versions/visualstudio/visual-studio-2010/dd393687(v=vs.100)) , **as extensões e as atualizações** compararão o manifesto de cada referência às extensões instaladas no sistema e instalará a extensão referenciada se ela ainda não estiver instalada. Se uma versão anterior de uma extensão referenciada for instalada, a versão mais recente a substituirá.

 Se um projeto em uma solução de vários projetos incluir uma referência a outro projeto na mesma solução, o pacote VSIX incluirá as dependências desse projeto. Você pode substituir esse comportamento selecionando a referência para o projeto interno e, em seguida, na janela **Propriedades** , definindo os **grupos de saída incluídos na propriedade VSIX** como `BuiltProjectOutputGroup` .

 Para incluir DLLs satélite de assemblies referenciados no pacote VSIX, adicione `SatelliteDllsProjectOutputGroup` aos **grupos de saída incluídos na propriedade VSIX** .

## <a name="installation-location"></a>Local de instalação
 Durante a instalação, **as extensões e as atualizações** do buscam o conteúdo do pacote VSIX em uma pasta em *%LocalAppData%\Microsoft\VisualStudio\14.0\Extensions*.

 Por padrão, a instalação se aplica somente ao usuário atual, pois *% LocalAppData%* é um diretório específico do usuário. No entanto, se você definir o elemento [AllUsers](/previous-versions/ee191547(v=vs.110)) do manifesto como `True` , a extensão será instalada em <em>.. \\ </em> VisualStudioInstallationFolder<em>\Common7\IDE\Extensions</em> e estará disponível para todos os usuários do computador.

## <a name="content_typesxml"></a>[Content_Types]. xml
 O arquivo *[Content_Types]. xml* identifica os tipos de arquivo no arquivo *. vsix* expandido. O Visual Studio usa esse arquivo durante a instalação do pacote, mas não instala o próprio arquivo. Para obter mais informações sobre esse arquivo, consulte [a estrutura do arquivo [Content_types]. xml](the-structure-of-the-content-types-dot-xml-file.md).

 Um arquivo *[Content_Types]. xml* é exigido pelo padrão OPC (Open Packaging Conventions). Para obter mais informações sobre o OPC, consulte [OPC: um novo padrão para empacotar seus dados](/archive/blogs/msdnmagazine/opc-a-new-standard-for-packaging-your-data) no site do MSDN.