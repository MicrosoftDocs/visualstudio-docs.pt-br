---
title: Live Unit Testing no Visual Studio
ms.date: 2017-03-07
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio ALM
- Live Unit Testing
author: rpetrusha
ms.author: ronpet
ms.workload:
- dotnet
ms.openlocfilehash: 6e0bd322b200fba3bf41f99c4119cbe287ce2967
ms.sourcegitcommit: a6734c4d76dae3d21b55b10f3bc618dfa6b62dea
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "42626925"
---
# <a name="live-unit-testing-with-visual-studio-2017"></a>Live Unit Testing com o Visual Studio 2017

Durante o desenvolvimento de um aplicativo, o Live Unit Testing executa os testes de unidade afetada automaticamente em segundo plano e apresenta os resultados e a cobertura de código dinâmica no IDE do Visual Studio em tempo real. Durante a modificação do código, o Live Unit Testing fornece comentários sobre como as alterações afetaram os testes existentes e se o novo código adicionado é abrangido por um ou mais testes existentes. Cuidadosamente, isso o lembrará de escrever testes de unidade durante as correções de bugs ou a adição novos recursos.

> [!NOTE]
> O Live Unit Testing está disponível para projetos do C# e do Visual Basic que se destinam ao .NET Core ou ao .NET Framework na Enterprise Edition do Visual Studio 2017.

Quando você utilizar o Live Unit Testing para seu teste, ele preservará os dados sobre o status dos seus testes. A capacidade de utilizar dados persistentes permite que o Live Unit Testing ofereça desempenho superior ao executar seus testes de forma dinâmica em resposta a mudanças de código.

## <a name="supported-test-frameworks"></a>Estruturas de teste com suporte
O Live Unit Testing funciona com as três estruturas de teste de unidade populares listadas na tabela a seguir. A versão mínima com suporte de seus adaptadores e suas estruturas também é listada na tabela. As estruturas de teste de unidade estão disponíveis em NuGet.org.

<table>
<tr>
   <th>Estrutura de teste</th>
   <th>Versão mínima do Adaptador do Visual Studio</th>
   <th>Versão mínima da Estrutura</th>
</tr>
<tr>
   <td>xUnit.net</td>
   <td> xunit.runner.visualstudio versão 2.2.0-beta3-build1187</td>
   <td>xunit 1.9.2</td>
</tr>
<tr>
   <td>NUnit</td>
   <td>NUnit3TestAdapter versão 3.5.1</td>
   <td>NUnit versão 3.5.0</td>
</tr>
<tr>
   <td>MSTest</td>
   <td>MSTest.TestAdapter 1.1.4-preview</td>
   <td>MSTest.TestFramework 1.0.5-preview</td>
</tr>
</table>

Se você tem projetos de teste baseados no MSTest mais antigos que referenciam o `Microsoft.VisualStudio.QualityTools.UnitTestFramework` e não deseja mover para os pacotes do NuGet do MSTest mais recentes, atualize para o Visual Studio 2017 versão 15.4.

Em alguns casos, talvez seja necessário restaurar explicitamente os pacotes NuGet referenciados pelos projetos na solução para que o Live Unit Testing funcione. Faça isso executando um build explícito da solução (selecione **Compilar** > **Recompilar Solução** no menu de nível superior do Visual Studio) ou restaurando pacotes da solução (clique com o botão direito do mouse na solução e selecione **Restaurar Pacotes NuGet**) antes de habilitar o Live Unit Testing.

## <a name="configure-live-unit-testing"></a>Configurar o Live Unit Testing

Configure o Live Unit Testing selecionando **Ferramentas** > **Opções** na barra de menus de nível superior do Visual Studio e, em seguida, selecionando **Live Unit Testing** no painel esquerdo da caixa de diálogo **Opções**.

