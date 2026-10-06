# GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Превратить `kitkotcat` profile README в короткую входную точку в QA-портфолио с `QA Buddy` как главным публичным проектом.

**Architecture:** Меняется только presentation layer профиля: один `README.md` переписывается поверх текущего profile repo без изменения истории проектов или их кода. Проверка строится на валидности публичных ссылок, отсутствии private/internal references и соответствии утверждённой структуре.

**Tech Stack:** GitHub Profile README, Markdown, Git/GitHub.

**Spec:** `docs/superpowers/specs/2026-10-06-profile-readme-design.md`

## Global Constraints

- Позиционирование: **Екатерина Пешкун · Junior QA Engineer**.
- Фокус: `Manual QA · REST API · SQL · Python · Pytest · Playwright`.
- Featured Projects: только `qa-buddy`, `api-testing-postman`, `mobile-app-testing`.
- `QA Cat Recorder`, `performance_lab`, `web-ui-ux-testing` не выводить в Featured Projects на этом этапе.
- Не ссылаться на private/internal repositories.
- English summary — не более 2 строк.
- Не использовать badge spam, GitHub stats, streaks, trophies и декоративный визуальный шум.
- Profile README не должен дублировать CV или длинно описывать стажировочные проекты.

## Review Focus

- Все Featured Project URLs должны открываться как публичные repositories.
- README не должен содержать ссылки на `boost`, `boost-demo`, `key-to-trust-mvp` или другие private/internal projects.
- `QA Cat Recorder` не должен появиться как featured project до завершения Store review/private-source решения.
- Формулировки про Playwright должны отражать обучение/практику, а не заявлять production-level expertise.
- Контактные ссылки должны сохранить существующие корректные email/Telegram данные без изменения адресов.

---

### Task 1: Сократить и перестроить profile README

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: утверждённую структуру и wording constraints из design spec.
- Produces: один читаемый profile README с Header, Featured Projects, Tools & Skills, Currently Learning, English Summary и Contacts.

- [ ] **Step 1: Зафиксировать текущий README как baseline для сравнения**

Run:

```bash
git show HEAD:README.md > /tmp/kitkotcat-readme-before.md
```

Expected: файл `/tmp/kitkotcat-readme-before.md` существует и содержит текущий длинный профиль.

- [ ] **Step 2: Переписать `README.md` по утверждённой структуре**

Required order:

```text
# Екатерина Пешкун
Junior QA Engineer
focus line
короткое summary
Featured Projects
Tools & Skills
Currently Learning
English summary
Contacts
```

`QA Buddy` должен быть первым и визуально самым заметным проектом. `api-testing-postman` и `mobile-app-testing` идут следом как дополнительные evidence repositories.

- [ ] **Step 3: Проверить, что README не содержит удалённые длинные секции и запрещённые featured projects**

Run:

```bash
python3 - <<'PY'
from pathlib import Path
text = Path('README.md').read_text()
forbidden = [
    '## Практический опыт',
    'Корпоративная web-платформа',
    'Web-сервис с backend-инфраструктурой',
    'QA Buddy Recorder — в разработке',
]
assert all(item not in text for item in forbidden), forbidden
for project in ['qa-buddy', 'api-testing-postman', 'mobile-app-testing']:
    assert project in text, project
print('README_STRUCTURE_OK')
PY
```

Expected: `README_STRUCTURE_OK`.

- [ ] **Step 4: Проверить private/internal references и позиционирование Automation**

Run:

```bash
python3 - <<'PY'
from pathlib import Path
text = Path('README.md').read_text().lower()
for private_name in ['boost-demo', 'key-to-trust-mvp']:
    assert private_name not in text, private_name
assert 'playwright' in text
assert 'изуч' in text or 'learning' in text or 'practice' in text
print('PUBLIC_POSITIONING_OK')
PY
```

Expected: `PUBLIC_POSITIONING_OK`.

- [ ] **Step 5: Commit README rewrite**

```bash
git add README.md
git commit -m "docs: обновить GitHub profile README"
```

---

### Task 2: Проверить публичные ссылки и финальный diff

**Files:**
- Verify: `README.md`
- Verify: `docs/superpowers/specs/2026-10-06-profile-readme-design.md`
- Verify: `docs/superpowers/plans/2026-10-06-profile-readme.md`

**Interfaces:**
- Consumes: финальный README из Task 1.
- Produces: подтверждение, что профиль ведёт только на корректные публичные проекты и не содержит случайных regressions.

- [ ] **Step 1: Проверить три Featured repositories через GitHub**

Verify these exact URLs return publicly accessible repositories:

```text
https://github.com/kitkotcat/qa-buddy
https://github.com/kitkotcat/api-testing-postman
https://github.com/kitkotcat/mobile-app-testing
```

Expected: все три repositories публичные и доступны без private-only references.

- [ ] **Step 2: Проверить Markdown links в README**

Run:

```bash
python3 - <<'PY'
from pathlib import Path
import re
text = Path('README.md').read_text()
links = re.findall(r'\[[^\]]+\]\((https?://[^)]+)\)', text)
assert links, 'No links found'
assert all('github.com/kitkotcat/' in u or 't.me/' in u for u in links)
print('LINK_SET_OK', len(links))
PY
```

Expected: `LINK_SET_OK <N>`.

- [ ] **Step 3: Проверить отсутствие whitespace/merge artifacts**

Run:

```bash
git diff --check origin/main...HEAD
```

Expected: no output, exit code 0.

- [ ] **Step 4: Review final diff against the spec**

Run:

```bash
git diff --stat origin/main...HEAD
git diff origin/main...HEAD -- README.md
```

Expected: README стал короче, Featured Projects видны явно, лишние стажировочные подробности удалены, контакты сохранены.

- [ ] **Step 5: Push branch and create PR**

```bash
git push origin docs/profile-readme-refresh
```

Create PR:

```text
base: main
head: docs/profile-readme-refresh
title: docs: refresh GitHub profile README
```

PR body должен кратко перечислить: сокращение profile README, три featured projects, public-link validation и сохранение learning-level wording для Playwright.

---

### Task 3: Pinning handoff after merge

**Files:**
- No repository file changes.

**Interfaces:**
- Consumes: merged profile README.
- Produces: ручной порядок pinned repositories в GitHub UI.

- [ ] **Step 1: После merge открыть GitHub profile pin editor**

Target order:

```text
1. qa-buddy
2. api-testing-postman
3. mobile-app-testing
```

- [ ] **Step 2: Не закреплять `performance_lab`, `qa-cat-recorder` или `web-ui-ux-testing` до отдельного решения/audit**

Expected: первые три pinned repositories соответствуют README и не создают противоречия с portfolio positioning.
