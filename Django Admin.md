---
Title: Admin Panel
Date: 01.03.2024
Time: 12:35
tags:
  - cheatsheet
  - credentials
---
### Add Admin Permissions to Managers (Manual)

`django shell`:
```python
Permission.objects.values('codename', 'id')  # List all permission id, codename
permission = Permission.objects.get(id=id)
user = User.objects.get(email='some@email.com')
user.user_permissions.add(permission)
user.save()
```

# Squash migrations

1. Squash migrations in application `accounts`
```python
./manage.py squashmigrations accounts 0001_first_migration 0002_second_migration --squashed-name squash_0001_0002
```

2. Push migration to all instances
3. Remove `replace` and dependencies
4. Push updates again
5. List applied migrations

```python
./manage.py showmigrations
```
------------------------------------
