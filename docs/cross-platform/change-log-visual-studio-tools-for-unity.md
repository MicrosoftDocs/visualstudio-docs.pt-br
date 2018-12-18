---
title: Log de alterações (Ferramentas do Visual Studio para Unity, Windows) | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2018
ms.technology: vs-unity-tools
ms.topic: conceptual
ms.assetid: ea490b7e-fc0d-44b1-858a-a725ce20e396
author: TerryGLee
ms.author: tglee
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: da2e91e15572a9904115926447523d8dba23a36a
ms.sourcegitcommit: e481d0055c0724d20003509000fd5f72fe9d1340
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2018
ms.locfileid: "51000720"
---
# <a name="change-log-visual-studio-tools-for-unity-windows"></a>Log de alterações (Ferramentas do Visual Studio para Unity, Windows)
Log de alterações de Ferramentas do Visual Studio para Unity.

## <a name="3807"></a>3.8.0.7
 Lançado em 20 de setembro de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Depurador:**

    -   Corrigido um deadlock na biblioteca usada para se comunicar com o mecanismo de depuração do Unity, causando o congelamento do Visual Studio ou Unity, especialmente ao pressionar "Anexar ao Unity" ou ao reiniciar o jogo.

## <a name="3806"></a>3.8.0.6
 Lançado em 27 de agosto de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Correção do recarregamento de projetos e soluções.

## <a name="3805"></a>3.8.0.5
 Lançado em 20 de agosto de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Correção do descarte de assinatura de monitoramento de projeto.

## <a name="3804"></a>3.8.0.4
 Lançado em 14 de agosto de 2018

### <a name="new-features"></a>Novos recursos

-   **Avaliação:**

    -   Foi adicionado suporte para valores de ponteiro.

    -   Foi adicionado suporte para métodos genéricos.

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   O recarregamento inteligente com vários projetos foi alterado.

## <a name="3803"></a>3.8.0.3
 Lançado em 24 de julho de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Foi revertida a solução alternativa para um bug de desempenho do Unity que foi corrigido pelo Unity.

## <a name="3802"></a>3.8.0.2
 Lançado em 7 de julho de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Solução alternativa temporária para um bug de desempenho do Unity: armazenar em cache MonoIslands ao gerar projetos.

## <a name="3801"></a>3.8.0.1
 Lançado em 26 de junho de 2018

### <a name="new-features"></a>Novos recursos

-   **Depuração:**

    -   Foi adicionado suporte para comandos UserLog e UserBreak.

    -   Foi adicionado o suporte para carregamento do tipo lento (otimizando a carga da rede e a latência de resposta de depurador).

### <a name="bug-fixes"></a>Correções de bug

-   **Avaliação:**

    -   Melhorias na avaliação da expressão e na pesquisa de método de operador binário.

## <a name="3800"></a>3.8.0.0
 Lançado em 30 de maio de 2018

### <a name="new-features"></a>Novos recursos

-   **Depuração:**

    -   Foi adicionado suporte para exibir as variáveis em construções de assíncronas.

    -   Foi adicionado suporte para o processamento de tipos aninhados ao definir pontos de interrupção, para evitar avisos em construções do compilador.

-   **Integração:**

    -   Foi adicionado suporte para gramáticas textmate para sombreadores (a carga de trabalho do C++ não é mais necessária para coloração de código do sombreador).

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Não converta mais um pdb portátil para mdb ao usar o novo tempo de execução do Unity.

## <a name="3701"></a>3.7.0.1
 Lançado em 7 de maio de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Instalador:**

    -   Correção de problema de dependência ao usar builds experimentais.

## <a name="3700"></a>3.7.0.0
 Lançado em 7 de maio de 2018

### <a name="new-features"></a>Novos recursos

-   **Depuração:**

    -   Adição de suporte para depuração orquestrada (depuração de vários players/editores na mesma sessão do Visual Studio).

    -   Adição de suporte para depuração de player USB no Android.

    -   Adição de suporte para depuração de player UWP/IL2CPP.

-   **Avaliação:**

    -   Adição de suporte para especificadores hexadecimais.

    -   Experiência de avaliação da janela de inspeção aprimorada.

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Correção do uso de configurações de exceção.

-   **Geração do Projeto:**

    -   Exclusão de unidades de compilação do gerenciador de pacotes da geração.

## <a name="3605"></a>3.6.0.5
 Lançado em 13 de março de 2018

### <a name="new-features"></a>Novos recursos

-   **Geração do Projeto:**

    -   Adicionado o suporte para o gerador de projeto novo no Unity 2018.1.

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Foi corrigido o tratamento de estados corrompidos com projetos personalizados.

-   **Depurador:**

    -   Foi corrigida a configuração da próxima instrução.

## <a name="3604"></a>3.6.0.4
 Lançado em 5 de março de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Correção da detecção de versão Mono.

-   **Integração:**

    -   Correção dos problemas de timing com 2018.1 e ativação de plug-in.

## <a name="3603"></a>3.6.0.3
 Lançado em 23 de fevereiro de 2018

### <a name="new-features"></a>Novos recursos

-   **Geração do Projeto:**

    -   Suporte adicionado para o .NET Standard.

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Corrigida a detecção da estrutura de destino Unity.

-   **Depurador:**

    -   Corrigida a quebra de exceções que são lançadas fora do código do usuário.

## <a name="3602"></a>3.6.0.2
 Lançado em 7 de fevereiro de 2018

### <a name="new-features"></a>Novos recursos

-   **Integração:**

    -   Atualize a superfície da API do UnityMessage para 2017.3.

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Somente recarrega projetos em alterações externas (com a limitação).

## <a name="3601"></a>3.6.0.1
 Lançado em 24 de janeiro de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Correção de pdb automático para conversão de símbolo de depuração de mdb.

    -   Correção de chamada indireta para EditorPrefs.GetBool afetando o inspetor ao tentar alterar o tamanho da matriz.

## <a name="3600"></a>3.6.0.0
 Lançado em 10 de janeiro de 2018

### <a name="new-features"></a>Novos recursos

-   **Geração do Projeto:**

    -   Adicionado o suporte para o modelo de referência MonoIsland 2018.1.

-   **Avaliação:**

    -   Adicionado o suporte para o identificador de $exception.

