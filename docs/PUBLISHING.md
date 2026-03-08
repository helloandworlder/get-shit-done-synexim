# Publishing

Use this checklist before the first public npm release of `get-shit-done-synexim`.

## 1. Verify npm account

```bash
npm whoami
```

If not logged in:

```bash
npm login
```

## 2. Verify package name availability

```bash
npm view get-shit-done-synexim version
```

- If npm returns `404`, the package name is still available.
- If npm returns a version, the package already exists and you should confirm ownership before publishing.

## 3. Run release checks

```bash
npm run release:check
```

This runs:
- `npm test`
- `npm pack --dry-run`
- `npm publish --dry-run --access public`

## 4. Publish

```bash
npm publish --access public
```

## 5. Verify install

```bash
npx get-shit-done-synexim@latest --help
```

## Notes

- `publishConfig.access` is already set to `public` in `package.json`.
- The package is intended to be installable via `npx get-shit-done-synexim@latest`.
- If the published package is not picked up immediately, wait for npm registry propagation and retry.
