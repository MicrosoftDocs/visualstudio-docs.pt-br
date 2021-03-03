---
title: Log de alterações (Ferramentas do Visual Studio para Unity, Mac) | Microsoft Docs
description: Exiba o log de alterações para Ferramentas do Visual Studio para Unity, Mac. Confira as alterações da versão 1.0.0.0 a 2.7.0.0 e posteriores.
ms.custom: ''
ms.date: 3/1/2021
ms.technology: vs-unity-tools
ms.prod: visual-studio-dev16
ms.topic: conceptual
ms.assetid: 33a6ac54-d997-4308-b5a0-af7387460849
author: therealjohn
ms.author: johmil
manager: crdun
ms.workload:
- unity
ms.openlocfilehash: f11c5c1407d16d7a82a9d8d24e6a8dd3a04e57eb
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683381"
---
# <a name="change-log-visual-studio-tools-for-unity-mac"></a>Log de alterações (Ferramentas do Visual Studio para Unity, Mac)

Log de alterações de Ferramentas do Visual Studio para Unity.

## <a name="2920"></a>2.9.2.0
Lançado em 2 de março de 2021

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigido o realce de pesquisa na caixa de diálogo de mensagem do Unity.

  - Correção de problemas de estabilidade com o projeto de Unity TreeView.

- **Pura**

  - Manipulação fixa de pontos de interrupção condicionais.

## <a name="2910"></a>2.9.1.0
Lançado em 9 de fevereiro de 2021

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para executar e depurar testes do Unity do IDE

- **Período**

  - Adicionado `Active Scene` a locais, mostrando objetos de jogo raiz.

  - Adicionado `this.gameObject` aos locais, Considerando que ele é amplamente usado em projetos do Unity.

  - Adicionados `Children` e `Components` grupos a todas as `GameObject` instâncias, para que você possa exibir facilmente toda a hierarquia de objetos.

  - Adicionado `Scene Path` a todas as `GameObject` instâncias, para mostrar o local na cena.

  - Adicionado suporte para `JobEntityBatch` /lambdas ao usar entidades com geradores de origem.

  - Suporte aprimorado para a exibição de matrizes grandes (usando o Bucket de índice).

  - Foram adicionadas mensagens de Unity ausentes para a API 2019,4.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção de problemas de estabilidade com a caixa de diálogo de mensagem do Unity

  - Correção de vários problemas de interface do usuário para idiomas que não são de PTB.

  - Correção de problemas de estabilidade com o [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md) diagnóstico.

- **Pura**

  - Correção dos problemas de desconexão de VM ao usar `Trace` métodos.

- **Período**

  - Filtragem fixa de propriedades obsoletas lançando exceções.

## <a name="2900"></a>2.9.0.0
Lançado em 20 de janeiro de 2021

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Suporte adicionado para `raytrace shaders` `UXML` arquivos e `USS` .

  - API de mensagens do Unity atualizada (para todos os métodos usados como corrotinas).

  - Detecção de SDK do Android atualizada.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - O [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) diagnóstico foi corrigido, fornecendo avisos incorretos para corrotinas e `AssetPostprocessor.OnAssignMaterialModel` .

## <a name="2840"></a>2.8.4.0
Lançado em 15 de dezembro de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigido um problema de confiabilidade ao fechar o assistente de criação de eventos do Unity.

## <a name="2830"></a>2.8.3.0
Lançado em 10 de novembro de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção da anexação ao Unity, mesmo que não haja nenhum projeto VSTU na solução.

