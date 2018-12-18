---
title: Adicionar diretórios à caixa de diálogo Novo projeto | Microsoft Docs
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
- New Project dialog box, extending
ms.assetid: 53b328f5-20bb-49a3-bf9e-1818f4fbdf50
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 6a03e61cf3699cd45a7b4b8e6a7e5b7d192ca6de
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51769742"
---
# <a name="adding-directories-to-the-new-project-dialog-box"></a>Adicionar diretórios à caixa de diálogo Novo Projeto
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Quando você cria novos tipos de projeto, você também pode registrar um novo diretório na **novo projeto** caixa de diálogo para exibi-los para uso como modelos. O exemplo de código a seguir explica como registrar um novo diretório, também conhecido como um nó. No exemplo, modelos expostos pelo VSPackage CLSID_Package são registrados. Como resultado, o lado esquerdo do **novo projeto** caixa de diálogo oferece o nó adicionado, com um nome determinado pelo recurso Folder_Label_ResID. Esse recurso é carregado do DLL de satélite do VSPackage.  
  
 O **pasta** valor representa um GUID de uma pasta sob a qual o nó de Folder_Label_ResID é exibido. No exemplo, o GUID que representa o **outros projetos** pasta na **tipos de projeto** painel da **novo projeto** caixa de diálogo. Se o **outros projetos** valor estiver ausente, o rótulo é posicionado no nível superior.  
  
 O valor de TemplatesDir Especifica o caminho completo do diretório que contém os modelos de projeto. Esses arquivos podem ser arquivos. vsz ou arquivos de modelo típico a ser clonado.  
  
 Se você especificar TemplatesLocalizedSubDir, ele deve ser a ID do recurso de uma cadeia de caracteres que nomeia o subdiretório do TemplatesDir que contém modelos localizados. Porque [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] carrega o recurso de cadeia de caracteres de uma DLL satélite se você tiver um, cada DLL satélite pode conter um nome de subdiretório diferentes. O valor de SortPriority Especifica uma prioridade de classificação.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Registrar modelos de projeto e Item](../../extensibility/internals/registering-project-and-item-templates.md)   
 [Adição de itens para a adicionar novo Item caixas de diálogo](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [Adicionar diretórios à caixa de diálogo Adicionar Novo Item](../../extensibility/internals/adding-directories-to-the-add-new-item-dialog-box.md)

