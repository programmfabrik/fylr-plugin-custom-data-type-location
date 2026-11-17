# custom-data-type-location

> **Warning:** this plugin is not maintained anymore. It is a port of the easydb 5 plugin, kept only so that the instances that already use it keep working. Use a field of type "GeoJSON" with the [geo-json plugin](https://github.com/programmfabrik/fylr-plugin-geo-json-public) instead, and move existing data models to it as soon as possible.
>
> A "Location" field stores a single point and cannot be searched: it is not offered in the expert search and does not show up on the search map of geo-json. Existing values are not converted to GeoJSON automatically, see "Moving to GeoJSON" below.

A fylr plugin that adds the custom data type "Location". With this data type geographic coordinates can be stored in a record. In the editor the position is picked on a map or entered as coordinates.

An optional display name can be stored with the position. The display name is localized and is shown instead of the coordinates. The display name is indexed, so records can be found with the fulltext search.

Each position can be assigned to a group with a line style. Map views that support groups use the line style to connect the positions of a group.

## Configuration

### Data model

Add a field of type "Location" to an object type. The field setting "Type" has the single option "Latitude and Longitude". No further settings are needed.

### Base configuration

The plugin needs no base configuration.

## Moving to GeoJSON

From fylr 6.35.5 on, the values of a "Location" field can be moved to a "GeoJSON" field with the CSV export and the CSV-Importer. Only two columns go through the CSV, the System-ID of each record and the "Location" field, so nothing else in the records is touched. Each location becomes a point with the same coordinates, and its display name becomes the name of the point. The "Location" field itself is not changed, so the result can be checked before the field is removed from the data model.

Do it right after adding the "GeoJSON" field: records without a location get an empty "GeoJSON" field.

1. Install the [geo-json plugin](https://github.com/programmfabrik/fylr-plugin-geo-json-public). In the data model, add a field of type "GeoJSON" to the object type that has the "Location" field, and make it editable in the mask used for the import.
2. Search the records of that object type, open the ⋮ menu of the results and choose "Export search...". Check "Output CSV". Under "Custom fields for CSV, XML and XLSX" click "Select custom fields", select only "System-ID" and, under the object type, the "Location" field, and click "Done". Run the export and download the CSV file. It has the column `_system_object_id`, the column of the "Location" field and one column per language with its display name.
3. Open the CSV-Importer and load the file. Set "CSV Field Names" to "1. Row", then choose the object type and the mask.
4. In "Import mapping", map only two columns: `_system_object_id` to `_system_object_id`, and the column of the "Location" field to the "GeoJSON" field. Leave the display name columns empty. Check this every time, the CSV-Importer remembers the mapping of the previous import by column position.
5. In "Import settings", set "Update field" to `_system_object_id`. Without it, the CSV-Importer creates new records instead of updating the existing ones.
6. Click "Prepare". The status has to show all rows under "Update", and the "JSON preview" only the "GeoJSON" field for each record. Then click "Update".

This covers "Location" fields at the top level of an object type, not inside nested fields.
