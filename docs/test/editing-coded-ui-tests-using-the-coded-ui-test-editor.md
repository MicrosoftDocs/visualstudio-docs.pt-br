---
title: Editando Testes de IU Codificados
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.codedUItest.testeditor
helpviewer_keywords:
- coded UI test, Coded UI Test Editor
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: d6c2fcf3d8807e9095abc9546e8bf1e39aecb8ea
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288722"
---
# <a name="edit-coded-ui-tests-using-the-coded-ui-test-editor"></a>Editar testes de IU codificados usando o Editor de Teste de IU Codificado

o Editor de testes de interface de usuário codificada permite modificar facilmente os testes de IU codificados. Ao usar o Editor de Teste de IU Codificado, é possível localizar, exibir e editar as propriedades de métodos de teste e ações de interface do usuário. Além disso, é possível utilizar o mapa de controles de interface do usuário para exibir e editar os controles correspondentes.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**Requisitos**

- Visual Studio Enterprise
- Componente de teste de IU codificado

## <a name="features-of-the-coded-ui-test-editor"></a>Funcionalidades do Editor de Teste de IU Codificado

Usar o Editor de Teste de IU Codificado é mais rápido e eficiente do que editar o código utilizando métodos de testes de IU codificados por meio do Editor de Códigos. Com o Editor de Teste de IU Codificado, é possível usar a barra de ferramentas e os menus de atalho para localizar e modificar rapidamente valores de propriedade associados a ações e controles de interface do usuário. Por exemplo, é possível usar a barra de ferramentas do Editor de Teste de IU Codificado para executar os seguintes comandos:

![Editor de Teste de IU](../test/media/uitesteditor.png)

1. [Localizar](../ide/finding-and-replacing-text.md) ajuda a localizar ações e controles de interface do usuário.

2. **Excluir** remove ações de interface do usuário indesejadas.

3. **Renomear** altera os nomes de métodos de teste e controles.

4. **Propriedades** abre a janela **Propriedades** do item selecionado.

5. **Dividir em um novo método** permite modularizar as ações de interface do usuário.

6. **Mover o Código** adiciona o código personalizado aos métodos de teste.

7. **Inserir Atraso Antes** adiciona uma pausa antes de uma ação de interface do usuário, especificada em milissegundos.

8. **Localizar o Controle de interface do usuário** identifica o local do controle na interface do usuário do aplicativo em teste.

9. **Localizar Todos** ajuda a verificar a propriedade de controle e as mudanças significativas nos controles do aplicativo.

Quando você abre o arquivo *UIMap.uitest* afiliado ao seu teste de IU codificado, o teste de IU codificado é aberto no **Editor de Teste de IU Codificado**. Os procedimentos a seguir descrevem como localizar e editar métodos de teste e propriedades das ações e dos controles da interface do usuário, usando a barra de ferramentas e os menus de atalho do editor.

## <a name="open-a-coded-ui-test"></a>Abrir um teste de IU codificado

Você pode exibir e editar o teste de interface do usuário codificado com base em Visual C# e Visual Basic usando o **Editor de teste de interface do usuário codificado**.

![Menu de contexto Editar com o Construtor de Teste de IU Codificado](../test/media/editcodeduitest.png)

No **Gerenciador de soluções**, abra o menu de atalho para *UIMap. UITest* e escolha **abrir**. O teste de interface do usuário codificado é exibido no **Editor de teste de interface do usuário codificado**. Agora, é possível exibir e editar os métodos, as ações e os controles correspondentes registrados no teste de IU codificado.

> [!TIP]
> Ao selecionar uma ação de interface do usuário localizada em um método do painel **Ações de interface do usuário**, o controle correspondente será realçado. Também é possível modificar a ação de interface do usuário ou as propriedades dos controles.

## <a name="modify-ui-action-and-control-properties"></a>Modificar as propriedades de controle e de ação de interface do usuário

Por meio do Editor de Teste de IU Codificado, é possível localizar e exibir rapidamente todas as ações de interface do usuário de métodos de teste. Ao selecionar a ação de interface do usuário no editor, o controle correspondente será realçado automaticamente. Do mesmo modo, ao selecionar um controle, as ações de interface do usuário correspondentes serão realçadas. Selecionar uma ação ou controle de interface do usuário facilita o uso da janela **Propriedades** para modificar as propriedades correspondentes.

