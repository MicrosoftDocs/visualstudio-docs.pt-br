---
title: Perguntas Frequentes sobre o Gerenciador de Testes
ms.date: 06/25/2020
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
manager: jillfra
ms.openlocfilehash: cf22c54da4af43c4953a8b92620031a14e25ec05
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468737"
---
# <a name="visual-studio-test-explorer-faq"></a>Perguntas frequentes sobre o Gerenciador de Testes do Visual Studio

## <a name="dynamic-test-discovery"></a>Detecção de testes dinâmica

**O Gerenciador de testes não está descobrindo meus testes que são definidos dinamicamente. (Por exemplo, teorias, adaptadores personalizados, características personalizadas, #ifdefs, etc.) Como posso descobrir esses testes?**

::: moniker range=">=vs-2019"
Crie seu projeto para executar a descoberta baseada em assembly.
::: moniker-end
::: moniker range="vs-2017"
Compile o projeto e verifique se a descoberta baseada em assembly está ativada em **Ferramentas** > **Opções** > **Teste**.
::: moniker-end
A [Detecção de testes em tempo real](https://devblogs.microsoft.com/dotnet/real-time-test-discovery/) é a detecção de testes baseada na origem. Ele não pode descobrir testes que usam teorias, adaptadores personalizados, características personalizadas, `#ifdef` instruções e muito mais, pois eles são definidos em tempo de execução. Um build é necessário para que esses testes sejam localizados com precisão. No Visual Studio 2017 versão 15.6 e posteriores, a descoberta baseada em assembly (o detector tradicional) é executada somente depois dos builds. Essa configuração significa que a detecção de testes em tempo real localiza o máximo de testes possível enquanto você está editando e a descoberta baseada em assembly permite que os testes definidos dinamicamente apareçam após um build. A detecção de testes em tempo real melhora a capacidade de resposta, mas ainda permite que você obtenha resultados completos e precisos após um build.

## <a name="test-explorer--plus-symbol"></a>Sinal de "+" (adição) do Gerenciador de Testes

**O que significa o '+' (sinal de mais) que aparece na linha superior do Gerenciador de Testes?**

O símbolo '+' (sinal de adição) indica que mais testes poderão ser descobertos após um build quando a descoberta baseada em assembly for executada. Esse símbolo será exibido quando forem detectados testes definidos dinamicamente no projeto.

![Linha de resumo do sinal de adição](media/testex-plussymbol.png)

::: moniker range="vs-2017"
## <a name="assembly-based-discovery"></a>Descoberta baseada em assembly

**A descoberta baseada em assembly não está mais funcionando para o meu projeto. Como fazer ativá-lo novamente?**

Acesse **Ferramentas** > **Opções** > **Teste** e marque a caixa **Adicionalmente, descobrir testes de assemblies compilados após builds.**

![Opção baseada em assembly](media/testex-toolsoptions.png)
::: moniker-end

## <a name="real-time-test-discovery"></a>Detecção de testes em tempo real

**Os testes agora aparecem no Gerenciador de testes enquanto eu digitar, sem precisar criar meu projeto. O que mudou?**

Esse recurso é chamado de [Detecção de testes em tempo real](https://devblogs.microsoft.com/dotnet/real-time-test-discovery/). Ele usa um analisador Roslyn para encontrar testes e popular o Gerenciador de Testes em tempo real, sem exigir que você compile o projeto. Para obter mais informações sobre o comportamento da detecção de testes para testes definidos dinamicamente, como teorias ou características personalizadas, confira [Detecção de testes dinâmica](#dynamic-test-discovery).

## <a name="real-time-test-discovery-compatibility"></a>Compatibilidade da detecção de testes em tempo real

**Quais linguagens e estruturas de teste podem usar a detecção de testes em tempo real?**

A [Detecção de testes em tempo real](https://devblogs.microsoft.com/dotnet/real-time-test-discovery/) só funciona em linguagens gerenciadas (C# e Visual Basic), pois é compilada com o compilador Roslyn. Por enquanto, a detecção de testes em tempo real só funciona para as estruturas xUnit, NUnit e MSTest.

## <a name="test-explorer-logs"></a>Logs do Gerenciador de Testes

**Como faço para ativar logs no Gerenciador de Testes?**

Navegue até **ferramentas**  >  **Opções**  >  **testar** e localize a seção de registro em log.

## <a name="uwp-test-discovery"></a>Detecção de testes da UWP

**Por que meus testes em projetos UWP não são detectados enquanto eu não implanto o aplicativo?**

Os testes UWP têm como destino um runtime diferente quando o aplicativo é implantado. Isso significa que para encontrar testes com precisão em projetos UWP, além de compilar seu projeto, você também precisa implantá-lo.

## <a name="test-explorer-sorting"></a>Classificação do Gerenciador de Testes

**Como funciona a classificação de resultados de teste no modo de exibição de hierarquia?**

O modo de exibição de hierarquia classifica os testes em ordem alfabética e não por resultado. Grupos anteriores por configurações classificaram os resultados de teste por resultado e, em seguida, em ordem alfabética. Você ainda pode habilitar a classificação por resultado clicando com o botão direito do mouse no cabeçalho da coluna no Gerenciador de testes, habilitando a coluna Estado e clicando no cabeçalho da coluna Estado para aplicar a classificação nessa coluna. Você pode fornecer comentários sobre o design neste [problema do GitHub](https://github.com/Microsoft/vstest/issues/1425).

## <a name="test-explorer-hierarchy-view"></a>Modo de exibição da hierarquia do Gerenciador de Testes

**No modo de exibição de hierarquia, há os ícones aprovado, falha, ignorado e não executado ao lado dos agrupamentos de nós pai. O que esses ícones significam?**

Os ícones ao lado dos agrupamentos Projeto, Namespace e Classe mostram o estado dos testes nesse agrupamento. Confira a tabela a seguir.

![Ícones de Hierarquia do Gerenciador de Testes](media/testex-hierarchyicons.png)

## <a name="search-by-file-path"></a>Pesquisar por caminho do arquivo

**Não existe mais um filtro de "caminho do arquivo" na caixa de pesquisa do Gerenciador de Testes.**

O filtro do caminho de arquivo na caixa de pesquisa do **Gerenciador de Testes** foi removida do Visual Studio 2017 versão 15.7. Essa funcionalidade tinha pouco uso e o Gerenciador de Testes pode recuperar métodos de teste com mais rapidez excluindo essa funcionalidade. Se essa alteração interromper seu fluxo de desenvolvimento, informe-nos enviando comentários na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com/).

## <a name="remove-undocumented-interfaces"></a>Remover interfaces não documentadas

**Algumas APIs relacionadas a teste não estão mais presentes no Visual Studio 2019. O que mudou?**

No Visual Studio 2019, serão removidas algumas APIs de janela de teste que foram marcadas como públicas anteriormente, mas nunca foram documentadas oficialmente. Elas foram marcadas como "preteridas" no Visual Studio 2017 para fornecer um aviso antecipado aos mantenedores de extensão. Para o nosso conhecimento, muito poucas extensões haviam encontrado essas APIs e criado uma dependência delas. Elas incluem `IGroupByProvider`, `IGroupByProvider<T>`, `KeyComparer`, `ISearchFilter`, `ISearchFilterToken`, `ISearchToken` e `SearchFilterTokenType`. Se essa alteração afetar sua extensão, fale conosco enviando um bug na [Comunidade de Desenvolvedores](https://developercommunity.visualstudio.com).

## <a name="test-adapter-nuget-reference"></a>Referência ao NuGet do adaptador de teste

**No Visual Studio 2017, versão 15.8, meus testes são detectados, mas não são executados**.

Todos os projetos de teste devem incluir a referência ao NuGet do adaptador de teste do .NET no arquivo .csproj. Caso contrário, a saída desse teste será exibida no projeto se a detecção por uma extensão do adaptador de teste for iniciada após um build, ou se o usuário tentar executar os testes selecionados:

**O projeto de teste {} não faz referência a nenhum adaptador .net NuGet. A descoberta de teste ou execução pode não funcionar para este projeto. É recomendável referenciar os adaptadores de teste do NuGet em cada projeto de teste .NET na solução.**

Em vez de usar extensões do adaptador de teste, os projetos são solicitados a usar os pacotes do adaptador de teste do NuGet. Esse requisito melhora bastante o desempenho e causa menos problemas com a integração contínua. Leia mais sobre a substituição da extensão do adaptador de teste do .NET nas [notas de versão](/visualstudio/releasenotes/vs2017-relnotes-v15.8#testadapterextension).

::: moniker range="vs-2017"
> [!NOTE]
> Se você estiver usando o adaptador de teste do NUnit 2 e não puder migrar para o adaptador de teste do NUnit 3, poderá desativar esse novo comportamento de descoberta no Visual Studio versão 15,8 no teste de opções de **ferramentas**  >  **Options**  >  **Test**.

![Comportamento do Adaptador do Gerenciador de Testes nas opções de ferramentas](media/testex-adapterbehavior.png)
::: moniker-end

## <a name="uwp-testcontainer-was-not-found"></a>O TestContainer do UWP não foi encontrado

**Meus testes do UWP não estão mais sendo executados no Visual Studio 2017 versão 15.7 e posterior.**

Projetos de teste do UWP recentes especificam uma propriedade de build da plataforma de teste que permite um melhor desempenho para identificar aplicativos de teste. Se você tiver um projeto de teste UWP que foi inicializado antes do Visual Studio versão 15,7, poderá ver esse erro nos testes de **saída**  >  **Tests**:

**System.AggregateException: Um ou mais erros ocorreram. ---> System.InvalidOperationException: O seguinte TestContainer não foi encontrado {} em Microsoft.VisualStudio.TestWindow.Controller.TestContainerProvider \<GetTestContainerAsync>d__61.MoveNext()**

Para corrigir esse erro: 

- Atualize a propriedade de build do projeto de teste usando o seguinte código:

```XML
<UnitTestPlatformVersion Condition="'$(UnitTestPlatformVersion)' == ''">$(VisualStudioVersion)</UnitTestPlatformVersion>
```

- Atualize a versão do SDK da TestPlatform usando o seguinte código:

```XML
<SDKReference Include="TestPlatform.Universal, Version=$(UnitTestPlatformVersion)" />
```
::: moniker range=">=vs-2019"
## <a name="using-preview-features"></a>Usando recursos de visualização

No Visual Studio 2019, você pode optar por recursos de visualização em **ferramentas > opções > ambiente > recursos de visualização**.
::: moniker-end
::: moniker range=">=vs-2017"
## <a name="using-feature-flags"></a>Como usar sinalizadores de recursos

**Como ativar sinalizadores de recursos para experimentar os novos recursos de teste?**

Sinalizadores de recursos são usados para enviar partes experimentais ou incompletas do produto para usuários ávidos que gostariam de fazer comentários antes que os recursos sejam fornecidos oficialmente. Eles podem desestabilizar a experiência de IDE. Use-os somente em ambientes de desenvolvimento seguros, como máquinas virtuais. Sinalizadores de recursos são sempre configurações que você usa por sua própria conta e risco. Você pode ativar funcionalidades experimentais com a [extensão de sinalizadores de recursos](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.FeatureFlagsExtension) ou por meio do Prompt de Comando do Desenvolvedor.

![Extensão de sinalizador de recursos](media/testex-featureflag.png)

Para ativar um sinalizador de recursos por meio do prompt de comando de desenvolvedor do Visual Studio, use o comando a seguir. Altere o caminho para onde o Visual Studio está instalado em seu computador e altere a chave do Registro para o sinalizador de recurso que você deseja.

```shell
vsregedit set “C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise" HKLM FeatureFlags\TestingTools\UnitTesting\HierarchyView Value dword 1
```

> [!NOTE]
> Você pode desativar o sinalizador com o mesmo comando, usando o valor 0 em vez de 1 após dword.
::: moniker-end
## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=fullName>
- [Criar e executar testes de unidade para código existente](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)
- [Teste de unidade em seu código](unit-test-your-code.md)
- [Perguntas frequentes sobre o Live Unit Testing](live-unit-testing-faq.md)
