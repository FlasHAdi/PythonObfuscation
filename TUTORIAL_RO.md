# Obfuscare Module Python - Ghid de Utilizare

## Ce este asta?

Acesta este un **Instrument de Protec?ie prin Obfuscare a Modulelor Python** care redenume?te automat toate metodele extensiilor Python C++ în ?iruri aleatorii, f?când extrem de dificil? în?elegerea structurii codului pentru inginerii reverse. Protejeaz? logica jocului/aplica?iei tale ascunzând numele reale ale func?iilor atât în fi?ierele surs? C++ cât ?i în scripturile Python.

## Ce protejeaz??

- **Ascunde numele func?iilor**: Înlocuie?te toate numele metodelor PyMethodDef cu ?iruri aleatorii (ex: `GetMainCharacterIndex` devine `xKjPqRtYwZaB`)
- **Sincronizeaz? modific?rile**: Actualizeaz? automat atât modulele C++ cât ?i fi?ierele Python pentru a folosi noile nume obfuscate
- **P?streaz? func?ionalitatea**: Aplica?ia ta continu? s? func?ioneze exact ca înainte, dar cu nume de metode ascunse
- **Protec?ie declara?ii import**: Men?ine declara?iile `from module import function` neschimbate pentru compatibilitate

## Cum se folose?te

### Pasul 1: Export? Fi?ierele Modulelor Python

Înainte de obfuscare, ar trebui s? extragi doar fi?ierele care con?in metode Python:

1. **Ruleaz?** `export_py_modules.py`
2. **Trage ?i las?** folderul t?u `Binary` pe script, SAU
3. **Scrie/lipe?te** calea când e?ti întrebat
4. Scriptul va copia toate fi?ierele relevante în folderul `Export_PythonModules`

### Pasul 2: Obfusc? Codul

1. **Ruleaz?** `obfuscate_py_module.py`
2. **Furnizeaz? dou? foldere**:
   - **Folderul Binary C++**: Con?ine fi?ierele surs? C++ ale jocului/aplica?iei tale (ex: `Binary/UserInterface/`)
   - **Folderul r?d?cin? Python**: Con?ine scripturile tale Python (ex: `root/`)
3. Po?i:
   - Trage ambele foldere pe script deodat? (C++ primul, apoi Python)
   - Trage un folder ?i scrie a doua cale
   - Ruleaz? normal ?i scrie/lipe?te ambele c?i

### Pasul 3: Verific? Backup-urile

Scriptul creeaz? automat backup-uri cu timestamp înainte de a face orice modific?ri:
- `Binary_backup_20260106`
- `root_backup_20260106`

P?streaz? aceste backup-uri în siguran?? în caz c? trebuie s? restaurezi fi?ierele originale!

### Pasul 4: Compileaz? ?i Testeaz?

1. Recompileaz? proiectul C++ cu fi?ierele surs? obfuscate
2. Testeaz? aplica?ia cu scripturile Python obfuscate
3. Toat? func?ionalitatea ar trebui s? func?ioneze exact ca înainte, dar cu nume de metode ascunse

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

**Dup? obfuscare (C++):**
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

**Dup? obfuscare (Python):**
```python
import player
index = player.xKjPqRtYwZaB()
player.mNpQrStUvWxY(True)
```

## Note Importante

- ?? F? întotdeauna backup la fi?ierele tale înainte de a rula obfuscarea
- ?? Testeaz? am?nun?it dup? obfuscare pentru a te asigura c? totul func?ioneaz?
- ?? P?streaz? o mapare a numelor vechi?noi dac? trebuie s? faci debug
- ?? Ruleaz? obfuscarea doar o dat? per ciclu de build
- ? Scriptul gestioneaz? multiple encodinguri de fi?iere (UTF-8, EUC-KR, CP949, etc.)
- ? Declara?iile import r?mân neschimbate pentru mai bun? compatibilitate

## Rezolvarea Problemelor

**Î: Scriptul spune "Invalid directory path"**
- Asigur?-te c? furnizezi calea corect? c?tre folder
- Încearc? s? tragi folderul direct pe fi?ierul scriptului

**Î: Unele func?ii nu sunt obfuscate**
- Scriptul proceseaz? doar fi?ierele care con?in `static PyMethodDef s_methods[]`
- Verific? dac? modulul t?u define?te corect aceast? structur?

**Î: Aplica?ia se blocheaz? dup? obfuscare**
- Restaureaz? din backup
- Verific? c? atât fi?ierele C++ cât ?i Python au fost procesate
- Verific? c? codul C++ se compileaz? f?r? erori

## Suport

Pentru probleme sau întreb?ri, te rug?m contacteaz? dezvoltatorul.
