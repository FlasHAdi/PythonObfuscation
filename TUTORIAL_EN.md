# Python Module Obfuscation - User Guide

## What is this?

This is a **Python Module Obfuscation Protection Tool** that automatically renames all Python C++ extension methods to random strings, making it extremely difficult for reverse engineers to understand your code structure. It protects your game/application logic by hiding the actual function names in both C++ source files and Python scripts.

## What does it protect?

- **Hides function names**: Replaces all PyMethodDef method names with random strings (e.g., `GetMainCharacterIndex` becomes `xKjPqRtYwZaB`)
- **Synchronizes changes**: Automatically updates both C++ modules and Python files to use the new obfuscated names
- **Preserves functionality**: Your application continues to work exactly as before, but with hidden method names
- **Import statements protection**: Keeps `from module import function` statements unchanged for compatibility

## How to use

### Step 1: Export Python Module Files

Before obfuscating, you should first extract only the files that contain Python methods:

1. **Run** `export_py_modules.py`
2. **Drag and drop** your `Binary` folder onto the script, OR
3. **Type/paste** the path when prompted
4. The script will copy all relevant files to `Export_PythonModules` folder

### Step 2: Obfuscate Your Code

1. **Run** `obfuscate_py_module.py`
2. **Provide two folders**:
   - **C++ Binary folder**: Contains your compiled game/app C++ source files (e.g., `Binary/UserInterface/`)
   - **Python root folder**: Contains your Python scripts (e.g., `root/`)
3. You can:
   - Drag both folders onto the script at once (C++ first, then Python)
   - Drag one folder and type the second path
   - Run normally and type/paste both paths

### Step 3: Verify Backups

The script automatically creates timestamped backups before making any changes:
- `Binary_backup_20260106`
- `root_backup_20260106`

Keep these backups safe in case you need to restore original files!

### Step 4: Compile and Test

1. Recompile your C++ project with the obfuscated source files
2. Test your application with the obfuscated Python scripts
3. All functionality should work exactly as before, but with hidden method names

## Example

**Before obfuscation (C++):**
```cpp
static PyMethodDef s_methods[] =
{
    { "GetMainCharacterIndex", playerGetMainCharacterIndex, METH_NOARGS },
    { "SetAttackKeyState", playerSetAttackKeyState, METH_VARARGS },
    { NULL, NULL, NULL }
};
```

**After obfuscation (C++):**
```cpp
static PyMethodDef s_methods[] =
{
    { "xKjPqRtYwZaB", playerGetMainCharacterIndex, METH_NOARGS },
    { "mNpQrStUvWxY", playerSetAttackKeyState, METH_VARARGS },
    { NULL, NULL, NULL }
};
```

**Before obfuscation (Python):**
```python
import player
index = player.GetMainCharacterIndex()
player.SetAttackKeyState(True)
```

**After obfuscation (Python):**
```python
import player
index = player.xKjPqRtYwZaB()
player.mNpQrStUvWxY(True)
```

## Important Notes

- ?? Always backup your files before running the obfuscation
- ?? Test thoroughly after obfuscation to ensure everything works
- ?? Keep a mapping of old?new names if you need to debug issues
- ?? Run obfuscation only once per build cycle
- ? The script handles multiple file encodings (UTF-8, EUC-KR, CP949, etc.)
- ? Import statements remain unchanged for better compatibility

## Troubleshooting

**Q: The script says "Invalid directory path"**
- Make sure you're providing the correct folder path
- Try dragging the folder directly onto the script file

**Q: Some functions are not obfuscated**
- The script only processes files containing `static PyMethodDef s_methods[]`
- Check if your module properly defines this structure

**Q: Application crashes after obfuscation**
- Restore from backup
- Check that both C++ and Python files were processed
- Verify your C++ code compiles without errors

## Support

For issues or questions, please contact the developer.
