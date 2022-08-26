---
title: "Week 5"
enableToc: false
---
#### What I managed:
#### 22/7
- Found a 'bug' with the ifcopenshell.api.execute_docs() func
- Added context, unit etc to my test node
- worked on a project from template node

#### 23/7
- IFC write file writes continuously with every change (really bad, when using a slider) -%3E should add an update button and overwrite changes in elements with the same ID
- Made a 'create project' node
- Continued working on a blender mesh to ifc node, but can't pass the representation to create entity node
- unfixed bug when using `should_run_listeners=True` in ifcopenshell.api.run()
#### 24/7
- fixed passing the representation to 'create entity', but blenderbim can't open the representation (show geometry) and 'create shape' node can't convert it into shape
- analysed diff. ifc files created with blenderbim and figured out that it needs to be converted to a product shape
- worked on a WIP api node
#### 25/7
- got the bmesh to ifc geo work properly
- worked on WIP Api node
- worked on quick project setup node>)
