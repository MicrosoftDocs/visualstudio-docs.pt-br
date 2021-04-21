---
title: Melhorar o desempenho de um suplemento do VSTO
description: Saiba como otimizar os suplementos do VSTO que você cria para aplicativos do Office para que eles sejam inicializados rapidamente, desligados, abram itens e executem outras tarefas.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29035f4867421ed3f05e5f0c3a5c196f58b7ab34
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825115"
---
# <a name="improve-the-performance-of-a-vsto-add-in"></a>Melhorar o desempenho de um suplemento do VSTO
  Você pode dar aos seus usuários uma experiência melhor otimizando os suplementos do VSTO criados para aplicativos do Office para que eles sejam iniciados rapidamente, desligados, abram itens e executem outras tarefas. Se o suplemento do VSTO for para Outlook, você também poderá reduzir a chance de o suplemento do VSTO ser desabilitado devido ao mau desempenho. Você pode aumentar o desempenho do suplemento do VSTO implementando as seguintes estratégias:

- [Carregue os suplementos do VSTO sob demanda](#Load).

- [Publique soluções do Office usando Windows Installer](#Publish).

- [Ignorar reflexão da faixa](#Bypass)de medida.

- [Execute operações caras em um thread de execução separado](#Perform).

  Para obter mais informações sobre como otimizar um suplemento do VSTO do Outlook, consulte [critérios de desempenho para manter os suplementos do VSTO habilitados](/previous-versions/office/jj228679(v=office.15)#performance-criteria-for-keeping-add-ins-enabled).

## <a name="load-vsto-add-ins-on-demand"></a><a name="Load"></a> Carregar suplementos do VSTO sob demanda
 Você pode configurar um suplemento do VSTO para carregar somente nas seguintes circunstâncias:

- A primeira vez que o usuário inicia o aplicativo após a instalação do suplemento do VSTO.

- A primeira vez que o usuário interage com o suplemento do VSTO depois de iniciar o aplicativo a qualquer hora subsequente.

  Por exemplo, o suplemento do VSTO pode preencher uma planilha com dados quando o usuário escolhe um botão personalizado rotulado como **obter meus dados**. O aplicativo deve carregar seu suplemento do VSTO pelo menos uma vez para que o botão **obter meus dados** possa aparecer na faixa de bits. No entanto, o suplemento do VSTO não é carregado novamente quando o usuário inicia o aplicativo na próxima vez. O suplemento do VSTO é carregado somente quando o usuário escolhe o botão **obter meus dados** .

### <a name="to-configure-a-clickonce-solution-to-load-vsto-add-ins-on-demand"></a>Para configurar uma solução de ClickOnce para carregar os suplementos do VSTO sob demanda

1. Em **Gerenciador de soluções**, escolha o nó do projeto.

2. Na barra de menus, escolha **Exibir**  >  **páginas de propriedades**.

3. Na guia **publicar** , escolha o botão **Opções** .

4. Na caixa de diálogo **Opções de publicação** , escolha o item de lista **configurações do Office** , escolha a opção **carregar sob demanda** e escolha o botão **OK** .

### <a name="to-configure-a-windows-installer-solution-to-load-vsto-add-ins-on-demand"></a>Para configurar uma solução de Windows Installer para carregar os suplementos do VSTO sob demanda

1. No registro, defina a `LoadBehavior` entrada da chave de **ID do \\ \\ _suplemento_ \Software\Microsoft\Office _ApplicationName_\Addins _raiz_** como **0x10**.

     Para obter mais informações, consulte [entradas do registro para suplementos do VSTO](../vsto/registry-entries-for-vsto-add-ins.md).

### <a name="to-configure-a-solution-to-load-vsto-add-ins-on-demand-while-you-debug-the-solution"></a>Para configurar uma solução para carregar os suplementos do VSTO sob demanda enquanto você depura a solução

1. Crie um script que defina a `LoadBehavior` entrada da chave de **\\ ID do \\ _suplemento_ \Software\Microsoft\Office _ApplicationName_\Addins _raiz_** para **0x10**.

     O código a seguir mostra um exemplo desse script.

    ```cmd/sh
    [HKEY_CURRENT_USER\Software\Microsoft\Office\Excel\Addins\MyAddIn]
    "Description"="MyAddIn"
    "FriendlyName"="MyAddIn"
    "LoadBehavior"=dword:00000010
    "Manifest"="c:\\Temp\\MyAddIn\\bin\\Debug\\MyAddIn.vsto|vstolocal"

    ```

2. Crie um evento de pós-compilação que atualiza o registro usando o script.

     O código a seguir mostra um exemplo de uma cadeia de caracteres de comando que você pode adicionar a um evento de pós-compilação.

    ```cmd/sh
    regedit /s "$(SolutionDir)$(SolutionName).reg"

    ```

     Para obter informações sobre como criar um evento de pós-compilação em um projeto C#, consulte [como especificar eventos de compilação &#40;C&#35;&#41;](../ide/how-to-specify-build-events-csharp.md).

     Para obter informações sobre como criar um evento de pós-compilação em um projeto Visual Basic, consulte [como especificar eventos de compilação &#40;Visual Basic&#41;](../ide/how-to-specify-build-events-visual-basic.md).

## <a name="publish-office-solutions-by-using-windows-installer"></a><a name="Publish"></a> Publicar soluções do Office usando Windows Installer
 Se você publicar sua solução usando Windows Installer, o tempo de execução das ferramentas do Visual Studio 2010 para Office ignorará as etapas a seguir quando o suplemento do VSTO for carregado.

- Validando o esquema de manifesto.

- Verificando atualizações automaticamente.

- Validando as assinaturas digitais dos manifestos de implantação.

  > [!NOTE]
  > Essa abordagem não será necessária se você implantar o suplemento do VSTO em um local seguro nos computadores dos usuários.

  Para obter mais informações, consulte [implantar uma solução do Office usando Windows Installer](../vsto/deploying-a-vsto-solution-by-using-windows-installer.md).

## <a name="bypass-ribbon-reflection"></a><a name="Bypass"></a> Ignorar reflexão da faixa de medida
 Se você criar uma solução usando o [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] , verifique se os usuários instalaram a versão mais recente do tempo de execução das ferramentas do Visual Studio 2010 para Office ao implantar a solução. Versões mais antigas do tempo de execução do VSTO refletidas em assemblies de solução para localizar personalizações de faixa de das. Esse processo pode fazer com que o suplemento do VSTO seja carregado mais lentamente.

 Como alternativa, você pode impedir que qualquer versão do tempo de execução do Visual Studio 2010 Tools for Office Use reflexão para identificar as personalizações da faixa de opção. Para seguir essa estratégia, substitua o `CreateRibbonExtensibility` método e retorne explicitamente os objetos da faixa de forma. Se o suplemento do VSTO não contiver nenhuma personalização da faixa de forma, retorne `null` dentro do método.

 O exemplo a seguir retorna um objeto de faixa de opções com base no valor de um campo.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_ribbon_choose_ribbon_4/ThisWorkbook.vb" id="Snippet1":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_ribbon_choose_ribbon_4/ThisWorkbook.cs" id="Snippet1":::

## <a name="perform-expensive-operations-in-a-separate-execution-thread"></a><a name="Perform"></a> Executar operações caras em um thread de execução separado
 Considere executar tarefas demoradas (como tarefas de longa execução, conexões de banco de dados ou outros tipos de chamadas de rede) em um thread separado. Para obter mais informações, consulte [suporte a threads no Office](../vsto/threading-support-in-office.md).

> [!NOTE]
> Todo o código que chama para o modelo de objeto do Office deve ser executado no thread principal.

## <a name="see-also"></a>Consulte também

- [Suplementos do VSTO de carregamento por demanda](/archive/blogs/andreww/demand-loading-vsto-add-ins)
- [Atraso ao carregar o CLR nos suplementos do Office](/archive/blogs/andreww/delay-loading-the-clr-in-office-add-ins)
- [Criar suplementos do VSTO para o Office usando o Visual Studio](create-vsto-add-ins-for-office-by-using-visual-studio.md)