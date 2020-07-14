---
title: 'CA2100: examinar as consultas SQL em busca de vulnerabilidades de segurança | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Review SQL queries for security vulnerabilities
- ReviewSqlQueriesForSecurityVulnerabilities
- CA2100
helpviewer_keywords:
- CA2100
- ReviewSqlQueriesForSecurityVulnerabilities
ms.assetid: 79670604-c02a-448d-9c0e-7ea0120bc5fe
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 797c071cdc74c36afeece304bfa4c708d7bf7147
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85521206"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100: Examinar consultas SQL em busca de vulnerabilidades de segurança
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Um método define a <xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName> propriedade usando uma cadeia de caracteres que é criada a partir de um argumento de cadeia de caracteres para o método.

## <a name="rule-description"></a>Descrição da Regra
 Esta regra pressupõe que o argumento da cadeia de caracteres contenha a entrada do usuário. Uma cadeia de caracteres de comando SQL criada com base na entrada do usuário é vulnerável a ataques de injeção SQL. Em um ataque de injeção de SQL, um usuário mal-intencionado fornece entrada que altera o design de uma consulta em uma tentativa de danificar ou obter acesso não autorizado ao banco de dados subjacente. As técnicas típicas incluem injeção de uma aspa simples ou apóstrofo, que é o delimitador de cadeia de caracteres literal SQL; dois traços, que representa um comentário SQL; e um ponto e vírgula, que indica que um novo comando segue. Se a entrada do usuário precisar fazer parte da consulta, use um dos itens a seguir, listado em ordem de eficácia, para reduzir o risco de ataque.

- Use um procedimento armazenado.

- Use uma cadeia de caracteres de comando com parâmetros.

- Valide a entrada do usuário para o tipo e o conteúdo antes de criar a cadeia de caracteres de comando.

  Os tipos a seguir [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] implementam a <xref:System.Data.IDbCommand.CommandText%2A> propriedade ou fornecem construtores que definem a propriedade usando um argumento de cadeia de caracteres.

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> e <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> e <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> e <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- [System. Data. SqlServerCe. SqlCeCommand] (<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeCommand?qualifyHint=False&amp;autoUpgrade=True>  -->) e [System. Data. SqlServerCe. SqlCeDataAdapter] (<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeDataAdapter?qualifyHint=False&amp;autoUpgrade=True>  -->)

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> e <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

  Observe que essa regra é violada quando o método ToString de um tipo é usado explicitamente ou implicitamente para construir a cadeia de caracteres de consulta. A seguir, é mostrado um exemplo.

```
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

 A regra foi violada porque um usuário mal-intencionado pode substituir o método ToString ().

 A regra também é violada quando ToString é usado implicitamente.

```
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>Como Corrigir Violações
 Para corrigir uma violação dessa regra, use uma consulta parametrizada.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 É seguro suprimir um aviso dessa regra se o texto do comando não contiver nenhuma entrada do usuário.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método, `UnsafeQuery` , que viola a regra e um método, `SaferQuery` que satisfaz a regra usando uma cadeia de caracteres de comando com parâmetros.

 [!code-cpp[FxCop.Security.ReviewSqlQueries#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cpp/FxCop.Security.ReviewSqlQueries.cpp#1)]
 [!code-csharp[FxCop.Security.ReviewSqlQueries#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cs/FxCop.Security.ReviewSqlQueries.cs#1)]
 [!code-vb[FxCop.Security.ReviewSqlQueries#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/vb/FxCop.Security.ReviewSqlQueries.vb#1)]

## <a name="see-also"></a>Consulte Também
 [Visão geral de segurança](https://msdn.microsoft.com/library/33e09965-61d5-48cc-9e8c-3b047cc4f194)
