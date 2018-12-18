---
title: Criando pastas de contêiner pai para soluções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- solutions, creating parent containers
- source control plug-ins, creating parent containers
ms.assetid: 961e68ed-2603-4479-a306-330eda2b2efa
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0a65595b7dabc28a6851820141a71460d84a4b73
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762538"
---
# <a name="creating-parent-container-folders-for-solutions"></a>Criando pastas de contêiner pai para soluções
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Na fonte de controle de plug-in API versão 1.2, um usuário pode especificar um destino de controle de origem de raiz única para todos os projetos da Web dentro da solução. Essa única raiz é chamado de uma raiz de Unificação de Super (SUR).  
  
 A fonte de plug-in de API de controle de versão 1.1, se o usuário tiver adicionado uma solução multiprojeto ao controle do código-fonte, o usuário foi solicitado para especificar um destino de controle de origem para cada projeto da Web.  
  
## <a name="new-capability-flags"></a>Novos sinalizadores de recurso  
 `SCC_CAP_CREATESUBPROJECT`  
  
 `SCC_CAP_GETPARENTPROJECT`  
  
## <a name="new-functions"></a>Novas funções  
 [SccCreateSubProject](../../extensibility/scccreatesubproject-function.md)  
  
 [SccGetParentProjectPath](../../extensibility/sccgetparentprojectpath-function.md)  
  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE quase sempre cria uma pasta SUR ao adicionar uma solução ao controle de origem. Especificamente, isso é feito nos seguintes casos:  
  
- O projeto é um compartilhamento de arquivos de projeto da Web.  
  
- Existem diferentes unidades para o projeto e o arquivo de solução.  
  
- Não há compartilhamento diferente para o projeto e o arquivo de solução.  
  
- Projetos foram adicionados separadamente (em uma solução de controle do código-fonte).  
  
  No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] é aconselhável que o nome da pasta SUR ser o mesmo que o nome da solução sem a extensão. A tabela a seguir resume o comportamento em duas versões.  
  
|Recurso|tSource 1.1 de versão de API de plug-in de controle|Versão 1.2 da API de plug-in de controle de origem|  
|-------------|----------------------------------------------|---------------------------------------------|  
|Adicionar solução ao SCC|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccGetProjPath()<br /><br /> SccOpenProject()|SccInitialize()<br /><br /> SccGetProjPath()<br /><br /> SccCreateSubProject()<br /><br /> SccCreateSubProject()<br /><br /> SccOpenProject()|  
|Adicionar o projeto à solução de controle do código-fonte|SccGetProjPath()<br /><br /> OpenProject()|SccGetParentProjectPath()<br /><br /> SccOpenProject() **Observação:** Visual Studio pressupõe que uma solução é um filho direto do SUR o.|  
  
## <a name="examples"></a>Exemplos  
 A tabela a seguir lista os dois exemplos. Em ambos os casos, o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] usuário é solicitado a fornecer um local de destino para a solução sob controle de origem até que o *user_choice* é especificado como um destino. Quando o user_choice for especificado, a solução e dois projetos são adicionados sem avisar o usuário para destinos de controle do código-fonte.  
  
|Solução contém|Em locais de disco|Estrutura do banco de dados padrão|  
|-----------------------|-----------------------|--------------------------------|  
|sln1.sln<br /><br /> Web1<br /><br /> WEB2|C:\Solutions\sln1<br /><br /> C:\Inetpub\wwwroot\Web1<br /><br /> \\\server\wwwroot$\web2|$/*user_choice*/sln1<br /><br /> $/*user_choice*  /C/Web1<br /><br /> $/*user_choice*/Web2|  
|sln1.sln<br /><br /> Web1<br /><br /> Win1|C:\Solutions\sln1<br /><br /> D:\Inetpub\wwwroot\Web1<br /><br /> C:\solutions\sln1\Win1|$/*user_choice*/sln1<br /><br /> $/*user_choice*  /D/web1<br /><br /> $/*user_choice*  /sln1/win1|  
  
 A pasta SUR e subpastas são criadas, independentemente da operação seja cancelada ou falha devido a um erro. Eles não são removidos automaticamente em condições de erro ou cancelamento.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] assume como padrão o comportamento da versão 1.1, se o plug-in de controle do código-fonte não retornar `SCC_CAP_CREATESUBPROJECT` e `SCC_CAP_GETPARENTPROJECT` sinalizadores de recurso. Além disso, os usuários de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] pode escolher reverter para o versão 1.1 comportamento, definindo o valor da chave a seguir como DWORD: 00000001:  
  
 [HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\8.0\SourceControl] "DoNotCreateSolutionRootFolderInSourceControl" = DWORD: 00000001  
  
## <a name="see-also"></a>Consulte também  
 [Novidades na Versão 1.2 da API do plug-in de controle de código-fonte](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)

