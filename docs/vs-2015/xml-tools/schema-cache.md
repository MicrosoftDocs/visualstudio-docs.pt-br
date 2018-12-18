---
title: Cache de esquema | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 35a7fcad-f3bf-4a96-9008-4306e7276223
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 071ae9f75ab48a2fbabba7c272ad542f59e9e8be
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49833142"
---
# <a name="schema-cache"></a>Cache de esquema
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]


O editor XML fornece um cache de esquema localizado no diretório de %InstallRoot% \ \ esquemas XML. O cache de esquema é global para todos os usuários em seu computador e inclui esquemas XML padrão que são usados para validação do IntelliSense e de documento XML.  

 O editor XML também pode encontrar esquemas localizadas na solução, os esquemas especificados na **esquemas** campo do documento **Properties** janela e esquemas identificados pelo `xsi:schemaLocation` e `xsi:noNamespaceSchemaLocation`atributos.  

 A tabela a seguir descreve os esquemas que são instalados com o editor XML.  


|     Filename      |                                                      Descrição                                                      |
|-------------------|-----------------------------------------------------------------------------------------------------------------------|
|    catalog.xsd    |             Esquema para arquivos de catálogo do editor XML. Para obter informações sobre catálogos do esquema, consulte abaixo.             |
| DotNetConfig.xsd  |                 Esquema para arquivos Web. config, "<http://schemas.microsoft.com/.NETConfiguration/v2.0>".                 |
|    msbuild.xsd    |              Esquema para os arquivos MSBuild, "<http://schemas.microsoft.com/developer/msbuild/2003>".              |
|    msdata.xsd     | Para anotações esquema XSD adicionados pela classe de <xref:System.Data.DataSet> , “urna: esquema-Microsoft-COM: XML-msdata”. |
|     msxsl.xsd     |                  Esquema para extensões do bloco de script do Microsoft XSLT, urna: esquema-Microsoft-COM: XSLT.                   |
| SnippetFormat.xsd |                 Esquema para os arquivos XML de snippet de código. Para exemplos, consulte %InstallDir% \ \ VC# expansões.                 |
|    Soap1.1.xsd    |            Esquema para Simple Object Access Protocol (SOAP) 1.1, http://schemas.xmlsoap.org/soap/envelope/.            |
|    Soap1.2.xsd    |                                     Esquema para o protocolo de acesso simples 1,2 do objeto.                                     |
| SiteMapSchema.xsd |            Esquema para o arquivo XML do mapa do site ASP.NET, "<http://schemas.microsoft.com/AspNet/SiteMap-File-1.0>".             |
|     wsdl.xsd      |                    Esquema para o Web Service Description Language http://schemas.xmlsoap.org/wsdl/.                     |
|     xenc.xsd      |                            Esquema para a criptografia de XML, http://www.w3.org/2000/09/xmldsig#.                             |
|     xhtml.xsd     |                                    Esquema para XHTML http://www.w3.org/1999/xhtml.                                     |
|     xlink.xsd     |                                  Esquema para XLink1.0, http://www.w3.org/1999/xlink.                                   |
|      xml.xsd      |              Esquema que descreve os atributos XML: space e XML: lang, http://www.w3.org/XML/1998/namespace.               |
|    xmlsig.xsd     |                        Esquema para assinaturas digitais XML, http://www.w3.org/2000/09/xmldsig#.                         |
|   xsdschema.xsd   |                            Esquema que descreve o XSD em si, http://www.w3.org/2001/XMLSchema.                            |
|     xslt.xsd      |                           Esquema XML para transformações, http://www.w3.org/1999/XSL/Transform.                            |

## <a name="updating-schemas-in-the-cache"></a>Atualizando esquemas no cache  
 O editor carrega o diretório de cache do esquema quando o pacote de editor XML é carregado e observações para todas as alterações ao executar. Se um esquema foi adicionado, é carregado automaticamente em um índice de memória conhecidos de esquemas. Se um esquema foi removido, ele é removido automaticamente de índice de memória. Se um esquema foi atualizado, invalida automaticamente o cache de memória deste esquema.  

> [!NOTE]
>  Porque o diretório de cache de esquema é global para seu computador, você só deve adicionar os esquemas aqui e padrões que são úteis para todos os projetos do Visual Studio que podem ser criados no seu computador.  

 O editor XML também suporta qualquer número de arquivos de catálogo de esquema no diretório de cache de esquema. Cataloga de esquema podem apontar para outros locais para esquemas que você deseja sempre o editor para saber. O arquivo de catalog.xsd define o formato para o arquivo de catálogo e é incluído no diretório de cache de esquema. O arquivo de catalog.xml é o catálogo padrão e contém links para outros esquemas no %InstallDir%. A seguir está uma amostragem do arquivo de catalog.xml:  

