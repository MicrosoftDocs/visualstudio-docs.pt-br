---
title: O comando DslTextTransform
description: Saiba que DslTextTransform.cmd é um script que chama TextTransform.exe e o executa com opções comuns.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, commands
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 65d1e1d02c5b7d13c2e86343c6307306542d00e2
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112388640"
---
# <a name="the-dsltexttransform-command"></a>O comando DslTextTransform
DslTextTransform.cmd é um script que chama TextTransform.exe e o executa com opções comuns. Você pode usar DslTextTransformation.cmd para automatizar um build noturno de seus [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] projetos. Para obter mais informações, [consulte Gerando arquivos com o utilitário TextTransform](../modeling/generating-files-with-the-texttransform-utility.md).

 DslTextTransform.cmd está localizado no seguinte diretório:

 **\<Visual Studio SDK Installation Path>\VisualStudioIntegration\Tools\Bin**

 Você pode especificar os seguintes argumentos como entrada para DslTextTransform.cmd:

- O diretório de saída do projeto de modelo de domínio.

- O diretório de saída do projeto de definição do designer.

- O local do arquivo de modelo de texto.

  DslTextTransform.cmd processa o arquivo de modelo de texto especificado usando os assemblies e processadores de diretiva padrão. Se você criar processadores de diretiva personalizados, poderá criar seu próprio arquivo em lotes que chama TextTransform.exe. Nesse arquivo em lotes, você pode especificar seus assemblies e os processadores de diretiva personalizados associados.
