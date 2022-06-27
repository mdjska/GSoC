 ---
 title: "Rough development schedule"
 tags:
 
---
#### Related Notes: [Project proposal](GSoC_proposal_mdj.md)

# Rough development schedule

The community bonding period should be used to make a thorough review of the project plan in collaboration with the mentor. The ideas outlined in the project description can be added or removed adjusting the scope of the project as needed. Possibilities for further development are many, providing a close to infinite amount of work if desired. But the basic version of the project that I think should possible to finish, should include:

-  Working, tested and documented nodes to allow the user to:
  - Create basic IfcElements by geometry from Blender. Basic elements include: IfcSpace, IfcWall, IfcWindow, IfcSlab, IfcFloor, IfcRoof, IfcBeam, IfcColumn, IfcCurtainwall, IfcFooting
  - Create other IfcElements that are not predefined
  - Assign attributes and materials to the elements
  - Structure the elements in an IFC hierarchy utilising IfcBuildingStorey, IfcBuilding and IfcProject
  - Decompose (get the information on) the created elements
  - Provide a list of available property sets and attributes
  - Query elements based on names, ids and attributes 
  - Read and write IFC-SPF files
  - Export quantity takeoff
  - Visualise geometry in Blender modelling viewport

##### Week 1

Research the contents of IFC standard in detail and note which classes, attributes and information should be included. Research ways of containing geometry in IFC. Familiarise myself with the functions in IfcOpenShell and BlenderBIM and classify the planned nodes into those that can be created by reusing functions directly, only providing a visual wrapper, those that would need smaller additions of functionalities and those that have to be written from scratch. 

Made a reviewed and more detailed description of the first part of planned components, defining the inputs and outputs.

##### Week 2

Setup development environment, a version control system etc. Test and debug existing nodes. Familiarise myself with writing and implementing nodes, adding functionality to the node UI. Begin to make changes to the existing nodes and create some new low level nodes.

##### Week 3 and 4

Begin coding the medium level nodes by using IfcOpenShell API. Customise the “Create Entity” node to class specific creation nodes. Document the code and write explanations for the user.

##### Week 5 and 6

Add functionalities to the element nodes. Work on incorporating property sets and materials. Create some sample IfcMaterials and IfcMaterialLayerSets and try creating a small library of them. If time allows; work on implementing and creating schedules.

##### Week 7 and 8

Ask community for feedback and make changes/review of the plan if needed. Continue working on the higher level nodes; assignment of elements to spaces, creation of zones, storeys, building and project. Test the exporting functionality to be able to check the resulting model.

##### Week 9 and 10

Work on other miscellaneous nodes like decomposition, visualisation and querying. Implement export of the model. Explore exporting MVDs and other formats.

##### Week 11 and 12

Finish up work with exporting and creating MVDs for eg. energy analysis. Buffer time, if any of the other work is not finished. Otherwise, try working on classification system mapping and COBie export. Try using microMVDs as unit tests for created IFC models. Create proof of concept model and document the functionalities. If time allows; work on any of the ideas not included in this plan.
