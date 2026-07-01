# Contributing to HR Candidate Screening API

Thank you for contributing to the `hr-assessment-api` project. To ensure a collaborative, consistent, and clean development environment, please follow these guidelines.

## Code of Conduct

All contributors are expected to keep the workspace professional, cooperative, and welcoming. Please respect other team members and reviewers.

## Branch and Development Workflow

We use a standard branching strategy for changes:

1. **Main Branch**: `main` contains the latest stable releases.
2. **Feature Branches**: Branch out from `main` using prefix conventions:
   - `feature/your-feature` for new functionality.
   - `bugfix/issue-details` for bugs.
   - `chore/task-name` for build scripts, configs, and library bumps.

### Commit Messages

Commit messages should follow the Conventional Commits pattern to maintain a clear changelog:

- `feat: implement pdf styling for result sheets`
- `fix: resolve prisma client connection leak`
- `docs: update setup steps for bun run`
- `refactor: clean up unused interfaces`

---

## Coding Guidelines

1. **Linting and Formatting**:
   - Run the lint check using `bun run lint` before committing any code.
   - Auto-format your code using `bun run format` to match Prettier config properties.
   - Do not disable lint warnings unless absolutely necessary and documented.

2. **Prisma Schemas**:
   - If you modify `prisma/schema.prisma`, verify that you run `bunx prisma generate` to rebuild TypeScript types.
   - Double-check that your migration scripts are compatible with PostgreSQL.

3. **Submitting a Pull Request (PR)**:
   - Verify that your code compiles properly with `bun run build`.
   - Open a PR targeting `main`.
   - Describe what the PR accomplishes, and list any environment variables added or database migrations run.