![Propriedades de ação de interface do usuário](../test/media/codeduiedituiaction.png)

Para modificar as propriedades de uma ação de interface do usuário, no painel **Ações de interface do usuário**, expanda o método de teste que contém uma ação de IU cujas propriedades você deseja editar, selecione a ação de interface do usuário e, em seguida, modifique as propriedades usando a janela Propriedades.

Por exemplo, se um servidor estiver indisponível e você tiver uma ação de interface do usuário associada ao seu navegador da Web que declara **ir para página da Web http: \/ /Contoso1/default.aspx**, você poderá alterar a URL para `http://Contoso2/default.aspx` .

![Propriedades de controle](../test/media/codeduitestcontrolprop.png)

Os procedimentos usados para modificar as ações de interface do usuário também podem ser utilizados para modificar as propriedades de um controle. No painel **Mapa do Controle de interface do usuário**, selecione o controle a ser editado e modifique as propriedades por meio da janela **Propriedades**.

Por exemplo, um desenvolvedor pode ter alterado a propriedade **(ID)** em um controle de botão no código-fonte do aplicativo em teste de “idSubmit” para “idLogin”. Com a alteração da propriedade **(ID)** no aplicativo, o teste de IU codificado não poderá localizar o controle de botão e falhará. Nesse caso, o testador pode abrir a coleção **Propriedades de Pesquisa** e alterar a propriedade **Id** para que ela corresponda ao novo valor usado pelo desenvolvedor no aplicativo. O testador também pode alterar o valor da propriedade **Nome Amigável** de “Enviar” para “Logon”. Com essa alteração, a ação de interface do usuário associada ao Editor de Teste de IU Codificado será atualizada de “Escolher botão ‘Enviar’” para “Escolher botão ‘Logon’”.

Após concluir as modificações, salve-as no arquivo *UIMap.Designer* escolhendo **Salvar** na barra de ferramentas do Visual Studio.

### <a name="tips"></a>Dicas

- Se a janela **Propriedades** não for exibida, pressione e segure **Alt** ao mesmo tempo em que pressiona **Enter** ou pressione **F4**.

- Para desfazer as alterações de propriedade feitas, selecione **desfazer** no menu **Editar** ou pressione **Ctrl** + **Z**.

- Você pode usar o botão **Localizar** na barra de ferramentas do editor de teste de interface do usuário codificado para abrir a ferramenta **Localizar e substituir** no Visual Studio. Em seguida, você pode usar o controle **Localizar** para localizar uma ação de interface do usuário no editor de teste de interface do usuário codificado. Por exemplo, você pode tentar localizar “Clicar no botão ‘Logon’”. Isso pode ser útil em testes grandes. Não é possível usar a funcionalidade de substituição na ferramenta **Localizar e Substituir** no Editor de Teste de IU Codificado. Para saber mais, confira o controle Localizar em [Localizar e substituir texto](../ide/finding-and-replacing-text.md).

