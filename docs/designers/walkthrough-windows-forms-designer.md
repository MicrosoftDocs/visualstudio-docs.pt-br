---
title: Tutorial do Designer de Formulários do Windows
ms.date: 08/09/2019
ms.topic: tutorial
helpviewer_keywords:
- Windows Forms Designer, get started
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 11f8480a3a48c1fdee514deb51411e2623055f09
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816456"
---
# <a name="tutorial-get-started-with-windows-forms-designer"></a>Tutorial: introdução ao Designer de Formulários do Windows

O Designer de Formulários do Windows fornece muitas ferramentas para criar aplicativos do Windows Forms. Este artigo ilustra como criar um aplicativo usando as várias ferramentas fornecidas pelo designer, incluindo as seguintes tarefas:

- Organizar os controles usando guias de alinhamento.
- Realizar tarefas de designer usando marcas inteligentes.
- Definir margens e preenchimento para controles.
- Organizar os controles usando um controle <xref:System.Windows.Forms.TableLayoutPanel>.
- Particionar o layout do controle usando um controle <xref:System.Windows.Forms.SplitContainer>.
- Navegar até o layout com a janela Estrutura de Tópicos do Documento.
- Posicionar os controles com a exibição de informações de tamanho e localização.
- Definir os valores de propriedade usando a janela Propriedades.

Quando terminar, haverá um controle personalizado que foi montado usando muitos dos recursos de layout disponíveis no Designer de Formulários do Windows. Este controle implementa a interface do usuário (IU) para uma calculadora simples. A imagem a seguir mostra o layout geral do controle da calculadora:

![Tour guiado da IU da calculadora](media/calculator-ui.gif)

## <a name="create-the-custom-control-project"></a>Criar o projeto de controle personalizado

A primeira etapa é criar o projeto de controle DemoCalculator.

1. Abra o Visual Studio e crie um novo projeto na **Biblioteca de Controle do Windows Forms**. Nomeie o projeto como **DemoCalculatorLib**.

   ::: moniker range=">=vs-2019"

   ![Modelo da Biblioteca de Controle do Windows Forms no Visual Studio 2019](media/windows-forms-control-library-template.png)

   ::: moniker-end

2. Para renomear o arquivo, no **Gerenciador de Soluções**, selecione **UserControl1.vb** ou **UserControl1.cs** com o botão direito do mouse, selecione **Renomear** e altere o nome do arquivo para DemoCalculator.vb ou DemoCalculator.cs. Selecione **Sim** quando for solicitado se deseja renomear todas as referências ao elemento de código “UserControl1”.

O Designer de Formulários do Windows mostra a superfície de designer para o controle DemoCalculator. Nessa exibição, é possível projetar graficamente a aparência do controle selecionando controles e componentes da Caixa de Ferramentas e colocando-os na superfície do designer. Para saber mais sobre controles personalizados, confira [Variedades de controles personalizados](/dotnet/framework/winforms/controls/varieties-of-custom-controls).

## <a name="design-the-control-layout"></a>Criar o layout de controle

O controle DemoCalculator contém vários controles do Windows Forms. Neste procedimento, você organizará os controles usando o Designer de Formulários do Windows.

1. No Designer de Formulários do Windows, altere o controle DemoCalculator para um tamanho maior selecionando a alça de dimensionamento no canto inferior direito e arrastando-a para baixo e para a direita. No canto inferior direito do Visual Studio, encontre as informações de tamanho e localização dos controles. Defina o tamanho do controle para uma largura de 500 e uma altura de 400, observando as informações de tamanho à medida que você redimensiona o controle.

2. Na **Caixa de Ferramentas**, selecione o nó **Contêineres** para abri-lo. Selecione o controle **SplitContainer** e arraste-o para a superfície do designer.

   `SplitContainer` é colocado na superfície do designer do controle DemoCalculator.

    > [!TIP]
    > O controle `SplitContainer` ajusta-se ao tamanho do controle DemoCalculator. Observe a janela **Propriedades** para consultar as configurações da propriedade para o controle `SplitContainer`. Encontre a propriedade <xref:System.Windows.Forms.SplitContainer.Dock%2A>. Seu valor é [DockStyle.Fill](xref:System.Windows.Forms.DockStyle.Fill), o que significa que o controle `SplitContainer` sempre se dimensionará para os limites do controle DemoCalculator. Redimensione o controle DemoCalculator para verificar esse comportamento.

3. Na janela **Propriedades**, altere o valor da propriedade <xref:System.Windows.Forms.SplitContainer.Dock%2A> para `None`.

    O controle `SplitContainer` reduz para o tamanho padrão e não acompanha mais o tamanho do controle DemoCalculator.

