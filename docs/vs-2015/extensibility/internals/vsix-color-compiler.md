---
title: Compilador de cores do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 19ca749b3ddd2190fd667ddb6c96c2a88c557999
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788427"
---
# <a name="vsix-color-compiler"></a>Compilador de cores do VSIX
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

A ferramenta do compilador de cor de extensão do Visual Studio é um aplicativo de console que usa um arquivo. XML que representa as cores de temas do Visual Studio existentes e converte-o para um. pkgdef arquivo para que essas cores podem ser usados no Visual Studio. Como é fácil comparar as diferenças entre arquivos. XML, essa ferramenta é útil para o gerenciamento de cores personalizadas no controle de origem. Ele também pode ser conectado em ambientes de compilação para que a saída da compilação é um arquivo. pkgdef válido.  
  
 **Esquema XML de tema**  
  
 Um arquivo. XML de tema completo tem esta aparência:  
  
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
  
 O \<tema > elemento define um tema inteiro. Um tema deve conter pelo menos um \<categoria > elemento. Elementos de tema são definidos como este:  
  
```xml  
<Theme Name="name" GUID="guid">  
      <!-- one or more Category elements -->  
</Theme>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Nome|[Obrigatório] O nome do tema|  
|GUID|[Obrigatório] GUID do tema (deve corresponder à formatação de GUID)|  
  
 Ao criar cores personalizadas para o Visual Studio, essas cores precisam ser definidos para os seguintes temas. Se nenhum cores existirem para um tema específico, o Visual Studio tenta carregar a ausência de cores do tema no claro.  
  
|||  
|-|-|  
|**Nome do tema**|**GUID de tema**|  
|Claro|{de3dbbcd-f642-433c-8353-8f1df4370aba}|  
|Escuro|{1ded0138-47ce-435e-84ef-9ec1f439b749}|  
|Azul|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
|{1&gt;Alto Contraste&lt;1}|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
  
 **Categoria**  
  
 O \<categoria > elemento define uma coleção de cores em um tema. Os nomes de categoria fornecem agrupamentos lógicos e devem ser definidos como restrito quanto possível. Uma categoria deve conter pelo menos um \<cor > elemento. Elementos de categoria são definidos como este:  
  
```xml  
<Category Name="name" GUID="guid">  
      <!-- one or more Color elements -->  
 </Category>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Nome|[Obrigatório] O nome da categoria|  
|GUID|[Obrigatório] GUID da categoria (deve corresponder à formatação de GUID)|  
  
 **Cor**  
  
 O \<cor > elemento define uma cor de um componente ou o estado da interface do usuário. O esquema de nomenclatura preferencial para uma cor é [tipo de interface do usuário] [estado]. Não use a palavra "color", pois ela é redundante. Uma cor claramente deve indicar o tipo de elemento e a situações ou "estado", para o qual a cor será aplicada. Uma cor não pode estar vazia e deve conter uma ou ambas uma \<plano de fundo > e \<em primeiro plano > elemento. Elementos de cor são definidos como este:  
  
```xml  
<Color Name="name">  
        <Background /> <!-- zero or one Background element -->  
        <Foreground /> <!-- zero or one Foreground element -->  
 </Color>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Nome|[Obrigatório] O nome da cor|  
  
 **Em segundo plano e/ou em primeiro plano**  
  
 O \<plano de fundo > e \<em primeiro plano > elementos definem o valor de uma cor e o tipo para o plano de fundo ou primeiro plano de um elemento de interface do usuário. Esses elementos não têm nenhum filho.  
  
```xml  
<Background Type="type" Source="int" />  
<Foreground Type="type" Source="int" />  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Tipo|[Obrigatório] O tipo da cor. Ele pode ser um dos seguintes:<br /><br /> *CT_INVALID:* a cor é inválido ou não foi definida.<br /><br /> *CT_RAW:* um valor ARGB bruto.<br /><br /> *CT_COLORINDEX:* NÃO USE.<br /><br /> *CT_SYSCOLOR:* uma cor de sistema do Windows em SysColor.<br /><br /> *CT_VSCOLOR:* uma cor do Visual Studio em __VSSYSCOLOREX.<br /><br /> *CT_AUTOMATIC:* a cor automática.<br /><br /> *CT_TRACK_FOREGROUND:* NÃO USE.<br /><br /> *CT_TRACK_BACKGROUND:* NÃO USE.|  
|Origem|[Obrigatório] O valor da cor em hexadecimal|  
  
 Todos os valores com suporte pela enumeração __VSCOLORTYPE são compatíveis com o esquema no atributo de tipo. No entanto, é recomendável que você use apenas CT_RAW e CT_SYSCOLOR.  
  
 **Todos juntos**  
  
 Este é um exemplo simple de um arquivo de tema válido. XML:  
  
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
  
 VsixColorCompiler \<arquivo XML > \<arquivo PkgDef > \<Args opcional >  
  
 **Argumentos**  
  
||||  
|-|-|-|  
|**Nome do comutador**|**Observações**|**Obrigatório ou opcional**|  
|Sem nome (arquivo. xml)|Isso é o primeiro parâmetro sem nome e é o caminho para o arquivo XML a ser convertido.|Necessária|  
|Sem nome (arquivo. pkgdef)|Isso é o segundo parâmetro sem nome e é o caminho de saída para o arquivo. pkgdef gerado.<br /><br /> Padrão: \<XML Filename >. pkgdef|Opcional|  
|/noLogo|Definir esse sinalizador interrompe as informações de produto e os direitos autorais de impressão.|Opcional|  
|/?|Imprima informações de Ajuda.|Opcional|  
|/help|Imprima informações de Ajuda.|Opcional|  
  
 **Exemplos**  
  
-   VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef  
  
-   /NoLogo VsixColorCompiler D:\xml\colors.xml  
  
## <a name="notes"></a>Observações  
  
-   Essa ferramenta exige que a versão mais recente do tempo de execução do VC + + ser instalado.  
  
-   Há suporte para apenas arquivos únicos. Não há suporte para conversão em massa por meio de caminhos de pasta.  
  
## <a name="sample-output"></a>Saída de exemplo  
 O arquivo. pkgdef gerado pela ferramenta será semelhante ao abaixo de chaves:  
  
```  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]  
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff  
  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]  
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff  
```

