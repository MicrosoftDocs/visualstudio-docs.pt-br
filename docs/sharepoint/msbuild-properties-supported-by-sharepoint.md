---
title: Propriedades de MSBuild suportadas pelo SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, MSBuild properties
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 1695a23ba9dddc27a37f23c714678fe6b779d328
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35669943"
---
# <a name="msbuild-properties-supported-by-sharepoint"></a>Propriedades de MsBuild suportadas por SharePoint
  Qualquer [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] propriedade definida no arquivo Microsoft.VisualStudio.SharePoint.targets, arquivo de projeto ou arquivo de usuário do projeto pode ser usada em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projetos do SharePoint. Além do comum [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] propriedades fornecidas pelo projeto do SharePoint define propriedades adicionais que são específicas para projetos do SharePoint.  
  
 Para obter uma lista do comum [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] propriedades, consulte [propriedades de projeto comuns do MSBuild](http://go.microsoft.com/fwlink/?LinkID=168687). Para obter uma lista completa das propriedades compatíveis com a linguagem de programação, examine os *. targets* arquivo, o arquivo de projeto (*. csproj* ou *. vbproj*), ou o usuário do projeto de arquivos ( *csproj* ou *. vbproj*).  
  
## <a name="msbuild-properties-specific-to-sharepoint"></a>Propriedades do MsBuild específicas para o SharePoint
 A seguinte tabela lista [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] as propriedades que se aplicam especificamente aos projetos do SharePoint na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Existem outras propriedades, mas eles são para uso interno.  
  
|Nome da Propriedade|Descrição|  
|-------------------|-----------------|  
|SharePointSiteUrl|Uma cadeia de caracteres que representa o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] ao site do SharePoint.|  
|SandboxedSolution|Um valor booliano que indica se a solução é uma solução em área restrita.|  
|ActiveDeploymentConfiguration|A configuração de implantação do Active Directory.|  
|IncludeAssemblyInPackage|Um valor booliano que indica se o assembly está incluído no arquivo do pacote.|  
|PreDeploymentCommand|Um valor de cadeia de caracteres que representa o comando para executar a etapa de comando de pré-implantação.|  
|PostDeploymentCommand|Um valor de cadeia de caracteres que representa o comando para executar a etapa de comando pós-implantação.|  
|CustomBeforeSharePointTargets|Uma cadeia de caracteres que representa o caminho de um [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] arquivo de destino. Se o arquivo de destino existe e é definido, ele será importado antes que os dados de destinos do SharePoint. Essa propriedade permite personalizar o processo de pacote por predefinir propriedades relacionadas ao empacotamento sem modificar o arquivo de destinos fornecido do SharePoint, ainda que o arquivo de destino ainda se aplica a todos os projetos do SharePoint.|  
|CustomAfterSharePointTargets|Uma cadeia de caracteres que representa o caminho de um [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] arquivo de destino. Se o arquivo de destino existe e é definido, é importado depois que todos os destinos dados do SharePoint. Essa propriedade permite que você personalize o processo de pacote, substituindo propriedades relacionadas ao empacotamento e destinos sem ter que modificar o arquivo de destinos fornecido do SharePoint, ainda que o arquivo de destino ainda se aplica a todos os projetos do SharePoint.|  
|LayoutPath|Uma cadeia de caracteres que representa o diretório raiz em que cada um dos arquivos sejam empacotados são colocados temporariamente os antes de serem adicionados para o *. wsp* arquivo. Esse caminho pode ser útil saber quando você substitui os destinos BeforeLayout e AfterLayout para adicionar, remover ou modificar os arquivos sejam empacotados, porque você pode usá-lo para alterar o conteúdo do *. wsp* arquivo.|  
|BasePackagePath|Uma cadeia de caracteres que representa a pasta na qual o pacote é colocado. Este valor usa o diretório de saída do projeto, como Bin\Debug.|  
|PackageExtension|Uma cadeia de caracteres que representa a extensão de nome de arquivo para acrescentar ao pacote. O valor padrão é wsp.|  
|AssemblyDeploymentTarget|Uma cadeia de caracteres que representa o local onde o assembly de projeto é implantado no servidor do SharePoint. Seu valor é GlobalAssemblyCache (o padrão) ou aplicativo Web. Essa propriedade também pode ser definida na janela Propriedades.|  
|PackageWithValidation|Um valor booliano que especifica se a validação é executada antes do empacotamento. Essa propriedade permite ignorar erros de validação durante a criação de pacotes.|  
|ValidatePackageDependsOn|Uma cadeia de caracteres que define os destinos adicionais a serem executados antes do destino ValidatePackage.|  
|TokenReplacementFileExensions|Uma cadeia de caracteres que define os arquivos que tenham seus tokens substituídos durante o empacotamento.|  
  
## <a name="use-msbuild-properties-in-the-properties-page"></a>Use as propriedades do MsBuild na página de propriedades
 Para obter flexibilidade, em vez de usar cadeias de caracteres codificadas na **linha de comando de pré-implantação** e **linha de comando de pós-implantação** caixas na página de propriedades do SharePoint, você pode usar o SharePoint propriedades como argumentos. Por exemplo, em vez de especificar um determinado [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] cadeia de caracteres para o site do SharePoint, em vez disso, você pode usar `$(SharePointSiteUrl)`.  
  
> [!NOTE]  
>  Você pode usar o [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] sintaxe da variável `$(` *propertyName* `)` ou a sintaxe da variável de ambiente `%` *propertyName* `%` para especificar uma propriedade.  
  
## <a name="see-also"></a>Consulte também
 [Referência do MSBuild](/visualstudio/msbuild/msbuild-reference)  
  