# TypeScript baseUrl behavior (до TS 6)

Этот мини-проект демонстрирует поведение резолва non-relative импортов через `baseUrl`, которое использовалось в TS 5.x ("до TS 6").

## Что показывает кейс

В `tsconfig.json` задано:

- `baseUrl: "./src"`
- `paths` **не используется**

А в `src/index.ts` есть импорты вида:

- `import { answer } from "shared/answer"`
- `import { formatMessage } from "utils/format"`

В TS 5.x такие bare-like пути резолвятся в локальные файлы относительно `baseUrl`.

## Структура

- `src/index.ts` — точка входа с non-relative импортами
- `src/shared/answer.ts`
- `src/utils/format.ts`
- `src/types/env.d.ts` — декларации для демонстрации типового окружения

## Команды

```bash
npm run trace:ts5
npm run check:ts5
```

Если хотите сравнить с веткой TS 6, можно попробовать:

```bash
npm run trace:next
npm run check:next
```

## Ожидаемый эффект в trace (TS 5.x)

В `--traceResolution` вы должны увидеть, что модуль `"shared/answer"` ищется и находится как файл внутри `src/shared/answer.ts` благодаря `baseUrl`.
