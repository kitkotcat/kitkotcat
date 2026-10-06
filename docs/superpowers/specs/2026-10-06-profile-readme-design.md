# GitHub Profile README — Design

## Goal

Сделать профиль `kitkotcat` короткой входной точкой в QA-портфолио, а не вторым резюме. Пользователь профиля должен за 15–30 секунд понять специализацию, увидеть ключевые навыки и перейти к сильным публичным проектам.

## Audience

- QA recruiters / HR;
- QA Lead / Senior QA;
- hiring managers;
- разработчики и коллеги, которые открывают GitHub из резюме.

## Positioning

Основное позиционирование:

**Екатерина Пешкун · Junior QA Engineer**

Фокус:

`Manual QA · REST API · SQL · Python · Pytest · Playwright`

Профиль должен показывать практический QA-фокус: Web/API/Backend, тестовая документация, CI и переход к автоматизации на Python.

## README structure

### 1. Header

- имя и роль;
- одна строка с ключевым стеком;
- 3–4 короткие строки о специализации;
- без длинной истории стажировок.

### 2. Featured Projects

В README показываются три основных публичных проекта:

1. **QA Buddy** — главный flagship project.
   - Web/API/Backend/Android QA portfolio;
   - test documentation;
   - Pytest;
   - CI quality gate.

2. **API Testing / Postman** — отдельное доказательство API testing practice.

3. **Mobile App Testing** — отдельное доказательство mobile QA practice.

`QA Cat Recorder` пока не выводится как основной featured project до завершения Chrome Web Store review и финального решения по private source repository.

`performance_lab` не выводится в top section: репозиторий слишком маленький и слабее трёх выбранных проектов.

`web-ui-ux-testing` пока не выводится до отдельного аудита.

### 3. Tools & Skills

Компактный блок без длинных описаний:

- Web/API: REST API, HTTP, JSON, Postman, Swagger/OpenAPI, DevTools;
- Data: SQL, PostgreSQL, DBeaver;
- QA: Test Design, Test Cases, Checklists, Bug Reports, Smoke/Regression/Retest;
- Engineering: Git, GitHub/GitLab, Docker;
- Automation: Python, Pytest, Playwright (learning/practice).

### 4. Currently Learning

Коротко:

**Python + Playwright test automation**

Допустимо перечислить:
- UI automation;
- API automation;
- fixtures / parametrization;
- CI integration.

### 5. Contacts

- GitHub;
- email;
- Telegram.

### 6. English summary

Не более 2 строк. Нужен только как быстрый ориентир для англоязычного посетителя.

## Content to remove

Из текущего README убрать:

- длинный блок «Практический опыт»;
- детальное описание корпоративной платформы;
- длинный блок про Docker/Redis/MinIO;
- повторяющиеся списки QA-практик;
- подробное объяснение нагрузочного тестирования;
- длинный отдельный блок про QA Buddy Recorder «в разработке»;
- дублирование информации из резюме.

Эти детали лучше хранить в CV и конкретных project README.

## Visual style

- чистый Markdown;
- без badge spam;
- без длинных tables, если они не ускоряют чтение;
- без GitHub stats widgets;
- без activity streaks / trophies;
- без декоративного визуального шума.

Главный визуальный акцент — названия и ссылки на проекты.

## Repository pinning

Рекомендуемый порядок pinned repositories:

1. `qa-buddy`
2. `api-testing-postman`
3. `mobile-app-testing`
4. `web-ui-ux-testing` — только после отдельного аудита

Pinning делается через GitHub UI, так как доступный connector не предоставляет write-action для pinned repositories.

## Success criteria

После обновления профиля:

- ключевая специализация видна без скролла или почти без него;
- QA Buddy виден как главный portfolio project;
- нет противоречия между profile README и реальным состоянием публичных репозиториев;
- profile README не повторяет CV;
- все project links рабочие;
- нет ссылок на private/internal projects;
- нет заявлений о навыках/опыте, которые не подтверждаются текущими публичными материалами или резюме пользователя.
