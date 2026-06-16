# Engineering

Engineering plans, design docs, and bug investigations for Berlitz AI Tutor. All organized by product area.

## Folders

| Folder | What's Here |
|--------|-------------|
| `plans/` | Implementation plans for upcoming features |
| `design/` | Technical design proposals and architecture decisions |
| `bug-investigations/` | Dated investigation plans for production bugs |

## Key Documents

| Document | Path | Description |
|----------|------|-------------|
| AI Tutor Architecture | `design/plans/ai-tutor-architecture.md` | Building-block architecture for the Learner App and AI Tutor module. Covers content pipeline, AI engine, presentation modes (audio-only + avatar), learning intelligence, evaluation framework, and essential/differentiator/enhancement classification. |
| Feature Matrix | `design/plans/feature-matrix.md` | 75 features across 11 areas with MVP scope, v1.0 definition, extensions, and viewpoint tags (Student, Berlitz, Enterprise, Teacher). 38 MVP features, 37 post-MVP. |

## Product Areas

All three folders share the same product-area structure:

| Product Area | Subfolder | What's Here |
|-------------|-----------|-------------|
| AI Tutor | `ai-tutor/` | Architecture, content pipeline design, avatar tech evaluation, speech engine benchmarks |
| | | |

## Naming Conventions

- **Plans:** `{feature-name}.md`
- **Design docs:** `{feature-name}-design.md`
- **Bug investigations:** `bug-{date}-{description}/investigation-plan.md`
