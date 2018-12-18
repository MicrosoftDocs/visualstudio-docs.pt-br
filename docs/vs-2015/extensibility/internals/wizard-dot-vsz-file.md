---
title: Assistente (. Arquivo vsz) | Microsoft Docs
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
- .vsz files
- vsz files
- wizards, files
ms.assetid: 72e1d0f3-eef1-455e-b803-96827f030f50
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 428a2faf85180b9239f128dde5a9dadca04139af
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786427"
---
# <a name="wizard-vsz-file"></a>Arquivo do assistente (.Vsz)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O ambiente de desenvolvimento integrado (IDE) usa arquivos. vsz para iniciar assistentes. Esses arquivos. vsz contêm informações que o IDE usa para determinar qual assistente deve ser chamado e quais informações devem ser passados para o assistente.  
  
 Um arquivo. vsz é uma versão de um arquivo de texto de formato. ini com nenhuma seção. Informações conhecidas para o IDE são armazenadas no início do arquivo. Isso fornece um link entre o assistente que chama o IDE e os parâmetros que estão no arquivo. vsz a serem passados para o IDE. O restante do arquivo fornece parâmetros que são específicos para o assistente e que devem ser coletados pelo IDE e passados para o assistente específico.  
  
 O exemplo a seguir mostra o conteúdo de um arquivo. vsz.  
  
```  
VSWizard 8.0  
Wizard=VsWizard.CBlankSiteWizard -or- {123-1234556-123334}  
Param="WIZARDNAME = Wizard One"  
Param="WIZARDUI = FALSE"  
```  
  
 A seguir estão as partes no arquivo. vsz.  
  
|Parte|Descrição|  
|----------|-----------------|  
|VSWizard|O primeiro parâmetro no arquivo é o número de versão do formato de arquivo de modelo. Esse número de versão deve ser 6.0, 7.0, 7.1 ou 8.0. Outros números não podem ser iniciados e causam um erro de formato inválido.|  
|Wizard|Este campo contém a OLE ProgID do assistente, ou como alternativa, uma representação de cadeia de caracteres do GUID do CLSID do assistente que é cocreated pelo IDE.|  
|Param|Essas partes são opcionais. Você pode adicionar tantas quantas forem necessárias.|  
  
 Os parâmetros permitem que o arquivo. vsz transmita parâmetros personalizados adicionais ao assistente. Cada valor é passado como um elemento de cadeia de caracteres em uma matriz de variantes para o assistente. Para obter mais informações, consulte [parâmetros personalizados](../../extensibility/internals/custom-parameters.md). Para obter informações sobre como usar um arquivo. vsz no desenvolvimento de assistentes personalizados, consulte [. Arquivo vsz (controle de projeto)](http://msdn.microsoft.com/library/b8678fee-6795-46d1-9338-48b22d5e9207)  
  
 Para adicionar uma ID de localidade padrão para o arquivo. vsz, especifique `FALLBACK_LCID`= xxxx, onde xxxx é a ID de localidade, por exemplo, 1033 para inglês. Quando `FALLBACK_LCID` parâmetro for definido, o assistente usa a ID de localidade de fallback fornecido se a ID atual não for encontrada.  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros personalizados](../../extensibility/internals/custom-parameters.md)   
 [Assistentes](../../extensibility/internals/wizards.md)   
 [Arquivos de descrição do diretório do modelo (.Vsdir)](../../extensibility/internals/template-directory-description-dot-vsdir-files.md)

