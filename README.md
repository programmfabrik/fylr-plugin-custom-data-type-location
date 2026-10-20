# custom-data-type-location

> **Warning:** this plugin is not maintained anymore. It is a port of the easydb 5 plugin, kept only so that the instances that already use it keep working. Use a field of type "GeoJSON" with the [geo-json plugin](https://github.com/programmfabrik/fylr-plugin-geo-json-public) instead, and move existing data models to it as soon as possible.
>
> A "Location" field stores a single point and cannot be searched: it is not offered in the expert search and does not show up on the search map of geo-json. Existing values are not converted to GeoJSON automatically.

A fylr plugin that adds the custom data type "Location". With this data type geographic coordinates can be stored in a record. In the editor the position is picked on a map or entered as coordinates.

An optional display name can be stored with the position. The display name is localized and is shown instead of the coordinates. The display name is indexed, so records can be found with the fulltext search.

Each position can be assigned to a group with a line style. Map views that support groups use the line style to connect the positions of a group.

## Configuration

### Data model

Add a field of type "Location" to an object type. The field setting "Type" has the single option "Latitude and Longitude". No further settings are needed.

### Base configuration

The plugin needs no base configuration.
