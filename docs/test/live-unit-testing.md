---
title: Live Unit Testing
ms.date: 04/07/2020
ms.topic: how-to
helpviewer_keywords:
- Live Unit Testing
author: mikejo5000
ms.author: mikejo
ms.workload:
- dotnet
ms.openlocfilehash: 185d722f65dce0062dc58a06a05590aacb68138b
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85906218"
---
# <a name="how-to-configure-and-use-live-unit-testing"></a>Como configurar e usar Live Unit Testing

Como você está desenvolvendo um aplicativo, Live Unit Testing executa automaticamente qualquer teste de unidade impactado em segundo plano e apresenta os resultados e a cobertura de código em tempo real. Durante a modificação do código, o Live Unit Testing fornece comentários sobre como as alterações afetaram os testes existentes e se o novo código adicionado é abrangido por um ou mais testes existentes. Isso me lembra com cuidado para escrever testes de unidade conforme você está fazendo correções de bugs ou adicionando novos recursos.

> [!NOTE]
> Live Unit Testing está disponível para projetos em C# e Visual Basic direcionados ao .NET Core ou .NET Framework na edição Enterprise do Visual Studio.

Quando você usa Live Unit Testing para seus testes, ele persiste dados sobre o status de seus testes. O uso de dados persistentes permite que o Live Unit Testing ofereça desempenho superior ao executar seus testes dinamicamente em resposta a alterações de código.

## <a name="supported-test-frameworks"></a>Estruturas de teste com suporte

O Live Unit Testing funciona com as três estruturas de teste de unidade populares listadas na tabela a seguir. A versão mínima com suporte de seus adaptadores e estruturas também é mostrada. As estruturas de teste de unidade estão disponíveis em NuGet.org.

|Estrutura de teste  |Versão mínima do Adaptador do Visual Studio  |Versão mínima da Estrutura  |
|---------|---------|---------|
|xUnit.net |xunit.runner.visualstudio versão 2.2.0-beta3-build1187 |xunit 1.9.2 |
|NUnit |NUnit3TestAdapter versão 3.5.1 |NUnit versão 3.5.0 |
|MSTest |MSTest.TestAdapter 1.1.4-preview |MSTest.TestFramework 1.0.5-preview |

Se você tiver projetos de teste com base em MSTest mais antigos que referenciem Microsoft. VisualStudio. QualityTools. UnitTestFramework e não quiser migrar para os pacotes do NuGet do MSTest mais recentes, atualize para o Visual Studio 2019 ou Visual Studio 2017.

Em alguns casos, talvez seja necessário restaurar explicitamente os pacotes NuGet referenciados por um projeto para que Live Unit Testing funcionem. Você pode fazer isso fazendo uma compilação explícita da solução (selecione **criar**  >  **solução de recompilação** no menu do Visual Studio de nível superior) ou restaurando pacotes na solução (clique com o botão direito do mouse na solução e selecione **restaurar pacotes NuGet**).

## <a name="configure"></a>Configurar

Configure Live Unit Testing selecionando **ferramentas**  >  **Opções** na barra de menus do Visual Studio de nível superior e, em seguida, selecionando **Live Unit Testing** no painel esquerdo da caixa de diálogo **Opções** .

