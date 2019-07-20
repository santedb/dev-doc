---
description: >-
  SanteGuard is a centralized audit and security repository which is compatible
  with SanteDB products and as well as any product using OAUTH and IHE ATNA.
---

# About SanteGuard

```uml
@startuml

	Class Stage
	Class Timeout {
		+constructor:function(cfg)
		+timeout:function(ctx)
		+overdue:function(ctx)
		+stage: Stage
	}
 	Stage <|-- Timeout

@enduml
```