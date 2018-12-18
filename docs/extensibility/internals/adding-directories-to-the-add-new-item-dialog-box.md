---
title: Adicionar diretórios para a caixa de diálogo Novo Item adicionar | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- Add New Item dialog box, extending
ms.assetid: 67ae8af6-3752-49e8-8ce3-007aca5f7982
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ba535908b1c5ccb06f0f29490c0b87c377d6b2be
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39498328"
---
# <a name="add-directories-to-the-add-new-item-dialog-box"></a>Adicionar diretórios à caixa de diálogo Adicionar Novo Item
O exemplo de código a seguir demonstra como registrar um novo conjunto de diretórios para o **Adicionar Novo Item** caixa de diálogo. Diretórios para o **Adicionar Novo Item** caixa de diálogo são diferentes para cada projeto. Portanto, os diretórios estão registrados com o **projetos** subchave, encontrado no **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\8.0Exp\Projects**.
  
## <a name="registry-script"></a>Script de registro  
  
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
  
 O `%Template_Path%` valor Especifica o caminho completo do diretório que contém os modelos de projeto. Esses modelos podem ser *. vsz* arquivos ou arquivos de modelo de um modelo a ser clonado.  
  
 O `SortPriority` valor Especifica uma prioridade de classificação.  
  
## <a name="add-items-to-an-existing-project"></a>Adicionar itens a um projeto existente  
 Você também pode adicionar itens a um projeto existente. Por exemplo, para um [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] projeto, você pode adicionar itens para o  *\<raiz > \Program Files\Microsoft Studio\VC Visual #\CSharpProjectItems\LocalProjectItems* pasta. Nesse caso, `%GUID_Project%` é o GUID de um projeto c# ({FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}).  
  
 Você também pode estender um projeto existente por um subtipo de projeto de programação. Com um subtipo de projeto, você pode estender um projeto sem precisar escrever um novo tipo de projeto. Para obter mais informações sobre os subtipos de projeto, consulte [subtipos de projeto](../../extensibility/internals/project-subtypes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Registrar os modelos de projeto e de item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Adicionar itens à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [Adicionar diretórios à caixa de diálogo Novo projeto](../../extensibility/internals/adding-directories-to-the-new-project-dialog-box.md)