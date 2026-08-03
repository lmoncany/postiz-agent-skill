# Postiz CLI / API reference

## Useful commands

```bash
postiz integrations:list
postiz posts:create -c "Hello" -s "2026-08-04T09:00:00Z" -i "<integration-id>"
```

## Public API endpoints

- `GET /api/public/v1/is-connected`
- `GET /api/public/v1/integrations`
- `POST /api/public/v1/upload`
- `POST /api/public/v1/posts`
- `GET /api/public/posts/<id>`

## Scheduling rule

1. List integrations.
2. Pick the one with the right `identifier`.
3. Create the post.
4. Read it back and verify the state.
