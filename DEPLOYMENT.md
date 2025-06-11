# GitHub Pages Deployment Guide

## 🚀 Текущий статус

Сайт успешно развернут на GitHub Pages: https://nullianism.github.io/

## 📋 Как работает деплой

1. **Автоматический деплой**: При каждом push в ветку `main` запускается GitHub Actions workflow
2. **Build процесс**: 
   - Синхронизация контента из submodule
   - Сборка Next.js приложения с статическим экспортом
   - Загрузка артефактов на GitHub Pages

## 🔧 Настройка (уже выполнена)

### 1. GitHub Actions Workflow
Файл `.github/workflows/deploy.yml` настроен для:
- Сборки Next.js приложения
- Использования официального GitHub Pages Action
- Кеширования зависимостей для ускорения сборки

### 2. Next.js конфигурация
В `next.config.ts`:
- `output: 'export'` - для статического экспорта
- `images.unoptimized: true` - для работы без серверной оптимизации

### 3. Настройки репозитория
В настройках репозитория на GitHub:
- Settings → Pages → Source: **GitHub Actions**

## 🛠️ Полезные команды

```bash
# Проверить статус деплоя
./scripts/check-deployment.sh

# Посмотреть логи последних запусков
gh run list --limit 5

# Посмотреть детали конкретного запуска
gh run view <RUN_ID>

# Локальная сборка для проверки
npm run build
```

## 📝 Важные моменты

1. **НЕ используйте ветку gh-pages** - GitHub Actions автоматически управляет деплоем
2. **.nojekyll файл** автоматически добавляется при сборке
3. **Submodules** автоматически обновляются при сборке

## 🐛 Решение проблем

### Если сайт показывает README.md вместо Next.js приложения:
1. Проверьте Settings → Pages → Source = "GitHub Actions"
2. Запустите workflow вручную: Actions → Deploy to GitHub Pages → Run workflow

### Если build падает:
1. Проверьте логи: `gh run view <RUN_ID> --log`
2. Убедитесь, что локально `npm run build` работает
3. Проверьте, что все зависимости установлены

## 📚 Ресурсы

- [Next.js Static Exports](https://nextjs.org/docs/app/building-your-application/deploying/static-exports)
- [GitHub Pages documentation](https://docs.github.com/en/pages)
- [GitHub Actions for Pages](https://github.com/actions/deploy-pages)
