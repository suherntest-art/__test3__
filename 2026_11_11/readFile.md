# Python 讀取檔案：一步一步練習

這份教學會帶你從「找到檔案」開始，練習讀取文字檔。範例資料在同一個資料夾的 [`sample.txt`](./sample.txt)。

## 第 1 步：認識範例檔案

先打開 `sample.txt` 看看。它是一般文字檔，每一行都是一筆簡單的學習紀錄。

Python 讀檔時需要知道檔案的位置。若你的程式（例如 `practice2.py`）和 `sample.txt` 放在同一個資料夾，可以使用檔名：

```python
file_path = "sample.txt"
```

若你從專案最上層執行程式，則使用相對於專案最上層的路徑：

```python
file_path = "2026_11_11/sample.txt"
```

> 相對路徑是從「程式目前的工作資料夾」開始計算，不一定是程式檔本身所在的位置。如果 Python 顯示找不到檔案，先確認工作資料夾和路徑。

## 第 2 步：讀取整份檔案

使用 `open()` 開啟檔案，再用 `read()` 讀出全部內容：

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

這段程式各部分的意思：

- `open(...)`：開啟檔案。
- `"sample.txt"`：檔案路徑。
- `"r"`：以讀取模式開啟（read）。
- `encoding="utf-8"`：指定文字編碼，避免中文讀取錯誤。
- `as file`：把開啟的檔案稱為 `file`，方便後續操作。
- `file.read()`：讀出整份檔案，結果存進 `content`。
- `with`：離開區塊時自動關閉檔案，是建議使用的寫法。

## 第 3 步：一次讀一行

如果想逐行處理，可以直接用 `for` 走訪檔案：

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line)
```

你可能會看到每行之間多出空白行，因為文字檔每行本身通常已經有換行符號，而 `print()` 也會再換行。

可以用 `strip()` 移除行首、行尾的空白和換行符號：

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    for line in file:
        print(line.strip())
```

## 第 4 步：把每一行放進清單

`readlines()` 會把所有行讀成一個清單：

```python
with open("sample.txt", "r", encoding="utf-8") as file:
    lines = file.readlines()

print(lines)
print("總共有", len(lines), "行")
```

清單中的每一項是一行文字，通常會包含行尾的換行符號。想逐項顯示乾淨的文字，可以這樣做：

```python
for line in lines:
    print(line.strip())
```

## 第 5 步：完整小練習

讀取範例檔案，並顯示行數與每一筆內容：

```python
file_path = "sample.txt"

with open(file_path, "r", encoding="utf-8") as file:
    lines = file.readlines()

print(f"檔案共有 {len(lines)} 行：")

for number, line in enumerate(lines, start=1):
    print(f"{number}. {line.strip()}")
```

`enumerate(..., start=1)` 會在走訪內容時同時提供編號，這裡讓編號從 1 開始。

## 換成自己的檔案

把 `sample.txt` 改成你自己的文字檔路徑即可。例如同一個資料夾中有 `notes.txt`：

```python
with open("notes.txt", "r", encoding="utf-8") as file:
    content = file.read()

print(content)
```

## 常見問題

### `FileNotFoundError`

Python 找不到指定路徑的檔案。請確認檔名、資料夾名稱和目前工作資料夾。若從專案最上層執行本資料夾中的程式，路徑可能要寫成 `2026_11_11/sample.txt`。

### 中文顯示亂碼

開檔時加上 `encoding="utf-8"`。範例檔案也是以 UTF-8 編碼儲存。

## 自己試試看

1. 用 `read()` 讀出整份 `sample.txt`。
2. 用 `for` 逐行顯示內容，並加上 `strip()`。
3. 用 `readlines()` 讀取後，印出檔案總行數。
4. 把範例檔案加上一行，再重新執行程式，觀察結果。
