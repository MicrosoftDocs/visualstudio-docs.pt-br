---
title: Habilitar testes de IU codificados dos controles | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ef1188f-89dc-413d-801d-0efdaf9b0427
caps.latest.revision: 24
ms.author: gewarren
manager: douge
ms.openlocfilehash: e5ab2ca3e0f7d8f7006177f89c6850ce9882681a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49848534"
---
# <a name="enable-coded-ui-testing-of-your-controls"></a>Habilitar testes de IU codificado dos controles
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

É possível testar o controle mais facilmente se você implementar o suporte à estrutura de teste de IU codificado. É possível adicionar níveis crescentes de suporte incrementalmente. Você pode começar com o suporte ao registro e reprodução e à validação de propriedade. Você poderá, então, usar isso como base para permitir que o construtor de teste de IU codificado reconheça as propriedades personalizadas do controle e fornecer classes personalizadas para acessar as propriedades do código gerado. Você também pode ajudar o construtor de teste de IU codificado a capturar ações da maneira mais próxima à intenção da ação que está sendo registrada.  
  
 **Neste tópico:**  
  
1. [Suporte ao registro e reprodução, e validação de propriedade com a implementação de acessibilidade](../test/enable-coded-ui-testing-of-your-controls.md#recordandplayback)  
  
2. [Suporte à validação de propriedade personalizada com a implementação de um provedor de propriedade](../test/enable-coded-ui-testing-of-your-controls.md#customproprties)  
  
3. [Suporte à geração de código com a implementação de uma classe para propriedades personalizadas de acesso](../test/enable-coded-ui-testing-of-your-controls.md#codegeneration)  
  
4. [Suporte a ações com reconhecimento de intenção com a implementação de um filtro de ação](../test/enable-coded-ui-testing-of-your-controls.md#intentawareactions)  
  
   ![CUIT&#95;Full](../test/media/cuit-full.png "CUIT_Full")  
  
##  <a name="recordandplayback"></a> Suporte ao registro, reprodução e validação de propriedade com a implementação de acessibilidade  
 O construtor de teste de IU codificado captura informações sobre os controles que ele encontra durante uma gravação e, em seguida, gera código para repetir essa sessão. Se o controle não der suporte à acessibilidade, o teste de IU codificado capturará ações (como cliques do mouse) usando coordenadas da tela. Quando o teste é executado, o código gerado emitirá os cliques do mouse nas mesmas coordenadas de tela. Se o controle for exibido em um local diferente na tela quando o teste for reproduzido, o código gerado falhará ao executar essa ação em seu controle. Isso poderá resultar em falhas se o teste for reproduzido em diferentes configurações de tela, em diferentes ambientes ou após alterações no layout da interface do usuário.  
  
 ![CUIT&#95;RecordNoSupport](../test/media/cuit-recordnosupport.png "CUIT_RecordNoSupport")  
  
 No entanto, se você implementar acessibilidade, o construtor de teste de IU codificado usará isso para capturar as informações sobre o controle quando ele registrar um teste e gerar o código. Em seguida, quando você executar o teste, o código gerado reproduzirá esses eventos em relação ao seu controle, mesmo que ele esteja em outro lugar na interface do usuário. Os autores do teste também serão capazes de criar asserções usando as propriedades básicas do controle.  
  
 ![CUIT&#95;Record](../test/media/cuit-record.png "CUIT_Record")  
  
### <a name="to-support-record-and-playback-property-validation-and-navigation-for-a-windows-forms-control"></a>Para dar suporte à gravação e reprodução, validação de propriedade e navegação para controle do Windows Forms  
 Implemente a acessibilidade para seu controle conforme descrito no procedimento a seguir e explicado em detalhes em <xref:System.Windows.Forms.AccessibleObject>.  
  
 ![CUIT&#95;Accessible](../test/media/cuit-accessible.png "CUIT_Accessible")  
  
1.  Implemente uma classe que seja derivada de <xref:System.Windows.Forms.Control.ControlAccessibleObject> e substitua a propriedade <xref:System.Windows.Forms.Control.AccessibilityObject%2A> para retornar um objeto da sua classe.  
  
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
  
2.  Substituir o objeto acessível <xref:System.Windows.Forms.AccessibleObject.Role%2A>, <xref:System.Windows.Forms.AccessibleObject.State%2A>, <xref:System.Windows.Forms.AccessibleObject.GetChild%2A> e <xref:System.Windows.Forms.AccessibleObject.GetChildCount%2A> propriedades e métodos.  
  
3.  Implemente outro objeto de acessibilidade para o controle filho e substitua o controle de filho <xref:System.Windows.Forms.Control.AccessibilityObject%2A> propriedade para retornar esse objeto de acessibilidade.  
  
4.  Substituir a <xref:System.Windows.Forms.AccessibleObject.Bounds%2A>, <xref:System.Windows.Forms.AccessibleObject.Name%2A>, <xref:System.Windows.Forms.AccessibleObject.Parent%2A>, <xref:System.Windows.Forms.AccessibleObject.Role%2A>, <xref:System.Windows.Forms.AccessibleObject.State%2A>, <xref:System.Windows.Forms.AccessibleObject.Navigate%2A>, e <xref:System.Windows.Forms.AccessibleObject.Select%2A> propriedades e métodos para o objeto de acessibilidade do controle filho.  
  
> [!NOTE]
>  Este tópico começa com o exemplo de acessibilidade em <xref:System.Windows.Forms.AccessibleObject> neste procedimento e, em seguida, se baseia nisso nos procedimentos restantes. Se você quiser criar uma versão de trabalho do exemplo de acessibilidade, criar um aplicativo de console e, em seguida, substitua o código em Program.cs pelo código de exemplo. Você precisará adicionar referências a Acessibilidade, System.Drawing e System.Windows.Forms. Você deve alterar os **Tipos de Inserção de Interoperabilidade** de Acessibilidade para **False** para eliminar um aviso de build. Você pode alterar o tipo de saída do projeto de **Aplicativo de Console** para **Aplicativos do Windows** para que uma janela de console não apareça ao executar o aplicativo.  
  
##  <a name="customproprties"></a> Suporte à validação de propriedade personalizada com a implementação de um provedor de propriedade  
 Depois de implementar o suporte básico para registro e reprodução e validação de propriedade, você pode disponibilizar as propriedades do controle personalizado para testes de IU codificados implementando um <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider> plug-in. Por exemplo, o procedimento a seguir cria um provedor de propriedade que permite que os testes de UI codificados acessem a propriedade State dos controles filho de CurveLegend do controle do gráfico.  
  
 ![CUIT&#95;CustomProps](../test/media/cuit-customprops.png "CUIT_CustomProps")  
  
### <a name="to-support-custom-property-validation"></a>Para dar suporte à validação de propriedade personalizada  
 ![CUIT&#95;Props](../test/media/cuit-props.png "CUIT_Props")  
  
1.  Substituir o legenda do objeto acessível curva <xref:System.Windows.Forms.AccessibleObject.Description%2A> propriedade para passar valores avançados da propriedade na cadeia de caracteres de descrição, separados da descrição principal (e uns dos outros se você estiver implementando diversas propriedades) por ponto e vírgula (;).  
  
    ```csharp  
    public class CurveLegendAccessibleObject : AccessibleObject  
    {  
        // add the state property value to the description  
        public override string Description  
        {  
            get  
            {  
                // Add “;” and the state value to the end  
                // of the curve legend’s description  
                return "CurveLegend; " + State.ToString();  
            }  
        }  
    }  
    ```  
  
2.  Crie um pacote de extensão de teste de interface do usuário para o seu controle, criando um projeto de biblioteca de classes e adicionando referências a Accessibility, Microsoft.VisualStudio.TestTools.UITesting, Microsoft.VisualStudio.TestTools.UITest.Common e Microsoft.VisualStudio.TestTools.Extension. Altere os **Tipos de Inserção de Interoperabilidade** para Acessibilidade para **False**.  
  
3.  Adicionar uma classe de provedor de propriedade que é derivada de <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider>.  
  
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
  
4.  Implemente o provedor de propriedade colocando os nomes e descritores de propriedade em um <xref:System.Collections.Generic.Dictionary%602>.  
  
    ```csharp  
    // Define a map of property descriptors for CurveLegend  
    private static Dictionary<string, UITestPropertyDescriptor> curveLegendPropertiesMap = null;  
    private static Dictionary<string, UITestPropertyDescriptor> CurveLegendPropertiesMap  
    {  
        get  
        {  
            if (curveLegendPropertiesMap == null)  
            {  
                UITestPropertyAttributes read =  
                    UITestPropertyAttributes.Readable |  
                    UITestPropertyAttributes.DoNotGenerateProperties;  
                curveLegendPropertiesMap =  
                    new Dictionary<string, UITestPropertyDescriptor>  
                        (StringComparer.OrdinalIgnoreCase);  
                curveLegendPropertiesMap.Add("State",  
                    new UITestPropertyDescriptor(typeof(string), read));  
            }  
            return curveLegendPropertiesMap;  
        }  
    }  
  
    // return the property descriptor  
    public override UITestPropertyDescriptor GetPropertyDescriptor(UITestControl uiTestControl, string propertyName)  
    {  
        return CurveLegendPropertiesMap[propertyName];  
    }  
  
    // return the property names  
    public override ICollection<string> GetPropertyNames(UITestControl uiTestControl)  
    {  
        if (uiTestControl.ControlType.NameEquals("Chart") || uiTestControl.ControlType.NameEquals("Text"))  
        {  
            // the keys of the property map are the collection of property names  
            return CurveLegendPropertiesMap.Keys;  
        }  
  
        // this is not my control  
        throw new NotSupportedException();  
    }  
  
    // Get the property value by parsing the accessible description  
    public override object GetPropertyValue(UITestControl uiTestControl, string propertyName)  
    {  
        if (String.Equals(propertyName, "State", StringComparison.OrdinalIgnoreCase))  
        {  
            object[] native = uiTestControl.NativeElement as object[];  
            IAccessible acc = native[0] as IAccessible;  
  
            string[] descriptionTokens = acc.accDescription.Split(new char[] { ';' });  
            return descriptionTokens[1];  
        }  
  
        // this is not my control  
        throw new NotSupportedException();  
    }  
    ```  
  
5.  Substitua <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetControlSupportLevel%2A?displayProperty=fullName> para indicar que o assembly fornece suporte específico do controle para o controle e seus filhos.  
  
    ```csharp  
    public override int GetControlSupportLevel(UITestControl uiTestControl)  
    {  
        // For MSAA, check the control type  
        if (string.Equals(uiTestControl.TechnologyName, "MSAA",  
            StringComparison.OrdinalIgnoreCase) &&  
            (uiTestControl.ControlType == "Chart"||uiTestControl.ControlType == "Text"))  
        {  
            return (int)ControlSupport.ControlSpecificSupport;  
        }  
  
        // This is not my control, so return NoSupport  
        return (int)ControlSupport.NoSupport;  
    }  
    ```  
  
6.  Substitua os métodos abstratos restantes de <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider?displayProperty=fullName>.  
  
    ```csharp  
    public override string[] GetPredefinedSearchProperties(Type specializedClass)  
    {  
        throw new NotImplementedException();  
    }  
  
    public override Type GetSpecializedClass(UITestControl uiTestControl)  
    {  
        throw new NotImplementedException();  
    }  
  
    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)  
    {  
        throw new NotImplementedException();  
    }  
  
    public override void SetPropertyValue(UITestControl uiTestControl, string propertyName, object value)  
    {  
        throw new NotImplementedException();  
    }  
  
    public override string GetPropertyForAction(UITestControl uiTestControl, UITestAction action)  
    {  
        throw new NotImplementedException();  
    }  
  
    public override string[] GetPropertyForControlState(UITestControl uiTestControl, ControlStates uiState, out bool[] stateValues)  
    {  
        throw new NotImplementedException();  
    }  
  
    ```  
  
7.  Adicione uma classe de pacote de extensão que é derivada de <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>.  
  
    ```csharp  
    using System;  
    using Microsoft.VisualStudio.TestTools.UITesting;  
    using Microsoft.VisualStudio.TestTools.UITest.Extension;  
    using Microsoft.VisualStudio.TestTools.UITest.Common;  
  
    namespace ChartControlExtensionPackage  
    {  
        internal class ChartControlExtensionPackage : UITestExtensionPackage  
        {  
        }  
    }  
    ```  
  
8.  Defina o atributo `UITestExtensionPackage` do assembly.  
  
    ```csharp  
    [assembly: Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage(  
                    "ChartControlExtensionPackage",  
                    typeof(ChartControlExtensionPackage.ChartControlExtensionPackage))]  
    namespace ChartControlExtensionPackage  
    {  
       …  
    ```  
  
9. Na classe de pacote de extensão, substitua <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A?displayProperty=fullName> para retornar a classe do provedor de propriedade quando um provedor de propriedade for solicitado.  
  
    ```csharp  
    internal class ChartControlExtensionPackage : UITestExtensionPackage  
    {  
        public override object GetService(Type serviceType)  
        {  
            if (serviceType == typeof(UITestPropertyProvider))  
            {  
                if (propertyProvider == null)  
                {  
                    propertyProvider = new ChartControlPropertyProvider();  
                }  
                return propertyProvider;  
            }  
            return null;  
        }  
  
        private UITestPropertyProvider propertyProvider = null;  
    }  
    ```  
  
10. Substitua as propriedades e os métodos abstratos restantes de <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage>.  
  
    ```csharp  
  
    public override void Dispose() { }  
  
    public override string PackageDescription  
    {  
        get { return "Supports coded UI testing of ChartControl"; }  
    }  
  
    public override string PackageName  
    {  
        get { return "ChartControl Test Extension"; }  
    }  
  
    public override string PackageVendor  
    {  
        get { return "Microsoft (sample)"; }  
    }  
  
    public override Version PackageVersion  
    {  
        get { return new Version(1, 0); }  
    }  
  
    public override Version VSVersion  
    {  
        get { return new Version(10, 0); }  
    }  
    ```  
  
11. Compile seus binários e copie-os para **%ProgramFiles%\Common\Microsoft Shared\VSTT\10.0\UITestExtensionPackages**.  
  
> [!NOTE]
>  Este pacote de extensão será aplicado a qualquer controle do tipo “Text”. Se você estiver testando vários controles do mesmo tipo, precisará testá-los separadamente e gerenciar quais pacotes de extensão são implantadas ao gravar os testes.  
  
##  <a name="codegeneration"></a> Suporte à geração de código com a implementação de uma classe para propriedades personalizadas de acesso  
 Quando o construtor de teste de IU codificado gera código de uma gravação de sessão, ele usa a classe <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestControl> para acessar os controles.  
  
```csharp  
  
      UITestControl uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;  
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.GetProperty("State").ToString());  
```  
  
 Se você já implementou um provedor de propriedade para conceder acesso às propriedades personalizadas do controle, poderá adicionar uma classe especializada que é usada para acessar essas propriedades para que o código gerado seja simplificado.  
  
```csharp  
  
      ControlLegend uIAText = this.UIItemWindow.UIChartControlWindow.UIAText;  
Assert.AreEqual(this.AssertMethod3ExpectedValues.UIATextState, uIAText.State);  
```  
  
### <a name="to-add-a-specialized-class-to-access-your-control"></a>Para adicionar uma classe especializada para acessar seu controle  
 ![CUIT&#95;CodeGen](../test/media/cuit-codegen.png "CUIT_CodeGen")  
  
1.  Implemente uma classe que é derivada de <xref:Microsoft.VisualStudio.TestTools.UITesting.WinControls.WinControl> e adicione o tipo do controle à coleção de propriedades de pesquisa no construtor.  
  
    ```csharp  
    public class CurveLegend:WinControl   
    {  
       public CurveLegend(UITestControl c) : base(c)   
       {  
          // The curve legend control is a “text” type of control  
          SearchProperties.Add(  
             UITestControl.PropertyNames.ControlType, "Text");  
       }  
    }  
    ```  
  
2.  Implemente as propriedades personalizadas do controle como propriedades da classe.  
  
    ```csharp  
    public virtual string State  
    {  
        get  
        {  
            return (string)GetProperty("State");  
        }  
    }  
    ```  
  
3.  Substitua o seu provedor de propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetSpecializedClass%2A?displayProperty=fullName> método para retornar o tipo da nova classe para a curva de controles filho de legenda.  
  
    ```csharp  
    public override Type GetSpecializedClass(UITestControl uiTestControl)   
    {   
       if (uiTestControl.ControlType.NameEquals("Text"))   
       {   
          // This is text type of control. For my control,  
          // that means it’s a curve legend control.  
          return typeof(CurveLegend);   
       }   
  
       // this is not a curve legend control  
       return null;  
    }  
    ```  
  
4.  Substitua o seu provedor de propriedade <xref:Microsoft.VisualStudio.TestTools.UITesting.UITestPropertyProvider.GetPropertyNamesClassType%2A> método para retornar o tipo PropertyNames método da nova classe.  
  
    ```csharp  
    public override Type GetPropertyNamesClassType(UITestControl uiTestControl)  
    {  
        if (uiTestControl.ControlType.NameEquals("Text"))  
        {  
          // This is text type of control. For my control,  
          // that means it’s a curve legend control.  
            return typeof(CurveLegend.PropertyNames);  
        }  
  
        // this is not a curve legend control  
        return null;  
    }  
    ```  
  
##  <a name="intentawareactions"></a> Suporte a ações com reconhecimento de intenção com a implementação de um filtro de ação  
 Quando o Visual Studio registra um teste, ele captura cada evento do mouse e do teclado. No entanto, em alguns casos, a intenção da ação pode ser perdida na série de eventos de mouse e de teclado. Por exemplo, se o controle dá suporte ao preenchimento automático, o mesmo conjunto de eventos de mouse e teclado podem resultar em um valor diferente quando o teste é reproduzido em um ambiente diferente. Você pode adicionar um plug-in de filtro de ação que substitui a série de eventos de teclado e mouse por uma única ação. Dessa forma, você pode substituir a série de eventos de mouse e de teclado, resultando na seleção de um valor com uma única ação que define o valor. Isso protege os testes de UI codificados contra as diferenças no preenchimento automático de um ambiente para outro.  
  
### <a name="to-support-intent-aware-actions"></a>Para dar suporte a ações com reconhecimento de intenção  
 ![CUIT&#95;Actions](../test/media/cuit-actions.png "CUIT_Actions")  
  
1.  Implementar uma classe de filtro de ação que é derivada de <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter>, substituindo as propriedades <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.ApplyTimeout%2A>, <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.Category%2A>, <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.Enabled%2A>, <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.FilterType%2A>, <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.Group%2A> e <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.Name%2A>.  
  
    ```csharp  
    internal class MyActionFilter : UITestActionFilter  
    {  
       // If the user actions we are aggregating exceeds the time allowed,  
       // this filter is not applied. (The timeout is configured when the  
       // test is run.)  
       public override bool ApplyTimeout  
       {  
          get { return true; }  
       }  
  
       // Gets the category of this filter. Categories of filters  
       // are applied in priority order.  
       public override UITestActionFilterCategory Category  
       {  
          get { return UITestActionFilterCategory.PostSimpleToCompoundActionConversion; }  
       }  
  
       public override bool Enabled  
       {  
          get { return true; }  
       }  
  
       public override UITestActionFilterType FilterType  
       {  
          // This action filter operates on a single action  
          get { return UITestActionFilterType.Unary; }  
       }  
  
       // Gets the name of the group to which this filter belongs.  
       // A group can be enabled/disabled using configuration file.  
       public override string Group  
       {  
          get { return "ChartControlActionFilters"; }  
       }  
  
       // Gets the name of this filter.  
       public override string Name  
       {  
          get { return "Convert Double-Click to Single-Click"; }  
       }  
    ```  
  
2.  Substitua <xref:Microsoft.VisualStudio.TestTools.UITest.Common.UITestActionFilter.ProcessRule%2A>. Esse exemplo substitui uma ação de clicar duas vezes por uma ação de clique único.  
  
    ```csharp  
    public override bool ProcessRule(IUITestActionStack actionStack)  
    {  
        if (actionStack.Count > 0)  
        {  
            MouseAction lastAction = actionStack.Peek() as MouseAction;  
            if (lastAction != null)  
            {  
                if (lastAction.UIElement.ControlTypeName.Equals(  
                     ControlType.Text.ToString(),  
                     StringComparison.OrdinalIgnoreCase))  
                {  
                    if(lastAction.ActionType == MouseActionType.DoubleClick)  
                    {  
                        // Convert to single click  
                        lastAction.ActionType = MouseActionType.Click;  
                    }  
                }  
            }  
        }  
        // Do not stop aggregation  
        return false;  
    }  
    ```  
  
3.  Adicione o filtro de ação ao método <xref:Microsoft.VisualStudio.TestTools.UITest.Extension.UITestExtensionPackage.GetService%2A> do seu pacote de extensão.  
  
    ```csharp  
    public override object GetService(Type serviceType)   
    {   
       if (serviceType == typeof(UITestPropertyProvider))   
       {   
          if (propertyProvider == null)  
          {  
             propertyProvider = new PropertyProvider();  
          }   
          return propertyProvider;  
       }   
       else if (serviceType == typeof(UITestActionFilter))   
       {   
          if (actionFilter == null)  
          {  
             actionFilter = new RadGridViewActionFilter();  
          }  
          return actionFilter;   
       }   
       return null;  
    }  
    ```  
  
4.  Compile seus binários e copie-os para %ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages.  
  
> [!NOTE]
>  O filtro de ação não depende da implementação de acessibilidade ou do provedor de propriedade.  
  
## <a name="debug-your-property-provider-or-action-filter"></a>Depurar seu provedor de propriedade ou filtro de ação  
 O provedor de propriedade e filtro de ação são implementados em um pacote de extensão que é carregado e executado pelo construtor de teste de IU codificado em um processo separado do seu aplicativo.  
  
#### <a name="to-debug-your-property-provider-or-action-filter"></a>Para depurar seu provedor de propriedade ou filtro de ação  
  
1.  Compile a versão de depuração do seu pacote de extensão e copie os arquivos .dll e .pdb para %ProgramFiles%\Common Files\Microsoft Shared\VSTT\10.0\UITestExtensionPackages.  
  
2.  Execute seu aplicativo (não no depurador).  
  
3.  Execute o construtor de teste de IU codificado.  
  
     `codedUITestBuilder.exe  /standalone`  
  
4.  Anexe o depurador ao processo codedUITestBuilder.  
  
5.  Defina os pontos de interrupção no seu código.  
  
6.  No construtor de teste de IU codificado, crie asserções para exercitar seu provedor de propriedade e registrar ações para exercitar seus filtros de ação.  
  
## <a name="external-resources"></a>Recursos externos  
  
### <a name="guidance"></a>Diretrizes  
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](http://go.microsoft.com/fwlink/?LinkID=255188)  
  
## <a name="see-also"></a>Consulte também  
 <xref:System.Windows.Forms.AccessibleObject>   
 [Usar automação de interface do usuário para testar código](../test/use-ui-automation-to-test-your-code.md)



