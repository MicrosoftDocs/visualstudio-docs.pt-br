---
title: Definir um perfil para estender UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- profiles, UML
- stereotypes, UML
- UML, profiles and stereotypes
- UML - extending, defining profiles
- UML, customizing
- UML, profiles
ms.assetid: 776589cb-f89d-48d5-aafa-04a4c074b0d6
caps.latest.revision: 44
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 37c4560b767828be0ec43419ff92ec5b6f9863ea
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730339"
---
# <a name="define-a-profile-to-extend-uml"></a>Definir um perfil para estender UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode definir um *perfil UML* para personalizar os elementos de modelo padrão para fins específicos. Um perfil define um ou mais *Estereótipos UML*. Um estereótipo pode ser usado para marcar um tipo como a representação de um determinado tipo de objeto. Um estereótipo também pode estender a lista de um elemento de propriedades.  
  
 Vários perfis são instalados com as edições com suporte do Visual Studio. Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport). Para obter mais informações sobre estes perfis e sobre como aplicar estereótipos, consulte [personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md).  
  
 Você pode definir seus próprios perfis para adaptar e estender o UML para sua própria área comercial ou arquitetura. Por exemplo:  
  
- Se você geralmente define sites, você pode definir seu próprio perfil que fornece um estereótipo de "Web Page que pode ser aplicado a classes em diagramas de classe. Você pode usar diagramas de classe para planejar um site da Web. Cada classe "Web Page teria propriedades adicionais para o conteúdo da página, estilo e assim por diante.  
  
- Se você desenvolver software bancário, você pode definir um perfil que fornece um estereótipo «Conta». Em seguida, você pode usar diagramas de classe para definir diferentes tipos de conta e mostrar as relações entre eles.  
  
  Você pode distribuir seus próprios perfis para sua equipe. Cada membro da equipe pode instalar o perfil. Isso permite editar e criar modelos que usam seus estereótipos.  
  
