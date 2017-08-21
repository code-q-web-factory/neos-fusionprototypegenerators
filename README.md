# CodeQ.FusionPrototypeGenerator

Fusion prototype generator that generates editable properties wrappers automatically. `propertyName` will contain raw property and `propertyNameEditable` contains the same property wrapped into Neos editable object.

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
