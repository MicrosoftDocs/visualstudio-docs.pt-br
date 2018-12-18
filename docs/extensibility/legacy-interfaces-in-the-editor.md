---
title: Interfaces herdadas no Editor | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy
ms.assetid: 741d45f5-0ea3-4614-972a-8728fe054e07
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e5fdabadc1c3a0b5deda42aa268607e0f764e9b7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849925"
---
# <a name="legacy-interfaces-in-the-editor"></a>Interfaces herdadas no editor
Você pode acessar o editor do Visual Studio de interfaces herdadas. O SDK do Visual Studio inclui adaptadores conhecidos como *shims*, que permitem que essas interfaces interagir com o novo editor. No entanto, é recomendável que você atualize seu código herdado para usar o novo editor de API. Seu código terá um desempenho melhor e você pode usar as novas tecnologias, como o Windows Presentation Foundation (WPF) e o MEF Managed Extensibility Framework ().  

## <a name="related-topics"></a>Tópicos relacionados  

| Título | Descrição |
| - | - |
| [Adaptar o código herdado para o editor](../extensibility/adapting-legacy-code-to-the-editor.md) | Explica como adaptar o seu código para o novo editor. |
| [Comportamento de novo ou alterado com adaptadores de editor](../extensibility/new-or-changed-behavior-with-editor-adapters.md) | Explica como o comportamento dos adaptadores de editor difere das versões anteriores do editor. |
| [Dentro do editor de núcleo](../extensibility/inside-the-core-editor.md) | Descreve os diferentes componentes de versões anteriores do editor. |
| [Criar uma instância o editor principal usando a API herdada](../extensibility/instantiating-the-core-editor-by-using-the-legacy-api.md) | Explica como usar a API herdada para instanciar o editor de núcleo. |
| [Fábricas de editor](../extensibility/editor-factories.md) | Explica como usar as fábricas de editor com a API herdada. |
| [Como: registrar os tipos de arquivo do editor](../extensibility/how-to-register-editor-file-types.md) | Explica como vincular uma extensão de nome de arquivo para o seu editor. |
| [Passo a passo: Criar um núcleo de editor e registrar um tipo de arquivo do editor](../extensibility/walkthrough-creating-a-core-editor-and-registering-an-editor-file-type.md) | Explica como criar um núcleo de editor e vinculá-lo uma extensão de nome de arquivo. |
| [Como: fornecer contexto para editores](../extensibility/how-to-provide-context-for-editors.md) | Explica como fornecer contexto para o seu editor. |
| [Serviços de linguagem e o editor de núcleo](../extensibility/language-services-and-the-core-editor.md) | Explica as interações entre um serviço de linguagem e um editor. |
| [Acessar o buffer de texto, usando a API herdada](../extensibility/accessing-the-text-buffer-by-using-the-legacy-api.md) | Explica como acessar o buffer de texto usando a API herdada. |
| [Exibição de theText de acesso usando a API herdada](../extensibility/accessing-thetext-view-by-using-the-legacy-api.md) | Explica como acessar a exibição de texto usando a API herdada. |
| [Personalizar janelas de código usando a API herdada](../extensibility/customizing-code-windows-by-using-the-legacy-api.md) | Explica como personalizar janelas de código usando a API herdada. |
| [Camadas de texto de acesso usando a API herdada](../extensibility/accessing-text-layers-by-using-the-legacy-api.md) | Explica como acessar diferentes camadas de texto usando a API herdada. |
| [Usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md) | Explica como adicionar marcadores de texto usando a API herdada. |
| [Personalizar menus e controles de editor usando a API herdada](../extensibility/customizing-editor-controls-and-menus-by-using-the-legacy-api.md) | Explica como personalizar controles de editor usando a API herdada. |
| [Gerenciar desfazer e refazer, usando a API herdada](../extensibility/managing-undo-and-redo-by-using-the-legacy-api.md) | Explica como gerenciar desfazer e refazer, usando a API herdada. |
| [Como: implementar o localizar e substituir o mecanismo](../extensibility/how-to-implement-the-find-and-replace-mechanism.md) | Explica como gerenciar a localizar e substituir, usando a API herdada. |
| [Como: suprimir notificações de alteração de arquivo](../extensibility/how-to-suppress-file-change-notifications.md) | Explica como suprimir as notificações de alteração de arquivo usando a API herdada. |
| [Criar designers e editores personalizados](../extensibility/creating-custom-editors-and-designers.md) | Explica como criar designers e editores personalizados. |
| [Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md) | Fornece links para documentos sobre os recursos que fornecem recursos de personalização para o [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] editor de núcleo, adicionando suporte para um serviço de linguagem. |
| [Use fontes e cores](../extensibility/using-fonts-and-colors.md) | Explica como usar fontes e cores com interfaces legadas. |