> [!TIP]
> Depois que o Live Unit Testing for habilitado (veja a próxima seção, [Iniciar, pausar e parar o Live Unit Testing](#start-pause-and-stop-live-unit-testing)), abra também a caixa de diálogo **Opções** selecionando **Teste** > **Live Unit Testing** > **Opções**.

A figura a seguir mostra as opções de configuração de Live Unit Testing disponíveis na caixa de diálogo:

  ![Image](./media/lut-options.png)

As opções configuráveis incluem:

- Se o Live Unit Testing é pausado quando uma solução é criada e depurada.

- Se o Live Unit Testing é pausado quando a energia da bateria do sistema fica abaixo de um limite especificado.

- Se o Live Unit Testing é executado automaticamente quando uma solução é aberta.

- Se você deseja habilitar o símbolo de depuração e a geração de comentário da documentação XML.

- O diretório no qual deseja armazenar os dados persistentes.

- A capacidade de excluir todos os dados persistentes. Isso é útil quando o Live Unit Testing se comporta de forma imprevisível ou inesperada, o que sugere que os dados persistentes foram corrompidos.
   
- O intervalo após o qual um caso de teste atinge o tempo limite; o padrão é 30 segundos.

- O número máximo de processos de teste criados pelo Live Unit Testing.

- A quantidade máxima de memória que os processos do Live Unit Testing podem consumir.

- O nível de informações gravadas na janela **Saída** do Live Unit Testing.

   As opções incluem sem log (**None**), somente mensagens de erro (**Error**), mensagens de erro e mensagens informativas (**Info**, o padrão) ou todos os detalhes (**Verbose**).

   Também é possível exibir a saída detalhada na janela **Saída** do Live Unit Testing atribuindo um valor igual a “1” a uma variável de ambiente no nível do usuário chamada `VS_UTE_DIAGNOSTICS` e reiniciando o Visual Studio.

   Para capturar mensagens de log detalhadas do MSBuild do Live Unit Testing em um arquivo, defina a variável de ambiente no nível do usuário `LiveUnitTesting_BuildLog` com o nome do arquivo que conterá o log.

## <a name="start-pause-and-stop-live-unit-testing"></a>Iniciar, pausar e parar o Live Unit Testing

Habilite o Live Unit Testing selecionando **Teste** > **Live Unit Testing** > **Iniciar** no menu de nível superior do Visual Studio. Quando o Live Unit Testing é habilitado, as opções disponíveis no menu **Live Unit Testing** mudam de um único item, **Iniciar**, para **Pausar**, **Parar** e **Reiniciar Limpo**.

> [!NOTE]
> Se você iniciar o Live Unit Testing em uma solução que não inclua um projeto de teste de unidade, as opções **Pausar**, **Parar** e **Redefinir Limpeza** serão exibidas no menu **Live Unit Testing**, mas o Live Unit Testing não será iniciado. A janela **Saída** exibe uma mensagem que começa com "Nenhum adaptador de teste com suporte é referenciado por essa solução..."

A qualquer momento, é possível pausar temporariamente ou parar por completo o Live Unit Testing. Talvez você deseje fazer isso, por exemplo, se estiver no meio de uma refatoração e souber que os testes serão interrompidos por algum tempo. As três opções de menu são:

- **Pausar**, que suspende o Live Unit Testing temporariamente.

    Quando o Live Unit Testing está em pausa, a sua visualização de cobertura não é exibida no editor, mas todos os dados coletados são preservados. Para retomar o Live Unit Testing, selecione **Continuar** no menu Live Unit Testing. O Live Unit Testing faz o trabalho necessário para ficar atualizado com todas as edições que foram feitas durante sua pausa e atualiza os glifos de forma adequada.

- **Parar**, para parar o Live Unit Testing por completo. O Live Unit Testing descarta todos os dados coletados.

- **Reiniciar Limpo**, que interrompe o Live Unit Testing, exclui os dados persistentes e reinicia o Live Unit Testing.

- **Opções**, que abre a caixa de diálogo **Opções** descrita na seção [Configurar o Live Unit Testing](#configure-live-unit-testing).

## <a name="view-coverage-visualization-in-the-editor-as-you-type"></a>Exibir a visualização de cobertura no editor durante a digitação

Depois de habilitado, o Live Unit Testing atualiza cada linha de código no editor do Visual Studio para mostrar se o código que está sendo escrito é abrangido por testes de unidade e se os testes que os abrangem são aprovados.  A figura a seguir mostra linhas de código com testes aprovados e não aprovados, bem como linhas de código que não são abrangidas por testes. As linhas decoradas com um "✓" verde são cobertas apenas por testes aprovados, as linhas com um "x" vermelho são cobertas por um ou mais testes com falha e as linhas com um "➖" azul não são cobertas por nenhum teste.

  ![Image](./media/lut-codewindow.png)

A visualização de cobertura do Live Unit Testing é atualizada imediatamente conforme o código é modificado no editor de código. Durante o processamento das edições, a visualização é alterada para indicar que os dados não estão atualizados, com a adição de uma imagem de temporizador redondo abaixo dos símbolos de aprovado, não aprovado e não abrangido, como mostra a figura a seguir.

  ![Image](./media/lut-codeupdating.png)

## <a name="get-information-on-successful-or-failed-tests"></a>Obter informações sobre testes com êxito ou com falha

Ao focalizar o símbolo de êxito ou de falha na janela de código, é possível ver quantos testes estão atingindo essa linha. Se você clicar no símbolo, poderá ver o status dos testes individuais, como mostra a figura a seguir:

  ![Image](./media/lut-failedinfo.png)

Além de fornecer os nomes e os resultados de testes, a dica de ferramenta permite executar novamente o conjunto de testes, bem como executar o conjunto de testes usando o depurador. Se você selecionar um ou mais dos testes na dica de ferramenta, é possível executar ou depurar apenas esses testes. Isso permite depurar seus testes sem ter que sair da janela de código. Ao depurar, além de observar quaisquer pontos de interrupção que você tenha definido, a execução do programa pausará quando o depurador executar um método [`Assert`](/dotnet/api/microsoft.visualstudio.testtools.unittesting.assert) que retorna um resultado inesperado.

Ao focalizar um teste com falha na dica de ferramenta, ele é expandido para fornecer informações adicionais sobre a falha, conforme mostrado na imagem a seguir. Se você clicar duas vezes no teste com falha na dica de ferramenta, poderá acessá-lo diretamente.

  ![Image](./media/lut-failedmsg.png)

Quando você navega para o teste que falhou, o Live Unit Testing também indica visualmente na assinatura do método os testes que foram aprovados (indicados por um ícone de béquer metade cheio e um "✓" verde), que falharam (um ícone de béquer metade cheio e um "🞩" vermelho) ou que não estão envolvidos no Live Unit Testing (um ícone de béquer metade cheio e um "➖" azul). Métodos de não teste não são decorados com um símbolo. A figura a seguir ilustra os quatro tipos de métodos.

  ![Image](media/lut-testsource.png)

## <a name="diagnose-and-correct-test-failures"></a>Diagnosticar e corrigir falhas de teste

No teste com falha, é possível depurar o código do produto com facilidade, fazer edições e continuar desenvolvendo o aplicativo. Como o Live Unit Testing é executado em segundo plano, você não precisa parar e reiniciá-lo durante o ciclo de depuração, edição e continuação.

Por exemplo, a falha de teste mostrada na figura anterior foi causada por uma suposição incorreta no método de teste de que caracteres não alfabéticos retornam `true` quando passados para o método <xref:System.Char.IsLower%2A?displayProperty=fullName>. Depois de corrigirmos o método de teste, descobrimos que todos os testes são aprovados. Enquanto estamos fazendo isso, não precisamos pausar nem parar o Live Unit Testing.

## <a name="live-unit-testing-and-test-explorer"></a>Live Unit Testing e o Gerenciador de Testes

Normalmente, o **Gerenciador de Testes** fornece a interface que permite executar, depurar e analisar os resultados de teste. O Live Unit Testing é integrado ao **Gerenciador de Testes**. Quando o Live Unit Testing não está habilitado ou está parado, o **Gerenciador de Testes** exibe o status dos testes de unidade na última vez que um teste foi executado. Alterações no código-fonte exigem uma nova execução dos testes. Por outro lado, quando o Live Unit Testing está habilitado, o status dos testes de unidade no **Gerenciador de Testes** é atualizado imediatamente. Não é mais necessário executar os testes de unidade explicitamente.

> [!NOTE]
> Abra o **Gerenciador de Testes** selecionando **Teste** > **Janelas** > **Gerenciador de Testes** no menu de nível superior do Visual Studio.

Você pode observar na janela do **Explorador de Testes** que alguns testes estão esmaecidos. Por exemplo, quando você habilita o Live Unit Testing depois de abrir um projeto salvo anteriormente, a janela do **Explorador de Testes** esmaece tudo exceto o teste que falhou, como mostra a imagem a seguir. Nesse caso, o Live Unit Testing reexecuta o teste com falha, mas não reexecuta os testes que tiveram êxito, uma vez que os dados persistentes do Live Unit Testing indicam que não houve nenhuma mudança desde a última vez em que os testes foram executados com êxito.

  ![Image](media/lut-test-explorer.png)

Você pode reexecutar qualquer teste que aparecer esmaecido selecionando as opções **Executar Todos** ou **Executar** no menu **Explorador de Testes** ou selecionando um ou mais testes no menu **Explorador de Testes**, clicando com o botão direito e selecionando **Executar Testes Selecionados** ou **Depurar Testes Selecionados** do menu pop-up. Conforme os testes são executados, eles são agrupados na parte superior.

Há algumas diferenças entre a execução e atualização automáticas dos resultados de teste do Live Unit Testing e a execução explícita de testes no **Gerenciador de Testes**. Entre elas, podemos incluir:

- A execução ou depuração de testes na janela Gerenciador de Testes executa binários regulares, ao passo que o Live Unit Testing executa binários instrumentados.
- O Live Unit Testing não cria um novo domínio de aplicativo para executar testes; em vez disso, ele executa testes no domínio padrão. Os testes executados na janela **Gerenciador de Testes** criam um novo domínio de aplicativo.
- O Live Unit Testing executa testes em cada assembly de teste sequencialmente. Se você executar vários testes na janela **Gerenciador de Testes** e o botão **Executar Testes em Paralelo** estiver selecionado, os testes serão executados em paralelo.

## <a name="live-unit-testing-and-large-solutions"></a>Live Unit Testing e soluções grandes

Se a solução tiver 10 ou mais projetos, quando você iniciar o Live Unit Testing e não houver dados persistentes, ou quando você selecionar a opção **Teste** > **Live Unit Testing** > **Redefinir Limpeza** no menu de nível superior do Visual Studio, o Visual Studio exibirá a caixa de diálogo a seguir para alertá-lo de que a execução dinâmica de muitos testes em projetos grandes pode afetar gravemente o desempenho. Se você selecionar **OK**, o Live Unit Testing executará todos os testes na solução. Se você selecionar **Cancelar**, será possível selecionar os testes a serem executados. Para obter mais informações sobre como fazer isso, confira a seção a seguir, [Incluir e excluir projetos e métodos de teste](#include-and-exclude-test-projects-and-test-methods).

 ![Caixa de diálogo do Live Unit Testing para projetos grandes](media/lut-large-project.png)

## <a name="include-and-exclude-test-projects-and-test-methods"></a>Incluir e excluir projetos de teste e métodos de teste

Para soluções com vários projetos de teste, é possível controlar quais projetos e quais métodos individuais em um projeto farão parte do Live Unit Testing. Por exemplo, se você tiver uma solução com centenas de projetos de teste, será possível selecionar um conjunto direcionado de projetos de teste para fazer parte do Live Unit Testing. Há várias maneiras de fazer isso, dependendo se você deseja excluir todos os testes no projeto ou solução, se deseja incluir ou excluir a maioria dos testes, ou se deseja excluir os testes individualmente. O Live Unit Testing salva o estado de inclusão/exclusão como uma configuração de usuário e a memoriza quando uma solução é fechada e reaberta.

**Excluir todos os testes em um projeto ou solução**

Para selecionar os projetos individuais em testes de unidade, faça o seguinte após a inicialização do Live Unit Testing:

1.  Clique com o botão direito do mouse no **Gerenciador de Soluções** e escolha **Testes Dinâmicos** > **Excluir** para excluir toda a solução.
1.  Clique com o botão direito do mouse em cada projeto de teste que deseja incluir nos testes e escolha **Testes Dinâmicos** > **Incluir**.

**Excluir testes individuais da janela do editor de códigos**

É possível usar a janela do editor de código para incluir ou excluir métodos de teste individuais. Clique com o botão direito do mouse na assinatura do método de teste na janela do editor de código e selecione **Testes Dinâmicos** > **Incluir [o método selecionado]**, **Testes Dinâmicos** > **Excluir [o método selecionado]** ou **Testes Dinâmicos** > **Excluir todos, exceto [o método selecionado]**, em que "o método selecionado" é o nome do método selecionado na janela de código.

**Excluir testes programaticamente**

Você pode aplicar o atributo <xref:System.Diagnostics.CodeAnalysis.ExcludeFromCodeCoverageAttribute> para excluir, de forma programática, métodos, classes ou estruturas de relatar sua cobertura no Live Unit Testing.

Você também pode usar os atributos a seguir para excluir métodos individuais do Live Unit Testing:

- Para xUnit: `[Trait("Category", "SkipWhenLiveUnitTesting")]`
- Para NUnit: `[Category("SkipWhenLiveUnitTesting")]`
- Para MSTest: `[TestCategory("SkipWhenLiveUnitTesting")]`

## <a name="see-also"></a>Consulte também

- [Ferramentas de teste de código](https://visualstudio.microsoft.com/vs/testing-tools/)
- [Blog do Live Unit Testing](https://go.microsoft.com/fwlink/?linkid=842514)
- [Perguntas Frequentes sobre os Testes de Unidade Dinâmicos](live-unit-testing-faq.md)
- [Vídeo do Channel 9: Live Unit Testing no Visual Studio 2017](https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T105)

