---
title: Persistindo dados no arquivo de projeto do MSBuild | Microsoft Docs
description: Saiba como persistir dados em um arquivo de projeto e usar IPersistXMLFragment para manter os dados no arquivo de projeto nos níveis de agregação de subtipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5e2cf082e4ca6a45bf42bd66ce34111d5c056787
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095011"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>Mantendo os dados no arquivo de projeto do MSBuild
Um subtipo de projeto pode precisar persistir dados específicos de subtipo no arquivo de projeto para uso posterior. Um subtipo de projeto usa a persistência de arquivo de projeto para atender aos seguintes requisitos:

1. Manter os dados usados como parte da criação do projeto. (Para obter mais informações sobre o Microsoft Build Engine, consulte [MSBuild](../../msbuild/msbuild.md).) As informações relacionadas à compilação também podem:

    1. Dados independentes de configuração. Ou seja, os dados armazenados em elementos do MSBuild com condições ausentes ou em branco.

    2. Dados dependentes de configuração. Ou seja, os dados armazenados em elementos do MSBuild que são condicionados para uma configuração de projeto específica. Por exemplo:

        ```
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        ```

2. Manter os dados que não são relevantes para a compilação. Esses dados podem ser expressos em XML de forma livre que não é validado em relação a um esquema XML.

    1. Dados independentes de configuração.

    2. Dados dependentes de configuração.

## <a name="persisting-build-related-information"></a>Mantendo informações de Build-Related
 A persistência de dados útil para criar um projeto é manipulada por meio do MSBuild. O sistema MSBuild mantém uma tabela mestra de informações relacionadas à compilação. Os subtipos de projeto são responsáveis por acessar esses dados para obter e definir valores de propriedade. Os subtipos de projeto também podem aumentar a tabela de dados relacionada à compilação Adicionando propriedades adicionais para serem persistidas e removendo as propriedades para que elas não sejam persistidas.

 Para modificar os dados do MSBuild, um subtipo de projeto é responsável por recuperar o objeto de Propriedade do MSBuild do sistema de projeto base por meio do <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> . <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> é uma interface implementada no sistema de projeto principal e as consultas de subtipo de projeto de agregação para ele executando `QueryInterface` .

 O procedimento a seguir descreve as etapas para remover uma propriedade usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> .

#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>Para remover uma propriedade de um arquivo de projeto do MSBuild

1. Chame `QueryInterface` <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> o subtipo do projeto.

2. Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> with `pszPropName` definido como a propriedade que você deseja remover.

### <a name="persisting-non-build-related-information"></a>Persistência de informações não relacionadas à compilação
 A persistência de dados em arquivos de projeto que não são importantes para compilação é tratada pelo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> .

 Você pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> no objeto principal `project subtype aggregator` , no `project subtype project configuration` objeto ou em ambos.

 Os seguintes pontos descrevem os principais conceitos relacionados à persistência de informações não relacionadas à compilação.

- O projeto base chama o subtipo de projeto principal (ou seja, o subtipo de projeto mais externo) objeto de agregador para carregar e salvar dados independentes de configuração e chama os objetos de configuração de projeto de subtipo de projeto para carregar ou salvar dados dependentes de configuração.

- O projeto base chama os métodos de <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> várias vezes para cada nível de agregação de subtipo de projeto e passa o GUID para cada nível.

- O projeto base passa ou recebe um fragmento XML dedicado a um subtipo de projeto específico e usa esse mecanismo como uma maneira de persistir o estado entre os níveis de agregação.

- O projeto base chama a implementação do subtipo de projeto mais externo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> passando em um GUID. Se o GUID pertencer ao subtipo de projeto mais externo, ele manipulará a chamada em si; caso contrário, ele delega a chamada para um subtipo de projeto interno, e assim por diante, até que o subtipo de projeto ao qual o GUID corresponde seja encontrado.

- Um subtipo de projeto também pode modificar o fragmento XML antes ou depois de delegar a chamada para um subtipo de projeto interno. O exemplo a seguir mostra um trecho de um arquivo de projeto, em que um nome de um arquivo que contém propriedades específicas para um subtipo de projeto é passado para esse subtipo de projeto.

    ```
    <ProjectExtensions>
        <VisualStudio>
          <FlavorProperties GUID="{<FlavorGUID>}">
            <FlavorProject TestFileFolder="TestFile" />
          </FlavorProperties>
        </VisualStudio>
      </ProjectExtensions>
    ```

## <a name="see-also"></a>Confira também
- [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)
