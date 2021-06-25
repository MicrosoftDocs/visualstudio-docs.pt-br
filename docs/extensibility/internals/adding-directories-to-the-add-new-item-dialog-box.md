---
title: Adicionando diretórios à caixa de diálogo Adicionar Novo Item | Microsoft Docs
description: Saiba como adicionar diretórios à caixa de diálogo Adicionar Novo Item no Visual Studio usando um script do Registro para registrar os diretórios.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: dab135f8e8632755674d7b3ddf5972592f74d315
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112904354"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>Adicionar diretórios à caixa de diálogo Adicionar Novo Item
O exemplo de código a seguir demonstra como registrar um novo conjunto de diretórios para a **caixa de diálogo** Adicionar Novo Item. Os diretórios da **caixa de diálogo Adicionar Novo Item** são diferentes para cada projeto. Portanto, os diretórios são registrados na sub-chave **Projetos,** encontrada em **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects**.

## <a name="registry-script"></a>Script do Registro

```
NoRemove Projects
{
  NoRemove %GUID_Project%
  {
    NoRemove AddItemTemplates
    {
      NoRemove TemplateDirs
      {
        ForceRemove %CLSID_Package%
        {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
          {
            val TemplatesDir = s '%Template_Path%'
            val SortPriority = d 2000
          }
        }
      }
    }
  }
}
```

 O `%Template_Path%` valor especifica o caminho completo do diretório que contém os modelos de projeto. Esses modelos podem ser arquivos *.vsz* ou arquivos de modelo prototípicos a serem clonados.

 O `SortPriority` valor especifica uma prioridade de classificação.

## <a name="add-items-to-an-existing-project"></a>Adicionar itens a um projeto existente
 Você também pode adicionar itens a um projeto existente. Por exemplo, para um projeto, você pode adicionar itens à pasta \Arquivos de [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] *\<root> Programas\Microsoft Visual Studio\VC#\CSharpProjectItems\LocalProjectItems.* Nesse caso, é o GUID de um projeto `%GUID_Project%` C# ({GUID04EC0-301F-11D3-BF4B-00C04F79EFBC}).

 Você também pode estender um projeto existente programando um subtipo de projeto. Com um subtipo de projeto, você pode estender um projeto sem escrever um novo tipo de projeto. Para obter mais informações sobre subtipos de projeto, consulte [Subtipos de projeto](../../extensibility/internals/project-subtypes.md).

## <a name="see-also"></a>Confira também
- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [Adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [Adicionar diretórios à caixa de diálogo Novo Projeto](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)
