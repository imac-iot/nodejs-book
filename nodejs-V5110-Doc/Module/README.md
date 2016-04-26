# Table of Contents
- [Modules](#modules)
  - [Accessing the main module](#accessing-the-main-module)
  - [Addenda:Package Manager Tips](#addendapackage-manager-tips)
  - [All Together](#all-together)
  - [Caching](#caching)
    - [Module Caching Caveats](#module-caching-caveats)
  - [Core Modules](#core-modules)
  - [Cycles](#cycles)
  - [File Modules](#file-modules)
  - [Loading from node_modules Folders](#loading-from-node_modules-folders)
  - [Loading from the global folders](#loading-from-the-global-folders)
  - [The module Object](#the-module-object)
    - [module.children](#modulechildren)
    - [module.exports](#moduleexports)
      - [exports alias](#exports-alias)
    - [module.filename](#modulefilename)
    - [module.id](#moduleid)
    - [module.loaded](#moduleloaded)
    - [module.parent](#moduleparent)
    - [module.require(id)](#modulerequireid)
   
# Modules

Node.js 有一個簡單的模組加載系統 。 在 Node.js 裡, 文件和模組是一對一的對應關係 。以下例子為 foo.js 加載同一目錄下的模組 circle.js 。

foo.js 內容:

```javascript
const circle = require('./circle.js');
console.log( `The area of a circle of radius 4 is ${circle.area(4)}`);
```

circle.js 內容:

```javascript
const PI = Math.PI;

exports.area = (r) => PI * r * r;  //計算圓面積

exports.circumference = (r) => 2 * PI * r;  //計算圓周長
```

透過 exports 物件使 circle.js 內 area() 和 circumference() 的函式可被導入 。


區域變數的模組為私有的，就像模組被包附在函式一樣 。在本例中變數 PI 是專屬於 circle.js 。

如果你想要將導入的模組像函式一樣(如建構函式)或者先導入模組後在賦值，使用 module.exports 而不是 exports.

如下 bar.js 導入一個 square 模組, 導出一個建構函式:

```javascript
const square = require('./square.js');
var mySquare = square(2);
console.log(`The area of my square is ${mySquare.area()}`);
```

定義 square 模組在 square.js :

```javascript
// assigning to exports will not modify module, must use module.exports
module.exports = (width) => {
  return {
    area: () => width * width
  };
}
```

模組系統由 require("module") 模組實現 。
# Accessing the main module

當一個檔案直接從 Node.js 執行,且 require.main 為其模組，這代表著你可以藉此測試其檔案是否已被執行 。 


```javascript
require.main === module
```

對於 foo.js 而言，當執行過 node foo.js時結果為true，但如果運行 require('./foo') 結果為 false 。

因為模組提供了檔案名稱的屬性 (通常為 __filename )， 能藉由檢查 require.main.filename 取得當前應用程序的入口點 。
# Addenda:Package Manager Tips

Node.js 的 require() 函式被設計為足以支援大量合理的目錄結構 Package 管理程序 如 dpkg, rpm, and npm 將能從未經修改的 Node.js 模組中找到可以建立的本地端 packages 。

以下為一個建議的目錄結構:

比方說我們希望目錄結構為 /usr/lib/node/<some-package>/<some-version> 擁有特定版本的 package 內容 。

Packages 可以互相依賴 。 比如說如果要安裝 package foo 可能會需要某個特定版本的 package bar 。bar package 本身具有相關性，在一些情況下這些依賴關係也有可能發生衝突或循環 。

Node.js 查詢任何載入模組的真實路徑(解析符號連結)然後尋找依賴於node_modules文件裡的描述，這種情況可以使用下方的架構解決 。

```javescript
/usr/lib/node/foo/1.2.3/ - foo package 版本為 1.2.3 的內容。
/usr/lib/node/bar/4.3.2/ - foo 依賴於 bar package 的內容
/usr/lib/node/foo/1.2.3/node_modules/bar - 符號連結於 /usr/lib/node/bar/4.3.2/.
/usr/lib/node/bar/4.3.2/node_modules/* - bar package 依賴的符號連結 。
```

因此，即使遇到循環或者衝突，每個模組都能得到一個可以使用的模組版本 。

所以當 foo package 使用 require('bar')方法，他將會取得 /usr/lib/node/foo/1.2.3/node_modules/bar 中的版本 。
而當 bar package 使用 require('quux')方法，他將會取得 /usr/lib/node/bar/4.3.2/node_modules/quux 中的版本 。

此外，為了使模組的查詢過程優話，可以將它們放在 /usr/lib/node_modules/<name>/<version> 目錄底下 。 那麼 Node.js 將不會刻意尋找缺少的依賴關係 。

為了提供給 Node.js 的 REPL 模組，將 /usr/lib/node_modules 檔案加入到 $NODE_PATH 環境變數可能是有用的 。

因為使用 node_modules 檔案尋找模組都是相對的，並且基於檔案的真實路徑呼叫 require()，package 本身是可以在任何地方 。

# All Together

為了取得將被載入的文件確切名稱, 使用 require.resolve() 函式 。

綜合上述所有，這是 require.resolve 偽代碼的高階算法：

```javascript
require(X) from module at path Y
1. If X is a core module,
   a. return the core module
   b. STOP
2. If X begins with './' or '/' or '../'
   a. LOAD_AS_FILE(Y + X)
   b. LOAD_AS_DIRECTORY(Y + X)
3. LOAD_NODE_MODULES(X, dirname(Y))
4. THROW "not found"

LOAD_AS_FILE(X)
1. If X is a file, load X as JavaScript text.  STOP
2. If X.js is a file, load X.js as JavaScript text.  STOP
3. If X.json is a file, parse X.json to a JavaScript Object.  STOP
4. If X.node is a file, load X.node as binary addon.  STOP

LOAD_AS_DIRECTORY(X)
1. If X/package.json is a file,
   a. Parse X/package.json, and look for "main" field.
   b. let M = X + (json main field)
   c. LOAD_AS_FILE(M)
2. If X/index.js is a file, load X/index.js as JavaScript text.  STOP
3. If X/index.json is a file, parse X/index.json to a JavaScript object. STOP
4. If X/index.node is a file, load X/index.node as binary addon.  STOP

LOAD_NODE_MODULES(X, START)
1. let DIRS=NODE_MODULES_PATHS(START)
2. for each DIR in DIRS:
   a. LOAD_AS_FILE(DIR/X)
   b. LOAD_AS_DIRECTORY(DIR/X)

NODE_MODULES_PATHS(START)
1. let PARTS = path split(START)
2. let I = count of PARTS - 1
3. let DIRS = []
4. while I >= 0,
   a. if PARTS[I] = "node_modules" CONTINUE
   c. DIR = path join(PARTS[0 .. I] + "node_modules")
   b. DIRS = DIRS + DIR
   c. let I = I - 1
5. return DIRS
```

# Caching

當模組第一次被載入時將被緩存，這代表著如果解析的為同一個文件每次得到的回傳結果都會相同 。

多次的呼叫 require('foo') 可能不會多次執行模組程式，這是一個重要的特性，有了它"部份完成"對象可以被返回可以說是加載時將會導致循環 。

如果你想要有一個模組多次執行，那麼導出函式並且呼叫它 。

#### Module Caching Caveats

模組都是基於它們的文件名稱被快取，模組會生成很多不同的名稱是根據本地端模組(載入於 node_modules 資料夾)的名稱，使用 require('foo') 這個方法每次的回傳結果並不一定都會相同，因為它會讀取到不同的檔案 。

此外，作業系統的檔案不區分大小寫，即使是檔案名稱大小寫不同也能指向同一個檔案，但是快取仍然會視他們為不同的模組，並多次重新加載該模組。例如， require('./foo') 和 require('./FOO') 雖然會指向同一個模組但是仍然會判定為不同物件　。

# Core Modules

Node.js 有許多編譯成二進制的模組，這些模組在其他地方有更詳細的資料　。

核心模組被定義於 Node.js 來源中，並且位於 lib/ 資料夾　。

如果核心模組的識別碼傳遞給 rqeuire() 將優先載入，例如， 即使已經擁有該名稱的文件 require('http') 還是會返回內建的 HTTP 模組　。

# Cycles
# File Modules
# Loading from node_modules Folders
# Loading from the global folders
# The module Object
### module.children
### module.exports
### exports alias
### module.filename
### module.id
### module.loaded
### module.parent
### module.require(id)