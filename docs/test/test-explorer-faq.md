---
title: Perguntas frequentes sobre o Gerenciador de Testes do Visual Studio
ms.date: 11/07/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Test Explorer
- Test window
- Visual Studio Test Explorer
- summary line
- unit tests
- Test Explorer FAQ
ms.author: kehavens
ms.workload:
- multiple
author: kendrahavens
manager: douge
ms.openlocfilehash: 49df84c5e852cfc282b6d679faf621669cf08148
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296327"
---
# <a name="visual-studio-test-explorer-faq"></a>Perguntas frequentes sobre o Gerenciador de Testes do Visual Studio

## <a name="dynamic-test-discovery"></a>Detecção de testes dinâmica

**O Gerenciador de Testes não está detectando meus testes definidos dinamicamente. (Por exemplo, teorias, adaptadores personalizados, características personalizadas, #ifdefs, etc.) Como faço para descobrir estes testes?**

  Compile o projeto e verifique se a descoberta baseada em assembly está ativada em **Ferramentas** > **Opções** > **Teste**.

  A [Detecção de testes em tempo real](https://go.microsoft.com/fwlink/?linkid=862824) é a detecção de testes baseada na origem. Ela não consegue detectar testes que usam teorias, adaptadores personalizados, características personalizadas, instruções `#ifdef`, entre outros, porque esses itens são definidos em tempo de execução. Um build é necessário para que esses testes sejam localizados com precisão. No Visual Studio 2017 versão 15.6 e posteriores, a descoberta baseada em assembly (o detector tradicional) é executada somente depois dos builds. Essa configuração significa que a detecção de testes em tempo real localiza o máximo de testes possível enquanto você está editando e a descoberta baseada em assembly permite que os testes definidos dinamicamente apareçam após um build. A detecção de testes em tempo real melhora a capacidade de resposta, mas ainda permite que você obtenha resultados completos e precisos após um build.

## <a name="test-explorer--plus-symbol"></a>Sinal de "+" (adição) do Gerenciador de Testes

**O que significa o "+" (sinal de adição) exibido na linha superior do Gerenciador de Testes?**

  O '+' (sinal de adição) indica que mais testes poderão ser detectados após um build se a detecção baseada em assembly estiver ativada. Esse símbolo será exibido quando forem detectados testes definidos dinamicamente no projeto.

  ![Linha de resumo do sinal de adição](media/testex-plussymbol.png)

## <a name="assembly-based-discovery"></a>Descoberta baseada em assembly

**A descoberta baseada em assembly não está mais funcionando no meu projeto. Como faço para ativá-la novamente?**

  Acesse **Ferramentas** > **Opções** > **Teste** e marque a caixa **Adicionalmente, descobrir testes de assemblies compilados após builds.**

  ![Opção baseada em assembly](media/testex-toolsoptions.png)

## <a name="real-time-test-discovery"></a>Detecção de testes em tempo real

**Agora os testes são exibidos no Gerenciador de Testes enquanto digito, sem a necessidade de compilar o projeto. O que mudou?**

  Esse recurso é chamado de [Detecção de testes em tempo real](https://go.microsoft.com/fwlink/?linkid=862824). Ele usa um analisador Roslyn para encontrar testes e popular o Gerenciador de Testes em tempo real, sem exigir que você compile o projeto. Para obter mais informações sobre o comportamento da detecção de testes para testes definidos dinamicamente, como teorias ou características personalizadas, confira a Pergunta frequente nº 1.

## <a name="real-time-test-discovery-compatibility"></a>Compatibilidade da detecção de testes em tempo real

**Quais linguagens e estruturas de teste podem usar a detecção de testes em tempo real?**

  A [Detecção de testes em tempo real](https://go.microsoft.com/fwlink/?linkid=862824) só funciona em linguagens gerenciadas (C# e Visual Basic), pois é compilada com o compilador Roslyn. Por enquanto, a detecção de testes em tempo real só funciona para as estruturas xUnit, NUnit e MSTest.

## <a name="test-explorer-logs"></a>Logs do Gerenciador de Testes

**Como faço para ativar logs no Gerenciador de Testes?**

  Navegue para **Ferramentas** > **Opções** > **Teste** e localize a seção Log.

## <a name="uwp-test-discovery"></a>Detecção de testes da UWP

**Por que meus testes em projetos UWP não são detectados enquanto eu não implanto o aplicativo?**

  Os testes UWP têm como destino um tempo de execução diferente quando o aplicativo é implantado. Isso significa que para encontrar testes com precisão em projetos UWP, além de compilar seu projeto, você também precisa implantá-lo.

## <a name="test-explorer-sorting"></a>Classificação do Gerenciador de Testes

**Como funciona a classificação de resultados de teste no modo de exibição de hierarquia?**

  O modo de exibição de hierarquia classifica os testes em ordem alfabética e não por resultado. As outras configurações de agrupamento normalmente classificam os resultados de teste por resultado e, em seguida, em ordem alfabética. Veja o grupo diferente pelas opções na imagem a seguir para comparação. Você pode fornecer comentários sobre o design [neste assunto do GitHub](https://github.com/Microsoft/vstest/issues/1425).

  ![SortingExamples](media/testex-sortingex.png)

## <a name="test-explorer-hierarchy-view"></a>Modo de exibição da hierarquia do Gerenciador de Testes

**No modo de exibição de hierarquia, há ícones passados, com falha, ignorados e não executados ao lado dos agrupamentos Projeto, Namespace e Classe. O que esses ícones significam?**

  Os ícones ao lado dos agrupamentos Projeto, Namespace e Classe mostram o estado dos testes nesse agrupamento. Consulte a tabela a seguir.

  ![Ícones de Hierarquia do Gerenciador de Testes](media/testex-hierarchyicons.png)

## <a name="search-by-file-path"></a>Pesquisar por caminho do arquivo

**Não existe mais um filtro de "caminho do arquivo" na caixa de pesquisa do Gerenciador de Testes.**

O filtro de caminho de arquivo na caixa de pesquisa do **Gerenciador de Testes** foi removida na versão prévia 3 da versão 15.7 do Visual Studio 2017. Esse recurso tinha pouco uso e o Gerenciador de Testes consegue recuperar os métodos de teste com mais rapidez ao excluir esse recurso. Se essa alteração interromper seu fluxo de desenvolvimento, informe-nos enviando comentários na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/).

## <a name="remove-undocumented-interfaces"></a>Remover interfaces não documentadas

**Algumas APIs relacionadas a teste não estão mais presentes no Visual Studio 2019. O que mudou?**

No Visual Studio 2019, serão removidas algumas APIs de janela de teste que foram marcadas como públicas anteriormente, mas nunca foram documentadas oficialmente. Elas foram marcadas como "preteridas" no Visual Studio 2017 para fornecer um aviso antecipado aos mantenedores de extensão. Para o nosso conhecimento, muito poucas extensões haviam encontrado essas APIs e criado uma dependência delas. Elas incluem `IGroupByProvider`, `IGroupByProvider<T>`, `KeyComparer`, `ISearchFilter`, `ISearchFilterToken`, `ISearchToken` e `SearchFilterTokenType`. Se essa alteração afetar sua extensão, fale conosco enviando um bug na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com).

## <a name="test-adapter-nuget-reference"></a>Referência ao NuGet do adaptador de teste

**No Visual Studio 2017, versão 15.8, meus testes são detectados, mas não são executados**.

Todos os projetos de teste devem incluir a referência ao NuGet do adaptador de teste do .NET no arquivo .csproj. Caso contrário, a saída desse teste será exibida no projeto se a detecção por uma extensão do adaptador de teste for iniciada após um build, ou se o usuário tentar executar os testes selecionados:

O **projeto de teste{} não faz referência a nenhum adaptador do NuGet do .NET. A execução ou a detecção de testes pode não funcionar para esse projeto. Recomendamos fazer referencia aos adaptadores de teste do NuGet em cada projeto de teste do .NET na solução.**

Em vez de usar extensões do adaptador de teste, os projetos são solicitados a usar os pacotes do adaptador de teste do NuGet. Esse requisito melhora bastante o desempenho e causa menos problemas com a integração contínua. Leia mais sobre a substituição da extensão do adaptador de teste do .NET nas [notas de versão](/visualstudio/releasenotes/vs2017-preview-relnotes#testadapterextension).

> [!NOTE]
> Se estiver usando o Adaptador de teste NUnit 2 e não puder migrar para o adaptador de teste NUnit 3, você poderá desativar esse novo comportamento de descoberta no Visual Studio versão 15.8 em **Ferramentas** > **Opções** > **Teste**.

  ![Comportamento do Adaptador do Gerenciador de Testes nas opções de ferramentas](media/testex-adapterbehavior.png)

## <a name="uwp-testcontainer-was-not-found"></a>O TestContainer do UWP não foi encontrado

**Meus testes do UWP não estão mais sendo executadas no Visual Studio 2017 versão 15.7 e posteriores.**

Projetos de teste do UWP recentes especificam uma propriedade de build da plataforma de teste que permite um melhor desempenho para identificar aplicativos de teste. Se um projeto de teste da UWP for inicializado antes do Visual Studio versão 15.7, o seguinte erro poderá aparecer em **Saída** > **Testes**:

**System.AggregateException: Um ou mais erros ocorreram. ---> System.InvalidOperationException: O seguinte TestContainer não foi encontrado {} em Microsoft.VisualStudio.TestWindow.Controller.TestContainerProvider <GetTestContainerAsync>d__61.MoveNext()**
  
Para corrigir esse erro:

- Atualize a propriedade de build do projeto de teste usando o seguinte código:

```XML
<UnitTestPlatformVersion Condition="'$(UnitTestPlatformVersion)' == ''">$(VisualStudioVersion)</UnitTestPlatformVersion>
```

- Atualize a versão do SDK da TestPlatform usando o seguinte código:

```XML
<SDKReference Include="TestPlatform.Universal, Version=$(UnitTestPlatformVersion)" />
```

## <a name="using-feature-flags"></a>Como usar sinalizadores de recursos

**Como faço para ativar sinalizadores de recursos para experimentar os novos recursos de teste?**

Sinalizadores de recursos são usados para enviar partes experimentais ou incompletas do produto para usuários ávidos que gostariam de fazer comentários antes que os recursos sejam fornecidos oficialmente. Eles podem desestabilizar a experiência de IDE. Use-os somente em ambientes de desenvolvimento seguros, como máquinas virtuais. Sinalizadores de recursos são sempre configurações que você usa por sua própria conta e risco. Você pode ativar funcionalidades experimentais com a [extensão de sinalizadores de recursos](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.FeatureFlagsExtension) ou por meio do Prompt de Comando do Desenvolvedor.

![Extensão de sinalizador de recursos](media/testex-featureflag.png)

Para ativar um sinalizador de recursos por meio do prompt de comando de desenvolvedor do Visual Studio, use o comando a seguir. Altere o caminho para onde o Visual Studio está instalado em seu computador e altere a chave do Registro para o sinalizador de recurso que você deseja.

```shell
vsregedit set “C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise" HKLM FeatureFlags\TestingTools\UnitTesting\HierarchyView Value dword 1
```

> [!NOTE]
> Você pode desativar o sinalizador com o mesmo comando, usando o valor 0 em vez de 1 após dword.

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=fullName>
- [Criar e executar testes de unidade para código existente](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)
- [Efetuar teste de unidade em seu código](unit-test-your-code.md)
- [Perguntas frequentes sobre o Live Unit Testing](live-unit-testing-faq.md)
