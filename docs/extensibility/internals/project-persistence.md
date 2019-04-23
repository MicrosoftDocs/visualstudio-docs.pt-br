---
title: Persistência de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- persistence, projects
- projects [Visual Studio SDK], persistance
ms.assetid: 42907bcf-4e27-46bd-a8cb-01c2ccd2bde5
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c19b623efca921e7557a818c3915faf6ea158641
ms.sourcegitcommit: 1fc6ee928733e61a1f42782f832ead9f7946d00c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60087297"
---
# <a name="project-persistence"></a>Persistência de projeto
Persistência é uma consideração de design chave para seu projeto. A maioria dos projetos usar itens de projeto que representam arquivos; [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] também oferece suporte a projetos cujos dados são não baseados em arquivo. Os arquivos de propriedade do projeto e o arquivo de projeto devem ser persistente. O IDE instrui o projeto para salvar a mesmo ou para um item de projeto.

 Modelos para projetos são passados para a fábrica de projeto. Os modelos devem dar suporte a inicialização de todos os itens de projeto acordo com os requisitos do tipo de projeto específico. Esses modelos podem posteriormente salvos como arquivos de projeto e gerenciados pelo IDE através da solução. Para obter mais informações, consulte [criação de projeto instâncias por usando fábricas de projetos](../../extensibility/internals/creating-project-instances-by-using-project-factories.md) e [soluções](../../extensibility/internals/solutions-overview.md).

 Itens de projeto podem ser baseado em arquivo ou não se baseiam no arquivo:

- Itens com base em arquivo podem ser local ou remoto. Em projetos da Web em c#, por exemplo, conexões com arquivos em um sistema remoto persistem localmente, enquanto que os próprios arquivos persistirem no sistema remoto.

- Itens com base em arquivo não podem salvar os itens a um banco de dados ou o repositório.

## <a name="commit-models"></a>Modelos de confirmação
 Depois de decidir onde se encontram os itens de projeto, você deve escolher o modelo apropriado de confirmação. Por exemplo, em um modelo baseado em arquivo com arquivos locais, cada projeto pode ser salvo com autonomia. Em um modelo de repositório, você pode salvar vários itens em uma transação. Para obter mais informações, consulte [decisões de Design de tipo de projeto](../../extensibility/internals/project-type-design-decisions.md).

 Para determinar as extensões de nome de arquivo, os projetos de implementam o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat> interface, que fornece informações permitindo que o cliente de um objeto que implemente a **Salvar como** caixa de diálogo — ou seja, para preencher o **Salvar como tipo**  suspensa listar e gerenciar a extensão de nome de arquivo inicial.

 As chamadas IDE a `IPersistFileFormat` itens de interface no projeto para indicar que o projeto deve manter seu projeto conforme apropriado. Portanto, o objeto é responsável por todos os aspectos de seu arquivo e formato. Isso inclui o nome do formato do objeto.

 No caso em que itens não são arquivos, `IPersistFileFormat` ainda é como não-file-based itens são mantidas. Projeto de arquivos, como arquivos. vbp para [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] arquivos de projetos ou. vcproj do [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] projetos, também deve ser persistente.

 Para salvar as ações, o IDE examina a tabela de documento (RDT) em execução e a hierarquia passa os comandos para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem> e o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2> interfaces. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.IsItemDirty%2A> método é implementado para determinar se o item foi modificado. Se o item tiver, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem.SaveItem%2A> método é implementado para salvar o item modificado.

 Os métodos no `IVsPersistHierarchyItem2` interface são usados para determinar se um item pode ser recarregado e, se o item pode ser, para recarregá-lo. Além disso, o <xref:Microsoft.VisualStudio.Shell.Interop.IVsPersistHierarchyItem2.IgnoreItemFileChanges%2A> método pode ser implementado para fazer com que itens alterados para serem descartados sem ser salvado.

## <a name="see-also"></a>Consulte também
- [Lista de verificação: Criação de novos tipos de projeto](../../extensibility/internals/checklist-creating-new-project-types.md)
- [Criar instâncias de projetos usando fábricas de projetos](../../extensibility/internals/creating-project-instances-by-using-project-factories.md)