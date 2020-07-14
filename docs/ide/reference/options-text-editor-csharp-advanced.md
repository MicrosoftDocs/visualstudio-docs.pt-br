---
title: Opções, Editor de Texto, C#, Avançado
ms.date: 01/16/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.CSharp.Outlining
- VS.ToolsOptionsPages.Text_Editor.CSharp.Advanced
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ff42473c6f56d69a56cfbd811f2687ba544c7c5e
ms.sourcegitcommit: 4d932000a0f7e79c9475fe66c02fe9addcd7e47a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86181060"
---
# <a name="options-text-editor-c-advanced"></a>Opções, Editor de Texto, C#, Avançado

Use a página de opções **Avançado** para modificar as configurações de formatação do editor, de refatoração de código e de comentários da documentação XML para C#. Para acessar essa página de opções, escolha **ferramentas**  >  **Opções**e, em seguida, escolha **Editor de texto**  >  **C#**  >  **avançado**.

> [!NOTE]
> É possível que nem todas as opções estejam listadas aqui.

## <a name="analysis"></a>Análise

- Análise de código ao vivo ou escopo de análise em segundo plano

   Configure o escopo de análise em segundo plano para código gerenciado. Para obter mais informações, consulte [como: configurar o escopo de análise de código ao vivo para código gerenciado](../../code-quality/configure-live-code-analysis-scope-managed-code.md).

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
- Sugerir o uso de tipos em assemblies de .NET Framework
::: moniker-end
                                         
::: moniker range="vs-2017"                                                
- Sugerir usos para tipos em assemblies de referência
::: moniker-end                                                            

- Sugerir usos para tipos em pacotes NuGet

   Quando essas opções estiverem selecionadas, uma [Ação Rápida](../quick-actions.md) estará disponível para instalar um pacote NuGet e para adicionar uma diretiva `using` para tipos não referenciados.

   ![Ação rápida para instalar o pacote NuGet no Visual Studio](media/nuget-lightbulb.png)

## <a name="highlighting"></a>Realce

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

Marque essas caixas de seleção para exibir linhas verticais pontilhadas entre chaves ( **{}** ) em seu código. Isso permite que você veja facilmente blocos individuais de código para o seu nível de declaração e construções no nível do código.

## <a name="editor-help"></a>Ajuda do Editor

- Gerar comentários da documentação XML para ///

   Quando selecionado, insere os elementos XML dos comentários da documentação XML depois que você digita a introdução de comentário `///`. Para obter mais informações sobre a documentação XML, confira [Comentários da documentação XML (Guia de Programação em C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments).

## <a name="see-also"></a>Veja também

- [Como inserir comentários XML para geração de documentação](../../ide/reference/generate-xml-documentation-comments.md)
- [Comentários de documentação XML (guia de programação C#)](/dotnet/csharp/programming-guide/xmldoc/xml-documentation-comments)
- [Documentar o código com comentários XML (guia do C#)](/dotnet/csharp/codedoc)
- [Definir opções do editor específicas a um idioma](../../ide/reference/setting-language-specific-editor-options.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
