---
title: Elemento ProjectTemplateLink (modelos do Visual Studio) | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- http://schemas.microsoft.com/developer/vstemplate/2005#ProjectTemplateLink
helpviewer_keywords:
- <ProjectTemplateLink> element [Visual Studio Templates]
- ProjectTemplateLink element [Visual Studio Templates]
ms.assetid: b0449111-8b48-45a1-a031-ea24b765e969
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 792c89b7c4a804a91a0c6e07ed4e9a1f2244ba7d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51738854"
---
# <a name="projecttemplatelink-element-visual-studio-templates"></a>Elemento ProjectTemplateLink (modelos do Visual Studio)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Especifica o caminho para o arquivo .vstemplate de um projeto em um modelo de vários projetos.  
  
 \<VSTemplate >  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<ProjectTemplateLink >  
-ou-  
\<VSTemplate >  
 \<TemplateContent >  
 \<ProjectCollection >  
 \<SolutionFolder >  
 \<ProjectTemplateLink >  
  
## <a name="syntax"></a>Sintaxe  
  
```  
<ProjectTemplateLink ProjectName="Name">  
    PathToTemplateFile  
</ProjectTemplateLink>  
```  
  
## <a name="attributes-and-elements"></a>Atributos e elementos  
 As seções a seguir descrevem atributos, elementos filho e elementos pai.  
  
### <a name="attributes"></a>Atributos  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|`ProjectName`|Atributo opcional.<br /><br /> Especifica o nome de cada projeto individual em um modelo de vários projetos. O **novo projeto** caixa de diálogo não é possível atribuir nomes a projetos individuais.|  
|`CopyParameters`|Permite que todas as variáveis no modelo de grupo principal sejam copiadas em cada um dos modelos vinculados.<br /><br /> Os parâmetros nos modelos vinculados têm um prefixo `"$ext_*$"`. Por exemplo, se no modelo de grupo pai o parâmetro `$projectname$` tem um valor **ExampleProject1**, quando o modelo vinculado obtém sua vez para ser executado, ele adquire um parâmetro `$ext_projectname$`, que é uma cópia do `$projectname$`parâmetro de modelo de grupo pai.<br /><br /> Isso permite que modelos vinculados compartilhem alguns parâmetros comuns, que podem ser convenientemente criados somente no modelo de grupo pai.<br /><br /> Esse atributo é opcional e padronizado automaticamente para `false` quando não é incluído.<br /><br /> Introduzido no Visual Studio 2013 Atualização 2. Para fazer referência a versão correta do produto, consulte [Referenciando Assemblies entregues no Visual Studio 2013 SDK Update 2](http://msdn.microsoft.com/en-us/42b65c3e-e42b-4c39-98c8-bea285f25ffb).|  
  
### <a name="child-elements"></a>Elementos filho  
 nenhuma.  
  
### <a name="parent-elements"></a>Elementos pai  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|[ProjectCollection](../extensibility/projectcollection-element-visual-studio-templates.md)|Especifica a organização e o conteúdo de modelos de vários projetos.|  
|[SolutionFolder](../extensibility/solutionfolder-element-visual-studio-templates.md)|Agrupa projetos em modelos de vários projetos.|  
  
## <a name="text-value"></a>Valor de texto  
 Um valor de texto é obrigatório.  
  
 Esse texto especifica o caminho para o arquivo .vstemplate do modelo.  
  
## <a name="remarks"></a>Comentários  
 Os modelos de vários projetos atuam como contêineres para dois ou mais projetos. O elemento `ProjectTemplateLink` é usado para especificar o local do arquivo .vstemplate para um dos projetos no modelo. O arquivo .vstemplate de um modelo de vários projetos contém um elemento `ProjectTemplateLink` para cada projeto no modelo. Para obter mais informações sobre modelos de vários projetos, consulte [como: criar modelos de multiprojeto](../ide/how-to-create-multi-project-templates.md).  
  
## <a name="example"></a>Exemplo  
 Esse exemplo mostra um arquivo simples .vstemplate raiz de vários projetos. Neste exemplo, o modelo contém dois projetos, `My Windows Application` e `My Class Library`. O atributo `ProjectName` no elemento `ProjectTemplateLink` define o nome do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para atribuir este projeto. Se o atributo `ProjectName` não existir, o nome do arquivo .vstemplate é usado como o nome do projeto.  
  
```  
<VSTemplate Version="3.0.0" Type="ProjectGroup"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">  
    <TemplateData>  
        <Name>Multi-Project Template Sample</Name>  
        <Description>An example of a multi-project template</Description>  
        <Icon>Icon.ico</Icon>  
        <ProjectType>VisualBasic</ProjectType>  
    </TemplateData>  
    <TemplateContent>  
        <ProjectCollection>  
            <ProjectTemplateLink ProjectName="My Windows Application">  
                WindowsApp\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
            <ProjectTemplateLink ProjectName="My Class Library" CopyParameters="true">  
                ClassLib\MyTemplate.vstemplate  
            </ProjectTemplateLink>  
        </ProjectCollection>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)   
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Como criar modelos multiprojeto](../ide/how-to-create-multi-project-templates.md)

