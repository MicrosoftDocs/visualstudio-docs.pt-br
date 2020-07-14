---
title: Habilitar testes de IU codificado dos controles
ms.date: 11/04/2016
ms.topic: how-to
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: d94c68a660201b0a8767b1405fcd4399cdf6d660
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288683"
---
# <a name="enable-coded-ui-testing-of-your-controls"></a>Habilitar testes de IU codificado dos controles

Implemente o suporte à estrutura de teste de IU codificado para que seu controle possa ser testado. É possível adicionar níveis crescentes de suporte incrementalmente. Comece com o suporte ao registro e reprodução e à validação de propriedade. Em seguida, baseie-se nele para habilitar o construtor de teste de IU codificado a reconhecer as propriedades personalizadas do controle. Forneça classes personalizadas para acessar essas propriedades do código gerado. Você também pode ajudar o construtor de teste de IU codificado a capturar ações da maneira mais próxima à intenção da ação que está sendo registrada.

![CUIT&#95;Full](../test/media/cuit_full.png)

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="support-record-and-playback-and-property-validation-by-implementing-accessibility"></a>Suporte ao registro, reprodução e validação de propriedade com a implementação de acessibilidade

O construtor de teste de IU codificado captura informações sobre os controles que ele encontra durante uma gravação e, em seguida, gera código para repetir essa sessão. Se o controle não der suporte à acessibilidade, o teste de IU codificado capturará ações (como cliques do mouse) usando coordenadas da tela. Quando o teste é executado, o código gerado emite as ações nas mesmas coordenadas de tela. Se o controle for exibido em um local diferente na tela quando o teste for reproduzido, o código gerado falhará ao executar a ação. Se não implementar a acessibilidade para o controle, talvez você veja falhas de teste se o teste for reproduzido em configurações de tela diferentes, em ambientes diferentes ou quando o layout da IU for alterada.

![CUIT&#95;RecordNoSupport](../test/media/cuit_recordnosupport.png)

Se você implementar a acessibilidade, o construtor de teste de IU codificado usará isso para capturar informações sobre seu controle quando registrar um teste. Em seguida, quando você executar o teste, o código gerado reproduzirá esses eventos em relação ao seu controle, mesmo que ele esteja em outro lugar na interface do usuário. Os autores do teste também podem criar asserções usando as propriedades básicas do controle.

![CUIT&#95;Record](../test/media/cuit_record.png)

### <a name="to-support-record-and-playback-property-validation-and-navigation-for-a-windows-forms-control"></a>Para dar suporte à gravação e reprodução, validação de propriedade e navegação para controle do Windows Forms
Implemente a acessibilidade para seu controle conforme descrito no procedimento a seguir e explicado em detalhes em <xref:System.Windows.Forms.AccessibleObject>.

![CUIT&#95;Accessible](../test/media/cuit_accessible.png)

1. Implemente uma classe que seja derivada de <xref:System.Windows.Forms.Control.ControlAccessibleObject> e substitua a propriedade <xref:System.Windows.Forms.Control.AccessibilityObject%2A> para retornar um objeto da sua classe.

    ```csharp
    public partial class ChartControl : UserControl
    {
        // Overridden to return the custom AccessibleObject for the control.
        protected override AccessibleObject CreateAccessibilityInstance()
        {
            return new ChartControlAccessibleObject(this);
        }

        // Inner class ChartControlAccessibleObject represents accessible information
        // associated with the ChartControl and is used when recording tests.
        public class ChartControlAccessibleObject : ControlAccessibleObject
        {
            ChartControl myControl;
            public ChartControlAccessibleObject(ChartControl ctrl)
                : base(ctrl)
            {
                myControl = ctrl;
            }
        }
    }
    ```

2. Substitua as propriedades e os métodos <xref:System.Windows.Forms.AccessibleObject.Role%2A>, <xref:System.Windows.Forms.AccessibleObject.State%2A>, <xref:System.Windows.Forms.AccessibleObject.GetChild%2A> e <xref:System.Windows.Forms.AccessibleObject.GetChildCount%2A> do objeto acessível.

3. Implemente outro objeto de acessibilidade para o controle filho e substitua a propriedade <xref:System.Windows.Forms.Control.AccessibilityObject%2A> do controle filho para retornar esse objeto de acessibilidade.

4. Substitua as propriedades e os métodos <xref:System.Windows.Forms.AccessibleObject.Bounds%2A>, <xref:System.Windows.Forms.AccessibleObject.Name%2A>, <xref:System.Windows.Forms.AccessibleObject.Parent%2A>, <xref:System.Windows.Forms.AccessibleObject.Role%2A>, <xref:System.Windows.Forms.AccessibleObject.State%2A>, <xref:System.Windows.Forms.AccessibleObject.Navigate%2A> e <xref:System.Windows.Forms.AccessibleObject.Select%2A> para o objeto de acessibilidade do controle filho.

> [!NOTE]
> Este tópico começa com o exemplo de acessibilidade em <xref:System.Windows.Forms.AccessibleObject> e, em seguida, se baseia nele nos procedimentos restantes. Se você quiser criar uma versão de trabalho do exemplo de acessibilidade, crie um aplicativo de console e substitua o código em *Program.cs* pelo código de exemplo. Adicione referências a Acessibilidade, System.Drawing e System.Windows.Forms. Altere os **Tipos de Inserção de Interoperabilidade** de Acessibilidade para **Falso** para eliminar um aviso de build. Você pode alterar o tipo de saída do projeto de **Aplicativo de Console** para **Aplicativos do Windows** para que uma janela de console não apareça ao executar o aplicativo.

## <a name="support-custom-property-validation-by-implementing-a-property-provider"></a>Suporte à validação de propriedade personalizada com a implementação de um provedor de propriedade

Depois de implementar o suporte básico para registro e reprodução e validação de propriedade, você poderá disponibilizar as propriedades personalizadas do controle para testes de IU codificados implementando um plug-in <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>. Por exemplo, o procedimento a seguir cria um provedor de propriedade que permite que os testes de IU codificados acessem a propriedade State dos controles filho de CurveLegend do controle do gráfico:

![CUIT&#95;CustomProps](../test/media/cuit_customprops.png)

### <a name="to-support-custom-property-validation"></a>Para dar suporte à validação de propriedade personalizada

![CUIT&#95;Props](../test/media/cuit_props.png)

1. Substitua a propriedade <xref:System.Windows.Forms.AccessibleObject.Description%2A> do objeto acessível da curva de legenda para passar valores de propriedade avançada na cadeia de caracteres de descrição. Separe vários valores com ponto-e-vírgula (;).

    ```csharp
    public class CurveLegendAccessibleObject : AccessibleObject
    {
        // add the state property value to the description
        public override string Description
        {
            get
            {
                // Add ";" and the state value to the end
                // of the curve legend's description
                return "CurveLegend; " + State.ToString();
            }
        }
    }
    ```

1. Crie um pacote de extensão de teste de IU para seu controle criando um projeto de biblioteca de classes. Adicione referências a Accessibility, Microsoft.VisualStudio.TestTools.UITesting, Microsoft.VisualStudio.TestTools.UITest.Common e Microsoft.VisualStudio.TestTools.Extension. Altere os **Tipos de Inserção de Interoperabilidade** para Acessibilidade para **False**.

1. Adicione uma classe de provedor de propriedade que seja derivada de <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>:

    ```csharp
    using System;
    using System.Collections.Generic;
    using Accessibility;
    using Microsoft.VisualStudio.TestTools.UITesting;
    using Microsoft.VisualStudio.TestTools.UITest.Extension;
    using Microsoft.VisualStudio.TestTools.UITesting.WinControls;
    using Microsoft.VisualStudio.TestTools.UITest.Common;

    namespace ChartControlExtensionPackage
    {
        public class ChartControlPropertyProvider : UITestPropertyProvider
        {
        }
    }
    ```

1. Implemente o provedor de propriedade colocando os nomes e descritores de propriedade em um <xref:System.Collections.Generic.Dictionary%602>.

1. Substitua <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A?displayProperty=fullName> para indicar que o assembly fornece suporte específico do controle para o controle e seus filhos.

1. Substitua os métodos abstratos restantes de <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider?displayProperty=fullName>

1. Adicione uma classe de pacote de extensão que seja derivada de <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>.

1. Defina o atributo `UITestExtensionPackage` do assembly.

1. Na classe de pacote de extensão, substitua <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A?displayProperty=fullName> para retornar a classe do provedor de propriedade quando um provedor de propriedade for solicitado.

1. Substitua as propriedades e os métodos abstratos restantes de <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>.

1. Compile seus binários e copie-os para *%ProgramFiles%\Common\Microsoft Shared\VSTT\10.0\UITestExtensionPackages*.

> [!NOTE]
> Este pacote de extensão será aplicado a qualquer controle que seja do tipo "Texto". Se você estiver testando vários controles do mesmo tipo, teste-os separadamente e gerenciar quais pacotes de extensão serão implantados ao registrar os testes.

## <a name="support-code-generation-by-implementing-a-class-to-access-custom-properties"></a>Suporte à geração de código com a implementação de uma classe para propriedades personalizadas de acesso

Quando o construtor de teste de IU codificado gera código de uma gravação de sessão, ele usa a classe <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl> para acessar os controles.

Se você já implementou um provedor de propriedade para conceder acesso às propriedades personalizadas do controle, poderá adicionar uma classe especializada usada para acessar essas propriedades. Adicionar uma classe especializada simplifica o código gerado.

### <a name="to-add-a-specialized-class-to-access-your-control"></a>Para adicionar uma classe especializada para acessar seu controle

![CUIT&#95;CodeGen](../test/media/cuit_codegen.png)

1. Implemente uma classe que seja derivada de <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinControl> e adicione o tipo do controle à coleção de propriedades de pesquisa no construtor.

1. Implemente as propriedades personalizadas do controle como propriedades da classe.

1. Substitua o método <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetSpecializedClass%2A?displayProperty=fullName> do provedor de propriedade para retornar o tipo da nova classe para os controles filho de legenda de curva.

1. Substitua o método <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetPropertyNamesClassType%2A> do provedor de propriedade para retornar o tipo do método PropertyNames da nova classe.

## <a name="support-intent-aware-actions-by-implementing-an-action-filter"></a>Suporte a ações com reconhecimento de intenção com a implementação de um filtro de ação

Quando o Visual Studio registra um teste, ele captura cada evento do mouse e do teclado. No entanto, em alguns casos, a intenção da ação pode ser perdida na série de eventos de mouse e de teclado. Por exemplo, se o controle dá suporte ao preenchimento automático, o mesmo conjunto de eventos de mouse e teclado podem resultar em um valor diferente quando o teste é reproduzido em um ambiente diferente. Você pode adicionar um plug-in de filtro de ação que substitui a série de eventos de teclado e mouse por uma única ação. Dessa forma, você pode substituir a série de eventos de mouse e de teclado que selecionam um valor com uma única ação que define o valor. Isso protege os testes de UI codificados contra as diferenças no preenchimento automático de um ambiente para outro.

### <a name="to-support-intent-aware-actions"></a>Para dar suporte a ações com reconhecimento de intenção

![CUIT&#95;Actions](../test/media/cuit_actions.png)

1. Implemente uma classe de filtro de ação derivada de [UITestActionFilter](/previous-versions/visualstudio/visual-studio-2012/dd985757(v=vs.110)), substituindo as propriedades [ApplyTimeout](/previous-versions/visualstudio/visual-studio-2012/dd984649%28v%3dvs.110%29), [Category](/previous-versions/visualstudio/visual-studio-2012/dd986905(v=vs.110)), [Enabled](/previous-versions/visualstudio/visual-studio-2012/dd985633(v=vs.110)), [FilterType](/previous-versions/visualstudio/visual-studio-2012/dd778726(v=vs.110)), [Group](/previous-versions/visualstudio/visual-studio-2012/dd779219(v=vs.110)) e [Name](/previous-versions/visualstudio/visual-studio-2012/dd998334(v=vs.110)).

1. Substitua [ProcessRule](/previous-versions/visualstudio/visual-studio-2012/dd987281(v=vs.110)). Esse exemplo substitui uma ação de clicar duas vezes por uma ação de clique único.

1. Adicione o filtro de ação ao método <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> do seu pacote de extensão.

1. Crie seus binários e copie-os para *%ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages*.

> [!NOTE]
> O filtro de ação não depende da implementação de acessibilidade ou do provedor de propriedade.

## <a name="debug-your-property-provider-or-action-filter"></a>Depurar seu provedor de propriedade ou filtro de ação

O provedor da propriedade e o filtro de ação são implementados em um pacote de extensão. O construtor de teste executa o pacote de extensão em um processo separado do seu aplicativo.

### <a name="to-debug-your-property-provider-or-action-filter"></a>Para depurar seu provedor de propriedade ou filtro de ação

1. Compilar a versão de depuração do seu pacote de extensão Copie os arquivos *. dll* e *. pdb* para *%ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages*.

2. Execute seu aplicativo (não no depurador).

3. Execute o construtor de teste de IU codificado.

     `codedUITestBuilder.exe  /standalone`

4. Anexe o depurador ao processo codedUITestBuilder.

5. Defina os pontos de interrupção no seu código.

6. No construtor de teste de IU codificado, crie asserções para exercitar seu provedor de propriedade e registrar ações para exercitar seus filtros de ação.

## <a name="see-also"></a>Veja também

- <xref:System.Windows.Forms.AccessibleObject>
- [Usar a automação da interface do usuário para testar o código](../test/use-ui-automation-to-test-your-code.md)