-   **Depurador:**

    -   Adicionado o suporte para atributos de DebuggerHidden/DebuggerStepThrough com o novo tempo de execução do Unity.

-   **Assistentes:**

    -   Introduza 'Última' versão para os assistentes.

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Correção do cálculo de guid de projeto para projetos de player.

-   **Depurador:**

    -   Correção de uma corrida na manipulação de eventos recentes.

-   **Assistentes:**

    -   Atualize o contexto do roslyn antes de inserir o método.

## <a name="3503"></a>3.5.0.3
 Lançado em 9 de janeiro de 2018

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Correção de pdb automático para conversão de símbolo de depuração de mdb.

## <a name="3502"></a>3.5.0.2
 Lançado em 4 de dezembro de 2017

### <a name="new-features"></a>Novos recursos

-   **Integração:**

    -   Projetos do Unity agora são automaticamente recarregados no Visual Studio quando você adiciona ou remove um script do Unity.

-   **Depurador:**

    -   Adicionada uma opção para usar o depurador Mono compartilhado pelo Xamarin e pelo Visual Studio para Mac para depurar o Editor Unity.

    -   Suporte adicionado para arquivos de símbolo de depuração portátil.

### <a name="bug-fixes"></a>Correções de bug

-   **Integração:**

    -   Problemas de dependências de instalação corrigidos.

    -   O menu de ajuda da API de unidade fixa não está sendo exibido.

-   **Geração do Projeto:**

    -   Correção da geração de projetos do player ao trabalhar em um jogo UWP com o back-end IL2CPP/.NET 4.6.

    -   Correção da extensão .dll extra adicionada por engano ao arquivo do assembly.

    -   Correção do uso de um nível específico de compatibilidade da API do projeto em vez do global.

    -   Não force o sinalizador AllowAttachedDebuggingOfEditor do Unity, uma vez que o padrão agora é ‘true’.

## <a name="3402"></a>3.4.0.2
 Lançado em 19 de setembro de 2017

### <a name="new-features"></a>Novos recursos

-   **Geração do Projeto:**

    -   Adicionado suporte para unidades de compilação assembly.json.

    -   Cópia de assemblies do Unity para a pasta do projeto interrompida.

-   **Depurador:**

    -   Adicionado suporte para definir a próxima instrução com o novo tempo de execução do Unity.

    -   Adicionado suporte para o tipo Decimal com o novo tempo de execução do Unity.

    -   Adicionado suporte para conversões implícitas/explícitas.

### <a name="bug-fixes"></a>Correções de bug

-   **Avaliação:**

    -   Corrigida a criação de matriz com tamanho implícito.

    -   Corrigidos os itens com locais gerados pelo compilador.

-   **Geração do Projeto:**

    -   Corrigida a referência a Microsoft.CSharp fixa para nível de API 4.6.

## <a name="3302"></a>3.3.0.2
 Lançado em 15 de agosto de 2017

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Correção da geração de solução do Visual Studio no Unity 5.5 e nas versões anteriores.

## <a name="3300"></a>3.3.0.0
 Lançado em 14 de agosto de 2017

### <a name="new-features"></a>Novos recursos

-   **Avaliação:**

    -   Adicionado suporte para criação de structs com o novo tempo de execução do Unity.

    -   Adicionado suporte minimalista para ponteiros.

### <a name="bug-fixes"></a>Correções de bug

-   **Avaliação:**

    -   Corrigida a invocação de método em tipos primitivos.

    -   Corrigida a avaliação de campo com tipos marcados com BeforeFieldInit.

    -   Corrigidas as chamadas sem suporte com operadores binários (subtract).

    -   Corrigidos problemas ao adicionar itens ao Visual Studio Watch.

-   **Geração do Projeto:**

    -   Corrigidas referências de nome de assembly com arquivos mcs.rsp.

    -   Corrigidas definições com níveis de API.

## <a name="3200"></a>3.2.0.0
 Lançado em 10 de maio de 2017

### <a name="new-features"></a>Novos recursos

-   **Instalador:**

    -   Adicionado suporte para limpar o cache MEF.

### <a name="bug-fixes"></a>Correções de bug

-   **Editor de Códigos:**

    -   Corrigida classificação/conclusão com atributos personalizados.

    -   Corrigida cintilação com mensagens Unity.

## <a name="3100"></a>3.1.0.0
 Lançado em 7 de abril de 2017

### <a name="new-features"></a>Novos recursos

