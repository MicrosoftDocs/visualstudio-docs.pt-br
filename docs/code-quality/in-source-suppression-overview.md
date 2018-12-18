---
title: Suprimir avisos da análise de código
ms.date: 08/03/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: 1e90de7acf13ca28a20a35aa3ad3e70f58780279
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39513040"
---
# <a name="suppress-code-analysis-warnings"></a>Suprimir avisos da análise de código

Geralmente é útil indicar que um aviso não é aplicável. Isso indica aos membros da equipe que o código foi revisado e que o aviso pode ser suprimido. Usos de supressão (ISS) no código-fonte a <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo para suprimir um aviso. O atributo pode ser colocado perto o segmento de código que gerou o aviso. Você pode adicionar o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> de atributo para o arquivo de origem, digitando-o, ou você pode usar o menu de atalho em um aviso na **lista de erros** para adicioná-lo automaticamente.

O <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> é um atributo condicional, que está incluído nos metadados de IL do seu assembly de código gerenciado, somente se o símbolo de compilação CODE_ANALYSIS for definido em tempo de compilação.

No C + + c++ CLI, use as macros da autoridade de certificação\_SUPRIMIR\_mensagem ou a autoridade de certificação\_GLOBAL\_SUPPRESS_MESSAGE no arquivo de cabeçalho para adicionar o atributo.

> [!NOTE]
> Você não deve usar supressões de código-fonte em compilações de versão, para impedir que os metadados de supressão na origem de envio acidentalmente. Além disso, devido ao custo de processamento de supressão de código-fonte, o desempenho do seu aplicativo pode ser prejudicado.

> [!NOTE]
> Se você migrar um projeto para Visual Studio 2017, você pode encontrar, de repente, com um grande número de avisos da análise de código. Esses avisos são provenientes [analisadores de Roslyn](roslyn-analyzers-overview.md). Se você não estiver pronto para corrigir os avisos, você pode suprimir todos eles, escolhendo **Analyze** > **executar análise de código e suprimir problemas ativos**.
>
> ![Executar análise de código e suprimir problemas no Visual Studio](media/suppress-active-issues.png)

## <a name="suppressmessage-attribute"></a>Atributo SuppressMessage

Quando você escolhe **suprimir** no menu de contexto ou o botão direito do mouse de um aviso de análise de código na **lista de erros**, um <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo é adicionado em seu código ou para a supressão global do projeto arquivo.

O <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo tem o seguinte formato:

```vb
<Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

As propriedades do atributo incluem:

- **Categoria** -a categoria na qual a regra é definida. Para obter mais informações sobre categorias de regras de análise de código, consulte [gerenciados avisos de código](../code-quality/code-analysis-for-managed-code-warnings.md).

- **CheckId** -o identificador da regra. O suporte inclui tanto um nome curto e longo para o identificador de regra. O nome curto é CAXXXX; o nome longo é CAXXXX:FriendlyTypeName.

- **Justificação** -o texto que é usado para documentar o motivo para suprimir a mensagem.

- **MessageId** -identificador exclusivo de um problema para cada mensagem.

- **Escopo** -o de destino no qual o aviso está sendo suprimido. Se o destino não for especificado, ele é definido como o destino do atributo. Escopos com suporte incluem o seguinte:

    - Módulo

    - Namespace

    - Recurso

    - Tipo

    - Membro

- **Destino** – um identificador que é usado para especificar o destino no qual o aviso está sendo suprimido. Ele deve conter um nome totalmente qualificado do item.

## <a name="suppressmessage-usage"></a>Uso de SuppressMessage

Avisos da análise de código são suprimidos no nível ao qual o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo é aplicado. Por exemplo, o atributo pode ser aplicado no assembly, módulo, tipo, membro ou nível de parâmetro. O objetivo é acoplar rigidamente as informações de supressão para o código onde ocorre a violação.

A forma geral de supressão inclui a categoria de regra e um identificador de regra, que contém uma representação legível por humanos opcional do nome da regra. Por exemplo:

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

Se houver motivos de desempenho estrito para minimizar os metadados de supressão na origem, o nome da regra pode ser omitido. A categoria de regra e a sua ID de regra juntos, constituem um identificador de regra suficientemente exclusivo. Por exemplo:

`[SuppressMessage("Microsoft.Design", "CA1039")]`

Por motivos de capacidade de manutenção, não é recomendável omitir o nome da regra.

## <a name="suppress-selective-violations-within-a-method-body"></a>Suprimir seletivas violações dentro de um corpo de método

Atributos de supressão podem ser aplicados a um método, mas não podem ser inseridos em um corpo de método. Isso significa que todas as violações de uma determinada regra são suprimidas, se você adicionar o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo ao método.

Em alguns casos, você talvez queira suprimir uma instância específica da violação, por exemplo, para que o código futuro não é automaticamente isento das regras de análise de código. Certas regras de análise de código permitem que você faça isso usando o `MessageId` propriedade do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo. Em geral, as regras de herdado para violações no sentido de um símbolo específico (uma variável local ou parâmetro) a `MessageId` propriedade. [CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500-variable-names-should-not-match-field-names.md) é um exemplo de tal uma regra. No entanto, as regras herdadas quanto a violações de código executável (não símbolo) não respeitam o `MessageId` propriedade. Além disso, os analisadores do .NET Compiler Platform ("Roslyn") não respeitam o `MessageId` propriedade.

Para suprimir uma violação de símbolo específico de uma regra, especifique o nome do símbolo para o `MessageId` propriedade do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo. O exemplo a seguir mostra o código com duas violações [CA1500:VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500-variable-names-should-not-match-field-names.md)&mdash;um para o `name` variável e outro para o `age` variável. Somente a violação para o `age` símbolo será suprimido.

```vb
Public Class Animal
    Dim age As Integer
    Dim name As String

    <CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId:="age")>
    Sub PrintInfo()
        Dim age As Integer = 5
        Dim name As String = "Charlie"

        Console.WriteLine("Age {0}, Name {1}", age, name)
    End Sub

