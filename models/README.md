# Editable diagram sources

- `visual-paradigm/`: UML project files in Visual Paradigm `.vpp` format, organized by workflow.
- `graphviz/fault-activity.dot`: the fault-handling activity flow in Graphviz format.

The [diagram gallery](../docs/UML.md) links each image to its editable source. To render the Graphviz file, run:

```sh
dot -Tsvg models/graphviz/fault-activity.dot -o assets/uml/fault/activity.svg
```
