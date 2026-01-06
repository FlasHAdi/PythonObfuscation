# Obfuscare Module Python - Ghid de Utilizare

## Ce este asta?

Acesta este un **Instrument de Protecție prin Obfuscare a Modulelor Python** care redenumește automat toate metodele extensiilor Python C++ în șiruri aleatorii, făcând extrem de dificilă înțelegerea structurii codului pentru inginerii reverse. Protejează logica jocului/aplicației tale ascunzând numele reale ale funcțiilor atât în fișierele sursă C++ cât și în scripturile Python.

## Ce protejează?

- **Ascunde numele funcțiilor**: Înlocuiește toate numele metodelor PyMethodDef cu șiruri aleatorii (ex: `GetMainCharacterIndex` devine `xKjPqRtYwZaB`)
- **Sincronizează modificările**: Actualizează automat atât modulele C++ cât și fișierele Python pentru a folosi noile nume obfuscate
- **Păstrează funcționalitatea**: Aplicația ta continuă să funcționeze exact ca înainte, dar cu nume de metode ascunse
- **Protecție declarații import**: Menține declarațiile `from module import function` neschimbate pentru compatibilitate

## Cum se folosește

### Pasul 1: Exportă Fișierele Modulelor Python

Înainte de obfuscare, ar trebui să extragi doar fișierele care conțin metode Python:

1. **Rulează** `export_py_modules.py`
2. **Trage și lasă** folderul tău `Binary` pe script, SAU
3. **Scrie/lipește** calea când ești întrebat
4. Scriptul va copia toate fișierele relevante în folderul `Export_PythonModules`

### Pasul 2: Obfuscă Codul

1. **Rulează** `obfuscate_py_module.py`
2. **Furnizează două foldere**:
   - **Folderul Binary C++**: Conține fișierele sursă C++ ale jocului/aplicației tale (ex: `Binary/UserInterface/`)
   - **Folderul rădăcină Python**: Conține scripturile tale Python (ex: `root/`)
3. Poți:
   - Trage ambele foldere pe script deodată (C++ primul, apoi Python)
   - Trage un folder și scrie a doua cale
   - Rulează normal și scrie/lipește ambele căi

### Pasul 3: Verifică Backup-urile

Scriptul creează automat backup-uri cu timestamp înainte de a face orice modificări:
- `Binary_backup_20260106`
- `root_backup_20260106`

Păstrează aceste backup-uri în siguranță în caz că trebuie să restaurezi fișierele originale!

### Pasul 4: Compilează și Testează

1. Recompilează proiectul C++ cu fișierele sursă obfuscate
2. Testează aplicația cu scripturile Python obfuscate
3. Toată funcționalitatea ar trebui să funcționeze exact ca înainte, dar cu nume de metode ascunse

## Exemplu

**Înainte de obfuscare (C++):**
```cpp
static PyMethodDef s_methods[] =
{
    { "GetMainCharacterIndex", playerGetMainCharacterIndex, METH_NOARGS },
    { "SetAttackKeyState", playerSetAttackKeyState, METH_VARARGS },
    { NULL, NULL, NULL }
};
```

**După obfuscare (C++):**
```cpp
static PyMethodDef s_methods[] =
{
    { "xKjPqRtYwZaB", playerGetMainCharacterIndex, METH_NOARGS },
    { "mNpQrStUvWxY", playerSetAttackKeyState, METH_VARARGS },
    { NULL, NULL, NULL }
};
```

**Înainte de obfuscare (Python):**
```python
import player
index = player.GetMainCharacterIndex()
player.SetAttackKeyState(True)
```

**După obfuscare (Python):**
```python
import player
index = player.xKjPqRtYwZaB()
player.mNpQrStUvWxY(True)
```

## Note Importante

- ⚠️ Fă întotdeauna backup la fișierele tale înainte de a rula obfuscarea
- ⚠️ Testează amănunțit după obfuscare pentru a te asigura că totul funcționează
- ⚠️ Păstrează o mapare a numelor vechi→noi dacă trebuie să faci debug
- ⚠️ Rulează obfuscarea doar o dată per ciclu de build
- ✅ Scriptul gestionează multiple encodinguri de fișiere (UTF-8, EUC-KR, CP949, etc.)
- ✅ Declarațiile import rămân neschimbate pentru mai bună compatibilitate

## Rezolvarea Problemelor

**Î: Scriptul spune "Invalid directory path"**
- Asigură-te că furnizezi calea corectă către folder
- Încearcă să tragi folderul direct pe fișierul scriptului

**Î: Unele funcții nu sunt obfuscate**
- Scriptul procesează doar fișierele care conțin `static PyMethodDef s_methods[]`
- Verifică dacă modulul tău definește corect această structură

**Î: Aplicația se blochează după obfuscare**
- Restaurează din backup
- Verifică că atât fișierele C++ cât și Python au fost procesate
- Verifică că codul C++ se compilează fără erori
