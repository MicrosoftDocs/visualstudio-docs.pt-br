---
title: Solução de problemas de cobertura de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 26de91b8-45e3-4976-a20e-a3bd1942ddcb
caps.latest.revision: 13
ms.author: gewarren
manager: douge
ms.openlocfilehash: f7df2f4c83a61c62a7774bea475d54c3deea4c47
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49306040"
---
# <a name="troubleshooting-code-coverage"></a>Solução de problemas de cobertura de código
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A ferramenta de análise da cobertura de código no Visual Studio coleta dados para assemblies nativos e gerenciados (arquivos .dll ou .exe). No entanto, em alguns casos, a janela Resultados de Cobertura de Código exibe um erro semelhante a "Esvaziar resultados gerados: ...." Existem vários motivos possíveis pelos quais isso pode acontecer. Este tópico deve ajudar a resolver esses problemas.  
  
## <a name="what-you-should-see"></a>O que você deve ver  
 Se você escolher um comando **Analisar Cobertura de Código** no menu Teste e se o build e os testes forem executados com êxito, você deverá ver uma lista de resultados na janela Cobertura de Código. Você talvez tenha que expandir os itens para ver os detalhes.  
  
 ![Resultados da cobertura de código com coloração](../test/media/codecoverage1.png "CodeCoverage1")  
  
 Para obter mais informações, consulte [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).  
  
## <a name="possible-reasons-for-seeing-no-results-or-old-results"></a>Possíveis motivos para não ver resultados ou ver resultados anteriores  
  
### <a name="do-you-have-the-right-edition-of-visual-studio"></a>Você tem a edição certa do Visual Studio?  
 Você precisa do Visual Studio Enterprise.  
  
### <a name="no-tests-were-executed"></a>Nenhum teste foi executado  
 Análise  
 Verifique a janela de saída. Na lista suspensa **Mostrar Saída de**, escolha **Testes**. Verifique se existe algum aviso ou erro registrado em log.  
  
 Explicação  
 A análise de cobertura de código é feita durante a execução de testes. Ela inclui apenas assemblies carregados na memória durante a execução dos testes. Se nenhum dos testes for executado, não haverá nada para a cobertura de código a ser reportado.  
  
 Resolução  
 No Gerenciador de Testes, escolha **Executar Tudo** para verificar se os testes foram executados com êxito. Corrija todas as falhas antes de usar **Analisar Cobertura de Código**.  
  
### <a name="youre-looking-at-a-previous-result"></a>Você está observou um resultado anterior  
 Quando você modificar e reexecutar os testes, um resultado anterior da cobertura de código poderá permanecer visível, inclusive a coloração de código com base nessa execução anterior.  
  
1.  Executar Analisar Cobertura de Código.  
  
2.  Não se esqueça de selecionar o conjunto de resultados mais recente na janela de resultados Cobertura de Código.  
  
