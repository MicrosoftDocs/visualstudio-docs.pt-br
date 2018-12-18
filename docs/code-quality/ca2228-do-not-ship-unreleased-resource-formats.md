---
title: 'CA2228: não remeter formatos de recurso não lançados'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotShipUnreleasedResourceFormats
- CA2228
helpviewer_keywords:
- CA2228
- DoNotShipUnreleasedResourceFormats
ms.assetid: 2c614edc-4e94-4b4f-8067-eea677a75cd9
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 71667a9d00dd1935e8eaeb281c5f0c6834208702
ms.sourcegitcommit: 401be39a42ffe007593528b5bba62583ca9fcafd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244392"
---
# <a name="ca2228-do-not-ship-unreleased-resource-formats"></a>CA2228: não remeter formatos de recurso não lançados

|||
|-|-|
|NomeDoTipo|DoNotShipUnreleasedResourceFormats|
|CheckId|CA2228|
|Categoria|Microsoft.Usage|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Um arquivo de recurso foi criado usando uma versão do .NET Framework que não é suportada atualmente.

## <a name="rule-description"></a>Descrição da regra
 Arquivos de recursos que foram compilados usando versões de pré-lançamento do .NET Framework não podem ser usados por versões com suporte do .NET Framework.

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, crie o recurso usando uma versão com suporte do .NET Framework.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 Não suprima um aviso nessa regra.