## <a name="2820"></a>2.8.2.0
Lançado em 27 de outubro de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Diagnóstico aprimorado [`UNT0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0010.md) para aplicar a tudo que herda de `Component` , não apenas `MonoBehaviour` .

## <a name="2810"></a>2.8.1.0
Lançado em 13 de outubro de 2020

### <a name="new-features"></a>Novos recursos

- **Período**

  - Suporte adicionado para conversão implícita com invocações. Anteriormente, o avaliador impôs a verificação de tipo estrito, resultando em `Failed to find a match for method([parameters...])` mensagens de aviso.

- **Integrar**

  - [`UNT0018`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0018.md)Diagnóstico adicionado. Você não deve usar `System.Reflection` recursos em mensagens críticas de desempenho como `Update` , `FixedUpdate` , `LateUpdate` ou `OnGUI` .

  - Melhoria [`USP0003`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0003.md) e [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) supressers, com suporte para todos os `AssetPostprocessor` métodos estáticos.

  - Adicionado o [`USP0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0016.md) supressor para `CS8618` . `C# 8.0` apresenta tipos de referência anuláveis e tipos de referência não anuláveis. A detecção de inicialização de tipos herdados de `UnityEngine.Object` não tem suporte e resultará em erros.

  - Agora, usando o mesmo mecanismo de geração de projeto asmdef e de Player para o Unity 2019. x e 2020. x +.
  
  - Experiência do usuário aprimorada ao gerar mensagens do Unity com um assistente.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção de conclusão inesperada de mensagens em comentários.

## <a name="2800"></a>2.8.0.0 
Lançado em 14 de setembro de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Geração fixa de projeto de Player com Unity 2019. x.

## <a name="2710"></a>2.7.1.0
Lançado em 5 de agosto de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - API de mensagens do Unity atualizada para 2019,4.

  - Adicionado o [`USP0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0013.md) supressor para `CA1823` . Campos particulares com os `SerializeField` `SerializeReference` atributos ou não devem ser marcados como não utilizados (FxCop).
  
  - Adicionado o [`USP0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0014.md) supressor para `CA1822` . As mensagens do Unity não devem ser sinalizadas como candidatos para o `static` modificador (FxCop).

  - Adicionado o [`USP0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0015.md) supressor para `CA1801` . Os parâmetros não utilizados não devem ser removidos das mensagens do Unity (FxCop).
  
  - `MenuItem`Suporte adicionado ao [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) supressor.  

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Fixos [`USP0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0001.md) e [`USP0002`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0002.md) supressers que não funcionam com parênteses extras ou com argumentos de método.
  
  - Atualização de banco de dados de ativo obrigatório fixa, mesmo quando a atualização automática foi desabilitada nas configurações do Unity.

## <a name="2700"></a>2.7.0.0
Lançado em 23 de junho de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Suporte adicionado para manter as pastas da solução quando o Unity está regenerando a solução e os projetos.

  - [`UNT0015`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0015.md)Diagnóstico adicionado. Detectar assinatura de método incorreta com o `InitializeOnLoadMethod` `RuntimeInitializeOnLoadMethod` atributo ou.

  - [`UNT0016`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0016.md)Diagnóstico adicionado. Usar `Invoke` , `InvokeRepeating` `StartCoroutine` ou `StopCoroutine` com um primeiro argumento sendo um literal de cadeia de caracteres não é de tipo seguro.

  - [`UNT0017`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0017.md)Diagnóstico adicionado. `SetPixels` a invocação está lenta.

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção da criação de pontos de interrupção enquanto o jogo está em execução no tempo de execução mono antigo (tentando associar o ponto de interrupção assim que ele é criado). 
  
- **Integrar**

  - Não redefina a seleção ao filtrar mensagens no assistente de mensagem do Unity.
  
  - Corrigidos [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md) [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) e [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) supressers com as seguintes regras: suprimir `IDE0044` (ReadOnly), `IDE0051` (não usado), `CS0649` (nunca atribuído) para todos os campos decorados com o atributo serializefield. Suprimir `CS0649` (nunca atribuído) para campos públicos de todos os tipos estendendo `Unity.Object`.

  - Correção de parâmetro de tipo genérico corrigido para [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md) .

- **Período**

  - Correção da comparação de igualdade com enums.

## <a name="2610"></a>2.6.1.0
Lançado em 19 de maio de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Avise se não for possível criar o servidor de mensagens no lado do Unity.

  - Execute analisadores corretamente durante a compilação leve.

  - Documentação da API corrigida com instalações do Hub do Unity.
  
  - Correção de falhas do Visualizador do depurador.

