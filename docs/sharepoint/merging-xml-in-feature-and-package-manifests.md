---
title: Mesclando XML em um recurso e pacote manifestos | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packaging
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d3101245d720e9fdd1c4923ea03acd5b2d4db816
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118446"
---
# <a name="merge-xml-in-feature-and-package-manifests"></a>Mesclar o XML em manifestos de recurso e pacote
  Recursos e pacotes são definidos por [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivos de manifesto. Esses manifestos empacotados são uma combinação de dados gerados em designers e personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] inseridos no modelo de manifesto pelos usuários. No tempo de empacotamento [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] mescla personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] instruções com o designer fornecido pelo [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] para formar o empacotados [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivo de manifesto. Elementos semelhantes, com as exceções disponível mais adiante exceções de mesclagem, são mesclados para evitar [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] erros de validação depois de implantar os arquivos para o SharePoint e para tornar o manifesto arquivos menores e mais eficiente.  
  
## <a name="modify-the-manifests"></a>Modificar os manifestos
 Você não pode modificar diretamente os arquivos de manifesto de pacote até que você desabilite os designers de pacote ou recurso. No entanto, você pode adicionar manualmente personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] elementos para o modelo de manifesto por meio os designers de pacote e o recurso ou o [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] editor. Para obter mais informações, consulte [como: personalizar um recurso do SharePoint](../sharepoint/how-to-customize-a-sharepoint-feature.md) e [como: personalizar um pacote de solução do SharePoint](../sharepoint/how-to-customize-a-sharepoint-solution-package.md).  
  
## <a name="feature-and-package-manifest-merge-process"></a>Processo de mesclagem de manifesto de recurso e pacote
 Ao combinar elementos personalizados junto com elementos fornecidos pelo designer, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usa o processo a seguir. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] verifica se cada elemento tem um valor de chave exclusivo. Se um elemento não tem nenhum valor de chave exclusivo, ele é acrescentado ao arquivo de manifesto empacotado. Da mesma forma, os elementos que têm várias chaves não podem ser mesclados. Portanto, eles são acrescentados ao arquivo de manifesto.  
  
 Se um elemento tem uma chave exclusiva, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] compara os valores do designer e as chaves personalizadas. Se os valores corresponderem, eles mesclagem em um único valor. Se os valores forem diferentes, o valor da chave designer é descartado e o valor da chave personalizado é usado. Coleções também são mescladas. Por exemplo, se o gerado pelo designer [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] e o personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] tanto contêm uma coleção de Assemblies, o manifesto de pacote contém apenas uma coleção de Assemblies.  
  
## <a name="merge-exceptions"></a>Exceções de mesclagem
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] mescla a maioria dos designer [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] elementos junto com personalizada semelhante [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] elementos, desde que eles têm um atributo de identificação único e exclusivo. No entanto, alguns elementos não têm o identificador exclusivo, necessário para [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] a mesclagem. Esses elementos são conhecidos como *mesclar exceções*. Nesses casos, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] não mescla personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] elementos junto com o designer fornecido pelo [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] elementos, mas em vez disso, acrescenta-o ao arquivo de manifesto empacotado.  
  
 A seguir está uma lista de exceções de mesclagem para o recurso e pacote [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] arquivos de manifesto.  
  
|Designer|Elemento XML|  
|--------------|-----------------|  
|Designer de recursos|ActivationDependency|  
|Designer de recursos|UpgradeAction|  
|Designer de pacote|SafeControl|  
|Designer de pacote|CodeAccessSecurity|  
  
## <a name="feature-manifest-elements"></a>Elementos do manifesto de recurso
 A tabela a seguir é uma lista de todos os elementos de manifesto de recurso que podem ser mesclados e sua chave exclusiva que é usado para correspondência.  
  
|Nome de elementos|Chave exclusiva|  
|------------------|----------------|  
|Recurso (todos os atributos)|*Nome do atributo* (cada nome de atributo do elemento recurso é uma chave exclusiva.)|  
|ElementFile|Local|  
|ElementManifests/ElementManifest|Local|  
|Propriedades ou propriedade|Chave|  
|CustomUpgradeAction|Nome|  
|CustomUpgradeActionParameter|Nome|  
  
> [!NOTE]  
>  Porque a única maneira de modificar o elemento CustomUpgradeAction está em personalizado [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] editor, o efeito da mesclagem não é baixo.  
  
## <a name="package-manifest-elements"></a>Elementos do manifesto de pacote
 A tabela a seguir é uma lista de todos os elementos de manifesto de pacote que podem ser mesclados e sua chave exclusiva que é usado para correspondência.  
  
|Nome de elementos|Chave exclusiva|  
|------------------|----------------|  
|Solução (todos os atributos)|*Nome do atributo* (cada nome de atributo do elemento de solução é uma chave exclusiva.)|  
|ApplicationResourceFiles/ApplicationResourceFile|Local|  
|Assemblies/Assembly|Local|  
|ClassResources/ClassResource|Local|  
|DwpFiles/DwpFile|Local|  
|FeatureManifests/FeatureManifest|Local|  
|Recursos/recursos|Local|  
|RootFiles/RootFile|Local|  
|SiteDefinitionManifests/SiteDefinitionManifest|Local|  
|WebTempFile|Local|  
|TemplateFiles/TemplateFile|Local|  
|SolutionDependency|SolutionID|  
  
## <a name="manually-add-deployed-files"></a>Adicionar manualmente os arquivos implantados
 Alguns elementos do manifesto, como ApplicationResourceFile e DwpFiles, especificam um local que inclui um nome de arquivo. No entanto, adicionar uma entrada de nome de arquivo para o modelo de manifesto não adiciona o arquivo subjacente ao pacote. Você deve adicionar o arquivo ao projeto para incluí-lo no pacote e defina sua propriedade de tipo de implantação adequadamente.  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)   
 [Compilar e depurar soluções do SharePoint](../sharepoint/building-and-debugging-sharepoint-solutions.md)  
  
