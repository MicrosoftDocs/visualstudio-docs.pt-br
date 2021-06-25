---
title: Provedor de Símbolos | Microsoft Docs
description: Saiba mais sobre os provedores de símbolos Visual Studio fornece para habilitar um avaliador de expressão a avaliar variáveis e expressões.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- symbol handler
- debugging [Debugging SDK], symbol handler
ms.assetid: 5fce651b-fead-4418-81b0-a011df7644ab
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3332bbf705d8e3149d864dbb35418fd4c12c523b
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112902911"
---
# <a name="symbol-provider"></a>Provedor de símbolos
Uma implementação do avaliador de expressão deve acessar as informações de depuração simbólicas geradas pelo compilador de linguagem para avaliar variáveis e expressões. Ele faz isso consumindo as interfaces de um SP (provedor de símbolos), também chamado de manipulador de símbolos.

 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] fornece SPs para código gerenciado, bem como código nativo usando o formato de arquivo de símbolo PDB (Program DataBase). A menos que haja uma necessidade forte de seu programa usar símbolos armazenados em um formato personalizado, é recomendável usar os SPs fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="implementation-notes"></a>Notas de implementação
 Os mecanismos de depuração esperam conversar com os SPs usando [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] interfaces CLR (Common Language Runtime). Como resultado, um SP que trabalhará com o Visual Studio de depuração deve dar suporte ao CLR. Uma lista completa de todas as interfaces de depuração CLR pode ser encontrada debugref.doc, que faz parte do [!INCLUDE[winsdklong](../../deployment/includes/winsdklong_md.md)] .

 Se o SP estiver funcionando apenas com o mecanismo de depuração personalizado, você poderá implementar o SP como quiser, dependendo das necessidades do mecanismo de depuração.

## <a name="see-also"></a>Confira também
- [Componentes do depurador](../../extensibility/debugger/debugger-components.md)
