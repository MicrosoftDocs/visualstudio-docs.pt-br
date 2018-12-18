---
title: Features1 do serviço de linguagem herdado | Microsoft Docs
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
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: bb66895066d0af1259c3509c40ec9fa4458e3f79
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51774038"
---
# <a name="legacy-language-service-features"></a>Recursos do serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um serviço de linguagem do framework (MPF) de pacote gerenciado pode dar suporte a um ou mais [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] recursos, como realce de sintaxe, IntelliSense e validação de ponto de interrupção. Cada recurso pode ser implementado independente dos outros, mas todos exigem um analisador e um scanner, exceto para o realce de sintaxe, que exige apenas um scanner.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Correspondência de chave em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a par de idiomas correspondente, também conhecido como correspondência de chaves.  
  
 [Comentar em código em um serviço de linguagem herdado](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a comentários ou remoção de comentários do código selecionado.  
  
 [Propriedades de documento personalizadas em um serviço de linguagem herdado](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a propriedades de documento que são inseridas em um arquivo de origem.  
  
 [Estruturar em tópico em um serviço de linguagem herdado](../../extensibility/internals/outlining-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte à estrutura de tópicos por meio da implementação de regiões ocultas.  
  
 [Reformatar o código em um serviço de linguagem herdado](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a reformatação de código.  
  
 [Suporte a snippets de código em um serviço de linguagem herdado](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a trechos de código, que são segmentos de código que são inseridos e podem ser editados.  
  
 [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)  
 Descreve o que é necessário para dar suporte a operação de informações de parâmetro do IntelliSense para exibir uma assinatura de método, como o método é digitado.  
  
 [Informações rápidas em um serviço de linguagem herdado](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a operação de informações rápidas do IntelliSense para exibir informações sobre um identificador.  
  
 [Preenchimento de membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a operação de preenchimento de membro IntelliSense para selecionar um membro de um namespace de uma lista.  
  
 [Preenchimento de palavra em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a operação do IntelliSense Complete Word para completar palavras parcialmente digitadas.  
  
 [Suporte a janela de automáticos em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)  
 Descreve o que pode fazer um serviço de linguagem para dar suporte a **automóveis** janela enquanto você está depurando.  
  
 [Suporte a barra de navegação em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)  
 Descreve como usar o **barra de navegação** na parte superior do modo de exibição do editor para fornecer uma navegação rápida em qualquer tipo ou membro no arquivo mostrado nesse modo de exibição...  
  
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a realce de sintaxe do código-fonte.  
  
 [Validar pontos de interrupção em um serviço de linguagem herdado](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)  
 Descreve o que pode fazer um serviço de linguagem para dar suporte a pontos de interrupção Validando fora de um depurador.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)  
 Descreve o analisador e scanner que são necessários para implementar todos os recursos de um serviço de linguagem que usa a estrutura de pacote gerenciado.  
  
 [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)  
 Descreve o que é necessário implementar um serviço de linguagem, usando o MPF.  
  
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)  
 Descreve as etapas necessárias para registrar um serviço de linguagem baseada em MPF com [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 [Usando o IntelliSense](../../ide/using-intellisense.md)  
 Explica como o IntelliSense torna as referências à linguagem fácil acesso.  
  
 [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)  
 Fornece informações sobre como usar a estrutura de pacote gerenciado (MPF) para implementar um serviço de linguagem completa no código gerenciado.

