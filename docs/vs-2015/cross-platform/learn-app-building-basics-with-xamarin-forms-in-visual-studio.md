---
title: Aprenda noções básicas de criação de aplicativos com o xamarin. Forms
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d22b5186-9e03-4e85-afc9-7cbe28522a6d
caps.latest.revision: 14
ms.author: crdun
manager: crdun
ms.openlocfilehash: 0cbc20bd714cabf9747145c114abfaa58a2e52a6
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53058318"
---
# <a name="learn-app-building-basics-with-xamarinforms-in-visual-studio"></a>Aprender as noções básicas de criação de aplicativos com o Xamarin.Forms no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


Após você concluir as etapas em [Configuração e instalação](../cross-platform/setup-and-install.md) e em [Verificar seu ambiente Xamarin](../cross-platform/verify-your-xamarin-environment.md), este passo a passo mostra como criar um aplicativo básico (mostrado abaixo) com Xamarin.Forms. Com o Xamarin.Forms, você escreverá todo o código da interface do usuário uma vez em uma PCL (biblioteca de classes portátil). O Xamarin, então, renderizará automaticamente os controles de interface do usuário nativos para as plataformas iOS, Android e Windows. Recomendamos essa abordagem porque a opção da PCL dá melhor suporte ao uso apenas das APIs do .NET que têm suporte em todas as plataformas de destino, e porque o Xamarin.Forms permite compartilhar o código da interface do usuário entre plataformas.

 ![Exemplo de Aplicativo Meteorológico em iOS, Android e Windows Phone](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin FormsGuide 1")

 Você executará as seguintes ações para compilar:

-   [Configurar sua solução](#solution)

-   [Escrever código de serviço de dados compartilhado](#dataservice)

-   [Começar a escrever código de interface do usuário compartilhado](#uicode)

-   [Testar seu aplicativo usando o Emulador do Visual Studio para Android](#test)

-   [Concluir a interface do usuário com uma aparência nativa entre plataformas](#finish)

> [!TIP]
>  Você pode encontrar o código-fonte completo desse projeto no [repositório xamarin-forms-samples no GitHub](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather).

##  <a name="solution"></a> Configurar sua solução
 Estas etapas criam uma solução do Xamarin.Forms que contém uma PCL para o código compartilhado e dois pacotes NuGet adicionados.

1.  No Visual Studio, crie uma nova solução de **Aplicativo em Branco (Portátil do Xamarin.Forms)** e dê a ela o nome de **WeatherApp**. Você pode localizar esse modelo mais facilmente digitando **Xamarin.Forms** no campo de pesquisa.

     Se não estiver lá, talvez você precise instalar o Xamarin ou habilitar o recurso do Visual Studio 2015, consulte [Configuração e instalação](../cross-platform/setup-and-install.md).

     ![Criando um novo projeto de aplicativo em branco &#40;portátil do Xamarin.Forms&#41;](../cross-platform/media/crossplat-xamarin-formsguide-2.png "CrossPlat Xamarin FormsGuide 2")

2.  Depois de clicar em OK para criar a solução, você terá vários projetos individuais:

    -   **WeatherApp (Portátil)**: a PCL em que você escreverá o código que é compartilhado entre plataformas, incluindo lógica de negócios comum e código de interface do usuário com Xamarin.Forms.

    -   **WeatherApp.Droid**: o projeto que contém o código nativo do Android. É definido como o projeto de inicialização padrão.

    -   **WeatherApp.iOS**: o projeto que contém o código iOS nativo.

    -   **WeatherApp.UWP**: o projeto que contém o código da UWP do Windows 10.

    -   **WeatherApp.Windows (Windows 8.1)**: o projeto que contém o código nativo do Windows 8.1.

    -   **WeatherApp.WinPhone (Windows Phone 8.1)**: o projeto que contém o código nativo do Windows Phone.

    > [!NOTE]
    >  Você tem a liberdade de excluir qualquer um dos projetos que for relativo a uma plataforma que não for de seu interesse. Para os fins deste passo a passo, faremos referência aos projetos do Android, iOS e Windows Phone 8.1. Trabalhar com os projetos da UWP e do Windows 8.1 é muito semelhante a trabalhar com o projeto do Windows Phone 8.1.

     Dentro de cada projeto nativo, você tem acesso ao designer nativo da plataforma correspondente e pode implementar telas e funcionalidades específicas da plataforma, conforme necessário.

3.  Atualize o pacote do NuGet do Xamarin.Forms em sua solução para a versão estável mais recente da seguinte maneira. Recomendamos faze isso sempre que você criar uma nova solução do Xamarin:

    -   Selecione **Ferramentas > Gerenciador de Pacotes do NuGet > Gerenciar Pacotes do NuGet para a Solução**.

    -   Na guia **Atualizações**, marque a atualização do **Xamarin.Forms** e marque para atualizar todos os projetos na solução. (Observação: deixe atualizações de Xamarin.Android.Support desmarcadas.)

    -   Atualize o campo **Versão** para a versão **Estável mais recente** disponível.

    -   Clique em **Atualizar**.

         ![Atualizando o pacote do NuGet do Xamarin.Forms](../cross-platform/media/crossplat-xamarin-formsguide-4.png "CrossPlat Xamarin FormsGuide 4")

4.  Adicione o pacote **Newtonsoft.Json** e o pacote NuGet ao projeto PCL, que você usará para processar as informações recuperadas de um serviço de dados de clima:

    -   No Gerenciador de Pacotes do NuGet (ainda aberto da etapa 3), selecione a guia **Procurar** e pesquise **Newtonsoft**.

    -   Selecione **Newtonsoft.Json**.

    -   Marque o projeto **WeatherApp** (esse é o projeto único no qual você precisa instalar o pacote).

    -   Verifique se o campo **Versão** está definido como a versão **Estável mais recente**.

    -   Clique em **Instalar**.

    -   ![Localizando e instalando o pacote do NuGet Newtonsoft.Json](../cross-platform/media/crossplat-xamarin-formsguide-5.png "CrossPlat Xamarin FormsGuide 5")

5.  Repita a etapa 4 para localizar e instalar o pacote **Microsoft.Net.Http**.

6.  Compile sua solução e verifique não se há erros de build.

##  <a name="dataservice"></a> Escrever código de serviço de dados compartilhados
 É no projeto **WeatherApp (Portátil)** que você escreverá código para a PCL (biblioteca de classes portátil) que será compartilhado entre todas as plataformas. A PCL é incluída automaticamente nos pacotes de aplicativo compilados pelos projetos de iOS, Android e Windows Phone.

 Para executar este exemplo, primeiro você precisa se inscrever para obter uma chave de API gratuita em [http://openweathermap.org/appid](http://openweathermap.org/appid).

 As etapas a seguir adicionam o código à PCL para acessar e armazenar dados do serviço meteorológico:

1.  Clique com botão direito do mouse no projeto **WeatherApp** e selecione **Adicionar > Classe…**. Na caixa de diálogo **Adicionar Novo Item**, dê ao arquivo o nome **Weather.cs**. Você usará essa classe para armazenar dados do serviço de dados de clima.

2.  Substitua todo o conteúdo de **Weather.cs** pelo seguinte:

    ```csharp
    namespace WeatherApp
    {
        public class Weather
        {
            public string Title { get; set; }
            public string Temperature { get; set; }
            public string Wind { get; set; }
            public string Humidity { get; set; }
            public string Visibility { get; set; }
            public string Sunrise { get; set; }
            public string Sunset { get; set; }

            public Weather()
            {
                //Because labels bind to these values, set them to an empty string to
                //ensure that the label appears on all platforms by default.
                this.Title = " ";
                this.Temperature = " ";
                this.Wind = " ";
                this.Humidity = " ";
                this.Visibility = " ";
                this.Sunrise = " ";
                this.Sunset = " ";
            }
        }
    }
    ```

3.  Adicione outra classe ao projeto PCL chamada **DataService.cs** em que você usará para processar dados JSON do serviço de dados de clima.

4.  Substitua todo o conteúdo de **DataService.cs** pelo código a seguir:

    ```csharp
    using System.Threading.Tasks;
    using Newtonsoft.Json;
    using System.Net.Http;

    namespace WeatherApp
    {
        public class DataService
        {
            public static async Task<dynamic> getDataFromService(string queryString)
            {
                HttpClient client = new HttpClient();
                var response = await client.GetAsync(queryString);

                dynamic data = null;
                if (response != null)
                {
                    string json = response.Content.ReadAsStringAsync().Result;
                    data = JsonConvert.DeserializeObject(json);
                }

                return data;
            }
        }
    }
    ```

5.  Adicione uma terceira classe à PCL chamada **Core**, na qual você colocará a lógica de negócios compartilhada, como a lógica que forma uma cadeia de caracteres de consulta com um CEP, chama o serviço de dados de clima e preenche uma instância da classe **Clima**.

6.  Substitua o conteúdo de **Core.cs** pelo seguinte:

    ```csharp
    using System;
    using System.Threading.Tasks;

    namespace WeatherApp
    {
        public class Core
        {
            public static async Task<Weather> GetWeather(string zipCode)
            {
                //Sign up for a free API key at http://openweathermap.org/appid
                string key = "YOUR KEY HERE";
                string queryString = "http://api.openweathermap.org/data/2.5/weather?zip="
                    + zipCode + ",us&appid=" + key + "&units=imperial";

                dynamic results = await DataService.getDataFromService(queryString).ConfigureAwait(false);

                if (results["weather"] != null)
                {
                    Weather weather = new Weather();
                    weather.Title = (string)results["name"];
                    weather.Temperature = (string)results["main"]["temp"] + " F";
                    weather.Wind = (string)results["wind"]["speed"] + " mph";
                    weather.Humidity = (string)results["main"]["humidity"] + " %";
                    weather.Visibility = (string)results["weather"][0]["main"];

                    DateTime time = new System.DateTime(1970, 1, 1, 0, 0, 0, 0);
                    DateTime sunrise = time.AddSeconds((double)results["sys"]["sunrise"]);
                    DateTime sunset = time.AddSeconds((double)results["sys"]["sunset"]);
                    weather.Sunrise = sunrise.ToString() + " UTC";
                    weather.Sunset = sunset.ToString() + " UTC";
                    return weather;
                }
                else
                {
                    return null;
                }
            }
        }
    }
    ```

7.  Compile o projeto da PCL **WeatherApp** para garantir que o código esteja correto.

##  <a name="uicode"></a> Começar a escrever código de interface do usuário compartilhado
 O Xamarin.Forms permite implementar código da interface do usuário compartilhado na PCL. Nessas etapas, você adicionará uma tela à PCL com um botão que atualiza seu texto com os dados retornados pelo código do serviço de dados meteorológicos adicionado na seção anterior:

1.  Adicione uma **Página Xaml do Forms** chamada **WeatherPage.cs** clicando com o botão direito do mouse no projeto **WeatherApp** e selecionando **Adicionar > Novo Item...**. Na caixa de diálogo **Adicionar Novo Item**, pesquisa em "Forms", selecione **Página Xaml do Forms** e nomeie-a **WeatherPage.cs**.

     O Xamarin.Forms é baseado em XAML, de forma que esta etapa cria um arquivo **WeatherPage.xaml** em conjunto com o arquivo code-behind aninhado **WeatherPage.xaml.cs**. Isso permite gerar a interface do usuário por meio de XAML ou código. Você fará um pouco dos dois neste passo a passo.

     ![Adicionando uma nova página XAML do Xamarin.Forms](../cross-platform/media/crossplat-xamarin-formsguide-6.png "CrossPlat Xamarin FormsGuide 6")

2.  Para adicionar um botão à tela WeatherPage, substitua o conteúdo de WeatherPage.xaml pelo seguinte:

    ```xaml
    <?xml version="1.0" encoding="utf-8" ?>
    <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
           xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
           x:Class="WeatherApp.WeatherPage">
      <Button x:Name="getWeatherBtn" Text="Get Weather"/>
    </ContentPage>
    ```

     Observe que o nome do botão deve ser definido usando o atributo **x:Name** para que você possa fazer referência a esse botão pelo nome de dentro do arquivo code-behind.

3.  Para adicionar um manipulador de eventos ao evento **Clicado** do botão para atualizar o texto do botão, substitua o conteúdo de **WeatherPage.xaml.cs** pelo código a seguir. (Fique à vontade para trocar "60601" por outro código postal.)

    ```csharp
    using System;
    using Xamarin.Forms;

    namespace WeatherApp
    {
        public partial class WeatherPage: ContentPage
        {
            public WeatherPage()
            {
                InitializeComponent();
                this.Title = "Sample Weather App";
                getWeatherBtn.Clicked += GetWeatherBtn_Clicked;

                //Set the default binding to a default object for now
                this.BindingContext = new Weather();
            }

            private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
            {
                Weather weather = await Core.GetWeather("60601");
                getWeatherBtn.Text = weather.Title;
            }
        }
    }
    ```

4.  Para abrir **WeatherPage** como a primeira tela quando o aplicativo for iniciado, substitua o construtor padrão em **App.cs** pelo código a seguir:

    ```csharp
    public App()
    {
        MainPage = new NavigationPage(new WeatherPage());
    }
    ```

5.  Compile o projeto da PCL WeatherApp para garantir que o código esteja correto.

##  <a name="test"></a> Testar seu aplicativo usando o Emulador do Visual Studio para Android
 Agora, você está pronto para executar o aplicativo! Vamos executar apenas a versão para Android por enquanto para verificar se o aplicativo está obtendo dados do serviço meteorológico. Mais tarde, você executará também as versões para Windows Phone e iOS após ter adicionado mais elementos da interface do usuário. (Observação: se estiver executando o Visual Studio no Windows 7, você seguirá as mesmas etapas, mas com o Xamarin Player.)

1.  Defina o projeto **WeatherApp.Droid** como o projeto de inicialização clicando com o botão direito do mouse e selecionando **Definir como Projeto de Inicialização**.

2.  Na barra de ferramentas do Visual Studio, você verá **WeatherApp.Droid** listado como o projeto de destino. Selecione um dos emuladores do Android para depuração e pressione **F5**. É recomendável usar uma das opções de **Emulador do VS** que executarão o aplicativo nas opções do Emulador do Visual Studio para Android.

     ![Selecionando um destino de depuração do Emulador do VS](../cross-platform/media/crossplat-xamarin-formsguide-7.png "CrossPlat Xamarin FormsGuide 7")

3.  Quando o aplicativo for iniciado no emulador, clique no botão **Get Weather** (Obter clima). Você verá o texto do botão atualizado para **Chicago, IL**, que é a propriedade *Title* dos dados recuperados do serviço meteorológico.

     ![Aplicativo meteorológico antes e depois de pressionar o botão](../cross-platform/media/crossplat-xamarin-formsguide-8.png "CrossPlat Xamarin FormsGuide 8")

##  <a name="finish"></a> Concluir a interface do usuário com uma aparência nativa entre plataformas
 O Xamarin.Forms renderiza controles nativos da interface do usuário para cada plataforma, para que seu aplicativo tenha uma aparência nativa automaticamente. Para ver isso mais claramente, vamos terminar a interface do usuário com um campo de entrada para um código postal e, em seguida, exibir os dados meteorológicos retornados do serviço.

1. Substitua o conteúdo de **WeatherPage.xaml** pelo código a seguir. Observe que cada elemento é nomeado usando o atributo **x:Name**, conforme descrito anteriormente, para que o elemento possa ser referenciado no código. O Xamarin.Forms também fornece um número de [opções de layout](http://developer.xamarin.com/guides/xamarin-forms/controls/layouts/) (xamarin.com); aqui, WeatherPage está usando [StackLayout](http://developer.xamarin.com/api/type/Xamarin.Forms.StackLayout/) (xamarin.com).

   ```xaml
   <?xml version="1.0" encoding="utf-8" ?>
   <ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
          xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
          x:Class="WeatherApp.WeatherPage">

     <ContentPage.Resources>
       <ResourceDictionary>
         <Style x:Key="labelStyle" TargetType="Label">
           <Setter Property="TextColor" Value="#a8a8a8" />
           <Setter Property="FontSize" Value="Small" />
         </Style>
         <Style x:Key="fieldStyle" TargetType="Label">
           <Setter Property="TextColor">
             <OnPlatform x:TypeArguments="Color" iOS="Black" Android="White" WinPhone="White" />
           </Setter>
           <Setter Property="FontSize" Value="Medium" />
         </Style>
         <Style x:Key="fieldView" TargetType="ContentView">
           <Setter Property="Padding" Value="10,0,0,0" />
         </Style>
       </ResourceDictionary>
     </ContentPage.Resources>

     <ContentPage.Content>
       <ScrollView>
         <StackLayout>
           <StackLayout Orientation="Horizontal" HorizontalOptions="FillAndExpand"
                 BackgroundColor="#545454">
             <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
               <Label Text="Search by Zip Code" TextColor="White" FontAttributes="Bold"
                   FontSize="Medium" />
               <Label x:Name="zipCodeLabel" Text="Zip Code" Style="{StaticResource labelStyle}" />
               <Entry x:Name="zipCodeEntry" />
             </StackLayout>
             <StackLayout Padding="0,0,0,10" VerticalOptions="End">
               <Button x:Name="getWeatherBtn" Text="Get Weather" WidthRequest="185" BorderWidth="1" >
                 <!-- Set iOS colors; use defaults on other platforms -->
                 <Button.TextColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.TextColor>
                 <Button.BorderColor>
                   <OnPlatform x:TypeArguments="Color" iOS="White"/>
                 </Button.BorderColor>
               </Button>
             </StackLayout>
           </StackLayout>
           <StackLayout Padding="10,10,10,10" HorizontalOptions="Start">
             <Label Text="Location" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label Text="{Binding Title}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Temperature" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="tempLabel" Text="{Binding Temperature}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Wind Speed" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="windLabel" Text="{Binding Wind}" Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Humidity" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="humidityLabel" Text="{Binding Humidity}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Visibility" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="visibilitylabel" Text="{Binding Visibility}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunrise" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunriseLabel" Text="{Binding Sunrise}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
             <Label Text="Time of Sunset" Style="{StaticResource labelStyle}" />
             <ContentView Style="{StaticResource fieldView}">
               <Label x:Name="sunsetLabel" Text="{Binding Sunset}"
                   Style="{StaticResource fieldStyle}" />
             </ContentView>
           </StackLayout>
         </StackLayout>
       </ScrollView>
     </ContentPage.Content>
   </ContentPage>
   ```

    Observe o uso da marca **OnPlatform** no Xamarin.Forms. **OnPlatform** seleciona um valor da propriedade específico à plataforma atual em que o aplicativo está em execução (consulte [Sintaxe XAML Externa](http://developer.xamarin.com/guides/xamarin-forms/user-interface/xaml-basics/essential_xaml_syntax/) (xamarin.com). Estamos usando-o aqui para definir uma cor de texto diferente para os campos de dados: Em branco no Android e Windows Phone, preto no iOS. Você pode usar **OnPlatform** para qualquer propriedade e qualquer tipo de dados para fazer ajustes específicos da plataforma em qualquer lugar em seu XAML. No arquivo code-behind, você pode usar a [API Device.OnPlatform](http://developer.xamarin.com/guides/xamarin-forms/platform-features/device/) para a mesma finalidade.

2. Em **WeatherPage.xaml.cs**, substitua manipulador de eventos **GetWeatherBtn_Clicked** pelo código a seguir. Esse código verifica se há um código postal no campo de entrada, recupera dados do código postal, define o contexto de associação da tela inteira para a instância resultante de Weather e define o texto do botão como "Pesquisar Novamente". Observe que cada rótulo na interface do usuário é associado a uma propriedade da classe Weather, de modo que quando você definir o contexto de associação da tela para uma instância de **Weather**, os rótulos serão atualizados automaticamente.

   ```csharp
   private async void GetWeatherBtn_Clicked(object sender, EventArgs e)
   {
       if (!String.IsNullOrEmpty(zipCodeEntry.Text))
       {
           Weather weather = await Core.GetWeather(zipCodeEntry.Text);
           this.BindingContext = weather;
           getWeatherBtn.Text = "Search Again";
       }
   }
   ```

3. Execute o aplicativo nas três plataformas — iOS, Android e Windows Phone — clicando com o botão direito do mouse no projeto apropriado, selecionando Definir como projeto de inicialização e iniciando o aplicativo em um dispositivo ou no emulador ou simulador. Insira um código postal válido dos Estados Unidos (como 60601) e pressione o botão Get Weather (Obter clima) para exibir dados meteorológicos para essa região, conforme mostrado abaixo. Você precisará ter o Visual Studio conectado a um computador Mac OS X em sua rede para o projeto de iOS.

    ![Exemplo de Aplicativo Meteorológico em iOS, Android e Windows Phone](../cross-platform/media/crossplat-xamarin-formsguide-1.png "CrossPlat Xamarin FormsGuide 1")

   O código-fonte completo desse projeto no [repositório xamarin-forms-samples no GitHub](https://github.com/xamarin/xamarin-forms-samples/tree/master/Weather).
