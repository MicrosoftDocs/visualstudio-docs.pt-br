---
title: Página Compilar, Designer de Projeto (Visual Basic) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
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
caps.latest.revision: 65
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: db830e04388b7465c941e2fdf069b49f98951a1f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660833"
---
# <a name="compile-page-project-designer-visual-basic"></a>Página de Compilação, Designer de Projeto (Visual Basic)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Use a página **Compilar** do Designer de Projeto para especificar instruções de compilação. Você também pode especificar opções avançadas do compilador e eventos de pré ou pós-build nessa página.

 Para acessar a página **Compilar**, escolha um nó de projeto (não o nó **Solução**) no **Gerenciador de Soluções**. Em seguida, escolha **Projeto**, **Propriedades** na barra de menus. Quando o Designer de Projeto for exibido, clique na guia **Compilar**.

 [!INCLUDE[note_settings_general](../../includes/note-settings-general-md.md)]

## <a name="configuration-and-platform"></a>Configuração e plataforma
 As configurações a seguir permitem selecionar a configuração e a plataforma a exibir ou modificar.

> [!NOTE]
> Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. Portanto, as listas **Configuração** e **Plataforma** não são exibidas. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e).

 **Configuração** Especifica quais definições de configuração devem ser exibidas ou modificadas. As configurações são **Depurar** (padrão), **Versão** ou **Todas as Configurações**. Para obter mais informações, consulte [Configurações de depuração e versão do projeto](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e) e [Como criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md).

 **Plataforma** Especifica quais configurações de plataforma devem ser exibidas ou modificadas. Você pode especificar **Qualquer CPU** (padrão), **x64** ou **x86**. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e).

