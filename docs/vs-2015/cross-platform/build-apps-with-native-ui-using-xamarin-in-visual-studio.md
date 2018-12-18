---
title: Compile aplicativos com interface do usuário nativa usando o Xamarin
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30f137e6-595d-4ce7-b8f5-415b07c1caa2
caps.latest.revision: 33
ms.author: crdun
manager: crdun
ms.openlocfilehash: 7a17f8468eca37b5b977aa6b892e268bda5376ba
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53066231"
---
# <a name="build-apps-with-native-ui-using-xamarin-in-visual-studio"></a>Criar aplicativos com interface do usuário nativa usando o Xamarin no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


Depois de concluir as etapas em [Configuração e instalação](../cross-platform/setup-and-install.md) e [Verificar seu ambiente Xamarin](../cross-platform/verify-your-xamarin-environment.md), este passo a passo mostra como criar um aplicativo Xamarin básico (mostrado abaixo) com as camadas de interface do usuário nativas. Com a interface do usuário nativa, o código compartilhado reside em uma PCL (biblioteca de classes portátil) e os projetos de plataforma individuais contêm as definições de interface do usuário.

 ![Aplicativo Xamarin no Android e no Windows Phone](../cross-platform/media/cross-plat-xamarin-build-1.png "Xamarin Multiplataformas Build 1")

 Você executará as seguintes ações para compilar:

