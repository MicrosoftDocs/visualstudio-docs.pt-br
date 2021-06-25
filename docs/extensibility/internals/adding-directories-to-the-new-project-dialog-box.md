---
title: Adicionando diretórios à caixa de diálogo Novo Projeto | Microsoft Docs
description: Saiba como adicionar diretórios à caixa de diálogo Novo Projeto no Visual Studio, para que você possa criar novos tipos de projeto e exibi-los para uso como modelos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 44554c8bd7b758f1bf191d1a4bef9ba07941191d
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901832"
---
# <a name="add-directories-to-the-new-project-dialog-box"></a>Adicionar diretórios à caixa de diálogo Novo Projeto
Ao criar novos tipos de projeto, você também  pode registrar um novo diretório na caixa de diálogo Novo Projeto para exibi-los para uso como modelos. O exemplo de código a seguir explica como registrar um novo diretório, também conhecido como um nó. No exemplo, os modelos expostos pelo VSPackage, *CLSID_Package*, são registrados. Como resultado, o lado  esquerdo da caixa de diálogo *Novo* Projeto oferece o nó adicionado, com um nome determinado pelo Folder_Label_ResID recurso. Esse recurso é carregado da DLL satélite vsPackage.

 O **valor** Pasta representa um GUID de uma pasta sob a *qual o nó Folder_Label_ResID* é exibido. No exemplo, o GUID representa a **pasta Outros Projetos** no painel **Tipos** de Projeto da caixa **de diálogo** Novo Projeto. Se o **valor Outros Projetos** estiver ausente, o rótulo será posicionado no nível superior.

 O `TemplatesDir` valor especifica o caminho completo do diretório que contém os modelos de projeto. Esses arquivos podem ser *arquivos .vsz* ou arquivos de modelo típicos a serem clonados.

 Se você especificar , ele deverá ser a ID de recurso de uma cadeia de caracteres que nomeia o `TemplatesLocalizedSubDir` subdiretório de que `TemplatesDir` contém modelos localizados. Como carrega o recurso de cadeia de caracteres de uma DLL satélite se você tiver uma, cada DLL satélite pode [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] conter um nome de subdiretório diferente. O `SortPriority` valor especifica uma prioridade de classificação.

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
- [Adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [Adicionar diretórios à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)
