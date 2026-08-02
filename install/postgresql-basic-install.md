# PostgreSQL Basic Install on RHEL / Rocky Linux

Ez egy alap PostgreSQL gyakorló jegyzet Linux admin / RHCSA utáni tanuláshoz.

## 1. PostgreSQL telepítése

```bash
dnf install postgresql-server postgresql-contrib -y
```

## 2. Adatbázis inicializálása

```bash
postgresql-setup --initdb
```

## 3. Szolgáltatás indítása és engedélyezése boot utánra

```bash
systemctl enable --now postgresql
```

## 4. Állapot ellenőrzése

```bash
systemctl status postgresql
```

## 5. Belépés postgres felhasználóval

```bash
su - postgres
```

PostgreSQL konzol indítása:

```bash
psql
```

Kilépés a PostgreSQL konzolból:

```sql
\q
```

Kilépés a postgres Linux felhasználóból:

```bash
exit
```

## 6. Teszt adatbázis létrehozása

```bash
su - postgres
createdb testdb
psql
```

PostgreSQL-ben:

```sql
\l
```

Kilépés:

```sql
\q
```

## 7. Teszt user létrehozása

```bash
su - postgres
createuser testuser
psql
```

PostgreSQL-ben:

```sql
ALTER USER testuser WITH PASSWORD 'Password123';
```

Kilépés:

```sql
\q
```

## 8. Adatbázis törlése gyakorlás után

```bash
su - postgres
dropdb testdb
```

## 9. Fontos parancsok

```bash
systemctl status postgresql
systemctl restart postgresql
systemctl enable postgresql
systemctl is-enabled postgresql
```

## 10. Hasznos psql parancsok

```sql
\l
```

Adatbázisok listázása.

```sql
\du
```

Felhasználók / role-ok listázása.

```sql
\c adatbazis_neve
```

Kapcsolódás egy adatbázishoz.

```sql
\dt
```

Táblák listázása az aktuális adatbázisban.

```sql
\q
```

Kilépés.

## 11. Ellenőrző lista

- PostgreSQL csomag telepítve
- Adatbázis inicializálva
- `postgresql` service fut
- Service engedélyezve boot utánra
- Be lehet lépni `postgres` userként
- `psql` működik
- Teszt adatbázis létrehozható
- Teszt user létrehozható

## Rövid összefoglaló

A PostgreSQL nem csak egy program, hanem Linuxon szolgáltatásként fut.  
Admin oldalról fontos tudni:

- hogyan telepítjük,
- hogyan inicializáljuk,
- hogyan indítjuk systemd-vel,
- hogyan ellenőrizzük,
- hogyan hozunk létre adatbázist és felhasználót.