```  
<SchemaCatalog xmlns="http://schemas.microsoft.com/xsd/catalog">  
  <Schema href="%InstallDir%/help/schemas/Favorites.xsd" targetNamespace="urn:Favorites-Schema"/>  
  <Schema href="%InstallDir%/help/schemas/Links.xsd" targetNamespace="urn:Links-Schema"/>  
  <Schema href="%InstallDir%/help/schemas/MyHelp.xsd" targetNamespace="urn:VSHelp-Schema"/>  
</SchemaCatalog>  
```  

 O atributo de `href` pode ser qualquer URL do caminho de arquivo ou de HTTP que aponta para o esquema. O caminho de arquivo pode ser relativo ao documento de catálogo. Os seguintes variáveis, delimitados por %%, são reconhecidos pelo editor e serão expandidos no caminho:  

- InstallDir  

- Sistema  

- ProgramFiles  

- Programas  

- CommonProgramFiles  

- ApplicationData  

- CommonApplicationData  

- LCID  

  O documento de catálogo pode incluir um elemento de `Catalog` , que aponta para outros catálogos. Você pode usar o elemento de `Catalog` para apontar para um catálogo central compartilhado por sua equipe ou empresa, ou um catálogo online compartilhado com seus sócios de negócios. O atributo de `href` é a URL do caminho de arquivo ou de HTTP para os outros catálogos. A seguir está um exemplo de elemento de `Catalog` :  

```  
<Catalog href="file://c:/xcbl/xcblCatalog.xml"/>  
```  

 O catálogo também pode controlar como os esquemas são associados com os documentos XML usando o elemento especial de `Association` . Esse elemento associa os esquemas que não têm namespace de destino com um extensão de arquivo específico, que pode ser útil porque o editor XML não faz nenhuma associação automática de esquemas que não possuem um atributo de `targetNamespace` . No exemplo a seguir o elemento de `Association` associa o esquema de dotNetConfig com todos os arquivos que possuem a extensão do arquivo de configuração”: “  

```  
<Association extension="config" schema="%InstallDir%/xml/schemas/dotNetConfig.xsd"/>  
```  

## <a name="localized-schemas"></a>Esquemas localizados  
 Em muitos casos o arquivo de catalog.xml não contém entradas para esquemas localizados. Você pode adicionar as entradas adicionais para o arquivo de catalog.xml apontando para o diretório encontrado de esquema.  

 No exemplo a seguir um novo elemento de `Schema` foi criado que usa a variável de %LCID% para apontar para o esquema encontrado.  

```  
<Schema href="%InstallRoot%/Common7/IDE/Policy/Schemas/%LCID%/TDLSchema.xsd"  
  targetNamespace="http://www.microsoft.com/schema/EnterpriseTemplates/TDLSchema"/>  
```  

## <a name="changing-the-location-of-the-schema-cache"></a>Alterando o local de cache do esquema  
 Você pode personalizar o local para o cache de esquema usando o **Miscelânea** página de opções. Se você tiver um diretório de esquemas favoritos, o editor pode ser configurado para usar esses esquemas.  

> [!NOTE]
>  Essa alteração afeta somente o usuário atual Visual Studio.  

#### <a name="to-change-the-schema-cache-location"></a>Para alterar o local de cache do esquema  

1.  No menu **Ferramentas**, selecione **Opções**.  

2.  Expandir **Editor de texto**, expanda **XML**e, em seguida, clique em **diversos**.  

3.  Clique o **navegue** botão a **esquemas** campo.  

4.  Selecione a pasta de cache de esquema e clique em **Okey**.  

#### <a name="to-add-another-directory-of-common-schemas"></a>Para adicionar um diretório diferente de esquemas comuns  

1.  Edite o arquivo de catalog.xml no diretório de cache do editor XML.  

2.  Adicionar um novo elemento de `<Catalog href="…"/>` que aponta para o diretório de esquemas adicionais.  

3.  Salve as alterações.  

     O catálogo é recarregado automaticamente.  

## <a name="see-also"></a>Consulte também  
 [Editor de XML](../xml-tools/xml-editor.md)



