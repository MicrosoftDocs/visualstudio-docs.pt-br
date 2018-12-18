---
title: Segurança
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- code access security, coding errors
- security [.NET Framework], about security
ms.assetid: 318c34ce-f643-468c-83a1-843196f5d845
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ae5db15fda1914d52be192a516d70704d2ad3cf6
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53061740"
---
# <a name="security-in-visual-studio"></a>Segurança no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você deve considerar a segurança em todos os aspectos do desenvolvimento do aplicativo, do design à implantação. Comece executando o Visual Studio com a máxima segurança possível. Consulte [Permissões de usuário](../ide/user-permissions-and-visual-studio.md).

 Para que você desenvolva aplicativos efetivamente seguros, é preciso ter um entendimento básico dos conceitos e dos recursos de segurança das plataformas para as quais você está desenvolvendo. Também é preciso entender as técnicas de codificação segura.

## <a name="understanding-security"></a>Noções básicas de segurança
 [Segurança](http://msdn.microsoft.com/library/9a9621d7-8883-4a4f-a874-65e8e09e20a6) Descreve a segurança de acesso do código, a segurança baseada em função, a política de segurança e as ferramentas de segurança do .NET Framework.

 [Defend Your Code with Top Ten Security Tips Every Developer Must Know (Proteja seu código com as dez principais dicas de segurança que todo desenvolvedor precisa saber)](http://go.microsoft.com/fwlink/?LinkId=72877) Descreve os problemas que você precisa observar para que eles não comprometam os dados ou o sistema.

## <a name="coding-for-security"></a>Codificação de segurança
 A maioria dos erros de codificação resulta em vulnerabilidades de segurança que ocorrem porque os desenvolvedores fazem suposições incorretas ao trabalhar com a entrada do usuário ou porque eles não entendem completamente a plataforma para a qual estão desenvolvendo.

 [Diretrizes de codificação segura](http://msdn.microsoft.com/library/4f882d94-262b-4494-b0a6-ba9ba1f5f177) fornece diretrizes para a classificação de componentes para solucionar problemas de segurança.

 [Práticas recomendadas de segurança](http://msdn.microsoft.com/library/86acaccf-cdb4-4517-bd58-553618e3ec42) aborda estouros de buffer e a visão completa do recurso de verificação de segurança do Microsoft Visual C++ fornecido pelo sinalizador de tempo de compilação /GS.
