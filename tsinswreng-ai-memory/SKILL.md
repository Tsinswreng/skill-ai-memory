---

name: tsinswreng-ai-memory

description: AI的持久化記憶。此skill爲必讀。執行任務前先看記憶、執行任務後再按需更新記憶

---

## 記憶的組織方式

`<項目根目錄>/.Tsinswreng/AiMemory/` 下爲全局AI記憶。 有時是`.Tsinswreng` 也可能會在`_Tsinswreng` 其中 `<項目根目錄>/.Tsinswreng/AiMemory/Main.typ`爲主文檔入口 `Main.typ`爲記憶入口。 由于記憶入口爲必讀項、所以一般我們不在`Main.typ`放置大量內容、而是將他作爲摘要和目錄使用。 具體內容放到其他文件夾下、然後在`Main.typ`中用`#link`函數引用。

例:

文件結構: 在項目根目錄下:

```
.Tsinswreng/
	AiMemory/
		Main.typ
		Journal/
			2026_0620.typ
		Startup/
			LaunchFrontend.typ
			LaunchBackend.typ
```

## `Main.typ`

```typ
#import "@preview/tsinswreng-auto-heading:0.1.0": auto-heading
#let H = auto-heading;

此項目是xxx(概述)

#H[項目啓動][
	前端項目啓動參照 #link("./Startup/LaunchFrontend.typ")[前端啓動文檔]
	後端項目啓動參照 #link("./Startup/LaunchBackend.typ")[後端啓動文檔]
]
```

## `Journal/`

用于放流水賬式的記錄。 主要用于審計 追溯等, **平常不讀。** **平常{沒必要讓其他會話讀到}的**記錄可以放裏面。 每天一個.typ文件, 如`2026_0620.typ`。

若你記的是重要內容 則勿記在`Journal`中!

> 怎樣判斷該不該記在Journal中? 舉一個簡單的例子(不唯一 僅供參考):
> 
> 2026-09-17 第三輪（用戶要求「註釋都改成用 \[Doc()\] 寫」）：全包 74 個檔、772 行 `///` 全換成 `[Doc()]`

你只描述了你的所做所爲, 在後續不同會話中幹活的AI Agent只需依賴當前狀態, 你上面的內容對他完全無參考價值 則這種只需寫進Journal裏。

## 何時讀取記憶

每次執行任務前先看一遍主文檔入口 `Main.typ`。 `Main.typ`中可能會引用其他文檔, 爲節約上下文, 你只**按需讀取**, 避免全盤寫入大量無關內容

### 不需要讀取`Obsolete/`下的文件

## 何時更新記憶

- 每次執行任務後、根據任務結果按需更新記憶。
- 必須使用typst語法、使用.typ文件、不使用markdown
- 標題盡量用 auto-heading 庫
- 保持入口乾淨整潔
- **避免堆積產生大文件** **不論是不是在入口**
  - **當有大文件堆積時應當報告給用戶！**

## 整理記憶

當用戶明確要求你整理記憶時纔看 [TrimMemory.typ](TrimMemory.typ)

## 強調要求

- 必須使用typst語法、使用.typ文件、不使用markdown
- 標題儘量用 auto-heading 庫
- 每次執行任務後、根據任務結果按需更新記憶
- 保持入口乾淨整潔
- 避免堆積產生大文件 不論是不是在入口
- 不需要渲染生成pdf。typst即供直接閱讀
