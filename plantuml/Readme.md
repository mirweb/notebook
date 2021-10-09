# PlantUML

* [PlantUML Homepage](https://plantuml.com/de/)


## Running local plantuml server

* running plantUML via [docker image](https://hub.docker.com/r/plantuml/plantuml-server)

```bash
docker run --name plantUML -d -p 8080:8080 plantuml/plantuml-server:latest
```

## simple example

```plantuml
Bob -> Alice : Hello
```

## overview stdlib

# icluded stdlib

* overview of inluded [stdlib](https://plantuml.com/de/stdlib), see also [platnuml-stdlib Github Repo](https://github.com/plantuml/plantuml-stdlib)

```plantuml
@startuml
version
@enduml
```

```plantuml
@startuml
stdlib
@enduml
```

## simple C4 Components Diagram

```plantuml
@startuml C4_Elements
!include <C4/C4_Component>


Person(personAlias, "Label", "Optional Description")
Container(containerAlias, "Label", "Technology", "Optional Description")
System(systemAlias, "Label", "Optional Description")

Rel(personAlias, containerAlias, "Label", "Optional Technology")
@enduml
```

## plantuml stdlib icons

```plantuml
@startuml
listopeniconic
@enduml
```