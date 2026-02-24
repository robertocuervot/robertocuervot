If the stats file fails or stops updating is probably due to the expiration of the PAT, 
in that case a new PAT has to be created and configured as a secret as it is explained by Copilot below (in spanish):


# 🔐 Cómo crear un *Personal Access Token* y guardarlo como secreto

## 1. Crear el token en GitHub

### 🧭 Paso 1: Ir a la sección correcta
1. Entra a GitHub.
2. Arriba a la derecha, haz clic en tu foto.
3. Ve a **Settings**.
4. En el menú lateral, baja hasta **Developer settings**.
5. Entra en **Personal access tokens**.
6. Selecciona **Fine-grained tokens** (muy importante, son los recomendados).

---

### 🛠️ Paso 2: Crear un nuevo token
1. Haz clic en **Generate new token** → **Generate new fine-grained token**.
2. Ponle un nombre, por ejemplo:  
   **readme-stats-token**
3. Opcional: establece una fecha de expiración (recomendado por seguridad).
4. En **Resource owner**, selecciona tu usuario.
5. En **Repository access**, elige:
   - **Only select repositories**
   - Selecciona tu repositorio de perfil.

---

### 🔑 Paso 3: Dar permisos mínimos necesarios
En la sección **Permissions**, configura:

#### **Repository permissions**
- **Metadata → Read**
- **Contents → Read**

Estos dos son suficientes para que GitHub Readme Stats pueda leer tus repos privados sin exponer nada.

---

### 🟢 Paso 4: Crear el token
1. Haz clic en **Generate token**.
2. GitHub te mostrará el token **una sola vez**.
3. **Cópialo inmediatamente**.

---

# 🔐 Guardar el token como secreto en tu repositorio

## 2. Guardarlo como secreto en GitHub

### 🧭 Paso 1: Ir a los secretos del repositorio
1. Entra a tu repositorio de perfil.
2. Ve a **Settings**.
3. En el menú lateral, selecciona **Secrets and variables**.
4. Entra en **Actions**.
5. Haz clic en **New repository secret**.

---

### 📝 Paso 2: Crear el secreto
- **Name:** `PAT_gh_stats`  
  (puedes usar otro nombre, pero este es claro y estándar)
- **Value:** pega el token que copiaste antes.

Haz clic en **Add secret**.

Listo: tu token está guardado de forma segura.

---

# 🔧 3. Usarlo en tu workflow

En tu archivo `.github/workflows/readme-stats.yml`, reemplaza:

```yaml
token: ${{ secrets.GITHUB_TOKEN }}
```

por:

```yaml
token: ${{ secrets.PAT_gh_stats }}
```

Con eso, las tarjetas podrán incluir estadísticas de tus repos privados sin exponer nada.

---
