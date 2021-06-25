---
title: Funções de retorno de chamada implementadas pelo IDE | Microsoft Docs
description: Saiba mais sobre as funções de retorno de chamada que o plug-in pode chamar em momentos apropriados durante uma operação de controle do código-fonte para passar informações para o IDE.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- source control plug-ins, callback functions
- callback functions, source control plug-ins
ms.assetid: 4a8833f0-6ac0-4ea7-9400-8275aa991468
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 78ce3a9cdd183cff0518ee3c6da9326c63297a85
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899141"
---
# <a name="callback-functions-implemented-by-the-ide"></a>Funções de retorno de chamada implementadas pelo IDE
Para tornar a integração com o IDE (ambiente de desenvolvimento integrado) o mais simples possível e para fornecer uma experiência unificada do usuário final, o plug-in de controle do código-fonte pode usar funções de retorno de chamada que são implementadas pelo IDE. O plug-in pode chamar essas funções em momentos apropriados durante uma operação de controle do código-fonte para passar informações para o IDE; o IDE pode exibir essas informações como elementos incorporados em sua interface do usuário nativa. O usuário tem uma experiência menos fragmentada nesse cenário do que se o plug-in empregasse sua própria interface do usuário.

 O arquivo de cabeçalho necessário é *SCC. h*. O local padrão é *\Program Files\VSIP 8.0 \ EnvSDK\common\inc \\*. Também está na pasta VSIP que tem a amostra de plug-in de controle do código-fonte em *\Program Files\VSIP \\ 8.0 \ MSSCCI*.

## <a name="in-this-section"></a>Nesta seção
- [LPTEXTOUTPROC](../extensibility/lptextoutproc.md) Descreve a função de retorno de chamada usada pelo [SccOpenProject](../extensibility/sccopenproject-function.md) para exibir mensagens do plug-in de controle do código-fonte por meio do IDE.

- [POPLISTFUNC](../extensibility/poplistfunc.md) Descreve a função de retorno de chamada que é usada pelo [SccPopulateList](../extensibility/sccpopulatelist-function.md) quando o IDE não tem acesso completo a informações disponíveis somente para o plug-in de controle do código-fonte, como uma lista completa de arquivos sob controle de versão.

- [QUERYCHANGESFUNC](../extensibility/querychangesfunc.md) Descreve a função de retorno de chamada que é usada pela operação [SccQueryChanges](../extensibility/sccquerychanges-function.md) .

- [POPDIRLISTFUNC](../extensibility/popdirlistfunc.md) Descreve a função de retorno de chamada que é usada pela operação [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) .

- [OPTNAMECHANGEPFN](../extensibility/optnamechangepfn.md) Descreve a função callback definida por uma chamada para o [SccSetOption](../extensibility/sccsetoption-function.md) que permite que o plug-in de controle do código-fonte comunique as alterações de nome de volta para o IDE.

## <a name="related-sections"></a>Seções relacionadas
- [SccOpenProject](../extensibility/sccopenproject-function.md) Abre um projeto.

- [SccPopulateList](../extensibility/sccpopulatelist-function.md) Examina a lista de arquivos em busca de seu status atual. Além disso, o usa a `pfnPopulate` função para notificar o chamador quando um arquivo não corresponde aos critérios para o `nCommand` .

- [SccPopulateDirList](../extensibility/sccpopulatedirlist-function.md) Examina uma lista de diretórios e arquivos em um projeto ou projetos que estão sob controle do código-fonte. Cada diretório e nome de arquivo encontrados é passado para uma função de retorno de chamada.

- [SccQueryChanges](../extensibility/sccquerychanges-function.md) Examina as alterações de nome que foram feitas em uma lista de arquivos. Cada nome de arquivo é passado para uma função de retorno de chamada junto com seu status de alteração.

- [SccSetOption](../extensibility/sccsetoption-function.md) Define uma ampla variedade de opções. Cada opção começa com `SCC_OPT_xxx` e tem seu próprio conjunto definido de valores.

- [Plug-ins de controle do código-fonte](../extensibility/source-control-plug-ins.md) Descreve o conteúdo da seção de referência do SDK de plug-in de controle do código-fonte.
