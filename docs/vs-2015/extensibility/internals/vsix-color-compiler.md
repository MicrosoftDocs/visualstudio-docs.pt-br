---
title: Compilador de cores do VSIX | Microsoft Docs
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c92fb2ad45bc0fb09c7e9bd8e87db38c13a99736
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546738"
---
# <a name="vsix-color-compiler"></a>Compilador de cores do VSIX
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A ferramenta de compilador de cores de extensão do Visual Studio é um aplicativo de console que usa um arquivo. XML que representa as cores dos temas existentes do Visual Studio e o faz em um arquivo. pkgdef para que essas cores possam ser usadas no Visual Studio. Como é fácil comparar as diferenças entre arquivos. xml, essa ferramenta é útil para gerenciar cores personalizadas no controle do código-fonte. Ele também pode ser conectado a ambientes de compilação para que a saída da compilação seja um arquivo. pkgdef válido.  
  
 **Esquema XML do tema**  
  
 Um arquivo Theme. XML completo tem a seguinte aparência:  
  
```xml  
<Themes>  
      <!—one or Theme elements -->  
      <Theme>  
        <!-- one or more Category elements -->  
        <Category>  
          <!-- one or more Color elements -->  
          <Color>  
            <!-- zero or one Background element -->  
            <Background />  
            <!-- zero or one Foreground element -->  
            <Foreground />  
          </Color>  
        </Category>  
      </Theme>  
</Themes>  
```  
  
 **Tema**  
  
 O \<Theme> elemento define um tema inteiro. Um tema deve conter pelo menos um \<Category> elemento. Elementos de tema são definidos desta forma:  
  
```xml  
<Theme Name="name" GUID="guid">  
      <!-- one or more Category elements -->  
</Theme>  
```  
  
|**Atributo**|**Definição**|  
|-|-|  
|Nome|Necessária O nome do tema|  
|GUID|Necessária O GUID do tema (deve corresponder à formatação de GUID)|  
  
 Ao criar cores personalizadas para o Visual Studio, essas cores precisam ser definidas para os temas a seguir. Se não existir nenhuma cor para um tema específico, o Visual Studio tentará carregar as cores ausentes do tema claro.  
  
|**Nome do tema**|**GUID do tema**|  
|-|-|  
|Claro|{de3dbbcd-f642-433c-8353-8f1df4370aba}|  
|Escuro|{1ded0138-47ce-435e-84ef-9ec1f439b749}|  
|Azul|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
|Alto Contraste|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
  
 **Categoria**  
  
 O \<Category> elemento define uma coleção de cores em um tema. Os nomes de categoria fornecem agrupamentos lógicos e devem ser definidos da forma mais restrita possível. Uma categoria deve conter pelo menos um \<Color> elemento. Os elementos de categoria são definidos desta forma:  
  
```xml  
<Category Name="name" GUID="guid">  
      <!-- one or more Color elements -->  
 </Category>  
```  
    
|**Atributo**|**Definição**|  
|-|-|  
|Nome|Necessária O nome da categoria|  
|GUID|Necessária O GUID da categoria (deve corresponder à formatação de GUID)|  
  
 **Cor**  
  
 O \<Color> elemento define uma cor para um componente ou estado da interface do usuário. O esquema de nomenclatura preferencial para uma cor é [tipo de interface do usuário] [estado]. Não use a palavra "Color", pois ela é redundante. Uma cor deve indicar claramente o tipo de elemento e as situações, ou "estado", para os quais a cor será aplicada. Uma cor não deve estar vazia e deve conter um ou ambos os \<Background> \<Foreground> elementos e. Os elementos de cor são definidos da seguinte maneira:  
  
```xml  
<Color Name="name">  
        <Background /> <!-- zero or one Background element -->  
        <Foreground /> <!-- zero or one Foreground element -->  
 </Color>  
```  
  
|**Atributo**|**Definição**|  
|-|-|  
|Nome|Necessária O nome da cor|  
  
 **Plano de fundo e/ou primeiro plano**  
  
 Os \<Background> \<Foreground> elementos e definem o valor e o tipo de uma cor para o plano de fundo ou o primeiro plano de um elemento de interface do usuário. Esses elementos não têm filhos.  
  
```xml  
<Background Type="type" Source="int" />  
<Foreground Type="type" Source="int" />  
```  
  
|**Atributo**|**Definição**|  
|-|-|  
|Type|Necessária O tipo da cor. Pode ser um dos seguintes:<br /><br /> *CT_INVALID:* A cor é inválida ou não está definida.<br /><br /> *CT_RAW:* Um valor de ARGB bruto.<br /><br /> *CT_COLORINDEX:* NÃO USE.<br /><br /> *CT_SYSCOLOR:* Uma cor de sistema do Windows de SysColor.<br /><br /> *CT_VSCOLOR:* Uma cor do Visual Studio de __VSSYSCOLOREX.<br /><br /> *CT_AUTOMATIC:* A cor automática.<br /><br /> *CT_TRACK_FOREGROUND:* NÃO USE.<br /><br /> *CT_TRACK_BACKGROUND:* NÃO USE.|  
|Fonte|Necessária O valor da cor representada em hexadecimal|  
  
 Todos os valores compatíveis com a enumeração __VSCOLORTYPE são suportados pelo esquema no atributo Type. No entanto, recomendamos que você use apenas CT_RAW e CT_SYSCOLOR.  
  
 **Todos juntos**  
  
 Este é um exemplo simples de um arquivo Theme. XML válido:  
  
```xml  
<Themes>  
  <Theme Name="Light" GUID="{de3dbbcd-f642-433c-8353-8f1df4370aba}">  
    <Category Name="MyCategory" GUID="{0A96238B-70CE-4479-9170-EECEAA3FCD58}">  
      <Color Name="MyActiveBorder">  
        <Background Type="CT_RAW" Source="FFCCCEDB" />  
      </Color>  
    </Category>  
  </Theme>  
</Themes>  
```  
  
## <a name="how-to-use-the-tool"></a>Como usar a ferramenta  
 **Sintaxe**  
  
 VsixColorCompiler \<XML file> \<PkgDef file>\<Optional Args>  
  
 **Argumentos**  
  
|**Nome do comutador**|**Observações**|**Obrigatório ou opcional**|  
|-|-|-|  
|Sem nome (arquivo. xml)|Esse é o primeiro parâmetro sem nome e é o caminho para o arquivo XML a ser convertido.|Obrigatório|  
|Sem nome (arquivo. pkgdef)|Esse é o segundo parâmetro sem nome e é o caminho de saída para o arquivo. pkgdef gerado.<br /><br /> Padrão: \<XML Filename> . pkgdef|Opcional|  
|/noLogo|A definição desse sinalizador impede que as informações de produtos e direitos autorais sejam impressas.|Opcional|  
|/?|Imprimir informações de ajuda.|Opcional|  
|/help|Imprimir informações de ajuda.|Opcional|  
  
 **Exemplos**  
  
- VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef  
  
- VsixColorCompiler D:\xml\colors.xml/noLogo  
  
## <a name="notes"></a>Observações  
  
- Essa ferramenta requer que a versão mais recente do tempo de execução do VC + + seja instalada.  
  
- Somente arquivos únicos têm suporte. Não há suporte para conversão em massa via caminhos de pasta.  
  
## <a name="sample-output"></a>Saída de exemplo  
 O arquivo. pkgdef gerado pela ferramenta será semelhante às chaves abaixo:  
  
```  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]  
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff  
  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]  
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff  
```
