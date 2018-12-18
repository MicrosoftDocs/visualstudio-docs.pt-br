---
title: Definir uma propriedade de automação exclusiva para controles UWP para teste
ms.date: 05/31/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
ms.author: gewarren
manager: douge
ms.workload:
- uwp
author: gewarren
ms.openlocfilehash: 1cc8986c3101bb2048e0cd4ace739974031344ed
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52894775"
---
# <a name="set-a-unique-automation-property-for-uwp-controls-for-testing"></a>Definir uma propriedade de automação exclusiva para controles UWP para teste

Se desejar executar testes de interface do usuário codificados no aplicativo UWP baseado em XAML, cada controle deverá ser identificado por uma propriedade de automação exclusiva. Você pode atribuir uma propriedade de automação exclusiva com base no tipo de controle XAML em seu aplicativo.

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

## <a name="static-xaml-definition"></a>Definição XAML estática

Para especificar uma propriedade de automação exclusiva para um controle definido no arquivo XAML, é possível definir **AutomationProperties.AutomationId** ou **AutomationProperties.Name** implícita ou explicitamente, conforme mostrado nos exemplos a seguir. Configurar qualquer um desses valores dá ao controle uma propriedade de automação exclusiva que pode ser usada para identificar o controle ao criar uma gravação da ação ou teste de IU codificado.

### <a name="set-the-property-implicitly"></a>Definir a propriedade implicitamente

Defina **AutomationProperties.AutomationId** como **ButtonX** usando a propriedade **Name** no XAML do controle.

```xaml
<Button Name="ButtonX" Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />
```

Defina **AutomationProperties.Name** como **ButtonY** usando a propriedade **Content** no XAML do controle.

```xaml
<Button Content="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />
```

### <a name="set-the-property-explicitly"></a>Definir a propriedade explicitamente

Defina **AutomationProperties.AutomationId** como **ButtonX** explicitamente no XAML do controle.

```xaml
<Button AutomationProperties.AutomationId="ButtonX" Height="31" HorizontalAlignment="Left" Margin="23,26,0,0"  VerticalAlignment="Top" Width="140" Click="ButtonX_Click" />
```

Defina **AutomationProperties.Name** como **ButtonY** explicitamente no XAML do controle.

```xaml
<Button AutomationProperties.Name="ButtonY" Height="31" HorizontalAlignment="Left" Margin="23,76,0,0" VerticalAlignment="Top" Width="140" Click="ButtonY_Click" />
```

## <a name="assign-unique-names"></a>Atribuir nomes exclusivos

No Blend para Visual Studio, selecione uma opção para atribuir nomes exclusivos a elementos interativos como botões, caixas de listagem, caixas de combinação e caixas de texto, que fornece aos controles valores exclusivos para **AutomationProperties.Name**.

Para atribuir nomes exclusivos a controles existentes, selecione **Ferramentas** > **Nomear elementos interativos**.

![Nomear elementos interativos no Blend para Visual Studio](../test/media/cuit_windowsstoreproperty_blend_1.png)

Para dar nomes exclusivos automaticamente a novos controles adicionados, selecione **Ferramentas** > **Opções** para abrir a caixa de diálogo **Opções**. Selecione **Designer XAML** e **Nomear automaticamente elementos interativos na criação**. Selecione **OK** para fechar a caixa de diálogo.

## <a name="use-a-data-template"></a>Usar um modelo de dados

É possível definir um modelo simples usando **ItemTemplate** para associar os valores em uma caixa de listagem para variáveis:

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

Também é possível usar um modelo com **ItemContainerStyle** para associar os valores a variáveis:

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

Para ambos os exemplos, é necessário substituir o método **ToString()** de **ItemSource**, conforme mostrado usando o exemplo de código a seguir. Esse código verifica se o valor **AutomationProperties.Name** é definido e é exclusivo, porque não é possível definir uma propriedade de automação exclusiva para cada item de lista associado de dados usando a associação. Configurar um valor exclusivo para a **Automação Properties.Name** nesse caso é suficiente.

> [!NOTE]
> Usando essa abordagem, o conteúdo interno do item de lista também pode ser definido para uma cadeia de caracteres na classe Employee por meio da associação. Conforme mostrado no exemplo, o controle de botão dentro de cada item de lista tem uma ID de automação exclusiva atribuída, que é a ID do funcionário.

```csharp
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

## <a name="use-a-control-template"></a>Usar um modelo de controle

Você pode usar um modelo de controle para que cada instância de um tipo específico obtenha uma propriedade de automação exclusiva quando ela for definida no código. Crie o modelo para que **AutomationProperty** associe-se a uma ID exclusiva na instância do controle. O XAML a seguir demonstra uma abordagem para criar essa associação com um modelo de controle:

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

Quando você define duas instâncias de um botão usando esse modelo de controle, a ID de automação é definida como a cadeia de caracteres de conteúdo exclusivo para os controles no modelo, como mostra o seguinte XAML:

```xaml
<Button Content="Button1" Style="{StaticResource MyButton}" Width="140"/>
<Button Content="Button2" Style="{StaticResource MyButton}" Width="140"/>
```

### <a name="dynamic-controls"></a>Controles dinâmicos

Se tiver controles criados dinamicamente do código e não criados estaticamente ou por meio de modelos em arquivos XAML, será necessário definir as propriedades **Content** ou **Name** para o controle. Essa ação garante que cada controle dinâmico tenha uma propriedade de automação exclusiva. Por exemplo, se houver uma caixa de seleção que deve ser exibida quando você seleciona um item de lista, você poderá definir essas propriedades, como mostrado aqui:

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

## <a name="see-also"></a>Consulte também

- [Testar aplicativos UWP com testes de IU codificados](../test/test-uwp-app-with-coded-ui-test.md)
