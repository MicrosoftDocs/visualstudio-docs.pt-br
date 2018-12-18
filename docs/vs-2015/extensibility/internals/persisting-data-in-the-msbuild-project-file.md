---
title: Manter dados no arquivo de projeto do MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- project files, persisting data in
ms.assetid: 6a920cb7-453d-4ffd-af1c-6f3084bd03f7
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 059ddc7b9b8fe0de06530af704bb5f7e271f6744
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749647"
---
# <a name="persisting-data-in-the-msbuild-project-file"></a>Mantendo os dados no arquivo de projeto do MSBuild
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Talvez seja necessário um subtipo de projeto manter dados específicos subtipo-no arquivo de projeto para uso posterior. Um subtipo de projeto usa a persistência de arquivo de projeto para atender aos seguintes requisitos:  
  
1.  Manter os dados usados como parte da criação do projeto. (Para obter mais informações sobre o Microsoft Build Engine, consulte [MSBuild](http://msdn.microsoft.com/en-us/7c49aba1-ee6c-47d8-9de1-6f29a906e20b).) Informações relacionadas ao build podem:  
  
    1.  Dados de configuração independente. Ou seja, os dados armazenados em elementos do MSBuild com condições em branco ou ausentes.  
  
    2.  Dados de configuração dependente. Ou seja, os dados armazenados em elementos do MSBuild são condicionados para uma configuração de projeto específico. Por exemplo:  
  
        ```  
        <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">  
        ```  
  
2.  Manter os dados que não não relevantes para compilar. Esses dados podem ser expressos em XML de forma livre que não é validado contra um esquema XML.  
  
    1.  Dados de configuração independente.  
  
    2.  Dados de configuração dependente.  
  
## <a name="persisting-build-related-information"></a>Manter informações de compilação  
 Persistência de dados úteis para a criação de um projeto é tratada pelo MSBuild. O sistema MSBuild mantém uma tabela mestre de informações relacionadas à compilação. Subtipos de projeto são responsáveis por acessar esses dados para obter e definir valores de propriedade. Subtipos de projeto também podem ampliar a tabela de dados relacionados à compilação Adicionando propriedades extras que devem ser persistidos e removendo propriedades para que eles não são mantidos.  
  
 Para modificar os dados do MSBuild, um subtipo de projeto é responsável por recuperar o objeto de propriedade do MSBuild do sistema de projeto base por meio de <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>. <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> é uma interface implementada no sistema de projeto de núcleo e as consultas de subtipo de projeto agregação para ela executando `QueryInterface`.  
  
 O procedimento a seguir descreve as etapas para remover uma propriedade usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>.  
  
#### <a name="to-remove-a-property-from-an-msbuild-project-file"></a>Para remover uma propriedade de um arquivo de projeto do MSBuild  
  
1.  Chame `QueryInterface` em <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage> do subtipo de projeto.  
  
2.  Chame <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage.RemoveProperty%2A> com `pszPropName` definido para a propriedade que você deseja remover.  
  
### <a name="persisting-non-build-related-information"></a>Informações relacionadas ao Build não persistente  
 Persistência de dados em arquivos de projeto que não importa a compilação é tratada por meio <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>.  
  
 Você pode implementar <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> principal `project subtype aggregator` objeto, o `project subtype project configuration` objeto, ou ambos.  
  
 Os pontos a seguir descrevem os principais conceitos sobre a persistência de não-compilação de informações relacionada.  
  
-   Projeto base chama no principal projeto subtipo (ou seja, o subtipo de projeto mais externo) agregador objeto para carregar e salvar dados de configuração independente e, em seguida, chama sobre os objetos de configuração de projeto de subtipo do projeto para carregar ou salvar a configuração dependente dados.  
  
-   O projeto base chama os métodos de <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> várias vezes para cada nível de agregação de subtipo de projeto e passa o GUID para cada nível.  
  
-   O projeto base passa ou recebe um fragmento XML que é dedicado a um subtipo de projeto específico e usa esse mecanismo, como uma forma de persistir o estado entre os níveis de agregação.  
  
-   O projeto base chama o subtipo de projeto mais externo <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>implementação passando um GUID. Se o GUID pertence o subtipo de projeto mais externo, ele lida com a chamada em si; Caso contrário, ela delega a chamada para um subtipo de projeto interno e assim por diante, até encontra o subtipo de projeto que o GUID corresponde ao.  
  
-   Um subtipo de projeto também pode modificar o fragmento XML antes ou depois de ela delega a chamada para um subtipo de projeto interno. O exemplo a seguir mostra um trecho de um arquivo de projeto, onde um nome de um arquivo que contém propriedades específicas para um subtipo de projeto, é passado para esse subtipo de projeto.  
  
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

