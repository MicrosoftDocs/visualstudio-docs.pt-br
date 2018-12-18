---
title: Manter os dados no arquivo de projeto MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 324f9dfd4e381e9580e4940f06f652ef64d9d3ec
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132072"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>Manter os dados no arquivo de projeto do MSBuild
Talvez seja necessário um subtipo de projeto manter dados específicos de subtipo para o arquivo de projeto para uso posterior. Um subtipo de projeto usa a persistência de arquivo de projeto para atender aos seguintes requisitos:  
  
1.  Manter dados usados como parte da construção do projeto. (Para obter mais informações sobre o Microsoft Build Engine, consulte [MSBuild](../../msbuild/msbuild.md).) Informações relacionadas à compilação podem:  
  
    1.  Dados de configuração independente. Ou seja, os dados armazenados em elementos de MSBuild com condições de espaço em branco ou ausentes.  
  
    2.  Dados de configuração dependente. Ou seja, os dados armazenados em elementos de MSBuild são condicionados para uma configuração de projeto específico. Por exemplo:  
  
        ```  
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        ```  
  
2.  Manter os dados que não são relevantes para a compilação. Esses dados podem ser expressos em XML de forma livre que não é validado em relação a um esquema XML.  
  
    1.  Dados de configuração independente.  
  
    2.  Dados de configuração dependente.  
  
## <a name="persisting-build-related-information"></a>Manter informações de compilação  
 Persistência de dados úteis para a criação de um projeto é tratada pelo MSBuild. O sistema de MSBuild mantém uma tabela mestre de informações relacionadas à compilação. Subtipos de projeto são responsáveis por acessar esses dados para obter e definir valores de propriedade. Subtipos de projeto também podem ampliar a tabela de dados relacionados a compilação Adicionando propriedades adicionais para ser persistente e remover propriedades de forma que eles não são persistentes.  
  
 Para modificar os dados do MSBuild, um subtipo de projeto é responsável por recuperar o objeto de propriedade de MSBuild do sistema de projeto base por <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>. <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> é uma interface implementada no sistema de projeto principal e as agregação consultas de subtipo de projeto para ela executando `QueryInterface`.  
  
 O procedimento a seguir descreve as etapas para remover uma propriedade usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>.  
  
#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>Para remover uma propriedade de um arquivo de projeto do MSBuild  
  
1.  Chamar `QueryInterface` em <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> do subtipo do projeto.  
  
2.  Chamar <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> com `pszPropName` definido como a propriedade que deseja remover.  
  
### <a name="persisting-non-build-related-information"></a>Informações relacionadas a compilação não persistente  
 Persistência de dados em arquivos de projeto que não são importantes para a compilação é tratada pelo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>.  
  
 Você pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> no principal `project subtype aggregator` objeto, o `project subtype project configuration` ou ambos.  
  
 Os pontos a seguir descrevem os principais conceitos sobre a persistência de informações de compilação não relacionadas.  
  
-   Chama o projeto com base no objeto de agregador de projeto principal subtipo (ou seja, o subtipo de projeto externo) para carregar e salvar dados de configuração independente e ela chama os objetos de configuração de projeto do projeto subtipo para carregar ou salvar configuração dependente dados.  
  
-   O projeto base chama os métodos de <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> várias vezes para cada nível de agregação de subtipo de projeto e passa o GUID para cada nível.  
  
-   O projeto base passa ou recebe um fragmento XML que é dedicado a um subtipo de projeto específico e usa esse mecanismo como uma maneira de persistir o estado entre os níveis de agregação.  
  
-   O projeto base chama o subtipo de projeto externo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>implementação passando um GUID. Se o GUID pertence o subtipo de projeto mais externo, ele trata a chamada em si; Caso contrário, ela delega a chamada para um subtipo de projeto interna e assim por diante, até encontra o subtipo de projeto que o GUID correspondente ao.  
  
-   Um subtipo de projeto também pode modificar o fragmento XML antes ou depois de ela delega a chamada para um subtipo de projeto interna. O exemplo a seguir mostra um trecho de um arquivo de projeto, onde um nome de um arquivo que contém propriedades específicas de um subtipo de projeto, é passado para esse subtipo de projeto.  
  
    ```  
    <ProjectExtensions>  
        <VisualStudio>  
          <FlavorProperties GUID="{<FlavorGUID>}">  
            <FlavorProject TestFileFolder="TestFile" />  
          </FlavorProperties>  
        </VisualStudio>  
      </ProjectExtensions>  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Subtipos de projeto](../../extensibility/internals/project-subtypes.md)