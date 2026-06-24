## 1.3.4 (2026-06-24)

### Bug Fixes

-  Add namn field to sorteringsordning spec and response ([49475](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/4947550ba236f37) Lars Persson)  
-  **deps**  update dependency se.fk.gradle:gradle-conventions to v1.18.3 ([ee2c1](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/ee2c10b28066814) renovate[bot])  
-  **deps**  update jackson monorepo ([fb87b](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/fb87b729d464a77) renovate[bot])  

### Dependency updates

- update gradle to v9.5.1 ([be642](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/be642ab3dd5f3b4) renovate[bot])  
## 1.3.3 (2026-06-12)

### Bug Fixes

-  add pagination support to getSorteringsordningar endpoint ([dda34](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/dda3435551ab6a5) Ulf Slunga)  

## 1.3.2 (2026-06-08)

### Bug Fixes

-  Replace api-npm-* workflows with gradle-* workflows ([2e5bf](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/2e5bf26433e9cc1) Lars Persson)  
-  Remove create / end operations ([af6bc](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/af6bccd83de323f) Lars Persson)  

## 1.3.1 (2026-06-05)

### Bug Fixes

-  correct POST /uppgifter response code to 201 Created ([27f27](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/27f27365c72bfcb) Ulf Slunga)  

## 1.3.0 (2026-06-05)

### Features

-  Split DefaultApi into UppgifterApi and SorteringsordningApi by tags ([d9931](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/d99319f3ed4f77e) Ulf Slunga)  

## 1.2.0 (2026-06-04)

### Features

-  fix oneOf discriminator TypeScript generation for Constraint type ([81025](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/81025e82d030e00) Ulf Slunga)  
-  add requirement tags and align krav-fas1 with updated krav ([22d71](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/22d714cf824c43b) Ulf Slunga)  
-  add fas 1 partial implementation requirements ([fa420](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/fa4209d9509565b) Ulf Slunga)  
-  document catch-all entries, bootstrap default, and 404 semantics ([67a0c](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/67a0c8d39a3b632) Ulf Slunga)  
-  wrap paginated responses in UppgiftPage envelope with total count ([9e349](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/9e3493819917472) Ulf Slunga)  
-  remove /sorteringsordning/latest endpoint superseded by default ([16b8b](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/16b8bc0dab4502f) Ulf Slunga)  
-  require a default sorteringsordning and reject delete of current default ([5f16b](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/5f16bc175dd6442) Ulf Slunga)  
-  add minItems: 1 to SorteringsordningResponse entries ([7dcab](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/7dcab2dcaecec7d) Ulf Slunga)  
-  allow constraint-free entries as catch-all sort ([17554](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/1755467321939eb) Ulf Slunga)  
-  enforce operator/field constraints via typed Constraint schemas ([9e30d](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/9e30d4631e0f242) Ulf Slunga)  
-  add default sorteringsordning endpoints and explicit default concept ([765be](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/765be6326c52f37) Ulf Slunga)  
-  add pagination, tighten limit/offset and entries constraints ([b913a](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/b913affa40855ac) Ulf Slunga)  
-  list all sorteringsordningar and add /latest endpoint ([722eb](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/722eb1d2ba59b4f) Ulf Slunga)  
-  add examples for constraint and sorteringsordning schemas ([682c4](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/682c43c022f4f1a) Ulf Slunga)  
-  add sorteringsordning schemas and request/response bodies ([76dcf](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/76dcfe2018fd22f) Ulf Slunga)  
-  add sorteringsordning endpoints and fix beskrivning typo ([3d6b4](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/3d6b4e23b6f2802) Ulf Slunga)  
-  refine sort order spec requirements and endpoint definitions ([a5785](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/a57859f2d47ee39) Ulf Slunga)  
-  add requirements doc for sort order specification ([b967c](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/b967ca53c73d16a) Ulf Slunga)  

### Bug Fixes

-  correct date field descriptions in OperativUppgift ([9a311](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/9a311ca3b9f662d) Ulf Slunga)  

## 1.1.2 (2026-06-04)

### Bug Fixes

-  Add missing description and operationId to uppgift patch and unassign operations ([4868d](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/4868d07237ea26f) Lars Persson)  

## 1.1.1 (2026-06-04)

### Bug Fixes

-  Add support for unassigning and reassigning task ([6c954](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/6c95479a551f487) Lars Persson)  

## 0.0.5 (2026-05-21)

### Bug Fixes

-  Add erbjudande to OperativUppgift ([bdfb0](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/bdfb0b711d44567) Lars Persson)  

## 0.0.4 (2026-05-21)

### Bug Fixes

-  Add erbjudande information to OUL uppgift create request ([443d1](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/443d187c8c7ea19) Lars Persson)  

## 0.0.3 (2026-05-20)

### Bug Fixes

-  Change group id to avoid collision with classes defined in other OUL openapi spec ([38a9d](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/38a9d14fffef522) Lars Persson)  

## 0.0.2 (2026-05-20)

### Bug Fixes

-  Add endpoint for listing uppgifter ([3d190](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/3d1903ed7bf3b9f) Lars Persson)  

# rimfrost-service-oul-management-openapi changelog

Changelog of rimfrost-service-oul-management-openapi.

## 0.0.1 (2026-05-12)

### Bug Fixes

-  id typ and gradle version ([f81bb](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/f81bb457982a7b9) Nils Elveros)  
-  add status ([08d6b](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/08d6bd8a0da5749) Nils Elveros)  
-  add CloudeventAttributes, subtopic and reson to end uppgift ([51cd0](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/51cd0a44f607736) Nils Elveros)  
-  initial commit with openapi specification ([b1eb7](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/b1eb714655a6804) Nils Elveros)  

### Other changes

**Fix gradlew permissions**


[8b983](https://github.com/Forsakringskassan/rimfrost-service-oul-management-openapi/commit/8b983d1716d1fb2) Lars Persson *2026-05-12 06:40:39*


