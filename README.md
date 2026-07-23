# custom-data-type-location

A fylr plugin that adds the custom data type "Location". With this data type geographic coordinates can be stored in a record. In the editor the position is picked on a map or entered as coordinates.

An optional display name can be stored with the position. The display name is localized and is shown instead of the coordinates. The display name is indexed, so records can be found with the fulltext search.

Each position can be assigned to a group with a line style. Map views that support groups use the line style to connect the positions of a group.

## Configuration

### Data model

Add a field of type "Location" to an object type. The field setting "Type" has the single option "Latitude and Longitude". No further settings are needed.

### Base configuration

The plugin needs no base configuration.
