---
title: Adicionando diretórios à caixa de diálogo novo projeto | Microsoft Docs
description: Saiba como adicionar diretórios à caixa de diálogo novo projeto no Visual Studio, para que você possa criar novos tipos de projeto e exibi-los para uso como modelos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ed90ddec0fe8c6cf1941f7e272552882107763a7
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105079099"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>Adicionar diretórios à caixa de diálogo novo projeto
Ao criar novos tipos de projeto, você também pode registrar um novo diretório na caixa de diálogo **novo projeto** para exibi-los para uso como modelos. O exemplo de código a seguir explica como registrar um novo diretório, também conhecido como um nó. No exemplo, os modelos expostos pelo VSPackage, *CLSID_Package*, são registrados. Como resultado, o lado esquerdo da caixa de diálogo **novo projeto** oferece o nó adicionado, com um nome determinado pelo recurso de *Folder_Label_ResID* . Esse recurso é carregado da DLL satélite do VSPackage.

 O valor da **pasta** representa um GUID de uma pasta sob a qual o nó de *Folder_Label_ResID* é exibido. No exemplo, o GUID representa a pasta **outros projetos** no painel **tipos de projeto** da caixa de diálogo **novo projeto** . Se o valor de **outros projetos** estiver ausente, o rótulo será posicionado no nível superior.

 O `TemplatesDir` valor especifica o caminho completo do diretório que contém os modelos de projeto. Esses arquivos podem ser arquivos *. vsz* ou arquivos de modelo típicos a serem clonados.

 Se você especificar `TemplatesLocalizedSubDir` , deverá ser a ID de recurso de uma cadeia de caracteres que nomeia o subdiretório de `TemplatesDir` que mantém os modelos localizados. Como [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o carrega o recurso de cadeia de caracteres de uma DLL satélite, se você tiver um, cada DLL satélite poderá conter um nome de subdiretório diferente. O `SortPriority` valor especifica uma prioridade de classificação.

```
NoRemove NewProjectTemplates
{
    NoRemove TemplateDirs
  {
    ForceRemove %CLSID_Package%
    {
      ForceRemove /1 = s '#%Folder_Label_ResID%'
      {
        val Folder = s '{DCF2A94A-45B0-11D1-ADBF-00C04FB6BE4C}'
        val TemplatesDir = s '%Template_Path%'
        val TemplatesLocalizedSubDir = s '#100'
        val SortPriority = d 1000
      }
    }
  }
}
```

## <a name="see-also"></a>Confira também
- [Registrar modelos de projeto e item](../../extensibility/internals/registering-project-and-item-templates.md)
- [Adicionar itens à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [Adicionar diretórios à caixa de diálogo Adicionar novo item](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