- Algumas vezes, pode ser difícil visualizar onde os controles estão localizados na interface do usuário do aplicativo em teste. Um dos recursos do Editor de Teste de IU Codificado é a seleção de um controle listado no mapa de controle da interface do usuário e a exibição da localização desse controle no aplicativo em teste. Para saber mais, confira [Localizar um controle de interface do usuário no aplicativo em teste](#locate-a-ui-control-in-the-application-under-test), mais adiante neste artigo.

- Pode ser necessário expandir a caixa de controles que contém o controle a ser editado. Para saber mais, confira [Localizar um controle e seus descendentes](#locate-a-control-and-its-descendants), mais adiante neste artigo.

## <a name="delete-unwanted-ui-actions"></a>Excluir ações de interface do usuário indesejadas

É possível remover ações de interface do usuário indesejadas do teste de IU codificado facilmente.

![Excluir a ação de interface do usuário](../test/media/codeduideleteuiaction.png)

No painel **Ações de interface do usuário**, expanda o método de teste que contém a ação de interface do usuário a ser excluída. Abra o menu de atalho da ação de interface do usuário e escolha **Excluir**.

## <a name="split-a-test-method-into-two-separate-methods"></a>Dividir um método de teste em dois métodos separados

É possível dividir um método de teste para refinar ou modularizar as ações de interface do usuário. Por exemplo, o teste pode ter um único método de teste com ações de interface do usuário em duas caixas de controles. As ações de interface do usuário podem ser modularizadas com mais eficiência em dois métodos que correspondam a um contêiner.

![Dividir um método de teste](../test/media/codeduitestsplitmethod1.png)

![Dois métodos de teste](../test/media/codeduitestsplitmethod2.png)

No painel **Ações de interface do usuário**, expanda o método de teste a ser dividido em dois métodos separados e selecione a ação de interface do usuário em que o novo método de teste começará. Abra o menu de atalho da ação de interface do usuário e escolha **Dividir em um novo método** ou escolha o botão **Dividir em um novo método** na barra de ferramentas do Editor de Teste de IU Codificado. O novo método de teste será exibido no painel **Ações de interface do usuário**. Ele contém as ações de interface do usuário da ação em que a divisão foi especificada.

Após a conclusão do método de divisão, salve as alterações no arquivo *UIMap.Designer* escolhendo **Salvar** na barra de ferramentas do Visual Studio.

> [!WARNING]
> Se você dividir um método, modifique os códigos que chamam o método existente para que eles também chamem o novo método a ser criado caso ainda deseje incluir essas ações de interface do usuário. Quando um método é dividido, uma caixa de diálogo do Microsoft Visual Studio é exibida. Ela avisa que é necessário modificar os códigos que chamam o método existente para que eles também chamem o novo método a ser criado. Escolha **Sim**.

### <a name="tips"></a>Dicas

- Para desfazer a divisão, escolha **desfazer** no menu **Editar** ou pressione **Ctrl** + **Z**.

- É possível renomear o novo método. Selecione-o no painel **ações da interface do usuário** e escolha o botão **renomear** na barra de ferramentas do editor de teste de IU codificado.

   -ou-

   Abra o menu de atalho do novo método de teste e escolha **Renomear**.

   Uma caixa de diálogo do Microsoft Visual Studio é exibida. Ela avisa que é necessário modificar os códigos que referenciam o método. Escolha **Sim**.

## <a name="move-a-test-method-to-the-uimap-file-to-facilitate-customization"></a>Mover um método de teste para o arquivo UIMap a fim de facilitar a personalização

Se que um dos métodos de teste no teste de IU codificado requerer um código personalizado, será necessário movê-lo para o arquivo *UIMap.cs* ou *UIMap.vb*. Caso contrário, o código será substituído sempre que o teste de IU codificado for recompilado. Se o método não for movido, o código personalizado será substituído sempre que o teste for recompilado.

No painel **ação da interface do usuário** , selecione o método de teste que você deseja mover para o arquivo *UIMap.cs* ou *UIMap. vb* para facilitar a funcionalidade de código personalizado que não será substituída quando o código de teste for recompilado. Em seguida, escolha o botão **Mover Código** na barra de ferramentas do Editor de Teste de IU Codificado ou abra o menu de atalho do método de teste e escolha **Mover Código**. O método de teste é removido do arquivo *UIMap.uitest* e não é mais exibido no painel **Ações de Interface do Usuário**. Para editar o arquivo de teste movido, abra o arquivo *UIMap.cs* ou *UIMap.vb* no **Gerenciador de Soluções**.

Após a conclusão do método de movimentação, salve as alterações no arquivo *UIMap.Designer* escolhendo **Salvar** na barra de ferramentas do Visual Studio.

> [!WARNING]
> Depois de mover um método, você não pode mais editá-lo usando o Editor de Teste de IU Codificado. Você deve adicionar seu código personalizado e mantê-lo usando o Editor de Códigos. Quando um método é movido, uma caixa de diálogo do Microsoft Visual Studio é exibida. Ela avisa que o método será movido do arquivo *UIMap.uitest* para o arquivo *UIMap.cs* ou *UIMap.vb* e que não será possível editar o método usando o Editor de Teste de IU Codificado. Escolha **Sim**.

### <a name="tips"></a>Dicas

Para desfazer a movimentação, selecione **desfazer** no menu **Editar** ou pressione **Ctrl** + **Z**. No entanto, você deve remover manualmente o código do arquivo *UIMap.cs* ou *UIMap. vb* .

## <a name="locate-a-ui-control-in-the-application-under-test"></a>Localizar um controle de interface do usuário no aplicativo em teste

Algumas vezes, pode ser difícil visualizar onde os controles estão localizados na interface do usuário do aplicativo em teste. Um dos recursos do Editor de Teste de IU Codificado é a seleção de um controle listado no mapa de controle da interface do usuário e a exibição da localização desse controle no aplicativo em teste. O recurso **Localizar o Controle de interface do usuário** no aplicativo em teste também pode ser usado para verificar modificações na propriedade de pesquisa de um controle.

![Localizar o controle de interface do usuário](../test/media/codeduilocatecontrol.png)

![Controle localizado no aplicativo em teste](../test/media/codeduilocatecontrol2.png)

No painel **Mapa de Controle de interface do usuário**, selecione o controle a ser localizado no aplicativo associado ao teste. Depois, abra o menu de atalho do controle e, em seguida, escolha **Localizar o Controle de interface do usuário**. No aplicativo em teste, o controle será designado com uma borda azul.

> [!NOTE]
> Antes de localizar um controle de interface do usuário, verifique se o aplicativo associado ao teste está em execução.

### <a name="tips"></a>Dicas

É possível usar a opção **Localizar Tudo** para verificar se todos os controles em um contêiner estão localizados corretamente. Essa opção será descrita na próxima seção.

## <a name="locate-a-control-and-its-descendants"></a>Localizar um controle e seus descendentes

É possível verificar se todos os controles em um contêiner estão localizados corretamente na interface do usuário do aplicativo em teste. Isso pode ser útil para verificar alterações de propriedade de pesquisa realizadas no contêiner. Além disso, se houve alterações significativas na interface do usuário do aplicativo em teste, é possível validar se os controles de propriedades de pesquisa existentes ainda estão corretos.

![Localizar todos os controles descendentes](../test/media/codeduilocateall.png)

![Todos os controles localizados](../test/media/codeduilocateall2.png)

No painel **Mapa de Controle de Interface do Usuário**, selecione a caixa de controles cujos descendentes você deseja localizar e exibir. Depois, abra o menu de atalho do controle e escolha **Localizar Tudo**. A caixa de controles e todos os controles descendentes serão marcados no Editor de Teste de IU Codificado com uma marca de seleção verde ou um ‘X’ vermelho. Essas marcas permitem saber se os controles foram localizados com êxito no aplicativo em teste.

> [!NOTE]
> Antes de localizar os controles de interface do usuário, verifique se o aplicativo associado ao teste está em execução.

## <a name="insert-a-delay-before-a-ui-action"></a>Inserir um atraso antes de uma ação de interface do usuário

Ocasionalmente, convém instruir o teste a aguardar a ocorrência de determinados eventos, como a exibição de uma janela, o desaparecimento da barra de progresso etc. Ao utilizar o Editor de Teste de IU Codificado, isso pode ser feito inserindo um atraso antes de uma ação de interface do usuário. É possível especificar quantos segundos o atraso durará.

![Inserir atraso antes de uma ação de interface do usuário](../test/media/codeduidelay.png)

![Atraso adicionado com 5 segundos](../test/media/codeduidealy2.png)

No painel **Ações de interface do usuário**, expanda o método de teste que contém a ação de interface do usuário na qual o atraso será inserido. Selecione a ação de interface do usuário. Depois, abra o menu de atalho da ação de interface do usuário e escolha **Inserir Atraso Antes**. Um atraso será inserido e realçado antes da ação de interface do usuário selecionada com o seguinte texto: **Aguarde 1 segundo de atraso de usuário entre ações**. Na janela **Propriedades** , altere o valor da propriedade **Delay** para o número desejado de milissegundos.

Após a inserção do atraso, salve as alterações no arquivo *UIMap.Designer* escolhendo **Salvar** na barra de ferramentas do Visual Studio.

Se for necessário garantir que um controle específico esteja disponível antes de uma ação de interface do usuário, considere a adição de código personalizado ao método de teste por meio do método UITestControl.WaitForControlXXX() apropriado. Para saber mais, confira [Fazer testes de IU codificado aguardarem eventos específicos durante a reprodução](../test/making-coded-ui-tests-wait-for-specific-events-during-playback.md).

## <a name="see-also"></a>Veja também

- [Usar a automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)
- [Criar testes de IU codificados](../test/use-ui-automation-to-test-your-code.md)
- [Criar um teste de interface do usuário codificado por dados](../test/creating-a-data-driven-coded-ui-test.md)
- [Passo a passo: criar, editar e manter um teste de IU codificado](../test/walkthrough-creating-editing-and-maintaining-a-coded-ui-test.md)
