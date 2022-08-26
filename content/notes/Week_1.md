---
title: "Week 1"
enableToc: false
---
#### Goals:
- [ ] Research the contents of IFC standard in detail and note which classes, attributes and information should be included. 
- [x] Research ways of containing geometry in IFC. ✅ 2022-06-30
- [ ] Familiarise myself with the functions in IfcOpenShell and BlenderBIM and classify the planned nodes into those that can be created by reusing functions directly, only providing a visual wrapper, those that would need smaller additions of functionalities and those that have to be written from scratch.
- [x] Make a reviewed and more detailed description of the first part of planned components, defining the inputs and outputs. ✅ 2022-06-30

#### What I managed:
This was mostly a research-heavvy week. With Dions and Thomas' explainations and a lot of reading, I finally feel like I understand the different geometry types better and what the link between geometry representations in Blender, Sverchok and IFC can look like. 
Also did quite a bit of reading up on the IFC schema in general from a more technical perspective, trying to identify the classes and attributes that should be included in the nodes (first simple use case).
Decided to make the mockups in Sverchok as ScriptNodeLite nodes, and make them follow the IFC schema more closely. I'm close to done with defining two different approaches to defining a space and corresponding building elements (differing in the inheritence hierarchy).
