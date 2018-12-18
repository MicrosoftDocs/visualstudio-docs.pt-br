---
title: Introdução à extensibilidade do depurador | Microsoft Docs
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
- getting started, Debugging SDK
- debugging [Debugging SDK], getting started
- Debugging SDK, getting started
ms.assetid: d6ce6f43-1409-4bf7-93cd-f3464ca23504
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bafdd45b57a9fe660e97127c2c99c333ead0e60a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51721169"
---
# <a name="getting-started-with-debugger-extensibility"></a>Introdução à extensibilidade do depurador
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] fornece as informações que você deve ter para criar e personalizar componentes do depurador usados para depurar programas de dentro do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração adicionou melhorias derivadas a usabilidade extenso teste realizado no anterior [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuradores. Você pode usar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração para percorrer um aplicativo de vários idioma, ou você pode implementar em interrupções de edição de variáveis durante a depuração de aplicativos e soluções de vários idiomas.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração é executada fora do processo com o programa que está sendo depurado e, portanto, é menos intrusiva no espaço de processo do aplicativo. Consequentemente, é mais fácil escrever componentes que interagem com o depurador sem afetar o seu programa de depuração.  
  
 Usar melhor o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)], você deve estar familiarizado com o seguinte:  
  
-   O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE)  
  
-   A linguagem de programação do C++  
  
-   COM ATL  
  
## <a name="in-this-section"></a>Nesta seção  
 [Roteiro para estender o depurador](../../extensibility/debugger/roadmap-for-extending-the-debugger.md)  
 Descreve o processo de implementação de depuração no seu produto, dependendo do seu compilador e sua saída.  
  
 [Componentes do depurador](../../extensibility/debugger/debugger-components.md)  
 Fornece uma visão geral de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração componentes, que incluem o mecanismo de depuração (DE), o avaliador de expressão (EE) e o manipulador de símbolo (SH).  
  
 [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)  
 Descreve os principais conceitos de arquiteturas de depuração.  
  
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)  
 Explica como o mecanismo de depuração (DES) simultaneamente opera dentro do código, documentação e contextos de avaliação de expressão. Descreve, para cada um dos três contextos, a localização, posição ou avaliação relevante a ele.  
  
 [Tarefas de depuração](../../extensibility/debugger/debugging-tasks.md)  
 Contém links para várias tarefas de depuração, como iniciar um programa e avaliar expressões.

