---
title: 'Como: instalar um plug-in de controle do código-fonte | Microsoft Docs'
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
- installation [Visual Studio SDK], source control plug-ins
- source control plug-ins, installing
ms.assetid: 9e2e01d9-7beb-42b2-99b2-86995578afda
caps.latest.revision: 33
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 5f151653387c95e77d775bfc9f37cbdfb9f824e7
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741627"
---
# <a name="how-to-install-a-source-control-plug-in"></a>Como: instalar um plug-in de controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Criando um controle de fonte plug-in envolve três etapas:  
  
1.  Crie uma DLL com as funções definidas na seção de referência de API de plug-in de controle do código-fonte desta documentação.  
  
2.  Implemente as funções definidas pelo API de plug-in de controle do código-fonte. Quando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] chamadas para ele, disponibilizar interfaces e caixas de diálogo de plug-in.  
  
3.  Registre a DLL, tornando as entradas do registro apropriado.  
  
## <a name="integration-with-visual-studio"></a>Integração com o Visual Studio  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] dá suporte a plug-ins de controle de origem que estão em conformidade com a API de plug-in de controle do código-fonte.  
  
### <a name="registering-the-source-control-plug-in"></a>Registrando o plug-in de controle do código-fonte  
 Antes de chama um ambiente de desenvolvimento integrado (IDE) em execução no sistema de controle do código-fonte, ele primeiro deve encontrar a fonte de DLL de plug-in que exporta a API de controle.  
  
##### <a name="to-register-the-source-control-plug-in-dll"></a>Para registrar o controle de fonte DLL de plug-in  
  
1.  Adicione duas entradas na chave HKEY_LOCAL_MACHINE na subchave do SOFTWARE que especifica seu subchave de nome de empresa seguido por seu subchave de nome de produto. O padrão é HKEY_LOCAL_MACHINE\SOFTWARE\\ *[nome da empresa]*\\ *[nome do produto]*\\ *[entrada]* = valor. As duas entradas sempre são chamadas SCCServerName e SCCServerPath. Cada um é uma cadeia de caracteres regular.  
  
     Por exemplo, se o nome da empresa é a Microsoft e seu produto de controle do código-fonte é chamado SourceSafe, então esse caminho de registro será HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe. Essa subchave a primeira entrada, SCCServerName, é uma cadeia de caracteres legível pelo usuário nomear seu produto. A segunda entrada, SCCServerPath, é o caminho completo para a fonte de controlar a DLL de plug-in IDE deve se conectar. A seguir fornece exemplos de entradas do registro:  
  
    |Exemplo de entrada de registro|Valor de exemplo|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerName|Microsoft Visual SourceSafe|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\SCCServerPath|c:\vss\win32\ssscc.dll|  
  
    > [!NOTE]
    >  O SCCServerPath é o caminho completo para o plug-in do SourceSafe. O plug-in de controle de origem usará nomes diferentes de produto e da empresa, mas os mesmos caminhos de entrada de registro.  
  
2.  As seguintes entradas de registro opcional podem ser usadas para modificar o comportamento do seu plug-in de controle de origem. Acesse essas entradas na subchave mesma como SccServerName e SccServerPath.  
  
    -   A entrada HideInVisualStudioregistry pode ser usada se você não quiser que seu código-fonte-plug-in controle apareça na lista de seleção de plug-in de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Essa entrada também afetará a comutação automática para o plug-in de controle do código-fonte. Um uso possível para essa entrada é se você fornecer um pacote de controle do código-fonte que substitui o plug-in de controle de origem, mas você deseja tornar mais fácil para o usuário migrar do usando o plug-in para o pacote de controle de origem de controle de origem. Quando o pacote de controle do código-fonte estiver instalado, ele define essa entrada de registro, que oculta o plug-in.  
  
         HideInVisualStudio é um valor DWORD e é definido como 1 para ocultar o plug-in ou 0 para mostrar o plug-in. Se a entrada do registro não aparecer, o comportamento padrão é mostrar o plug-in.  
  
    -   A entrada do registro DisableSccManager pode ser usada para desabilitar ou ocultar a **inicie \<servidor de controle de origem >** opção de menu que normalmente aparece sob o **arquivo**  ->   **Controle de fonte** submenu. Selecionando esse menu opção chamadas a [SccRunScc](../../extensibility/sccrunscc-function.md) função. O plug-in de controle de origem pode não oferecer suporte a um programa externo e, portanto, você talvez queira desativar ou ocultar até mesmo os **inicie** opção de menu.  
  
         DisableSccManager é um valor DWORD é definido como 0 para habilitar o **inicie \<servidor de controle de origem >** opção de menu, definido como 1 para desabilitar a opção de menu e definido como 2 para ocultar a opção de menu. Se essa entrada de registro não aparecer, o comportamento padrão é mostrar a opção de menu.  
  
    |Exemplo de entrada de registro|Valor de exemplo|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\HideInVisualStudio|1|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SourceSafe\DisableSccManager|1|  
  
