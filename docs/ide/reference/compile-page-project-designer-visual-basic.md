---
title: Página de Compilação, Designer de Projeto (Visual Basic)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesCompile
helpviewer_keywords:
- compilation, Visual Basic projects
- compilation, options [Visual Basic]
- compilers, Visual Basic options
- compilation, instructions [Visual Basic]
- compiler options, Visual Basic
- Project Designer, Compile page
- Compile page in Project Designer
ms.assetid: b2a80230-906e-4e85-b3e0-fcd9c40426e1
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6d1b5c55c3bc1732d0b394473f25c0b103c917f4
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38808368"
---
# <a name="compile-page-project-designer-visual-basic"></a>Página de Compilação, Designer de Projeto (Visual Basic)

Use a página **Compilar** do Designer de Projeto para especificar instruções de compilação. Você também pode especificar opções avançadas do compilador e eventos de pré ou pós-build nessa página.

Para acessar a página **Compilar**, escolha um nó de projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto**, **Propriedades** na barra de menus. Quando o Designer de Projeto for exibido, clique na guia **Compilar**.

[!INCLUDE[note_settings_general](../../data-tools/includes/note_settings_general_md.md)]

## <a name="configuration-and-platform"></a>Configuração e plataforma

As configurações a seguir permitem selecionar a configuração e a plataforma a exibir ou modificar.

> [!NOTE]
> Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. Portanto, as listas **Configuração** e **Plataforma** não são exibidas.

 **Configuração**

 Especifica quais definições de configuração exibir ou modificar. As configurações são **Depurar** (padrão), **Versão** ou **Todas as Configurações**. Para saber mais, consulte [Noções básicas das configurações de build](../../ide/understanding-build-configurations.md) e [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md).

 **Plataforma**

 Especifica quais configurações de plataforma exibir ou modificar. Você pode especificar **Qualquer CPU** (padrão), **x64** ou **x86**.

## <a name="compiler-configuration-options"></a>Opções de configuração do compilador

As configurações a seguir permitem definir as opções de configuração do compilador.

 **Caminho de saída de build**

 Especifica o local dos arquivos de saída para a configuração deste projeto. Digite o caminho da saída de build nesta caixa ou clique no botão **Procurar** para selecionar um caminho. Observe que o caminho é relativo; se você inserir um caminho absoluto, ele será salvo como relativo. O caminho padrão é bin\Debug\ ou bin\Release\\.

 Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. O comando **Build** do menu **Depurar** (F5) colocará o build no local de depuração, independentemente do **Caminho de saída** você especificar. No entanto, o comando **Build** do menu **Build** o coloca no local especificado.
  
 **Opção explícita**  
 Especifica se a declaração implícita de variáveis deve ser permitida. Selecione **Ativar** para exigir a declaração explícita de variáveis. Isso faz o compilador relatar erros se variáveis não forem declaradas antes de serem usadas. Selecione **Desativar** para permitir a declaração implícita de variáveis.  
  
 Essa configuração corresponde à opção do compilador [/optionexplicit](/dotnet/visual-basic/reference/command-line-compiler/optionexplicit).  
  
 Se um arquivo de código-fonte contiver uma [Instrução Explícita de Opção](/dotnet/visual-basic/language-reference/statements/option-explicit-statement), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Explícita** na **página Compilar**.  
  
 Quando você cria um novo projeto, a configuração **Opção Explícita** na **página Compilar** é definida como o valor da configuração **Opção Explícita** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial de **Opção Explícita** em **Padrões de VB** é **Ativada**.  
  
 Configurar **Opção Explícita** como `Off` geralmente não é uma boa prática. Você poderia digitar incorretamente um nome de variável em um ou mais locais, o que levaria a resultados inesperados na execução do programa.  
  
 **Opção estrita**  
Especifica se semântica do tipo estrito deve ser imposta. Quando **Opção Estrita** está **Ativada**, as seguintes condições causam um erro em tempo de compilação:  
  
-   Conversões de estreitamento implícitas  
  
-   Associação tardia  
  
-   Digitação implícita que resulta em um tipo `Object`  
  
Erros de conversão de redução implícita ocorrerem quando há uma conversão de tipo de dados implícita que é uma conversão de redução. Para obter mais informações, consulte [Instrução Opção Estrita](/dotnet/visual-basic/language-reference/statements/option-strict-statement), [Conversões Explícitas e Implícitas](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions) e [Conversões de Expansão e Redução](/dotnet/visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions).  
  
Um objeto tem associação tardia quando é atribuído a uma propriedade ou a um método de uma variável declarada como sendo do tipo `Object`. Para obter mais informações, consulte [Instrução Opção Estrita](/dotnet/visual-basic/language-reference/statements/option-strict-statement) e [Associação Antecipada e Tardia](/dotnet/visual-basic/programming-guide/language-features/early-late-binding).
  
