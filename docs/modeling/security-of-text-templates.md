---
title: Segurança de modelos de texto
description: Saiba mais sobre modelos de segurança e texto, incluindo tópicos como código arbitrário e processadores de diretiva mal-intencionados.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, security
author: mgoertz-msft
ms.author: mgoertz
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0a740a6f7a4c532a61a5e412c94fa4321c5da707
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112385754"
---
# <a name="security-of-text-templates"></a>Segurança de modelos de texto
Os modelos de texto têm as seguintes preocupações de segurança:

- Os modelos de texto são vulneráveis a inserções de código arbitrárias.

- Se o mecanismo que o host usa para encontrar um processador de diretiva não for seguro, um processador de diretiva mal-intencionado poderá ser executado.

## <a name="arbitrary-code"></a>Código arbitrário
 Ao escrever um modelo, você pode colocar qualquer código dentro das \<# #> marcas. Isso permite que o código arbitrário seja executado de dentro de um modelo de texto.

 Certifique-se de obter modelos de fontes confiáveis. Certifique-se de avisar os usuários finais do seu aplicativo para não executar modelos que não são de fontes confiáveis.

## <a name="malicious-directive-processor"></a>Processador de diretiva mal-intencionada
 O mecanismo de modelo de texto interage com um host de transformação e um ou mais processadores de diretiva para transformar o texto do modelo em um arquivo de saída. Para obter mais informações, consulte [O processo de transformação modelo de texto](../modeling/the-text-template-transformation-process.md).

 Se o mecanismo que o host usa para encontrar um processador de diretiva não for seguro, ele correrá o risco de executar um processador de diretiva mal-intencionado. O processador de diretiva mal-intencionada pode fornecer código que é executado `FullTrust` no modo quando o modelo é executado. Se você criar um host de transformação de modelo de texto personalizado, deverá usar um mecanismo seguro, como o Registro, para que o mecanismo localize processadores de diretiva.
