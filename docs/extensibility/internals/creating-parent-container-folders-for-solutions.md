---
title: Criando pastas de contêiner pai para soluções | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 87fbda8cb55d0d2a6ef9f21a2a7878d4babd3fe6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49830685"
---
# <a name="create-parent-container-folders-for-solutions"></a>Criar pastas de contêiner para soluções de pai
No código-fonte controle plug-in API versão 1.2, um usuário pode especificar um destino de controle de origem de raiz única para todos os projetos da web dentro da solução. Essa única raiz é chamado de uma raiz de Unificação de Super (SUR).  
  
 Na fonte de controle de plug-in API versão 1.1, se o usuário tiver adicionado uma solução multiprojeto ao controle do código-fonte, o usuário foi solicitado a especificar um destino de controle de origem para cada projeto da web.  
  
## <a name="new-capability-flags"></a>Novos sinalizadores de recurso  
 `SCC_CAP_CREATESUBPROJECT`  
  
 `SCC_CAP_GETPARENTPROJECT`  
  
## <a name="new-functions"></a>Novas funções  
 [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)  
  
 [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE quase sempre cria uma pasta SUR ao adicionar uma solução ao controle de origem. Especificamente, isso é feito nos seguintes casos:  
  
-   O projeto é um projeto de web de compartilhamento de arquivo.  
  
-   Existem diferentes unidades para o projeto e o arquivo de solução.  
  
-   Não há compartilhamento diferente para o projeto e o arquivo de solução.  
  
-   Projetos foram adicionados separadamente (em uma solução de controle do código-fonte).  
  

No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)], é aconselhável que o nome da pasta SUR ser o mesmo que o nome da solução sem a extensão. A tabela a seguir resume o comportamento em duas versões.  
  
|Recurso|Versão 1.1 do API de plug-in de controle de origem|Versão 1.2 da API de plug-in de controle de origem|  
|-------------| - | - |  
|Adicionar solução ao SCC|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccGetProjPath()<br /><br /> SccOpenProject()|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject()|  
|Adicionar o projeto à solução de controle do código-fonte|SccGetProjPath()<br /><br /> OpenProject()|SccGetParentProjectPath()<br /><br /> SccOpenProject()<br /><br />  **Observação:** Visual Studio pressupõe que uma solução é um filho direto do SUR o.|  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir lista os dois exemplos. Em ambos os casos, o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] usuário é solicitado a fornecer um local de destino para a solução sob controle de origem até que o *user_choice* é especificado como um destino. Quando o user_choice for especificado, a solução e dois projetos são adicionados sem avisar o usuário para destinos de controle do código-fonte.  
  
|Solução contém|Em locais de disco|Estrutura do banco de dados padrão|  
|-----------------------|-----------------------|--------------------------------|  
|*sln1.sln*<br /><br /> Web1<br /><br /> WEB2|*C:\Solutions\sln1*<br /><br /> *C:\Inetpub\wwwroot\Web1*<br /><br /> \\\server\wwwroot$\Web2|$/ < user_choice > / sln1<br /><br /> $/ < user_choice >/C/Web1<br /><br /> $/ < user_choice > / Web2|  
|*sln1.sln*<br /><br /> Web1<br /><br /> Win1|*C:\Solutions\sln1*<br /><br /> *D:\Inetpub\wwwroot\Web1*<br /><br /> *C:\solutions\sln1\Win1*|$/ < user_choice > / sln1<br /><br /> $/ < user_choice >/D/web1<br /><br /> $/ < user_choice >/sln1/win1|  
  
 A pasta SUR e subpastas são criadas, independentemente da operação for cancelada ou falha devido a um erro. Eles não são removidos automaticamente em condições de erro ou cancelamento.  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] assume como padrão o comportamento da versão 1.1, se o plug-in de controle do código-fonte não retornar `SCC_CAP_CREATESUBPROJECT` e `SCC_CAP_GETPARENTPROJECT` sinalizadores de recurso. Além disso, os usuários do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] pode escolher reverter para o versão 1.1 comportamento, definindo o valor da chave a seguir *DWORD: 00000001*:  
  
 **[HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] DoNotCreateSolutionRootFolderInSourceControl** = *DWORD: 00000001*
  
## <a name="see-also"></a>Consulte também  
 [O que há de novo no controle de fonte de plug-in API versão 1.2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)