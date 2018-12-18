---
title: Parâmetros de modelo | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio templates, parameters
- template parameters [Visual Studio]
- project templates, parameters
- item templates, parameters
ms.assetid: 1b567143-08c6-4d7a-b484-49f0671754fe
caps.latest.revision: 27
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ef4e1a6e3c56df744ce5375a1cb3a1dbd53a6fad
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49238895"
---
# <a name="template-parameters"></a>Parâmetros de modelo
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Usando parâmetros em seus modelos, você pode substituir os valores das principais partes do modelo, como nomes de classe e namespaces, quando o modelo é instanciado. Esses parâmetros são substituídos pelo assistente de modelo que é executado em segundo plano quando um usuário clica em **OK** nas caixas de diálogo **Novo Projeto** ou **Adicionar Novo Item**.  
  
## <a name="declaring-and-enabling-template-parameters"></a>Declarando e habilitando parâmetros de modelo  
 Parâmetros de modelo são declarados no formato $*parâmetro*$. Por exemplo:  
  
-   $safeprojectname$  
  
-   $guid1$  
  
-   $guid5$  
  
#### <a name="to-enable-parameter-substitution-in-templates"></a>Para habilitar a substituição de parâmetro nos modelos  
  
1.  No arquivo .vstemplate do modelo, localize o elemento `ProjectItem` que corresponde ao item para o qual você deseja habilitar a substituição de parâmetro.  
  
2.  Defina o atributo `ReplaceParameters` do elemento `ProjectItem` como `true`.  
  
3.  No arquivo de código do item de projeto, inclua parâmetros conforme apropriado. Por exemplo, o parâmetro a seguir especifica que o nome de projeto safe seja usado para o namespace em um arquivo:  
  
    ```  
    namespace $safeprojectname$  
    ```  
  
## <a name="reserved-template-parameters"></a>Parâmetros de modelo reservados  
 A tabela a seguir lista os parâmetros de modelo reservados que podem ser usados por qualquer modelo.  
  
> [!NOTE]
>  Parâmetros de modelo diferenciam maiúsculas de minúsculas.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|`clrversion`|Versão atual do CLR (Common Language Runtime).|  
|`GUID [1-10]`|Um GUID usado para substituir o GUID do projeto em um arquivo de projeto. É possível especificar até 10 GUIDs exclusivos (por exemplo, `guid1)`.|  
|`itemname`|O nome fornecido pelo usuário na caixa de diálogo **Adicionar Novo Item**.|  
|`machinename`|O nome do computador atual (por exemplo, Computer01).|  
|`projectname`|O nome fornecido pelo usuário na caixa de diálogo **Novo Projeto**.|  
|`registeredorganization`|O valor da chave do Registro de HKLM\Software\Microsoft\Windows NT\CurrentVersion\RegisteredOrganization.|  
|`rootnamespace`|O namespace raiz do projeto atual. Esse parâmetro se aplica somente a modelos de item.|  
|`safeitemname`|O nome fornecido pelo usuário na caixa de diálogo **Adicionar Novo Item**, com todos os caracteres desprotegidos e espaços removidos.|  
|`safeprojectname`|O nome fornecido pelo usuário na caixa de diálogo **Novo Projeto**, com todos os caracteres desprotegidos e espaços removidos.|  
|`time`|A hora atual no formato DD/MM/AAAA 00:00:00.|  
|`SpecificSolutionName`|O nome da solução. Quando "criar diretório da solução" estiver marcado, `SpecificSolutionName` terá o nome da solução. Quando "criar diretório da solução" não estiver marcado, `SpecificSolutionName` estará em branco.|  
|`userdomain`|O domínio do usuário atual.|  
|`username`|O nome de usuário atual.|  
|`webnamespace`|O nome do site da Web atual. Esse parâmetro é usado no modelo de formulário da Web para assegurar nomes de classe exclusivos. Se o site da Web estiver no diretório raiz do servidor Web, esse parâmetro de modelo será resolvido para o diretório raiz do servidor Web.|  
|`year`|O ano atual no formato AAAA.|  
  
## <a name="custom-template-parameters"></a>Parâmetros de modelo personalizados  
 Você pode especificar seus próprios valores e parâmetros de modelo, além dos parâmetros de modelo reservados padrão, que são usados durante a substituição de parâmetros. Para obter mais informações, consulte [Elemento CustomParameters (modelos do Visual Studio)](../extensibility/customparameters-element-visual-studio-templates.md)  
  
## <a name="example-replacing-files-names"></a>Exemplo: substituindo nomes de arquivos  
 Você pode especificar nomes de arquivo variáveis para itens de projeto usando um parâmetro com o atributo `TargetFileName`. Por exemplo, você pode especificar que o arquivo .exe use o nome do projeto, especificado por `$projectname$`, como o nome do arquivo.  
  
```  
<TemplateContent>  
    <ProjectItem  
        ReplaceParameters="true"  
        TargetFileName="$projectname$.exe">  
            File1.exe  
    </ProjectItem>  
      ...  
</TemplateContent>  
```  
  
## <a name="example-using-the-project-name-for-the-namespace-name"></a>Exemplo: usando o nome do projeto como nome do namespace  
 Para usar o nome do projeto como namespace em um arquivo de classe do Visual C#, Class1.cs, use a sintaxe a seguir:  
  
```  
#region Using directives  
  
using System;  
using System.Collections.Generic;  
using System.Text;  
  
#endregion  
  
namespace $safeprojectname$  
{  
    public class Class1  
        {  
            public Class1()  
                {  
  
                }  
         }  
}  
```  
  
 No arquivo .vstemplate do modelo do projeto, inclua o seguinte XML ao fazer referência ao arquivo Class1.cs:  
  
```  
<TemplateContent>  
    <ProjectItem ReplaceParameters="true">  
        Class1.cs  
    </ProjectItem>  
    ...  
</TemplateContent>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Personalizando modelos](../ide/customizing-project-and-item-templates.md)



