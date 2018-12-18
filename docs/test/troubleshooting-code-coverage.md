---
title: Solução de problemas de cobertura de código
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: troubleshooting
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: 2651a84ae3c621237f34ff1667da6ecbacf0923a
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055096"
---
# <a name="troubleshoot-code-coverage"></a>Solução de problemas de cobertura de código

A ferramenta de análise da cobertura de código no Visual Studio coleta dados para assemblies nativos e gerenciados (arquivos *.dll* ou *.exe*). No entanto, em alguns casos, a janela **Resultados da Cobertura de Código** exibe um erro semelhante a "Resultados vazios gerados: ..." Há várias razões pelas quais você pode obter resultados vazios. Este artigo ajuda você a resolver esses problemas.

## <a name="what-you-should-see"></a>O que você deve ver

Se você escolher um comando **Analisar Cobertura de Código** no menu **Teste** e se o build e os testes forem executados com êxito, você deverá ver uma lista de resultados na janela **Cobertura de Código**. Você talvez tenha que expandir os itens para ver os detalhes.

![Resultados da cobertura de código com coloração](../test/media/codecoverage1.png)

Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

## <a name="possible-reasons-for-seeing-no-results-or-old-results"></a>Possíveis motivos para não ver resultados ou ver resultados anteriores

### <a name="do-you-have-the-right-edition-of-visual-studio"></a>Você tem a edição certa do Visual Studio?
 Você precisa do Visual Studio Enterprise.

### <a name="no-tests-were-executed"></a>Nenhum teste foi executado

Análise&mdash;Verifique a janela de saída. Na lista suspensa **Mostrar Saída de**, escolha **Testes**. Verifique se existe algum aviso ou erro registrado em log.

Explicação&mdash;A análise de cobertura de código é feita durante a execução de testes. Ela inclui apenas assemblies carregados na memória durante a execução dos testes. Se nenhum dos testes for executado, não haverá nada para a cobertura de código a ser reportado.

Resolução&mdash;No Gerenciador de Testes, escolha **Executar Tudo** para verificar se os testes foram executados com êxito. Corrija todas as falhas antes de usar **Analisar Cobertura de Código**.

### <a name="youre-looking-at-a-previous-result"></a>Você está olhando um resultado anterior

Quando você modificar e reexecutar os testes, um resultado anterior da cobertura de código poderá permanecer visível, inclusive a coloração de código com base nessa execução anterior.

1.  Executar Analisar Cobertura de Código.

2.  Não se esqueça de selecionar o conjunto de resultados mais recente na janela **Resultados da Cobertura de Código**.

### <a name="pdb-symbol-files-are-unavailable"></a>Os arquivos .pdb (símbolo) não estão disponíveis

Análise – Abra a pasta de destino de compilação (normalmente *bin\debug*) e verifique se, para cada assembly, existe um arquivo *.pdb* no mesmo diretório do arquivo *.dll* ou *.exe*.

Explicação – O mecanismo de cobertura de código exige que todo assembly tenha seu arquivo *.pdb* associado acessível durante a execução de teste. Se não houver nenhum arquivo *.pdb* para um assembly específico, o assembly não será analisado.

O arquivo *.pdb* precisa ser gerado do mesmo build dos arquivos *.dll* ou *.exe*.

Resolução – Garanta que as configurações de build gerem o arquivo *.pdb*. Se os arquivos *.pdb* não forem atualizados quando o projeto for compilado, abra as propriedades do projeto, selecione a página **Build**, escolha **Avançado** e inspecione **Informações de Depuração**.

