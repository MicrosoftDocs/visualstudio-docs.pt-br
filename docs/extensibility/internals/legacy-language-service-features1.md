---
title: Linguagem herdada serviço Features1 | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework]
ms.assetid: a646e4f0-767d-4cd1-8e1a-9a2aa210a1b7
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0c931147d20454a920e20cec61e1f6000a9b043d
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131724"
---
# <a name="legacy-language-service-features"></a>Recursos de serviço de linguagem herdada
Um serviço de idioma do pacote gerenciado framework (MPF) pode dar suporte a um ou mais [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] recursos, como o realce de sintaxe, IntelliSense e validação de ponto de interrupção. Cada recurso pode ser implementado independente dos outros, mas exigem um analisador e um scanner, exceto de realce de sintaxe, que exige apenas um scanner.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Correspondência de chave em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte ao par de idioma correspondente, também conhecido como correspondência de chaves.  
  
 [Comentar em código em um serviço de linguagem herdado](../../extensibility/internals/commenting-code-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a comentários e removendo marca de comentário do código selecionado.  
  
 [Propriedades de documento personalizadas em um serviço de linguagem herdado](../../extensibility/internals/custom-document-properties-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a propriedades de documento que são inseridas em um arquivo de origem.  
  
 [Estruturar em tópico em um serviço de linguagem herdado](../../extensibility/internals/outlining-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a estrutura de tópicos por meio da implementação de regiões ocultas.  
  
 [Reformatar o código em um serviço de linguagem herdado](../../extensibility/internals/reformatting-code-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a reformatação de código.  
  
 [Suporte a trechos de código em um serviço de linguagem herdado](../../extensibility/internals/support-for-code-snippets-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte a trechos de código, que são segmentos de código que são inseridos e podem ser editados.  
  
 [Informações de parâmetro em um serviço de linguagem herdado](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)  
 Descreve o que é necessário para dar suporte à operação de informações de parâmetro do IntelliSense para exibir uma assinatura de método, como o método é digitado.  
  
 [Informações rápidas em um serviço de linguagem herdado](../../extensibility/internals/quick-info-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte à operação de informações rápidas do IntelliSense para exibir informações sobre um identificador.  
  
 [Preenchimento de membro em um serviço de linguagem herdado](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte à operação de conclusão de membro do IntelliSense para selecionar um membro de um namespace de uma lista.  
  
 [Preenchimento de palavra em um serviço de linguagem herdado](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte à operação IntelliSense Complete Word para concluir palavras parcialmente digitadas.  
  
 [Suporte a janela de automáticos em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-autos-window-in-a-legacy-language-service.md)  
 Descreve o que pode fazer um serviço de linguagem para dar suporte a **Autos** janela enquanto você está depurando.  
  
 [Suporte a barra de navegação em um serviço de linguagem herdado](../../extensibility/internals/support-for-the-navigation-bar-in-a-legacy-language-service.md)  
 Descreve como usar o **barra de navegação** na parte superior do modo de exibição de editor para fornecer uma navegação rápida a qualquer tipo ou membro do arquivo mostrado no modo de exibição.  
  
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)  
 Descreve o que é necessário para dar suporte ao realce de sintaxe do código-fonte.  
  
 [Validar pontos de interrupção em um serviço de linguagem herdado](../../extensibility/internals/validating-breakpoints-in-a-legacy-language-service.md)  
 Descreve o que pode fazer um serviço de linguagem para dar suporte a pontos de interrupção validação fora de um depurador.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)  
 Descreve o analisador e o scanner que são necessários para implementar todos os recursos de um serviço de linguagem que usa a estrutura de pacote gerenciado.  
  
 [Implementar um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service2.md)  
 Descreve o que é necessário para implementar um serviço de idioma usando MPF.  
  
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)  
 Descreve as etapas necessárias para registrar um serviço de linguagem baseada em MPF com [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
 [Usando o IntelliSense](../../ide/using-intellisense.md)  
 Explica como IntelliSense facilita a referências de linguagem acessar.  
  
 [Implementar um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)  
 Fornece informações sobre como usar a estrutura de pacote gerenciado (MPF) para implementar um serviço de linguagem completos em código gerenciado.