-   [Configurar sua solução](#solution)

-   [Escrever código de serviço de dados compartilhado](#dataservice)

-   [Projetar a interface do usuário para Android](#Android)

-   [Projetar a interface do usuário para Windows Phone](#Windows)

-   [Próximas etapas](#next)

> [!TIP]
>  Você pode encontrar o código-fonte completo para esse projeto no [repositório de amostras móveis no GitHub](https://github.com/xamarin/mobile-samples/tree/master/Weather).
>
>   Se você tiver dificuldades ou encontrar erros, publique perguntas em [forums.xamarin.com](http://forums.xamarin.com). Muitos erros podem ser resolvidos atualizando para os SDKs mais recentes exigidos pelo Xamarin, que são descritos em [Notas de Versão do Xamarin](https://developer.xamarin.com/releases/) para cada plataforma.
>
> [!NOTE]
>  A documentação do desenvolvedor do Xamarin também oferece várias instruções passo a passo com seções de Início Rápido e de Aprofundamento conforme listado abaixo. Em todas essas páginas, certifique-se de que "Visual Studio" esteja selecionado no canto superior direito da página para ver instruções passo a passo específicas do Visual Studio.
>
> - Aplicativos Xamarin com interface do usuário nativa:
>
>   -   [Olá, Android](https://developer.xamarin.com/guides/android/getting_started/hello,android/) (aplicativo simples com uma tela)
>   -   [Olá, Android multitela](https://developer.xamarin.com/guides/android/getting_started/hello,android_multiscreen/) (aplicativo com navegação entre telas)
>   -   [Passo a passo de fragmentos do Android](http://developer.xamarin.com/guides/android/platform_features/fragments/fragments_walkthrough/) (usado para telas mestre/detalhadas, entre outros elementos)
>   -   [Hello, iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/)
>   -   [Multitela Hello, iOS](https://developer.xamarin.com/guides/ios/getting_started/hello,_iOS_multiscreen/)
>   -   Aplicativos Xamarin com Xamarin.Forms (interface do usuário compartilhada)
>
>   -   [Hello, Xamarin.Forms](https://developer.xamarin.com/guides/cross-platform/xamarin-forms/getting-started/hello-xamarin-forms/quickstart/)
>   -   [Multitela Hello, Xamarin.Forms](https://developer.xamarin.com/guides/cross-platform/xamarin-forms/getting-started/hello-xamarin-forms-multiscreen/)

##  <a name="solution"></a> Configurar sua solução
 Estas etapas criam uma solução Xamarin com interface do usuário nativa que contém uma PCL para o código compartilhado e dois pacotes NuGet adicionados.

1. No Visual Studio, crie uma nova solução de **Aplicativo em Branco (Portátil Nativo)** e dê a ela o nome de **WeatherApp**. Você pode localizar esse modelo mais facilmente digitando **Portátil Nativo** no campo de pesquisa.

    Se não estiver lá, talvez você precise instalar o Xamarin ou habilitar o recurso do Visual Studio 2015, consulte [Configuração e instalação](../cross-platform/setup-and-install.md).

2. Depois de clicar em OK para criar a solução, você terá vários projetos individuais:

   - **WeatherApp (Portátil)**: a PCL em que você escreverá o código que é compartilhado entre plataformas, incluindo lógica de negócios comum e código de interface do usuário com Xamarin.Forms.

   - **WeatherApp.Droid**: o projeto que contém o código nativo do Android. É definido como o projeto de inicialização padrão.

   - **WeatherApp.iOS**: o projeto que contém o código iOS nativo.

   - **WeatherApp.WinPhone (Windows Phone 8.1)**: o projeto que contém o código nativo do Windows Phone.

     Dentro de cada projeto nativo, você tem acesso ao designer nativo para a plataforma correspondente e pode implementar telas específicas da plataforma.

3. Adicione o pacote **Newtonsoft.Json** e o pacote NuGet ao projeto PCL, que você usará para processar as informações recuperadas de um serviço de dados de clima:

   -   Clique com botão direito do mouse em **Solução 'WeatherApp'** no Gerenciador de Soluções e selecione **Gerenciar Pacotes NuGet para Solução…**.

        Na janela do NuGet, selecione a guia **Procurar** e pesquise **Newtonsoft**.

   -   Selecione **Newtonsoft.Json**.

   -   No lado direito da janela, verifique o projeto **WeatherApp** (esse é o projeto único no qual você precisa instalar o pacote).

   -   Verifique se o campo **Versão** está definido como a versão **Estável mais recente**.

   -   Clique em **Instalar**.

   -   ![Localizando e instalando o pacote do NuGet Newtonsoft.Json](../cross-platform/media/crossplat-xamarin-formsguide-5.png "CrossPlat Xamarin FormsGuide 5")

4. Repita a etapa 3 para localizar e instalar o pacote **Microsoft.Net.Http**.

5. Compile sua solução e verifique não se há erros de build.

##  <a name="dataservice"></a> Escrever código de serviço de dados compartilhados
 É no projeto **WeatherApp (Portátil)** que você escreverá código para a PCL (biblioteca de classes portátil) que será compartilhado entre todas as plataformas. A PCL é incluída automaticamente nos pacotes de aplicativo compilados por projetos iOS, Android e Windows Phone.

 As etapas a seguir então adicionam código para o PCL acessar e armazenar dados de serviço de clima:

1.  Para executar este exemplo, primeiro você precisa se inscrever para obter uma chave de API gratuita em [http://openweathermap.org/appid](http://openweathermap.org/appid).

2.  Clique com botão direito do mouse no projeto **WeatherApp** e selecione **Adicionar > Classe…**. Na caixa de diálogo **Adicionar Novo Item**, dê ao arquivo o nome **Weather.cs**. Você usará essa classe para armazenar dados do serviço de dados de clima.

3.  Substitua todo o conteúdo de **Weather.cs** pelo seguinte:

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

4.  Adicione outra classe ao projeto PCL chamada **DataService.cs** em que você usará para processar dados JSON do serviço de dados de clima.

5.  Substitua todo o conteúdo de **DataService.cs** pelo código a seguir:

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

6.  Adicione uma terceira classe à PCL chamada **Core**, na qual você colocará a lógica de negócios compartilhada, como a lógica que forma uma cadeia de caracteres de consulta com um CEP, chama o serviço de dados de clima e preenche uma instância da classe **Clima**.

7.  Substitua o conteúdo de **Core.cs** pelo seguinte:

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

                //Make sure developers running this sample replaced the API key
                if (key == "YOUR API KEY HERE")
                {
                    throw new ArgumentException("You must obtain an API key from openweathermap.org/appid and save it in the 'key' variable.");
                }

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

8.  Substitua *YOUR KEY HERE* no código pela chave de API que você obteve na etapa 1 (ainda precisa de aspas).

9. Exclua MyClass.cs na PCL, porque ela não será utilizada.

10. Compile o projeto da PCL **WeatherApp** para garantir que o código esteja correto.

##  <a name="Android"></a> Projetar a interface do usuário para Android
 Agora projetaremos a interface do usuário, conectaremos essa interface ao seu código compartilhado e então executaremos o aplicativo.

### <a name="design-the-look-and-feel-of-your-app"></a>Criar a aparência de seu aplicativo

1.  Em **Gerenciador de Soluções**, expanda a pasta **WeatherApp.Droid**>**Recursos**>**layout** e abra **Main.axml**. Isso abre o arquivo no designer visual. (Se for exibido um erro relacionado a Java, consulte esta [postagem de blog](http://forums.xamarin.com/discussion/32365/connection-to-the-layout-renderer-failed-in-xs-5-7-and-xamarinvs-3-9).)

    > [!TIP]
    >  Há muitos outros arquivos no projeto. Explorá-los está além do escopo deste tópico, mas se você quiser aprofundar-se na estrutura de um projeto Android um pouco mais, consulte a [Part 2 Deep Dive](http://developer.xamarin.com/guides/android/getting_started/hello,android/hello,android_deepdive/) (Parte 2, Aprofundamento) do tópico Hello Android (Olá, Android) em xamarin.com.

2.  Selecione e exclua o botão padrão que aparece no designer.

3.  Abra a Caixa de Ferramentas com **Exibir > Outras Janelas > Caixa de Ferramentas**.

4.  Em **Caixa de Ferramentas**, arraste um controle **RelativeLayout** para o designer. Você usará esse controle como um contêiner pai para outros controles.

    > [!TIP]
    >  Se, a qualquer momento, o layout parecer não ser exibido corretamente, salve o arquivo e troque entre as guias **Design** e **Fonte** para atualizar.

5.  Na janela **Propriedades**, defina a propriedade **tela de fundo** (no grupo Estilo) como `#545454`.

6.  Na **Caixa de Ferramentas**, arraste um controle **TextView** para o controle **RelativeLayout**.

7.  Na janela **Propriedades**, defina essas propriedades (observação: pode ajudar classificar a lista em ordem alfabética usando o botão de classificação na barra de ferramentas de janela Propriedades):

    |Propriedade|Valor|
    |--------------|-----------|
    |**text**|**Pesquisar por CEP**|
    |**id**|`@+id/ZipCodeSearchLabel`|
    |**layout_marginLeft**|`10dp`|
    |**textColor**|`@android:color/white`|
    |**textStyle**|`bold`|

    > [!TIP]
    >  Observe que muitas propriedades não contêm uma lista suspensa de valores que você pode selecionar.  Pode ser difícil adivinhar qual valor de cadeia de caracteres usar para qualquer propriedade específica. Para obter sugestões, tente pesquisar o nome de uma propriedade na página [R.attr](http://developer.android.com/reference/android/R.attr.html).
    >
    >  Além disso, uma pesquisa rápida na Web geralmente leva a uma página no [http://stackoverflow.com/](http://stackoverflow.com/) na qual outras pessoas já usaram a mesma propriedade.

     Para referência, se você mudar para a exibição **Fonte**, deverá ver o seguinte código para esse elemento:

    ```xml
    <TextView
        android:text="Search by Zip Code"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:id="@+id/ZipCodeSearchLabel"
        android:layout_centerVertical="true"
        android:layout_marginLeft="10dp"
        android:textColor="@android:color/white"
        android:textStyle="bold" />

    ```

8.  Na **Caixa de Ferramentas**, arraste um controle **TextView** para o controle **RelativeLayout** e posicione-o abaixo do controle ZipCodeSearchLabel. Para fazer isso, largue o novo controle na borda apropriada do controle existente; isso ajuda a aplicar zoom ao designer para isso.

9. Na janela **Propriedades**, defina estas propriedades:

    |Propriedade|Valor|
    |--------------|-----------|
    |**text**|**Código Postal**|
    |**id**|`@+id/ZipCodeLabel`|
    |**layout_marginLeft**|`10dp`|
    |**layout_marginTop**|`5dp`|

     O código na exibição **Fonte** deve ter esta aparência:

    ```xml
    <TextView
        android:text="Zip Code"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/ZipCodeSearchLabel"
        android:id="@+id/ZipCodeLabel"
        android:layout_marginTop="5dp"
        android:layout_marginLeft="10dp" />
    ```

10. Na **Caixa de Ferramentas**, arraste um controle de **Número** para **RelativeLayout** e posicione-o abaixo do rótulo **CEP**. Então defina as propriedades a seguir:

    |Propriedade|Valor|
    |--------------|-----------|
    |**id**|`@+id/zipCodeEntry`|
    |**layout_marginLeft**|`10dp`|
    |**layout_marginBottom**|`10dp`|
    |**width**|`165dp`|

     Novamente, o código:

    ```xml
    <EditText
        android:inputType="number"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/ZipCodeLabel"
        android:id="@+id/zipCodeEntry"
        android:layout_marginLeft="10dp"
        android:layout_marginBottom="10dp"
        android:width="165dp" />
    ```

11. Na **Caixa de Ferramentas**, arraste um **Botão** para o controle **RelativeLayout** e posicione-o à direita do controle zipCodeEntry. Então defina estas propriedades:

    |Propriedade|Valor|
    |--------------|-----------|
    |**id**|`@+id/weatherBtn`|
    |**text**|**Get Weather**|
    |**layout_marginLeft**|`20dp`|
    |**layout_alignBottom**|`@id/zipCodeEntry`|
    |**width**|`165dp`|

    ```xml
    <Button    android:text="Get Weather"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_toRightOf="@id/zipCodeEntry"
        android:id="@+id/weatherBtn"
        android:layout_marginLeft="20dp"
        android:layout_alignBottom="@id/zipCodeEntry"
        android:width="165dp" />
    ```

12. Agora você tem experiência suficiente para criar uma interface do usuário básica usando o designer Android. Você também pode criar uma interface do usuário adicionando marcação diretamente ao arquivo .asxml da página. Para criar o restante da interface do usuário dessa maneira, mude para a exibição Fonte no designer, então cole a seguinte marcação *abaixo* da marca `</RelativeLayout>` (sim, está abaixo da marca... esses elementos não estão contidos no ReleativeLayout).

    ```xml
    <TextView
            android:text="Location"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/locationLabel"
            android:layout_marginLeft="10dp"
            android:layout_marginTop="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/locationText"
            android:layout_marginLeft="20dp"
            android:layout_marginBottom="10dp" />
        <TextView
            android:text="Temperature"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/tempLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/tempText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />
        <TextView
            android:text="Wind Speed"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/windLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/windText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />
        <TextView
            android:text="Humidity"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/humidtyLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/humidityText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />
        <TextView
            android:text="Visibility"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/visibilityLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/visibilityText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />
        <TextView
            android:text="Time of Sunrise"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/sunriseLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/sunriseText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />
        <TextView
            android:text="Time of Sunset"
            android:textAppearance="?android:attr/textAppearanceSmall"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/sunsetLabel"
            android:layout_marginLeft="10dp" />
        <TextView
            android:textAppearance="?android:attr/textAppearanceMedium"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:id="@+id/sunsetText"
            android:layout_marginBottom="10dp"
            android:layout_marginLeft="20dp" />

    ```

13. Salve o arquivo e mude para o modo de exibição de **Design**. Sua interface do usuário deve aparecer da seguinte maneira:

     ![Interface do usuário para aplicativo Android](../cross-platform/media/xamarin-androidui.png "Xamarin_AndroidUI")

14. Abra **MainActivity.cs** e exclua as linhas no método *OnCreate* que se referem ao botão padrão removido anteriormente. O código deve ser assim quando você terminar:

    ```
    protected override void OnCreate (Bundle bundle)
    {
        base.OnCreate (bundle);

        // Set our view from the "main" layout resource
        SetContentView (Resource.Layout.Main);
    }
    ```

15. Compile o projeto Android para verificar seu trabalho. Observe que compilar adiciona IDs de controle ao arquivo **Resource.Designer.cs**, de modo que você pode se referir aos controles por nome no código.

### <a name="consume-your-shared-code"></a>Consumir seu código compartilhado

1.  Abra o arquivo **MainActivity.cs** do projeto **WeatherApp** no editor de código e substitua seu conteúdo pelo código a seguir. Esse código chama o método `GetWeather` que você definiu no seu código compartilhado. Em seguida, na interface do usuário do aplicativo, ele mostra os dados recuperados daquele método.

    ```csharp
    using System;
    using Android.App;
    using Android.Widget;
    using Android.OS;

    namespace WeatherApp.Droid
    {
        [Activity(Label = "Sample Weather App", MainLauncher = true, Icon = "@drawable/icon")]
        public class MainActivity : Activity
        {
            protected override void OnCreate(Bundle bundle)
            {
                base.OnCreate(bundle);

                SetContentView(Resource.Layout.Main);

                Button button = FindViewById<Button>(Resource.Id.weatherBtn);

                button.Click += Button_Click;
            }

            private async void Button_Click(object sender, EventArgs e)
            {
                EditText zipCodeEntry = FindViewById<EditText>(Resource.Id.zipCodeEntry);

                if (!String.IsNullOrEmpty(zipCodeEntry.Text))
                {
                    Weather weather = await Core.GetWeather(zipCodeEntry.Text);
                    FindViewById<TextView>(Resource.Id.locationText).Text = weather.Title;
                    FindViewById<TextView>(Resource.Id.tempText).Text = weather.Temperature;
                    FindViewById<TextView>(Resource.Id.windText).Text = weather.Wind;
                    FindViewById<TextView>(Resource.Id.visibilityText).Text = weather.Visibility;
                    FindViewById<TextView>(Resource.Id.humidityText).Text = weather.Humidity;
                    FindViewById<TextView>(Resource.Id.sunriseText).Text = weather.Sunrise;
                    FindViewById<TextView>(Resource.Id.sunsetText).Text = weather.Sunset;
                }
            }
        }
    }
    ```

### <a name="run-the-app-and-see-how-it-looks"></a>Execute o aplicativo e veja a aparência dele

1.  Em **Gerenciador de Soluções**, garanta que o projeto **WeatherApp.Droid** esteja definido como o projeto de inicialização.

2.  Selecione um destino de emulador ou dispositivo apropriado e inicie o aplicativo pressionando a tecla F5.

3.  No dispositivo ou no emulador, digite um CEP válido dos Estados Unidos na caixa de edição (por exemplo: 60601) e pressione **obter clima**. Dados de clima para aquela região então são exibidos nos controles.

     ![Aplicativo de clima para Android e Windows Phone](../cross-platform/media/xamarin-getstarted-results.png "Xamarin_GetStarted_Results")

> [!TIP]
>  O código-fonte completo para esse projeto está no [repositório de amostras móveis no GitHub](https://github.com/xamarin/mobile-samples/tree/master/Weather).

##  <a name="Windows"></a> Projetar a interface do usuário para Windows Phone
 Agora projetaremos a interface do usuário para Windows Phone, conectaremos essa interface ao seu código compartilhado e então executaremos o aplicativo.

### <a name="design-the-look-and-feel-of-your-app"></a>Criar a aparência de seu aplicativo
 O processo de criação da interface do usuário nativa do Windows Phone em um aplicativo Xamarin não é diferente de nenhum outro aplicativo nativo do Windows Phone. Por esse motivo, não entraremos em detalhes aqui sobre como usar o designer. Para isso, consulte [Criando uma interface do usuário usando o Designer de XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

 Em vez disso, simplesmente abra MainPage.xaml e substitua todo o código XAML pelo seguinte:

```xaml
<Page
    x:Class="WeatherApp.WinPhone.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:WeatherApp.WinPhone"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>
        <StackPanel HorizontalAlignment="Left" Height="40" Margin="10,0,0,0" VerticalAlignment="Top" Width="400">
            <TextBlock x:Name="pageTitle" Text="Weather App" FontSize="30" />
        </StackPanel>
        <StackPanel HorizontalAlignment="Left" Height="120" Margin="10,40,0,0" VerticalAlignment="Top" Width="400" Background="#FF545454">

            <TextBlock x:Name="zipCodeSearchLabel" TextWrapping="Wrap" Text="Search by Zip Code" FontSize="18" FontWeight="Bold" HorizontalAlignment="Left" Margin="10,10,0,0"/>
            <TextBlock x:Name="zipCodeLabel" TextWrapping="Wrap" Text="Zip Code" Margin="10,5,0,0" FontSize="14" Foreground="#FFA8A8A8"/>
            <StackPanel Orientation="Horizontal">
                <TextBox x:Name="zipCodeEntry" Margin="10,10,0,0" Text="" VerticalAlignment="Top" InputScope="Number" Width="165" />
                <Button x:Name="weatherBtn" Content="Get Weather" Width="165" Margin="20,0,0,0" Height="60" Click="GetWeatherButton_Click"/>
            </StackPanel>
        </StackPanel>
        <StackPanel Margin="10,175,0,0">
            <TextBlock x:Name="locationLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Location" VerticalAlignment="Top"/>
            <TextBlock x:Name="locationText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="tempLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Temperature" VerticalAlignment="Top"/>
            <TextBlock x:Name="tempText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="windLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Wind Speed" VerticalAlignment="Top"/>
            <TextBlock x:Name="windText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="humidityLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Humidity" VerticalAlignment="Top"/>
            <TextBlock x:Name="humidityText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="visibilityLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Temperature" VerticalAlignment="Top"/>
            <TextBlock x:Name="visibilityText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="sunriseLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Time of Sunriweatherse" VerticalAlignment="Top"/>
            <TextBlock x:Name="sunriseText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
            <TextBlock x:Name="sunsetLabel" HorizontalAlignment="Left" FontSize="14" Foreground="#FFA8A8A8" TextWrapping="Wrap" Text="Time of Sunset" VerticalAlignment="Top"/>
            <TextBlock x:Name="sunsetText" Margin="10,0,0,10" HorizontalAlignment="Left" FontSize="18" TextWrapping="Wrap" VerticalAlignment="Top"/>
        </StackPanel>
    </Grid>
</Page>
```

 No modo de exibição de design, sua interface do usuário deve aparecer da seguinte maneira:

 ![Interface do usuário do aplicativo Windows Phone](../cross-platform/media/xamarin-winphone-finalui.png "Xamarin_WinPhone_FinalUI")

### <a name="consume-your-shared-code"></a>Consumir seu código compartilhado

1.  No designer, selecione o botão **Obter Clima**.

2.  Na janela **Propriedades**, escolha o botão de manipulador de eventos (![ícone Manipuladores de Eventos do Visual Studio](../cross-platform/media/blend-vs-eventhandlers-icon.png "blend_VS_EventHandlers_icon")).

     Esse ícone é exibido no canto superior da janela **Propriedades**.

3.  Ao lado do evento **Clicar**, digite **GetWeatherButton_Click** e, em seguida, pressione a tecla ENTER.

     Isso gera um manipulador de eventos chamado `GetWeatherButton_Click`. O editor de códigos abre e coloca o cursor dentro do bloco de códigos do manipulador de eventos.  Observação: se o editor não abrir ao pressionar ENTER, apenas clique duas vezes no nome do evento.

4.  Substitua o manipulador de eventos pelo código a seguir.

    ```csharp
    private async void GetWeatherButton_Click(object sender, RoutedEventArgs e)
    {
        if (!String.IsNullOrEmpty(zipCodeEntry.Text))
        {
            Weather weather = await Core.GetWeather(zipCodeEntry.Text);
            locationText.Text = weather.Title;
            tempText.Text = weather.Temperature;
            windText.Text = weather.Wind;
            visibilityText.Text = weather.Visibility;
            humidityText.Text = weather.Humidity;
            sunriseText.Text = weather.Sunrise;
            sunsetText.Text = weather.Sunset;

            weatherBtn.Content = "Search Again";
        }
    }
    ```

     Esse código chama o método `GetWeather` que você definiu no seu código compartilhado. Esse é o mesmo método chamado em seu aplicativo Android. Esse código também mostra os dados recuperados do método nos controles da interface do usuário do seu aplicativo.

5.  Em MainPage.xaml.cs, que está aberta, exclua todo o código dentro do método **OnNavigatedTo**. Esse código tratou de modo simples o botão padrão removido quando substituímos o conteúdo de MainPage.xaml.

### <a name="run-the-app-and-see-how-it-looks"></a>Execute o aplicativo e veja a aparência dele

1.  No **Gerenciador de Soluções**, defina o projeto **WeatherApp.WinPhone** como o projeto de inicialização.

2.  Inicie o aplicativo pressionando a tecla F5.

3.  No emulador do Windows Phone, digite um CEP válido dos Estados Unidos, na caixa de edição (por exemplo: 60601) e pressione **obter clima**. Dados de clima para aquela região então são exibidos nos controles.

     ![Versão do Windows do aplicativo em execução](../cross-platform/media/xamarin-getstarted-results-windows.png "Xamarin_GetStarted_Results_Windows")

> [!TIP]
>  O código-fonte completo para esse projeto está no [repositório de amostras móveis no GitHub](https://github.com/xamarin/mobile-samples/tree/master/Weather).

##  <a name="next"></a> Próximas etapas
 **Adicionar a interface do usuário para iOS à solução**

 Estenda este exemplo adicionando a interface do usuário nativa para iOS. Para isso, você precisará conectar-se a um Mac na sua rede local que tenha o Xcode e o Xamarin instalados. Depois de fazer isso, você poderá usar o designer de iOS diretamente no Visual Studio. Consulte o [repositório de amostras móveis no GitHub](https://github.com/xamarin/mobile-samples/tree/master/Weather) para um aplicativo completo.

 Consulte também o passo a passo [Hello, iOS](http://developer.xamarin.com/guides/ios/getting_started/hello,_iOS/hello,iOS_quickstart/) (Olá, iOS) (xamarin.com). Nesta página, garanta que "Visual Studio" esteja selecionado no canto superior direito das páginas em xamarin.com para que o conjunto correto de instruções seja exibido.

 **Adicionar código específico da plataforma em um projeto compartilhado**

 O código compartilhado em uma PCL é neutro em termos de plataforma, pois a PCL é compilada uma vez e incluída em cada pacote do aplicativo específico da plataforma. Se você quiser escrever código compartilhado que use compilação condicional para isolar o código específico da plataforma, poderá usar um projeto *compartilhado*. Para obter mais detalhes, consulte [Opções de compartilhamento ode](http://developer.xamarin.com/guides/cross-platform/application_fundamentals/building_cross_platform_applications/sharing_code_options/) (xamarin.com).

## <a name="see-also"></a>Consulte também
 [Site de desenvolvedor do Xamarin](http://developer.xamarin.com/) [Centro de desenvolvimento do Windows](https://dev.windows.com/en-us) [Swift e C# pôster de referência rápida](http://aka.ms/scposter)
