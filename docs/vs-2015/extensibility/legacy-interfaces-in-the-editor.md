---
title: Interfaces herdadas no Editor | Microsoft Docs
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
- editors [Visual Studio SDK], legacy
ms.assetid: 741d45f5-0ea3-4614-972a-8728fe054e07
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 45c3de943a1716877fcf33af4d16fd163721d04b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737511"
---
# <a name="legacy-interfaces-in-the-editor"></a>Interfaces herdadas no Editor
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode acessar o editor do Visual Studio de interfaces herdadas. O SDK do Visual Studio inclui adaptadores conhecidos como *shims*, que permitem que essas interfaces interagir com o novo editor. No entanto, é recomendável que você atualize seu código herdado para usar o novo editor de API. Seu código terá um desempenho melhor e você pode usar as novas tecnologias, como o Windows Presentation Foundation (WPF) e o MEF Managed Extensibility Framework ().  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Adaptando um código herdado para o editor](../extensibility/adapting-legacy-code-to-the-editor.md)|Explica como adaptar o seu código para o novo editor.|  
|[Comportamento novo ou alterado com adaptadores de editor](../extensibility/new-or-changed-behavior-with-editor-adapters.md)|Explica como o comportamento dos adaptadores de editor difere das versões anteriores do editor.|  
|[Dentro do editor principal](../extensibility/inside-the-core-editor.md)|Descreve os diferentes componentes de versões anteriores do editor.|  
|[Criando uma instância do editor principal usando a API herdada](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md)|Explica como usar a API herdada para instanciar o editor de núcleo.|  
|[Fábricas de editor](../extensibility/editor-factories.md)|Explica como usar as fábricas de editor com a API herdada.|  
|[Como registrar tipos de arquivo do editor](../extensibility/how-to-register-editor-file-types.md)|Explica como vincular uma extensão de nome de arquivo para o seu editor.|  
|[Passo a passo: Criar um editor principal e registrar um tipo de arquivo do editor](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md)|Explica como criar um núcleo de editor e vinculá-lo uma extensão de nome de arquivo.|  
|[Como fornecer contexto para editores](../extensibility/how-to-provide-context-for-editors.md)|Explica como fornecer contexto para o seu editor.|  
|[Serviços de linguagem e o editor principal](../extensibility/language-services-and-the-core-editor.md)|Explica as interações entre um serviço de linguagem e um editor.|  
|[Acessando o buffer de texto usando a API herdada](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md)|Explica como acessar o buffer de texto usando a API herdada.|  
|[Acessando a exibição de texto usando a API herdada](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md)|Explica como acessar a exibição de texto usando a API herdada.|  
|[Personalizando janelas de código usando a API herdada](../extensibility/customizing-code-windows-by-using-the-legacy-api.md)|Explica como personalizar janelas de código usando a API herdada.|  
|[Acessando camadas de texto usando a API herdada](../extensibility/accessing-text-layers-by-using-the-legacy-api.md)|Explica como acessar diferentes camadas de texto usando a API herdada.|  
|[Usando marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md)|Explica como adicionar marcadores de texto usando a API herdada.|  
|[Personalizando menus e controles do editor usando a API herdada](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md)|Explica como personalizar controles de editor usando a API herdada.|  
|[Gerenciamento de desfazer e refazer, usando a API herdada](../extensibility/managing-undo-and-redo-by-using-the-legacy-api.md)|Explica como gerenciar desfazer e refazer, usando a API herdada.|  
|[Como implementar o mecanismo de localizar e substituir](../extensibility/how-to-implement-the-find-and-replace-mechanism.md)|Explica como gerenciar a localizar e substituir, usando a API herdada.|  
|[Como suprimir notificações de alteração de arquivo](../extensibility/how-to-suppress-file-change-notifications.md)|Explica como suprimir as notificações de alteração de arquivo usando a API herdada.|  
|[Criar designers e editores personalizados](../extensibility/creating-custom-editors-and-designers.md)|Explica como criar designers e editores personalizados.|  
|[Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)|Fornece links para documentos sobre os recursos que fornecem recursos de personalização para o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] editor de núcleo, adicionando suporte para um serviço de linguagem.|  
|[Usando fontes e cores](../extensibility/using-fonts-and-colors.md)|Explica como usar fontes e cores com interfaces legadas.|