4. Selecione o glifo de marca inteligente (![Smart Tag Glyph](media/smart-tag-glyph.gif)) no canto superior direito do controle `SplitContainer`. Selecione **Encaixar no Contêiner Pai** para definir a propriedade `Dock` como `Fill`.

    O controle `SplitContainer` se encaixa nos limites do controle DemoCalculator.

    > [!NOTE]
    > Vários controles oferecem marcas inteligentes para facilitar o design. Para obter mais informações, consulte [Walkthrough: Execute tarefas comuns usando marcas inteligentes em controles de Windows Forms](/dotnet/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls).

5. Selecione a borda vertical entre os painéis e arraste-a para a direita, de modo que a maior parte do espaço seja tomada pelo painel esquerdo.

    `SplitContainer` divide o controle DemoCalculator em dois painéis com uma borda móvel separando-os. O painel à esquerda mostrará os botões e a tela da calculadora, e o painel à direita mostrará um registro das operações aritméticas realizadas pelo usuário.

6. Na janela **Propriedades**, altere o valor da propriedade `BorderStyle` para `Fixed3D`.

7. Na **Caixa de Ferramentas**, selecione o nó **Controles Comuns** para abri-lo. Selecione o controle `ListView` e arraste-o para o painel direito do controle `SplitContainer`.

8. Selecione o glifo de marca inteligente do controle `ListView`. No painel de marcas inteligentes, altere a configuração `View` para `Details`.

9. No painel de marcas inteligentes, selecione **Editar Colunas**.

   A caixa de diálogo **Editor de Coleção ColumnHeader** abre.

10. Na caixa de diálogo **Editor de Coleção ColumnHeader**, selecione **Adicionar** para adicionar uma coluna ao controle `ListView`. Altere o valor da propriedade `Text` da coluna para **Histórico**. Selecione **OK** para criar a coluna.

11. No painel de marcas inteligentes, selecione **Encaixar no Contêiner Pai** e, em seguida, selecione o glifo de marca inteligente para fechar o painel de marcas inteligentes.

12. Na **Caixa de Ferramentas** do nó **Contêineres**, arraste um controle `TableLayoutPanel` para o painel esquerdo do controle `SplitContainer`.

    O controle `TableLayoutPanel` aparece na superfície do designer com o painel de marcas inteligentes aberto. O controle `TableLayoutPanel` organiza seus controles filhos em uma grade. O controle `TableLayoutPanel` manterá a exibição e os botões do controle DemoCalculator. Para obter mais informações, consulte [Walkthrough: organizar controles usando um TableLayoutPanel](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-a-tablelayoutpanel).

13. Selecione **Editar Linhas e Colunas** no painel de marcas inteligentes.

    A caixa de diálogo **Estilos de Coluna e Linha** abre.

14. Selecione o botão **Adicionar** até que cinco colunas sejam exibidas. Selecione todas as cinco colunas e, em seguida, selecione **Porcentagem** na caixa **Tipo de Tamanho**. Defina o valor **Porcentagem** como **20**. Isso define cada coluna com a mesma largura.

15. Em **Mostrar**, selecione **Linhas**.

16. Selecione **Adicionar** até que cinco linhas sejam exibidas. Selecione todas as cinco linhas e, em seguida, selecione **Porcentagem** na caixa **Tipo de Tamanho**. Defina o valor **Porcentagem** como **20**. Isso define cada linha com a mesma altura.

17. Selecione**OK** para aceitar as alterações e, em seguida, selecione o glifo de marca inteligente para fechar o painel de marcas inteligentes.

18. Na janela **Propriedades**, altere o valor da propriedade `Dock` para `Fill`.

## <a name="populate-the-control"></a>Preencher o controle

Agora que o layout do controle está configurado, você pode preencher o controle DemoCalculator com botões e uma tela.

1. Na **Caixa de Ferramentas**, clique duas vezes no ícone de controle `TextBox`.

   Um controle `TextBox` é colocado na primeira célula do controle `TableLayoutPanel`.

2. Na janela **Propriedades**, altere o valor da propriedade ColumnSpan do controle `TextBox` para **5**.

   O controle `TextBox` fica centralizado em sua linha.

3. Altere o valor da propriedade `Anchor` do controle `TextBox` para `Left`, `Right`.

   O controle `TextBox` expande horizontalmente para abranger todas as cinco colunas.

4. Altere o valor da propriedade `TextBox` do controle `TextAlign` para `Right`.

5. Na janela **Propriedades**, expanda o nó de propriedade `Font`. Defina `Size` como **14** e `Bold` como **true** para os controles `TextBox`.

6. Selecione o controle `TableLayoutPanel`.

7. Na **Caixa de Ferramentas**, clique duas vezes no ícone `Button`.

   Um controle `Button` é colocado na próxima célula aberta do controle `TableLayoutPanel`.

