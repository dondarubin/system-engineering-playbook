# StartON Launchpad — Системная инженерия

Документация проекта StartON Launchpad — Разработка программного обеспечения для привлечения инвестиций с использованием современных решений.

---

## Локальная разработка

1. Установите mdBook: [инструкция](https://rust-lang.github.io/mdBook/guide/installation.html)
2. Запустите сервер разработки:

```bash
make dev
```

или

```bash
mdbook serve --open
```

3. Откройте http://localhost:3000 в браузере

## Развёртывание на GitHub Pages

1. Перейдите в Settings → Actions → General
2. Установите "Read and write permissions" в Workflow permissions
3. После push в main автоматически запустится сборка
4. В Settings → Pages выберите ветку `gh-pages`
5. Документация будет доступна по адресу: `https://[username].github.io/system-engineering-playbook/`
