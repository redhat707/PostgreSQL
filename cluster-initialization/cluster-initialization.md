# 02 - PostgreSQL adatbázis-klaszter inicializálása

Az előző lépésben a PostgreSQL szervert már telepítettük.

Most inicializáljuk az adatbázis-klasztert, majd elindítjuk a PostgreSQL szolgáltatást.

---

## 1. Adatbázis-klaszter inicializálása

Rocky Linux / RHEL rendszeren:

```bash
sudo postgresql-setup --initdb
```

Sikeres inicializálás esetén ehhez hasonló eredményt kapunk:

```text
Initializing database ... OK
```

> Az inicializálást csak egyszer kell elvégezni egy új PostgreSQL telepítés után.

---

## 2. Az adatkönyvtár ellenőrzése

Az alapértelmezett PostgreSQL adatkönyvtár:

```text
/var/lib/pgsql/data
```

Ellenőrzés:

```bash
sudo ls -la /var/lib/pgsql/data
```

Fontosabb létrejött fájlok és könyvtárak:

```text
postgresql.conf
pg_hba.conf
pg_ident.conf
base/
global/
pg_wal/
```

### Fontos fájlok

- `postgresql.conf` - a PostgreSQL fő konfigurációs fájlja
- `pg_hba.conf` - hozzáférési és hitelesítési szabályok
- `pg_wal/` - Write-Ahead Log fájlok

---

## 3. PostgreSQL szolgáltatás indítása

```bash
sudo systemctl start postgresql
```

---

## 4. Automatikus indítás engedélyezése

Így a PostgreSQL rendszerindítás után is automatikusan elindul:

```bash
sudo systemctl enable postgresql
```

A kettő egy paranccsal is elvégezhető:

```bash
sudo systemctl enable --now postgresql
```

---

## 5. Szolgáltatás állapotának ellenőrzése

```bash
sudo systemctl status postgresql
```

A helyes állapot:

```text
Active: active (running)
```

Gyors ellenőrzés:

```bash
systemctl is-active postgresql
systemctl is-enabled postgresql
```

Elvárt eredmény:

```text
active
enabled
```

---

## 6. Kapcsolódás PostgreSQL-hez

Váltás a `postgres` rendszerfelhasználóra:

```bash
sudo -iu postgres
```

PostgreSQL konzol indítása:

```bash
psql
```

Sikeres kapcsolódás esetén:

```text
postgres=#
```

---

## 7. Adatbázisok ellenőrzése

A PostgreSQL konzolban:

```sql
\l
```

Az inicializálás után többek között ezek az adatbázisok léteznek:

```text
postgres
template0
template1
```

Kilépés a PostgreSQL konzolból:

```sql
\q
```

Majd kilépés a `postgres` Linux-felhasználóból:

```bash
exit
```

---

## 8. Gyors ellenőrzés

Az adatbázisok megjelenítése közvetlenül Linuxból:

```bash
sudo -u postgres psql -c '\l'
```

PostgreSQL verzió ellenőrzése:

```bash
sudo -u postgres psql -c 'SELECT version();'
```

---

## Röviden

A teljes folyamat:

```bash
sudo postgresql-setup --initdb
sudo systemctl enable --now postgresql
sudo systemctl status postgresql
sudo -u postgres psql -c '\l'
```

---

## Mit tanultunk?

Ebben a feladatban:

- inicializáltuk a PostgreSQL adatbázis-klasztert
- ellenőriztük az adatkönyvtárat
- elindítottuk a PostgreSQL szolgáltatást
- engedélyeztük az automatikus indulást
- csatlakoztunk a PostgreSQL szerverhez
- ellenőriztük az alapértelmezett adatbázisokat

---

**Következő lépés:** PostgreSQL alapkonfiguráció és a `postgresql.conf` megismerése.
