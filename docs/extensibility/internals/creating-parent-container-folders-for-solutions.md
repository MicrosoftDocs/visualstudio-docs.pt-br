---
title: Criando pastas de contêiner pai para soluções | Microsoft Docs
description: Saiba como usar a API de plug-in de controle do código-fonte versão 1,2 para especificar um destino de controle do código-fonte de raiz única para todos os projetos da Web em uma solução.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2c9b3b5c01e9c1ad5de9fbb0a44398d3f7963295
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056826"
---
# <a name="create-parent-container-folders-for-solutions"></a>Criar pastas de contêiner pai para soluções
Na API de plug-in de controle do código-fonte versão 1,2, um usuário pode especificar um destino de controle do código-fonte de raiz única para todos os projetos da Web na solução. Essa raiz única é chamada de sur (raiz unificada).

 Na API de plug-in de controle do código-fonte versão 1,1, se o usuário adicionou uma solução multiprojeto ao controle do código-fonte, o usuário foi solicitado a especificar um destino de controle do código-fonte para cada projeto Web.

## <a name="new-capability-flags"></a>Novos sinalizadores de capacidade
 `SCC_CAP_CREATESUBPROJECT`

 `SCC_CAP_GETPARENTPROJECT`

## <a name="new-functions"></a>Novas funções
- [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)

- [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)

 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE quase sempre cria uma pasta sur ao adicionar uma solução ao controle do código-fonte. Especificamente, isso é feito nos seguintes casos:

- O projeto é um projeto Web de compartilhamento de arquivos.

- Há unidades diferentes para o projeto e o arquivo de solução.

- Há diferentes compartilhamentos para o projeto e o arquivo de solução.

- Os projetos foram adicionados separadamente (em uma solução controlada por origem).

No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] , é recomendável que o nome da pasta sur seja o mesmo que o nome da solução sem a extensão. A tabela a seguir resume o comportamento nas duas versões.

|Recurso|API de plug-in de controle do código-fonte versão 1,1|API de plug-in de controle do código-fonte versão 1,2|
|-------------| - | - |
|Adicionar solução ao SCC|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccGetProjPath()<br /><br /> SccOpenProject()|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject()|
|Adicionar projeto à solução controlada por origem|SccGetProjPath()<br /><br /> OpenProject ()|SccGetParentProjectPath()<br /><br /> SccOpenProject()<br /><br />  **Observação:**  O Visual Studio pressupõe que uma solução é um filho direto do SUR.|

## <a name="examples"></a>Exemplos
 A tabela a seguir lista dois exemplos. Em ambos os casos, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usuário será solicitado a fornecer um local de destino para a solução no controle do código-fonte até que a  *user_choice* seja especificada como um destino. Quando o user_choice é especificado, a solução e dois projetos são adicionados sem solicitar ao usuário destinos de controle do código-fonte.

|A solução contém|Em locais de disco|Estrutura padrão do banco de dados|
|-----------------------|-----------------------|--------------------------------|
|*sln1. sln*<br /><br /> Web1<br /><br /> Web2|*C:\Solutions\sln1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot $ \Web2|$/<user_choice>/sln1<br /><br /> $/<user_choice>/C/Web1<br /><br /> $/<user_choice>/web2|
|*sln1. sln*<br /><br /> Web1<br /><br /> Win1|*C:\Solutions\sln1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/<user_choice>/sln1<br /><br /> $/<user_choice>/D/web1<br /><br /> $/<user_choice>/sln1/win1|

 A pasta SUR e as subpastas são criadas independentemente de a operação ser cancelada ou falhar devido a um erro. Elas não são removidas automaticamente em condições de cancelamento ou erro.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o padrão é o comportamento da versão 1,1 se o plug-in de controle do código-fonte não retornar `SCC_CAP_CREATESUBPROJECT` e os `SCC_CAP_GETPARENTPROJECT` sinalizadores de funcionalidade. Além disso, os usuários de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] podem optar por reverter para o comportamento da versão 1,1 definindo o valor da seguinte chave como *DWORD: 00000001*:

 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl**  =  *DWORD: 00000001*

## <a name="see-also"></a>Confira também
- [O que há de novo na API de plug-in de controle do código-fonte versão 1,2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
