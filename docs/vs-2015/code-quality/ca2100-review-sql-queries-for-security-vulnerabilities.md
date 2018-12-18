---
title: 'CA2100: Revisar consultas SQL para vulnerabilidades de segurança | Microsoft Docs'
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
- Review SQL queries for security vulnerabilities
- ReviewSqlQueriesForSecurityVulnerabilities
- CA2100
helpviewer_keywords:
- CA2100
- ReviewSqlQueriesForSecurityVulnerabilities
ms.assetid: 79670604-c02a-448d-9c0e-7ea0120bc5fe
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c77e448a492a64e3bbdf0f86809cdf82d7fd72fa
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49877394"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100: revisar consultas SQL para vulnerabilidades de segurança
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Define um método de <xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName> propriedade usando uma cadeia de caracteres que é criada a partir de um argumento de cadeia de caracteres para o método.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra pressupõe que o argumento da cadeia de caracteres contenha a entrada do usuário. Uma cadeia de caracteres de comando SQL criada com base na entrada do usuário é vulnerável a ataques de injeção SQL. Em um ataque de injeção de SQL, um usuário mal-intencionado fontes de entrada que altera o design de uma consulta em uma tentativa de danificar ou acesso não autorizado a banco de dados subjacente. Técnicas típicas incluem a injeção de uma aspa simples ou apóstrofe, que é o delimitador de literal de cadeia de caracteres SQL; dois traços, o que significa um comentário SQL; e um ponto e vírgula, que indica que um novo comando segue. Se a entrada do usuário deve fazer parte da consulta, use um dos seguintes, listados por ordem de eficiência, reduzir o risco de ataque.

- Use um procedimento armazenado.

- Use uma cadeia de caracteres de comando com parâmetros.

- Valide a entrada do usuário para o tipo e o conteúdo antes de compilar a cadeia de caracteres de comando.

  O seguinte [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] tipos implementam a <xref:System.Data.IDbCommand.CommandText%2A> propriedade ou fornecer construtores que defina a propriedade usando um argumento de cadeia de caracteres.

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> e <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> e <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> e <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- [System.Data.SqlServerCe.SqlCeCommand] (<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeCommand?qualifyHint=False&amp;autoUpgrade=True>  -->) e [System.Data.SqlServerCe.SqlCeDataAdapter] (<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeDataAdapter?qualifyHint=False&amp;autoUpgrade=True>  -->)

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> e <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

  Observe que essa regra é violada quando o método ToString de um tipo é usado explicitamente ou implicitamente para construir a cadeia de caracteres de consulta. Confira o exemplo abaixo.

```
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

 A regra é violada porque um usuário mal-intencionado pode substituir o método ToString ().

 A regra também é violada quando ToString é usado implicitamente.

```
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, use uma consulta parametrizada.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso nessa regra, se o texto do comando não contiver qualquer entrada do usuário.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método `UnsafeQuery`, que viola a regra e um método, `SaferQuery`, que satisfaz a regra usando uma cadeia de caracteres de comando com parâmetros.

 [!code-cpp[FxCop.Security.ReviewSqlQueries#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cpp/FxCop.Security.ReviewSqlQueries.cpp#1)]
 [!code-csharp[FxCop.Security.ReviewSqlQueries#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cs/FxCop.Security.ReviewSqlQueries.cs#1)]
 [!code-vb[FxCop.Security.ReviewSqlQueries#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/vb/FxCop.Security.ReviewSqlQueries.vb#1)]

## <a name="see-also"></a>Consulte também
 [Visão geral de segurança](http://msdn.microsoft.com/library/33e09965-61d5-48cc-9e8c-3b047cc4f194)