End Class
```

```csharp
public class Animal
{
    int age;
    string name;

    [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Maintainability", "CA1500:VariableNamesShouldNotMatchFieldNames", MessageId = "age")]
    private void PrintInfo()
    {
        int age = 5;
        string name = "Charlie";

        Console.WriteLine($"Age {age}, Name {name}");
    }
}
```

## <a name="generated-code"></a>Código gerado

Compiladores de código gerenciado e algumas ferramentas de terceiros geram código para facilitar o desenvolvimento rápido de código. Código gerado pelo compilador que aparece nos arquivos de origem geralmente é marcado com o `GeneratedCodeAttribute` atributo.

Você pode escolher se deseja suprimir avisos da análise de código e erros de código gerado. Para obter informações sobre como suprimir esses avisos e erros, consulte [como: suprimir avisos para o código gerado pelo](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md).

> [!NOTE]
> Análise de código ignora `GeneratedCodeAttribute` quando ele é aplicado a um assembly inteiro ou um único parâmetro.

## <a name="global-level-suppressions"></a>Supressões no nível global

A ferramenta de análise de código gerenciado examina `SuppressMessage` atributos que são aplicados no nível do assembly, módulo, tipo, membro ou parâmetro. Também é acionado violações em relação a recursos e namespaces. Essas violações deve ser aplicadas no nível global no escopo e são direcionadas. Por exemplo, a seguinte mensagem suprime uma violação de namespace:

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> Quando você suprime um aviso com escopo de namespace, ele suprime o aviso em relação ao namespace em si. Ele não suprime o aviso em relação aos tipos no namespace.

Qualquer supressão pode ser expressos com a especificação de um escopo explícito. Esses supressões devem residir no nível global. Você não pode especificar a supressão de nível de membro decorando um tipo.

Supressões no nível global são a única maneira de suprimir as mensagens que se referem ao código gerado pelo compilador que não é mapeado para a fonte de usuário fornecido explicitamente. Por exemplo, o código a seguir suprime uma violação em relação a um construtor emitidos pelo compilador:

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` sempre contém o nome totalmente qualificado do item.

## <a name="global-suppression-file"></a>Arquivo de supressão global

O arquivo de supressão global mantém supressões supressões no nível global ou supressões que não especificam um destino. Por exemplo, supressões quanto a violações de nível de assembly são armazenadas nesse arquivo. Além disso, alguns supressões de ASP.NET são armazenadas nesse arquivo, porque as configurações de nível de projeto não estão disponíveis para o código por trás de um formulário. Um arquivo de supressão global é criado e adicionado ao seu projeto na primeira vez que você selecione o **no arquivo de supressão do projeto** opção do **suprimir** comando o **Error List**janela.

## <a name="see-also"></a>Consulte também

- <xref:System.Diagnostics.CodeAnalysis>
- [Usar os analisadores de Roslyn](../code-quality/use-roslyn-analyzers.md)