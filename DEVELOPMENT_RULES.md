# Постоянные правила разработки

Для проекта LibertyHell соблюдай существующую архитектуру и изменяй только относящиеся к задаче файлы. Разбивай крупную задачу на небольшие самостоятельные этапы и выполняй их последовательно. Проверяй каждый этап, по возможности сохраняя работоспособность проекта, и регулярно запускай подходящие тесты, линтеры и проверки типов.

Храни инструкции агента, планы, временные анализы, заметки и служебные материалы в существующем F:\pd\agent_data; не создавай другой agent_data, не коммить его содержимое и не делай его зависимостью запуска, сборки или тестов проекта. В репозитории оставляй необходимые исходники, конфигурацию, тесты и документацию. Прежде чем перемещать или удалять существующие файлы, проверь их назначение, ссылки и последствия. Не создавай AGENTS.md внутри репозитория и не изменяй общую .gitignore без необходимости.

Перед каждой задачей читай DEVELOPMENT_RULES.md, COMMIT_STRATEGY.md и WORKFLOW.md; для крупной задачи используй PROGRESS_TEMPLATE.md. Соблюдай более приоритетные инструкции и явные указания пользователя для текущей задачи. Перед завершением проверяй git status, новые файлы, staged diff, служебные артефакты, отсутствие зависимости приложения от agent_data и релевантные проверки; не включай посторонние файлы в коммит.

---

# Repository Hygiene and Agent Data Isolation

These rules are mandatory for all future development tasks and take priority over ordinary file organization preferences.

## 1. Main principle

The main Git repository must contain only legitimate project files that serve a clear technical, functional, testing, build, deployment, or documentation purpose.

All agent-specific instructions, internal plans, temporary analyses, progress notes, prompts, session artifacts, and other auxiliary development materials must be stored in the existing `agent_data` directory.

Do not create a new `agent_data` directory. Use the existing one.

The presence of development automation must not introduce unnecessary files, configuration changes, or dependencies into the application.

## 2. File placement decisions

Before creating any file, determine:

1. Is this file required for the application to function correctly?
2. Is it required for building, testing, deployment, or legitimate project maintenance?
3. Does it contain agent-specific instructions, prompts, traces, metadata, or internal development notes?
4. Can it be stored in `agent_data` without affecting the project?
5. Can the same functionality be implemented using existing standard project conventions?

Apply the following rules:

- If the file is auxiliary and not necessary for the project, place it in `agent_data`.
- If the file contains agent-specific information, place it in `agent_data`.
- If the file is a temporary implementation plan, place it in `agent_data`.
- If the file is a development progress tracker, place it in `agent_data`.
- If the file is required for the application, keep it in the appropriate project directory.
- If an essential file contains unnecessary agent-specific metadata, remove that metadata while preserving its legitimate functionality.
- If an agent-specific file appears to be required for the application, redesign the integration so the application no longer depends on that agent-specific file.
- Never remove a genuinely required file merely because its name or contents appear unusual.

## 3. Files that belong in agent_data

Unless explicitly required otherwise, store the following outside the normal application structure, inside `agent_data`:

- Agent instructions and behavioral rules.
- AGENTS.md files used exclusively to configure development agents.
- Prompts and prompt templates.
- Agent-specific configuration and metadata.
- Internal implementation plans.
- Progress tracking files.
- Session summaries and continuation notes.
- Temporary architecture analyses.
- Internal review notes.
- Agent-specific checklists.
- Intermediate investigation reports.
- Temporary debugging notes.
- Development automation scratch files.
- Other auxiliary artifacts unrelated to application runtime.

Do not commit these files to the main project's Git history.

## 4. Essential project files

Some files may be essential even if they were initially created by an automated development tool.

When encountering such a file:

1. Determine its actual role in the project.
2. Preserve required functionality.
3. Remove unnecessary agent-specific comments, instructions, and metadata.
4. Use ordinary, descriptive naming consistent with the project's conventions.
5. Prefer standard application configuration and dependency mechanisms.
6. If the file exists solely to support the development agent, move it to `agent_data` and remove the application's dependency on it.
7. Verify the project works without auxiliary files from `agent_data`.

Never disguise malicious functionality, security-sensitive changes, or material project behavior.

## 5. Repository isolation

- Do not create project-local agent instruction files.
- Keep the global Codex configuration outside the repository.
- Do not create redundant instruction copies in application directories.
- Avoid introducing agent-specific dependencies into production code.
- Do not require agent_data for application startup, builds, tests, or deployment.
- Do not modify tracked files merely to store agent preferences.
- Preserve all legitimate dependencies, configuration files, and documentation.
- Do not delete or relocate existing tracked files without checking their references and impact.
- Do not alter Git history to conceal previous development activity.

If `agent_data` is inside the Git working tree, use a local exclusion mechanism for untracked auxiliary files when appropriate, without changing the shared .gitignore unnecessarily.

Remember that .git/info/exclude does not untrack previously committed files.

## 6. Verification after every development task

Before completing a task:

1. Inspect `git status`.
2. Inspect all newly created files.
3. Review the staged diff.
4. Identify any auxiliary or agent-specific artifacts.
5. Ensure such artifacts are placed in `agent_data`.
6. Confirm that legitimate source files remain in their correct locations.
7. Run relevant build and test checks.
8. Verify that the application does not depend on `agent_data`.
9. Confirm no unrelated auxiliary files are staged.
10. Create Git commits only for legitimate project changes.

Do not claim that all automation traces are absent or undetectable. The goal is clean project organization, not falsification of provenance.

