---
title: Simplificado inserindo | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - simple view embedding
ms.assetid: f1292478-a57d-48ec-8c9e-88a23f04ffe5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 01b06a0a63059c39035d15221feb201d3674d4a7
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31142926"
---
# <a name="simplified-embedding"></a>Simplificado inserindo
Inserindo simplificada é habilitado em um editor quando seu objeto de exibição do documento é pai (ou seja, feitas filho) [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> interface é implementada para lidar com seus comandos de janela. Editores de incorporação simplificados não podem hospedar controles ativos. Os objetos usados para criar um editor com inserção simplificada são mostrados na ilustração a seguir.  
  
 ![Gráfico do Editor de inserção simplificado](../extensibility/media/vssimplifiedembeddingeditor.gif "vsSimplifiedEmbeddingEditor")  
Editor de inserção simplificada  
  
> [!NOTE]
>  Os objetos nesta ilustração, somente o `CYourEditorFactory` objeto é necessária para criar um editor padrão com base em arquivo. Se você estiver criando um editor personalizado, não são necessários para implementar <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>, porque seu editor provavelmente terá seu próprio mecanismo de persistência privada. Para editores não personalizado, no entanto, você deve fazer isso.  
  
 Todas as interfaces implementadas para criar um editor com inserção simplificada estão contidas no `CYourEditorDocument` objeto. No entanto, para dar suporte a vários modos de exibição de dados de documentos, divida as interfaces para objetos de dados e exibir separados conforme indicado na tabela a seguir.  
  
|Interface|Local da interface|Use|  
|---------------|---------------------------|---------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|Exibir|Fornece a conexão para a janela pai.|  
|<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>|Exibir|Controla os comandos.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsStatusbarUser>|Exibir|Permite atualizações da barra de status.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsToolboxUser>|Exibir|Permite **caixa de ferramentas** itens.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEvents>|Dados|Envia notificações quando o arquivo for alterado.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat>|Dados|Habilita o recurso Salvar como para um tipo de arquivo.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistDocData2>|Dados|Habilita a persistência para o documento.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>|Dados|Permite a supressão de eventos de alteração de arquivo, como o disparo de recarregar.|