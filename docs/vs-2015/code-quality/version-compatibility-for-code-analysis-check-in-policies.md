---
title: Compatibilidade de versão para políticas do Check-In de análise de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- version compatibility, code analysis check-in policy
- check-in policies, version compatibility for code analysis
ms.assetid: 1af376e3-3be7-4445-803b-76a858567a5b
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 840a12e7f4c0e3853e885a803dea5a92e05a5a27
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49261476"
---
# <a name="version-compatibility-for-code-analysis-check-in-policies"></a>Compatibilidade da versão para políticas de check-in de análise do código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você deve avaliar e autor usando versões diferentes das políticas de seleção da análise de código [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], você deve saber as diferenças em como [!INCLUDE[vstsTfsOrcasLong](../includes/vststfsorcaslong-md.md)] e [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] avaliar políticas de check-in.  
  
## <a name="version-compatibility-for-evaluating-check-in-policies"></a>Compatibilidade de versão para avaliação de políticas de Check-In  
  
-   Quando as políticas do check-in de análise de código são avaliadas na [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)], todas as regras que existiam na [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] , mas não existem no [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] são ignorados.  
  
-   Quando as políticas do check-in de análise de código são avaliadas na [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)], todas as novas regras que são exclusivas para [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] são ignorados.  
  
-   Se a política de check-in do análise código especifica os assemblies de regras, [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] ignora todas as regras que são especificadas por assemblies que não reconhece.  
  
-   Se a política de check-in do análise código especifica os assemblies de regras que [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] não reconhece, será exibida uma mensagem.  
  
## <a name="version-compatibility-for-authoring-check-in-policies"></a>Compatibilidade de versão para a criação de políticas de Check-In  
  
-   Se você criou uma política de check-in do análise código usando o [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] versão do [!INCLUDE[esprtfc](../includes/esprtfc-md.md)], você não pode usar o [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] versão do [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] modificá-lo. Além disso, [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] não é possível avaliar a política.  
  
-   Se você criou uma política de check-in do análise código usando [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] na [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)], você pode usar [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] na [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)] modificar e a política também pode ser avaliada pelo [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)]. Depois de modificar a política por meio [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] na [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)], você não pode editar a política usando [!INCLUDE[esprtfc](../includes/esprtfc-md.md)] em [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)]. [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] pode avaliar essas políticas sem problemas com nomes fortes incompatíveis.  
  
-   Para criar uma política de check-in do análise código com configurações de regra que se aplicam a ambos [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] e [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)], você deve criar a política no [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)], fazer todas as alterações necessárias e salvar a política. Se as alterações às regras existem somente no [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)], modificar e salvar a política em [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)].  
  
     Depois de salvar a política no [!INCLUDE[vstsTfsOrcasShort](../includes/vststfsorcasshort-md.md)], você não poderá mais alterar as configurações para regras que existem no [!INCLUDE[vstsTfsRosarioShort](../includes/vststfsrosarioshort-md.md)] apenas.



