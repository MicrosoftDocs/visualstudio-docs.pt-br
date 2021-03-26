---
title: Funções da API de plug-in de controle do código-fonte | Microsoft Docs
description: Saiba mais sobre as funções que a API de plug-in de controle do código-fonte fornece, que deve ser implementada pelo plug-in de controle do código-fonte.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, functions
ms.assetid: 4b0536dd-4f92-4ef2-9031-4548281f37aa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c28c175d53fb37cf890dad4240a84fb132f6af35
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090116"
---
# <a name="source-control-plug-in-api-functions"></a>Funções de API de plug-in de controle do código-fonte
A API de plug-in de controle do código-fonte fornece as seguintes funções, que devem ser implementadas pelo plug-in de controle do código-fonte de acordo com essa API. As assinaturas de cada função e a semântica associada aos sinalizadores de bits e a outros parâmetros são descritas detalhadamente nessa referência.

## <a name="initialization-and-housekeeping-functions"></a>Funções de inicialização e manutenção

|Função|Descrição|
|--------------|-----------------|
|[SccCloseProject](../extensibility/scccloseproject-function.md)|Fecha um projeto.|
|[SccGetCommandOptions](../extensibility/sccgetcommandoptions-function.md)|Solicita ao usuário as opções avançadas para o comando fornecido.|
|[SccGetVersion](../extensibility/sccgetversion-function.md)|Retorna a versão do plug-in de controle do código-fonte.|
|[SccInitialize](../extensibility/sccinitialize-function.md)|Inicializa o plug-in de controle do código-fonte. Ele é chamado uma vez para cada instância do plug-in.|
|[SccOpenProject](../extensibility/sccopenproject-function.md)|Abre um projeto.|
|[SccSetOption](../extensibility/sccsetoption-function.md)|Uma função genérica usada para definir uma ampla variedade de opções. Cada opção começa com `SCC_OPT_xxx` e tem seu próprio conjunto definido de valores.|
|[SccUninitialize](../extensibility/sccuninitialize-function.md)|Chamado uma vez quando um plug-in de controle do código-fonte precisa ser desconectado.|

## <a name="core-source-control-functions"></a>Funções de controle do código-fonte principal

|Função|Descrição|
|--------------|-----------------|
|[SccAdd](../extensibility/sccadd-function.md)|Adiciona uma matriz de arquivos especificados por nomes de caminho totalmente qualificados ao sistema de controle do código-fonte.|
|[SccAddFromScc](../extensibility/sccaddfromscc-function.md)|Permite que o usuário procure arquivos que já estão no sistema de controle do código-fonte e, em seguida, torne esses arquivos parte do projeto atual.|
|[SccCheckin](../extensibility/scccheckin-function.md)|Faz o check-in de uma matriz de arquivos.|
|[SccCheckout](../extensibility/scccheckout-function.md)|Faz o check-out de uma matriz de arquivos.|
|[SccDiff](../extensibility/sccdiff-function.md)|Mostra as diferenças entre o arquivo do usuário local especificado por um nome de caminho totalmente qualificado e a versão no controle do código-fonte.|
|[SccGet](../extensibility/sccget-function.md)|Recupera uma cópia somente leitura de um conjunto de arquivos.|
|[SccGetEvents](../extensibility/sccgetevents-function.md)|Verifica o status dos arquivos sobre os quais o chamador pediu (via `SccQueryInfo` ).|
|[SccGetProjPath](../extensibility/sccgetprojpath-function.md)|Faz com que o plug-in de controle do código-fonte solicite ao usuário um caminho de projeto que seja significativo para o plug-in.|
|[SccHistory](../extensibility/scchistory-function.md)|Mostra o histórico de uma matriz de nomes de arquivos locais totalmente qualificados.|
|[SccPopulateList](../extensibility/sccpopulatelist-function.md)|Examina a lista de arquivos em busca de seu status atual. Além disso, o usa a `pfnPopulate` função para notificar o chamador quando um arquivo não corresponde aos critérios para o `nCommand` .|
|[SccProperties](../extensibility/sccproperties-function.md)|Mostra as propriedades de um arquivo totalmente qualificado.|
|[SccQueryInfo](../extensibility/sccqueryinfo-function.md)|Examina uma lista de arquivos totalmente qualificados para seu status atual.|
|[SccRemove](../extensibility/sccremove-function.md)|Remove a matriz de arquivos totalmente qualificados do sistema de controle do código-fonte.|
|[SccRename](../extensibility/sccrename-function.md)|Renomeia o arquivo fornecido com um novo nome no sistema de controle do código-fonte.|
|[SccRunScc](../extensibility/sccrunscc-function.md)|Acessa a gama completa de recursos do sistema de controle do código-fonte.|
|[SccUncheckout](../extensibility/sccuncheckout-function.md)|Desfaz um check-out de uma matriz de arquivos.|

