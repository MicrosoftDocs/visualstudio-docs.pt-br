---
title: Contribuindo para a caixa de diálogo Adicionar novo item | Microsoft Docs
description: Saiba como contribuir para a caixa de diálogo Adicionar novo item no Visual Studio registrando adicionar modelos de item na subchave do registro de projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, contributing to
ms.assetid: b2e53175-9372-4d17-8c2b-9264c9e51e9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8186f25f8e1631f0e13aa7a8f43620812c4c7693
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057046"
---
# <a name="contribute-to-the-add-new-item-dialog-box"></a>Contribuir para a caixa de diálogo Adicionar novo item
Um subtipo de projeto pode fornecer um novo diretório completo de itens para a caixa de diálogo **Adicionar novo item** , registrando adicionar modelos de **Item** na subchave do registro **projetos** .

## <a name="register-add-new-item-templates"></a>Registrar adicionar novos modelos de item
 Esta seção está localizada em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0\Projects** no registro. As entradas de registro abaixo pressupõem um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto agregado por um subtipo de projeto hipotético. As entradas para o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto estão listadas abaixo.

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

 A subchave **AddItemTemplates\TemplateDirs** contém entradas de registro com o caminho para o diretório em que os itens disponibilizados na caixa de diálogo **Adicionar novo item** são colocados.

 O ambiente carrega automaticamente todos os dados de **Additemtemplates** na subchave do registro **Projects** . Esses dados podem incluir os dados para implementações de projeto base, bem como os dados para tipos de subtipo de projeto específicos. Cada subtipo de projeto é identificado por um **GUID** de tipo de projeto. O subtipo de projeto pode especificar que um conjunto alternativo de modelos de **adição de item** deve ser usado para uma instância de projeto determinada, dando suporte à `VSHPROPID_ AddItemTemplatesGuid` enumeração de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> em <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> implementação para retornar o valor de GUID do subtipo do projeto. Se a `VSHPROPID_AddItemTemplatesGuid` propriedade não for especificada, o GUID do projeto base será usado.

 Você pode filtrar itens na caixa de diálogo **Adicionar novo item** implementando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> interface no objeto agregador de subtipo do projeto. Por exemplo, um subtipo de projeto que implementa um projeto de banco de dados agregando um [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projeto, pode filtrar os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] itens específicos da caixa de diálogo **Adicionar novo item** implementando a filtragem e, por sua vez, pode adicionar itens específicos do projeto de banco de dados ao dar suporte ao `VSHPROPID_ AddItemTemplatesGuid` <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A> . Para obter mais informações sobre como filtrar e adicionar itens à caixa de diálogo **Adicionar novo item** , consulte [Adicionar itens à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md).

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg2>
- [CATIDs para objetos que normalmente são usados para estender projetos](../../extensibility/internals/catids-for-objects-that-are-typically-used-to-extend-projects.md)
