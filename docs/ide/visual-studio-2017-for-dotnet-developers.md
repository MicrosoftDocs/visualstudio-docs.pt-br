---
title: Aumentar a produtividade de desenvolvimento do .NET
description: Uma visão geral da navegação, da análise de código, do teste de unidade e de outros recursos para ajudá-lo a escrever um código .NET melhor mais rápido.
author: kuhlenh
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.date: 06/14/2018
ms.topic: conceptual
helpviewer_keywords:
- editor
ms.workload:
- dotnet
ms.openlocfilehash: 5a2158663defe02dc51e91e888d47f325db7226a
ms.sourcegitcommit: 20d1b9a5bf041bb28453501eb63bc0537a8e4f54
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2018
ms.locfileid: "51645140"
---
# <a name="visual-studio-2017-c-productivity-guide"></a>Guia de produtividade em C# do Visual Studio 2017

Saiba como o [Visual Studio de 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) faz com que os desenvolvedores sejam mais produtivos do que nunca. Aproveite nossas melhorias em desempenho e produtividade como a navegação para assemblies descompilados, sugestões de nomes de variáveis durante a digitação, um modo de exibição de hierarquia no **Gerenciador de Testes**, opção Ir para Todos (**Ctrl**+**T**) para navegar para as declarações de arquivo/tipo/membro/símbolo, um **Auxiliar de Exceção** inteligente, configuração e imposição de estilo de código e muitas correções de código e refatorações.

## <a name="im-used-to-my-keyboard-shortcuts-from-a-different-extensioneditoride"></a>Estou acostumado aos meus atalhos de teclado de uma extensão/editor/IDE diferente

**Novo no Visual Studio 2017 versão 15.8** Se você estiver vindo de outro IDE ou ambiente de codificação, poderá alterar o esquema do seu teclado para *Visual Studio Code* ou *ReSharper (Visual Studio)*:

![Esquemas de teclado no Visual Studio](../ide/media/VS2017Guide-Keyboard.png)

Algumas extensões também oferecem esquemas de teclado:

- [Teclas de acesso para Visual Studio (ReSharper/IntelliJ)](https://marketplace.visualstudio.com/items?itemName=JustinClareburtMSFT.HotKeys)
- [Emulação de Emacs](https://marketplace.visualstudio.com/items?itemName=JustinClareburtMSFT.EmacsEmulation)
- [VSVim](https://marketplace.visualstudio.com/items?itemName=JaredParMSFT.VsVim)

Estes são os atalhos populares do Visual Studio:

| Atalho (todos os perfis) | Comando | Descrição |
|-|-|-|
| **Ctrl**+**T** | Ir para Todos | Navegue diretamente para qualquer declaração de arquivo/tipo/membro/símbolo |
| **F12** (também **Ctrl**+**Clique**) | Ir para definição | Vá até onde um símbolo estiver definido |
| **Ctrl**+**F12** | Ir Para Implementação | Navegue de um membro ou tipo base até suas várias implementações |
| **Shift**+**F12** | Localizar Todas as Referências | Veja todas as referências de símbolo ou de literal |
| **Ctrl**+**.** (também **Alt**+**Enter** no Perfil C#) | Ações e Refatorações Rápidas | Veja quais correções de código, ações de geração de código, refatorações ou outras ações rápidas estão disponíveis na posição do cursor ou na seleção do código |
| **Ctrl**+**D** | Duplicar linha | Duplica a linha de código onde o cursor está posicionado (disponível no **Visual Studio 2017 versão 15.6** e posterior) |
| **Shift**+**Alt**+**+**/**-** | Expandir/Reduzir seleção | Expande ou reduz a seleção atual no editor (disponível no **Visual Studio 2017 versão 15.5** e posteriores) |
| **Shift** + **Alt** + **.** | Inserir próximo sinal de interpolação correspondente | Adiciona uma seleção e um sinal de interpolação no próximo local que corresponde à seleção atual (disponível no **Visual Studio 2017 versão 15.8** e posterior) |
| **Ctrl**+**Q** | Início Rápido | Pesquise todas as configurações do Visual Studio |
| **F5** | Iniciar a depuração | Inicie a depuração do aplicativo |
| **Ctrl**+**F5** | Executar sem Depurar | Execute o aplicativo localmente sem depuração |
| **Ctrl**+**K**,**D** (Perfil Padrão) ou **Ctrl**+**E**,**D** (Perfil C#) | [Formatar Documento](code-styles-and-quick-actions.md#format-document-command) | Limpe as violações de formatação de um arquivo com base nas configurações de nova linha, de espaçamento e de recuo |
| **Ctrl**+**\\**,**Ctrl**+**E** (Perfil Padrão) ou **Ctrl**+**W**,**E** (Perfil do C#) | Exibir Lista de Erros | Veja todos os erros no documento, no projeto ou na solução |
| **Alt** + **PgUp/PgDn** | Ir para o problema seguinte/anterior | Vá para o erro, aviso ou sugestão seguinte/anterior no documento (disponível no **Visual Studio 2017 versão 15.8** e posterior) |

> [!NOTE]
> Algumas extensões desassociam as associações de teclas padrão do Visual Studio. Para usar os comandos a acima, restaure as associações de teclas para os padrões do Visual Studio acessando **Ferramentas** > **Importar e Exportar Configurações** > **Redefinir todas as configurações** ou **Ferramentas** > **Opções** > **Teclado** > **Redefinir**.

Saiba mais atalhos de teclado e comandos no Visual Studio na [nossa documentação](../ide/tips-and-tricks-for-visual-studio.md).

## <a name="i-need-a-way-to-quickly-navigate-to-files-or-types"></a>Preciso de uma maneira para navegar rapidamente nos arquivos ou tipos

O Visual Studio 2017 tem um recurso chamado **Ir para Todos** (**Ctrl**+**T**). **Ir para Todos** permite que você acesse rapidamente qualquer declaração de arquivo, tipo, membro ou símbolo.

- Altere a localização desta barra de pesquisa ou desative a "visualização de navegação dinâmica" com o ícone **engrenagem**.
- Filtre os resultados usando nossa sintaxe de consulta (por exemplo, "t mytype"). Você também pode definir o escopo da pesquisa somente para o documento atual.
- Há suporte para a correspondência de camelCase!

![Ir para todos no Visual Studio](../ide/media/VS2017Guide-go-to-all.png)

## <a name="my-team-enforces-code-style-rules-on-our-codebase"></a>Minha equipe impõe regras de estilo de código em nossa base de código

Use um arquivo *.editorconfig* para codificar as convenções de codificação e aplicá-las à fonte.

- Você pode instalar a [extensão Serviços de linguagem EditorConfig](https://aka.ms/editorconfig), que torna mais fácil adicionar e editar um arquivo *.editorconfig* no Visual Studio.
- Experimente a [extensão do IntelliCode para o Visual Studio](/visualstudio/intellicode/intellicode-visual-studio). Essa extensão experimental infere os estilos de código a partir do código existente e, em seguida, cria um arquivo *.editorconfig* não vazio com suas preferências de estilo de código já definidas.
- Confira a [documentação das opções de convenção de codificação .NET](https://aka.ms/editorconfigDocs).
- Confira [este gist](https://gist.github.com/kuhlenh/5471666a7a2c57fea427e81cf0a41da8) para obter um exemplo de arquivo *.editorconfig*.

![Imposição de estilo de código no Visual Studio](../ide/media/VSGuide_CodeStyle.png)

## <a name="i-need-more-refactorings-and-code-fixes"></a>Preciso de mais correções de código e refatorações

O Visual Studio 2017 vem com muitas refatorações, ações de geração de códigos e correções de códigos. As linhas onduladas vermelhas representam erros, as linhas onduladas verdes representam avisos e os três pontos cinzas representam sugestões de código. Acesse as correções de código clicando no ícone de lâmpada/chave de fenda ou pressionando **Ctrl**+**.** ou **Alt**+**Enter**. Cada correção vem com uma janela de visualização que mostra a diferença do código em tempo real de como a correção funciona.

- As correções rápidas e refatorações comuns incluem:
  - *Renomear*
  - *Método Extract*
  - *Alterar assinatura do método*
  - *Gerar construtor*
  - *Método Generate*
  - *Mover Tipo para Arquivo*
  - *Adicionar Null-Check*
  - *Adicionar Parâmetro*
  - *Remover Usos Desnecessários*
  - Confira mais em nossa [documentação](https://aka.ms/refactorings)
- Crie sua própria refatoração ou correção de código com [analisadores Roslyn](https://github.com/dotnet/roslyn/wiki/Getting-Started-Writing-a-Custom-Analyzer-&-Code-Fix).
- Vários membros da comunidade codificaram extensões gratuitas que adicionam outras inspeções de código:
  - [Analisadores FXCop](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)
  - [Roslynator](https://marketplace.visualstudio.com/items?itemName=josefpihrt.Roslynator2017)
  - [SonarLint para Visual Studio](https://marketplace.visualstudio.com/items?itemName=SonarSource.SonarLintforVisualStudio2017)
  - [StyleCopAnalyzers](https://www.nuget.org/packages/stylecop.analyzers/)

![Refatorações no Visual Studio](../ide/media/VSGuide_CodeAnalysis.png)

## <a name="i-need-find-usages-go-to-implementation-navigate-to-decompiled-assemblies"></a>Preciso Localizar Usos, Ir Para Implementação, Navegar para Assemblies Descompiladas

O Visual Studio 2017 tem muitos recursos para ajudar você a pesquisar e navegar em sua base de código. Leia mais sobre os [recursos de Navegação de código](../ide/navigating-code.md)

| Recurso | Atalho | Detalhes/melhorias |
|- | - | -|
| Localizar Todas as Referências | **Shift**+**F12**| Os resultados são coloridos e podem ser agrupados por projeto, definição etc. Também é possível “bloquear” resultados. |
| Ir Para Implementação | **Ctrl**+**F12** | É possível usar “Ir para definição” na palavra-chave `override` para navegar até o membro substituído |
| Ir para definição | **F12** ou **Ctrl**+**Clique**| Ou pressione **Ctrl** enquanto clica para navegar até a definição |
| Inspecionar Definição | **Alt**+**F12** | Exibição embutida de uma definição |
| Visualizador de Estrutura | Linhas cinzas pontilhadas entre chaves | Passe o mouse para ver a estrutura do código |
| Navegação para assemblies descompilados | **F12** ou **Ctrl**+**Clique** | Navegue para a fonte externa (descompilada com o ILSpy) habilitando o recurso: **Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Avançado** > **Habilitar a navegação para fontes descompiladas**. |

![Ir para Todos e Localizar Todas as Referências](../ide/media/VSIDE_Productivity_Navigation.png)

## <a name="i-want-to-run-and-see-my-unit-tests"></a>Preciso executar e ver meus testes de unidade

Fizemos muitos aprimoramentos à experiência de teste no Visual Studio 2017. Use qualquer uma das nossas experiências de teste de unidade com as estruturas de teste MSTest v1, v2 MSTest, NUnit ou XUnit.

- A detecção de testes do **Gerenciador de Testes** está rápida na versão 15.6 (para obter melhores resultados, atualize para a versão mais recente do adaptador de teste).
- Organize seus testes no Gerenciador de Testes com nossa nova *classificação hierárquica* na versão 15.6.
- O [Live Unit Testing](../test/live-unit-testing.md) executa continuamente os testes afetados pelas alterações de código e atualiza os ícones do editor embutido para informar o status dos testes. Inclua ou exclua testes específicos ou projetos de teste pelo *Live Test Set*.

![Exibição de hierarquia do Gerenciador de Testes no Visual Studio](../ide/media/VSGuide_Testing.png)

## <a name="i-want-to-debug-my-code"></a>Quero depurar meu código

Nós adicionamos inúmeros recursos de depuração novos no Visual Studio 2017:

- *Executar até o clique* permite que você passe o mouse ao lado de uma linha de código, pressione o ícone verde 'executar' que é exibido e execute o programa até atingir essa linha.
- O novo **Auxiliar de Exceção** coloca as informações mais importantes, como qual variável é 'nula' em uma NullReferenceException, na parte superior da caixa de diálogo.
- A opção [Retroceder](../debugger/how-to-use-intellitrace-step-back.md) a depuração permite voltar para os pontos de interrupção ou para as etapas anteriores e exibir o estado do aplicativo como ele estava anteriormente.
- A opção [Depuração de instantâneo](/azure/application-insights/app-insights-snapshot-debugger) permite investigar o estado de um aplicativo Web online no momento em que uma exceção foi gerada (é necessário estar no Azure).

![Novo Auxiliar de Exceção no Visual Studio 2017](../ide/media/VSGuide_Debugging.png)

## <a name="i-want-to-use-version-control-with-my-projects"></a>Desejo usar o controle de versão com meus projetos

Você pode usar o Git ou o TFVC para armazenar e atualizar seu código no Visual Studio.

- Organize as alterações locais com o **Team Explorer** e use a barra de status para acompanhar confirmações e alterações pendentes.
- Configure a integração e a entrega contínuas de seus projetos no Visual Studio com nossa extensão [Ferramentas de Entrega Contínua para Visual Studio](https://marketplace.visualstudio.com/items?itemName=VSIDEDevOpsMSFT.ContinuousDeliveryToolsforVisualStudio) e adote um fluxo de trabalho de desenvolvedor Agile.

![Controle do código-fonte no Visual Studio](../ide/media/VSIDE_Productivity_SourceControl.png)

## <a name="what-other-features-do-i-need-to-know-about"></a>Quais outros recursos que preciso conhecer?

Aqui está uma lista dos recursos do editor e de produtividade para escrever códigos com mais eficiência. Pode ser necessário ativar alguns recursos, pois eles ficam desativado por padrão (eles podem indexar itens em sua máquina, são controversos ou atualmente são experimentais).

| Recurso | Detalhes | Como habilitar |
|-|-|-|
| Arquivo local no Gerenciador de Soluções | Realça o arquivo ativo no **Gerenciador de Soluções** | **Ferramentas** > **Opções** > **Projetos e Soluções** > **Acompanhar Item Ativo no Gerenciador de Soluções** |
| Adicionar usos para tipos em assemblies de referência e pacotes do NuGet | Mostra uma lâmpada com uma correção de código para instalar um pacote do NuGet para um tipo não referenciado | **Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Avançado** > **Sugerir usos para tipos em assemblies de referência** e **Sugerir usos para tipos em pacotes NuGet** |
| Habilitar análise de solução completa | Ver todos os erros na solução na **Lista de Erros** | **Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Avançado** > **Habilitar análise completa da solução** |
| Habilitar a navegação para origens descompiladas | Habilite Ir Para a Definição em tipos/membros de fontes externas e usar o descompilador ILSpy para mostrar os corpos de método | **Ferramentas** > **Opções** > **Editor de Texto** > **C#** > **Avançado** > **Habilitar navegação para fontes descompiladas** |
| Modo de conclusão/sugestão | Altera o comportamento de conclusão no IntelliSense – os desenvolvedores com experiência em IntelliJ tendem a alterar aqui a configuração padrão | **Menu** > **Editar** > **IntelliSense** > **Ativar/Desativar Modo de Preenchimento** |
| [CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md) | Exibe informações de referência de código e o histórico de alterações no editor | **Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens** > **CodeLens** |
| [Snippets de código](../ide/visual-csharp-code-snippets.md) | Ajudar a remover um texto clichê | Digite um nome de snippet e pressione **Tab** duas vezes. |

## <a name="missing-a-feature-that-makes-you-productive-or-experiencing-poor-performance"></a>Está faltando um recurso que melhora a sua produtividade ou está enfrentando um baixo desempenho?

Há várias maneiras de enviar comentários:

- Solicitações de recursos do .NET podem ser preenchidas em nosso [repositório GitHub](https://github.com/dotnet/roslyn/issues).
- As solicitações de recursos, os bugs e os problemas de desempenho do Visual Studio podem ser informados usando o ícone **Enviar Comentários** no canto superior direito da janela do Visual Studio.