Erros de tipo de objeto implícitos ocorrem quando um tipo apropriado não pode ser inferido de uma variável declarada, portanto, um tipo de `Object` é inferido. Isso ocorre principalmente quando você usa uma instrução `Dim` para declarar uma variável sem usar uma cláusula `As` e `Option Infer` está desativado. Para obter mais informações, consulte [Instrução Opção Explícita](/dotnet/visual-basic/language-reference/statements/option-strict-statement), [Instrução Opção Inferir](/dotnet/visual-basic/language-reference/statements/option-infer-statement) e [Especificação de Linguagem Visual Basic](/dotnet/visual-basic/reference/language-specification).  
  
A configuração **Opção Estrita** corresponde à opção do compilador [/optionstrict](/dotnet/visual-basic/reference/command-line-compiler/optionstrict).  
  
Se um arquivo de código-fonte contiver uma [Instrução Opção Explícita](/dotnet/visual-basic/language-reference/statements/option-strict-statement), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Explícita** na **página Compilar**.  
  
Quando você cria um projeto, a configuração **Opção Estrita** na **página Compilar** é definida como o valor da configuração **Opção Estrita** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial de **Opção Estrita** em **Padrões do VB** é **Desativada**.  
  
**Avisos Individuais da Opção Estrita.** A seção **Configurações de Aviso** da **página Compilar** tem configurações que correspondem às três condições que causam um erro em tempo de compilação quando `Option Strict` está ativado. A seguir estão estas configurações:  
  
-   **Conversão implícita**  
  
-   **Associação tardia; a chamada poderia falhar no tempo de execução**  
  
-   **Tipo implícito; objeto assumido**  
  
Quando você define **Opção Estrita** como **Ativada**, todas estas três definições de configuração de aviso são definidas como **Erro**. Quando você define **Opção Estrita** como **Desativada**, todas as três configurações são definidas como **Nenhum**.  
  
Você pode alterar individualmente cada definição de configuração de aviso como **Nenhum**, **Aviso** ou **Erro**. Se todas as três definições de configuração de aviso estiverem definidas como **Erro**, `On` aparecerá na caixa `Option strict`. Se todas as três estiverem definidas como **Nenhum**, `Off` será exibido nessa caixa. Para qualquer outra combinação dessas configurações, **(personalizado)** será exibido.  
  
**Opção comparar**  
Especifica o tipo de comparação de cadeias de caracteres a usar. Selecione **Binário** para instruir o compilador a usar comparações de cadeias de caracteres binárias com diferenciação de maiúsculas e minúsculas. Selecione **Texto** usar comparações de cadeias de caracteres de texto específicas da localidade sem diferenciação de maiúsculas e minúsculas.  
  
Essa configuração corresponde à opção do compilador [/optioncompare](/dotnet/visual-basic/reference/command-line-compiler/optioncompare).  
  
Se um arquivo de código-fonte contiver uma [Instrução Opção Comparar](/dotnet/visual-basic/language-reference/statements/option-compare-statement), o valor `Binary` ou `Text` na instrução substituirá a configuração **Opção Comparar** na **página Compilar**.  
  
Ao criar um projeto, a configuração **Opção Comparar** na página **Compilar** é definida como o valor da configuração **Opção Comparar** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração inicial padrão de **Opção Comparar** em **Padrões do VB** é **Binário**.  
  
**Opção inferir**  
Especifica se você deve permitir inferência de tipo de variável local nas declarações de variável. Selecione **Ativado** para permitir o uso de inferência de tipo de variável local. Selecione **Desativado** para bloquear a inferência de tipo de variável local.  
  
Essa configuração corresponde à opção do compilador [/optioninfer](/dotnet/visual-basic/reference/command-line-compiler/optioninfer).  
  
Se um arquivo de código-fonte contiver uma [Instrução Opção Inferir](/dotnet/visual-basic/language-reference/statements/option-infer-statement), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Inferir** na **página Compilar**.  
  
Quando você cria um projeto, a configuração **Opção Inferir** na **página Compilar** é definida como o valor da configuração **Opção Inferir** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial da **Opção Inferir** em **Padrões do VB** é **Ativada**.  
  
**CPU de Destino**  
Especifica o processador de destino do arquivo de saída. Especifique **x86** para qualquer processador compatível com Intel de 32 bits, **x64** para qualquer processador compatível com Intel de 64 bits, **ARM** para qualquer processador ARM ou **Qualquer CPU** para especificar que qualquer processador é aceitável. **Qualquer CPU** é o valor padrão para novos projetos, pois permite que o aplicativo seja executado no maior número de tipos de hardware.  
  
