---
title: 'Como: Criar manualmente modelos da Web | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio templates, Web
- templates [Visual Studio], Web
- Web templates [Visual Studio]
- project templates [Visual Studio], Web
ms.assetid: 731c4027-a152-48c5-bfc4-93490bf1949f
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 8a505fe3428a8e16c321eee4764f8a62fff65511
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431091"
---
# <a name="how-to-manually-create-web-templates"></a>Como: Criar manualmente modelos da Web
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Criar um modelo de Web é diferente de criar outros tipos de modelos. Como modelos de projeto Web aparecem na caixa de diálogo **Adicionar Novo Site** e itens de projetos da Web são categorizados por linguagem de programação, o arquivo .vstemplate deve especificar o modelo como um modelo de Web e identificar a linguagem de programação.  
  
> [!NOTE]
> Modelos da Web devem conter um arquivo .webproj vazio que é especificado usando o atributo `File` do elemento `Project`. Embora projetos da Web não precisem de arquivos de projeto, esse arquivo é necessário para que um modelo da Web funcione corretamente.  
  
### <a name="to-manually-create-a-web-template"></a>Para criar manualmente um modelo da Web  
  
1. Crie um projeto Web.  
  
2. Modifique ou exclua os arquivos no projeto ou adicione novos arquivos ao projeto.  
  
3. Crie um arquivo XML e salve-o usando uma extensão de nome de arquivo .vstemplate no mesmo diretório que o seu projeto. Não adicione-o ao seu projeto no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
4. Crie o arquivo XML .vstemplate para fornecer metadados de modelo de projeto. Para obter mais informações, consulte o exemplo na seção a seguir.  
  
5. Localize o elemento `ProjectType` no arquivo .vstemplate e defina o valor de texto para `Web`.  
  
6. Após o elemento `ProjectType`, adicione um elemento `ProjectSubType` e defina o valor de texto como a linguagem de programação do modelo. A linguagem de programação pode ter um dos seguintes valores:  
  
   - CSharp  
  
   - VisualBasic  
  
     Por exemplo:  
  
   ```  
   <TemplateData>  
       ...  
       <ProjectType>Web</ProjectType>  
       <ProjectSubType>CSharp</ProjectSubType>  
       ...  
   </TemplateData>  
   ```  
  
7. Selecione os arquivos em seu modelo (isso inclui o modelo .vstemplate), clique com o botão direito do mouse na seleção, clique em **Enviar Para** e, em seguida, em **Pasta Compactada (zipada)**. Os arquivos são compactados em um arquivo .zip.  
  
8. Coloque o arquivo de modelo .zip no diretório de modelo de projeto [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]. Por padrão, esse diretório é \Meus Documentos\Visual Studio *Versão*\Templates\Meus Modelos Exportados\\.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra um arquivo .vstemplate básico para um modelo de projeto Web.  
  
```  
<VSTemplate Version="2.0.0" Type="Project"  
    xmlns="http://schemas.microsoft.com/developer/vstemplate/2005">>  
    <TemplateData>  
        <Name>MyWebProjecStarterKit</Name>  
        <Description>A simple Web template</Description>  
        <Icon>icon.ico</Icon>  
        <ProjectType>Web</ProjectType>  
        <ProjectSubType>CSharp</ProjectSubType>  
        <DefaultName>WebSite</DefaultName>  
    </TemplateData>  
    <TemplateContent>  
        <Project File="WebApplication.webproj">  
            <ProjectItem>icon.ico</ProjectItem>  
            <ProjectItem OpenInEditor="true">Default.aspx</ProjectItem>  
            <ProjectItem>Default.aspx.cs</ProjectItem>  
        </Project>  
    </TemplateContent>  
</VSTemplate>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Criando modelos de projeto e de item](../ide/creating-project-and-item-templates.md)   
 [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
