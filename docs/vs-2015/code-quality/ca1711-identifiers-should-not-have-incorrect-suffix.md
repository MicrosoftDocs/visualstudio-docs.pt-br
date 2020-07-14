---
title: 'CA1711: os identificadores não devem ter um sufixo incorreto | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
helpviewer_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1e753083e9b4bda1e33553021ccb0027a2af2533
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544008"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711: Identificadores não devem ter um sufixo incorreto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|Categoria|Microsoft. Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um identificador tem um sufixo incorreto.

## <a name="rule-description"></a>Descrição da Regra
 Por convenção, somente os nomes de tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, devem terminar com sufixos reservados específicos. Outros nomes de tipo não devem usar esses sufixos reservados.

 A tabela a seguir lista os sufixos reservados e os tipos de base e interfaces com os quais eles estão associados.

|Sufixo|Tipo/interface base|
|------------|--------------------------|
|Atributo|<xref:System.Attribute?displayProperty=fullName>|
|Coleção|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|Dicionário|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|Um delegado de manipulador de eventos|
|Exceção|<xref:System.Exception?displayProperty=fullName>|
|Permissão|<xref:System.Security.IPermission?displayProperty=fullName>|
|Fila|<xref:System.Collections.Queue?displayProperty=fullName>|
|Pilha|<xref:System.Collections.Stack?displayProperty=fullName>|
|STREAM|<xref:System.IO.Stream?displayProperty=fullName>|

 Além disso, os seguintes sufixos **não** devem ser usados:

- Delegar

- Enumeração

- Impl-use ' Core ' em vez disso

- Ex ou sufixo semelhante para distingui-lo de uma versão anterior do mesmo tipo

  As convenções de nomenclatura fornecem uma aparência comum para as bibliotecas direcionadas ao Common Language Runtime. Isso reduz a curva de aprendizado necessária para novas bibliotecas de software e aumenta a confiança do cliente de que a biblioteca foi desenvolvida por alguém que tenha experiência no desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remova o sufixo do nome do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprimir um aviso dessa regra, a menos que o sufixo tenha um significado não ambíguo no domínio do aplicativo.

## <a name="related-rules"></a>Regras relacionadas
 [CA1710: Identificadores devem ter um sufixo correto](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>Consulte Também
 [Atributos](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: eventos e delegados](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
