---
title: 'CA2100: revisar consultas SQL para vulnerabilidades de segurança'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
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
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 69c8ba3b5cd30b71828a34c4b3dc8d7b4584b613
ms.sourcegitcommit: ad5fb20f18b23eb8bd2568717f61edc6b7eee5e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47859040"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100: revisar consultas SQL para vulnerabilidades de segurança

|||
|-|-|
|NomeDoTipo|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não são significativas|

## <a name="cause"></a>Causa
 Define um método de <xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName> propriedade usando uma cadeia de caracteres que é criada a partir de um argumento de cadeia de caracteres para o método.

## <a name="rule-description"></a>Descrição da regra

Esta regra pressupõe que o argumento da cadeia de caracteres contenha a entrada do usuário. Uma cadeia de caracteres de comando SQL criada com base na entrada do usuário é vulnerável a ataques de injeção SQL. Em um ataque de injeção de SQL, um usuário mal-intencionado fontes de entrada que altera o design de uma consulta em uma tentativa de danificar ou acesso não autorizado a banco de dados subjacente. Técnicas típicas incluem a injeção de uma aspa simples ou apóstrofe, que é o delimitador de literal de cadeia de caracteres SQL; dois traços, o que significa um comentário SQL; e um ponto e vírgula, que indica que um novo comando segue. Se a entrada do usuário deve fazer parte da consulta, use um dos seguintes, listados por ordem de eficiência, reduzir o risco de ataque.

- Use um procedimento armazenado.

- Use uma cadeia de caracteres de comando com parâmetros.

- Valide a entrada do usuário para o tipo e o conteúdo antes de compilar a cadeia de caracteres de comando.

Os seguintes tipos de .NET Framework implementam o <xref:System.Data.IDbCommand.CommandText%2A> propriedade ou fornecer construtores que defina a propriedade usando um argumento de cadeia de caracteres.

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> e <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> e <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> e <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

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

## <a name="how-to-fix-violations"></a>Como corrigir violações
 Para corrigir uma violação dessa regra, use uma consulta parametrizada.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
 É seguro suprimir um aviso nessa regra, se o texto do comando não contiver qualquer entrada do usuário.

## <a name="example"></a>Exemplo
 O exemplo a seguir mostra um método `UnsafeQuery`, que viola a regra e um método, `SaferQuery`, que satisfaz a regra usando uma cadeia de caracteres de comando com parâmetros.

 [!code-vb[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/VisualBasic/ca2100-review-sql-queries-for-security-vulnerabilities_1.vb)]
 [!code-csharp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CSharp/ca2100-review-sql-queries-for-security-vulnerabilities_1.cs)]
 [!code-cpp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CPP/ca2100-review-sql-queries-for-security-vulnerabilities_1.cpp)]

## <a name="see-also"></a>Consulte também
 [Visão geral de segurança](/dotnet/framework/data/adonet/security-overview)