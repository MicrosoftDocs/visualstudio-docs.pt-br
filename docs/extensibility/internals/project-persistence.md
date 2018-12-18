---
title: Persistência de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b85bb6155ca25abec67b582dc4d877dbd8290501
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31131118"
---
# <a name="project-persistence"></a>Persistência de projeto
Persistência é uma consideração de design importante para seu projeto. A maioria dos projetos usar itens de projeto que representam arquivos; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] também oferece suporte a projetos cujos dados são não baseados em arquivo. Os arquivos de propriedade do projeto e o arquivo de projeto devem ser persistente. O IDE instrui o projeto para salvar um item de projeto ou consigo próprio.  
  
 Modelos para projetos são passados para a fábrica de projeto. Os modelos devem dar suporte a inicialização de todos os itens de projeto acordo com os requisitos do tipo de projeto específico. Esses modelos posteriormente podem ser salvos como arquivos de projeto e gerenciados pelo IDE por meio da solução. Para obter mais informações, consulte [criar projeto instâncias por usando fábricas de projeto](../../extensibility/internals/creating-project-instances-by-using-project-factories.md) e [soluções](../../extensibility/internals/solutions.md).  
  
 Itens de projeto podem ser baseada em arquivo ou não baseados em arquivo:  
  
-   Itens com base em arquivo podem ser local ou remoto. Em projetos Web em c#, por exemplo, as conexões com arquivos em um sistema remoto persistirem localmente, enquanto os próprios arquivos persistirem no sistema remoto.  
  
-   Itens com base em arquivo não podem salvar itens em um banco de dados ou um repositório.  
  
## <a name="commit-models"></a>Confirmar modelos  
 Depois de decidir onde se encontram os itens de projeto, você deve escolher o modelo de confirmação apropriado. Por exemplo, em um modelo baseado em arquivo com arquivos locais, cada projeto pode ser salvo autonomia. Em um modelo de repositório, você pode salvar vários itens em uma transação. Para obter mais informações, consulte [decisões de Design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).  
  
 Para determinar as extensões de nome de arquivo, projetos de implementam o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> interface, que fornece informações permitindo que o cliente de um objeto para implementar o **Salvar como** caixa de diálogo — ou seja, preencha o **Salvar como tipo**  suspensa listar e gerenciar a extensão de nome de arquivo inicial.  
  
 O IDE chama o `IPersistFileFormat` interface no projeto para indicar que o projeto deve manter seu projeto itens conforme apropriado. Portanto, o objeto possui todos os aspectos do seu arquivo e o formato. Isso inclui o nome do formato do objeto.  
  
 No caso em que itens não são arquivos, `IPersistFileFormat` ainda é como não-baseada em arquivo itens são persistentes. Projeto de arquivos, como arquivos. vbp para [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] arquivos de projetos ou. vcproj para [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projetos, também deve ser persistente.  
  
 Para salvar as ações, o IDE examina a tabela de documento (RDT) em execução e a hierarquia passa os comandos para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> interfaces. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A> método é implementado para determinar se o item foi modificado. Se o item tiver, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> método é implementado para salvar o item modificado.  
  
 Os métodos de `IVsPersistHierarchyItem2` interface são usados para determinar se um item pode ser recarregado e, se o item pode ser recarregá-lo. Além disso, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> método pode ser implementado para fazer com que itens alterados sejam descartadas sem ser salvado.  
  
## <a name="see-also"></a>Consulte também  
 [Lista de verificação: Criar novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [Criar instâncias de projetos usando fábricas de projetos](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)