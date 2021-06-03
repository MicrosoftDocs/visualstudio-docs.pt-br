---
title: Opções, Editor de Texto, C#, Avançado
description: Saiba como usar a página Avançado na seção C# para modificar as configurações de formatação do editor, a refactoração de código e os comentários de documentação XML para C#.
ms.custom: SEO-VS-2020
ms.date: 06/01/2021
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
author: mikadumont
ms.author: midumont
manager: jmartens
ms.workload:
- dotnet
ms.openlocfilehash: 29f6dd2b4a101132bc7bc19664c51fd5d4b8283e
ms.sourcegitcommit: f50bbdb15c4f9fca0fa245ca765183c378960cc5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/03/2021
ms.locfileid: "111351976"
---
# <a name="options-text-editor-c-advanced"></a>Opções, Editor de Texto, C#, Avançado

Use a página de opções **Avançado** para modificar as configurações de formatação do editor, de refatoração de código e de comentários da documentação XML para C#. Para acessar essa página de opções, escolha **Opções**  >  **de** Ferramentas e, em seguida, escolha **Editor de Texto**  >  **C#**  >  **Avançado.**

> [!NOTE]
> É possível que nem todas as opções estejam listadas aqui.

## <a name="analysis"></a>Análise

- Análise de código ao vivo ou escopo de análise em segundo plano

   Configure o escopo da análise em segundo plano para o código gerenciado. Para obter mais informações, [consulte Como configurar o escopo de análise de código ao vivo para código gerenciado.](../../code-quality/configure-live-code-analysis-scope-managed-code.md)

## <a name="using-directives"></a>Usando diretivas

- Colocar as diretivas “System” primeiro ao classificar os usos

   Quando selecionado, o comando **Remover e classificar usos** no menu de clique com o botão direito do mouse classifica as diretivas `using` e coloca os namespaces "System" no topo da lista.

   Antes da classificação:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   Após a classificação:

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using AutoMapper;
   using FluentValidation;
   using Newtonsoft.Json;
   ```

- Separar usando grupos de diretivas

   Quando selecionado, o comando **Remover e classificar usos** no menu de clique com o botão direito do mouse separa as diretivas `using` inserindo uma linha vazia entre os grupos de diretivas que têm o mesmo namespace de raiz.

   Antes da classificação:

   ```csharp
   using AutoMapper;
   using FluentValidation;
   using System.Collections.Generic;
   using System.Linq;
   using Newtonsoft.Json;
   using System;
   ```

   Após a classificação:

   ```csharp
   using AutoMapper;

   using FluentValidation;

   using Newtonsoft.Json;

   using System;
   using System.Collections.Generic;
   using System.Linq;
   ```

::: moniker range=">=vs-2019"                                              
- Sugerir usos para tipos em .NET Framework assemblies
::: moniker-end
                                         
::: moniker range="vs-2017"                                                
- Sugerir usos para tipos em assemblies de referência
::: moniker-end                                                            

- Sugerir usos para tipos em pacotes NuGet

   Quando essas opções estiverem selecionadas, uma [Ação Rápida](../quick-actions.md) estará disponível para instalar um pacote NuGet e para adicionar uma diretiva `using` para tipos não referenciados.

   ![Ação rápida para instalar o pacote NuGet no Visual Studio](media/nuget-lightbulb.png)

- Adicionar diretivas using ausentes quando colar

    Quando essa opção for selecionada, as diretivas serão adicionadas automaticamente ao código quando `using` você colar um tipo em um arquivo.

## <a name="highlighting"></a>Realçar

- Realçar referências a símbolo sob o cursor

   Quando o cursor é posicionado em um símbolo, ou ao clicar em um símbolo, todas as instâncias desse símbolo no arquivo de código são realçadas.

## <a name="outlining"></a>Estrutura de tópicos

- Entrar no modo de estrutura de tópicos quando os arquivos forem abertos

   Quando selecionado, descreve o arquivo de código automaticamente, o que cria blocos de código recolhíveis. Na primeira vez que um arquivo é aberto, blocos #regions e blocos de códigos inativos são recolhidos.

- Mostrar separadores de linha de procedimento

   O editor de texto indica o escopo visual dos procedimentos. Uma linha é desenhada nos arquivos de origem *.cs* do seu projeto nos locais listados na tabela a seguir:

   |Local no arquivo de origem .cs|Exemplo de local da linha|
   |---------------------------------|------------------------------|
   |Após o encerramento de um constructo de declaração de bloco|–   No final de uma classe, estrutura, módulo, interface ou enumeração<br />–   Depois de uma propriedade, função ou sub<br />–   Não entre cláusulas get e set em uma propriedade|
   |Depois de um conjunto de constructos de linha única|–   Depois das instruções de importação, antes de uma definição de tipo em um arquivo de classe<br />–   Depois de variáveis declaradas em uma classe, antes de qualquer procedimento|
   |Depois de declarações de linha única (declarações de nível não de bloco)|–   Após instruções de importação, instruções de herdar, declarações de variável, declarações de evento, declarações de delegado e instruções de declaração DLL|

## <a name="block-structure-guides"></a>Guias de estrutura de bloco

Marque essas caixas de seleção para exibir linhas verticais pontilhadas entre os colchetes ( **{}** ) em seu código. Isso permite que você veja facilmente blocos individuais de código para o seu nível de declaração e construções no nível do código.

## <a name="comments"></a>Comentários

- Gerar comentários da documentação XML para ///

   Quando selecionado, insere os elementos XML dos comentários da documentação XML depois que você digita a introdução de comentário `///`. Para obter mais informações sobre a documentação XML, confira [Comentários da documentação XML (Guia de Programação em C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments).

::: moniker range=">=vs-2019"

## <a name="inline-hints"></a>Dicas em linha

- Dicas de Nome de Parâmetro Embutido 
    
    Quando selecionado, insere dicas de nome de parâmetro para literais, literais de cast e instações de objeto antes de cada argumento em chamadas de função.  
    
    ![Dicas de nome de parâmetro em linha para CSharp](media/inline-parameter-name-hints-csharp.png)

- Dicas de tipo em linha 
    
    Quando selecionada, insere dicas de tipo para variáveis com tipos inferidos e tipos de parâmetro lambda.  
    
    ![Dicas de tipo em linha para CSharp](media/inline-type-hints-csharp.png)

## <a name="inheritance-margin"></a>Margem de herança 

- Quando selecionado, adiciona ícones às margens que representam as implementações e substituições do código. Clicar nos ícones de margem de herança exibirá opções de herança que você pode selecionar para navegar.

    ![Margem de herança](media/inheritance-margin.png)

::: moniker-end

## <a name="see-also"></a>Confira também

- [Como inserir comentários XML para geração de documentação](../../ide/reference/generate-xml-documentation-comments.md)
- [Comentários de documentação XML (Guia de Programação em C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [Documentar o código com comentários XML (guia do C#)](/dotnet/csharp/codedoc)
- [Definir opções do editor específicas a um idioma](../../ide/reference/setting-language-specific-editor-options.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
