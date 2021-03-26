---
title: Provedor de símbolos | Microsoft Docs
description: Saiba mais sobre os provedores de símbolos que o Visual Studio fornece para habilitar um avaliador de expressão para avaliar variáveis e expressões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 132e3c15eed86c9008e49b74b6da6e5da5a3ce33
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079378"
---
# <a name="symbol-provider"></a>Provedor de símbolos
Uma implementação do avaliador de expressão deve acessar as informações de depuração simbólicas geradas pelo compilador de linguagem para avaliar variáveis e expressões. Ele faz isso consumindo as interfaces de um provedor de símbolo (SP), também chamado de manipulador de símbolo.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece o SPs para código gerenciado, bem como código nativo usando o formato de arquivo de símbolo do banco de dados do programa (PDB). A menos que haja uma forte necessidade de o programa usar símbolos armazenados em um formato personalizado, é recomendável que você use os SPs fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="implementation-notes"></a>Notas de implementação
 Os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] mecanismos de depuração esperam se comunicar com o SPS usando interfaces CLR (Common Language Runtime). Como resultado, um SP que estará trabalhando com os mecanismos de depuração do Visual Studio deve dar suporte ao CLR. Uma lista completa de todas as interfaces de depuração CLR pode ser encontrada em debugref.doc, que faz parte do [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] .

 Se o SP estiver funcionando apenas com o mecanismo de depuração personalizado, você poderá implementar o SP, como se desejar, dependendo das necessidades do mecanismo de depuração.

## <a name="see-also"></a>Confira também
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
