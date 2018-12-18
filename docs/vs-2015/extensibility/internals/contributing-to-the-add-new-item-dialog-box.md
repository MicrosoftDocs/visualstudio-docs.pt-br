---
title: Contribuindo para a caixa de diálogo Novo Item adicionar | Microsoft Docs
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
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
caps.latest.revision: 19
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: eb4db6bb361a47ca7c4d974950a99f4f1e9f395b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766546"
---
# <a name="contributing-to-the-add-new-item-dialog-box"></a>Contribuindo com a caixa de diálogo Adicionar Novo Item
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um subtipo de projeto pode fornecer um novo diretório completo de itens para o **Adicionar Novo Item** caixa de diálogo, registrando **Adicionar Item** modelos sob o `Projects` subchave do registro.  
  
## <a name="registering-add-new-item-templates"></a>Registrar modelos para adicionar novo Item  
 Esta seção está localizada sob **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects** no registro. As entradas do Registro abaixo pressupõem uma [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] projeto agregados por um subtipo de projeto hipotético. As entradas para o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] projeto estão listadas abaixo.  
  
```  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}]  
@="#2143"  
"DefaultProjectExtension"="vbproj"  
"PossibleProjectExtensions"="vbproj;vbp"  
"ProjectTemplatesDir"="visualStudioInstallPath\\Vb\\.\\VBProjects"  
  
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects\{F184B08F-C81C-45F6-A57F-5ABD9991F28F}\AddItemTemplates\TemplateDirs\{12345678-1234-1234-1122334455667788}\/1]  
@="#100"  
"TemplatesDir"="projectSubTypeTemplatesDir\\VBProjectItems"  
```  
  
 O `AddItemTemplates\TemplateDirs` subchave contém entradas do registro com o caminho para o diretório em que itens disponibilizados na **Adicionar Novo Item** caixa de diálogo são colocados.  
  
 O ambiente carrega automaticamente todos os `AddItemTemplates` dados sob o `Projects` subchave do registro. Isso pode incluir os dados para implementações de base do projeto, bem como os dados específicos subtipo para tipos de projeto. Subtipo de cada projeto é identificado por um tipo de projeto `GUID`. O subtipo de projeto pode especificar que uma alternativa é definida de `Add Item` modelos devem ser usados para uma instância de determinado projeto flavored dando suporte a `VSHPROPID_ AddItemTemplatesGuid` enumeração de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> em <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> implementação para retornar o GUID valor do subtipo de projeto. Se `VSHPROPID_AddItemTemplatesGuid` propriedade não for especificada, o projeto base que GUID é usado.  
  
 Você pode filtrar itens na **Adicionar Novo Item** caixa de diálogo, Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> interface no objeto do agregador de subtipo de projeto. Por exemplo, um subtipo de projeto que implementa um projeto de banco de dados agregando um [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] do projeto, pode filtrar o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] específicos de itens da **Adicionar Novo Item** caixa de diálogo com a implementação de filtragem e em Ativar, poderá adicionar itens específicos do projeto de banco de dados, oferecendo suporte a `VSHPROPID_ AddItemTemplatesGuid` em <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>. Para obter mais informações sobre filtragem e adição de itens para o **Adicionar Novo Item** caixa de diálogo, consulte [adicionando itens para as caixas de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md).  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>   
 [CATIDs para objetos normalmente usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)