## <a name="2600"></a>2.6.0.0
Lançado em 14 de abril de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - [`UNT0012`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0012.md)Diagnóstico adicionado. Detectar e encapsular chamadas para corrotinas no `StartCoroutine()` .

  - [`UNT0013`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0013.md)Diagnóstico adicionado. Detectar e remover atributo inválido ou redundante `SerializeField` .

  - [`UNT0014`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0014.md)Diagnóstico adicionado. Detecção `GetComponent()` chamada com tipo não componente ou não de interface.

  - Adicionado o [`USP0009`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0009.md) supressor para `IDE0051` . Não sinalize os métodos com o `ContextMenu` atributo ou referenciado por um campo com o `ContextMenuItem` atributo como não utilizado.

  - Adicionado o [`USP0010`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0010.md) supressor para `IDE0051` . Não sinalize campos com o `ContextMenuItem` atributo como não usado.

  - Adicionado o [`USP0011`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0011.md) supressor para `IDE0044` . Não crie campos com o `ContextMenuItem` atributo somente leitura.

  - [`USP0004`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0004.md)[`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md)e [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) agora estão trabalhando para ambos os `SerializeReference` `SerializeField` atributos e.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Somente envie comandos start/stop para o Unity quando o editor for capaz de se comunicar.

  - Correção da documentação do QuickInfo com mensagens herdadas.

  - Escopo de mensagem fixo para a `CreateInspectorGUI` mensagem.

  - Não relate [`UNT0001`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0001.md) métodos com modificadores polimórficos.

- **Período**

  - Manipulação fixa de uso de alias.
  
  - Manipulação fixa de valores nulos.  

## <a name="2520"></a>2.5.2.0

Lançado em 23 de março de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Registro fixo de threads ao anexar.

## <a name="2510"></a>2.5.1.0

Lançado em 3 de março de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado o [`USP0008`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0008.md) supressor para `IDE0051` . Os métodos privados usados com Invoke, InvokeRepeating, StartCoroutine ou StopCoroutine não devem ser marcados como não utilizados.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção da documentação do OnDrawGizmos/OnDrawGizmosSelected.

- **Período**

  - Inspeção de argumento lambda fixo.

## <a name="2501"></a>2.5.0.1

Lançado em 19 de fevereiro de 2020

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção [`UNT0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/UNT0006.md) da verificação de diagnóstico para assinatura de mensagem incorreta. Ao inspecionar tipos com vários níveis de herança, esse diagnóstico pode falhar com a seguinte mensagem: `warning AD0001: Analyzer 'Microsoft.Unity.Analyzers.MessageSignatureAnalyzer' threw an exception of type 'System.ArgumentException' with message 'An item with the same key has already been added` .

## <a name="2500"></a>2.5.0.0

Lançado em 22 de janeiro de 2020

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para arquivos HLSL.
  
  - Foi alternado para uma interface do usuário da caixa de diálogo Nova pasta.
  
  - Alternado para uma nova grade de propriedades acessível para configurações.

  - Adicionado o [`USP0006`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0006.md) supressor para `IDE0051` . Campos privados com o `SerializeField` atributo não devem ser marcados como não utilizados.

  - Adicionado o [`USP0007`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0007.md) supressor para `CS0649` . Os campos com o `SerializeField` atributo não devem ser marcados como não atribuídos.  

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Geração de projeto fixa (o `GenerateTargetFrameworkMonikerAttribute` destino nem sempre foi localizado corretamente).

- **Período**

  - Avaliação de cadeia de caracteres fixa (não usando chamadas ToString ())

## <a name="2420"></a>2.4.2.0

Lançado em 3 de dezembro de 2019

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigido o diagnóstico com interfaces definidas pelo usuário.

  - Correção de dicas de ferramenta rápidas com expressões malformadas.
  
## <a name="2410"></a>2.4.1.0

Lançado em 6 de novembro de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Suporte adicionado para processos em segundo plano do Unity. (O depurador é capaz de se conectar automaticamente ao processo principal em vez de um processo filho).

  - Adicionada uma dica de ferramenta rápida para mensagens do Unity, exibindo a documentação associada.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção do analisador de comparação de marcas `UNT0002` com expressões binárias e de invocação avançadas.

### <a name="deprecated-features"></a>Recursos preteridos