> [!TIP]
> Após a habilitação da Live Unit Testing (consulte a próxima seção, [Iniciar, pausar e parar Live Unit Testing](#start-pause-and-stop)), você também pode abrir a caixa de diálogo **Opções** selecionando **testar**  >  **Live Unit Testing**  >  **Opções**de Live unit testing.

A imagem a seguir mostra as opções de configuração de Live Unit Testing disponíveis na caixa de diálogo:

![Opções de configuração do Live Unit Testing](./media/lut-options.png)

As opções configuráveis incluem:

- Se o Live Unit Testing é pausado quando uma solução é criada e depurada.

- Se o Live Unit Testing é pausado quando a energia da bateria do sistema fica abaixo de um limite especificado.

- Se o Live Unit Testing é executado automaticamente quando uma solução é aberta.

- Se você deseja habilitar o símbolo de depuração e a geração de comentário da documentação XML.

- O diretório no qual deseja armazenar os dados persistentes.

- A capacidade de excluir todos os dados persistentes. Isso é útil quando Live Unit Testing está se comportando de forma imprevisível ou inesperada, o que sugere que os dados persistentes foram corrompidos.

- O intervalo após o qual um caso de teste atinge o tempo limite. O padrão é 30 segundos.

- O número máximo de processos de teste criados pelo Live Unit Testing.

- A quantidade máxima de memória que os processos do Live Unit Testing podem consumir.

- O nível de informações gravadas na janela **Saída** do Live Unit Testing.

   As opções incluem sem log (**None**), somente mensagens de erro (**Error**), mensagens de erro e mensagens informativas (**Info**, o padrão) ou todos os detalhes (**Verbose**).

   Também é possível exibir a saída detalhada na janela **Saída** do Live Unit Testing atribuindo um valor igual a “1” a uma variável de ambiente no nível do usuário chamada `VS_UTE_DIAGNOSTICS` e reiniciando o Visual Studio.

   Para capturar mensagens de log detalhadas do MSBuild do Live Unit Testing em um arquivo, defina a variável de ambiente no nível do usuário `LiveUnitTesting_BuildLog` com o nome do arquivo que conterá o log.

## <a name="start-pause-and-stop"></a>Iniciar, pausar e parar

Para habilitar Live Unit Testing, selecione **testar**  >  **Live Unit Testing**  >  **Iniciar** no menu de nível superior do Visual Studio. Quando Live Unit Testing estiver habilitada, as opções disponíveis no menu **Live Unit Testing** serão alteradas de um único item, **Iniciar**, para **Pausar** e **parar**:

- **Pausa** temporariamente suspende Live unit testing.

  Quando o Live Unit Testing é pausado, a visualização de cobertura não aparece no editor, mas todos os dados coletados são preservados. Para retomar o Live Unit Testing, selecione **Continuar** no menu Live Unit Testing. Live Unit Testing faz o trabalho necessário para acompanhar todas as edições que foram feitas enquanto estava em pausa e atualiza os glifos adequadamente.

- **Parar** completamente Live unit testing. O Live Unit Testing descarta todos os dados coletados.

> [!NOTE]
> Se você iniciar Live Unit Testing em uma solução que não inclui um projeto de teste de unidade, as opções **Pausar** e **parar** serão exibidas no menu **Live Unit Testing** , mas Live Unit Testing não será iniciado. A janela **saída** exibe uma mensagem que começa, "nenhum adaptador de teste com suporte é referenciado por esta solução...".

A qualquer momento, é possível pausar temporariamente ou parar por completo o Live Unit Testing. Você pode desejar fazer isso, por exemplo, se você estiver no meio de uma refatoração e souber que seus testes serão desfeitos por algum tempo.

## <a name="view-coverage-visualization"></a>Exibir visualização de cobertura

Depois de habilitado, o Live Unit Testing atualiza cada linha de código no editor do Visual Studio para mostrar se o código que você está escrevendo é coberto por testes de unidade e se os testes que cobrem estão sendo aprovados. A imagem a seguir mostra linhas de código com testes de passagem e com falha, bem como linhas de código que não são cobertas por testes. As linhas decoradas com um "✓" verde são cobertas apenas por testes aprovados, as linhas com um "x" vermelho são cobertas por um ou mais testes com falha e as linhas com um "➖" azul não são cobertas por nenhum teste.

![Cobertura de código no Visual Studio](./media/lut-codewindow.png)

A visualização de cobertura Live Unit Testing é atualizada imediatamente quando você modifica o código no editor de código. Ao processar as edições, a visualização muda para indicar que os dados não estão atualizados, adicionando uma imagem de timer redonda abaixo dos símbolos de passagem, falha e não cobertos, como mostra a imagem a seguir.

![Cobertura de código no Visual Studio com ícone de temporizador](./media/lut-codeupdating.png)

## <a name="get-information-about-test-status"></a>Obter informações sobre o status do teste

Ao focalizar o símbolo de êxito ou de falha na janela de código, é possível ver quantos testes estão atingindo essa linha. Para ver o status dos testes individuais, selecione o símbolo:

![Status do teste para um símbolo no Visual Studio](./media/lut-failedinfo.png)

Além de fornecer os nomes e o resultado dos testes, a dica de ferramenta permite que você execute novamente ou depure o conjunto de testes. Se você selecionar um ou mais dos testes na dica de ferramenta, é possível executar ou depurar apenas esses testes. Isso permite depurar seus testes sem ter que sair da janela de código. Ao depurar, além de observar quaisquer pontos de interrupção que você tenha definido, a execução do programa pausará quando o depurador executar um método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert> que retorna um resultado inesperado.

Ao focalizar um teste com falha na dica de ferramenta, ele é expandido para fornecer informações adicionais sobre a falha, conforme mostrado na imagem a seguir. Para navegar diretamente para um teste com falha, clique duas vezes nele na dica de ferramenta.

![Informações de dica de ferramenta de teste com falha no Visual Studio](./media/lut-failedmsg.png)

Quando você navega para o teste com falha, Live Unit Testing visualmente indica na assinatura do método os testes que têm:

- aprovado (indicado por uma Beaker de meio inteira, juntamente com um "✓" verde)
- falha (uma Beaker metade completa junto com um " 🞩 ") vermelho
- Não estão envolvidos em Live Unit Testing (uma Beaker inteira, juntamente com um "➖" azul)

Métodos de não teste não são decorados com um símbolo. A imagem a seguir ilustra todos os quatro tipos de métodos.

![Métodos de teste no Visual Studio com símbolo de aprovação ou reprovação](media/lut-testsource.png)

## <a name="diagnose-and-correct-test-failures"></a>Diagnosticar e corrigir falhas de teste

No teste com falha, você pode depurar facilmente o código do produto, fazer edições e continuar desenvolvendo seu aplicativo. Como Live Unit Testing é executado em segundo plano, você não precisa parar e reiniciar Live Unit Testing durante o ciclo de depuração, edição e continuação.

Por exemplo, a falha de teste mostrada na imagem anterior foi causada por uma pressuposição incorreta no método de teste que os caracteres não alfabéticos retornam `true` quando passados para o <xref:System.Char.IsLower%2A?displayProperty=fullName> método. Depois de corrigir o método de teste, todos os testes devem passar. Você não precisa pausar ou parar Live Unit Testing.

::: moniker range="vs-2017"
## <a name="test-explorer"></a>Gerenciador de Testes

O **Gerenciador de testes** fornece uma interface que permite executar e depurar testes e analisar os resultados do teste. O Live Unit Testing é integrado ao **Gerenciador de Testes**. Quando o Live Unit Testing não está habilitado ou está parado, o **Gerenciador de Testes** exibe o status dos testes de unidade na última vez que um teste foi executado. Alterações no código-fonte exigem uma nova execução dos testes. Por outro lado, quando o Live Unit Testing está habilitado, o status dos testes de unidade no **Gerenciador de Testes** é atualizado imediatamente. Você não precisa executar os testes de unidade explicitamente.

> [!TIP]
> Abra **Live Unit Testing** selecionando **testar**  >  **Windows**  >  o**Gerenciador de testes** do Windows no menu de nível superior do Visual Studio.

Você pode observar na janela **Test Explorer** que alguns testes estão desbotados. Por exemplo, quando você habilita Live Unit Testing depois de abrir um projeto salvo anteriormente, a janela **Gerenciador de testes** desbotau tudo, exceto o teste com falha, como mostra a imagem a seguir. Nesse caso, Live Unit Testing executou novamente o teste com falha, mas ele não executa novamente os testes bem-sucedidos. Isso ocorre porque os dados persistentes do Live Unit Testing indicam que não houve alterações desde que os testes foram executados pela última vez com êxito.

![Falha no teste no Gerenciador de testes](media/lut-test-explorer.png)

Você pode executar novamente os testes que aparecem desbotados selecionando as opções **executar tudo** ou **executar** no menu **Gerenciador de teste** . Ou, selecione um ou mais testes no menu **Gerenciador de testes** , clique com o botão direito do mouse e selecione **executar testes selecionados** ou **depurar testes selecionados** no menu pop-up. Conforme os testes são executados, eles são agrupados na parte superior.

Há algumas diferenças entre a execução e atualização automáticas dos resultados de teste do Live Unit Testing e a execução explícita de testes no **Gerenciador de Testes**. Entre elas, podemos incluir:

- A execução ou depuração de testes na janela Gerenciador de Testes executa binários regulares, ao passo que o Live Unit Testing executa binários instrumentados.
- O Live Unit Testing não cria um novo domínio de aplicativo para executar testes; em vez disso, ele executa testes no domínio padrão. Os testes executados na janela **Gerenciador de Testes** criam um novo domínio de aplicativo.
- O Live Unit Testing executa testes em cada assembly de teste sequencialmente. Na janela **Test Explorer** , você pode optar por executar vários testes em paralelo.
::: moniker-end

::: moniker range=">=vs-2019"
## <a name="live-unit-testing-window"></a>Janela de Live Unit Testing

**Live Unit Testing**, semelhante ao **Gerenciador de testes**, fornece uma interface que permite executar e depurar testes e analisar os resultados do teste. Quando Live Unit Testing está habilitado, o status dos testes de unidade no **Gerenciador de testes** é atualizado imediatamente. Você não precisa executar os testes de unidade explicitamente. Quando Live Unit Testing não estiver habilitado ou for interrompido, **Live Unit Testing** exibirá o status dos testes de unidade na última vez em que um teste foi executado. Depois de reiniciar Live Unit Testing, uma alteração de código-fonte é necessária para executar novamente os testes.

> [!TIP]
> Inicie Live Unit Testing selecionando **testar**  >  **Live Unit Testing**  >  **Iniciar** no menu de nível superior do Visual Studio. Você também pode abrir a janela **Live Unit Testing** usando **Exibir**  >  **outra**  >  **janela**do Windows Live unit testing.

Você pode observar na janela de **Live Unit Testing** que alguns testes estão desbotados. Por exemplo, quando você parar e reiniciar Live Unit Testing, a janela **Live Unit Testing** esmaecerá todos os testes, como mostra a imagem a seguir. Os resultados de teste desatualizados indicam que o teste não era parte da execução de teste de unidade dinâmica mais recente. Os testes são executados somente quando uma alteração no teste ou as dependências do teste é detectada. Se não houver nenhuma alteração, isso evita que a execução do teste seja desnecessariamente. Nesse caso, o resultado do teste esmaecido é ainda "atualizado", embora ele não faça parte da execução mais recente.

![Desbotando testes no Gerenciador de testes](media/vs-2019/lut-test-explorer.png)

Você pode executar novamente os testes que aparecem desbotados fazendo uma alteração de código.

Há algumas diferenças entre a execução e atualização automáticas dos resultados de teste do Live Unit Testing e a execução explícita de testes no **Gerenciador de Testes**. Entre elas, podemos incluir:

- A execução ou depuração de testes na janela Gerenciador de Testes executa binários regulares, ao passo que o Live Unit Testing executa binários instrumentados.
- O Live Unit Testing não cria um novo domínio de aplicativo para executar testes; em vez disso, ele executa testes no domínio padrão. Os testes executados na janela **Gerenciador de Testes** criam um novo domínio de aplicativo.
- O Live Unit Testing executa testes em cada assembly de teste sequencialmente. Na janela **Test Explorer** , você pode optar por executar vários testes em paralelo.
::: moniker-end

## <a name="large-solutions"></a>Soluções grandes

Se sua solução tiver 10 ou mais projetos, o Visual Studio exibirá a caixa de diálogo a seguir quando você:

- Iniciar Live Unit Testing e não há dados persistentes
- Selecione **ferramentas**  >  **Opções**  >  **Live Unit Testing**  >  **excluir dados persistentes**

![Caixa de diálogo do Live Unit Testing para projetos grandes](media/lut-large-project.png)

A caixa de diálogo avisa que a execução dinâmica de grandes números de testes em projetos grandes pode afetar seriamente o desempenho. Se você selecionar **OK**, o Live Unit Testing executará todos os testes na solução. Se você selecionar **Cancelar**, será possível selecionar os testes a serem executados. A seção a seguir explica como fazer isso.

## <a name="include-and-exclude-test-projects-and-test-methods"></a>Incluir e excluir projetos de teste e métodos de teste

Para soluções com muitos projetos de teste, você pode controlar quais projetos e métodos individuais em um projeto participam Live Unit Testing. Por exemplo, se você tiver uma solução com centenas de projetos de teste, será possível selecionar um conjunto direcionado de projetos de teste para fazer parte do Live Unit Testing. Há várias maneiras de fazer isso, dependendo se você deseja excluir todos os testes no projeto ou solução, incluir ou excluir a maioria dos testes ou excluir testes individuais. O Live Unit Testing salva o estado de inclusão/exclusão como uma configuração de usuário e a memoriza quando uma solução é fechada e reaberta.

### <a name="exclude-all-tests-in-a-project-or-solution"></a>Excluir todos os testes em um projeto ou solução

Para selecionar os projetos individuais em testes de unidade, faça o seguinte após a inicialização do Live Unit Testing:

1. Clique com o botão direito do mouse no **Gerenciador de Soluções** e escolha **Testes Dinâmicos** > **Excluir** para excluir toda a solução.
1. Clique com o botão direito do mouse em cada projeto de teste que você gostaria de incluir nos testes e escolha **testes ao vivo**,  >  **incluindo**.

### <a name="exclude-individual-tests-from-the-code-editor-window"></a>Excluir testes individuais da janela do editor de códigos

É possível usar a janela do editor de código para incluir ou excluir métodos de teste individuais. Clique com o botão direito do mouse na assinatura do método de teste na janela Editor de código e selecione uma das seguintes opções:

- **Testes**  >  ao vivo **Incluir \<selected method> **
- **Testes**  >  ao vivo **Excluir \<selected method> **
- **Testes**  >  ao vivo **Excluir tudo, \<selected method> exceto**

### <a name="exclude-tests-programmatically"></a>Excluir testes programaticamente

Você pode aplicar o atributo <xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute> para excluir, de forma programática, métodos, classes ou estruturas de relatar sua cobertura no Live Unit Testing.

Use os seguintes atributos para excluir métodos individuais de Live Unit Testing:

- Para xUnit: `[Trait("Category", "SkipWhenLiveUnitTesting")]`
- Para NUnit: `[Category("SkipWhenLiveUnitTesting")]`
- Para MSTest: `[TestCategory("SkipWhenLiveUnitTesting")]`

Use os seguintes atributos para excluir um assembly inteiro de testes de Live Unit Testing:

- Para xUnit: `[assembly: AssemblyTrait("Category", "SkipWhenLiveUnitTesting")]`
- Para NUnit: `[assembly: Category("SkipWhenLiveUnitTesting")]`
- Para MSTest: `[assembly: TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>Confira também

- [Ferramentas de teste de código](https://visualstudio.microsoft.com/vs/testing-tools/)
- [Blog de Live Unit Testing](https://devblogs.microsoft.com/visualstudio/live-unit-testing-in-visual-studio-2017-enterprise/)
- [Perguntas frequentes Live Unit Testing](live-unit-testing-faq.md)
- [Vídeo do Channel 9: Live Unit Testing no Visual Studio](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T105)
