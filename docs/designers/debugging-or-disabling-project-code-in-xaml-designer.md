---
title: Depurar ou desabilitar o código do projeto no Designer XAML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: ac600581-8fc8-49e3-abdf-1569a3483d74
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 191d180a68edd439c729fa963b607c992ff3c00e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49816763"
---
# <a name="debug-or-disable-project-code-in-xaml-designer"></a>Depurar ou desabilitar o código do projeto no Designer XAML

Em muitos casos, as exceções sem tratamento no Designer **XAML** podem ser causadas quando o código do projeto tenta acessar propriedades ou métodos que retornam valores diferentes ou que funcionam de maneira diferente quando o aplicativo é executado no designer. Você pode resolver essas exceções ao depurar o código do projeto em outra instância do Visual Studio ou impedir exceções temporariamente desabilitando o código do projeto no designer.

O código do projeto inclui:

-   Controles personalizados e controles de usuário

-   Bibliotecas de classes

-   Conversores de valor

-   Associações em relação a dados de tempo de design gerados do código do projeto

Quando o código do projeto está desabilitado, o Visual Studio mostra espaços reservados. Por exemplo, o Visual Studio mostra o nome da propriedade para uma associação em que os dados não estão mais disponíveis ou um espaço reservado para um controle que não está mais funcionando.

![Caixa de diálogo de exceção sem tratamento](../designers/media/xaml_unhandledexception.png)

## <a name="to-determine-if-project-code-is-causing-an-exception"></a>Para determinar se o código do projeto está causando uma exceção

1.  Na caixa de diálogo de exceção sem tratamento, selecione o link **Clique aqui para recarregar o designer**.

2.  Na barra de menus, selecione **Depurar** > **Iniciar Depuração** para compilar e executar o aplicativo.

     Se o aplicativo for compilado e executado com êxito, a exceção de tempo de design pode ser causada pela execução do seu código de projeto no designer.

## <a name="to-debug-project-code-running-in-the-designer"></a>Para depurar o código de projeto em execução no designer

1.  Na caixa de diálogo de exceção sem tratamento, selecione o link **Clique aqui para desabilitar o código do projeto em execução e recarregar o designer**.

2.  No Gerenciador de tarefas do Windows, selecione o botão **Finalizar Tarefa** para fechar todas as instâncias do Designer XAML do Visual Studio que estão sendo executadas.

     ![Instâncias do Designer XAML no TaskManager](../designers/media/xaml_taskmanager.png)

3.  No Visual Studio, abra a página XAML que contém o código ou o controle que deseja depurar.

4.  Abra uma nova instância do Visual Studio e, em seguida, abra uma segunda instância do seu projeto.

5.  Defina um ponto de interrupção no código do projeto.

6.  Na nova instância do Visual Studio, na barra de menus, selecione **Depurar** > **Anexar ao Processo**.

7.  Na caixa de diálogo **Anexar ao Processo**, na lista de **Processos Disponíveis** selecione **XDesProc.exe** e, em seguida, selecione o botão **Anexar**.

     ![O processo do Designer XAML](../designers/media/xaml_attach.png)

     Este é o processo para o designer XAML na primeira instância do Visual Studio.

8.  Na primeira instância do Visual Studio, na barra de menus, escolha **Depurar** > **Iniciar Depuração**.

     Agora, você pode intervir em seu código que está sendo executado no designer.

## <a name="to-disable-project-code-in-the-designer"></a>Para desabilitar o código do projeto no designer

-   Na caixa de diálogo de exceção sem tratamento, selecione o link **Clique aqui para desabilitar o código do projeto em execução e recarregar o designer**.

-   Como alternativa, na barra de ferramentas do **Designer XAML**, clique no botão **Desabilitar código do projeto**.

     ![O botão Desabilitar Código do Projeto](../designers/media/xaml_disablecode.png)

     Você pode alternar o botão novamente para reabilitar o código do projeto.

    > [!NOTE]
    > Para projetos que buscam processadores ARM ou X64, o Visual Studio não pode executar o código do projeto no designer, portanto, o botão **Desabilitar código de projeto** está desabilitado no designer.

-   Qualquer opção faz com que o designer seja recarregado e, em seguida, desabilite todo o código do projeto associado.

    > [!NOTE]
    > Desabilitar o código do projeto pode levar a uma perda de dados do tempo de design. Uma alternativa é depurar o código em execução no designer.

## <a name="control-display-options"></a>Opções de exibição de controle

> [!NOTE]
> **Controlar Opções de Exibição** só está disponível para aplicativos da Plataforma Universal do Windows que se destinam ao Windows 10 Fall Creators Update (build 16299) ou posterior. O recurso **Opções de Exibição do Controle** está disponível no Visual Studio 2017 versão 15.9 ou posterior. 

No designer XAML, você pode alterar as opções de exibição de controle para exibir somente os controles de plataforma do SDK do Windows. Isso pode aumentar a confiabilidade do designer XAML.

Para alterar as opções de exibição de controle, clique no ícone na parte inferior esquerda da janela do designer e selecione uma opção em **Opções de Exibição de Controle**:

![Opções de Exibição de Controle](../designers/media/control_display_options.png)

Quando você selecionar **Exibir Somente os Controles de Plataforma**, todos os controles personalizados provenientes de SDKs, controles de usuário do cliente e outros não serão renderizados completamente. Em vez disso, eles serão substituídos por controles de fallback para demonstrar o tamanho e a posição do controle.

## <a name="see-also"></a>Consulte também

- [Projetar XAML no Visual Studio e no Blend para Visual Studio](../designers/designing-xaml-in-visual-studio.md)
