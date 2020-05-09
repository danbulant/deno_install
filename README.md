# Deno install

**Krátké příkazy k instalaci deno.**

[![Build Status](https://github.com/denoland/deno_install/workflows/ci/badge.svg?branch=master)](https://github.com/denoland/deno_install/actions)

## Instalace nejnovější verze

**Pomocí Shell (linux a Mac OS):**

```sh
curl -fsSL https://deno.land/x/install/install.sh | sh
```

**Pomocí PowerShell (Windows):**

```powershell
iwr https://deno.land/x/install/install.ps1 -useb | iex
```

## Instalace vybrané verze

**Pomocí Shell (linux a Mac OS):**

```sh
curl -fsSL https://deno.land/x/install/install.sh | sh -s v0.38.0
```

**Pomocí PowerShell (Windows):**

```powershell
iwr https://deno.land/x/install/install.ps1 -useb -outf install.ps1; .\install.ps1 v0.38.0
```

## Install via Package Manager

**Pomocí [Scoop](https://scoop.sh):**

```powershell
scoop install deno
```

**Pomocí [Homebrew](https://formulae.brew.sh/formula/deno):**

```sh
brew install deno
```

**Pomocí [Chocolatey](https://chocolatey.org/packages/deno):**

```powershell
choco install deno
```

## Instalace a spravování více verzí

**Pomocí [asdf](https://asdf-vm.com) a [asdf-deno](https://github.com/asdf-community/asdf-deno):**

```sh
asdf plugin-add deno https://github.com/asdf-community/asdf-deno.git

asdf install deno 0.38.0

# Aktivujte globálně pomocí:
asdf global deno 0.38.0

# Aktivujte lokálně do vybrané složky pomocí:
asdf local deno 0.38.0
```

**Pomocí [Scoop](https://github.com/lukesampson/scoop/wiki/Switching-Ruby-And-Python-Versions):**

```sh
# Nainstalujte vybranou verzi
scoop install deno@0.22.0

# Přepněte na v0.22.0
scoop reset deno@0.22.0

# Přepněte na nejnovější verzi
scoop reset deno
```

## Proměnné prostředí (Environment Variables)

- `DENO_INSTALL` - Složka do které se má DENO nainstalovat
  `$HOME/.deno`. Spustitelný soubor se uloží do `$DENO_INSTALL/bin`. 
  Jedna možnost jak toto využít:

  **Pomocí Shell (`/usr/local`):**

  ```sh
  curl -fsSL https://deno.land/x/install/install.sh | sudo DENO_INSTALL=/usr/local sh
  ```

  **Pomocí PowerShell (`C:\Program Files\deno`):**

  ```powershell
  # Spusťte jako administrátor
  $env:DENO_INSTALL = "C:\Program Files\deno"
  iwr https://deno.land/x/install/install.ps1 -useb | iex
  ```

## Kompatibilita

- Shell instalátor je možno použít pomocí [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about).

## Známé problémy

### Spouštění skriptů je zakázáno

```
PS C:\> iwr https://deno.land/x/install/install.ps1 -useb -outf install.ps1; .\install.ps1 v0.38.0
.\install.ps1 : File C:\install.ps1 cannot be loaded because running scripts is disabled on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:71
+ ... /x/install/install.ps1 -useb -outf install.ps1; .\install.ps1 v0.38.0
+                                                     ~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], ParentContainsErrorRecordException
    + FullyQualifiedErrorId : UnauthorizedAccess
```

*(Poznámka: pokud se Vás tento problém týká napište mi český překlad. Jelikož nepoužívám windows, nemohl jsem zreplikovat. Děkuji)*

**Kdy se tento problém objevuje?**

Pokud je [ExecutionPolicy](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_execution_policies) ve vašem systému nastaveno na `Undefined` (Nenastavené) nebo `Restricted` (omezené).

**Jak může být tento problém opraven?**

Povolte skripty z internetu nastavením ExecutionPolicy na `RemoteSigned` (vzdálené nepodepsané):

```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
```
