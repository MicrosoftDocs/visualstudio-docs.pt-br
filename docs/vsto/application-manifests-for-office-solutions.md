---
title: Manifestos do aplicativo para soluções do Office
ms.date: 02/02/2017
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application manifests [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a6272f145ee2c7ef2a91cc635112e440e6404457
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85531502"
---
# <a name="application-manifests-for-office-solutions"></a>Manifestos do aplicativo para soluções do Office
  Um manifesto de aplicativo é um arquivo XML que descreve os assemblies que são carregados em uma solução de Microsoft Office. As ferramentas de desenvolvimento Microsoft Office no Visual Studio usam o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] esquema de manifesto do aplicativo definido na referência de [manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md) .

 Os manifestos de aplicativo para soluções do Office usam os seguintes [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] elementos e atributos.

|Elemento|Descrição|Atributos|
|-------------|-----------------|----------------|
|[&#60;elemento&#62; do assembly &#40;aplicativo ClickOnce&#41;](../deployment/assembly-element-clickonce-deployment.md)|Obrigatórios. Elemento de nível superior.|**manifestVersion**|
|[&#60;elemento&#62; de assemblyIdentity &#40;aplicativo ClickOnce&#41;](../deployment/assemblyidentity-element-clickonce-deployment.md)|Obrigatórios. Identifica o [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] assembly primário do aplicativo.|**name**<br /><br /> **version**<br /><br /> **publicKeyToken**<br /><br /> **processorArchitecture**<br /><br /> **idioma**|
|[&#60;elemento de&#62; trustInfo &#40;aplicativo ClickOnce&#41;](../deployment/trustinfo-element-clickonce-application.md)|Identifica os requisitos de segurança do aplicativo.|Nenhum|
|[Elemento&#62; do ponto de entrada do&#60;&#40;aplicativo ClickOnce&#41;](../deployment/entrypoint-element-clickonce-application.md)|Obrigatórios. Identifica o ponto de entrada de código do aplicativo para execução.|**name**<br /><br /> **dependencyname**<br /><br /> **customHostSpecified**|
|[Elemento&#62; de dependência de&#60;&#40;aplicativo ClickOnce&#41;](../deployment/dependency-element-clickonce-deployment.md)|Obrigatórios. Identifica cada dependência necessária para que o aplicativo seja executado. Opcionalmente, identifica os assemblies que precisam ser pré-instalados.|Nenhum|
|[&#60;elemento&#62; de arquivo &#40;aplicativo ClickOnce&#41;](../deployment/file-element-clickonce-application.md)|Obrigatórios. Identifica cada arquivo não assembly que é usado pelo aplicativo. Pode incluir dados de isolamento de Component Object Model (COM) associados ao arquivo.|**name**<br /><br /> **size**|

 Os manifestos de aplicativo para soluções do Office têm o seguinte elemento no `co.v1` namespace.

```xml
<entryPoint>
    <co.v1:customHostSpecified />
</entryPoint>
```

 Esses manifestos de aplicativo também têm os seguintes elementos e atributos no `vstav3` namespace.

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
|[&#60;elemento de&#62; customHostSpecified &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customhostspecified-element-office-development-in-visual-studio.md)|Obrigatórios. Marca o manifesto especificamente como uma solução do Office.|Nenhum|
|[&#60;suplemento&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/addin-element-office-development-in-visual-studio.md)|Obrigatórios. Armazena pontos de entrada em um único namespace.|Nenhum|
|[&#60;elemento de&#62; entryPointsCollection &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypointscollection-element-office-development-in-visual-studio.md)|Obrigatórios. Agrupa todos os assemblies para uma ou mais soluções do Office.|**id**|
|[&#60;entryPoints&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoints-element-office-development-in-visual-studio.md)|Obrigatórios. Agrupa todos os assemblies para executar uma solução do Office.|Nenhum|
|[&#60;entryPoint&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/entrypoint-element-office-development-in-visual-studio.md)|Obrigatórios. Identifica o assembly a ser executado em uma solução do Office.|**classes**<br /><br /> **contrato**|
|[&#60;atualizar o elemento&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/update-element-office-development-in-visual-studio.md)|Obrigatórios. Configura as atualizações para a solução.|**habilitado**<br /><br /> **expiration**|
|[&#60;ações&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactions-element-office-development-in-visual-studio.md)|Opcional. Agrupa todas as ações pós-implantação, que são executadas depois que as soluções do Office são instaladas.|Nenhum|
|[&#60;elemento&#62; de ação de &#40;de desenvolvimento do Office no Visual Studio&#41;](../vsto/postaction-element-office-development-in-visual-studio.md)|Opcional. Identifica uma ação pós-implantação.|Nenhum|
|[&#60;elemento de&#62; postActionData &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/postactiondata-element-office-development-in-visual-studio.md)|Opcional. Configura os dados para uma ação pós-implantação.|Nenhum|
|[&#60;elemento de&#62; de aplicativo &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/application-element-office-development-in-visual-studio.md)|Obrigatórios. Encapsula as informações específicas do aplicativo em um único nó.|Nenhum|
|[&#60;personalizações&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customizations-element-office-development-in-visual-studio.md)|Obrigatórios. Armazena todas as informações específicas do host de aplicativo em um namespace separado.|Nenhum|
|[&#60;personalização&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/customization-element-office-development-in-visual-studio.md)|Obrigatórios. Armazena informações específicas do host do aplicativo em um namespace separado.|**xmlns**|
|[&#60;elemento de&#62; de documento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/document-element-office-development-in-visual-studio.md)|Necessário apenas para soluções de nível de documento. Armazena informações específicas de personalização.|**Solution**|
|[&#60;elemento de&#62; appAddin &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/appaddin-element-office-development-in-visual-studio.md)|Necessário apenas para soluções de nível de aplicativo. Armazena informações específicas de personalização.|**aplicativo**<br /><br /> **LoadBehavior**<br /><br /> **keyName**|
|[Elemento&#60;FriendlyName&#62; &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/friendlyname-element-office-development-in-visual-studio.md)|Opcional. Armazena o nome do suplemento do VSTO que aparece na lista de suplementos do VSTO instalados.|Nenhum|
|[&#60;Descrição&#62; elemento &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/description-element-office-development-in-visual-studio.md)|Necessário apenas para suplementos do VSTO. o armazena a descrição que aparece na lista de programas instalados.|Nenhum|
|[&#60;elemento de&#62; formRegions &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregions-element-office-development-in-visual-studio.md)|Necessário apenas para os suplementos do VSTO do Outlook que incluem regiões de formulário.|Nenhum|
|[&#60;elemento de&#62; formRegion &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/formregion-element-office-development-in-visual-studio.md)|Necessário apenas para os suplementos do VSTO do Outlook que incluem regiões de formulário.|**Nome**|
|[&#60;elemento de&#62; vstoRuntime &#40;desenvolvimento do Office no Visual Studio&#41;](../vsto/vstoruntime-element-office-development-in-visual-studio.md)|Obrigatórios. Descreve uma versão específica do Ferramentas do Visual Studio para o tempo de execução do Office que é suportado pela solução do Office.|**liberar**<br /><br /> **version**<br /><br /> **URL de suporte**|

## <a name="remarks"></a>Comentários
 Você pode editar manualmente os manifestos de aplicativo e implantação em soluções do Office. Posteriormente, você deve assinar novamente o aplicativo e os manifestos de implantação usando o Manifest Generation and Editing Tool (*mage.exe* e *mageui.exe*). Para obter mais informações, consulte [como: assinar novamente manifestos de aplicativo e implantação](../deployment/how-to-re-sign-application-and-deployment-manifests.md).

## <a name="file-location"></a>Local do arquivo
 Um manifesto de aplicativo é específico para uma única versão de uma solução. Por esse motivo, os manifestos do aplicativo devem ser armazenados separadamente dos manifestos de implantação. [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]coloca os arquivos específicos da versão em um subdiretório nomeado após a versão associada no subdiretório *arquivos do aplicativo* na pasta de publicação.

## <a name="file-name-syntax"></a>Sintaxe de nome de arquivo
 O nome de um arquivo de manifesto do aplicativo deve ser o nome completo e a extensão do aplicativo, conforme identificado no elemento **AssemblyIdentity** , seguido pela extensão *. manifest*. Por exemplo, um manifesto de aplicativo que se refere à personalização de *OutlookAddIn1.dll* usaria a seguinte sintaxe de nome de arquivo.

 `OutlookAddIn1.dll.manifest`

## <a name="see-also"></a>Confira também

- [Manifestos de implantação para soluções do Office](../vsto/deployment-manifests-for-office-solutions.md)
- [Manifesto do aplicativo ClickOnce](../deployment/clickonce-application-manifest.md)