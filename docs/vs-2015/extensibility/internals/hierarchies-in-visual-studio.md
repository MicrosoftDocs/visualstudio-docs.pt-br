---
title: Hierarquias no Visual Studio | Microsoft Docs
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
- hierarchies, Visual Studio IDE
- IDE, hierarchies
ms.assetid: 0a029a7c-79fd-4b54-bd63-bd0f21aa8d30
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9d0f5d884f3d1b890aa3faeefa27ec1209af8b91
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51741806"
---
# <a name="hierarchies-in-visual-studio"></a>Hierarquias no Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ambiente de desenvolvimento integrado (IDE) exibe um projeto como um *hierarquia*. No IDE, uma hierarquia é uma árvore de nós, onde cada nó tem um conjunto de propriedades associadas. Um *hierarquia de projeto* é um contêiner que mantém os itens do projeto, as relações dos itens e propriedades associadas dos itens e comandos.  
  
 Na [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], você gerencia hierarquias de projeto usando a interface de hierarquia, <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> interface redireciona você invocar de itens de projeto para a janela de hierarquia apropriada, em vez do manipulador de comandos padrão de comandos.  
  
## <a name="project-hierarchies"></a>Hierarquias de projeto  
 Cada hierarquia do projeto contém itens que você pode exibir e editar. Esses itens variam dependendo do tipo de projeto. Por exemplo, um projeto de banco de dados pode conter procedimentos armazenados, exibições de banco de dados e tabelas de banco de dados. Um projeto de linguagem de programação, por outro lado, provavelmente incluirá arquivos de origem e arquivos de recurso para caixas de diálogo e bitmaps. Hierarquias podem ser aninhadas, que oferece alguns maior flexibilidade quando você cria uma hierarquia do projeto.  
  
 Quando você cria um novo tipo de projeto, o tipo de projeto controla o conjunto completo de itens que podem ser editadas nele. No entanto, os projetos podem conter itens para os quais não têm suporte de edição. Por exemplo, os projetos do Visual C++ podem conter arquivos HTML, mesmo que o Visual C++ não fornece qualquer editor personalizado para o tipo de arquivo HTML.  
  
 Hierarquias de gerenciam a persistência dos itens que contidos nelas. A implementação da hierarquia deve controlar as propriedades especiais que afetam a persistência dos itens dentro da hierarquia. Por exemplo, se os itens representam os objetos em um repositório em vez de arquivos, a implementação de hierarquia deve controlar a persistência desses objetos. O próprio IDE direciona a hierarquia para salvar os itens em conformidade com a entrada do usuário, mas o IDE não controla as ações necessárias para salvar esses itens. Em vez disso, o projeto está no controle.  
  
 Quando um usuário abre um item em um editor, a hierarquia que controla esse item é selecionada e se torna a hierarquia do Active Directory. A hierarquia selecionada determina o conjunto de comandos disponíveis para atuar no item. Acompanhamento de foco do usuário dessa maneira permite que a hierarquia refletir o contexto do usuário atual.  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de projeto](../../extensibility/internals/project-types.md)   
 [Seleção e moeda no IDE](../../extensibility/internals/selection-and-currency-in-the-ide.md)   
 [Exemplos de VSSDK](../../misc/vssdk-samples.md)

