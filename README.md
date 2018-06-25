# CodeQ.FusionPrototypeGenerator

The default Neos DefaultPrototypeGenerator generates a Fusion prototype definition for a given node type. A node will be rendered by Neos.Neos:Content by default with a template in resource://PACKAGE_KEY/Private/Templates/NodeTypes/NAME.html and forwards all public node properties to the template Fusion object.

This improved generator uses [CodeQ.SimpleTemplate](https://github.com/rolandschuetz/neos-simpletemplate) to map the template file path according to current Neos best practises. 

Also, this Fusion prototype generator automatically creates editable properties. `propertyName` will contain the raw property and `propertyNameEditable` contains the same property wrapped into Neos editable object.

To activate these generators, make your base nodetypes to inherit from mixins provided by this package, e.g.:

```
# All nodetypes that want to use new generators should inherit from these ones instead of "Neos.Neos:Content" and "Neos.Neos:Document"
'CodeQ.Site:Content':
  abstract: true
  superTypes:
    'Neos.Neos:Content': true
    'CodeQ.FusionPrototypeGenerator:ContentPrototypeGeneratorMixin': true

'CodeQ.Site:Document':
  abstract: true
  superTypes:
    'Neos.Neos:Document': true
    'CodeQ.FusionPrototypeGenerator:DocumentPrototypeGeneratorMixin': true
```

## Example

Let's say you have a content node type to show a headline:

```
'CodeQ.Site:Content.Headline':
  ...
  properties:
    title:
      type: string
      ui:
        inlineEditable: true
        aloha:
          placeholder: 'Enter headline here...'
```

The generator will automatically generate on the fly a Fusion prototype like this:

```
prototype(CodeQ.Site:Content.Headline) < prototype(CodeQ.SimpleTemplate:Template) {
	title = ${q(node).property("title")}
	title.@process.convertUris = ConvertUris

	titleEditable = Neos.Fusion:Tag {
		content = ${q(node).property("title")}
		content.@process.convertUris = ConvertUris
		@process.contentElementEditable = ContentElementEditable {
			property = "title"
		}
	}
}
```

Now create a inline editable Fluid template `Resources/Private/Fusion/Content/Headline/Headline.html`with the content

```
<div class="headline">
	{titleEditable -> f:format.raw()}
</div>
```
