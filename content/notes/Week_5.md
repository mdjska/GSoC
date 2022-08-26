---
title: "Week 5"
enableToc: false
---
#### What I managed:
#### 22/7
- Found a 'bug' with the `ifcopenshell.api.execute_docs()` func
- Added context, unit etc to my test node
- Worked on a 'project from template' node

#### 23/7
- IFC write file writes continuously with every change (really bad, when using a slider) - should add an update button and overwrite changes in elements with the same ID
- Made a 'create project' node
- Continued working on a blender mesh to ifc node, but can't pass the representation to create entity node
- There is a bug when using `should_run_listeners=True` in `ifcopenshell.api.run('geometry.add_representation')`,  just turned it off for now.. 
#### 24/7
- Fixed passing the representation to 'create entity', but blenderbim can't open the representation (show geometry) and 'create shape' node can't convert it into shape
- Analysed diff. ifc files created with blenderbim and figured out that it needs to be converted to a product shape
- Worked on a WIP api node
#### 25/7
- Got the bmesh to ifc geo work properly (although I haven't fixed the bug with `listeners`)
- Worked on 'WIP Api' node - I'm missing input types to be able to create node sockets with the correct type. Right now everything is a string type.
- Worked on 'quick project setup' node