## <a name="compiler-configuration-options"></a>Opções de configuração do compilador
 As configurações a seguir permitem definir as opções de configuração do compilador.

 **Caminho de saída da compilação** Especifica o local dos arquivos de saída para a configuração deste projeto. Digite o caminho da saída de build nesta caixa ou clique no botão **Procurar** para selecionar um caminho. Observe que o caminho é relativo; se você inserir um caminho absoluto, ele será salvo como relativo. O caminho padrão é bin\Debug\ ou bin\Release\\. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e).

 Com configurações de build simplificadas, o sistema do projeto determina se é necessário compilar uma versão de depuração ou de liberação. O comando **Build** do menu **Depurar** (F5) colocará o build no local de depuração, independentemente do **Caminho de saída** você especificar. No entanto, o comando **Build** do menu **Build** o coloca no local especificado. Para obter mais informações, consulte [Configurações de projeto de depuração e versão](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e).

 **Opção explicit** Especifica se deve ser permitida a declaração implícita de variáveis. Selecione **Ativar** para exigir a declaração explícita de variáveis. Isso faz o compilador relatar erros se variáveis não forem declaradas antes de serem usadas. Selecione **Desativar** para permitir a declaração implícita de variáveis.

 Essa configuração corresponde à opção do compilador [/optionexplicit](https://msdn.microsoft.com/library/5d296ab3-bafe-4c4d-9887-78f162ed86c7).

 Se um arquivo de código-fonte contiver uma [Instrução Explícita de Opção](https://msdn.microsoft.com/library/e82ac1ad-2cd3-49b2-b985-8bcf016f3fcc), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Explícita** na **página Compilar**.

 Quando você cria um novo projeto, a configuração **Opção Explícita** na **página Compilar** é definida como o valor da configuração **Opção Explícita** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial de **Opção Explícita** em **Padrões de VB** é **Ativada**.

 Configurar **Opção Explícita** como `Off` geralmente não é uma boa prática. Você poderia digitar incorretamente um nome de variável em um ou mais locais, o que levaria a resultados inesperados na execução do programa.

 **Opção strict** Especifica se deve ser imposta a semântica de tipo estrito. Quando **Opção Estrita** está **Ativada**, as seguintes condições causam um erro em tempo de compilação:

- Conversões de estreitamento implícitas

- Associação tardia

- Digitação implícita que resulta em um tipo `Object`

  Erros de conversão de redução implícita ocorrerem quando há uma conversão de tipo de dados implícita que é uma conversão de redução. Para obter mais informações, consulte [Instrução Opção Estrita](https://msdn.microsoft.com/library/5883e0c1-a920-4274-8e46-b0ff047eaee5), [Conversões Explícitas e Implícitas](https://msdn.microsoft.com/library/77de1659-af8a-492c-967e-e7ef60ccce66) e [Conversões de Expansão e Redução](https://msdn.microsoft.com/library/058c3152-6c28-4268-af44-2209e774f0bd).

  Um objeto tem associação tardia quando é atribuído a uma propriedade ou a um método de uma variável declarada como sendo do tipo `Object`. Para obter mais informações, consulte [Instrução Opção Estrita](https://msdn.microsoft.com/library/5883e0c1-a920-4274-8e46-b0ff047eaee5) e [Associação Antecipada e Tardia](https://msdn.microsoft.com/library/d6ff7f1e-b94f-4205-ab8d-5cfa91758724).

  Erros de tipo de objeto implícitos ocorrem quando um tipo apropriado não pode ser inferido de uma variável declarada, portanto, um tipo de `Object` é inferido. Isso ocorre principalmente quando você usa uma instrução `Dim` para declarar uma variável sem usar uma cláusula `As` e `Option Infer` está desativado. Para obter mais informações, consulte [Instrução Opção Explícita](https://msdn.microsoft.com/library/5883e0c1-a920-4274-8e46-b0ff047eaee5), [Instrução Opção Inferir](https://msdn.microsoft.com/library/4ad3e6e9-8f5b-4209-a248-de22ef6e4652) e [Especificação de Linguagem Visual Basic](https://msdn.microsoft.com/library/42c30017-19d0-442e-87a2-850b66ddc3df).

  A configuração **Opção Estrita** corresponde à opção do compilador [/optionstrict](https://msdn.microsoft.com/library/c7b10086-0fa4-49db-b3c8-4ae0db5957da).

  Se um arquivo de código-fonte contiver uma [Instrução Opção Explícita](https://msdn.microsoft.com/library/5883e0c1-a920-4274-8e46-b0ff047eaee5), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Explícita** na **página Compilar**.

  Quando você cria um projeto, a configuração **Opção Estrita** na **página Compilar** é definida como o valor da configuração **Opção Estrita** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial de **Opção Estrita** em **Padrões do VB** é **Desativada**.

  **Avisos Individuais da Opção Estrita.** A seção **Configurações de Aviso** da **página Compilar** tem configurações que correspondem às três condições que causam um erro em tempo de compilação quando `Option Strict` está ativado. A seguir estão estas configurações:

- **Conversão implícita**

- **Associação tardia; a chamada poderia falhar no tempo de execução**

- **Tipo implícito; objeto assumido**

  Quando você define **Opção Estrita** como **Ativada**, todas estas três definições de configuração de aviso são definidas como **Erro**. Quando você define **Opção Estrita** como **Desativada**, todas as três configurações são definidas como **Nenhum**.

  Você pode alterar individualmente cada definição de configuração de aviso como **Nenhum**, **Aviso** ou **Erro**. Se todas as três definições de configuração de aviso estiverem definidas como **Erro**, `On` aparecerá na caixa `Option strict`. Se todas as três estiverem definidas como **Nenhum**, `Off` será exibido nessa caixa. Para qualquer outra combinação dessas configurações, **(personalizado)** será exibido.

  **Opção compare** Especifica o tipo de comparação de cadeia de caracteres a ser usada. Selecione **Binário** para instruir o compilador a usar comparações de cadeias de caracteres binárias com diferenciação de maiúsculas e minúsculas. Selecione **Texto** usar comparações de cadeias de caracteres de texto específicas da localidade sem diferenciação de maiúsculas e minúsculas.

  Essa configuração corresponde à opção do compilador [/optioncompare](https://msdn.microsoft.com/library/7237b766-b44d-4cc5-9a3c-885348a7d9e4).

  Se um arquivo de código-fonte contiver uma [Instrução Opção Comparar](https://msdn.microsoft.com/library/54e8eeeb-3b0d-4fb9-acce-fbfbd5975f6e), o valor `Binary` ou `Text` na instrução substituirá a configuração **Opção Comparar** na **página Compilar**.

  Ao criar um projeto, a configuração **Opção Comparar** na página **Compilar** é definida como o valor da configuração **Opção Comparar** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração inicial padrão de **Opção Comparar** em **Padrões do VB** é **Binário**.

  **Opção infer** Especifica se deve ser permitida a inferência de tipo de variável local nas declarações de variável. Selecione **Ativado** para permitir o uso de inferência de tipo de variável local. Selecione **Desativado** para bloquear a inferência de tipo de variável local.

  Essa configuração corresponde à opção do compilador [/optioninfer](https://msdn.microsoft.com/library/f6c09db1-0553-464a-abe3-d4510c61d6ed).

  Se um arquivo de código-fonte contiver uma [Instrução Opção Inferir](https://msdn.microsoft.com/library/4ad3e6e9-8f5b-4209-a248-de22ef6e4652), o valor `On` ou `Off` na instrução substituirá a configuração **Opção Inferir** na **página Compilar**.

  Quando você cria um projeto, a configuração **Opção Inferir** na **página Compilar** é definida como o valor da configuração **Opção Inferir** na caixa de diálogo **Opções**. Para exibir ou alterar a configuração nesta caixa de diálogo, no menu **Ferramentas**, clique em **Opções**. Na caixa de diálogo **Opções**, expanda **Projetos e Soluções** e, em seguida, clique em **Padrões de VB**. A configuração padrão inicial da **Opção Inferir** em **Padrões do VB** é **Ativada**.

  **CPU de destino** Especifica o processador a ser direcionado pelo arquivo de saída. Especifique **x86** para qualquer processador compatível com Intel de 32 bits, **x64** para qualquer processador compatível com Intel de 64 bits, **ARM** para qualquer processador ARM ou **Qualquer CPU** para especificar que qualquer processador é aceitável. **Qualquer CPU** é o valor padrão para novos projetos, pois permite que o aplicativo seja executado no maior número de tipos de hardware.

  Para obter mais informações, consulte [/platform (Visual Basic)](https://msdn.microsoft.com/library/f9bc61e6-e854-4ae1-87b9-d6244de23fd1).

  **Preferir 32 bits** Se a caixa de seleção **Preferir 32 bits** estiver marcada, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 e 64 bits do Windows. Caso contrário, o aplicativo será executado como um aplicativo de 32 bits em versões de 32 bits do Windows e como um aplicativo de 64 bits em versões de 64 bits do Windows.

  Executar como um aplicativo de 64 bits duplica o tamanho do ponteiro e pode causar problemas de compatibilidade com bibliotecas exclusivamente de 32 bits. Fará sentido executar um aplicativo de 64 bits somente se ele for executado consideravelmente mais rápido ou precisar de mais de 4 GB de memória.

  Essa caixa de seleção estará disponível somente se todas as seguintes condições forem verdadeiras:

- Na **Página Compilar**, a lista **CPU de destino** está definida como **Qualquer CPU**.

- Na **Página Aplicativo**, a lista **Tipo de aplicativo** especifica que o projeto é um aplicativo.

- Na **Página Aplicativo**, a lista **Estrutura de destino** especifica o .NET Framework 4.5.

  **Configurações de aviso** Esta tabela lista as condições de build e o nível de notificação correspondente de **Nenhum**, **Aviso** ou **Erro** para cada um.

  Por padrão, todos os avisos do compilador são adicionados à Lista de Tarefas durante a compilação. Selecione **Desabilitar todos os avisos** para instruir o compilador a não enviar avisos ou erros. Selecione **Tratar todos os avisos como erros** se você desejar que o compilador trate avisos como erros que devem ser corrigidos.

  **Desabilitar todos os avisos** Especifica se deve ser permitido que o compilador emita notificações conforme o especificado na tabela **Condição e notificação**, já descrita neste documento. Por padrão, essa caixa de seleção está desmarcada. Marque esta caixa de seleção para instruir o compilador a não emitir avisos ou erros.

  Essa configuração corresponde à opção do compilador [/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83).

  **Tratar todos os avisos como erros** Especifica como tratar avisos. Por padrão, essa caixa de seleção está desmarcada, de modo que todas as notificações de aviso permanecem definidas como **Aviso**. Marque essa caixa de seleção para alterar todas as notificações de aviso para **Erro**.

  Essa opção estará disponível somente se **Desabilitar todos os avisos** estiver desmarcada.

  **Gerar arquivo de documentação XML** Especifica se devem ser geradas informações sobre a documentação. Por padrão, essa caixa de seleção está marcada, instruindo o compilador a gerar informações sobre a documentação e incluí-las em um arquivo XML. Desmarque esta caixa de seleção para instruir o compilador a não criar documentação.

  Essa configuração corresponde à opção do compilador [/doc](https://msdn.microsoft.com/library/5fc32ec9-a149-4648-994c-a8d0cccd0a65).

  **Registrar para interoperabilidade COM** Especifica se o aplicativo gerenciado poderá expor um objeto COM (um COM Callable Wrapper) que permita que um objeto COM interaja com o aplicativo.

  Por padrão, essa caixa de seleção está desmarcada, o que especifica que o aplicativo não permitirá interoperabilidade COM. Marque essa caixa de seleção para permitir a interoperabilidade COM.

  Essa opção não está disponível para projetos de Aplicativos do Windows ou Aplicativo de Console.

  **Eventos de Build** Clique neste botão para acessar a caixa de diálogo **Eventos de Build**. Use essa caixa de diálogo para especificar as instruções de configuração de pré e de pós-build para o projeto. Essa caixa de diálogo aplica-se a somente projetos Visual Basic. Para obter mais informações, consulte [Caixa de diálogo Eventos de Build(Visual Basic)](../../ide/reference/build-events-dialog-box-visual-basic.md).

  **Opções Avançadas de Build** Clique neste botão para acessar a caixa de diálogo **Configurações do AdvancedCompiler**. Use a caixa de diálogo **Configurações Avançadas do Compilador** para especificar as propriedades avançadas de configuração de build de um projeto. Essa caixa de diálogo aplica-se a somente projetos Visual Basic. Para obter mais informações, consulte [Caixa de diálogo Configurações Avançadas do Compilador (Visual Basic)](../../ide/reference/advanced-compiler-settings-dialog-box-visual-basic.md).

## <a name="see-also"></a>Consulte também
 [Depurar e liberar configurações de projeto](https://msdn.microsoft.com/0440b300-0614-4511-901a-105b771b236e) [Gerenciando Propriedades de compilação](https://msdn.microsoft.com/94308881-f10f-4caf-a729-f1028e596a2c) [como: especificar eventos de compilação (Visual Basic)](../../ide/how-to-specify-build-events-visual-basic.md) [Visual Basic compilador de linha de comando](https://msdn.microsoft.com/library/6b57c444-50c7-4b88-8f59-ed65cff5e05c) [como: criar e editar configurações](../../ide/how-to-create-and-edit-configurations.md)
