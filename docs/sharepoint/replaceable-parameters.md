---
title: Parâmetros substituíveis | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, tokens
- tokens [SharePoint development in Visual Studio]
- replaceable parameters [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, replaceable parameters
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload: office
ms.openlocfilehash: e79442ea42583f326f9cb59360777269c399b7a0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49879292"
---
# <a name="replaceable-parameters"></a>Parâmetros substituíveis
  Parâmetros substituíveis, ou *tokens*, pode ser usado em arquivos de projeto para fornecer valores para os itens de solução do SharePoint cujos valores reais não são conhecidos em tempo de design. Elas são semelhantes em função para o padrão [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] tokens de modelo. Para obter mais informações, consulte [parâmetros de modelo](/visualstudio/ide/template-parameters).  
  
## <a name="token-format"></a>Formato do token
 Tokens começam e terminam com um caractere de cifrão ($). Na implantação, todos os tokens usados são substituídos por valores reais quando um projeto é empacotado em um pacote de solução do SharePoint (*. wsp* arquivo). Por exemplo, o token **$SharePoint.Package.Name$** possa ser resolvida para a cadeia de caracteres "Pacote de teste do SharePoint".  
  
## <a name="token-rules"></a>Regras de token
 As seguintes regras se aplicam aos tokens:  
  
- Tokens podem ser especificados em qualquer lugar em uma linha.  
  
- Tokens não podem abranger várias linhas.  
  
- O mesmo token pode ser especificado mais de uma vez na mesma linha e no mesmo arquivo.  
  
- Tokens diferentes podem ser especificadas na mesma linha.  
  
  Tokens que não segue essas regras são ignorados e não resultam em um aviso ou erro.  
  
  A substituição de tokens por valores de cadeia de caracteres é feita imediatamente após a transformação de manifesto. Essa substituição permite que o usuário edite os modelos com tokens de manifesto.  
  
### <a name="token-name-resolution"></a>Resolução de nome do token
 Na maioria dos casos, um token será resolvido como um valor específico, independentemente de onde ele está contido. No entanto, se o token estiver relacionado a um pacote ou recurso, valor do token depende de onde ele está contido. Por exemplo, se um recurso está em empacotar um, em seguida, o token `$SharePoint.Package.Name$` resolve para o valor "Pacote de r." Se o mesmo recurso está no pacote B, em seguida, `$SharePoint.Package.Name$` resolve para o "Pacote B."  
  
## <a name="tokens-list"></a>Lista de tokens
 A tabela a seguir lista os tokens disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|$SharePoint.Project.FileName$|O nome do que contém o arquivo, do projeto, como *NewProj.csproj*.|  
|$SharePoint.Project.FileNameWithoutExtension$|O nome do arquivo de projeto sem a extensão de nome de arquivo. Por exemplo, "NewProj".|  
|$SharePoint.Project.AssemblyFullName$|O nome de exibição (nome forte) do projeto do assembly de saída.|  
|$SharePoint.Project.AssemblyFileName$|O nome do projeto do assembly de saída.|  
|$SharePoint.Project.AssemblyFileNameWithoutExtension$|O nome do projeto saída do assembly, sem a extensão de nome de arquivo.|  
|$SharePoint.Project.AssemblyPublicKeyToken$|Assembly, convertido em uma cadeia de caracteres de saída do token de chave pública do projeto. (16-caracteres de "x2" formato hexadecimal.)|  
|$SharePoint.Package.Name$|O nome do pacote de conteúdo.|  
|$SharePoint.Package.FileName$|O nome do arquivo de definição do pacote que o contém.|  
|$SharePoint.Package.FileNameWithoutExtension$|O nome (sem extensão) do pacote de conteúdo arquivo de definição.|  
|$SharePoint.Package.Id$|A ID do SharePoint para o pacote de conteúdo. Se um recurso é usado em mais de um pacote, esse valor será alterado.|  
|$SharePoint.Feature.FileName$|O nome do arquivo de definição do que contém recursos, como *Feature1.feature*.|  
|$SharePoint.Feature.FileNameWithoutExtension$|O nome do arquivo de definição de recurso, sem a extensão de nome de arquivo.|  
|$SharePoint.Feature.DeploymentPath$|O nome da pasta que contém o recurso no pacote. Esse token é igual à propriedade "Caminho de implantação" no Designer de recurso. Um valor de exemplo é "Project1_Feature1".|  
|$SharePoint.Feature.Id$|A ID do SharePoint do recurso de recipiente. Esse token, como com todos os tokens de nível de recurso, pode ser usado somente pelos arquivos incluídos em um pacote por meio de um recurso, não adicionados diretamente a um pacote fora de um recurso.|  
|$SharePoint.ProjectItem.Name$|O nome do item de projeto (não o nome de arquivo), conforme obtido de **ISharePointProjectItem.Name**.|  
|$SharePoint.Type. \<GUID >. $ AssemblyQualifiedName|O nome qualificado do assembly da correspondência de tipo a [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] do token. O formato do [!INCLUDE[TLA2#tla_guid](../sharepoint/includes/tla2sharptla-guid-md.md)] fica em letras minúsculas e corresponde ao formato Guid.ToString("D") (ou seja, xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx).|  
|$SharePoint.Type. \<GUID >. $ FullName|O nome completo do tipo correspondente a GUID no token. O formato do GUID fica em letras minúsculo e corresponde ao formato Guid.ToString("D") (ou seja, xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx).|  
  
## <a name="add-extensions-to-the-token-replacement-file-extensions-list"></a>Adicionar extensões à lista de extensões de arquivo de substituição de token
 Embora os tokens, teoricamente, podem ser usados por qualquer arquivo que pertence a um projeto do SharePoint item incluído no pacote, por padrão, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] procura tokens somente em arquivos de pacote, arquivos de manifesto e arquivos que têm as seguintes extensões:  
  
- [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)]  
  
- ASCX  
  
- ASPX  
  
- Web Part  
  
- DWP  
  
  Essas extensões são definidas pelo `<TokenReplacementFileExtensions>` elemento no arquivo Microsoft.VisualStudio.SharePoint.targets, localizado na... \\< arquivos de programa\>\MSBuild\Microsoft\VisualStudio\v11.0\SharePointTools pasta.  
  
  No entanto, você pode, adicionar extensões de arquivo adicionais à lista. Adicionar um `<TokenReplacementFileExtensions>` elemento para qualquer PropertyGroup no arquivo de projeto do SharePoint que é definido antes do \<importação > do arquivo de destinos do SharePoint.  
  
> [!NOTE]  
>  Como a substituição de token ocorre depois que um projeto é compilado, você não deve adicionar extensões de arquivo para tipos de arquivos que são compilados, como *. CS*, *. vb* ou *. resx*. Tokens são substituídos somente em arquivos que não são compilados.  
  
 Por exemplo, para adicionar as extensões de nome de arquivo (*.myextension* e *.yourextension*) à lista de extensões de nome de arquivo de substituição de token, adicione o seguinte a um projeto (*. csproj* ) arquivo:  
  
```xml  
<Project ToolsVersion="4.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>  
.  
.  
.  
    <!-- Define the following property to add your extension to the list of token replacement file extensions.  -->  
<TokenReplacementFileExtensions>myextension;yourextension</TokenReplacementFileExtensions>  
</PropertyGroup>  
```  
  
 Você pode adicionar a extensão diretamente para o público-alvo (*. targets*) arquivos. No entanto, adicionar a extensão altera a lista de extensões para todos os projetos do SharePoint empacotados no sistema local, não apenas seu próprio. Esta extensão pode ser conveniente quando você o único desenvolvedor do sistema ou se a maioria dos seus projetos exigirem. No entanto, porque ele é específico do sistema, essa abordagem não é portátil e, portanto, é recomendável que você adiciona quaisquer extensões para o arquivo de projeto em vez disso.  
  
## <a name="see-also"></a>Consulte também
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
