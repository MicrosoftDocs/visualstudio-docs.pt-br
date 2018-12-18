---
title: Suporte a controle de origem | Microsoft Docs
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
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8310a18d9390858256067ba8dd16b61129b819a6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51746320"
---
# <a name="supporting-source-control"></a>Suporte para controle do código-fonte
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] dá suporte a check-outs de arquivo, check-ins e outras operações de controle do código-fonte para seu projeto ou um editor. Como um cliente de controle do código-fonte [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] foi projetado para interagir com um pacote de controle do código-fonte, como [!INCLUDE[vsvss](../../includes/vsvss-md.md)], que fornece o arquivamento, controle de versão e recursos de controle para um conjunto de arquivos definido dinamicamente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelo para pacotes de controle do código-fonte](../../extensibility/internals/model-for-source-control-packages.md)  
 Descreve as interfaces que um tipo de projeto deve implementar para dar suporte ao controle do código-fonte.  
  
 [Decisões de design](../../extensibility/internals/source-control-design-decisions.md)  
 Fornece as perguntas para cujas respostas alterar como você pode implementar um tipo de projeto.  
  
 [Detalhes de configuração](../../extensibility/internals/source-control-configuration-details.md)  
 Descreve como dar suporte a controle de origem é alterado a implementação de um tipo de projeto.  
  
 [Diretrizes adicionais para projetos e editores](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)  
 Discute as práticas recomendadas para tipos de projeto e editores.  
  
 [Detalhes de tempo de execução](../../extensibility/internals/source-control-runtime-details.md)  
 Descreve como registrar um projeto quando um usuário adiciona a um sistema de controle de origem.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>  
 Indica para o ambiente ou o pacote de controle de origem que um arquivo está prestes a ser alterada na memória ou salvos.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>  
 Permite que projetos e hierarquias se registrem com controle do código-fonte e obter informações sobre o status de controle do código-fonte.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>  
 Quando implementado em um sistema de projeto para fornecer controle de origem para arquivos de projeto e itens de projeto.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>  
 Usado por projetos para consultar o ambiente de permissão para adicionar, remover ou renomear um arquivo ou diretório em uma solução.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>  
 Notifica os clientes das alterações que foram feitas em arquivos de projeto ou diretórios.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece uma visão geral dos projetos como blocos de construção básicos do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] o ambiente de desenvolvimento integrado (IDE). São fornecidos links para tópicos adicionais que explicam como projetos de controle de criação e compilação de código.

