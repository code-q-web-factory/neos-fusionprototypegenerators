# CodeQ.FusionPrototypeGenerator

The default Neos DefaultPrototypeGenerator generates a Fusion prototype definition for a given node type. A node will be rendered by Neos.Neos:Content by default with a template in resource://PACKAGE_KEY/Private/Templates/NodeTypes/NAME.html and forwards all public node properties to the template Fusion object.

This generator uses [CodeQ.SimpleTemplate](https://github.com/rolandschuetz/neos-simpletemplate) to map the tempalte file path according to current Neos best practises. 

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
