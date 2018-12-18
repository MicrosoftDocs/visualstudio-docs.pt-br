---
title: Definir uma propriedade de automação exclusiva para controles da Windows Store para teste | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9bdd74ff-2534-4fc7-a5c3-a77bf7843037
caps.latest.revision: 12
ms.author: gewarren
manager: douge
ms.openlocfilehash: 25890adaf22d1855426813c35e69766bba02a1c8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833922"
---
# <a name="set-a-unique-automation-property-for-windows-store-controls-for-testing"></a>Definir uma propriedade de automação exclusiva para controles da Windows Store para teste
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se desejar executar testes de IU codificados no aplicativo da Windows Store baseado em XAML, será necessário ter uma propriedade de automação exclusiva que identifica cada controle.  
  
 Você pode atribuir uma propriedade de automação exclusiva com base no tipo de controle XAML em seu aplicativo. Aqui está como atribuir essa propriedade de automação exclusiva nas seguintes situações:  
  
-   [Definição XAML estática de controles](#UniquePropertyWindowsStoreControlsStaticXAML)  
  
-   [Atribuir propriedades de automação exclusiva usando o Visual Studio ou o Blend for Visual Studio](#UniquePropertyWindowsStoreControlsExpressionBlend)  
  
-   [Usar um DataTemplate](#UniquePropertyWindowsStoreControlsDataTemplate)  
  
-   [Usar um modelo de controle](#UniquePropertyWindowsStoreControlsControlTemplate)  
  
-   [Controles dinâmicos](#UniquePropertyWindowsStoreControlsDynamicControls)  
  
## <a name="use-methods-to-assign-a-unique-automation-property"></a>Usar métodos para atribuir uma propriedade de automação exclusiva  
  
###  <a name="UniquePropertyWindowsStoreControlsStaticXAML"></a> Definição XAML estática  
 Para especificar uma propriedade de automação exclusiva para um controle que é definido no arquivo XAML, você pode definir o AutomationProperties.AutomationId ou o AutomationProperties.Name implicitamente ou explicitamente, conforme mostrado nos exemplos a seguir. Configurar qualquer um desses valores dá ao controle uma propriedade de automação exclusiva que pode ser usada para identificar o controle ao criar uma gravação da ação ou teste de IU codificado.  
  
 **Definir a propriedade implicitamente**  
  
 Defina o AutomationProperties.AutomationId como **ButtonX** usando a propriedade Name no XAML para o controle.  
  
```xaml  
<Button Name="ButtonX" Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />  
  
```  
  
 Defina o AutomationProperties.Name como **ButtonY** usando a propriedade Content no XAML para o controle.  
  
```xaml  
<Button Content="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />  
  
```  
  
 **Definir a propriedade explicitamente**  
  
 Defina o AutomationProperties.AutomationId como **ButtonX** explicitamente no XAML para o controle.  
  
```xaml  
<Button AutomationProperties.AutomationId=“ButtonX” Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />  
  
```  
  
 Defina o AutomationProperties.Name como **ButtonY** explicitamente no XAML para o controle.  
  
```  
<Button AutomationProperties.Name="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />  
```  
  
###  <a name="UniquePropertyWindowsStoreControlsExpressionBlend"></a> Atribuir propriedades de automação exclusiva usando o Visual Studio ou o Blend for Visual Studio  
 Você pode usar o Visual Studio ou o Blend for Visual Studio para atribuir nomes exclusivos para elementos interativos, como botões, caixas de listagem, caixas de combinação e caixas de texto. Isso dá ao controle um valor exclusivo para AutomationProperties.Name.  
  
 **Visual Studio:** no menu **Ferramentas**, aponte para **Opções** e escolha **Editor de Texto**, **XAML** e **Diversos**.  
  
 Selecione **Nomear Automaticamente Elementos Interativos na Criação** e selecione **OK**.  
  
 ![Opções diversas de XAML](../test/media/cuit-windowsstoreapp-b.png "CUIT_WindowsStoreApp_B")  
  
 **Blend for Visual Studio:** use um dos seguintes métodos para fazer isso no Blend for Visual Studio.  
  
> [!NOTE]
>  Você somente pode usar esse método para controles que são criados estaticamente usando XAML.  
  
 **Como fornecer um nome exclusivo para controles existentes**  
  
 No menu **Ferramentas**, escolha **Elementos Interativos do Nome**, conforme mostrado aqui:  
  
 ![Escolha Nomes de Elementos Interativos no menu Ferramentas](../test/media/cuit-windowsstoreproperty-blend-1.png "CUIT_WindowsStoreProperty_Blend_1")  
  
 **Como atribuir automaticamente um nome exclusivo aos controles que você criou**  
  
 No menu **Ferramentas**, aponte para **Opções** e escolha **Projeto**. Selecione **Nomear Automaticamente Elementos Interativos na Criação** e selecione **OK**, como mostrado aqui:  
  
 ![Defina o projeto para nomear elementos interativos](../test/media/cuit-windowsstoreproeprty-blend-2.png "CUIT_WindowsStoreProeprty_Blend_2")  
  
###  <a name="UniquePropertyWindowsStoreControlsDataTemplate"></a> Usar um modelo de dados  
 Você pode definir um modelo simples usando o ItemTemplate para associar os valores em uma caixa de listagem para variáveis usando o XAML a seguir.  
  
```xaml  
  
<ListBox Name="listBox1" ItemsSource="{Binding Source={StaticResource employees}}">  
   <ListBox.ItemTemplate>  
      <DataTemplate>  
         <StackPanel Orientation="Horizontal">  
            <TextBlock Text="{Binding EmployeeName}" />  
            <TextBlock Text="{Binding EmployeeID}" />  
         </StackPanel>  
      </DataTemplate>  
   </ListBox.ItemTemplate>  
</ListBox>  
```  
  
 Você também pode usar um modelo com ItemContainerStyle para associar os valores a variáveis usando o XAML a seguir.  
  
```xaml  
  
      <ListBox Name="listBox1" ItemsSource="{Binding Source={StaticResource employees}}">  
            <ListBox.ItemContainerStyle>  
                <Style TargetType="ListBoxItem">  
                    <Setter Property="Template">  
                        <Setter.Value>  
                            <ControlTemplate TargetType="ListBoxItem">  
                                <Grid>  
                                    <Button Content="{Binding EmployeeName}" AutomationProperties.AutomationId="{Binding EmployeeID}"/>  
                                </Grid>  
                            </ControlTemplate>  
                        </Setter.Value>  
                    </Setter>  
                </Style>  
            </ListBox.ItemContainerStyle>           
        </ListBox>  
  
```  
  
 Para ambos os exemplos, você deve, em seguida, substituir o método ToString() do ItemSource, conforme mostrado, usando o código a seguir. Esse código verifica se o valor de AutomationProperties.Name é definido e é exclusivo, porque você não pode definir uma propriedade de automação exclusiva para cada item de lista vinculada de dados usando a associação. Configurar um valor exclusivo para a automação Properties.Name nesse caso é suficiente.  
  
> [!NOTE]
>  Usando essa abordagem, o conteúdo interno do item de lista também pode ser definido para uma cadeia de caracteres na classe Employee por meio da associação. Conforme mostrado no exemplo, o controle de botão dentro de cada item de lista tem uma ID de automação exclusiva atribuída, que é a ID do funcionário.  
  
```  
  
Employee[] employees = new Employee[]   
{  
   new Employee("john", "4384"),  
   new Employee("margaret", "7556"),  
   new Employee("richard", "8688"),  
   new Employee("george", "1293")  
};  
  
listBox1.ItemsSource = employees;  
  
public override string ToString()  
{  
    return EmployeeName + EmployeeID; // Unique Identification to be set as the AutomationProperties.Name  
}  
  
```  
  
###  <a name="UniquePropertyWindowsStoreControlsControlTemplate"></a> Usar um modelo de controle  
 Você pode usar um modelo de controle para que cada instância de um tipo específico obtenha uma propriedade de automação exclusiva quando ela for definida no código. Você deve criar o modelo para que o AutomationProperty seja associado a uma ID exclusiva na instância do controle. O XAML a seguir demonstra uma abordagem para criar essa associação com um modelo de controle.  
  
```xaml  
  
<Style x:Key="MyButton" TargetType="Button">  
<Setter Property="Template">  
   <Setter.Value>  
<ControlTemplate TargetType="Button">  
   <Grid>  
      <CheckBox HorizontalAlignment="Left" AutomationProperties.AutomationId="{TemplateBinding Content}"></CheckBox>  
      <Button Width="90" HorizontalAlignment="Right" Content="{TemplateBinding Content}" AutomationProperties.AutomationId="{TemplateBinding Content}"></Button>  
   </Grid>  
</ControlTemplate>  
   </Setter.Value>  
</Setter>  
</Style>  
  
```  
  
 Quando você define duas instâncias de um botão usando esse modelo de controle, a ID de automação é definida como a cadeia de caracteres de conteúdo exclusiva para os controles no modelo, como mostra o XAML a seguir.  
  
```xaml  
  
<Button Content=”Button1” Style="{StaticResource MyButton}" Width="140"/>  
<Button Content=”Button2” Style="{StaticResource MyButton}" Width="140"/>  
```  
  
###  <a name="UniquePropertyWindowsStoreControlsDynamicControls"></a> Controles dinâmicos  
 Se tiver controles que são criados dinamicamente do código e não criados estaticamente ou por meio de modelos em arquivos XAML, você deverá definir as propriedades Content ou Name para o controle. Isso garante que cada controle dinâmico tenha uma propriedade de automação exclusiva. Por exemplo, se houver uma caixa de seleção que deve ser exibida quando você seleciona um item de lista, você poderá definir essas propriedades, como mostrado aqui:  
  
```csharp  
  
private void CreateCheckBox(string txt, StackPanel panel)  
   {  
      CheckBox cb = new CheckBox();  
      cb.Content = txt; // Sets the AutomationProperties.Name  
      cb.Height = 50;  
      cb.Width = 100;  
      cb.Name = "DynamicCheckBoxAid"+ txt; // Sets the AutomationProperties.AutomationId  
      panel.Children.Add(cb);  
    }  
  
```  