-   **Depurador:**

    -   Suporte adicionado para o novo tempo de execução do Unity (com compatibilidade com .NET 4.6/C# 6).

-   **Geração do Projeto:**

    -   Suporte adicionado para o perfil do .NET 4.6.

    -   Suporte adicionado para arquivos mcs.rsp.

    -   Sempre habilite a opção de compilação não segura quando o Unity 5.6 for usado.

    -   Suporte adicionado para a geração de projeto "Player" ao usar a plataforma da Windows Store e o back-end il2cpp.

### <a name="bug-fixes"></a>Correções de bug

-   **Editor de Códigos:**

    -   Posição fixa do cursor após a inserção do método com preenchimento automático.

-   **Geração do Projeto:**

    -   Versão do assembly removido após o processamento.

## <a name="3001"></a>3.0.0.1
 Lançado em 7 de março de 2017

### <a name="this-version-includes-all-new-features-and-bug-fixes-introduced-with-28x-series"></a>Esta versão inclui todos os novos recursos e as correções de bugs introduzidas com a série 2.8.x.

## <a name="2820---30-preview-3"></a>2.8.2.0 – 3.0 versão prévia 3
 Lançado em 25 de janeiro de 2017

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do Projeto:**

    -   Corrigida regressão em que projetos de Plug-Ins eram referenciados duas vezes, primeiro como uma DLL binária em então como uma referência de projeto.

## <a name="2810---30-preview-2"></a>2.8.1.0 – 3.0 versão prévia 2
 Lançado em 23 de janeiro de 2017

### <a name="bug-fixes"></a>Correções de bug

-   **Editor de Códigos:**

    -   Corrigida uma falha ao iniciar uma declaração de atributo sem preenchimento de chaves.

-   **Depurador:**

    -   Corrigidos pontos de interrupção com co-rotinas no novo compilador/tempo de execução do Unity.

    -   Adicionado aviso no caso de um ponto de interrupção não vinculável (quando nenhum local de origem correspondente é encontrado).

-   **Geração do Projeto:**

    -   Corrigida a geração de csproj com caracteres especiais/localizados.

    -   Corrigidas referências fora de Ativos, como Biblioteca (como o SDK do Facebook).

-   **Diversos:**

    -   Adicionada verificação para evitar a execução do Unity ao instalar ou desinstalar.

    -   Mudado para https para ter a documentação do Unity remota como destino.

## <a name="2800---30-preview"></a>2.8.0.0 – 3.0 versão prévia
 Lançado em 17 de novembro de 2016

### <a name="new-features"></a>Novos recursos

-   **Geral:**

    -   Adicionado suporte do instalador do Visual Studio 2017.

    -   Adicionado suporte à extensão do Visual Studio 2017.

    -   Adicionado suporte a localização.

-   **Editor de Códigos:**

    -   Adicionado C# IntelliSense para mensagens do Unity.

    -   Adicionada coloração do código C# para mensagens do Unity.

-   **Depurador:**

    -   Adicionado suporte para `is`, `as`, conversão direta, `default`, expressões `new`.

    -   Adicionado suporte para expressões concat de cadeia de caracteres.

    -   Adicionado suporte para exibição hexadecimal de valores inteiros.

    -   Adicionado suporte para a criação de novas variáveis temporárias (instruções).

    -   Adicionado suporte para conversões implícitas de primitivas.

    -   Adicionadas mensagens de erro melhores quando um tipo é esperado ou não é encontrado.

-   **Geração do Projeto:**

    -   Removido o sufixo CSharp dos nomes de projeto.

    -   Removida referência a um arquivo de destino msbuild em todo o sistema.

-   **Assistentes:**

    -   Adicionado suporte para mensagens do Unity em tipos não de Comportamento, como Editor ou EditorWindow.

    -   Mudado para Roslyn para injetar e formatar mensagens do Unity.

### <a name="bug-fixes"></a>Correções de bug

-   **Depurador:**

    -   Corrigido um bug que provocava a falha do Unity ao avaliar tipos genéricos.

    -   Corrigido o tratamento de tipos anuláveis.

    -   Corrigido o tratamento de enums.

    -   Corrigido o tratamento de tipos de membros aninhados.

    -   Corrigido acesso do indexador de coleção.

    -   Corrigido o suporte para depurar quadros do iterador com o novo Compilador C#.

-   **Geração do Projeto:**

    -   Corrigido um bug que impedia a compilação ao ter o player da Web do Unity como destino.

    -   Corrigido um bug que impedia a compilação ao compilar um script com um nome de arquivo codificado para web.

## <a name="2300"></a>2.3.0.0
 Lançado em 14 de julho de 2016

### <a name="new-features"></a>Novos recursos

-   **Geral:**

    -   Adicionada uma opção para desabilitar os logs de console do Unity na lista de erros do Visual Studio.

    -   Adicionada uma opção para permitir a modificação de propriedades de projeto geradas.

-   **Depurador:**

    -   Adicionados visualizadores de cadeia de caracteres de texto, XML, HTML e JSON.

-   **Assistentes:**

    -   Adicionados MonoBehaviors ausentes.

### <a name="bug-fixes"></a>Correções de bug

-   **Geral:**

    -   Corrigido um conflito com ReSharper que impedia a exibição de controles dentro de configurações do Visual Studio.

    -   Corrigido um conflito com o Xamarin que impedia a depuração em alguns casos.

-   **Depurador:**

    -   Corrigido um problema que fazia o Visual Studio congelar durante a depuração.

    -   Corrigido um problema com pontos de interrupção de função no Visual Studio 2015.

    -   Corrigidos vários problemas de avaliação de expressão.

## <a name="2200"></a>2.2.0.0
 Lançado em 4 de fevereiro de 2016

### <a name="new-features"></a>Novos recursos

-   **Assistentes:**

    -   Adicionada pesquisa inteligente ao assistente **Implementar MonoBehavior**.

    -   Assistentes passaram a reconhecer o contexto; por exemplo, mensagens de NetworkBehavior só estão disponíveis ao trabalhar com um NetworkBehavior.

    -   Adicionado suporte para mensagens de NetworkBehavior nos assistentes.

-   **Interface do Usuário:**

    -   Adicionada uma opção para configurar a visibilidade das mensagens MonoBehavior.

    -   Remoção das páginas de propriedades do Visual Studio que não são relevantes para projetos do Unity.

### <a name="bug-fixes"></a>Correções de bug

-   **Geração do projeto:**

    -   Corrigidas referências a UnityEngine e UnityEditor no Unity 4.6.

    -   Corrigida a geração de arquivos de projeto quando Unity está em execução no OSX.

    -   Corrigido o tratamento de nomes de projeto contendo caracteres de sustenido (#).

    -   Restringidos projetos gerados a 4 C#.

-   **Depurador:**

    -   Corrigido um problema com a avaliação da expressão ao depurar dentro de uma co-rotina do Unity.

    -   Corrigido um problema que fazia o Visual Studio congelar durante a depuração.

-   **Interface do Usuário:**

    -   Corrigida uma incompatibilidade com a extensão [Tabs Studio](https://tabsstudio.com/) do Visual Studio.

-   **Instalador:**

    -   Suporte para a instalação do VSTU em todos os computadores (instalar para todos os usuários), criando entradas de Registro HKLM.

    -   Corrigidos problemas com a desinstalação do VSTU quando a mesma versão do VSTU é instalada para várias versões diferentes do Visual Studio. Por exemplo, quando tanto VSTU **2015** 2.1.0.0 quanto VSTU **2013** 2.1.0.0 foram instalados.

## <a name="2100"></a>2.1.0.0
 Lançado em 8 de setembro de 2015

### <a name="new-features"></a>Novos recursos

-   Suporte para Unity 5.2

### <a name="bug-fixes"></a>Correções de bug

-   Exibir itens de menu no Unity < 4.2

-   Uma mensagem de erro não é mais exibida quando o Visual Studio bloqueia arquivos IntelliSense XML.

-   Processe pontos de interrupção <\<When Changed>> condicionais quando o argumento condicional não for um valor booliano.

-   Corrigidas referências aos assemblies UnityEngine e UnityEditor para aplicativos da Windows Store.

-   Corrigido erro ao executar em etapas no depurador: não é possível executar em etapas, exceção geral.

-   Corrigidos pontos de interrupção de contagem de ocorrências no Visual Studio 2015.

## <a name="2000"></a>2.0.0.0
 Lançado em 20 de julho de 2015

### <a name="bug-fixes"></a>Correções de bug

-   **Integração do Unity:**

    -   Corrigida a conversão de símbolos de depuração criados com o Visual Studio 2015 ao importar uma DLL e seus símbolos de depuração (PDB).

    -   Sempre gere arquivos MDB ao importar DLL e seus símbolos de depuração (PDB), exceto quando um arquivo MDB também for fornecido.

    -   Corrigida poluição do diretório de projeto do Unity com um diretório obj.

    -   Corrigida a geração de referências a System.Xml.Link e System.Runtime.Serialization.

    -   Adicionado suporte para vários assinantes aos ganchos de API de geração de arquivo de projeto.

    -   Sempre conclua a geração do arquivo de projeto mesmo quando um dos arquivos a ser gerado estiver bloqueado.

    -   Adicionado suporte para curingas * no filtro de extensão de arquivo ao especificar os arquivos a serem incluídos no projeto C#.

-   **Integração com o Visual Studio:**

    -   Corrigido um problema de compatibilidade com Productivity Power Tools.

    -   Corrigida a geração de MonoBehaviors em torno de declarações de representantes e eventos.

-   **Depurador:**

    -   Corrigido um congelamento potencial durante a depuração.

    -   Corrigido um problema em que locais não eram exibidos em determinados registros de ativação.

    -   Corrigida a inspeção de matrizes vazias.

## <a name="1990---20-preview-2"></a>1.9.9.0 – 2.0 versão prévia 2
 Lançado em 2 de abril de 2015

### <a name="new-features"></a>Novos recursos

-   **Explorador de Projeto do Unity:**

    -   renomeie a classe automaticamente ao renomear um arquivo no Explorador de Projeto do Unity (consulte a caixa de diálogo **Opções**).

    -   Selecione automaticamente scripts recém-criados no Explorador de Projeto do Unity.

    -   Acompanhe o script ativo no Explorador de Projeto do Unity (consulte a caixa de diálogo **Opções**).

    -   Faça a sincronização dupla do Gerenciador de Soluções do Visual Studio (consulte a caixa de diálogo **Opções**).

    -   Adote ícones do Visual Studio no Explorador de Projeto do Unity.

-   **Depurador:**

    -   selecione o destino de depuração ativo em uma lista de destinos de depuração salvos ou usados recentemente (consulte a caixa de diálogo **Opções**).

    -   Crie pontos de interrupção de função em métodos MonoBehavior e aplique-os a várias classes de MonoBehavior.

    -   Dê suporte à Criação de ID de Objeto no depurador.

    -   Dê suporte à contagem de ocorrências de ponto de interrupção no depurador.

    -   Dê suporte a quebra na exceção no depurador (Experimental. consulte a caixa de diálogo **Opções**).

    -   Dê suporte à criação de objetos e matrizes ao avaliar expressões no depurador.

    -   Dê suporte à comparações nula ao avaliar expressões no depurador.

    -   Filtre membros obsoletos em janelas Inspeção do depurador.

-   **Instalador:**

    -   otimizadas as Ferramentas do Visual Studio para o registro de extensão do Unity.

    -   Instale as Ferramentas do Visual Studio para o pacote do Unity para Unity 5.

-   **Documentação:** melhore o desempenho da geração de documentação.

-   **Assistentes:** dê suporte a novos métodos MonoBehavior para Unity 4.6 e Unity 5.

-   **Unity:** pesquise sinalizadores não seguros e definições personalizadas em arquivos .rsp durante a geração do arquivo de projeto.

-   **Interface do usuário:** adicionada a caixa de diálogo **Opções** das Ferramentas do Visual Studio para Unity no Visual Studio.

### <a name="bug-fixes"></a>Correções de bug

-   **Explorador de Projeto do Unity:**

    -   Atualize o Explorador de Projeto do Unity depois que os arquivos forem movidos ou renomeados do Gerenciador de Soluções do Visual Studio.

    -   Preserve seleções ao renomear arquivos no Explorador de Projeto do Unity.

    -   Previna a expansão e o recolhimento automáticos quando o usuário clicar duas vezes em arquivos Explorador de Projeto do Unity.

    -   Certifique-se de que arquivos recém-selecionados estejam visíveis no Explorador de Projeto do Unity.

-   **Depurador:**

    -   Previna um possível congelamento do Visual Studio ao avaliar expressões no depurador.

    -   Certifique-se de que as invocações de método ocorram no domínio adequado no depurador.

-   **Unity:**

    -   Corrija o local do UnityVS.OpenFile com o Unity 5.

    -   Corrija o local do pdb2mdb com o Unity 5.

    -   Previna uma possível exceção durante a geração do arquivo de projeto.

    -   Previna um possível congelamento ao executar Unity em OSX.

    -   Lide com exceções internas.

    -   Envie logs do console do Unity para a lista de erros do VS.

-   **Documentação:** corrigir a geração de documentação a nova documentação do Unity.

-   **Projeto:** mova e renomeie arquivos .meta do Unity quando necessário, até mesmo em pastas.

-   **Assistentes:** corrigem a ordem dos parâmetros do método MonoBehavior ao gerar o código.

-   **Interface do Usuário:** dá suporte a temas do Visual Studio para ícones e menu de contexto.

## <a name="1980---20-preview"></a>1.9.8.0 – 2.0 versão prévia
 Lançado em 12 de novembro de 2014

### <a name="new-features"></a>Novos recursos

-   Dê suporte para Visual Studio 2015.

-   Coloração de código para sombreadores do Unity no Visual Studio 2015.

-   Aprimorada a visualização de valores durante a depuração:

    -   melhor visualização para ArrayLists, Listas, Tabelas de Hash e Dicionários.

    -   Mostra membros Não Públicos e membros Estáticos como categorias em exibições de inspeção e local.

    -   Aprimorada a exibição de SerializedProperty do Unity para avaliar apenas o campo de valor válido para a propriedade.

    -   Suporte a DebuggerDisplayAttribute para classes e structs.

    -   Suporte a DebuggerTypeProxyAttribute.

-   Faça a inserção dos métodos MonoBehaviour usando nossos assistentes para respeitar as convenções de codificação do usuário.

-   Implemente suporte a Modelos de Texto de Tempo de Compilação em projetos gerados no UnityVS.

-   Implemente suporte a recursos ResX em projetos gerados no UnityVS.

-   Dê suporte a sombreadores de abertura no Visual Studio do Unity.

### <a name="bug-fixes"></a>Correções de bug

-   Limpe os soquetes antes de iniciar o jogo no Unity depois de Anexar e Jogar ter sido disparado no Visual Studio. Isso corrige alguns problemas com a estabilidade da conexão entre o Unity e o VS ao usar Anexar e Reproduzir.

-   Evite chamar métodos na interface do depurador de mecanismo de script do Unity propensos a congelar o Unity. Isso corrige o congelamento do Unity ao anexar o depurador.

-   Corrija a exibição de pilhas de chamadas quando não houver símbolos disponíveis.

-   Não registre o retorno de chamada de log se não for necessário.

## <a name="1920"></a>1.9.2.0
 Lançado em 9 de outubro de 2014

### <a name="new-features"></a>Novos recursos

-   Melhore a detecção de jogadores do Unity.

-   Ao usar nosso abridor de arquivos, faça o Unity passar o número de linha, bem como o nome do arquivo.

-   Assume como padrão a documentação online do Unity se não houver documentação local.

### <a name="bug-fixes"></a>Correções de bug

-   Corrija falhas potenciais do Unity ao atingir um ponto de interrupção depois de recarregar um domínio.

-   Corrija exceções mostradas no console do Unity ao fechar nossas janelas Configuração ou Sobre depois de um recarregamento de domínio.

-   Corrija a detecção do Unity 64 bits em execução localmente.

-   Corrija a filtragem de MonoBehaviours por versão do Unity em assistentes.

-   Corrija o bug em que todos os ativos eram incluídos nos arquivos de projeto se o filtro de extensão estivesse vazio.

## <a name="1910"></a>1.9.1.0
 Lançado em 22 de setembro de 2014

### <a name="new-features"></a>Novos recursos

-   Otimize o ponto de interrupção da associação para locais de origem.

-   Dê suporte para métodos sobrecarregados na Avaliação de Expressão do depurador.

-   Dê a primitivas de conversão boxing e tipos de valor na Avaliação de Expressão do depurador.

-   Dê suporte à recriação do ambiente de variáveis locais C# ao depurar métodos anônimos.

-   Exclua e renomeie arquivos .meta ao excluir ou renomear arquivos do Visual Studio.

### <a name="bug-fixes"></a>Correções de bug

-   Corrija a manipulação de temas do Visual Studio. Anteriormente, as caixas de diálogo em temas pretos podiam aparecer vazias.

-   Corrija o congelamento do Unity ao conectar o depurador enquanto o Unity está recompilando.

-   Corrija pontos de interrupção ao depurar editores ou jogadores remotos compilados em outro sistema.

-   Corrija uma possível falha do Visual Studio quando um ponto de interrupção é atingido.

-   Corrija a associação de pontos de interrupção para evitar que pontos de interrupção apareçam como descarregados.

-   Corrija a manipulação de escopo de variáveis no depurador para evitar variáveis dinâmicas que pareçam fora do escopo.

-   Corrija a pesquisa de membros estáticos na Avaliação de Expressão do depurador.

-   Corrija a exibição de tipos na Avaliação de Expressão do depurador para mostrar propriedades e campos estáticos.

-   Corrija a geração da solução quando os nomes de projeto do Unity incluírem caracteres especiais que o Visual Studio proíba (problema de Conexão nº 948666).

-   Corrija o pacote Unity de Ferramentas do Visual Studio para interromper imediatamente o envio de eventos do console após a opção ter sido desmarcada (problema de conexão nº 933357).

-   Corrija a detecção de referências para regenerar corretamente referências a novas APIs como UnityEngine.UI nos projetos gerados do UnityVS.

-   Corrija o instalador para exigir que o Visual Studio esteja fechado antes da instalação para evitar instalações corrompidas.

-   Corrija o instalador para instalar os Assemblies de Referência do Unity como um componente autônomo apropriado, compartilhado entre todas as versões do VSTU.

-   Corrija scripts de abertura com VSTU em versões de 64 bits do Unity.

## <a name="1900"></a>1.9.0.0
 Lançado em 29 de julho de 2014

### <a name="new-features"></a>Novos recursos

-   Na janela Anexar Depurador do Unity, adicione a capacidade de inserir um IP personalizado e uma porta para depurar.

-   Adicione a opção de configuração para definir o Unity para executar em segundo plano ou não.

-   Adicione a opção de configuração para gerar arquivos de solução e projeto ou somente os arquivos de projeto.

-   Destino de inicialização: escolha Anexar ao Unity ou Anexar ao Unity e Reproduzir.

-   Exibição de matrizes multidimensionais no depurador.

-   Lide com novas portas de depuração do Player do Unity.

-   Lide com referências a novos assemblies do Unity como os assemblies da GUI do Unity 4.6.

-   Desconstrói fechamentos para exibir corretamente as variáveis locais durante a depuração.

-   Desconstrói variáveis de iteradores geradas em argumentos ao depurar.

-   Preserve o estado do Explorador de Projeto do Unity depois de recarregar um projeto.

-   Adicione um comando para sincronizar o Explorador de Projeto do Unity com o documento atual.

### <a name="bug-fixes"></a>Correções de bug

-   Corrija os pontos de interrupção condicionais cujas condições sejam definidas antes de iniciar o depurador.

-   Corrija referências ao UnityEngine para evitar avisos.

-   Corrija versões de análise para betas do Unity.

-   Corrija o problema em que variáveis não seriam exibidas na janela de variáveis locais ao atingir um ponto de interrupção ou execução em etapas.

-   Corrija as dicas de ferramentas de variáveis no Visual Studio 2013.

-   Corrija a geração da documentação do IntelliSense para Unity 4.5.

-   Corrija a comunicação entre Unity/Visual Studio depois de um recarregamento de domínio (reproduzir/parar no Unity).

-   Corrija a manipulação de partes dos temas do Visual Studio.

> [!IMPORTANT]
>  Sendo C# a linguagem predominante no ecossistema do Unity (os novos Exemplos de Ativo estão em C#, a documentação do Unity assumirá C# como padrão), removemos o nosso suporte básico para UnityScript e Boo para focar melhor na experiência do C#. Como resultado, soluções VSTU agora são somente C# e são muito mais rápidas para carregar.

## <a name="1820"></a>1.8.2.0
 Lançado em 7 de janeiro de 2014

### <a name="new-features"></a>Novos recursos

-   Aplique uma solução alternativa a um problema na camada de rede do mecanismo de script do Unity em Mavericks para a descoberta remota de editores.

-   Lide com novas portas para descobrir jogadores remotos do Unity.

-   Consulte o assembly do UnityEngine específico para o destino de build atual.

-   Adicione configuração para filtrar arquivos para incluir em projetos gerados.

-   Adicione configuração para desabilitar o envio de logs de console à lista de erros do Visual Studio. Isso será útil se você estiver usando o PlayMaker ou o Console Pro, uma vez que pode haver apenas um retorno de chamada registrado no Unity para receber os logs do console.

-   Adicione configuração para desabilitar a geração de símbolos de depuração do mdb. Isso será útil se você mesmo estiver gerando o mdb.

### <a name="bug-fixes"></a>Correções de bug

-   Corrija uma regressão quando arquivos abertos no VS do Unity >=4.2 perderiam IntelliSense.

-   Corrija nossas caixas de diálogo do VS para tratar de temas personalizados.

-   Corrija o fechamento no menu de contexto do UPE.

-   Previna falhas no Unity quando o assembly gerado específico da versão estiver fora de sincronia.

## <a name="1810"></a>1.8.1.0
 Lançado em 21 de novembro de 2013

### <a name="new-features"></a>Novos recursos

-   Ajustados os assistentes MonoBehaviour com APIs do Unity 4.3.

-   Assistentes de MonoBehaviour filtram APIs do Unity dependendo da versão que você usa.

-   Adicione uma referência ao System.Xml.Linq aos projetos para Unity > 4.1.

-   Melhore as chamadas a Debug.Log para não incluir o início do stracktrace na mensagem.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido um bug em que interferiríamos no tratamento padrão de arquivos JavaScript no Visual Studio.

-   Corrigido um pixel branco exibido no VS, desta vez de verdade.

-   Corrigida a exclusão do assembly UnityVS.VersionSpecific no caso de ele ser marcado como somente leitura por um SCM.

-   Corrigidas exceções ao criar soquetes no pacote do UnityVS.

-   Corrigida uma falha no Visual Studio ao carregar imagens de estoque de assemblies do Visual Studio.

-   Corrigido um bug na geração do UnityVS.VersionSpecific para compilações de origem do Unity.

-   Corrigido um possível congelamento ao abrir um soquete no pacote do Unity.

-   Corrigido o tratamento do projeto do Unity com um traço (-) no nome.

-   Corrigidos scripts de abertura do Unity para não confundir a ordem ALT+TAB para o Unity 4.2 e superiores.

## <a name="1800"></a>1.8.0.0
 Lançado em 24 de setembro de 2013

### <a name="new-features"></a>Novos recursos

-   Velocidade de conexão do depurador drasticamente aprimorada.

-   Trate automaticamente a navegação para arquivo e linha no Unity 4.2 e posteriores.

-   Pontos de interrupção condicionais.

-   O gerador de arquivo de projeto agora trata de modelos T4.

-   Atualize os assistentes de MonBehavior com novas APIs.

-   Documentação do IntelliSense em C# para tipos do Unity.

-   Avaliação de expressões aritméticas e lógicas.

-   Melhor descoberta dos editores remotos para a visualização de depuração remota.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido um bug em que perderíamos um thread no VS depois de desconectar o depurador.

-   Corrigido um pixel branco exibido no VS.

-   Corrigido o tratamento de cliques no ícone da barra de status.

-   Corrigida a geração de referências com assemblies em pastas de Plug-Ins.

-   Corrigida a criação de soquetes do pacote do UnityVS em caso de exceções.

-   Corrigida a detecção de novas versões do UnityVS.

-   Corrigido o aviso do gerenciador de licenças quando a licença expirou.

-   Corrigido um bug que poderia tornar a lista de processo vazia na janela de anexar depurador ao processo do VS.

-   Corrigidos valores inconstantes de boolianos na exibição local.

## <a name="1220"></a>1.2.2.0
 Lançado em 9 de julho de 2013

### <a name="bug-fixes"></a>Correções de bug

-   Lide com nomes totalmente qualificados no avaliador de expressão.

-   Corrigido um congelamento relacionado a tratamento de exceção em que o mecanismo de script do Unity envia-nos dados de stackframe incorretos.

-   Corrigido o processo de build para destinos da Web.

-   Corrigido um erro poderia ocorrer se o Visual Studio fosse iniciado e um arquivo excluído estivesse na lista de arquivos a abrir na inicialização.

-   Corrigido o UnityVS.OpenFile para lidar com arquivos não de script, como sombreadores compilados.

-   Agora fazemos referência a Boo.Lang e UnityScript.Lang de todos os projetos C#.

-   Corrigida a geração de referências em projetos se o projeto tiver caracteres especiais.

-   Aplique a solução alternativa a um problema de VS em que chamadas de método para projetos descartados disparariam vários NullReferenceException MessageBox.

-   Corrigido o tratamento de assemblies do Unity 4.2 Beta.

## <a name="1210"></a>1.2.1.0
 Lançado em 9 de abril de 2013

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a implantação local dos assemblies do Unity para a conclusão de código no caso de um erro de E/S (como arquivos somente leitura ou arquivos bloqueados pelo Visual Studio).

-   Corrigida uma regressão em que abrir um script do Unity não se concentraria no arquivo se ele já estivesse aberto Visual Studio.

-   Corrigido o problema de desempenho do novo tratamento de exceção.

-   Corrigida a associação de pontos de interrupção em algumas DLLs externas.

## <a name="1200"></a>1.2.0.0
 Lançado em 25 de março de 2013

### <a name="new-features"></a>Novos recursos

-   Velocidade de conexão do depurador drasticamente aprimorada.

-   Explorador de Projeto do Unity otimizado para projetos maiores.

-   Respeite as configurações do Visual Studio para quebrar (ou não) em exceções com e sem tratamento.

-   Respeite a configuração do Visual Studio para chamar ToString em variáveis locais.

-   Adicione novo menu Depurar -> Anexar depurador do Unity, que você pode usar para depurar players do Unity.

-   Preserve projetos personalizados adicionados à solução do UnityVS ao gerar o arquivo de solução.

-   Adicione novo atalho de teclado CTRL+ALT+M -> CTRL+H para exibir a documentação do Unity para a função do Unity ou membro na posição do cursor.

-   Leve arquivos de resposta do compilador (rsp) em consideração ao compilar do Visual Studio.

-   Desconstrua os tipos gerados pelo compilador para mostrar variáveis ao depurar métodos do gerador.

-   Simplifique a depuração remota eliminando a necessidade de configurar uma pasta compartilhada para o Unity. Agora você apenas precisa ter acesso ao seu projeto do Unity do Windows.

-   Instale um perfil personalizado do Unity como um perfil de destino do .net padrão. Isso corrige todos os falsos positivos ReSharper poderia mostrar.

-   Aplique uma solução alternativa ao bug do mecanismo de script do Unity para que o depurador não quebre em threads não registrados corretamente.

-   Retrabalhe o abridor de arquivo para evitar uma condição de corrida no VS em que ele alegava poder abrir arquivos, enquanto falhava na solicitação de abertura de arquivo.

-   O UnityVS agora está pedindo para atualizar o build quando o VS está compilando o projeto e não mais no salvamento de arquivo.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido nosso perfil .net personalizado

-   Corrigida a integração de temas, isso corrige os problemas com o tema escuro do VS 2012.

-   Corrigido o atalho de comportamento rápido no VS 2012.

-   Corrigido um problema execução em etapas que poderia acontecer ao depurar e um thread não principal atingia um ponto de interrupção.

-   Corrigida a conclusão do UnityScript e do Boo de aliases de tipo, como int.

-   Corrigida exceção ao escrever uma nova cadeia de caracteres UnityScript ou Boo.

-   Corrigidas exceções nos menus do Unity quando uma solução não era carregada.

-   Corrigido o bug UVS-48: digitar aspas duplas às vezes produz um erro e interrompe toda a função (conclusão de código, realce de sintaxe etc).

-   Corrigido o bug UVS-46: arquivo de script aberto (UnityScript) duplicado ao clicar na Lista de Erros do Visual Studio.

-   Corrigido o bug UVS-42: o logotipo de conectividade do Unity na barra de status não trata eventos de mouse no VS 2012.

-   Corrigido o bug UVS-44: CTRL+SHIFT+Q não está disponível no VS 2012 para MonoBehaviours Rápidos.

-   Corrigido o bug UVS-40: itens selecionados no Explorador de Projeto do Unity são ilegíveis quando a janela está inativa no tema "escuro" do VS2012.

-   Corrigido o bug UVS-39: problema ao criar tokens de cadeias de caracteres de escape.

-   Corrigido o bug UVS-35: invocar ToString em objetos ao inspecionar variáveis.

-   Corrigido o bug UVS-27: inconsistência da janela Ir Para Símbolo com tema "escuro" no VS2012.

-   Corrigido o bug UVS-11: locais em co-rotinas.

## <a name="1100---beta-release"></a>1.1.0.0 – versão beta
 Lançado 9 de março, de 2013

## <a name="10130"></a>1.0.13.0
 Lançado em 21 de janeiro de 2013

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido um travamento do Visual Studio que poderia acontecer se o depurador de destino estivesse enviando eventos de thread inválidos. Isso normalmente aconteceria ao depurar um Unity remoto em OSX.

-   Corrigido um travamento do Visual Studio que poderia ocorrer se uma exceção desligasse o depurador.

-   Corrigidos nossos auxiliares MonoBehavior quando um MonoBehavior C# está em um namespace.

-   Corrigidas dicas de ferramenta do depurador para UnityScript no Visual Studio 2012.

-   Corrigida a geração de projeto quando apenas constantes de depuração são alteradas do Unity.

-   Corrigida a navegação pelo teclado no Explorador de Projeto do Unity.

-   Corrigida a coloração do UnityScript para cadeias de caracteres de escape.

-   Corrigido o abridor de arquivo para estimar melhor o nome do projeto quando usado fora do Unity. Isso é necessário quando o usuário utiliza um abridor de arquivo de terceiros no Unity que delega para o UnityVS.

-   Corrigido o tratamento de mensagens longas enviadas do Unity para o UnityVS. Antes disso, mensagens longas poderiam provocar falhas em nossa parte de mensagens do UnityVS. Como consequência, às vezes o UnityVS não abre um arquivo do Unity.

## <a name="10120"></a>1.0.12.0
 Lançado em 3 de janeiro de 2013

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido o travamento do Visual Studio que poderia acontecer quando o Visual Studio estava excluindo um ponto de interrupção.

-   Corrigido um bug em que alguns pontos de interrupção não seriam atingidos depois de o Unity ter recompilado scripts de jogo.

-   Corrigido o depurador para notificar corretamente o Visual Studio quando pontos de interrupção eram desvinculados.

-   Corrigido um problema de registro que poderia impedir o depurador do Visual Studio de depurar programas nativos.

-   Corrigida uma exceção que poderia acontecer ao avaliar expressões Boo e UnityScript.

-   Corrigida uma regressão em que alterar o nível da API .net no Unity não dispararia uma atualização dos arquivos de projeto.

-   Corrigida uma falha de API em que o código do usuário não conseguia participar do manipulador de retorno de chamada de log.

## <a name="10110"></a>1.0.11.0
 Lançado em 28 de novembro de 2012

### <a name="new-features"></a>Novos recursos

-   Suporte oficial do Unity 4.

-   Manipulação de scripts do Explorador de Projeto do Unity.

-   Integração na janela Navegar Para do Visual Studio.

-   Análise de mensagem do console Info, de modo que clicar na Lista de Erros o levará ao primeiro stackframe com símbolos.

-   Adicione uma [API](../cross-platform/customize-project-files-created-by-vstu.md) para permitir que o usuário participe da geração do projeto.

-   Adicione uma [API](../cross-platform/share-the-unity-log-callback-with-vstu.md) para permitir que o usuário participe de LogCallback.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida regressão no segundo plano do Explorador de Projeto do Unity no Visual Studio 2012.

-   Corrigida a geração de projeto para usuários do perfil .net completo.

-   Corrigida a geração de projeto para usuários do destino da Web.

-   Corrigida a geração de projeto para incluir símbolos de compilação DEBUG e TRACE como o Unity faz.

-   Corrigida falha ao usar caracteres especiais em nossa janela Ir Para Símbolo.

-   Corrigida falha se não pudermos injetar nosso ícone na barra de status do Visual Studio.

## <a name="10100"></a>1.0.10.0
 Lançado em 9 de outubro de 2012

### <a name="bug-fixes"></a>Correções de Bug

-   Corrigida a tela de fundo do Explorador de Projeto do Unity no Visual Studio 2010.

-   Corrigido um congelamento do Visual Studio que poderia acontecer se o UnityVS tentasse anexar o depurador a um Unity cuja interface do depurador tivesse falhado anteriormente.

-   Corrigido um congelamento do Visual Studio que poderia ocorrer quando um ponto de interrupção era definido e um recarregamento do AppDomain ocorreria.

-   Corrigido o modo como assemblies são recuperados do Unity para evitar o bloqueio de arquivos e confundir o processo de build do Unity.

## <a name="1090"></a>1.0.9.0
 Lançado em 3 de outubro de 2012

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a geração de projeto quando o projeto do Unity inclui ativos JavaScript reais.

-   Corrigido tratamento de erro na avaliação da expressão.

-   Corrigida a configuração de novos valores para campos de tipos de valor.

-   Corrigidos possíveis efeitos colaterais ao passar o cursor do mouse sobre expressões do editor de código.

-   Corrigido o modo como os tipos são pesquisados em assemblies carregados para a avaliação da expressão.

-   Corrigido o bug UVS-21: avaliação de atribuição em objetos do Unity não tem efeito.

-   Corrigido o bug UVS-21: ponteiro inválido ao avaliar uma invocação de método para a API de Matemática do Unity.

## <a name="1080"></a>1.0.8.0
 Lançado em 26 de setembro de 2012

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a maneira como o abridor script adquiria o caminho para o projeto para garantir que ele pudesse abrir tanto o Visual Studio quanto os scripts.

-   Corrigido um bug com pontos de interrupção criados enquanto a sessão de depuração estava em execução que poderia fazer o Visual Studio travar.

-   Corrigido como UnityVS é registrado no Visual Studio 2010.

## <a name="1070"></a>1.0.7.0
 Lançado em 14 de setembro de 2012

### <a name="new-features"></a>Novos recursos

-   Suporte ao Visual Studio 2012.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a geração de arquivos de projeto do Editor e Plug-Ins para corresponder ao comportamento do Unity.

-   Corrigida a conversão de símbolos .pdb no Unity 4.

> [!IMPORTANT]
>  Devido ao suporte do Visual Studio 2012, foi necessário renomear alguns arquivos de mover outros. O pacote do UnityVS para importar o Unity agora se chama UnityVS 2010 ou 2012 UnityVS para, respectivamente, o Visual Studio 2010 e o Visual Studio 2012. Essa versão também requer que os arquivos de projeto UnityVS sejam regenerados.

## <a name="1060---internal-build"></a>1.0.6.0 – build interno
 Lançado em 12 de setembro de 2012

## <a name="1050"></a>1.0.5.0
 Lançado em 10 de setembro de 2012

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a geração de arquivos de projeto quando scripts ou sombreadores tinham um caractere xml inválido.

-   Corrigida a detecção de instâncias do Unity quando Unity era conectado ao servidor de Ativo. Isso disparou falhas em abrir arquivos do Unity e na conexão automática do depurador do Visual Studio.

## <a name="1040"></a>1.0.4.0
 Lançado em 5 de setembro de 2012

### <a name="new-features"></a>Novos recursos

-   Conversão automática de símbolos de depuração no Unity.

     Se você tiver um assembly .dll do .NET com seu .pdb associado na pasta Ativo, simplesmente reimporte o assembly e o UnityVS converterá o .pdb para um arquivo de símbolos de depuração que o mecanismo de script do Unity compreende e você poderá intervir em seus assemblies do .NET do UnityVS.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida uma falha do UnityVS durante a depuração causada por exceções geradas por métodos ou propriedades dentro do Unity.

## <a name="1030"></a>1.0.3.0
 Lançado em 4 de setembro de 2012

### <a name="new-features"></a>Novos recursos

-   Nova opção de configuração para desabilitar o uso do UnityVS para abrir arquivos do Unity.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a geração de referências ao UnityEditor para projetos não de editor.

-   Corrigida a definição do símbolo UNITY_EDITOR para projetos não de editor.

-   Corrigida falha aleatória do VS causada pela nossa barra de status personalizada.

## <a name="1020"></a>1.0.2.0
 Lançado em 30 de agosto de 2012

### <a name="bug-fixes"></a>Correções de bug

-   Corrigido conflito com o depurador PythonTools.

-   Corrigidas referências a Mono.Cecil.

-   Corrigido um bug em como assemblies de scripts eram recuperados do Unity com o Unity 4 b7.

## <a name="1010"></a>1.0.1.0
 Lançado em 28 de agosto de 2012

### <a name="new-features"></a>Novos recursos

-   Suporte de visualização para Unity 4.0 Beta.

### <a name="bug-fixes"></a>Correções de bug

-   Corrigida a inspeção de propriedades gerando exceções.

-   Corrigida a ordem decrescente para objetos base ao inspecionar objetos.

-   Corrigida lista suspensa em branco para o ponto de inserção no assistente do MonoBehavior.

-   Corrigida a conclusão para dll dentro da pasta Ativo para UnityScript e Boo.

## <a name="1000---initial-release"></a>1.0.0.0 – versão inicial
 Lançado em 22 de agosto de 2012