### <a name="pdb-symbol-files-are-unavailable"></a>Os arquivos .pdb (símbolo) não estão disponíveis  
 Análise  
 Abra a pasta de destino de compilação (normalmente bin\debug) e verifique se, para cada assembly, existe um arquivo .pdb no mesmo diretório do arquivo .dll ou .exe.  
  
 Explicação  
 O mecanismo de cobertura de código exige que todo assembly tenha seu arquivo .pdb associado acessível durante a execução do teste. Se não houver arquivo .pdb para um determinado assembly, ele não será analisado.  
  
 O arquivo .pdb deve ser gerado com base na mesma compilação dos arquivos .dll ou .exe.  
  
 Resolução  
 Verifique se as configurações de compilação geram o arquivo .pdb. Se os arquivos .pdb não forem atualizados quando o projeto for compilado, abra as propriedades do projeto, selecione a página **Build**, escolha **Avançado** e inspecione **Informações de Depuração**.  
  
 Se os arquivos .pdb e .dll ou .exe estiverem em locais diferentes, copie o arquivo .pdb para o mesmo diretório. Também é possível configurar o mecanismo de cobertura de código para procurar arquivos .pdb em outro local. Para obter mais informações, consulte [Personalizando a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
### <a name="using-an-instrumented-or-optimized-binary"></a>Usando um binário instrumentado ou otimizado  
 Análise  
 Determine se o binário passou por algum formulário de otimização avançada como, por exemplo, Otimização Guiada por Perfil, ou foi instrumentado por uma ferramenta de criação de perfil como vsinstr.exe ou vsperfmon.exe.  
  
 Explicação  
 Se um assembly já tiver sido instrumentado ou otimizado por outra ferramenta de criação de perfil, o assembly será omitido da análise de cobertura de código.  
  
 A análise de cobertura de código não pode ser realizada nesses assemblies.  
  
 Resolução  
 Desative a otimização e use uma nova compilação.  
  
### <a name="code-is-not-managed-net-or-native-c-code"></a>O código é não gerenciado (.NET) ou nativo (C++)  
 Análise  
 Verifique se você está executando alguns testes em código gerenciado ou do C++.  
  
 Explicação  
 A análise de cobertura de código no Visual Studio está disponível apenas no código gerenciado e nativo (C++). Se você estiver trabalhando com ferramentas de terceiros, um ou todo o código poderá ser executado em uma plataforma diferente.  
  
 Resolução  
 Nenhum disponível.  
  
### <a name="assembly-has-been-installed-by-ngen"></a>O assembly foi instalado por NGen  
 Análise  
 Verifique se o assembly não é carregado com base no cache de imagem nativa.  
  
 Explicação  
 Por motivos de desempenho, os assemblies de imagem nativa não são analisados. Para obter mais informações, consulte [Ngen.exe (Gerador de Imagens Nativas)](http://msdn.microsoft.com/library/44bf97aa-a9a4-4eba-9a0d-cfaa6fc53a66).  
  
 Resolução  
 Use uma versão MSIL do assembly. Não o processe com NGen.  
  
### <a name="custom-runsettings-file-with-bad-syntax"></a>Arquivo .runsettings personalizado com sintaxe incorreta  
 Análise  
 Se você estiver usando um arquivo .runsettings personalizado, ele poderá conter um erro de sintaxe.  
  
 Isso resulta na ausência de execução de cobertura de código. A janela de cobertura de código não é aberta ao final da execução de teste ou mostra resultados anteriores.  
  
 Explicação  
 É possível executar testes de unidade com um arquivo .runsettings personalizado para configurar opções de cobertura de código. As opções permitem incluir ou excluir arquivos. Para obter mais informações, consulte [Personalizando a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
 Resolução  
 Existem dois tipos possíveis de falhas:  
  
-   **Erro de XML**  
  
     Abra o arquivo .runsettings no editor XML do Visual Studio. Procure indicações de erro.  
  
-   **Erro na expressão regular**  
  
     Cada cadeia de caracteres no arquivo é uma expressão regular. Revise cada um em busca de erros e, em especial, procure:  
  
    -   Parênteses incompatíveis (...) ou parênteses sem escape \\(…\\). Se quiser corresponder um parêntese na cadeia de pesquisa, você deverá usar o escape. Por exemplo, para realizar a correspondência de uma função, use: `.*MyFunction\(double\)`  
  
    -   Asterisco ou sinal de adição no início de uma expressão. Para comparar qualquer cadeia de caracteres, use um ponto seguido de um asterisco: `.*`  
  
### <a name="custom-runsettings-file-with-incorrect-exclusions"></a>Arquivo .runsettings personalizado com exclusões incorretas  
 Análise  
 Se você estiver usando um arquivo .runsettings personalizado, verifique se ele inclui o assembly.  
  
 Explicação  
 É possível executar testes de unidade com um arquivo .runsettings personalizado para configurar opções de cobertura de código. As opções permitem incluir ou excluir arquivos. Para obter mais informações, consulte [Personalizando a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
 Resolução  
 Remova todos os nós `Include` do arquivo .runsettings e, em seguida, descarte todos os nós `Exclude`. Se isso corrigir o problema, recoloque-os em estágios.  
  
 Verifique se o nó DataCollectors especifica a Cobertura de Código. Compare-o com o exemplo em [Personalizando a análise de cobertura de código](../test/customizing-code-coverage-analysis.md).  
  
## <a name="some-code-is-always-shown-as-not-covered"></a>Um código é sempre mostrado como não coberto  
  
### <a name="initialization-code-in-native-dlls-is-executed-before-instrumentation"></a>O código de inicialização em DLLs nativas é executado antes da instrumentação  
 Análise  
 No código nativo vinculado estaticamente, a função de inicialização **DllMain** e o código que ele chama às vezes são mostrados como não cobertos, mesmo que o código tenha sido executado.  
  
 Explicação  
 A ferramenta de cobertura de código funciona inserindo-se a instrumentação em um assembly pouco antes do início da execução do aplicativo. Em qualquer assembly carregado anteriormente, o código de inicialização em **DllMain** é executado assim que o assembly é carregado e antes da execução do aplicativo. Esse código aparentemente não estará coberto.  
  
 Normalmente, isso se aplica aos assemblies carregados estaticamente.  
  
 Resolução  
 nenhuma.  
  
## <a name="see-also"></a>Consulte também  
 [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md)