8. Na **Caixa de Ferramentas**, clique duas vezes no ícone `Button` mais quatro vezes para preencher a segunda linha do controle `TableLayoutPanel`.

9. Selecione todos os cinco controles `Button` pressionando a tecla **Shift** durante a seleção. Pressione **Ctrl** + **C** para copiar os `Button` controles para a área de transferência.

10. Pressione **Ctrl** + **V** três vezes para colar cópias dos `Button` controles nas linhas restantes do `TableLayoutPanel` controle.

11. Selecione todos os 20 controles `Button` pressionando a tecla **Shift** durante a seleção.

12. Na janela **Propriedades**, altere o valor da propriedade `Dock` para `Fill`.

    Todos os controles `Button` são encaixados para preencher suas células.

13. Na janela **Propriedades**, expanda o nó de propriedade `Margin`. Defina o valor de `All` como **5**.

    Todos os controles `Button` são menores para criar uma margem maior entre eles.

14. Selecione **button10** e **button20**, em seguida, pressione **Excluir** para removê-los do layout.

15. Selecione **button5** e **button15**, em seguida, altere o valor da propriedade `RowSpan` para **2**. Esses serão os botões **Limpar** e **=** para o controle DemoCalculator.

## <a name="use-the-document-outline-window"></a>Usar a janela Estrutura de Tópicos do Documento

Ao preencher o controle ou formulário com vários controles, talvez seja mais fácil navegar no layout com a janela Estrutura de Tópicos do Documento.

1. Na barra de menus, escolha **Exibir**  >  **outro**  >  **estrutura de tópicos de documento**do Windows.

   A janela Estrutura de Tópicos do Documento mostra um modo de exibição de árvore do controle DemoCalculator e seus controles. Controles de contêiner, como `SplitContainer`, mostram seus controles filhos como subnós na árvore. Também é possível renomear controles no local usando a janela Estrutura de Tópicos do Documento.

2. Na janela **Estrutura de Tópicos do Documento**, clique com o botão direito do mouse em **button1** e, em seguida, selecione **Renomear**. Altere seu nome para sevenButton.

3. Usando a janela **Estrutura de Tópicos do Documento**, renomeie os controles `Button` do nome gerado pelo designer para o nome de produção, de acordo com a lista a seguir:

   - button1 para **sevenButton**

   - button2 para **eightButton**

   - button3 para **nineButton**

   - button4 para **divisionButton**

   - button5 para **clearButton**

   - button6 para **fourButton**

   - button7 para **fiveButton**

   - button8 para **sixButton**

   - button9 para **multiplicationButton**

   - button11 para **oneButton**

   - button12 para **twoButton**

   - button13 para **threeButton**

   - button14 para **subtractionButton**

   - button15 para **equalsButton**

   - button16 para **zeroButton**

   - button17 para **changeSignButton**

   - button18 para **decimalButton**

   - button19 para **additionButton**

