---
title: 'CA1711: Os identificadores não devem ter sufixo incorreto | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
helpviewer_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1f42416a6d88edc417c0150685ab4c7e198aa808
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49837094"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711: os identificadores não devem ter sufixo incorreto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|Categoria|Microsoft.Naming|
|Alteração Significativa|Quebra|

## <a name="cause"></a>Causa
 Um identificador tem um sufixo incorreto.

## <a name="rule-description"></a>Descrição da Regra
 Por convenção, somente os nomes dos tipos que estendem determinados tipos de base ou que implementam determinadas interfaces, ou tipos derivados desses tipos, devem terminar com sufixos reservados específicos. Outros nomes de tipo não devem usar esses sufixos reservados.

 A tabela a seguir lista os sufixos reservados e os tipos base e interfaces com a qual eles estão associados.

|Sufixo|Tipo/Interface base|
|------------|--------------------------|
|Atributo|<xref:System.Attribute?displayProperty=fullName>|
|Coleção|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|Dicionário|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|Um delegado de manipulador de eventos|
|Exceção|<xref:System.Exception?displayProperty=fullName>|
|Permissão|<xref:System.Security.IPermission?displayProperty=fullName>|
|fila|<xref:System.Collections.Queue?displayProperty=fullName>|
|Pilha|<xref:System.Collections.Stack?displayProperty=fullName>|
|Fluxo|<xref:System.IO.Stream?displayProperty=fullName>|

 Além disso, os seguintes sufixos devem **não** ser usado:

- delegado

- Enum

- Impl - use 'Core' em vez disso

- Ex ou sufixo semelhante para distingui-lo de uma versão anterior do mesmo tipo

  Convenções de nomenclatura de fornecem uma aparência comum para bibliotecas que direcionam o common language runtime. Isso reduz a curva de aprendizado que é necessário para novas bibliotecas de software e aumenta a confiança do cliente que a biblioteca foi desenvolvida por alguém que tenha experiência em desenvolvimento de código gerenciado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Remova o sufixo do nome do tipo.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 Não suprima um aviso nessa regra, a menos que o sufixo tem um significado inequívoco no domínio do aplicativo.

## <a name="related-rules"></a>Regras relacionadas
 [CA1710: os identificadores devem ter o sufixo correto](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>Consulte também
 [Atributos](http://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB: delegados e eventos](http://msdn.microsoft.com/en-us/d98fd58b-fa4f-4598-8378-addf4355a115)