3.  Adicione a subchave SourceCodeControlProvider, sob a chave HKEY_LOCAL_MACHINE na subchave do SOFTWARE.  
  
     Sob essa subchave, a entrada do registro ProviderRegKey é definido como uma cadeia de caracteres que representa a subchave que você colocou no registro na etapa 1. O padrão é HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey = SOFTWARE\\ *[nome da empresa]*\\ *[nome do produto]*.  
  
     A seguir está o conteúdo de exemplo para essa subchave.  
  
    |Entrada de registro|Valor de exemplo|  
    |--------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\ProviderRegKey|SOFTWARE\Microsoft\SourceSafe|  
  
    > [!NOTE]
    >  O plug-in de controle de origem usará a mesma subchave e nomes de entrada, mas o valor será diferente.  
  
4.  Crie uma subchave denominada InstalledSCCProviders SourceCodeControlProvider na subchave e, em seguida, colocar uma entrada sob essa subchave.  
  
     O nome desta entrada é o nome legível pelo usuário do provedor (o mesmo que o valor especificado para a entrada SCCServerName) e o valor for, mais uma vez, a subchave criada na etapa 1. O padrão é HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\\ *[nome de exibição]* = SOFTWARE\\ *[nome da empresa]* \\ *[nome do produto]*.  
  
     Por exemplo:  
  
    |Exemplo de entrada de registro|Valor de exemplo|  
    |---------------------------|------------------|  
    |HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider\InstalledSCCProviders\Microsoft Visual SourceSafe|SOFTWARE\Microsoft\SourceSafe|  
  
    > [!NOTE]
    >  Pode haver várias fonte plug-ins de controle registradas dessa forma. Isso é como [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] localiza todos instalados plug-ins baseados na API de plug-in de controle do código-fonte.  
  
## <a name="how-an-ide-locates-the-dll"></a>Como um IDE localiza a DLL  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] IDE tem duas maneiras de localizar a fonte de DLL de plug-in de controle:  
  
- Localize o controle de fonte padrão plug-in e conectá-lo silenciosamente.  
  
- Localize fonte registrada de todos os plug-ins de controle, do qual o usuário escolhe um.  
  
  Para localizar a DLL da primeira forma, o IDE se parece na subchave HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider para a entrada ProviderRegKey. O valor desta entrada aponta para outra subchave. O IDE, em seguida, procura por uma entrada denominada SccServerPath nessa segunda subchave sob HKEY_LOCAL_MACHINE. O valor desta entrada aponta o IDE para a DLL.  
  
> [!NOTE]
>  O IDE não carrega DLLs de caminhos relativos (por exemplo,.\NewProvider.DLL). Especifique um caminho completo para a DLL (por exemplo, c:\Providers\NewProvider.DLL). Isso reforça a segurança do IDE, impedindo que o carregamento de DLLs de plug-in não autorizados ou delegadas.  
  
 Para localizar a DLL da segunda forma, o IDE se parece em todas as entradas na subchave HKEY_LOCAL_MACHINE\Software\SourceCodeControlProvider\InstalledSCCProviders<em>.</em> Cada entrada tem um nome e um valor. O IDE exibirá uma lista desses nomes para o usuário<em>.</em> Quando o usuário escolhe um nome, o IDE localiza o valor para o nome selecionado que aponta para uma subchave. O IDE procurará uma entrada denominada SccServerPath nessa subchave sob HKEY_LOCAL_MACHINE. O valor desta entrada aponta o IDE para a DLL correta.  
  
 Um plug-in de controle de origem precisa dar suporte a ambas as maneiras de localizar a DLL e, consequentemente, definir ProviderRegKey, substituindo qualquer definição anterior. Mais importante, ele deve se adicionar à lista de InstalledSccProviders para que o usuário possa ter uma opção do qual plug-in de controle do código-fonte para usar.  
  
> [!NOTE]
>  Como a chave HKEY_LOCAL_MACHINE é usada, o plug-in de controle do código-fonte apenas uma pode ser registrado como o controle de fonte padrão plug-in em um determinado computador (no entanto, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] permite que os usuários determinar quais plug-in de controle de origem que desejam usar, na verdade, para um solução específica). Durante o processo de instalação, verifique se um plug-in de controle de origem já estiver definido; Nesse caso, peça ao usuário se deseja ou não definir o controle de fonte de novos plug-in que está sendo instalado como o padrão. Durante a desinstalação, não remova outros subchaves do registro que são comuns a controle de origem todos os plug-ins em HKEY_LOCAL_MACHINE\SOFTWARE\SourceCodeControlProvider; Remova somente seu subchave SCC específico.  
  
## <a name="how-the-ide-detects-version-1213-support"></a>Como o IDE detecta a versão 1.2/1.3 suporte  
 Como faz [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] detectar se uma funcionalidade de versão 1.2 e 1.3 do plug-in dá suporte à API de plug-in de controle do código-fonte? Para declarar a funcionalidade avançada, o plug-in de controle de origem deve implementar a função correspondente.  
  
 Primeiro, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] verifica o valor retornado ao chamar o [SccGetVersion](../../extensibility/sccgetversion-function.md). Ele deve ser maior que ou igual a 1.2.  
  
 Em seguida, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] determina se o novo recurso específico tem suporte, examinando o `lpSccCaps` argumento a [SccInitialize](../../extensibility/sccinitialize-function.md).  
  
 Se estas duas condições forem atendidas, as novas funções de suporte nas versões 1.2 e 1.3 podem ser chamadas.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução](../../extensibility/internals/getting-started-with-source-control-plug-ins.md)