Para obter mais informações, consulte [/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform).  
  
**Preferir 32 bits**  
Se a caixa de seleção **Preferir 32 bits** estiver marcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 e 64 bits do Windows. Caso contrário, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits do Windows e como um aplicativo de 64 bits em versões de 64 bits do Windows.  
  
Executar como um aplicativo de 64 bits duplica o tamanho do ponteiro e pode causar problemas de compatibilidade com bibliotecas exclusivamente de 32 bits. Fará sentido executar um aplicativo de 64 bits somente se ele for executado consideravelmente mais rápido ou precisar de mais de 4 GB de memória.  
  
Essa caixa de seleção estará disponível somente se todas as seguintes condições forem verdadeiras:  
  
-   Na **Página Compilar**, a lista **CPU de destino** está definida como **Qualquer CPU**.  
  
-   Na **Página Aplicativo**, a lista **Tipo de aplicativo** especifica que o projeto é um aplicativo.  
  
-   Na **Página Aplicativo**, a lista **Estrutura de destino** especifica o .NET Framework 4.5.  
  
**Configurações de aviso**  
Esta tabela lista condições de build e o nível de notificação correspondente de **Nenhum**, **Aviso** ou **Erro** para cada um.  
  
Por padrão, todos os avisos do compilador são adicionados à Lista de Tarefas durante a compilação. Selecione **Desabilitar todos os avisos** para instruir o compilador a não enviar avisos ou erros. Selecione **Tratar todos os avisos como erros** se você desejar que o compilador trate avisos como erros que devem ser corrigidos.  
  
**Desabilitar todos os avisos**  
Especifica se o compilador deve poder emitir notificações conforme especificado na tabela **Condição e Notificação** descrita anteriormente neste documento. Por padrão, essa caixa de seleção está desmarcada. Marque esta caixa de seleção para instruir o compilador a não emitir avisos ou erros.  
  
Essa configuração corresponde à opção do compilador [/nowarn](/dotnet/visual-basic/reference/command-line-compiler/nowarn).  
  
**Tratar todos os avisos como erros**  
Especifica como tratar avisos. Por padrão, essa caixa de seleção está desmarcada, de modo que todas as notificações de aviso permanecem definidas como **Aviso**. Marque essa caixa de seleção para alterar todas as notificações de aviso para **Erro**.  
  
Essa opção estará disponível somente se **Desabilitar todos os avisos** estiver desmarcada.  
  
**Gerar arquivo de documentação XML**  
Especifica se devem ser geradas informações sobre a documentação. Por padrão, essa caixa de seleção está marcada, instruindo o compilador a gerar informações sobre a documentação e incluí-las em um arquivo XML. Desmarque esta caixa de seleção para instruir o compilador a não criar documentação.  
  
Essa configuração corresponde à opção do compilador [/doc](/dotnet/visual-basic/reference/command-line-compiler/doc).  
  
**Registrar para interoperabilidade COM**  
Especifica se o seu aplicativo gerenciado exibirá um objeto COM (um wrapper que pode ser chamado por COM) que permite a um objeto COM interagir com o aplicativo.  
  
Por padrão, essa caixa de seleção está desmarcada, o que especifica que o aplicativo não permitirá interoperabilidade COM. Marque essa caixa de seleção para permitir a interoperabilidade COM.  
  
Essa opção não está disponível para projetos de Aplicativos do Windows ou Aplicativo de Console.  
  
**Eventos de Build**  
Clique nesse botão para acessar a caixa de diálogo **Eventos de Build**. Use essa caixa de diálogo para especificar as instruções de configuração de pré e de pós-build para o projeto. Essa caixa de diálogo aplica-se a somente projetos Visual Basic. Para obter mais informações, consulte [Caixa de diálogo Eventos de Build(Visual Basic)](../../ide/reference/build-events-dialog-box-visual-basic.md).  
  
**Opções avançadas de compilação**  
Clique neste botão para acessar a caixa de diálogo **Configurações Avançadas do Compilador**. Use a caixa de diálogo **Configurações Avançadas do Compilador** para especificar as propriedades avançadas de configuração de build de um projeto. Essa caixa de diálogo aplica-se a somente projetos Visual Basic. Para obter mais informações, consulte [Caixa de diálogo Configurações Avançadas do Compilador (Visual Basic)](../../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md).  


## <a name="see-also"></a>Consulte também

- [Como especificar eventos de build (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md)
- [Compilador de linha de comando do Visual Basic](/dotnet/visual-basic/reference/command-line-compiler/index)
- [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md)