---
title: Suporte a controle de origem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- source control [Visual Studio SDK], supporting
ms.assetid: 567acde3-354e-4f39-8d99-0ef86c103396
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9ae3590a5d02c2b3f1d4b67f724d0177f671f7d2
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31130647"
---
# <a name="supporting-source-control"></a>Suporte a controle de origem
[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] dá suporte a check-out do arquivo, check-ins e outras operações de controle de origem para o projeto ou o editor. Como um cliente de controle de origem, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] é projetado para interagir com um pacote de controle de origem, como [!INCLUDE[vsvss](../../extensibility/includes/vsvss_md.md)], que fornece arquivamento, controle de versão e recursos de controle para um conjunto de arquivos definido dinamicamente.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Modelo para pacotes de controle do código-fonte](../../extensibility/internals/model-for-source-control-packages.md)  
 Descreve as interfaces de um tipo de projeto deve implementar para dar suporte ao controle de origem.  
  
 [Decisões de design](../../extensibility/internals/source-control-design-decisions.md)  
 Fornece as perguntas cujas respostas alterar como você implementa um tipo de projeto.  
  
 [Detalhes de configuração](../../extensibility/internals/source-control-configuration-details.md)  
 Descreve como dar suporte a controle de origem muda a implementação de um tipo de projeto.  
  
 [Diretrizes adicionais para projetos e editores](../../extensibility/internals/additional-source-control-guidelines-for-projects-and-editors.md)  
 Discute as práticas recomendadas para tipos de projeto e editores.  
  
 [Detalhes de tempo de execução](../../extensibility/internals/source-control-runtime-details.md)  
 Descreve como registrar um projeto quando um usuário adiciona a um sistema de controle de origem.  
  
## <a name="reference"></a>Referência  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsQueryEditQuerySave2>  
 Indica para o ambiente ou o pacote de controle de origem que um arquivo está prestes a ser alterada na memória ou salvo.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccManager2>  
 Permite que os projetos e hierarquias para se registrar com o controle de origem e obter informações sobre o status de controle de origem.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSccProject2>  
 Implementado em um sistema de projeto para fornecer controle de origem para arquivos de projeto e itens de projeto.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocuments2>  
 Usado por projetos para consultar o ambiente de permissão Adicionar, remover ou renomear um arquivo ou diretório em uma solução.  
  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsTrackProjectDocumentsEvents2>  
 Notifica os clientes de alterações que foram feitas em arquivos de projeto ou diretórios.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece uma visão geral de projetos como blocos de construção básicos do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente de desenvolvimento integrado (IDE). São fornecidos links para tópicos adicionais que explicam como projetos de controle de criar e compilar o código.