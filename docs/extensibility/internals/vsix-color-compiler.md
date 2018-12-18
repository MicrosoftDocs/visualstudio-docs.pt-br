---
title: Compilador de cor do VSIX | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 99395da7-ec34-491d-9baa-0590d23283ce
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 115f3a6c9d01d1e92a5eb7c840dfb17abcfd3c72
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31144324"
---
# <a name="vsix-color-compiler"></a>Compilador do VSIX cor
A ferramenta do compilador de cor de extensão do Visual Studio é um aplicativo de console que usa um arquivo. XML que representa as cores de temas existentes do Visual Studio e converte-o para um .pkgdef de arquivos para que essas cores podem ser usados no Visual Studio. Como é fácil comparar as diferenças entre arquivos. XML, essa ferramenta é útil para o gerenciamento de cores personalizadas no controle de origem. Ele também pode ser conectado em ambientes de desenvolvimento para que a saída da compilação é um arquivo de .pkgdef válido.  
  
 **Esquema XML do tema**  
  
 Um arquivo. XML de tema completa tem esta aparência:  
  
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
|GUID|[Obrigatório] GUID do tema (devem corresponder à formatação de GUID)|  
  
 Ao criar cores personalizadas para o Visual Studio, essas cores precisam ser definidos para os seguintes temas. Se nenhuma cor existir um tema específico, Visual Studio tenta carregar a ausência de cores do tema claro.  
  
|||  
|-|-|  
|**Nome do tema**|**GUID de tema**|  
|Claro|{de3dbbcd-f642-433c-8353-8f1df4370aba}|  
|Escuro|{1ded0138-47ce-435e-84ef-9ec1f439b749}|  
|Azul|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
|{1&gt;Alto Contraste&lt;1}|{a4d6a176-b948-4b29-8c66-53c97a1ed7d0}|  
  
 **Categoria**  
  
 O \<categoria > elemento define uma coleção de cores em um tema. Nomes de categoria fornecem agrupamento lógico e devem ser definidos como restrito possível. Uma categoria deve conter pelo menos um \<cor > elemento. Elementos de categoria são definidos como este:  
  
```xml  
<Category Name="name" GUID="guid">  
      <!-- one or more Color elements -->  
 </Category>  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Nome|[Obrigatório] O nome da categoria|  
|GUID|[Obrigatório] GUID da categoria (devem corresponder à formatação de GUID)|  
  
 **Cor**  
  
 O \<cor > elemento define uma cor para um componente ou o estado da interface do usuário. O esquema de nomenclatura preferencial para uma cor é [tipo de interface do usuário] [estado]. Não use a palavra "cores", pois é redundante. Uma cor claramente deve indicar o tipo de elemento e a situações ou "estado", para que a cor será aplicada. Uma cor não deve estar vazia e deve conter um ou ambos um \<em segundo plano > e \<em primeiro plano > elemento. Elementos de cor são definidos como este:  
  
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
  
 **Plano de fundo e/ou em primeiro plano**  
  
 O \<em segundo plano > e \<em primeiro plano > elementos definem o valor de uma cor e o tipo para o plano de fundo ou primeiro plano de um elemento de interface do usuário. Esses elementos não têm filhos.  
  
```xml  
<Background Type="type" Source="int" />  
<Foreground Type="type" Source="int" />  
```  
  
|||  
|-|-|  
|**Atributo**|**Definição**|  
|Tipo|[Obrigatório] O tipo da cor. Pode ser um dos seguintes:<br /><br /> *CT_INVALID:* a cor é inválido ou não foi definida.<br /><br /> *CT_RAW:* um valor ARGB bruto.<br /><br /> *CT_COLORINDEX:* NÃO USE.<br /><br /> *CT_SYSCOLOR:* uma cor de sistema do Windows em SysColor.<br /><br /> *CT_VSCOLOR:* __VSSYSCOLOREX uma cor Visual Studio.<br /><br /> *CT_AUTOMATIC:* a cor automática.<br /><br /> *CT_TRACK_FOREGROUND:* NÃO USE.<br /><br /> *CT_TRACK_BACKGROUND:* NÃO USE.|  
|Origem|[Obrigatório] O valor da cor em hexadecimal|  
  
 O esquema no atributo de tipo oferece suporte a todos os valores com suporte pela enumeração __VSCOLORTYPE. No entanto, é recomendável que você use somente CT_RAW e CT_SYSCOLOR.  
  
 **Todos juntos**  
  
 Este é um exemplo simples de um arquivo. XML de tema válido:  
  
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
|Sem nome (arquivo. xml)|Isso é o primeiro parâmetro sem nome e é o caminho para o arquivo XML para converter.|Necessária|  
|Sem nome (.pkgdef arquivo)|Este é o segundo parâmetro sem nome e é o caminho de saída para o arquivo .pkgdef gerado.<br /><br /> Padrão: \<nome do arquivo XML > .pkgdef|Opcional|  
|/noLogo|Defina esse sinalizador para de informações de produto e os direitos autorais da impressão.|Opcional|  
|/?|Imprima informações de Ajuda.|Opcional|  
|/help|Imprima informações de Ajuda.|Opcional|  
  
 **Exemplos**  
  
-   VsixColorCompiler D:\xml\colors.xml D:\pkgdef\colors.pkgdef  
  
-   /NoLogo VsixColorCompiler D:\xml\colors.xml  
  
## <a name="notes"></a>Observações  
  
-   Essa ferramenta requer que a versão mais recente do tempo de execução do VC + + esteja instalado.  
  
-   Há suporte para apenas arquivos únicos. Não há suporte para conversão em massa por meio de caminhos de pastas.  
  
## <a name="sample-output"></a>Saída de exemplo  
 O arquivo .pkgdef gerado pela ferramenta será semelhante ao abaixo de chaves:  
  
```  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\Environment]  
"Data"=hex:3a,00,00,00,0b,00,00,00,01,00,00,00,c3,d9,4e,62,fd,bd,fa,41,96,c3,7c,82,4e,a3,2e,3d,01,00,00,00,0c,00,00,00,41,63,74,69,76,65,42,6f,72,64,65,72,01,cc,ce,db,ff,01,33,31,24,ff  
  
[$RootKey$\Themes\{de3dbbcd-f642-433c-8353-8f1df4370aba}\TreeView]  
"Data"=hex:38,00,00,00,0b,00,00,00,01,00,00,00,8e,f0,ec,92,13,8b,f4,4c,99,e9,ae,26,92,38,21,85,01,00,00,00,0a,00,00,00,42,61,63,6b,67,72,6f,75,6e,64,01,f5,f5,f5,ff,01,1e,1e,1e,ff  
```