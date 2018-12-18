---
title: Estereótipos padrão para modelos UML | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- UML, stereotypes
- UML diagrams, stereotypes
ms.assetid: 8a8c2321-1cae-4ba8-bb9e-23495c3404d8
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 1fcc876a847429c0de9600a5a727b19334819119
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51763236"
---
# <a name="standard-stereotypes-for-uml-models"></a>Estereótipos padrão para modelos UML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode adicionar estereótipos a elementos de modelo UML para fornecer informações adicionais para o leitor, ou para processamento de máquina. Estereótipos são definidos nos perfis e cada perfil fornece o conjunto de estereótipos. Vários perfis são fornecidos com o Visual Studio. Você também pode definir seus próprios perfis que podem conter seus próprios estereótipos. Para obter mais informações, consulte [definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md).  
  
 Para ver quais versões do Visual Studio dão suporte a esse recurso, consulte [suporte de versão para a arquitetura e ferramentas de modelagem](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).  
  
## <a name="the-standard-profiles"></a>Os perfis padrão  
 Os seguintes perfis estão disponíveis em uma edição com suporte do Visual Studio, assim que ele foi instalado.  
  
|Perfil|Finalidade|  
|-------------|-------------|  
|[L2 de perfil padrão de UML](#L2)|Um conjunto padrão de estereótipos que pode ser usado para adicionar informações extras sobre um elemento ou um relacionamento.|  
|[L3 do perfil padrão de UML](#L3)|Um conjunto padrão de estereótipos que pode ser usado para adicionar informações extras sobre um elemento ou um relacionamento.|  
|[Perfil do c#](#NetProfile)|Se você pretende uma classe ou outro elemento em um modelo UML para representar o código do programa, você pode indicar isso aplicando um dos estereótipos do perfil do c#.<br /><br /> Essas estereótipos também adicionar propriedades aos elementos de modelo.|  
  
 Quando você cria um novo modelo UML, o UML padrão perfis L2 e L3 são vinculadas ao modelo, a menos que você remova os links.  
  
 Para usar os estereótipos em qualquer um desses perfis, primeiro você deve vincular o perfil a um pacote ou um modelo que contém os elementos que você deseja aplicá-las.  
  
#### <a name="to-link-a-profile-to-a-model-or-a-package"></a>Para vincular a um perfil para um modelo ou um pacote  
  
1.  Abra **Gerenciador de modelos UML**. Sobre o **arquitetura** , aponte para **Windows**e, em seguida, clique em **Gerenciador de modelos UML**.  
  
2.  Localize um pacote ou um modelo que contém todos os elementos aos quais deseja aplicar os estereótipos no perfil.  
  
3.  Clique com botão direito do pacote ou o modelo e, em seguida, clique em **propriedades**.  
  
4.  No **propriedades** janela, defina as **perfis** propriedade para os perfis que você deseja.  
  
#### <a name="to-remove-the-link-between-a-profile-and-a-model-or-package"></a>Para remover o vínculo entre um perfil e um modelo ou pacote  
  
1.  No Gerenciador de modelos UML, clique no modelo ou pacote e, em seguida, clique em **propriedades**.  
  
2.  Na janela Propriedades, defina as **perfis** propriedade vazia.  
  
    > [!NOTE]
    >  Você pode desvincular um perfil somente se nenhum dos elementos no modelo ou pacote usar estereótipos do perfil.  
  
#### <a name="to-apply-a-stereotype-to-a-model-element"></a>Para aplicar um estereótipo para um elemento de modelo  
  
1.  O elemento de modelo em um diagrama ou no botão direito do mouse **Gerenciador de modelos UML**e, em seguida, clique em **propriedades**.  
  
2.  Clique o **estereótipos** propriedade e selecione os estereótipos que você deseja aplicar.  
  
     Os estereótipos selecionados aparecem em «divisas» no elemento de modelo, para a maioria dos tipos de elemento.  
  
    > [!NOTE]
    >  Se você não conseguir ver a **estereótipos** propriedade, ou se o estereótipo desejado não aparecer, verifique se o elemento de modelo está dentro de um pacote ou um modelo ao qual o perfil apropriado foi vinculado.  
  
3.  Alguns estereótipos permitem que você defina os valores das propriedades adicionais para o elemento de modelo. Para ver essas propriedades, expanda o **estereótipos** propriedade.  
  
###  <a name="L2"></a> L2 de perfil padrão de UML  
 Os estereótipos seguir podem ser usados para especializar o significado dos elementos de modelo UML, a menos que o link para o perfil foi removido do modelo.  
  
 O significado exato dessas estereótipos é determinado por suas próprias convenções locais e por qualquer ferramenta que você pode usar para processar o modelo.  
  
|Estereótipo|Aplica-se a|Significado|  
|----------------|----------------|-------------|  
|auxiliar|Classe|Uma classe que dá suporte a outra classe, normalmente com a implementação de lógica adicional. A outra classe pode ter o estereótipo «foco».|  
|Chamada |Dependência|A classe do cliente chama as operações do fornecedor.|  
|criar|Dependência|A classe do cliente cria instâncias do fornecedor.|  
|criar|Mensagem|O remetente cria o receptor.|  
|criar|Operação|Esta operação é um construtor.|  
|derivar|Dependência|O elemento de cliente é computado totalmente ou parcialmente do fornecedor.|  
|destruir|Operação|A operação destrói a instância.|  
|documento|Artefato|Um «arquivo» que é não uma fonte ou um executável.|  
|entidade|Componente|O componente representa um conceito de negócios.|  
|executável|Artefato|Um executável «arquivo».|  
|Arquivo |Artefato|Um arquivo físico.|  
|foco|Classe|Uma classe que define a lógica de negócios principal, que há suporte para várias classes «auxiliar».|  
|estrutura|Pacote|Esse pacote define um padrão de design reutilizáveis.|  
|Implementar|Componente|A implementação de «especificação».|  
|implementationClass|Classe|A classe descreve uma implementação, e cada instância de tempo de execução tem uma classe de implementação fixa. Compare com «type».|  
|Criar uma instância|Dependência|O cliente cria instâncias do fornecedor.|  
|biblioteca|Artefato|Uma biblioteca «arquivo».|  
|metaclasse|Classe|As instâncias dessa classe também são classes.|  
|modelLibrary|Pacote|Contém elementos de modelo que se destina a ser reutilizado com a importação de pacotes. Normalmente definido como parte de um perfil e importados automaticamente pelo aplicativo do perfil.|  
|process|Componente|Um componente baseado em transação, ou um que executa um thread.|  
|realização|Componente de classe, Interface,|Descreve uma implementação.|  
|refinar|Dependência|A classe de cliente, do componente ou pacote fornece mais informações sobre a especificação ou design que o fornecedor.|  
|responsabilidade|Dependência|O comentário no final de fornecedor da dependência define as responsabilidades da classe de cliente ou componente.|  
|script|Artefato|Que é interpretado «souboru».|  
|Enviar|Dependência|A operação de origem envia o sinal de destino.|  
|serviço|Componente|Um componente sem monitoração de estado.|  
|origem|Artefato|Compilável «arquivo».|  
|especificação|Componente de classe, Interface,|Define o comportamento de um componente ou objeto sem definir como ele funciona internamente.|  
|subsistema|Componente|Uma parte de um sistema grande. Um subsistema de um diagrama de caso de uso é um componente com o estereótipo do subsistema.|  
|rastreamento|Dependência|O elemento de cliente é parte do design que percebe que o fornecedor. As duas extremidades dessa dependência costumam ser em modelos diferentes. Um desses modelos é uma realização dos outros.|  
|tipo|Classe|Especifica o comportamento de um objeto sem informando como ela é implementada. Um objeto é um membro de um tipo se ele está em conformidade com a especificação.|  
|utility|Classe|Uma coleção de funções estáticas. A classe não tem instâncias.|  
  
###  <a name="L3"></a> L3 do perfil padrão de UML  
 Os estereótipos seguir podem ser usados para especializar o significado dos elementos de modelo UML, a menos que o perfil foi desvinculado do modelo.  
  
 O significado exato dessas estereótipos é determinado por suas próprias convenções locais e por qualquer ferramenta que você pode usar para processar o modelo.  
  
|Estereótipo|Aplica-se a|Descrição|  
|----------------|----------------|-----------------|  
|buildComponent|Componente|Uma coleção de elementos usados para definir uma compilação.|  
|Metamodelo|Modelo|Define uma linguagem de modelagem, como uma variante do UML, ou uma linguagem específica de domínio.|  
|systemModel|Modelo|Um modelo que é uma coleção de modelos que se aplicam ao mesmo sistema, por exemplo, uma especificação, uma realização e relacionamentos de rastreamento entre eles.|  
  
##  <a name="NetProfile"></a> Perfil do c#  
 Os estereótipos definidos neste perfil permitem que você indicar que um elemento de modelo destina-se para a tradução para o código do programa. Cada estereótipo define propriedades adicionais que podem ser definidas no elemento de modelo.  
  
 Para disponibilizar essas estereótipos, vincule um modelo ou pacote para o perfil do c#. Em seguida, você pode aplicar os estereótipos a elementos de modelo no modelo ou pacote.  
  
 Os estereótipos disponíveis, os elementos aos quais elas se aplicam e as propriedades adicionais que eles se tornam disponíveis são resumidas na tabela a seguir.  
  
|Estereótipo|Aplica-se a|Propriedades|  
|----------------|----------------|----------------|  
|**Classe do c#**|Classe UML<br /><br /> Componente|**Atributos CLR**<br /><br /> **É parcial**<br /><br /> **Está lacrado**<br /><br /> **É estático**<br /><br /> **Não é seguro**<br /><br /> **Visibilidade do pacote**|  
|**Struct c#**|Classe UML<br /><br /> Componente|**Atributos CLR**<br /><br /> **É parcial**<br /><br /> **Não é seguro**<br /><br /> **Visibilidade do pacote**|  
|**Membros globais do c#**|Classe UML<br /><br /> Componente|**Atributos CLR**|  
|**Interface c#**|Interface UML|**Atributos CLR**<br /><br /> **É parcial**<br /><br /> **Visibilidade do pacote**|  
|**Enum do c#**|Enumeração de UML|**ClrAttributes**<br /><br /> **Tipo base**|  
|**Namespace do c#**|Pacote UML|**Atributos CLR**<br /><br /> **Nome de base**<br /><br /> **Usando namespaces**|  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar estereótipos a elementos de modelo UML](../modeling/add-stereotypes-to-uml-model-elements.md)   
 [Personalizar o modelo com perfis e estereótipos](../modeling/customize-your-model-with-profiles-and-stereotypes.md)   
 [Definir um perfil para estender UML](../modeling/define-a-profile-to-extend-uml.md)



