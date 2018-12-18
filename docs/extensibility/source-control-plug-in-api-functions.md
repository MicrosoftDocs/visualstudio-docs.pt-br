---
title: Funções de API de plug-in de controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a834c4352ea2444c2669a57f760ed373999b07dd
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31144363"
---
# <a name="source-control-plug-in-api-functions"></a>Funções de API de plug-in de controle de origem
A API de plug-in de controle de origem contém as seguintes funções, que devem ser implementadas pelo plug-in de acordo com essa API de controle de origem. As assinaturas de cada função e a semântica associada com os sinalizadores de bit e outros parâmetros são descritos em detalhes nesta referência.  
  
## <a name="initialization-and-housekeeping-functions"></a>Funções de manutenção do sistema e de inicialização  
  
|Função|Descrição|  
|--------------|-----------------|  
|[SccCloseProject](../extensibility/scccloseproject-function.md)|Fecha um projeto.|  
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|Solicita ao usuário para as opções avançadas para o comando fornecido.|  
|[SccGetVersion](../extensibility/sccgetversion-function.md)|Retorna a versão do controle da fonte de plug-in.|  
|[SccInitialize](../extensibility/sccinitialize-function.md)|Inicializa o plug-in de controle de origem. Ele é chamado uma vez para cada instância do plug-in.|  
|[SccOpenProject](../extensibility/sccopenproject-function.md)|Abre um projeto.|  
|[SccSetOption](../extensibility/sccsetoption-function.md)|Uma função genérica usada para definir uma ampla variedade de opções. Cada opção inicia com `SCC_OPT_xxx` e tem seu próprio conjunto definido de valores.|  
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|Chamado uma vez quando um plug-in de controle de origem precisa ser desconectado.|  
  
## <a name="core-source-control-functions"></a>Principais funções de controle de origem  
  
|Função|Descrição|  
|--------------|-----------------|  
|[SccAdd](../extensibility/sccadd-function.md)|Adiciona uma matriz de arquivos especificados por nomes de caminho totalmente qualificado para o sistema de controle de origem.|  
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|Permite que o usuário procurar arquivos que já estão no sistema de controle de origem e, em seguida, fazer parte desses arquivos do projeto atual.|  
|[SccCheckin](../extensibility/scccheckin-function.md)|Verifica em uma matriz de arquivos.|  
|[SccCheckout](../extensibility/scccheckout-function.md)|Check-out de uma matriz de arquivos.|  
|[SccDiff](../extensibility/sccdiff-function.md)|Mostra as diferenças entre o arquivo do usuário local especificado por um nome de caminho totalmente qualificado e a versão no controle de origem.|  
|[SccGet](../extensibility/sccget-function.md)|Recupera uma cópia somente leitura de um conjunto de arquivos.|  
|[SccGetEvents](../extensibility/sccgetevents-function.md)|Verifica o status de arquivos que o chamador solicitou sobre (via `SccQueryInfo`).|  
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|Faz com que o plug-in para solicitar ao usuário para um caminho de projeto que seja significativo para o plug-in de controle de origem.|  
|[SccHistory](../extensibility/scchistory-function.md)|Mostra o histórico para uma matriz de nomes de arquivo local totalmente qualificado.|  
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|Examina a lista de arquivos para o seu status atual. Além disso, usa o `pfnPopulate` função para notificar o chamador quando um arquivo não corresponde aos critérios para o `nCommand`.|  
|[SccProperties](../extensibility/sccproperties-function.md)|Mostra as propriedades de um arquivo totalmente qualificado.|  
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|Examina uma lista de arquivos totalmente qualificados para o seu status atual.|  
|[SccRemove](../extensibility/sccremove-function.md)|Remove a matriz de arquivos totalmente qualificados do sistema de controle de origem.|  
|[SccRename](../extensibility/sccrename-function.md)|Renomeia o arquivo fornecido para um novo nome no sistema de controle de origem.|  
|[SccRunScc](../extensibility/sccrunscc-function.md)|Acessa a gama completa de recursos do sistema de controle do código-fonte.|  
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|Desfaz um check-out de um conjunto de arquivos.|  
  
## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>Funções que oferecem suporte à capacidade adicional (versão 1.2 da API de plug-in de controle de origem)  
 Esse grupo de funções define a funcionalidade adicional incluída na versão 1.2 da API de plug-in de controle de origem. Eles fornecem acesso a recursos de controle de origem e os recursos mais avançados.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|Inicia uma operação em lote.|  
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|Cria um subprojeto com o nome especificado em um projeto existente do pai.|  
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|Mostra as diferenças entre o diretório do usuário local especificado por um nome de caminho totalmente qualificado e o local de banco de dados de controle de origem.|  
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|Examina uma lista de diretórios totalmente qualificados para o seu status atual.|  
|[SccEndBatch](../extensibility/sccendbatch-function.md)|Termina uma operação em lote.|  
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|Retorna pai caminho do projeto fornecido (o projeto deve existir).|  
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|Verifica se vários check-outs em um arquivo são permitidos.|  
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|Verifica se o plug-in criará MSSCCPRJ. Arquivos SCC.|  
  
## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>Funções que oferecem suporte a recursos avançados (versão 1.3 da API de plug-in de controle de origem)  
 Esse grupo de funções define a funcionalidade adicional incluída na versão 1.3 da API de plug-in de controle de origem. Eles fornecem acesso a recursos de controle de origem e os recursos mais avançados.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|Adiciona uma lista de arquivos do controle de origem para o projeto atual.|  
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|Recupera uma lista de arquivos do controle de origem sem uma interface do usuário.|  
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|Recupera uma lista de arquivos no controle de origem que são diferentes dos arquivos locais.|  
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|Recupera os sinalizadores que especificam os recursos estendidos com suporte de plug-in de controle de origem.|  
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|Recupera as opções específicas do usuário.|  
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|Examina uma lista de diretórios e arquivos em um projeto ou projetos que estão sob o controle de origem. Cada nome de diretório e arquivo encontrado é passado para uma função de retorno de chamada.|  
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|Examina as alterações de nome a uma lista de arquivos. Cada nome de arquivo é passado para uma função de retorno de chamada com o status da alteração.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: scc.h  
  
 (Fornecido no SDK do ambiente comum inclui pasta, por padrão *[unidade]* \Program Files\VSIP 8.0\EnvSDK\common\inc; também é fornecido na pasta com o exemplo de MSSCCI VSIP *[unidade]* \Program Files\VSIP 8.0\MSSCCI).  
  
## <a name="see-also"></a>Consulte também  
 [Plug-ins de controle de origem](../extensibility/source-control-plug-ins.md)   
 [Criar um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)