---
title: Incorporação simplificada | Microsoft Docs
description: Saiba mais sobre inserção simplificada, que pode ser habilitada em um editor quando seu objeto de exibição de documento é um filho do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dca3b0c11c916a1fc47e4687bfeeabee35bcdfb4
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105056370"
---
# <a name="simplified-embedding"></a>Incorporação simplificada
A incorporação simplificada é habilitada em um editor quando seu objeto de exibição de documento é pai de (ou seja, tornou-se um filho de) [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e a <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface é implementada para manipular seus comandos de janela. Editores de inserção simplificados não podem hospedar controles ativos. Os objetos usados para criar um editor com inserção simplificada são mostrados na ilustração a seguir.

 ![Gráfico do editor de inserção simplificado](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor") Editor com incorporação simplificada

> [!NOTE]
> Dos objetos nesta ilustração, somente o `CYourEditorFactory` objeto é necessário para criar um editor padrão baseado em arquivo. Se você estiver criando um editor personalizado, não precisará implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2> , porque seu editor provavelmente terá seu próprio mecanismo de persistência privada. No entanto, para editores não personalizados, você deve fazer isso.

 Todas as interfaces implementadas para criar um editor com incorporação simplificada estão contidas no `CYourEditorDocument` objeto. No entanto, para dar suporte a várias exibições de dados de documento, divida as interfaces em dados separados e exiba objetos conforme indicado na tabela a seguir.

|Interface|Local da interface|Uso|
|---------------|---------------------------|---------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|Visualizar|Fornece conexão com a janela pai.|
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Visualizar|Manipula comandos.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|Visualizar|Habilita atualizações da barra de status.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|Visualizar|Habilita itens da **caixa de ferramentas** .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|Dados|Envia notificações quando o arquivo é alterado.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Dados|Habilita o recurso salvar como para um tipo de arquivo.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|Dados|Habilita a persistência para o documento.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|Dados|Permite a supressão de eventos de alteração de arquivo, como o disparo de recarregamento.|
