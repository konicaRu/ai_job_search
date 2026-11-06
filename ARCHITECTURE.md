# ARCHITECTURE

## Назначение

Локальное рабочее пространство агента для подготовки писем и интервью по методике ai-job-search, адаптированное под русский язык и российские вакансии.

## Структура

- `AGENTS.md` — вход для агента и приоритет русского сценария.
- `AI_JOB_SEARCH_RU_SKILL_FINAL.md` — текущий сценарий письма и будущая воронка.
- `AI_JOB_SEARCH_RU_PLAN_FINAL.md` — цели и этапы.
- `.claude/skills/job-application-assistant/` — исходные методические файлы и профиль.
- `.claude/commands/` — оригинальные сценарии apply/interview/outcome и прочие.
- `tools/` — оригинальные Python-утилиты; `tests/` — их тесты.
- `.agents/skills/` — исходные поисковые порталы, зависимости пока не установлены.
- `documents/applications/` — личные архивы вакансий и интервью, исключены из Git.
- `company_research/` — исследование компании; кеш исключён из Git.
- `.runtime/` — локальный Python и кеш, исключены из Git.
- `.upstream-source/` — исходный checkout для сверки, исключён из Git.
- `UPSTREAM.md` — версия исходника; `README.upstream.md` — исходное руководство.

## Стек и команды

Агент с веб-поиском + Markdown-инструкции + Python 3.12.14. Письмо создаёт агент, Python извлекает и проверяет данные. Отдельного сервера нет.

```powershell
& '.runtime/python/cpython-3.12.14-windows-x86_64-none/python.exe' -m unittest tests.test_posting_guard tests.test_fetch_page tests.test_robots_check tests.test_page_decode
```

Входная проверка: `tools/posting_guard.py`; резервная веб-загрузка: `tools/fetch_page.py`, `tools/robots_check.py`. CodeGraph пока не инициализирован.

## Roadmap

Первое письмо на реальной вакансии → переписка HR → подготовка к интервью → расшифровка и обновление подготовки. Поиск и PDF — позже.

## Changelog

### 2026-11-06

Перенесён upstream `256237903e115f47501e7774fff9004e80c32311`, подключён русский сценарий, установлен Python. Выбранные 149 тестов прошли; создание реального письма ещё не проверялось. Инициализирован локальный Git с origin konicaRu/ai_job_search.
