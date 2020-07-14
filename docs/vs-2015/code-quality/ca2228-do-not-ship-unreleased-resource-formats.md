---
title: 'CA2228: não enviar formatos de recurso não lançados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 4adcae1c1cc616cdbcf5a7aa15342d221c2f4300
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540576"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228: Não fornecer formatos de recurso não lançados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|Categoria|Microsoft. Usage|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um arquivo de recurso foi criado usando uma versão do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] que não tem suporte no momento.

## <a name="rule-description"></a>Descrição da Regra
 Os arquivos de recursos criados com versões de pré-lançamento do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] podem não ser utilizáveis por versões com suporte do .NET Framework.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, compile o recurso usando uma versão com suporte do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] k.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra.