4. Usando as janelas **Estrutura de Tópicos do Documento** e **Propriedades**, altere o valor da propriedade `Text` para cada nome de controle `Button` de acordo com a lista a seguir:

   - Altere a propriedade de texto do controle sevenButton para **7**

   - Altere a propriedade de texto do controle eightButton para **8**

   - Altere a propriedade de texto do controle nineButton para **9**

   - Alterar a propriedade texto do controle divisionButton para **/** (barra invertida)

   - Altere a propriedade de texto do controle clearButton para **Limpar**

   - Altere a propriedade de texto do controle fourButton para **4**

   - Altere a propriedade de texto do controle fiveButton para **5**

   - Altere a propriedade de texto do controle sixButton para **6**

   - Alterar a propriedade texto do controle multiplicationButton para **\*** (asterisco)

   - Altere a propriedade de texto do controle oneButton para **1**

   - Altere a propriedade de texto do controle twoButton para **2**

   - Altere a propriedade de texto do controle threeButton para **3**

   - Alterar a propriedade texto do controle subtractionButton para **-** (hífen)

   - Alterar a propriedade texto do controle equalsButton para **=** (sinal de igual)

   - Altere a propriedade de texto do controle zeroButton para **0**

   - Altere a propriedade texto do controle changeSignButton para**+/-**

   - Altere a propriedade de texto do controle decimalButton para **.** (ponto final)

   - Alterar a propriedade texto do controle additionButton para **+** (sinal de adição)

5. Na superfície do designer, mantenha pressionada a tecla **Shift** e clique para selecionar todos os controles `Button`.

6. Na janela **Propriedades**, expanda o nó de propriedade `Font`. Defina `Size` como **14** e `Bold` como **true** para todos os controles `Button`.

Isso conclui o design do controle DemoCalculator. Tudo o que resta é fornecer a lógica da calculadora.

## <a name="implement-event-handlers"></a>Implementar manipuladores de eventos

Os botões no controle DemoCalculator têm manipuladores de eventos que podem ser usados ​​para implementar grande parte da lógica da calculadora. O Designer de Formulários do Windows possibilita implementar os stubs de todos os manipuladores de eventos para todos os botões com um clique duplo.

1. Na superfície do designer, mantenha pressionada a tecla **Shift** e clique para selecionar todos os controles `Button`.

2. Clique duas vezes em um dos controles `Button`.

   O Editor de Códigos abre para os manipuladores de eventos gerados pelo designer.

## <a name="test-the-control"></a>Testar o controle

Como o controle DemoCalculator herda da classe <xref:System.Windows.Forms.UserControl>, é possível testar seu comportamento com o **Contêiner de Teste de Classes UserControl**. Para obter mais informações, consulte [como: testar o comportamento de tempo de execução de um UserControl](/dotnet/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol).

1. Pressione **F5** para compilar e executar o controle DemoCalculator no **Contêiner de Teste de Classes UserControl**.

2. Selecione a borda entre os painéis `SplitContainer` e arraste para a esquerda e para a direita. `TableLayoutPanel` e todos os seus controles filhos se redimensionam para caber no espaço disponível.

3. Quando terminar de testar o controle, selecione **Fechar**.

## <a name="use-the-control-on-a-form"></a>Usar o controle em um formulário

O controle DemoCalculator pode ser usado em outros controles compostos ou em um formulário. O procedimento a seguir descreve como usá-lo.

### <a name="create-the-project"></a>Criar o projeto

A primeira etapa é criar o projeto do aplicativo. Você usará esse projeto para criar o aplicativo que exibe seu controle personalizado.

1. Crie um novo projeto **Aplicativo do Windows Forms** e nomeie-o como **DemoCalculatorTest**.

2. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DemoCalculatorTest** e selecione **Adicionar referência** para abrir a caixa de diálogo **Adicionar referência** .

3. Selecione a guia **Projetos** e clique duas vezes no projeto DemoCalculatorLib para adicionar a referência ao projeto de teste.

4. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **DemoCalculatorTest** e, em seguida, selecione **Definir como Projeto de Inicialização**.

5. No Designer de Formulários do Windows, aumente o tamanho do formulário para aproximadamente **700 x 500**.

### <a name="use-the-control-in-the-forms-layout"></a>Usar o controle no layout do formulário

Para usar o controle DemoCalculator em um aplicativo, é preciso colocá-lo em um formulário.

1. Na **Caixa de Ferramentas**, expanda o nó **Componentes do DemoCalculatorLib**.

2. Arraste o controle **DemoCalculator** da **Caixa de Ferramentas** para seu formulário. Mova o controle para o canto superior esquerdo do formulário. Quando o controle estiver próximo das bordas do formulário, *guias de alinhamento* aparecerão. Guias de alinhamento indicam a distância da propriedade `Padding` do formulário e da propriedade `Margin` do controle. Posicione o controle no local indicado pelas guias de alinhamento.

   Para obter mais informações, consulte [Walkthrough: organizar controles usando Snaplines](/dotnet/framework/winforms/controls/walkthrough-arranging-controls-on-windows-forms-using-snaplines).

3. Arraste um controle `Button` da **Caixa de Ferramentas** e solte-o no formulário.

4. Mova o controle `Button` em volta do controle DemoCalculator e observe onde as guias de alinhamento aparecem. Você pode alinhar seus controles com precisão e facilidade usando esse recurso. Exclua o controle `Button` quando terminar.

5. Clique com o botão direito do mouse no controle DemoCalculator e selecione **Propriedades**.

6. Altere o valor da propriedade `Dock` para `Fill`.

7. Selecione o formulário e, em seguida, expanda o nó da propriedade `Padding`. Altere o valor de **Todos** para **20**.

   O tamanho do controle DemoCalculator é reduzido para acomodar o novo valor de `Padding` do formulário.

8. Redimensione o formulário arrastando as várias alças de dimensionamento para diferentes posições. Observe como o controle DemoCalculator muda para se ajustar.

## <a name="next-steps"></a>Próximas etapas

Este artigo demonstrou como construir a interface do usuário para uma calculadora simples. Para continuar, você pode ampliar sua funcionalidade implementando a lógica da calculadora e, em seguida, [publicar o aplicativo usando o ClickOnce](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md). Ou continue com um tutorial diferente no qual você [cria um visualizador de imagens usando o Windows Forms](../ide/tutorial-1-create-a-picture-viewer.md).

## <a name="see-also"></a>Veja também

- [Controles de formulários do Windows](/dotnet/framework/winforms/controls/)
- [Acessibilidade para controles do Windows Forms](/dotnet/framework/winforms/controls/providing-accessibility-information-for-controls-on-a-windows-form)
- [Publicar usando o ClickOnce](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)
