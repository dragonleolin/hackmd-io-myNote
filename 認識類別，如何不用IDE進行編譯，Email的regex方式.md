---
tags: Java 
---

# 認識類別，如何不用IDE進行編譯，Email的regex方式

## 類別(class): 物件的藍圖, Java程式的基本單元
類別有可能是1.自行開發2.官方3.第三方(3rd-party), 2跟3都會有JavaDoc文件

第三方會有1.JAR(.jar): Java Archive File 2. Java Doc

類別分為寫:1.變數(靜態特性)2.方法(動態特性)3.建構子, 用: 了解功能並組合。

遞迴 : 自己呼叫自己的方法。

## 命名方式

命名規則: 首字必須是_(下底線)、$(任何幣別)、字母(任何字母)。

類別命名:首字必須大寫、要是名詞，第二個單字開頭要大寫。

變數命名:首字必須小寫、要是名詞，第二個單字開頭要大寫。

方法命名:首字必須小寫、要是動詞，第二個單字開頭要大寫。

## 使用文字編譯器寫程式碼
cmd 內可用set path 查詢現在的環境變數內的path路徑情況。 

不用編譯器也可以用命令提示字元去做編譯(javac 檔案名稱.java)跟啟動(java 檔案名稱)。

若讀不到.java檔可能有隱藏的附檔名, 檢視>選項>檢視>把隱藏已知檔案類型的副檔名勾勾拿掉。

## 類別的組成
JAVA由三個部分所組成: `<修飾字> class <*名稱> { }`

類別內可以放: 1.Variable 2. Method 3. Constructor

ReturnType: 執行結果，要回覆:資料型別(DataType)，不回覆:
 ```void <修飾字> <*ReturnType> <*方法名稱> (<參數>) { }```
 
如果直接new出來的物件只能使用一次,但節省記憶體空間, 
`如new B().test(); `

會重複使用到的會給一個命名
`如 B b = new B();  b.test();`

## Q: NetBeans引用其他套件
netbeans引入外部的包: tool -> Libraries -> New Library ->檔名可用包的名字, 點OK->在

classpath、sources、javadoc內加入檔名.jar、檔名-sources.jar、docs資料夾。

在程式內就可以引用`import  org.apache.commons.io.FileUtils;`

刪除資料夾檔案程式換使用Apache內的lib(org.apache.commons.io.FileUtils)，引用時要用

         try{
               FileUtils.forceDelete(file);
                }catch (IOException e) {
                e.printStackTrace();
            }   
         
            
## Q: 用命令提示字元先編譯.java在執行.class
* cmd->javac 檔名.java(副檔名) ->java 檔名
* 引入外部jar檔，cmd->javac -cp  外部的.jar 檔名.java ->java 檔名
* 若程式檔案存檔編碼格式為ANSI者, 輸入-encodingMS950, 若為UTF-8者, 輸入-encoding utf-8,可解決編碼問題進行編譯  cmd -> javac -encoding utf8 -classpath(縮寫可以用cp) 外部檔檔名.jar(絕對路徑) 檔名.java(絕對路徑) ->執行要先cd 回package的上一層, 再輸入java -cp 外部檔檔名.jar(絕對路徑); package名稱.檔名

## Q: 把編譯過的程式打包成jar檔, 跟執行jar檔的方法
1.先建立一個manifest.mf的檔案裏面的名稱都要後面空一格, 若接資料夾要用點去接, 如:
```
1.Main-Class: hellojava(跟package名稱要一致).Hello
2.Class-Path: commons-io-2.6.jar
3.要有空行
4.要有空行
```
建立一個hellojava資料夾把編譯出來的class檔都放入

`cmd-> jar cvfm 壓縮檔名.jar manifest.mf 資料夾名稱/檔名.class commons-io-2.6.jar(相對位置) `

==c: 創建一個新的jar檔, v: 會列出壓縮狀態(也可以不要) f: 指定jar包檔名, m: 指定manifest.mf檔案==

2.進行執行jar檔輸入指令java -jar 檔名.jar

若要用.bat檔可以直接執行, 建立各個檔案, 內容是cmd的執行指令, 副檔名用.bat就可完成。

## Q: Email信箱驗證，使用Matcher跟Pattern
要導入import java.util.regex.Matcher 跟 import java.util.regex.Pattern去做驗證
```
Pattern p = Pattern.compile(regex);
Matcher m = p.matcher(email);
boolean b = m.find();
也可直接寫Pattern.matches(regex, email)
```
regex的驗證如: 

`"^[a-z0-9]{1,20}(\\.)?[a-z0-9]+@[a-zA-Z0-9]{2,20}([\\-])?([\\w]+)[\\.][a-zA-Z]{2,5}(\\.[a-zA-Z]{2,5})?(\\.[a-zA-Z]{2,5})?$"`

`^`開頭 `\w{1, 63}` 為大小寫字母、數字、底線, 至少1-63字元, `+`表示至少要有一個字元以上, `*`表示至少0以上字元, `[\\.|\\-]`必須要有`.`或是`-`, `(\.[a-zA-Z]{2,63})?`為問號代表括弧內的字元可有可無, `$`為結束位置。

> [name=Luke] [time=Sun, Jan 12, 2020] [color=#907bf7]




