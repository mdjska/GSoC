---
 title: "My original proposal"
---
#### Related Notes: [Development schedule]([Development_schedule])

# Create visual programming nodes for generating BIM data with IfcSverchok

*Also available on the [OSArch Wiki](https://wiki.osarch.org/index.php?title=User:Mdjska).*

### Project Information
 
This proposal is written for issue #34, project [“Create visual programming nodes for generating BIM data with IfcSverchok”](https://github.com/opencax/GSoC/issues/43), written by Dion Moult. The project would primarily contribute to the BlenderBIM project, which is part of the IfcOpenShell community. In GSoC, IfcOpenShell operates under the umbrella-organisation BRL-CAD. 

## Create visual programming nodes for generating BIM data with IfcSverchok

### Abstract and motivation

Industry Foundation Class (IFC) is the leading open data format for the built environment, based on the [ISO 16739-1:2018](https://www.iso.org/standard/70303.html) standard. It’s the foundation of the openBIM workflow, that ensures the interoperability, longevity and transparency of all BIM data. Today, IFC is most often used as a vendor-neutral and software-agnostic way of exchanging building information, but there is increasing interest in using the IFC schema as the native format for working with BIM data. Native IFC would greatly increase the quality of produced IFC files and ensure no data is lost on import/export. Both IFC and the openBIM process are created by the buildingSMART organisation. 

Blender, with its mature modelling and rendering capabilities, has the potential to become a powerful BIM authoring tool. Open data and integrated python console already give many options for customising the data and meta data of any geometric object. The BlenderBIM plugin introduces the possibility to assign the properties of IFC classes to native blender geometry and export correctly structured IFC files through the use of the IfcOpenShell software library that already contains many useful functions to work with the IFC schema. Other tools like IFC Diff, IFC Clash, IFC COBie or IFC Patch extend the functionalities of working with IFC in Blender even more, but for the most part have a GUI and require that the user is comfortable with scripting/using a console.

The visual scripting language for Blender, Sverchok, opens many of the possibilities of code to the non-coding user. Sverchok’s counterpart for the Rhinoceros3D modelling software, Grasshopper, has had huge success and popularity among architects, engineers and designers. There exists a plugin for Grasshopper, called Geometry Gym, that enables creating IFC geometry and data through the visual programming nodes, allowing the users to create their own parametric workflows and incorporate IFC data directly into their design process. 

An equivalent plugin for Sverchok, would allow an integrated parametric design and native IFC workflow to be completed fully inside the FOSS environment. It would also be a strong foundation for integrations with other Building Performance Simulations (BPS) tools, including energy-, daylight-, structural-, wind- or environmental analysis. Integration and porting of the nodes to FreeCAD would also be possible.

Some of the basic nodes are already coded under the [IfcSverchok](https://github.com/IfcOpenShell/IfcOpenShell/tree/v0.7.0/src/ifcsverchok) project. The work will involve testing the existing nodes and writing many more to support the full use case. Since the IFC schema is very large, and often difficult to grasp for new users, emphasis will be on integrating the concepts of IFC into a typical design process in a natural manner and communicating the relevant information comprehensively to the user.  



### Detailed project description

The first and foremost use case of IfcSverchok is to enable creating building models enriched with model data in accordance with the IFC schema in Blender. The scope of the planned components can be narrowed or extended depending on the rate of progress. 

A mockup of a workflow creating an .ifc file based on existing geometry, is shown below. Since many of the components could be either generated directly, or be heavily based on, IfcOpenShell functions, the flowchart is expressed in quite high level nodes, that could be shown to the user. Still, the presented components are not comprehensive. 

The question of what data type the geometry provided to the components would have, is left open right now. To begin with, it’s assumed that the geometry is fully modelled in either Blender itself (eg. with the help of BlenderBIM) or in native Sverchok nodes. Then the mesh or NURBS geometry would have to be translated to solids accepted by IFC. Another approach would be to directly generate geometry through the IfcSverchok components. This approach would be fully parametric, but would be quite labour intensive, both for the user and in development. Right now, it should be reserved for more complex elements that wouldn’t be intuitive to model through other methods.
A mixed approach, of asking the user to provide a simple geometry like a surface or a curve, and then building the rest of the element based on it, could be beneficial. This would allow to automatically get the location of the element in the projects coordinate system, which can be troublesome for users if it has to be provided as cartesian points. At the same time, it gives the user an intuition of the elements placement in relation to the rest of the model. Example of this in the flowchart is creating an IfcSpace based on a boundary curve and a height or creating beams with different profiles, based on just a curve. 

The presented workflow in general, is based around the idea of using IfcSpaces as a central concept to rapidly develop the whole building and fill in the more detailed information as it becomes available. This process is more in line with the typical design process, where architects would often start with abstract areas with the only information available about them being their intended use functions and rough sizes. 
This approach could allow the model to stay parametric, even when large parts of the geometry change at a later point. If the specific constructions are added to the spaces, instead of the other way around, the user can reshape the spaces or even change their plancement in relation to each other, without having to remodel any of the actual elements like the walls or floors. This would of course require, that the geometry isn’t modelled separately, but is coupled with the spaces’ parameters.

On the leftmost side, the IfcSpaces are created either from Blender/Sverchok geometry or by dimensions. An ordered list of points could also form the basis of the simple geometry. The resulting space or a list of spaces can then be parsed to a component that would associate related building elements to a space or spaces. It could place the instance of IfcBuildingElement in the space.BoundedBy and obj.RelatedBuildingElement properties.
Class specific nodes would be written for all IfcBuildingElement by customising the CreateEntity function. Components for other relevant IfcElements could be added, and a “CreateCustomEntity” node would always give the user possibility to add another, not implemented, entity type.



The diagram can be found in a better resolution at https://wiki.osarch.org/index.php?title=File:IfcSverchok_node_graph.svg. 

![[notes/images/IfcSverchok_node_graph_4.svg]]

Aparts from linking geometry, adding meta data like name and ID, the IfcElement creation nodes should all expose and give the possibility to set the relevant property sets. User should be able to find the names of property sets and their respective properties corresponding to the given class, and set their values. Another important feature is the possibility to assign materials to building elements. I imagine that a small library of typical materials (instances of IfcMaterial) and constructions made from these materials (IfcMaterialLayerSets) would come with the plugin and be available to be used simply by picking them from a dropdown menu. Alternatively, the user should be able to modify these standard materials or create their own from scratch. In that case, the ifc material properties, such as energy, mechanical, thermal and optical, should be exposed and the user should be able to assign as many as they wish. Simple unit tests could be implemented here; eg. if the model should later be used for daylight or energy analysis, then the material should require to eg. have the thermal conductivity and transmittance properties filled in. The user should be able to save custom materials and constructions to a local library of sorts and reuse them in the same or other project. The same could be implemented at IfcBuildingElement level.

If multiple spaces are given, the component could try to find adjacencies between spaces and thus pinpoint if any constructions/elements are shared between them. The user, should then have the possibility to easily define these elements with different specifications, eg. another construction type. 
The possibility to assign elements in a more manual manner, by eg. directly picking the associated space face, or completely detached from the space, should also be possible.
Finally, implementing occupancy or other schedules on a space level would be desired. These could though also be implemented on zone, building storey or building level. The resulting object, would still be an IfcSpace, but with relational data on all bounding elements. 

Further, the model creation would continue upwards in a hierarchical manner. Optional IfcZones could be created from multiple IfcSpaces. The same with IfcBuildingStoreys. Building storeys or the IfcBuilding itself, should contain all other building elements, that cannot be associated with one IfcSpace. This could be large facade walls, curtainwalls, slabs, roofs, beams etc. IfcBuilding would contain some typical meta data like name, address, elevation etc., but could also be enriched with more advanced data like occupancy type or details on the HVAC systems used. IFCSite could additionally contain a geometrical representation of the terrain itself, but also the context geometry and vegetation, that could, among others, be used for daylight and energy simulations. Material properties or schedules of this optional context geometry could also be added here. 

The IfcProject should add the final information on owner history, IFC schema version, define the coordinate system, the true north and units. Conversions to other classification systems like the Uniclass or Omniclass could also be implemented, either by a predefined or user-defined mapping of Ifc codes to other classification codes. The IFC data and classification system information could then be structured into a COBie spreadsheet (either .xml file or an excel .xlsx), which is a type of MVD for the IFC schema, with the official name “Basic FM handover view”.
Unit tests checking for example if any of the elements clash (self intersect) or if the model contains all required objects could be added as a final step before writing the file. Here, the microMVDs (Model View Definitions) already implemented in BIMTester could be utilised, letting the user read and choose unit tests written in plain English. Possibility of letting the user write their own microMVDs and save them in their local library, should be explored. 

When all is ready, multiple ways of writing and exporting the project should be possible; obviously as IFC-SPF (.ifc extension), but also a .JSON file and .csv using IFC CSV. IFC-XML format could also be explored.

Different MVDs - smaller subsets of the full IFC model - could be predefined matching some typical use cases. For example, exporting a *light version* without the geometry, or a structural analysis model. A simple quantity takeoff (possibly using IfcQuantitySets) should be possible to export easily. Especially the material quantities, eg. subdivided by types or spaces, could be helpful for environmental analysis. A light model containing only the spaces and relevant properties of their constructions would be useful for energy or daylight analysis with for example EnergyPlus or Radiance. Here, the “Space boundary add-on view” MVD could be utilised to eg. only export certain critical spaces for analysis.

Lastly, the grouping at the bottom, shows ideas for additional nodes that would be helpful. It contains, among others, nodes for decomposing all created classes and entities from libraries like materials, constructions and schedules. Querying and filtering elements based on names, ids and all associated attributes and then modifying, displaying or deleting the elements, would also be essential.  The final part of core functionalities, would be performing these actions on existing, .ifc files and combining it with the functionalities of IFC Patch to fix bad data in imported IFC models. 

#### Links to any code or algorithms you intend to use

The work will be a continuation of IfcSverchok nodes found on https://github.com/IfcOpenShell/IfcOpenShell/tree/v0.7.0/src/ifcsverchok. 

IfcOpenShell python API (https://github.com/IfcOpenShell/IfcOpenShell/tree/v0.7.0/src/ifcopenshell-python) will be utilised in many of the nodes. 

Other functions from the BlenderBIM and native Sverchok code base will also be used. Code bases from other projects like 

### Possibilities for further development

There is a huge potential for future development on top of a working, parametric IFC tool. Firstly, the described use case only utilised a selected part of the IFC schema, especially related to buildings. Many other features and details can be implemented in the building realm, but also whole other parts of the schema geared towards other infrastructures like bridges, tunnels and reads exist. Together, local urban plans and environments around the building could be modelled using IFC.
Taking an IfcSpace first approach would presumably make it easy to associate the models with Ladybug tools’ Honeybee zones, enabling many environmental simulations. Constructions and materials could be linked to EnergyPlus’ or OpenStudio libraries making simulations seamless. 
Materials could also be linked to environmental Life Cycle Inventory Analysis (LCIA) data like Ecoinvent or Environmental Product Declarations (EPDs) from databases like the German ÖKOBAUDAT. Such a mapping would greatly simplify export to any environmental software like OpenLCA or other.
Structural analysis and costing are yet another areas that could be built on top of IfcSverchok.

The nodes could possibly also be ported to FreeCAD using PyFlow and support the native IFC workflow. Maybe could some of the FreeCAD parts library (like the architectural parts) even be made available directly in Sverchok, making it possible to create native IFC models very efficiently. 
