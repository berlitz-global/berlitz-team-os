# Content Service Schema Design: Lesson and Exercise Data Model — 2026-06-15

**Attendees:** Rob Zinkov, Daniel Peter
**Date:** 2026-06-15

## TL;DR

- Rob and Daniel aligned on a data model for the content service's `/lesson/{id}` endpoint, settling on a hierarchical schema: learning paths → modules → lessons → exercises.
- Exercises will be typed via an enum (e.g., matching pairs, fill-in-the-blank, ordering) with each type carrying its own evaluation expression; a shared pool-of-exercises table is preferred over any custom serialization format.
- Lessons are currently static but the design must accommodate future AI-generated lessons — once generated, a lesson persists so users can resume it.
- The backend will return the full lesson payload in a single response (not paginated per exercise), enabling offline use; the API will follow a backend-for-frontend pattern where the backend dictates UI shape.

## Decisions

- Lesson schema will follow a **learning path → module → lesson → exercise** hierarchy.
- Exercises will be stored in a **shared pool table**, typed via an enum, each type carrying its own data shape and evaluation expression.
- **User state** (progress, completion) will live in a separate `user_lessons` layer derived from, not embedded in, the lesson definition.
- The `/lesson/{id}` endpoint will return the **full lesson payload in one response** (not paginated per exercise), enabling offline use.
- Schema must use **plain serializable JSON** — no custom serialization formats.
- New exercise types will be added by **extending the enum** and adding a matching backend shape and frontend component.

## Action items

| Owner | Action | Status |
| ----- | ------ | ------ |
| Daniel Peter | Formalize the exercise type enum and data shapes based on existing exercise types (matching pairs, fill-in-the-blank, ordering, etc.) | New |
| Rob Zinkov | Confirm which exercise types need to be supported at launch | New |

## Open questions

- How will learning path routing work for content that does not fit neatly into a module (e.g., Cultural Navigator lessons)?
- What is the complete set of exercise types to be supported at launch, and do any require non-trivial evaluation logic?
- How will dynamically generated lessons be triggered and parameterized (i.e., what parameters define a "generation context" for a lesson)?

## Discussion

### Scope of the schema problem

Rob opened the meeting by framing the question: how should lessons be stored given that they contain interactive elements (quizzes, videos, audio) arranged in specific orders, and will eventually be authored by a combination of humans and AI? He noted the schema challenge is harder for self-study-style exercises than for tutoring lessons — tutoring lessons are largely text (prompts plus triggered actions), so their schema is straightforward. Self-study exercises have heterogeneous types and a potentially extensible type set.

### Current lesson model and open questions

Daniel confirmed the existing system serves a static, fixed set of lessons, with a fixed set of exercise types (e.g., matching pairs, fill-in-the-blank). He framed the key open questions:

1. What are the exercise types, and how does each type define its data shape?
2. Are lessons statically defined or dynamically assembled per user?
3. What is the shape (data object) of a lesson?
4. How is the API endpoint structured — are lessons scoped per user or per course?
5. How is the user's learning path dynamically tracked?

### Static vs. dynamic lesson generation

Rob clarified the intended direction: lessons are currently static, but the goal is to move toward automatically generating lessons within defined parameters. Once a lesson is generated it persists — if a user leaves and returns, they resume the same generated lesson. Daniel confirmed this approach.

### Data model: exercises, lessons, modules, paths

Daniel proposed and Rob agreed on the following layered structure:

- **Exercise pool:** a flat table of all exercises, each tagged with a type (enum) and an evaluation expression describing correct/incorrect answers. Exercise types are discriminated-union / enum cases — each carries a different data shape. Example: an "ordering" exercise stores its list elements plus the correct order.
- **Lesson:** an ordered list of exercises drawn from the pool, tracking which exercise comes next.
- **User lesson:** a lesson with per-user state (progress, completion, errors). Distinct from the lesson definition itself.
- **Module:** an ordered collection of lessons. Daniel introduced "modules" as the grouping layer within a path.
- **Learning path:** an ordered collection of modules. A user can have multiple learning paths (e.g., one per language). Path and module state is derived from user-lesson state.

Rob noted that some lessons (e.g., Cultural Navigator content) may not fit neatly into a module, but was broadly comfortable with the path → module → lesson → exercise hierarchy.

### Schema design principles

Daniel emphasized the schema should avoid any custom serialization format. It should be simple, serializable JSON read and written from a database. The backend should be flexible enough to support both statically defined and dynamically constructed lessons without the data type itself being the constraint.

### Exercise type extensibility

Rob and Daniel agreed that adding a new exercise type should be straightforward: extend the enum, define the new JSON shape on the backend, and build a corresponding frontend component that knows how to render and evaluate that exercise type.

### API shape: full lesson payload vs. per-exercise fetching

Rob expressed a product preference for fetching the entire lesson in a single API call rather than fetching one exercise at a time. His reasoning: lesson content is not large, and a full upfront fetch enables offline use. Daniel agreed. The API will follow a backend-for-frontend (BFF) pattern: the backend tells the frontend what UI shape to render, and the frontend reports completion/error back.