Se os arquivos *.pdb* e *.dll* ou *.exe* estiverem em locais diferentes, copie o arquivo *.pdb* para o mesmo diretório. Também é possível configurar o mecanismo de cobertura de código para pesquisar arquivos *.pdb* em outro local. Para obter mais informações, confira [Personalizar a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

### <a name="use-an-instrumented-or-optimized-binary"></a>Usar um binário instrumentado ou otimizado

Análise – determine se o binário passou por alguma forma de otimização avançada, como a Otimização Guiada por Perfil, ou foi instrumentado por uma ferramenta de criação de perfil como *vsinstr.exe* ou *vsperfmon.exe*.

Explicação&mdash;Se um assembly já tiver sido instrumentado ou otimizado por outra ferramenta de criação de perfil, o assembly será omitido da análise de cobertura de código. A análise de cobertura de código não pode ser realizada nesses assemblies.

Resolução&mdash;Desative a otimização e use um novo build.

### <a name="code-is-not-managed-net-or-native-c-code"></a>O código é não gerenciado (.NET) ou nativo (C++)

Análise&mdash;Verifique se você está executando alguns testes em código gerenciado ou do C++.

Explicação&mdash;A análise de cobertura de código no Visual Studio está disponível apenas no código gerenciado e nativo (C++). Se você estiver trabalhando com ferramentas de terceiros, um ou todo o código poderá ser executado em uma plataforma diferente.

Resolução&mdash;Nenhuma disponível.

### <a name="assembly-has-been-installed-by-ngen"></a>O assembly foi instalado por NGen

Análise&mdash;Verifique se o assembly não é carregado com base no cache de imagem nativa.

Explicação&mdash;Por motivos de desempenho, os assemblies de imagem nativa não são analisados. Para obter mais informações, consulte [Ngen.exe (Gerador de Imagens Nativas)](/dotnet/framework/tools/ngen-exe-native-image-generator).

Resolução&mdash;Use uma versão MSIL do assembly. Não o processe com NGen.

### <a name="custom-runsettings-file-with-bad-syntax"></a>Arquivo .runsettings personalizado com sintaxe incorreta

Análise&mdash;Se você estiver usando um arquivo *.runsettings* personalizado, ele poderá conter um erro de sintaxe. A cobertura de código não é executada e a janela de cobertura de código não é aberta ao final da execução de teste ou mostra resultados anteriores.

Explicação – você pode executar os testes de unidade com um arquivo *.runsettings* personalizado para configurar as opções de cobertura de código. As opções permitem incluir ou excluir arquivos. Para obter mais informações, confira [Personalizar a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

Resolução&mdash;Existem dois tipos possíveis de falhas:

-   **Erro de XML**

     Abra o arquivo *.runsettings* no editor XML do Visual Studio. Procure indicações de erro.

-   **Erro na expressão regular**

     Cada cadeia de caracteres no arquivo é uma expressão regular. Examine cada um em busca de erros e, em especial, procure:

    -   Parênteses incompatíveis (...) ou parênteses sem escape \\(…\\). Se quiser corresponder um parêntese na cadeia de pesquisa, você deverá usar o escape. Por exemplo, para realizar a correspondência de uma função, use: `.*MyFunction\(double\)`

    -   Asterisco ou sinal de adição no início de uma expressão. Para comparar qualquer cadeia de caracteres, use um ponto seguido de um asterisco: `.*`

### <a name="custom-runsettings-file-with-incorrect-exclusions"></a>Arquivo .runsettings personalizado com exclusões incorretas

Análise&mdash;Se você estiver usando um arquivo *.runsettings* personalizado, verifique se ele inclui o assembly.

Explicação – você pode executar os testes de unidade com um arquivo *.runsettings* personalizado para configurar as opções de cobertura de código. As opções permitem incluir ou excluir arquivos. Para obter mais informações, confira [Personalizar a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

Resolução – Remova todos os nós `Include` do arquivo *.runsettings* e, em seguida, remova todos os nós `Exclude`. Se isso corrigir o problema, recoloque-os em estágios.

Verifique se o nó DataCollectors especifica a Cobertura de Código. Compare-o com a amostra contida em [Personalizar a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).

## <a name="some-code-is-always-shown-as-not-covered"></a>Um código é sempre mostrado como não coberto

### <a name="initialization-code-in-native-dlls-is-executed-before-instrumentation"></a>O código de inicialização em DLLs nativas é executado antes da instrumentação

Análise&mdash;No código nativo vinculado estaticamente, a função de inicialização **DllMain** e o código que ele chama às vezes são mostrados como não cobertos, mesmo que o código tenha sido executado.

Explicação&mdash;A ferramenta de cobertura de código funciona inserindo-se a instrumentação em um assembly pouco antes do início da execução do aplicativo. Em qualquer assembly carregado anteriormente, o código de inicialização em **DllMain** é executado assim que o assembly é carregado e antes da execução do aplicativo. Esse código aparentemente não foi abordado, o que, em geral, se aplica aos assemblies carregados estaticamente.

Resolução&mdash;Nenhuma.

## <a name="see-also"></a>Consulte também

- [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)