> [!NOTE]
>  Se você aplicar os estereótipos de um perfil em um modelo que você está editando e, em seguida, compartilha o modelo com outras pessoas, eles devem instalar o mesmo perfil em seus próprios computadores. Caso contrário, eles não poderão ver os estereótipos que você usou.  
  
 Um perfil geralmente é parte de uma maior [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão. Por exemplo, você poderia definir um comando que traduz algumas partes de um modelo em código. Você pode definir um perfil que os usuários devem aplicar a pacotes que desejam traduzir. Você distribuiria seu novo comando juntamente com o perfil em um único [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] extensão.  
  
 Você também pode definir variantes localizadas de um perfil. Os usuários que carregam sua extensão veem a variante que é apropriada para sua própria cultura.  
  
##  <a name="DefineProfile"></a> Como definir um perfil  
  
#### <a name="to-define-a-uml-profile"></a>Para definir um perfil UML  
  
1.  Criar um novo arquivo XML com a extensão de nome de arquivo `.profile`.  
  
2.  Adicione definições estereótipas de acordo com as diretrizes descritas em [a estrutura de um perfil](#Schema).  
  
3.  Adicionar o perfil a uma extensão do Visual Studio (`.vsix` arquivo). Você pode criar uma nova extensão para o seu perfil, ou adicionar o perfil a uma extensão existente.  
  
     Consulte a próxima seção, [como adicionar um perfil para uma extensão do Visual Studio](#AddProfile).  
  
4.  Instale a extensão em seu computador.  
  
    1.  Clique duas vezes no arquivo de extensão, que tem uma extensão de nome de arquivo `.vsix`.  
  
    2.  Reinicie o Visual Studio.  
  
5.  Verifique se que o perfil foi instalado.  
  
    1.  Selecione o modelo no Gerenciador de UML.  
  
    2.  Na janela Propriedades, clique o **perfis** propriedade. Seu perfil aparecerá no menu. Defina a marca de seleção ao lado do perfil.  
  
    3.  Selecione um elemento para o qual o seu perfil define estereótipos. Na janela Propriedades, clique o **estereótipos** propriedade. Seus estereótimos serão exibidos na lista. Defina a marca de seleção em um dos estereótipos.  
  
    4.  Se o perfil Definir propriedades adicionais para esse estereótipo, expanda a propriedade do estereótipo para visualizá-los.  
  
6.  Envie o arquivo de extensão para outros usuários do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para instalar em seus computadores.  
  
##  <a name="AddProfile"></a> Como adicionar um perfil para uma extensão do Visual Studio  
 Para instalar um perfil e permitem que você enviá-las a outros usuários, você deve adicionar o perfil para uma extensão do Visual Studio. Para obter mais informações, consulte [Implantando extensões do Visual Studio](http://go.microsoft.com/fwlink/?LinkId=160780).  
  
#### <a name="to-define-a-profile-in-a-new-visual-studio-extension"></a>Para definir um perfil em uma nova extensão do Visual Studio  
  
1. Crie um projeto de extensão do Visual Studio.  
  
   > [!NOTE]
   >  Você deve ter instalado [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] usar esse procedimento.  
  
   1.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
   2.  No **novo projeto** caixa de diálogo **modelos instalados**, expanda **Visual c#**, clique em **extensibilidade**e, em seguida, clique em  **Projeto do VSIX**. Defina o nome do projeto e clique em **Okey**.  
  
2. Adicione o perfil ao projeto.  
  
   -   No Gerenciador de soluções, clique com botão direito no projeto, aponte para **Add**e, em seguida, clique em **Item existente**. Na caixa de diálogo, localize o arquivo de perfil.  
  
3. Definir o arquivo de perfil **copiar para saída** propriedade.  
  
   1.  No Gerenciador de soluções, clique com botão direito no arquivo do perfil e, em seguida, clique em **propriedades**.  
  
   2.  Na janela Propriedades, defina as **Copy to Output Directory** propriedade **copiar sempre**.  
  
4. No Gerenciador de soluções, abra `source.extension.vsixmanifest`.  
  
    O arquivo é aberto no editor de manifesto de extensão.  
  
5. Sobre o **ativos** página, adicione uma linha que descreve o perfil:  
  
   -   Clique em **Novo**. Defina os campos na **adicionar novo ativo** caixa de diálogo da seguinte maneira.  
  
   -   Definir **tipo** para `Microsoft.VisualStudio.UmlProfile`  
  
        Isso não é uma das opções de menu suspenso. Digite o nome do teclado.  
  
   -   Clique em **arquivo no sistema de arquivos** e selecione o nome do seu arquivo de perfil, por exemplo `MyProfile.profile`  
  
6. Compile o projeto.  
  
7. **Para depurar o perfil**, pressione F5.  
  
    Uma instância experimental do Visual Studio é aberto. Nesse caso, abra um projeto de modelagem. No Gerenciador de UML, selecione o elemento raiz do modelo e na janela Propriedades, selecione seu perfil. Em seguida, selecione elementos dentro do modelo e defina os estereótipos que você definiu para eles.  
  
8. **Para extrair o VSIX para implantação**  
  
   1.  No Windows Explorer, abra a pasta **.\bin\Debug** ou **.\bin\Release** para encontrar o **. VSIX** arquivo. Esse é um [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] arquivo de extensão. Pode ser instalado em seu computador e enviado para outros usuários do Visual Studio.  
  
   2.  Para instalar a extensão:  
  
       1.  Clique duas vezes o `.vsix` arquivo. Instalador de extensão do Visual Studio será iniciado.  
  
       2.  Reinicie todas as instâncias do Visual Studio que estão em execução.  
  
   O procedimento alternativo a seguir pode ser usado para extensões pequenas se você não tiver instalado [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)].  
  
#### <a name="to-define-a-profile-extension-without-using-visual-studio-sdk"></a>Para definir uma extensão de perfil sem usar o SDK do Visual Studio  
  
1.  Crie um diretório do Windows que contém três arquivos a seguir:  
  
    -   *YourProfile* `.profile`  
  
    -   `extension.vsixmanifest`  
  
    -   `[Content_Types].xml` -Digite esse nome, como mostrado aqui, com colchetes  
  
2.  Editar `[Content_Types].xml` para conter o texto a seguir. Observe que ele contém uma entrada para cada extensão de nome de arquivo.  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">  
      <Default Extension="profile" ContentType="application/octet-stream" />  
      <Default Extension="vsixmanifest" ContentType="text/xml" />  
    </Types>  
    ```  
  
3.  Copiar um existente `extension.vsixmanifest` e editá-lo com um editor de XML. Altere a ID, nome e nós de conteúdo.  
  
    -   Você pode encontrar um exemplo de `extension.vsixmanifest` neste diretório:  
  
         *unidade* **: \Program Files\Microsoft \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles Visual Studio [versão]**  
  
    -   O nó de conteúdo deve ser assim:  
  
        ```  
        <Content>  
          <CustomExtension Type="Microsoft.VisualStudio.UmlProfile"  
          >YourProfile.Profile</CustomExtension>  
        </Content>  
        ```  
  
4.  Compacte os três arquivos em um arquivo compactado.  
  
     No Windows Explorer, selecione os três arquivos, clique com botão direito, aponte para **enviar para**e, em seguida, clique em **pasta compactada (zipada)**.  
  
5.  Renomeie o arquivo compactado e altere sua extensão de nome de arquivo `.zip` para `.vsix`.  
  
6.  Para instalar o perfil em qualquer computador com edições apropriadas do Visual Studio, clique duas vezes o `.vsix` arquivo.  
  
#### <a name="to-install-a-uml-profile-from-a-visual-studio-extension"></a>Para instalar um perfil UML de uma extensão do Visual Studio  
  
1.  Clique duas vezes o `.vsix` de arquivos no Windows Explorer ou abri-lo no Visual Studio.  
  
2.  Clique em **instalar** na caixa de diálogo que aparece.  
  
3.  Para desinstalar ou desabilitar temporariamente a extensão, abra **extensões e atualizações** da **ferramentas** menu.  
  
##  <a name="Localized"></a> Como definir perfis localizados  
 Você pode definir perfis diferentes para culturas ou idiomas diferentes e empacotá-los todos na mesma extensão. Quando um usuário carrega a extensão, eles verão o perfil que você definiu para sua cultura.  
  
 Você sempre deve fornecer um perfil padrão. Se você não tiver definido um perfil para a cultura do usuário, eles verão o perfil padrão.  
  
#### <a name="to-define-a-localized-profile"></a>Para definir um perfil localizado  
  
1.  Criar um perfil, conforme descrito nas seções anteriores[como definir um perfil](#DefineProfile) e [como adicionar um perfil para uma extensão do Visual Studio](#AddProfile). Isso é o perfil padrão e será usado em qualquer instalação para o qual você não fornecer um perfil localizado.  
  
2.  Adicione um novo diretório no mesmo diretório que o arquivo de perfil padrão.  
  
    > [!NOTE]
    >  Se você estiver compilando a extensão usando um projeto de extensão do Visual Studio, use o Gerenciador de soluções para adicionar uma nova pasta para o projeto.  
  
3.  Altere o nome da nova pasta ao código curto ISO para a cultura localizada, como `bg` para o búlgaro ou `fr` para francês. Você deve usar um código de cultura neutra, normalmente com duas letras, não uma cultura específica, como `fr-CA`. Para obter mais informações sobre códigos de cultura, consulte [método CultureInfo GetCultures](http://go.microsoft.com/fwlink/?LinkId=160782), que fornece uma lista completa dos códigos de cultura.  
  
4.  Adicione uma cópia do perfil padrão para o novo diretório. Não altere seu nome de arquivo.  
  
     Uma amostra [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] pasta de extensão, antes que ela é compilada ou compactada em um `.vsix` de arquivos, conteria as pastas e arquivos a seguir:  
  
     `extension.vsixmanifest`  
  
     `MyProfile.profile`  
  
     `fr\MyProfile.profile`  
  
     `de\MyProfile.profile`  
  
    > [!NOTE]
    >  Você não deve inserir em `extension.vsixmanifest` uma referência para as versões localizadas dos perfis. Os arquivos de perfil copiados devem ter o mesmo nome que o perfil na pasta pai.  
  
5.  Editar a nova cópia do perfil, convertendo para o idioma de destino, todas as partes que serão visíveis ao usuário, como o `displayName` atributos.  
  
6.  Você pode criar pastas adicionais de cultura e perfis localizados para culturas quantos desejar.  
  
7.  Compile a extensão do Visual Studio, criando o projeto de extensão ou compactando todos os arquivos, conforme descrito nas seções anteriores.  
  
##  <a name="Schema"></a> A estrutura de um perfil  
 O arquivo XSD para perfis UML pode ser encontrado no exemplo a seguir: [definindo estereótipos e perfis XSD](http://go.microsoft.com/fwlink/?LinkID=213811). Para ajudar a editar arquivos de perfil, instale o `.xsd` de arquivo em:  
  
 **%ProgramFiles%\Microsoft visual Studio [versão] \XML\Schemas.**  
  
 Esta seção usa o perfil c# como um exemplo. A definição de perfil completo pode ser vista:  
  
 *unidade* **: \Program Files\Microsoft \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\CSharp.profile Visual Studio [versão]**  
  
 As primeiras partes desse caminho podem diferir em sua instalação.  
  
 Para obter mais informações sobre o perfil do .NET, consulte [estereótipos padrão para modelos UML](../modeling/standard-stereotypes-for-uml-models.md).  
  
### <a name="main-sections-of-the-uml-profile-definition"></a>Seções principais da definição de perfil UML  
 Cada perfil contém o seguinte conteúdo:  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<profile dslVersion="1.0.0.0"   
       name="CSharpProfile" displayName="C# Profile"   
       xmlns="http://schemas.microsoft.com/UML2.1.2/ProfileDefinition">  
  <stereotypes>...</stereotypes>  
  <metaclasses>...</metaclasses>  
  <propertyTypes>...</propertyTypes>  
</profile>  
```  
  
> [!NOTE]
>  O atributo chamado `name` não deve conter espaços ou pontuação. O atributo `displayName`, que aparece na interface do usuário, deve ser uma cadeia de caracteres XML válida.  
  
 Cada perfil contém três seções principais. Na ordem inversa, elas são da seguinte maneira:  
  
-   `<propertyTypes>` -uma lista de tipos que são usados para as propriedades definidas na seção de estereótipos.  
  
-   `<metaclasses>` -uma lista dos tipos de elemento de modelo ao qual os estereótipos deste perfil se aplicam, como IClass, IInterface, IOperation, IDependency.  
  
-   `<stereotypes>` -as definições estereótipas. Cada definição inclui os nomes e tipos de propriedades que são adicionados ao elemento de modelo de destino.  
  
#### <a name="property-types"></a>Tipos de propriedade  
 O `<propertyTypes>` seção declara uma lista de tipos que são usados para as propriedades no `<stereotypes>` seção. Há dois tipos de propriedade: externo e enumeração.  
  
 Um tipo externo declara o nome totalmente qualificado de um tipo .NET padrão:  
  
```  
<externalType name="System.String" />  
```  
  
 Um tipo de enumeração define um conjunto de valores literais:  
  
```  
<enumerationType name="PackageVisibility">  
  <enumerationLiterals>  
    <enumerationLiteral name="internal" displayName="internal"  />  
    <enumerationLiteral name="protectedinternal" displayName="protected internal" />  
  </enumerationLiterals>  
</enumerationType>  
```  
  
#### <a name="metaclasses"></a>Metaclasses  
 O `<metaclasses>` seção é uma lista dos tipos de elemento de modelo ao qual os estereótipos deste perfil podem ser definidos:  
  
```  
<metaclass   
      name="Microsoft.VisualStudio.Uml.Classes.IClass" />  
<metaclass  
      name="Microsoft.VisualStudio.Uml.Classes.IInterface" />  
<metaclass  
      name="Microsoft.VisualStudio.Uml.Components.IComponent" />  
```  
  
 Para obter a lista completa dos tipos de relação e de elemento de modelo que você pode usar como metaclasses, consulte [tipos de elemento de modelo](#Elements).  
  
#### <a name="stereotype-definition"></a>Definição de estereótipo  
 O `<stereotypes>` seção contém uma ou mais definições de estereótipo:  
  
```  
<stereotype name="CSharpClass" displayName="C# Class"> ...  
```  
  
 Cada estereótipo lista um ou mais elemento ou relação de tipos de modelo ao qual ele pode ser aplicado. Você pode fornecer o nome de um tipo base, para incluir todos os seus tipos derivados. Por exemplo, se você especificar `Microsoft.VisualStudio.Uml.Classes.IType`, o estereótipo pode ser aplicado a `IClass`, `IInterface`, `IEnumeration`e vários outros tipos de elemento.  
  
```  
<metaclasses>  
  <metaclassMoniker name=  
   "/CSharpProfile/Microsoft.VisualStudio.Uml.Classes.IClass" />  
</metaclasses>  
```  
  
 O `name` atributo de `metaclassMoniker` é um link para um elemento no `<metaClasses>` seção.  
  
> [!NOTE]
>  O nome do moniker deve começar com `/yourProfileName/`, onde `yourProfileName` é definido no `name` atributo do perfil ("CSharpProfile" neste exemplo). O moniker termina com o nome de uma das entradas na seção de metaclasses.  
  
 Cada estereótipo pode listar zero ou mais propriedades que ele adiciona a qualquer elemento de modelo ao qual ela é aplicada. O `<propertyType>` contém um link para um dos tipos que são definidos na `<propertyTypes>` seção. O link deve ser um `<externalTypeMoniker>` para se referir a um `<externalType>,` ou um `<enumerationTypeMoniker>` para se referir a um `<enumerationType>`. Novamente, o link começa com o nome do seu perfil.  
  
```  
  <properties>  
    <property name="IsStatic"   
            displayName="Is Static" defaultValue="false">  
      <propertyType>  
<externalTypeMoniker   
               name="/CSharpProfile/System.Boolean" />  
      </propertyType>  
    </property>  
    <property name="PackageVisibility"   
              displayName="Package Visibility"  
              defaultValue="internal">  
      <propertyType>  
        <enumerationTypeMoniker   
              name="/CSharpProfile/PackageVisibility"/>  
      </propertyType>  
    </property>  
  </properties>  
</stereotype>  
```  
  
##  <a name="Elements"></a> Tipos de elemento de modelo  
 O conjunto de tipos para os quais você pode definir estereótipos está listado no [tipos de elemento de modelo UML](../modeling/uml-model-element-types.md).  
  
## <a name="troubleshooting"></a>Solução de problemas  
 Meus estereótipos não aparecem em Meus modelos de UML.  
 Você precisa selecionar seu perfil em um pacote ou modelo. Os estereótipos aparecerão em elementos dentro do pacote ou modelo. Para obter mais informações, consulte [elementos de modelo de adicionar Estereótipos UML](../modeling/add-stereotypes-to-uml-model-elements.md).  
  
 O seguinte erro aparece quando abro um modelo UML: **VS1707: os seguintes perfis não podem ser carregados porque ocorreu um erro de serialização: MyProfile.profile**  
 1.  Verifique se a sintaxe XML básica do Profile está correta.  
  
2. Certifique-se de que cada nome de apelido esteja no formulário /ProfileName/NodeName. O profileName é o valor do atributo name no nó raiz de perfil. O nodeName é o valor do atributo de nome de uma metaclasse, externalType ou enumerationType.  
  
3. Certifique-se a sintaxe é conforme descrito aqui e conforme demonstrado _unidade_**: \Program Files\Microsoft Visual Studio [versão] \Common7\IDE\Extensions\Microsoft\Architecture Tools\UmlProfiles\\** .  
  
4. Desinstale a extensão com defeito. Sobre o **ferramentas** menu, clique em **extensões e atualizações**.  
  
   -   Se a extensão não aparecer, consulte o próximo item.  
  
5. Recompile o arquivo VSIX e abri-lo no Windows Explorer para reinstalá-lo. Reinicie o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
   A extensão não aparece no Gerenciador de extensões, mas ao tentar reinstalá-lo, a seguinte mensagem aparecerá: **a extensão já está instalada para todos os produtos aplicáveis.**  
   1.  Remover o arquivo de extensão de uma subpasta da *LocalAppData*\Microsoft\VisualStudio\\\Extensions\ [versão]  
  
   -   Para ver *LocalAppData*, você deve definir Mostrar arquivos e pastas ocultos na guia Exibir das opções de pasta do Windows Explorer.  
  
   -   *LocalAppData* normalmente é c:\Users\\*nome de usuário*\AppData\Local\  
  
6. Reinicie o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar estereótipos a elementos de modelo UML](../modeling/add-stereotypes-to-uml-model-elements.md)   
 [Personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md)   
 [Estereótipos padrão para modelos UML](../modeling/standard-stereotypes-for-uml-models.md)   
 [Exemplo: Elementos UML de cor por estereótipo](http://go.microsoft.com/fwlink/?LinkID=213841)   
 [Exemplo: Configuração de estereótipos, perfis XSD](http://go.microsoft.com/fwlink/?LinkID=213811)