## <a name="functions-that-support-additional-capability-version-12-of-the-source-control-plug-in-api"></a>Funções que dão suporte a recursos adicionais (versão 1,2 da API de plug-in de controle do código-fonte)
 Esse grupo de funções define a funcionalidade adicional incluída na versão 1,2 da API de plug-in de controle do código-fonte. Eles fornecem acesso a recursos e recursos de controle do código-fonte mais avançados.

|Função|Descrição|
|--------------|-----------------|
|[SccBeginBatch](../extensibility/sccbeginbatch-function.md)|Inicia uma operação em lote.|
|[SccCreateSubProject](../extensibility/scccreatesubproject-function.md)|Cria um subprojeto com o nome fornecido em um projeto pai existente.|
|[SccDirDiff](../extensibility/sccdirdiff-function.md)|Mostra as diferenças entre o diretório do usuário local especificado por um nome de caminho totalmente qualificado e o local do banco de dados de controle do código-fonte.|
|[SccDirQueryInfo](../extensibility/sccdirqueryinfo-function.md)|Examina uma lista de diretórios totalmente qualificados para seu status atual.|
|[SccEndBatch](../extensibility/sccendbatch-function.md)|Finaliza uma operação em lote.|
|[SccGetParentProjectPath](../extensibility/sccgetparentprojectpath-function.md)|Retorna o caminho pai do projeto fornecido (o projeto deve existir).|
|[SccIsMultiCheckoutEnabled](../extensibility/sccismulticheckoutenabled-function.md)|Verifica se vários check-outs em um arquivo são permitidos.|
|[SccWillCreateSccFile](../extensibility/sccwillcreatesccfile-function.md)|Verifica se o plug-in criará MSSCCPRJ. Arquivos SCC.|

## <a name="functions-that-support-advanced-capability-version-13-of-the-source-control-plug-in-api"></a>Funções que dão suporte à funcionalidade avançada (versão 1,3 da API de plug-in de controle do código-fonte)
 Esse grupo de funções define a funcionalidade adicional incluída na versão 1,3 da API de plug-in de controle do código-fonte. Eles fornecem acesso a recursos e recursos de controle do código-fonte mais avançados.

|Função|Descrição|
|--------------|-----------------|
|[SccAddFilesFromSCC](../extensibility/sccaddfilesfromscc-function.md)|Adiciona uma lista de arquivos do controle do código-fonte ao projeto atual.|
|[SccBackgroundGet](../extensibility/sccbackgroundget-function.md)|Recupera uma lista de arquivos do controle do código-fonte sem uma interface do usuário.|
|[SccEnumChangedFiles](../extensibility/sccenumchangedfiles-function.md)|Recupera uma lista de arquivos no controle do código-fonte que são diferentes dos arquivos locais.|
|[SccGetExtendedCapabilities](../extensibility/sccgetextendedcapabilities-function.md)|Recupera sinalizadores que especificam funcionalidades estendidas com suporte pelo plug-in de controle do código-fonte.|
|[SccGetUserOption](../extensibility/sccgetuseroption-function.md)|Recupera opções específicas do usuário.|
|[SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md)|Examina uma lista de diretórios e arquivos em um projeto ou projetos que estão sob controle do código-fonte. Cada diretório e nome de arquivo encontrados é passado para uma função de retorno de chamada.|
|[SccQueryChanges](../extensibility/sccquerychanges-function.md)|Examina as alterações de nome feitas em uma lista de arquivos. Cada nome de arquivo é passado para uma função de retorno de chamada com seu status de alteração.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: SCC. h

 (Fornecido no SDK do ambiente, o inclui a pasta, por padrão *[unidade]* \Program Files\VSIP 8.0 \ EnvSDK\common\inc; também fornecida na pasta VSIP com o exemplo MSSCCI, *[unidade]* \Arquivos de Files\VSIP \ MSSCCI).

## <a name="see-also"></a>Confira também
- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md)
- [Criando um plug-in de controle do código-fonte](../extensibility/internals/creating-a-source-control-plug-in.md)
