# Flujo de trabajo en Git y GitHub — A ProP

## 1. Ramas y cambios
- **`main`**: Rama principal con la base validada del proyecto.
- **Ramas de trabajo o commits incrementales**: Subir cambios pequeños por componente o archivo con mensajes claros en inglés o español.

## 2. Mensajes de commit recomendados
- `Add base inventory.ini for A ProP infrastructure`
- `Add base Nginx reverse proxy template for A ProP`
- `Document Vault variables structure in variables/vault.yml`

## 3. Seguridad y variables sensibles
- No guardar contraseñas, claves privadas ni tokens en texto plano en el repositorio.
- Gestionar los secretos mediante **Ansible Vault** en `variables/vault.yml`.
