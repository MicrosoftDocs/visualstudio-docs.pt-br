---
title: Adicionar Propriedade de rastreamento à definição de DSL
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- tracking properties [Domain-Specific Language Tools], walkthrough
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d80a8d2ab334495daac4d82fe5c8faa2ad04683d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544242"
---
# <a name="add-a-tracking-property-to-a-domain-specific-language-definition"></a>Adicionar uma propriedade de controle a uma definição de Linguagem Específica de Domínio

Este tutorial mostra como adicionar uma propriedade de rastreamento a um modelo de domínio.

Uma propriedade de *domínio de rastreamento* é uma propriedade que pode ser atualizada pelo usuário, mas que tem um valor padrão que é calculado usando os valores de outros elementos ou propriedades de domínio.

Por exemplo, no Ferramentas de Linguagem Específica de Domínio (ferramentas DSL), a propriedade nome de exibição de uma classe de domínio tem um valor padrão que é calculado usando o nome da classe de domínio, mas um usuário pode alterar o valor em tempo de design ou redefini-lo para o valor calculado.

Neste tutorial, você cria uma DSL (linguagem específica de domínio) que tem uma propriedade de rastreamento de namespace que tem um valor padrão baseado na propriedade de namespace padrão do modelo. Para obter mais informações sobre propriedades de rastreamento, consulte [definindo propriedades de rastreamento](https://msdn.microsoft.com/0538b0e4-6221-4e7d-911a-b92cd622f0be).

- As ferramentas DSL dão suporte ao rastreamento de descritores de propriedade. No entanto, o designer de DSL não pode ser usado para adicionar uma propriedade de controle a um idioma. Portanto, você deve adicionar um código personalizado para definir e implementar a propriedade de controle.

  Uma propriedade de rastreamento tem dois Estados: rastreamento e atualizado pelo usuário. As propriedades de rastreamento têm os seguintes recursos:

- Quando estiver no estado de rastreamento, o valor da propriedade de rastreamento será calculado e o valor será atualizado conforme outras propriedades no modelo mudarem.

- Quando estiver atualizado pelo estado do usuário, o valor da propriedade de rastreamento manterá o valor para o qual o usuário definiu a propriedade pela última vez.

- Na janela **Propriedades** , o comando **Redefinir** para a propriedade de rastreamento só é habilitado quando a propriedade está no estado atualizado por usuário. O comando **Reset** define o estado da propriedade de rastreamento como rastreamento.

- Na janela **Propriedades** , quando a propriedade de rastreamento está no estado de rastreamento, seu valor é exibido em uma fonte regular.

- Na janela **Propriedades** , quando a propriedade de rastreamento está no estado atualizado por usuário, seu valor é exibido em uma fonte em negrito.

## <a name="prerequisites"></a>Pré-requisitos

Antes de poder iniciar este passo a passos, você deve primeiro instalar estes componentes:

| | |
|-|-|
| Visual Studio | [http://go.microsoft.com/fwlink/?LinkID=185579](https://visualstudio.microsoft.com/) |
| [!INCLUDE[vssdk_current_short](../modeling/includes/vssdk_current_short_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185580](/azure/devops/integrate/index?view=azure-devops&viewFallbackFrom=vsts) |
| [!INCLUDE[dsl](../modeling/includes/dsl_md.md)] | [http://go.microsoft.com/fwlink/?LinkID=185581](https://code.msdn.microsoft.com/site/search?query=%22Modeling%20SDK%22&f%5B0%5D.Value=%22Modeling%20SDK%22&f%5B0%5D.Type=SearchText&ac=5) |

## <a name="create-the-project"></a>Criar o projeto

1. Crie um projeto Designer de Linguagem Específica de Domínio. Nomeie-o como `TrackingPropertyDSL`.

2. No **Assistente de designer de linguagem específica de domínio**, defina as seguintes opções:

    1. Selecione o modelo **MinimalLanguage** .

    2. Use o nome padrão para a linguagem específica do domínio, `TrackingPropertyDSL` .

    3. Defina a extensão para os arquivos de modelo como `trackingPropertyDsl` .

    4. Use o ícone de modelo padrão para os arquivos de modelo.

    5. Defina o nome do produto como `Product Name` .

    6. Defina o nome da empresa como `Company Name` .

    7. Use o valor padrão para o namespace raiz para projetos na solução, `CompanyName.ProductName.TrackingPropertyDSL` .

    8. Permita que o assistente crie um arquivo de chave de nome forte para seus assemblies.

    9. Examine os detalhes da solução e clique em **concluir** para criar o projeto de definição de DSL.

## <a name="customize-the-default-dsl-definition"></a>Personalizar a definição de DSL padrão
 Nesta seção, você personaliza a definição de DSL para conter os seguintes itens:

- Uma propriedade de rastreamento de namespace para cada elemento do modelo.

- Uma propriedade booleana IsNamespaceTracking para cada elemento do modelo. Essa propriedade indicará se a propriedade de rastreamento está no estado de rastreamento ou no estado atualizado pelo usuário.

- Uma propriedade de namespace padrão para o modelo. Essa propriedade será usada para calcular o valor padrão da propriedade de rastreamento de namespace.

- Uma propriedade calculada CustomElements para o modelo. Essa propriedade indicará a proporção de elementos que têm um namespace personalizado.

### <a name="to-add-the-domain-properties"></a>Para adicionar as propriedades de domínio

1. No designer de DSL, clique com o botão direito do mouse na classe de domínio **ExampleModel** , aponte para **Adicionar**e clique em **nomedodomínio**.

    1. Nomeie a nova propriedade `DefaultNamespace` .

    2. Na janela **Propriedades** da nova propriedade, defina **valor padrão** como `DefaultNamespace` e defina **tipo** como **cadeia de caracteres**.

2. Para a classe de domínio **ExampleModel** , adicione uma propriedade de domínio chamada `CustomElements` .

     Na janela **Propriedades** da nova propriedade, defina **tipo** como **calculado**.

3. Para a classe de domínio **exampleelement** , adicione uma propriedade de domínio chamada `Namespace` .

     Na janela **Propriedades** da nova propriedade, defina **é navegável** como **false**e defina **tipo** como **CustomStorage**.

4. Para a classe de domínio **exampleelement** , adicione uma propriedade de domínio chamada `IsNamespaceTracking` .

     Na janela **Propriedades** da nova propriedade, defina **é navegável** como **false**, defina **valor padrão** como `true` e defina **tipo** como **booliano**.

### <a name="to-update-the-diagram-elements-and-dsl-details"></a>Para atualizar os elementos de diagrama e os detalhes de DSL

1. No designer de DSL, clique com o botão direito do mouse na forma de geometria **ExampleShape** , aponte para **Adicionar**e clique em **decorador de texto**.

    1. Nomeie o novo decorador de texto `NamespaceDecorator` .

    2. Na janela **Propriedades** do decorador de texto, defina **Position** como **InnerBottomLeft**.

2. No designer de DSL, selecione a linha que conecta a classe **exampleelement** à forma **ExampleShape** .

    1. Na janela **detalhes de DSL** , selecione a guia **mapas de decoradores** .

    2. Na lista **decoradores** , selecione **NamespaceDecorator**, marque a caixa de seleção e, na lista **propriedade de exibição** , selecione **namespace**.

3. No **Gerenciador de DSL**, expanda a pasta **classes de domínio** , clique com o botão direito do mouse no nó **Exemploelement** e clique em **Adicionar novo tipo de domínio descritor**.

    1. Expanda o nó **exampleelement** e selecione o nó **descritor de tipo personalizado (descritor de tipo de domínio)** .

    2. Na janela **Propriedades** do descritor de tipo de domínio, defina **código personalizado** como **true**.

4. No **Gerenciador de DSL**, selecione o nó **comportamento de serialização XML** .

    1. Na janela **Propriedades** , defina **pós-carregamento personalizado** como **verdadeiro**.

## <a name="transform-templates"></a>Transformar modelos

Agora que você definiu as classes de domínio e as propriedades de sua DSL, é possível verificar se a definição de DSL pode ser transformada corretamente para regenerar o código para o seu projeto.

1. Na barra de ferramentas **Gerenciador de soluções** , clique em **transformar todos os modelos**.

2. O sistema regenera o código para a solução e salva DslDefinition. DSL. Para obter informações sobre o formato XML dos arquivos de definição, consulte [o arquivo DslDefinition. DSL](../modeling/the-dsldefinition-dsl-file.md).

## <a name="create-files-for-custom-code"></a>Criar arquivos para código personalizado

Quando você transforma todos os modelos, o sistema gera o código-fonte que define a linguagem específica do domínio nos projetos DSL e DslPackage. Para que você possa evitar interferir no texto gerado, escreva seu código personalizado em arquivos que são diferentes dos arquivos de código gerados.

Você deve fornecer o código para manter o valor e o estado da sua propriedade de controle. Para ajudá-lo a distinguir o código personalizado do código gerado e para evitar conflitos de nomenclatura de arquivo, coloque os arquivos de código personalizados em uma subpasta separada.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **DSL** , aponte para **Adicionar**e clique em **nova pasta**. Nomeie a nova pasta `CustomCode` .

2. Clique com o botão direito do mouse na pasta New **CustomCode** , aponte para **Adicionar**e clique em **novo item**.

3. Selecione o modelo de **arquivo de código** , defina o **nome** como e `NamespaceTrackingProperty.cs` clique em **OK**.

     O arquivo NamespaceTrackingProperty.cs é criado e aberto para edição.

4. Na pasta, crie os seguintes arquivos de código: `ExampleModel.cs,``HelperClasses.cs` , `Serialization.cs` e `TypeDescriptor.cs` .

5. No projeto **DslPackage** , crie também uma `CustomCode` pasta e adicione a ela um arquivo de `Package.cs` código.

## <a name="add-helper-classes-to-support-tracking-properties"></a>Adicionar classes auxiliares para dar suporte a propriedades de acompanhamento

Para o arquivo HelperClasses.cs, adicione as `TrackingHelper` classes e da `CriticalException` seguinte maneira. Você fará referência a essas classes mais adiante neste guia.

1. Adicione o código a seguir ao arquivo HelperClasses.cs.

    ```csharp
    using System;
    using System.Collections;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        internal static class TrackingHelper
        {
            /// <summary>Notify each model element in a collection that a tracked
            /// property has changed.</summary>
            /// <param name="store">The store for the model.</param>
            /// <param name="collection">The collection of model elements that
            /// contain the tracking property.</param>
            /// <param name="propertyId">The ID of the tracking property.</param>
            /// <param name="trackingPropertyId">The ID of the property that
            /// indicates whether the tracking property is tracking.</param>
            internal static void UpdateTrackingCollectionProperty(
                Store store,
                IEnumerable collection,
                Guid propertyId,
                Guid trackingPropertyId)
            {
                DomainPropertyInfo propInfo =
                    store.DomainDataDirectory.GetDomainProperty(propertyId);

                DomainPropertyInfo trackingPropInfo =
                    store.DomainDataDirectory.GetDomainProperty(trackingPropertyId);

                Debug.Assert(propInfo != null);
                Debug.Assert(trackingPropInfo != null);
                Debug.Assert(trackingPropInfo.PropertyType.Equals(typeof(bool)),
                    "Tracking property not specified as a boolean");

                foreach (ModelElement element in collection)
                {
                    // If the tracking property is currently tracking, then notify
                    // it that the tracked property has changed.
                    bool isTracking = (bool)trackingPropInfo.GetValue(element);
                    if (isTracking)
                    {
                        propInfo.NotifyValueChange(element);
                    }
                }
            }
        }

        /// <summary>Helper class to flag critical exceptions from ones that are
        /// safe to ignore.</summary>
        internal static class CriticalException
        {
            /// <summary>Gets whether an exception is critical and can not be
            /// ignored.</summary>
            /// <param name="ex">The exception to check.</param>
            /// <returns>True if the exception is critical.</returns>
            internal static bool IsCriticalException(Exception ex)
            {
                if (ex is NullReferenceException
                    || ex is StackOverflowException
                    || ex is OutOfMemoryException
                    || ex is System.Threading.ThreadAbortException)
                    return true;

                if (ex.InnerException != null)
                    return IsCriticalException(ex.InnerException);

                return false;
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-custom-type-descriptor"></a>Adicionar código personalizado para o descritor de tipo personalizado

Implemente o `GetCustomProperties` método para o descritor de tipo para a `ExampleModel` classe de domínio.

> [!NOTE]
> O código que as ferramentas de DSL geram para o descritor de tipo personalizado para `ExampleModel` chamadas `GetCustomProperties` ; no entanto, as ferramentas de DSL não geram código que implementa o método.

A definição desse método cria o descritor de propriedade de rastreamento para a propriedade de rastreamento de namespace. Além disso, o fornecimento de atributos para a propriedade de controle permite que a janela **Propriedades** exiba a propriedade corretamente.

### <a name="to-modify-the-type-descriptor-for-the-examplemodel-domain-class"></a>Para modificar o descritor de tipo para a classe de domínio ExampleModel

1. Adicione o código a seguir ao arquivo TypeDescriptor.cs.

    ```csharp
    using System;
    using System.ComponentModel;
    using Microsoft.VisualStudio.Modeling;
    using Microsoft.VisualStudio.Modeling.Design;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the custom type descriptor for the ExampleElement domain class, add
        // the GetCustomProperties method.
        public partial class ExampleElementTypeDescriptor
        {
            /// <summary>Returns the property descriptors for the described
            /// ExampleElement domain class.</summary>
            /// <remarks>This method adds the tracking property descriptor.
            /// </remarks>
            private PropertyDescriptorCollection GetCustomProperties(
                Attribute[] attributes)
            {
                // Get the default property descriptors from the base class
                PropertyDescriptorCollection propertyDescriptors =
                    base.GetProperties(attributes);

                // Get a reference to the model element that is being described.
                ExampleElement source = this.ModelElement as ExampleElement;

                //Add the descriptor for the tracking property.
                if (source != null)
                {
                    DomainPropertyInfo domainProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.NamespaceDomainPropertyId);

                    DomainPropertyInfo trackingProperty =
                        source.Store.DomainDataDirectory.GetDomainProperty(
                            ExampleElement.IsNamespaceTrackingDomainPropertyId);

                    // Define attributes for the tracking property so that the
                    // Properties window displays the property correctly.
                    Attribute[] attr = new Attribute[] {
                        new DisplayNameAttribute("Element Namespace"),
                        new DescriptionAttribute("The namespace of the element."),
                        new CategoryAttribute("Tracking Properties"),
                    };

                    propertyDescriptors.Add(new TrackingPropertyDescriptor(
                        source, domainProperty, trackingProperty, attr));
                }

                // Return the property descriptors for this element
                return propertyDescriptors;
            }
        }
    }
    ```

## <a name="adding-custom-code-for-the-package"></a>Adicionando código personalizado para o pacote

O código gerado define um provedor de descrição de tipo para a classe de domínio Exampleelement; no entanto, você deve adicionar código para instruir a DSL a usar esse provedor de descrição de tipo.

1. Adicione o código a seguir ao arquivo Package.cs.

    ```csharp
    using System.ComponentModel;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // Override the default Initialize method.
        internal sealed partial class TrackingPropertyDSLPackage
        {
            protected override void Initialize()
            {
                // Add the custom type descriptor for the ExampleElement type.
                TypeDescriptor.AddProvider(
                    new ExampleElementTypeDescriptionProvider(),
                    typeof(ExampleElement));

                base.Initialize();
            }
        }
    }
    ```

## <a name="add-custom-code-for-the-model"></a>Adicionar código personalizado para o modelo

Implemente o `GetCustomElementsValue` método para a `ExampleModel` classe de domínio.

> [!NOTE]
> O código que as ferramentas DSL geram para `ExampleModel` chamadas `GetCustomElementsValue` ; no entanto, as ferramentas DSL não geram código que implementa o método.

A definição do `GetCustomElementsValue` método fornece a lógica para a propriedade calculada CustomElements de `ExampleModel` . Esse método conta o número de `ExampleElement` classes de domínio que têm uma propriedade de rastreamento de namespace que tem um valor atualizado pelo usuário e retorna uma cadeia de caracteres que representa essa contagem como uma proporção do total de elementos no modelo.

Além disso, adicione um `OnDefaultNamespaceChanged` método a `ExampleModel` e substitua o `OnValueChanged` método da `DefaultNamespacePropertyHandler` classe aninhada de `ExampleModel` para chamar `OnDefaultNamespaceChanged` .

Como a propriedade DefaultNamespace é usada para calcular a propriedade de rastreamento de namespace, o `ExampleModel` deve notificar todas as `ExampleElement` classes de domínio que o valor de DefaultNamespace foi alterado.

### <a name="to-modify-the-property-handler-for-the-tracked-property"></a>Para modificar o manipulador de propriedades para a propriedade rastreada

1. Adicione o código a seguir ao arquivo ExampleModel.cs.

    ```csharp
    using System.Linq;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        public partial class ExampleModel
        {
            public string GetCustomElementsValue()
            {
                if (this.Elements.Count == 0) return "0/0";

                int number = this.Elements.Count(e => !e.IsNamespaceTracking);
                return string.Format("{0}/{1}", number, this.Elements.Count);
            }

            #region Value changed handler for the tracked property

            // When a tracked property changes, it needs to notify all of the properties
            // that track it.

            /// <summary>Called by the DefaultNamespace property value handler when the
            /// DefaultNamespace property changes.</summary>
            /// <param name="oldValue">The previous value of the property.</param>
            /// <param name="newValue">The new value of the property.</param>
            protected virtual void OnDefaultNamespaceChanged(
                string oldValue, string newValue)
            {
                // Use the helper class to notify all of the elements in the model
                // that the default namespace has changed.
                TrackingHelper.UpdateTrackingCollectionProperty(
                    this.Store,
                    this.Elements,
                    ExampleElement.NamespaceDomainPropertyId,
                    ExampleElement.IsNamespaceTrackingDomainPropertyId);
            }

            // Update the change handler for the DefaultNamespace property.
            internal sealed partial class DefaultNamespacePropertyHandler
            {
                /// <summary>Called when the DefaultNamespace property changes.</summary>
                /// <param name="element">The model element that has the property that
                /// changed.</param>
                /// <param name="oldValue">The previous value of the property.</param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleModel element, string oldValue, string newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);

                    if (!element.Store.InUndoRedoOrRollback)
                    {
                        element.OnDefaultNamespaceChanged(oldValue, newValue);
                    }
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-for-the-tracking-property"></a>Adicionar código personalizado para a propriedade de rastreamento

Adicione um `CalculateNamespace` método à `ExampleElement` classe de domínio.

Definir esse método fornece a lógica para a propriedade calculada CustomElements de `ExampleModel` . Esse método conta o número de `ExampleElement` classes de domínio que têm uma propriedade de rastreamento de namespace que está no estado atualizado pelo usuário e retorna uma cadeia de caracteres que representa essa contagem como uma proporção do total de elementos no modelo.

Além disso, adicione armazenamento para, e métodos para obter e definir, a propriedade de armazenamento personalizado de namespace da `ExampleElement` classe de domínio.

> [!NOTE]
> O código que as ferramentas de DSL geram para `ExampleModel` chama os métodos get e Set; no entanto, as ferramentas DSL não geram código que implementa os métodos.

### <a name="to-add-the-method-for-the-custom-type-descriptor"></a>Para adicionar o método para o descritor de tipo personalizado

1. Adicione o código a seguir ao arquivo NamespaceTrackingProperty.cs.

    ```csharp
    using System;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        // To the domain class that has the tracking property, add the caluclation
        // for when the property is tracking.
        public partial class ExampleElement
        {
            /// <summary>Calculates the actual value of the property when it is
            /// tracking.</summary>
            /// <returns>The value of the tracking property when it is
            /// tracking.</returns>
            /// <remarks>Making this method virtual allows child classes to modify
            /// the calculation. This method does not need to perform validation, as
            /// its caller handles validation prior to calling this method.
            /// <para>In this case, the tracking value depends on the default namespace
            /// property of the parent model.</para></remarks>
            protected virtual string CalculateNamespace()
            {
                return this.ExampleModel.DefaultNamespace;
            }

            #region Tracking property implementation

            // Implement the Namespace domain property of the ExampleElement domain class,
            // and update the IsNamespaceTracking domain property value handler.

            /// <summary>Storage for the Namespace property.</summary>
            private string namespaceStorage;

            /// <summary>Gets the value of the Namespace property.</summary>
            /// <returns>The value of the Namespace property.</returns>
            private string GetNamespaceValue()
            {
                // Only retrieve the tracked value if the store is not in the
                // middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!loading && this.IsNamespaceTracking)
                {
                    try
                    {
                        return this.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                        return default(string);
                    }
                    catch (Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                        else
                        {
                            return default(string);
                        }
                    }
                }

                return namespaceStorage;
            }

            /// <summary>Sets the value of the Namespace property.</summary>
            /// <param name="value">The new value for the property.</param>
            private void SetNamespaceValue(string value)
            {
                namespaceStorage = value;

                // Only update the state of the tracking property if the store is
                // not in the middle of a serialization transaction.
                bool loading = this.Store.TransactionManager.InTransaction
                    && this.Store.TransactionManager.CurrentTransaction.IsSerializing;

                if (!this.Store.InUndoRedoOrRollback && !loading)
                {
                    this.IsNamespaceTracking = false;
                }
            }

            // Update the default behavior of the ExampleElement.IsNamespaceTracking
            // domain property value handler.
            internal sealed partial class IsNamespaceTrackingPropertyHandler
            {
                /// <summary>Called after the IsNamespaceTracking property changes.
                /// </summary>
                /// <param name="element">The model element that has the property
                /// that changed.</param>
                /// <param name="oldValue">The previous value of the property.
                /// </param>
                /// <param name="newValue">The new value of the property.</param>
                protected override void OnValueChanged(
                    ExampleElement element, Boolean oldValue, Boolean newValue)
                {
                    base.OnValueChanged(element, oldValue, newValue);
                    if (!element.Store.InUndoRedoOrRollback && newValue)
                    {
                        DomainPropertyInfo propInfo =
                            element.Store.DomainDataDirectory.GetDomainProperty(
                                ExampleElement.NamespaceDomainPropertyId);
                        propInfo.NotifyValueChange(element);
                    }
                }

                /// <summary>Performs the reset operation for the IsNamespaceTracking
                /// property for a model element.</summary>
                /// <param name="element">The model element that has the property
                /// to reset.</param>
                internal void ResetValue(ExampleElement element)
                {
                    object calculatedValue = null;

                    try
                    {
                        calculatedValue = element.CalculateNamespace();
                    }
                    catch (NullReferenceException)
                    {
                    }
                    catch (System.Exception e)
                    {
                        if (CriticalException.IsCriticalException(e))
                        {
                            throw;
                        }
                    }

                    if ((calculatedValue != null
                        && object.Equals(element.Namespace, calculatedValue)))
                    {
                        element.isNamespaceTrackingPropertyStorage = true;
                    }
                }

                /// <summary>Method to set IsNamespaceTracking to false so that this
                /// instance of this tracking property is not storage-based.
                /// </summary>
                /// <param name="element">The element on which to reset the property
                /// value.</param>
                internal void PreResetValue(ExampleElement element)
                {
                    // Force the IsNamespaceTracking property to false so that the value
                    // of the Namespace property is retrieved from storage.
                    element.isNamespaceTrackingPropertyStorage = false;
                }
            }

            #endregion
        }
    }
    ```

## <a name="add-custom-code-to-support-serialization"></a>Adicionar código personalizado para dar suporte à serialização

Adicione código para dar suporte ao comportamento de pós-carregamento personalizado para serialização de XML.

> [!NOTE]
> O código que as ferramentas de DSL geram chama os `OnPostLoadModel` `OnPostLoadModelAndDiagram` métodos e; no entanto, as ferramentas de DSL não geram código que implementa esses métodos.

### <a name="to-add-code-to-support-the-custom-post-load-behavior"></a>Para adicionar código para dar suporte ao comportamento de pós-carregamento personalizado

1. Adicione o código a seguir ao arquivo Serialization.cs.

    ```csharp
    using System;
    using System.Diagnostics;
    using Microsoft.VisualStudio.Modeling;

    namespace CompanyName.ProductName.TrackingPropertyDSL
    {
        #region Helper classes for maintaining state while the store is serializing.

        public abstract partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Reset the tracking state properties to their natural values
            /// based on comparing storage with calculation.</summary>
            /// <param name="store">The store that contains this model.</param>
            internal static void ResetTrackingProperties(Store store)
            {
                // Two passes required - one to set all elements to storage-based
                // then another to set some back to being tracking.
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.PreResetIsTrackingProperties();
                        continue;
                    }
                }
                foreach (ModelElement element in store.ElementDirectory.AllElements)
                {
                    ExampleElement myElementInstance = element as ExampleElement;
                    if (myElementInstance != null)
                    {
                        myElementInstance.ResetIsTrackingProperties();
                        continue;
                    }
                }
            }
        }

        // Add the pre-reset and reset methods for the model element.
        public partial class ExampleElement
        {
            /// <summary>Calls the pre-reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void PreResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.PreResetValue(this);
            }

            /// <summary>Calls the reset method on the associated property value
            /// handler for each tracking property of this model element.</summary>
            internal virtual void ResetIsTrackingProperties()
            {
                ExampleElement.IsNamespaceTrackingPropertyHandler.Instance.ResetValue(this);
            }
        }

        #endregion

        #region Custom serialization code

        // To the serialization helper for the TrackingPropertyDSL class, add post
        // load handlers to bind the tracking property to the serialization process.
        // These handlers manage the tracking states and property values when the
        // model is serialized and deserialized.
        public partial class TrackingPropertyDSLSerializationHelperBase
        {
            /// <summary>Customize model loading.</summary>
            /// <param name="serializationResult">The serialization result from the
            /// load operation.</param>
            /// <param name="partition">The partition in which the new
            /// instance was created.</param>
            /// <param name="fileName">The name of the file from which the
            /// instance was deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.
            /// </param>
            private void OnPostLoadModel(
                SerializationResult serializationResult,
                Partition partition,
                string fileName,
                ExampleModel modelRoot)
            {
            }

            /// <summary>Customize model and diagram loading.</summary>
            /// <param name="serializationResult">Stores serialization result from
            /// the load operation.</param>
            /// <param name="modelPartition">Partition in which the new
            /// instance will be created.</param>
            /// <param name="modelFileName">Name of the file from which the
            /// instance will be deserialized.</param>
            /// <param name="diagramPartition">Partition in which the new
            /// diagram instance will be created.</param>
            /// <param name="diagramFileName">Name of the file from which the
            /// diagram instance will be deserialized.</param>
            /// <param name="modelRoot">The root of the file that was loaded.</param>
            /// <param name="diagram">The diagram matching the modelRoot.</param>
            private void OnPostLoadModelAndDiagram(
                SerializationResult serializationResult,
                Partition modelPartition,
                string modelFileName,
                Partition diagramPartition,
                string diagramFileName,
                ExampleModel modelRoot,
                TrackingPropertyDSLDiagram diagram)
            {
                Debug.Assert(modelPartition != null);
                Debug.Assert(modelPartition.Store != null);

                // Tracking properties need to be set up according to whether the
                // serialization matches the calculated values.
                TrackingPropertyDSLSerializationHelperBase.ResetTrackingProperties(
                    modelPartition.Store);
            }
        }

        #endregion
    }
    ```

## <a name="test-the-language"></a>Testar o idioma

A próxima etapa é criar e executar o designer de DSL em uma nova instância do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] para que você possa verificar se a propriedade de rastreamento está funcionando corretamente.

1. No menu **Compilar**, clique em **Recompilar Solução**.

2. No menu **depurar** , clique em **Iniciar Depuração**.

    A compilação experimental do [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] abre a solução de **depuração** , que contém um arquivo de teste vazio.

3. Em **Gerenciador de soluções**, clique duas vezes no arquivo Test. trackingPropertyDsl para abri-lo no designer e, em seguida, clique na superfície de design.

    Observe que, na janela **Propriedades** do diagrama, a propriedade **namespace padrão** é **DefaultNamespace**e a propriedade **Custom Elements** é **0/0**.

4. Arraste um elemento **exampleelement** da **caixa de ferramentas** para a superfície do diagrama.

5. Na janela **Propriedades** do elemento, selecione a propriedade **namespace do elemento** e altere o valor de **DefaultNamespace** para **OtherNamespace**.

    Observe que o valor do **namespace do elemento** agora é mostrado em negrito.

6. Na janela **Propriedades** , clique com o botão direito do mouse em **namespace do elemento**e clique em **Redefinir**.

    O valor da propriedade é alterado para **DefaultNamespace**e o valor é mostrado em uma fonte regular.

    Clique com o botão direito do mouse em **namespace do elemento** novamente. O comando **Reset** agora está desabilitado porque a propriedade está atualmente em seu estado de controle.

7. Arraste outro **exemploelement** da **caixa de ferramentas** para a superfície do diagrama e altere seu **namespace de elemento** para **OtherNamespace**.

8. Clique na superfície de design.

    Na janela **Propriedades** do diagrama, o valor dos **elementos personalizados** agora é **1/2**.

9. Altere o **namespace padrão** do diagrama de **DefaultNamespace** para **NewNamespace**.

     O **namespace** do primeiro elemento rastreia a propriedade de **namespace padrão** , enquanto o **namespace** do segundo elemento retém seu valor atualizado pelo usuário de **OtherNamespace**.

10. Salve a solução e, em seguida, feche a compilação experimental.

## <a name="next-steps"></a>Próximas etapas

Se você planeja usar mais de uma propriedade de controle ou implementar propriedades de rastreamento em mais de uma DSL, você pode criar um modelo de texto para gerar o código comum para dar suporte a cada propriedade de controle. Para obter mais informações sobre modelos de texto, consulte [geração de código e modelos de texto T4](../modeling/code-generation-and-t4-text-templates.md).

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Modeling.Design.TrackingPropertyDescriptor>
- <xref:Microsoft.VisualStudio.Modeling.Design.ElementTypeDescriptor>
- [Como definir uma linguagem específica do domínio](../modeling/how-to-define-a-domain-specific-language.md)
- [Como criar uma solução de linguagem específica de domínio](../modeling/how-to-create-a-domain-specific-language-solution.md)
