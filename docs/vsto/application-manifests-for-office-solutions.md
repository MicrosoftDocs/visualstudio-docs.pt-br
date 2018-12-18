---
title: Manifestos de aplicativo para soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9665be31a59de33713f981889bc8cb8a8cb55eea
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248170"
---
# <a name="application-manifests-for-office-solutions"></a>Manifestos de aplicativo para soluções do Office
  Um manifesto de aplicativo é um arquivo XML que descreve os assemblies que são carregados em uma solução do Microsoft Office. Usam as ferramentas de desenvolvimento do Microsoft Office no Visual Studio a [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] esquema de manifesto de aplicativo definida na [manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest) referência.  
  
 Manifestos de aplicativo para soluções do Office usam o seguinte [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] elementos e atributos.  
  
|Elemento|Descrição|Atributos|  
|-------------|-----------------|----------------|  
|[&#60;assembly&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/assembly-element-clickonce-deployment)|Necessário. Elemento de nível superior.|**manifestVersion**|  
|[&#60;assemblyIdentity&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/assemblyidentity-element-clickonce-deployment)|Necessário. Identifica o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] assembly principal do aplicativo.|**name**<br /><br /> **version**<br /><br /> **publicKeyToken**<br /><br /> **ProcessorArchitecture**<br /><br /> **language**|  
|[&#60;trustInfo&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/trustinfo-element-clickonce-application)|Identifica os requisitos de segurança do aplicativo.|Nenhum|  
|[&#60;entryPoint&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/entrypoint-element-clickonce-application)|Necessário. Identifica o ponto de entrada de código do aplicativo para execução.|**name**<br /><br /> **dependencyName**<br /><br /> **customHostSpecified**|  
|[&#60;dependência&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/dependency-element-clickonce-deployment)|Necessário. Identifica cada dependência necessária para a execução do aplicativo. Opcionalmente, identifica os assemblies que precisam ser pré-instalado.|Nenhum|  
|[&#60;arquivo&#62; elemento &#40;aplicativo ClickOnce&#41;](/visualstudio/deployment/file-element-clickonce-application)|Necessário. Identifica cada arquivo não assembly que é usado pelo aplicativo. Pode incluir dados de isolamento (COM Component Object Model) associados ao arquivo.|**name**<br /><br /> **size**|  
  
 Manifestos de aplicativo para soluções do Office têm o seguinte elemento `co.v1` namespace.  
  
```xml  
<entryPoint>  
    <co.v1:customHostSpecified />  
</entryPoint>   
```  
  
 Esses manifestos de aplicativo também tem os seguintes elementos e atributos no `vstav3` namespace.  
  
```xml  
<addIn>  
  <entryPointsCollection>  
    <entryPoints>  
      <entryPoint>  
      </entryPoint>  
    </entryPoints>  
  </entryPointsCollection>  
  <update></update>  
  <postActions>  
    <postAction>  
      <postActionData>  
      </postActionData>  
    <postAction>  
  </postActions>  
  <application>  
    <customizations>  
      <customization>  
      </customization>  
    </customizations>  
  </application  
</addIn>  
```  
  
|Elemento|Descrição|Atributos|  
|-------------|-----------------|----------------|  
|[&#60;customHostSpecified&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customhostspecified-element-office-development-in-visual-studio.md)|Necessário. Marca o manifesto especificamente como uma solução do Office.|Nenhum|  
|[&#60;suplemento do&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/addin-element-office-development-in-visual-studio.md)|Necessário. Armazena pontos de entrada em um único namespace.|Nenhum|  
|[&#60;entryPointsCollection&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypointscollection-element-office-development-in-visual-studio.md)|Necessário. Agrupa todos os assemblies para um ou mais soluções do Office.|**id**|  
|[&#60;pontos de entrada&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)|Necessário. Grupos de todos os assemblies para executar uma solução do Office.|Nenhum|  
|[&#60;entryPoint&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoint-element-office-development-in-visual-studio.md)|Necessário. Identifica o assembly para ser executado em uma solução do Office.|**class**<br /><br /> **contrato**|  
|[&#60;atualizar&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/update-element-office-development-in-visual-studio.md)|Necessário. Configura as atualizações para a solução.|**habilitado**<br /><br /> **expiração**|  
|[&#60;postActions&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactions-element-office-development-in-visual-studio.md)|Opcional. Agrupa todas as ações de pós-implantação que são executados após a instalação de soluções do Office.|Nenhum|  
|[&#60;postAction&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postaction-element-office-development-in-visual-studio.md)|Opcional. Identifica uma ação pós-implantação.|Nenhum|  
|[&#60;postActionData&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactiondata-element-office-development-in-visual-studio.md)|Opcional. Configura os dados para uma ação pós-implantação.|Nenhum|  
|[&#60;aplicativo&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/application-element-office-development-in-visual-studio.md)|Necessário. Encapsula as informações específicas do aplicativo em um único nó.|Nenhum|  
|[&#60;personalizações de&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customizations-element-office-development-in-visual-studio.md)|Necessário. Armazena todas as informações de host específico do aplicativo em um namespace separado.|Nenhum|  
|[&#60;personalização&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customization-element-office-development-in-visual-studio.md)|Necessário. Armazena informações de host específico do aplicativo em um namespace separado.|**xmlns**|  
|[&#60;documento&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/document-element-office-development-in-visual-studio.md)|Necessário apenas para soluções de nível de documento. Armazena informações específicas de personalização.|**solutionId**|  
|[&#60;appAddin&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/appaddin-element-office-development-in-visual-studio.md)|Necessário apenas para soluções em nível de aplicativo. Armazena informações específicas de personalização.|**Aplicativo**<br /><br /> **LoadBehavior**<br /><br /> **keyName**|  
|[&#60;nome amigável&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md)|Opcional. Armazena o nome do suplemento VSTO que aparece na lista de VSTO Add-ins instalados.|Nenhum|  
|[&#60;Descrição&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/description-element-office-development-in-visual-studio.md)|Necessário apenas para suplementos do VSTO. Armazena a descrição que aparece na lista de programas instalados.|Nenhum|  
|[&#60;formRegions&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregions-element-office-development-in-visual-studio.md)|Necessário apenas para Outlook suplementos do VSTO que incluem regiões de formulário.|Nenhum|  
|[&#60;formRegion&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregion-element-office-development-in-visual-studio.md)|Necessário apenas para Outlook suplementos do VSTO que incluem regiões de formulário.|**Nome**|  
|[&#60;vstoRuntime&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/vstoruntime-element-office-development-in-visual-studio.md)|Necessário. Descreve uma versão específica do Visual Studio Tools para Office runtime que é compatível com a solução do Office.|**release**<br /><br /> **version**<br /><br /> **supportUrl**|  
  
## <a name="remarks"></a>Comentários  
 Você pode editar manualmente o aplicativo e manifestos de implantação em soluções do Office. Depois disso, você deve reassinar o aplicativo e manifestos de implantação usando o Manifest Generation and Editing Tool (*mage.exe* e *mageui.exe*). Confira mais informações em [Como: Assinar novamente os manifestos de aplicativo e implantação](/visualstudio/deployment/how-to-re-sign-application-and-deployment-manifests).  
  
## <a name="file-location"></a>Local do arquivo  
 Um manifesto de aplicativo é específico para uma única versão de uma solução. Por esse motivo, os manifestos de aplicativo devem ser armazenados separadamente dos manifestos de implantação. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] coloca os arquivos específicos de versão em um subdiretório chamado depois da versão associada na *arquivos de aplicativo* subdiretório na pasta publish.  
  
## <a name="file-name-syntax"></a>Sintaxe de nome de arquivo  
 O nome de um arquivo de manifesto do aplicativo deve ser o nome completo e a extensão do aplicativo, conforme identificado na **assemblyIdentity** elemento, seguido pela extensão *. manifest*. Por exemplo, um manifesto de aplicativo refere-se para o *OutlookAddIn1.dll* personalização usaria a seguinte sintaxe de nome de arquivo.  
  
 `OutlookAddIn1.dll.manifest`  
  
## <a name="see-also"></a>Consulte também  
 [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)   
 [Manifesto do aplicativo ClickOnce](/visualstudio/deployment/clickonce-application-manifest)  
  
  