- **Integrar**

  - No futuro, Ferramentas do Visual Studio para Unity dará suporte apenas ao Visual Studio 2017 +.

## <a name="2400"></a>2.4.0.0

Lançado em 15 de outubro de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado o [`USP0005`](https://github.com/microsoft/Microsoft.Unity.Analyzers/blob/main/doc/USP0005.md) supressor para `IDE0060` (parâmetro não usado) para todas as mensagens do Unity.

  - Adicionada uma dica de ferramenta rápida para campos marcados com `TooltipAttribute` . (Isso também funcionará para um acessador get simples usando esse campo).

## <a name="2330"></a>2.3.3.0

Lançado em 23 de setembro de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Foi adicionado um novo supressor para IDE0060, para impedir que o IDE mostre uma correção rápida para remover parâmetros não utilizados.
    - `USP0005` para `IDE0060` : as mensagens do Unity são invocadas pelo tempo de execução do Unity.

## <a name="2320"></a>2.3.2.0

Lançado em 16 de setembro de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Nós aprofundamos a compreensão de que o Visual Studio tem para projetos do Unity adicionando novos diagnósticos específicos ao Unity. Também tornamos o IDE mais inteligente, suprimindo diagnósticos C# gerais que não se aplicam a projetos do Unity. Por exemplo, o IDE não mostrará uma correção rápida para alterar uma variável de inspetor para a `readonly` qual impediria que você modificasse a variável no editor do Unity.
    - `UNT0001`: As mensagens do Unity são chamadas pelo tempo de execução mesmo se estiverem vazias, não as declare para evitar o processamento de uncesseray pelo tempo de execução do Unity.
    - `UNT0002`: A comparação de marcas usando a igualdade de cadeia de caracteres é mais lenta do que o método CompareTag interno.
    - `UNT0003`: O uso da forma genérica de GetComponent é preferencial para a segurança de tipo.
    - `UNT0004`: A mensagem de atualização é dependente de taxa de quadros e deve usar time. deltaTime em vez de time. fixedDeltaTime.
    - `UNT0005`: A mensagem FixedUpdate é independente de taxa de quadros e deve usar time. fixedDeltaTime em vez de time. deltaTime.
    - `UNT0006`: Uma assinatura de método incorreta foi detectada para esta mensagem do Unity.
    - `UNT0007`: Unity substitui o operador de comparação nulo para objetos do Unity que é incompatível com a União nula.
    - `UNT0008`: Unity substitui o operador de comparação nulo para objetos do Unity que é incompatível com a propagação nula.
    - `UNT0009`: Ao aplicar o atributo InitializeOnLoad a uma classe, você precisa fornecer um construtor estático. O atributo InitializeOnLoad verifica se ele será chamado quando o editor for iniciado.
    - `UNT0010`: Monocomportamentos só devem ser criados usando addComponent (). O MonoBehaviour é um componente e precisa ser anexado a um GameObject.
    - `UNT0011`: ScriptableObject só deve ser criado usando CreateInstance (). ScriptableObject precisa ser criado pelo mecanismo do Unity para manipular métodos de mensagem do Unity.
    - `USP0001` para `IDE0029` : objetos Unity não devem usar União nula.
    - `USP0002` para `IDE0031` : objetos Unity não devem usar a propagação nula.
    - `USP0003` para `IDE0051` : as mensagens do Unity são invocadas pelo tempo de execução do Unity.
    - `USP0004` para `IDE0044` : campos com um atributo serializefield não devem ser criados somente leitura.

## <a name="2310"></a>2.3.1.0

Lançado em 4 de setembro de 2019

### <a name="new-features"></a>Novos recursos

- **Período**

  - Adição de suporte para melhor exibição de tipo, ou seja, `List<object>` em vez de `List'1[[System.Object, <corlib...>]]` .

  - Suporte adicionado para acesso de membro de ponteiro, ou seja, `p->data->member` .

  - Suporte adicionado para conversões implícitas em inicializadores de matriz, ou seja, `new byte [] {1,2,3,4}` .

  - Suporte adicionado para o editor hexadecimal ao inspecionar matrizes de bytes e cadeias de caracteres.

## <a name="2300"></a>2.3.0.0

Lançado em 13 de agosto de 2019

### <a name="bug-fixes"></a>Correções de bug

- **Período**

  - Correção de problemas de depuração com exceções.

  - Correção da avaliação de pseudo identificadores (como $exception).

  - Impedir falha ao desreferenciar endereços inválidos.  

  - Corrigido o problema com AppDomains descarregados.

## <a name="2200"></a>2.2.0.0

Lançado em 25 de julho de 2019

### <a name="bug-fixes"></a>Correções de bug

- **Período**

  - corrigida a inspeção com tipos IntPtr.

- **Depurador**

  - corrigida a manipulação de catchpoints e pontos de interrupção de função.

## <a name="2130"></a>2.1.3.0

Lançado em 9 de julho de 2019

### <a name="new-features"></a>Novos recursos

- **Depurador**

  - adicionado suporte para captura de subclasses de exceções;

  - adicionado suporte a protocolo MDS 2.51.

- **Integrar**

  - adicionado suporte para arquivos asmdef.

  - Mude para o modo de renomeação quando um arquivo for adicionado de um modelo (para imitar o comportamento do Editor do Unity).

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - corrigida a manipulação de mensagens malformadas durante a comunicação com players do Unity.

- **Período**

  - corrigida a manipulação de namespaces em expressões.

## <a name="2120"></a>2.1.2.0

Lançado em 2 de julho de 2019

### <a name="bug-fixes"></a>Correções de bug

- **Período**

  - corrigido o relatório de erros com expressões não analisáveis.

## <a name="2110"></a>2.1.1.0

Lançado em 27 de junho de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Atualização da API MonoBehaviour para 2019.1.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - corrigido o desempenho do Gerenciador de Projetos do Unity.

  - Correção de emissão de relatórios de erros e avisos para a saída quando a compilação leve está habilitada.

  - Desempenho de construção leve e fixo.

## <a name="2100"></a>2.1.0.0

Lançado em 20 de junho de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Desabilitada a compilação completa para projetos Unity, em favor de usar os erros e avisos do IntelliSense. Na verdade, o Unity cria uma solução do Visual Studio com projetos de biblioteca de classes que representam o que o Unity está fazendo internamente. Dito isso, o resultado da compilação no Visual Studio nunca é usado ou selecionado pelo Unity quando seu pipeline de compilação é fechado. A criação no Visual Studio está apenas consumindo recursos para nada. Se você precisar de um build completo por ter ferramentas ou uma configuração que dependa disso, poderá desabilitar essa otimização (Configurações/Ferramentas para Unity/Desabilitar o build completo de projetos).
  
  - Adicionado suporte para pacotes Unity no UPE. Somente pacotes referenciados (usando manifest.json na pasta `Packages`) e pacotes locais (incorporados na pasta `Packages`) são visíveis.

## <a name="2021"></a>2.0.2.1

Lançamento em 30 de maio de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Ícone personalizado adicionado para destinos de execução do Unity.

## <a name="2020"></a>2.0.2.0

Lançado em 2 de abril de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para atualizar automaticamente o banco de dados de ativos do Unity ao salvar. Isso é habilitado por padrão e acionará uma recompilação no lado Unity ao salvar um script no Visual Studio. Você pode desativar esse recurso em Ferramentas\Opções\Ferramentas para Unity\Atualizar AssetDatabase do Unity ao salvar.

  - Adicionado suporte para a configuração de instalação preferencial do Unity para obter a documentação offline.

  - Adicionado menu de contexto para o novo editor.

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção de filtragem de montagem e inspeção de estrutura com quadros vazios.

## <a name="2011"></a>2.0.1.1
 
 Lançado em 26 de março de 2019

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Tornar temporariamente o Mono o depurador utilizável padrão e único para este lançamento muito específico.

## <a name="2006"></a>2.0.0.6

Lançado em 26 de março de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para "Anexar ao Unity e Reproduzir".

## <a name="2005"></a>2.0.0.5

Lançado em 20 de março de 2019

### <a name="new-features"></a>Novos recursos

- **Geração de projeto:**

  - Preservar propriedades externas ao processar o arquivo da solução.
  
- **Período**

  - Adicionado suporte para nomes qualificados por alias (somente o namespace global por enquanto). Portanto, o avaliador de expressão agora aceita tipos usando o formato global::namespace.type.

  - Adicionado suporte para o formulário `pointer[index]`, que é semanticamente idêntico ao formulário de desreferenciamento de ponteiro `*(pointer+index)`.

## <a name="2004"></a>2.0.0.4

Lançado em 5 de março de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - A API foi atualizada `ScriptableObject` .

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Removidos namespaces de modelos.

## <a name="2003"></a>2.0.0.3
 
 Lançado em 5 de março de 2019

### <a name="new-features"></a>Novos recursos

- **Geração de projeto:**

  - Campos públicos e serializados não irão mais gerar avisos. Suprimemos automaticamente os avisos de `CS0649` `IDE0051` compilador e em projetos do Unity que criaram essas mensagens.

- **Integrar**

  - Avisar para anexar a uma instância específica se mais de um processo do Unity estiver em execução.

- **Período**

  - Adicionado suporte para funções locais.

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção de atributo personalizado de leitura em argumentos nomeados ao usar versões de protocolo antigas.

## <a name="2002"></a>2.0.0.2

Lançado em 4 de fevereiro de 2019

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Atualização da API MonoBehaviour.

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção de valores primitivos de configuração no depurador.

## <a name="2001"></a>2.0.0.1

Lançado em 4 de dezembro de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção de pacote de instalação autossuficiente.

## <a name="2000"></a>2.0.0.0
 Lançado em 4 de dezembro de 2018

### <a name="new-features"></a>Novos recursos

- **Depurador**

  - Substituição do depurador do Unity no Mac pelo mesmo principal depurador Unity do Windows.

  - Substituição do NRefactory em favor do Roslyn para avaliação de expressão.

  - Adicionado suporte para ponteiros: desreferenciamento, conversão e aritmética de ponteiro (tanto o Unity 2018.2+ quanto o novo runtime são necessários para isso).

  - Adicionado suporte para o modo de exibição de ponteiro de matriz (como no C++). Selecione uma expressão de ponteiro e acrescente uma vírgula e o número de elementos que você deseja ver.

  - Adicionado suporte para construções assíncronas.

  - Adicionado suporte para as pseudovariáveis (identificadores de objeto e de exceção).

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Correção de avaliação de expressão com expressões malformadas ou sem suporte.

## <a name="1700"></a>1.7.0.0

Lançado em 13 de novembro de 2018

### <a name="new-features"></a>Novos recursos

- **Depurador**

  - Adição de outras informações de cliente (IP, nome do computador) à caixa de diálogo Anexar.

### <a name="bug-fixes"></a>Correções de bug

- **Depurador**

  - Corrigido um deadlock na biblioteca usada para se comunicar com o mecanismo de depuração do Unity, causando o congelamento do Visual Studio ou Unity, especialmente ao pressionar "Anexar ao Unity" ou ao reiniciar o jogo.

- **Integrar**

  - Correção da ativação de plug-in do Unity quando outro editor padrão é selecionado.

  - Correção da criação do modelo de arquivo do Unity.

## <a name="1602"></a>1.6.0.2

Lançado em 24 de julho de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Foi revertida a solução alternativa para um bug de desempenho do Unity que foi corrigido pelo Unity.

## <a name="1601"></a>1.6.0.1

Lançado em 10 de julho de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Suporte à coloração de código de Sombreador corrigido.

## <a name="1600"></a>1.6.0.0

Lançado em 26 de junho de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Assistentes**

  - Erro de digitação corrigido com a mensagem OnApplicationFocus.

- **Geração de projeto:**

  - Solução alternativa temporária para um bug de desempenho do Unity: armazenar em cache MonoIslands ao gerar projetos.

  - Não converta mais um pdb portátil para mdb ao usar o novo runtime do Unity.

## <a name="1502"></a>1.5.0.2

Lançado em 18 de abril de 2018

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para a conclusão de código básico do Sombreador.

  - Adicionado suporte para ativar/desativar comentários em arquivos do Sombreador.

## <a name="1501"></a>1.5.0.1

Lançado em 28 de março de 2018

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para modelos adicionais no Explorador de Projeto do Unity.

## <a name="1500"></a>1.5.0.0

Lançado em 21 de março de 2018

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para detectar e anexar a players Android conectados por USB.

## <a name="1403"></a>1.4.0.3

Lançado em 5 de março de 2018

### <a name="new-features"></a>Novos recursos

- **Geração de projeto:**

  - Adicionado o suporte para o gerador de projeto novo no Unity 2018.1.

- **Integrar**

  - Adicionado painel de opções para configurações dedicadas.

## <a name="1402"></a>1.4.0.2

Lançado em 24 de janeiro de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Geração de projeto:**

  - Correção da detecção de versão Mono.

- **Integrar**

  - Correção dos problemas de timing com 2018.1 e ativação de plug-in.

  - Corrigidas as notificações ao detectar um novo player.

## <a name="1401"></a>1.4.0.1

Lançado em 23 de janeiro de 2018

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigida a funcionalidade de Expandir/Recolher pastas ao clicar duas vezes

## <a name="1400"></a>1.4.0.0

Lançado em 13 de dezembro de 2017

### <a name="new-features"></a>Novos recursos

- **Geração de projeto:**

  - Suporte adicionado para o .NET Standard.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção de pdb automático para conversão de símbolo de depuração de mdb.

## <a name="1301"></a>1.3.0.1

Lançado em 12 de dezembro de 2017

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Correção de chamada indireta para EditorPrefs.GetBool afetando o inspetor ao tentar alterar o tamanho da matriz.

- **Assistentes**

  - Atualize o contexto do roslyn antes de inserir o método.

## <a name="1300"></a>1.3.0.0

Lançado em 20 de novembro de 2017

### <a name="new-features"></a>Novos recursos

- **Assistentes**

  - Adicionado o assistente "Implementar mensagem do Unity".

  - Adicionado suporte para nova API de conclusão no VS para Mac 7.4.

## <a name="1200"></a>1.2.0.0

Lançado em 23 de outubro de 2017

### <a name="new-features"></a>Novos recursos

- **Depurador**

  - Suporte adicionado para arquivos de símbolo de depuração portátil.

### <a name="bug-fixes"></a>Correções de bug

- **Geração de projeto:**

  - Correção da extensão .dll extra adicionada por engano ao arquivo do assembly.

  - Não force o sinalizador AllowAttachedDebuggingOfEditor do Unity, uma vez que o padrão agora é ‘true’.

## <a name="1103"></a>1.1.0.3

Lançado em 23 de outubro de 2017

### <a name="new-features"></a>Novos recursos

- **Geração de projeto:**

  - Suporte adicionado para o perfil do .NET 4.6.

## <a name="1102"></a>1.1.0.2

Lançado em 8 de agosto de 2017

### <a name="new-features"></a>Novos recursos

- **Depurador**

  - Iniciar a caixa de diálogo Anexar ao processo se não souber a qual Unity anexar.

- **Geração de projeto:**

  - Sempre habilite a opção de compilação não segura quando o Unity 5.6 for usado.

## <a name="1101"></a>1.1.0.1

Lançado em 20 de julho de 2017

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para recursos localizados.

## <a name="1100"></a>1.1.0.0

Lançado em 12 de julho de 2017

### <a name="new-features"></a>Novos recursos

- **Integrar**

  - Adicionado suporte para anexar a players e editores por meio da janela Anexar ao processo.

- **Geração de projeto:**

  - Corrigidas referências de nome de assembly com arquivos mcs.rsp.

  - Adicionado suporte para unidades de compilação assembly.json.

  - Corrigidas definições com níveis de API.

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigida mensagem de erro do sombreador ao compilar.

## <a name="1001"></a>1.0.0.1

Lançado em 4 de maio de 2017

### <a name="bug-fixes"></a>Correções de bug

- **Integrar**

  - Corrigido acompanhamento de documento ativo com projetos regulares e híbridos.

## <a name="1000"></a>1.0.0.0

Lançado em 3 de maio de 2017
