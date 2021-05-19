---
title: Suprimir violações da análise de código
ms.date: 05/10/2021
description: Saiba como suprimir violações de análise de código Visual Studio. Entenda como usar o atributo SuppressMessageAttribute para supressão na origem.
ms.custom: SEO-VS-2020
ms.topic: conceptual
helpviewer_keywords:
- source suppression, code analysis
- code analysis, source suppression
author: mikadumont
ms.author: midumont
manager: jmartens
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.openlocfilehash: fd177a96b8789760927933fad5c0320553a72f57
ms.sourcegitcommit: 162be102d2c22a1c4ad2c447685abd28e0e85d15
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2021
ms.locfileid: "109973324"
---
# <a name="suppress-code-analysis-violations"></a>Suprimir violações da análise de código

Geralmente, é útil indicar que um aviso não é aplicável. Isso indica aos membros da equipe que o código foi revisado e que o aviso pode ser suprimido. Este artigo descreve as diferentes maneiras de suprimir violações de análise de código usando o Visual Studio IDE.

::: moniker range=">=vs-2019"

## <a name="suppress-violations-using-the-editorconfig-file"></a>Suprimir violações usando o arquivo EditorConfig

Em um **arquivo EditorConfig**, de definido a severidade como `none` , por exemplo, `dotnet_diagnostic.CA1822.severity = none` . Para adicionar um arquivo EditorConfig, consulte [Adicionar um arquivo EditorConfig a um projeto](../ide/create-portable-custom-editor-options.md#add-and-remove-editorconfig-files).

::: moniker-end

## <a name="suppress-violations-in-source-code"></a>Suprimir violações no código-fonte

Você pode suprimir violações no código usando uma diretiva de pré-processador, a diretiva [#pragma warning (C#)](/dotnet/csharp/language-reference/preprocessor-directives.md#pragma-warning) ou [Disable (Visual Basic)](/dotnet/visual-basic/language-reference/directives/disable-enable.md) para suprimir o aviso apenas para uma linha de código específica. Ou você pode usar o [atributo SuppressMessage](#in-source-suppression-and-the-suppressmessage-attribute).

- No **editor de código**

  Coloque o cursor na linha de código com a violação e pressione **Ctrl** + **Period (.)** para abrir o menu **Ações Rápidas.** Selecione **Suprimir CAXXXX** e escolha em **Origem** ou **em Origem (atributo).**

  Se você escolher **em Origem**, verá uma visualização da diretiva de pré-processador que será adicionada ao seu código.

  ::: moniker range="vs-2017"
  :::image type="content" source="media/suppress-diagnostic-from-editor.png" alt-text="Suprimir o diagnóstico do menu ações rápidas":::
  ::: moniker-end
  ::: moniker range=">=vs-2019"
  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor.png" alt-text="Suprimir o diagnóstico do menu ações rápidas":::

  Se você escolher **em Origem (atributo),** verá uma visualização do atributo [SuppressMessage](#in-source-suppression-and-the-suppressmessage-attribute) que será adicionada ao seu código.

  :::image type="content" source="media/vs-2019/suppress-diagnostic-from-editor-attribute.png" alt-text="Suprimir o diagnóstico do menu de ações rápidas usando o atributo":::
  ::: moniker-end

- Na lista **de erros**

  Selecione as regras que você deseja suprimir e clique com o botão direito do mouse e selecione **suprimir**  >  **na origem**.

  - Se você suprimir **na origem**, a caixa de diálogo **Visualizar alterações** será aberta e mostrará uma visualização do [aviso de #pragma](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) do C# ou Visual Basic diretiva de [aviso de #Disable](/dotnet/visual-basic/language-reference/directives/directives) que é adicionada ao código-fonte.

    ![Visualização da adição de #pragma Aviso no arquivo de código](media/pragma-warning-preview.png)

  Na caixa de diálogo **Visualizar alterações** , selecione **aplicar**.

  > [!NOTE]
  > Se você não vir a opção de menu **suprimir** em **Gerenciador de soluções**, a violação provavelmente será proveniente da compilação e não da análise dinâmica. O **lista de erros** exibe diagnósticos ou violações de regra, tanto da análise de código ao vivo quanto da compilação. Como o diagnóstico de compilação pode ser obsoleto, por exemplo, se você tiver editado o código para corrigir a violação, mas não tiver recriado, não poderá suprimir esses diagnósticos do **lista de erros**. Os diagnósticos da análise ao vivo ou do IntelliSense estão sempre atualizados com as fontes atuais e podem ser suprimidos no **lista de erros**. Para excluir o diagnóstico de *compilação* da sua seleção, alterne o filtro de origem **lista de erros** do **Build + IntelliSense** **somente para IntelliSense**. Em seguida, selecione o diagnóstico que você deseja suprimir e continue conforme descrito anteriormente.
  >
  > ![Lista de Erros filtro de origem no Visual Studio](media/error-list-filter.png)

## <a name="suppress-violations-using-a-global-suppression-file"></a>Suprimir violações usando um arquivo de supressão global

O [arquivo de supressão global](#global-level-suppressions) usa o [atributo SuppressMessage](#in-source-suppression-and-the-suppressmessage-attribute).

- No **lista de erros**, selecione as regras que você deseja suprimir e, em seguida, clique com o botão direito do mouse e selecione **suprimir**  >  **no arquivo de supressão**. A caixa de diálogo **Visualizar alterações** é aberta e mostra uma visualização do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo que é adicionado ao arquivo de supressões global.

  ![Visualização da adição do atributo SuppressMessage ao arquivo de supressão](media/preview-changes-in-suppression-file.png)

- No **editor** de códigos, coloque o cursor na linha de código com a violação e pressione Ações e redatorações rápidas (ou pressione **Período Ctrl**(.) para abrir o menu Ações **Rápidas.** +   Selecione **Suprimir CAXXXX** e escolha **em Suprimir Arquivo**. Você verá uma visualização do [arquivo de supressão global](#global-level-suppressions) que será criado ou modificado.

::: moniker range=">=vs-2019"

- No menu **Analisar,** selecione **Analisar**  >  **Build e Suprimir Problemas Ativos** na barra de menus para suprimir todas as violações atuais. Às vezes, isso é chamado de "baselining".

::: moniker-end
::: moniker range="vs-2017"

- No menu **Analisar,** selecione **Analisar** Executar Code Analysis e Suprimir Problemas Ativos na barra de menus para  >   suprimir todas as violações atuais. Às vezes, isso é chamado de "baselining".
::: moniker-end

## <a name="suppress-violations-using-project-settings"></a>Suprimir violações usando configurações de projeto

No Gerenciador de Soluções , abra as propriedades do projeto (clique com  o botão direito do mouse no projeto e escolha Propriedades **(ou** pressione **Alt + Enter)** e use a guia **Code Analysis** para configurar opções. Por exemplo, você pode desabilitar a análise de código ao vivo ou desabilitar analisadores .NET.

## <a name="suppress-violations-using-a-rule-set"></a>Suprimir violações usando um conjunto de regras

No **editor do conjunto de** regras , des marque a caixa de seleção ao lado de seu nome ou des marque **Ação** como **Nenhum.**

## <a name="in-source-suppression-and-the-suppressmessage-attribute"></a>Supressão na origem e o atributo SuppressMessage

A supressão na origem (ISS) usa o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo para suprimir um aviso. O atributo pode ser colocado próximo ao segmento de código que gerou o aviso. Você pode adicionar o atributo ao arquivo de origem digitando-o ou pode usar o menu de atalho em um aviso na Lista de Erros para adicioná-lo <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> automaticamente. 

O atributo é um atributo condicional, que é incluído nos metadados IL do assembly de código gerenciado, somente se o símbolo de compilação CODE_ANALYSIS for definido no <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> tempo de compilação.

No C++/CLI, use as macros AC SUPPRESS MESSAGE ou CA GLOBAL SUPPRESS_MESSAGE no arquivo \_ \_ de \_ \_ header para adicionar o atributo.

> [!NOTE]
> Você não deve usar supressões na origem em builds de versão, para evitar o envio acidental dos metadados de supressão na origem. Além disso, devido ao custo de processamento da supressão na origem, o desempenho do seu aplicativo pode ser degradado.

::: moniker range="vs-2017"

> [!NOTE]
> Se você migrar um projeto para o Visual Studio 2017, poderá, de repente, enfrentar um grande número de avisos de análise de código. Se você não estiver pronto para corrigir os avisos, poderá suprimir todos eles selecionando **analisar**  >  **executar análise de código e suprimir problemas ativos**.
>
> ![Executar análise de código e suprimir problemas no Visual Studio](media/suppress-active-issues.png)

::: moniker-end

::: moniker range=">=vs-2019&quot;

> [!NOTE]
> Se você migrar um projeto para o Visual Studio 2019, poderá, de repente, enfrentar um grande número de avisos de análise de código. Se você não estiver pronto para corrigir os avisos, poderá suprimir todos eles selecionando **analisar**  >  **Compilar e suprimir problemas ativos**.

::: moniker-end

### <a name=&quot;suppressmessage-attribute&quot;></a>Atributo SuppressMessage

Quando você seleciona **suprimir** no menu de contexto ou clique com o botão direito do mouse em um aviso de análise de código na **lista de erros**, um <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo é adicionado no código ou no arquivo de supressão global do projeto.

O <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo tem o seguinte formato:

```vb
<Scope:SuppressMessage(&quot;Rule Category&quot;, &quot;Rule Id&quot;, Justification = &quot;Justification&quot;, MessageId = &quot;MessageId&quot;, Scope = &quot;Scope&quot;, Target = &quot;Target")>
```

```csharp
[Scope:SuppressMessage("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")]
```

```cpp
CA_SUPPRESS_MESSAGE("Rule Category", "Rule Id", Justification = "Justification", MessageId = "MessageId", Scope = "Scope", Target = "Target")
```

As propriedades do atributo incluem:

- **Categoria** – a categoria na qual a regra é definida. Para obter mais informações sobre categorias de regra de análise de código, consulte [avisos de código gerenciado](/dotnet/fundamentals/code-analysis/quality-rules/index).

- **CheckId** -o identificador da regra. O suporte inclui um nome curto e longo para o identificador de regra. O nome curto é CAXXXX; o nome longo é CAXXXX: FriendlyTypeName.

- **Justificação** – o texto que é usado para documentar o motivo da supressão da mensagem.

- **MessageId** -identificador exclusivo de um problema para cada mensagem.

- **Escopo** -o destino no qual o aviso está sendo suprimido. Se o destino não for especificado, ele será definido como o destino do atributo. Os [escopos](xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope) com suporte incluem o seguinte:

  - [`module`](#module-suppression-scope) – Esse escopo suprime avisos em relação a um assembly. É uma supressão global que se aplica a todo o projeto.

  - `resource` - ([somente FxCop](../code-quality/static-code-analysis-for-managed-code-overview.md) herdado) Esse escopo suprime avisos em informações de diagnóstico gravados em arquivos de recurso que fazem parte do módulo (assembly). Esse escopo não é lido/respeitado nos compiladores C#/VB para diagnóstico do analisador Roslyn, que analisa apenas os arquivos de origem.

  - `type` – Esse escopo suprime avisos em relação a um tipo.

  - `member` – Esse escopo suprime avisos em relação a um membro.

  - `namespace` – Esse escopo suprime avisos no próprio namespace. Ele não suprime avisos contra tipos dentro do namespace.

  - `namespaceanddescendants` - (Requer o compilador versão 3.x ou superior e Visual Studio 2019) Esse escopo suprime avisos em um namespace e todos os seus símbolos descendentes. O `namespaceanddescendants` valor é ignorado pela análise herdada.

- **Destino** – um identificador usado para especificar o destino no qual o aviso está sendo suprimido. Ele deve conter um nome de item totalmente qualificado.

Quando você vir avisos Visual Studio, poderá exibir exemplos de adicionando uma supressão ao `SuppressMessage` [arquivo de supressão global](../code-quality/use-roslyn-analyzers.md#suppress-violations). O atributo de supressão e suas propriedades necessárias aparecem em uma janela de visualização.

### <a name="suppressmessage-usage"></a>Uso de SuppressMessage

Code Analysis avisos são suprimidos no nível ao qual o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo é aplicado. Por exemplo, o atributo pode ser aplicado no nível de assembly, módulo, tipo, membro ou parâmetro. A finalidade disso é a adoção rígida das informações de supressão ao código em que a violação ocorre.

A forma geral de supressão inclui a categoria de regra e um identificador de regra, que contém uma representação opcional acessível por humanos do nome da regra. Por exemplo:

`[SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]`

Se houver motivos estritos de desempenho para minimizar os metadados de supressão na origem, o nome da regra poderá ser omitido. A categoria de regra e sua ID de regra juntos constituem um identificador de regra suficientemente exclusivo. Por exemplo:

`[SuppressMessage("Microsoft.Design", "CA1039")]`

Para fins de manutenção, omitir o nome da regra não é recomendado.

### <a name="suppress-selective-violations-within-a-method-body"></a>Suprimir violações seletivas dentro de um corpo de método

Atributos de supressão podem ser aplicados a um método, mas não podem ser inseridos dentro de um corpo de método. Isso significa que todas as violações de uma regra específica serão suprimidas se você adicionar o <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo ao método.

Em alguns casos, talvez você queira suprimir uma instância específica da violação, por exemplo, para que o código futuro não seja automaticamente isento da regra de análise de código. Determinadas regras de análise de código permitem que você faça isso usando a `MessageId` Propriedade do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo. Em geral, as regras herdadas para violações em um determinado símbolo (uma variável local ou parâmetro) respeitam a `MessageId` propriedade. [CA1500: VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) é um exemplo dessa regra. No entanto, as regras herdadas para violações no código executável (não símbolo) não respeitam a `MessageId` propriedade. Além disso, os analisadores de .NET Compiler Platform ("Roslyn") não respeitam a `MessageId` propriedade.

Para suprimir uma violação de símbolo específica de uma regra, especifique o nome do símbolo para a `MessageId` Propriedade do <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> atributo. O exemplo a seguir mostra o código com duas violações de [CA1500: VariableNamesShouldNotMatchFieldNames](../code-quality/ca1500.md) &mdash; uma para a `name` variável e outra para a `age` variável. Somente a violação do `age` símbolo é suprimida.

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

### <a name="global-level-suppressions"></a>Supressões de nível global

A ferramenta de análise de código gerenciado examina `SuppressMessage` os atributos que são aplicados no nível do assembly, módulo, tipo, membro ou parâmetro. Ele também dispara violações em relação a recursos e namespaces. Essas violações devem ser aplicadas no nível global e têm escopo e destino. Por exemplo, a seguinte mensagem suprime uma violação de namespace:

`[module: SuppressMessage("Microsoft.Design", "CA1020:AvoidNamespacesWithFewTypes", Scope = "namespace", Target = "MyNamespace")]`

> [!NOTE]
> Quando você suprimi um aviso com `namespace` escopo, ele suprime o aviso em relação ao próprio namespace. Ele não suprime o aviso em relação aos tipos dentro do namespace.

Qualquer supressão pode ser expressa especificando um escopo explícito. Essas supressões devem residir no nível global. Não é possível especificar a supressão no nível do membro decorando um tipo.

As supressões de nível global são a única maneira de suprimir mensagens que se referem ao código gerado pelo compilador que não é mapeado para a fonte de usuário fornecida explicitamente. Por exemplo, o código a seguir suprime uma violação contra um construtor emitido pelo compilador:

`[module: SuppressMessage("Microsoft.Design", "CA1055:AbstractTypesDoNotHavePublicConstructors", Scope="member", Target="Microsoft.Tools.FxCop.Type..ctor()")]`

> [!NOTE]
> `Target` sempre contém o nome do item totalmente qualificado.

#### <a name="global-suppression-file"></a>Arquivo de supressão global

O arquivo de supressão global mantém supressões que são supressões de nível global ou supressões que não especificam um destino. Por exemplo, as supressões para violações no nível do assembly são armazenadas nesse arquivo. Além disso, algumas ASP.NET supressões são armazenadas nesse arquivo porque as configurações no nível do projeto não estão disponíveis para código por trás de um formulário. Um arquivo de supressão global é criado e adicionado ao seu projeto na primeira vez que você seleciona a opção **No** Arquivo de Supressão de Projeto do comando **Suprimir** na janela **Lista de** Erros.

#### <a name="module-suppression-scope"></a>Escopo de supressão de módulo

Você pode suprimir violações de qualidade de código para todo o assembly usando o escopo **do** módulo.

Por exemplo, o seguinte atributo em seu arquivo de projeto _GlobalSuppressions_ suprimirá a violação ConfigureExpressit para um projeto ASP.NET Core:

`[assembly: System.Diagnostics.CodeAnalysis.SuppressMessage("Reliability", "CA2007:Consider calling ConfigureAwait on the awaited task", Justification = "ASP.NET Core doesn't use thread context to store request context.", Scope = "module")]`

### <a name="generated-code"></a>Código gerado

Compiladores de código gerenciado e algumas ferramentas de terceiros geram código para facilitar o desenvolvimento rápido de código. O código gerado pelo compilador que aparece nos arquivos de origem geralmente é marcado com o `GeneratedCodeAttribute` atributo .

Para análise de código-fonte, você pode suprimir mensagens no código gerado em um `.editorconfig` arquivo. Para obter mais informações, consulte [Excluir código gerado.](/dotnet/fundamentals/code-analysis/configuration-options#exclude-generated-code)

Para a análise de código herdado, você pode escolher se deseja suprimir avisos de análise de código e erros de código gerado. Para obter informações sobre como suprimir esses avisos e erros, consulte [como suprimir avisos para código gerado](../code-quality/how-to-suppress-code-analysis-warnings-for-generated-code.md).

> [!NOTE]
> A análise de código ignora `GeneratedCodeAttribute` quando é aplicada a um assembly inteiro ou a um único parâmetro.

## <a name="see-also"></a>Confira também

- <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute.Scope>
- <xref:System.Diagnostics.CodeAnalysis>
- [Usar analisadores de código](../code-quality/use-roslyn-analyzers.md)
