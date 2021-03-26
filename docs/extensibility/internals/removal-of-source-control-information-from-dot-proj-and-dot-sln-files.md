---
title: Remover informações de controle do código-fonte de arquivos. proj e. sln
description: Na API de plug-in de controle do código-fonte, as informações de SCC são armazenadas em um MSSCCPRJ. Arquivo SCC em vez dos arquivos de projeto e solução.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- source control plug-ins, .sln and .proj files
ms.assetid: 7b06883f-35de-41e2-9a9e-d3edba236f17
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5fd4b4f12ab819903408d4d895773664e892b3ac
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105069381"
---
# <a name="removal-of-source-control-information-from-proj-and-sln-files"></a>Remoção de informações de controle do código-fonte de arquivos. proj e. sln

Na versão 1,2 da API de plug-in de controle do código-fonte, as informações de SCC são armazenadas em um MSSCCPRJ. Arquivo SCC. A vantagem do MSSCCPRJ. O arquivo SCC é que as informações de SCC não são controladas pela origem, como estão nos arquivos. proj e. sln.

## <a name="version-12-changes"></a>Alterações da versão 1,2

 Em plug-ins de controle do código-fonte baseados na API de plug-in de controle do código-fonte versão 1,1, as informações sobre o controle do código-fonte são armazenadas nos arquivos do projeto (. proj) e da solução (. sln). O local do banco de dados das informações de controle do código-fonte é especificado pelo AuxPath, e o local específico dentro do banco de dados é especificado pelo ProjName. Esse comportamento pode causar problemas após as operações de ramificação, bifurcação ou cópia porque o ProjName normalmente seria inválido após qualquer uma dessas operações.

 Na API de plug-in de controle do código-fonte versão 1,1, o IDE usava arquivos ~ SAK para detectar se um plug-in tem suporte para o MSSCCPRJ. Método SCC de armazenar informações de controle do código-fonte. A API de plug-in de controle do código-fonte versão 1,2 fornece um novo recurso para detectar o suporte para MSSCCPRJ. Arquivo SCC sem usar um arquivo ~ SAK. Para obter mais informações, consulte [eliminação de ~ Sak arquivos](../../extensibility/internals/elimination-of-tilde-sak-files.md).

## <a name="see-also"></a>Confira também

- [Novidades na API do plug-in de controle do código-fonte versão 1.2](../../extensibility/internals/what-s-new-in-the-source-control-plug-in-api-version-1-2.md)
