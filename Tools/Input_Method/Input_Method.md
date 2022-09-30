#### fcitx 安装

```
sudo pacman -S --noconfirm fcitx-im kcm-fcitx fcitx-configtool
```

配置 fcitx

```
sudo echo -e "export GTK_IM_MODULE=fcitx\nexport QT_IM_MODULE=fcitx\nexport XMODIFIERS=@im=fcitx">>~/.xprofile
```

##### googlepinyin
`sudo pacman -S fcitx-googlepinyin`

<p class='ind'>
重启后在状态栏找到键盘右键 --> config --> input method --> 添加后确认应用生效，默认的切换输入法快捷键为ctrl + 空格</p>

<p class='ind'>可自行安装搜狗输入法，manjaro 软件管理软件中也可以直接安装谷歌输入法。（目前用 googlepinyin，之前用搜狗有乱码，不知道为什么）</p>


##### rime
rime 在 ibus 中有无法正常将待选字由纵向选择改为横向，改底层配置解决后重新部署会恢复原来的

`yay -S fictx-rime` 安装即可，在 fcitx 中选择配置即可
默认的为繁体字，需要简体的`F4`后选择合适的即可优先简体

默认情况下，Rime 只会列出 5 个候选项，可以通过修改 "menu/page_size" 的值来手动更改列出候选项的个数
```
cd ~/.config/fcitx/rime && rm default.yaml && touch default.custom.yaml && vim default.custom.yaml
```
后写入
```
patch:
     "menu/page_size": 9
```

默认情况下，如果输入\，默认选择三个选项，不利于效率,希望的时输入\，可以直接上屏中文的顿号、。
```
cd ~/.config/fcitx/rime && touch luna_pinyin.custom.yaml && vim luna_pinyin.custom.yaml
```
后写入
```
patch:
  punctuator:
    full_shape:
      # ' ' : { commit: '　' }
      # ',' : { commit: ， }
      # '.' : { commit: 。 }
      # '<' : [ '《', '〈', '«', '‹' ]
      # '>' : [ '》', '〉', '»', '›' ]
      # '/' : [ '／', '÷' ]
      # '?' : { commit: ？ }
      # ';' : { commit: ； }
      # ':' : { commit: ： }
      # '''' : { pair: [ '‘', '’' ] }
      # '"' : { pair: [ '“', '”' ] }
      # '\' : [ '、', '＼' ]
      # '|' : [ '·', '｜', '§', '¦' ]
      # '`' : { commit: ｀ }
      # '~' : '～'
      # '!' : { commit: ！ }
      # '@' : { commit: ＠ }
      # '#' : { commit: ＃ }
      # '%' : { commit: ％ }
      # '$' : [ ￥, '$', '€', '£', '¥', '¢', '¤', ₩ ]
      # '^' : { commit: …… }
      # '&' : '＆'
      # '*' : [ ＊, ·, ・, ×, ※, ❂ ]
      # '(' : '（'
      # ')' : '）'
      # '-' : '－'
      # '_' : '——'
      # '+' : '＋'
      # '=' : [ '＝']
      # '[' : [ '「', '【', '〔', '［' ]
      # ']' : [ '」', '】', '〕', '］' ]
      # '{' : [ '『', '〖', '｛' ]
      # '}' : [ '』', '〗', '｝' ]
    half_shape:
      ',' : { commit: '，' }
      '.' : { commit: '。' }
      '<' : [ 《, 〈, «, ‹, ˂, ˱ ]
      '>' : [ 》, 〉, », ›, ˃, ˲ ]
      '/' : [ '//', '/**/', '/', ÷, ／, '\', ＼ ]
      '?' : { commit: ？ }
      ';' : { commit: ； }
      ':' : { commit: ： }
      '''' : { pair: [ '‘', '’' ] }
      '"' : { pair: [ '“', '”' ] }
      '\' : { commit: '、' }
      '|' : [ '|', '｜', '§', '¦', '‖' ]
      '`' : { commit:  '``' } # [ '``', '`', ·, ・, ‵, ‶, ‷, ′, ″, ‴, ⁗ ]
      '~' : [ '~', ·, ～, ˜, ˷, ⸯ, ≈, ≋, ≃, ≅, ≇, ∽, ⋍, ≌, ﹏, ﹋, ﹌ ]
      '!' : { commit: ！ }
      '@' : [ '@', ©, ®, ℗ ] # "@"
      '#' : '#' # [ '#', № ]
      '%' : [ '%', ％, '°', '℃', ‰, ‱, ℉, '℅', '℆', '℀', '℁', '⅍' ]
      '$' : [ ￥, '$', '€', '£', '¥', '¢', '¤', ₩ ]
      '^' : { commit: …… }
      '&' : '&'
      '*' : '*' # [ '*', ＊, ·, ・, ×, ※, ❂, ⁂, ☮, ☯, ☣ ]
      '(' : '（' # "（"
      ')' : '）' # "）"
      '-' : '-' # "－"
      '_' :  [ '——', '_' ]
      '+' : '+' # "＋"
      '=' : '='
      '[' : '['
      ']' : ']'
      '{' : '{' # "｛"
      '}' : '}' # "｝"
    symbols:
  #符號、電腦
      '/fh': [ ©, ®, ℗, ℠, ™, ℡, ℻, ☇, ☈, ☉, ☊, ☋, ☌, ☍, ☎, ☏, ☐, ☑, ☒, ☓, ☕, ☖, ☗, ⛉, ⛊, ☘, ☙, ☚, ☛, ☜, ☝, ☞, ☟, ☠, ☡, ☢, ☣, ☤, ☥, ☦, ☧, ☨, ☩, ☪, ☫, ☬, ☭, ☮, ☯, ☸, ♨, ♰, ♱, ♲, ♳, ♴, ♵, ♶, ♷, ♸, ♹, ♺, ♻, ♼, ♽, ♾, ♿, ⚆, ⚇, ⚈, ⚉, ⚐, ⚑, ⚒, ⚓, ⚔, ⚕, ⚖, ⚗, ⚘, ⚙, ⚚, ⚛, ⚜, ⚝, ⚞, ⚟, ⚠, ⚡, ⚰, ⚱, ⚲, ⚳, ⚴, ⚵, ⚶, ⚷, ⚸, ⚹, ⚺, ⚻, ⚼, ⚽, ⚾, ⚿, ⛀, ⛁, ⛂, ⛃, ⛋, ⛌, ⛍, ⛎, ⛏, ⛐, ⛑, ⛒, ⛓, ⛔, ⛕, ⛖, ⛗, ⛘, ⛙, ⛚, ⛛, ⛜, ⛝, ⛞, ⛟, ⛠, ⛡, ⛢, ⛣, ⛨, ⛩, ⛪, ⛫, ⛬, ⛭, ⛮, ⛯, ⛰, ⛱, ⛲, ⛳, ⛴, ⛵, ⛶, ⛷, ⛸, ⛹, ⛺, ⛻, ⛼, ⛽, ⛾, ⛿ ]
      '/dn': [ , ❖, ◁, ⌘, ⌥, ⎇, ⇧, ⇪, ↩, ⌅, ⌤, ⌫, ⌦, ⌧, ⌨, ⌀, ⌖, ⌗, ⏏, ↖, ↘, ⇞, ⇟, ⌚, ⏰, ⏱, ⏲, ⏳, ⌛, ⌜, ⌝⌞⌟, ⍑, ⏩, ⏪, ⏫, ⏬, ⏭, ⏮, ⏯ ]
  #象棋、麻將、色子、撲克
      '/xq': [ ♔, ♕, ♖, ♗, ♘, ♙, ♚, ♛, ♜, ♝, ♞, ♟ ]
      '/mj': [ 🀀, 🀁, 🀂, 🀃, 🀄, 🀅, 🀆, 🀇, 🀈, 🀉, 🀊, 🀋, 🀌, 🀍, 🀎, 🀏, 🀐, 🀑, 🀒, 🀓, 🀔, 🀕, 🀖, 🀗, 🀘, 🀙, 🀚, 🀛, 🀜, 🀝, 🀞, 🀟, 🀠, 🀡, 🀢, 🀣, 🀤, 🀥, 🀦, 🀧, 🀨, 🀩, 🀪, 🀫 ]
      '/sz': [ ⚀, ⚁, ⚂, ⚃, ⚄, ⚅ ]
      '/pk': [ ♠, ♡, ♢, ♣, ♤, ♥, ♦, ♧ ]
  #表情
      '/bq': [ ☻, ☺, ☹ ]
  #天氣
      '/tq': [ ☀, ☁, ⛅, ⛈, ⛆, ☂, ☔, ☃, ⛄, ⛇ ]
  #音樂
      '/yy': [ 𝄞, ♩, ♪, ♫, ♬, ♭, ♮, ♯ ]
  #兩性
      '/lx': [ ♂, ♀, ⚢, ⚣, ⚤, ⚥, ⚦, ⚧, ⚨, ⚩, ⚪, ⚫, ⚬, ⚭, ⚮, ⚯ ]
  #八卦、八卦名、六十四卦、六十四卦名、太玄經
      '/bg': [ ☰, ☱, ☲, ☳, ☴, ☵, ☶, ☷ ]
      '/bgm': [ 乾, 兌, 離, 震, 巽, 坎, 艮, 坤 ]
      '/lssg': [ ䷀, ䷁, ䷂, ䷃, ䷄, ䷅, ䷆, ䷇, ䷈, ䷉, ䷊, ䷋, ䷌, ䷍, ䷎, ䷏, ䷐, ䷑, ䷒, ䷓, ䷔, ䷕, ䷖, ䷗, ䷘, ䷙, ䷚, ䷛, ䷜, ䷝, ䷞, ䷟, ䷠, ䷡, ䷢, ䷣, ䷤, ䷥, ䷦, ䷧, ䷨, ䷩, ䷪, ䷫, ䷬, ䷭, ䷮, ䷯, ䷰, ䷱, ䷲, ䷳, ䷴, ䷵, ䷶, ䷷, ䷸, ䷹, ䷺, ䷻, ䷼, ䷽, ䷾, ䷿ ]
      '/lssgm': [ 乾, 坤, 屯, 蒙, 需, 訟, 師, 比, 小畜, 履, 泰, 否, 同人, 大有, 謙, 豫, 隨, 蠱, 臨, 觀, 噬嗑, 賁, 剝, 復, 无妄, 大畜, 頤, 大過, 坎, 離, 咸, 恆, 遯, 大壯, 晉, 明夷, 家人, 睽, 蹇, 解, 損, 益, 夬, 姤, 萃, 升, 困, 井, 革, 鼎, 震, 艮, 漸, 歸妹, 豐, 旅, 巽, 兌, 渙, 節, 中孚, 小過, 既濟, 未濟 ]
      '/txj': [ ⚊, ⚋, ⚌, ⚍, ⚎, ⚏, 𝌀, 𝌁, 𝌂, 𝌃, 𝌄, 𝌅, 𝌆, 𝌇, 𝌈, 𝌉, 𝌊, 𝌋, 𝌌, 𝌍, 𝌎, 𝌏, 𝌐, 𝌑, 𝌒, 𝌓, 𝌔, 𝌕, 𝌖, 𝌗, 𝌘, 𝌙, 𝌚, 𝌛, 𝌜, 𝌝, 𝌞, 𝌟, 𝌠, 𝌡, 𝌢, 𝌣, 𝌤, 𝌥, 𝌦, 𝌧, 𝌨, 𝌩, 𝌪, 𝌫, 𝌬, 𝌭, 𝌮, 𝌯, 𝌰, 𝌱, 𝌲, 𝌳, 𝌴, 𝌵, 𝌶, 𝌷, 𝌸, 𝌹, 𝌺, 𝌻, 𝌼, 𝌽, 𝌾, 𝌿, 𝍀, 𝍁, 𝍂, 𝍃, 𝍄, 𝍅, 𝍆, 𝍇, 𝍈, 𝍉, 𝍊, 𝍋, 𝍌, 𝍍, 𝍎, 𝍏, 𝍐, 𝍑, 𝍒, 𝍓, 𝍔, 𝍕, 𝍖 ]
  #天體、星座、星座名、十二宮
      '/tt': [ ☄, ☼, ☽, ☾, ☿, ♀, ♁, ♂, ♃, ♄, ♅, ♆, ♇ ]
      '/xz': [ ♈, ♉, ♊, ♋, ♌, ♍, ♎, ♏, ♐, ♑, ♒, ♓ ]
      '/xzm': [ 白羊座, 金牛座, 雙子座, 巨蟹座, 獅子座, 室女座, 天秤座, 天蠍座, 人馬座, 摩羯座, 寶瓶座, 雙魚座 ]
      '/seg': [ 白羊宮, 金牛宮, 雙子宮, 巨蟹宮, 獅子宮, 室女宮, 天秤宮, 天蠍宮, 人馬宮, 摩羯宮, 寶瓶宮, 雙魚宮 ]
  #星號
      '/xh': [ ★, ☆, ⛤, ⛥, ⛦, ⛧, ✡, ❋, ❊, ❉, ❈, ❇, ❆, ❅, ❄, ❃, ❂, ❁, ❀, ✿, ✾, ✽, ✼, ✻, ✺, ✹, ✸, ✷, ✶, ✵, ✴, ✳, ✲, ✱, ✰, ✯, ✮, ✭, ✬, ✫, ✪, ✩, ✧, ✦, ✥, ✤, ✣, ✢ ]
  #方塊
      '/fk': [ ▀, ▁, ▂, ▃, ▄, ▅, ▆, ▇, █, ▉, ▊, ▋, ▌, ▍, ▎, ▏, ▐, ░, ▒, ▓, ▔, ▕, ▖, ▗, ▘, ▙, ▚, ▛, ▜, ▝, ▞, ▟ ]
  #幾何
      '/jh': [ ■, □, ▢, ▣, ▤, ▥, ▦, ▧, ▨, ▩, ▪, ▫, ▬, ▭, ▮, ▯, ▰, ▱, ▲, △, ▴, ▵, ▶, ▷, ▸, ▹, ►, ▻, ▼, ▽, ▾, ▿, ◀, ◁, ◂, ◃, ◄, ◅, ◆, ◇, ◈, ◉, ◊, ○, ◌, ◍, ◎, ●, ◐, ◑, ◒, ◓, ◔, ◕, ◖, ◗, ◘, ◙, ◚, ◛, ◜, ◝, ◞, ◟, ◠, ◡, ◢, ◣, ◤, ◥, ◦, ◧, ◨, ◩, ◪, ◫, ◬, ◭, ◮, ◯, ◰, ◱, ◲, ◳, ◴, ◵, ◶, ◷, ◸, ◹, ◺, ◻, ◼, ◽, ◾, ◿ ]
  #箭頭
      '/jt': [  →, ←, ↑, ↓, ↚, ↛, ↔, ↮, ↕, ↖, ↗, ↘, ↙, ↜, ↝, ↞, ↟, ↠, ↡, ↢, ↣, ↤, ↥, ↦, ↧, ↨, ↩, ↪, ↫, ↬, ↭, ↯, ↰, ↱, ↲, ↳, ↴, ↵, ↶, ↷, ↸, ↹, ↺, ↻, ↼, ↽, ↾, ↿, ⇀, ⇁, ⇂, ⇃, ⇄, ⇅, ⇆, ⇇, ⇈, ⇉, ⇊, ⇋, ⇌, ⇐, ⇍, ⇑, ⇒, ⇏, ⇓, ⇔, ⇎, ⇕, ⇖, ⇗, ⇘, ⇙, ⇚, ⇛, ⇜, ⇝, ⇞, ⇟, ⇠, ⇡, ⇢, ⇣, ⇤, ⇥, ⇦, ⇧, ⇨, ⇩, ⇪, ⇫, ⇬, ⇭, ⇮, ⇯, ⇰, ⇱, ⇲, ⇳, ⇴, ⇵, ⇶, ⇷, ⇸, ⇹, ⇺, ⇻, ⇼, ⇽, ➔, ➘, ➙, ➚, ➛, ➜, ➝, ➞, ➟, ➠, ➡, ➢, ➣, ➤, ➥, ➦, ➧, ➨, ➩, ➪, ➫, ➬, ➭, ➮, ➱, ➲, ➳, ➴, ➵, ➶, ➷, ➸, ➹, ➺, ➻, ➼, ➽, ➾ ]
  #數學
      '/sx': [ ︴, －, ∈, ∏, ∑, ＋, ±, ÷, ×, ＜, ≮, ＝, ≠, ＞, ≯, ∕, √, ∝, ∞, ∟, ∠, ∥, ∧, ∨, ∩, ∪, ∫, ∮, ∴, ∵, ∷, ∽, ≈, ≌, ≒, ≡, ≤, ≥, ≦, ≧, ⊕, ⊙, ⊥, ⊿, ㏑, ㏒ ]
  #數字+圈/弧/點
      '/szq': [ ⓪, ①, ②, ③, ④, ⑤, ⑥, ⑦, ⑧, ⑨, ⑩, ⑪, ⑫, ⑬, ⑭, ⑮, ⑯, ⑰, ⑱, ⑲, ⑳, ㉑, ㉒, ㉓, ㉔, ㉕, ㉖, ㉗, ㉘, ㉙, ㉚, ㉛, ㉜, ㉝, ㉞, ㉟, ㊱, ㊲, ㊳, ㊴, ㊵, ㊶, ㊷, ㊸, ㊹, ㊺, ㊻, ㊼, ㊽, ㊾, ㊿, ⓿, ❶, ❷, ❸, ❹, ❺, ❻, ❼, ❽, ❾, ❿, ⓫, ⓬, ⓭, ⓮, ⓯, ⓰, ⓱, ⓲, ⓳, ⓴ ]
      '/szh': [ ⑴, ⑵, ⑶, ⑷, ⑸, ⑹, ⑺, ⑻, ⑼, ⑽, ⑾, ⑿, ⒀, ⒁, ⒂, ⒃, ⒄, ⒅, ⒆, ⒇ ]
      '/szd': [ ⒈, ⒉, ⒊, ⒋, ⒌, ⒍, ⒎, ⒏, ⒐, ⒑, ⒒, ⒓, ⒔, ⒕, ⒖, ⒗, ⒘, ⒙, ⒚, ⒛ ]
  #字母+圈/弧
      '/zmq': [ ⓐ, Ⓐ, ⓑ, Ⓑ, ⓒ, Ⓒ, ⓓ, Ⓓ, ⓔ, Ⓔ, ⓕ, Ⓕ, ⓖ, Ⓖ, ⓗ, Ⓗ, ⓘ, Ⓘ, ⓙ, Ⓙ, ⓚ, Ⓚ, ⓛ, Ⓛ, ⓜ, Ⓜ, ⓝ, Ⓝ, ⓞ, Ⓞ, ⓟ, Ⓟ, ⓠ, Ⓠ, ⓡ, Ⓡ, ⓢ, Ⓢ, ⓣ, Ⓣ, ⓤ, Ⓤ, ⓥ, Ⓥ, ⓦ, Ⓦ, ⓧ, Ⓧ, ⓨ, Ⓨ, ⓩ, Ⓩ ]
      '/zmh': [ ⒜, ⒝, ⒞, ⒟, ⒠, ⒡, ⒢, ⒣, ⒤, ⒥, ⒦, ⒧, ⒨, ⒩, ⒪, ⒫, ⒬, ⒭, ⒮, ⒯, ⒰, ⒱, ⒲, ⒳, ⒴, ⒵ ]
  #數字、分數
      '/0': [ 〇, 零, ₀, ⁰, ⓪, ⓿ , ０]
      '/1': [ 一, 壹, ₁, ¹, Ⅰ, ⅰ, ①, ➀, ❶, ➊, ⓵, ⑴, ⒈, １, ㊀, ㈠, 弌, 壱, 幺, ㆒ ]
      '/2': [ 二, 貳, ₂, ², Ⅱ, ⅱ, ②, ➁, ❷, ➋, ⓶, ⑵, ⒉, ２, ㊁, ㈡, 弍, 弐, 貮, 㒃, 㒳, 兩, 倆, ㆓]
      '/3': [ 三, 叄, ₃, ³, Ⅲ, ⅲ, ③, ➂, ❸, ➌, ⓷, ⑶, ⒊, ３, ㊂, ㈢, 參, 参, 叁, 弎, 仨, ㆔]
      '/4': [ 四, 肆, ₄, ⁴, Ⅳ, ⅳ, ④, ➃, ❹, ➍, ⓸, ⑷, ⒋, ４, ㊃, ㈣, 亖]
      '/5': [ 五, 伍, ₅, ⁵, Ⅴ, ⅴ, ⑤, ➄, ❺, ➎, ⓹, ⑸, ⒌, ５, ㊄, ㈤, 㐅, 㠪, 𠄡 ]
      '/6': [ 六, 陸, ₆, ⁶, Ⅵ, ⅵ, ⑥, ➅, ❻, ➏, ⓺, ⑹, ⒍, ６, ㊅, ㈥, ↅ]
      '/7': [ 七, 柒, ₇, ⁷, Ⅶ, ⅶ, ⑦, ➆, ❼, ➐, ⓻, ⑺, ⒎, ７, ㊆, ㈦, 漆]
      '/8': [ 八, 捌, ₈, ⁸, Ⅷ, ⅷ, ⑧, ➇, ❽, ➑, ⓼, ⑻, ⒏, ８, ㊇, ㈧ ]
      '/9': [ 九, 玖, ₉, ⁹, Ⅸ, ⅸ, ⑨, ➈, ❾, ➒, ⓽, ⑼, ⒐, ９, ㊈, ㈨ ]
      '/10': [ 十, 拾, ₁₀, ¹⁰, Ⅹ, ⅹ, ⑩, ➉, ❿, ➓, ⓾, ⑽, ⒑, １０, ㊉, ㈩, 什 ]
      '/fs': [ ⅟, ½, ↉, ⅓, ⅔, ¼, ⅕, ⅖, ⅗, ⅘, ⅙, ⅚, ⅐, ⅛, ⅜, ⅝, ⅞, ⅑, ⅒ ]
  #蘇州碼
      '/szm': [ 〡, 〢, 〣, 〤, 〥, 〦, 〧, 〨, 〩, 〸, 〹, 〺 ]
  #羅馬數字
      '/lm': [ ⅰ, ⅱ, ⅲ, ⅳ, ⅴ, ⅵ, ⅶ, ⅷ, ⅸ, ⅹ, ⅺ, ⅻ, ⅼ, ⅽ, ⅾ, ⅿ ]
      '/lmd': [ Ⅰ, Ⅱ, Ⅲ, Ⅳ, Ⅴ, Ⅵ, Ⅶ, Ⅷ, Ⅸ, Ⅹ, Ⅺ, Ⅻ, Ⅼ, Ⅽ, Ⅾ, Ⅿ ]
  #拉丁
      '/a': [ ₐ, ᵃ, ª, ᵄ, á, à, ȧ, â, ä, ǎ, ă, ā, ã, å, ą, ⱥ, ấ, ầ, ắ, ằ, ǡ, ǻ, ǟ, ẫ, ẵ, ả, ȁ, ȃ, ẩ, ẳ, ᶏ, ạ, ḁ, ậ, ẚ, ặ, ɐ, ɑ, ɒ, ᶛ, ᵅ ]
      '/b': [ ᵇ, ḃ, ᵬ, ƀ, ɓ, ᶀ, ḅ, ḇ, ƃ, ᵦ, ᵝ, β ]
      '/c': [ ᶜ, ć, ċ, ĉ, č, ç, ȼ, ḉ, ƈ, ᵓ, ɔ, ᶗ, ɕ, ᶝ ]
      '/d': [ ᵈ, ḋ, ď, ď, ᵭ, ḑ, đ, ƌ, ɗ, ᶁ, ḍ, ᶑ, ḓ, ḏ, ð, ʤ, ƍ, ᶞ, ǳ, ǆ, ɖ, ʣ, ʥ, ȡ, ẟ ]
      '/e': [ ₑ, ᵉ, é, è, ė, ê, ë, ě, ĕ, ē, ẽ, ę, ȩ, ɇ, ế, ề, ḗ, ḕ, ễ, ḝ, ẻ, ȅ, ȇ, ể, ẹ, ᶒ, ḙ, ḛ, ᶟ, ệ, ɛ, ǝ, ə, ₔ, ᵊ, ɚ, ɘ, ɜ, ɝ, ɞ, ʚ, ȝ, ᶾ, ᶕ, ᶚ, ᴈ, ᶓ, ᶔ, ᵋ, ᵌ, ⱸ ]
      '/f': [ ᶠ, ḟ, ᵮ, ƒ, ᶂ, ﬀ, ﬃ, ﬄ, ﬁ, fʲ, ﬂ, ʩ, ɟ, ɸ, ᶲ, ᵩ, ᵠ ]
      '/g': [ ᵍ, ᵷ, ǵ, ġ, ĝ, ǧ, ğ, ḡ, ģ, ǥ, ɠ, ᶃ, ɣ, ᶢ, ɡ, ˠ, ᵧ, ᵞ ]
      '/h': [  ͪ, ḣ, ĥ, ḧ, ȟ, ḩ, ħ, ɦ, ḥ, ḫ, ẖ, ⱨ, ɥ, ᶣ, ʱ, ƕ, ʮ, ʯ, ꜧ, ɧ ]
      '/i': [ ᵢ, ı, ᴉ, í, ì, î, ï, ǐ, ĭ, ī, ĩ, į, ɨ, ḯ, ᶤ, ỉ, ȉ, ȋ, ị, ᶖ, ḭ, ᵎ, ɩ, ᶥ, ᵼ, ĳ ]
      '/j': [ ⱼ, ʲ, ȷ, ĵ, ǰ, ɉ, ɟ, ᶡ, ʄ, ᶨ, ʝ ]
      '/k': [ ᵏ, ḱ, ǩ, ķ, ƙ, ᶄ, ḳ, ḵ, ⱪ, ʞ ]
      '/l': [ ˡ, ĺ, ŀ, ľ, ɫ, ⱡ, ļ, ƚ, ł, ƛ, ᶅ, ᶪ, ᶩ, ḷ, ɭ, ḽ, ḻ, ḹ, ɬ, ɮ, ǉ, ỻ, ʪ, ʫ, ȴ ]
      '/m': [ ᵐ, ḿ, ṁ, ᵯ, ᶬ, ɱ, ᶆ, ṃ, ɯ, ᵚ, ɰ, ᶭ, ᴟ ]
      '/n': [ ⁿ, ń, ǹ, ṅ, ň, ñ, ᵰ, ņ, ᶮ, ɲ, ŉ, ƞ, ᶇ, ṇ, ɳ, ᶯ, ṋ, ṉ, ȵ ]
      '/o': [ ₒ, ᵒ, º, ó, ò, ȯ, ô, ö, ǒ, ŏ, ō, õ, ǫ, ő, ố, ồ, ɵ, ø, ṓ, ṑ, ȱ, ṍ, ȫ, ổ, ọ, ớ, ờ, ỡ, ộ, ɷ, ở, ợ, ᵔ, ᵕ, œ, ȣ, ᴔ, ⱺ ]
      '/p': [ ᵖ, ṕ, ṗ, ᵱ, ᵽ, ƥ, ᶈ ]
      '/q': [ ʠ, ɋ, ȹ ]
      '/r': [ ᵣ, ŕ, ṙ, ř, ᵲ, ŗ, ɍ, ᵳ, ɽ, ȑ, ȓ, ᶉ, ṛ, ṟ, ṝ, ɹ, ɺ, ɻ, ɼ, ɾ, ɿ, ʳ, ʴ, ʵ, ᵨ ]
      '/s': [ ˢ, ś, ṡ, ŝ, š, ᵴ, ş, ṥ, ṧ, ᶳ, ʂ, ᶊ, ṣ, ș, ȿ, ṩ, ʃ, ᶴ, ƨ, ʆ, ʅ, ƪ, ß, ſ, ẛ ]
      '/t': [ ᵗ, ṫ, ť, ᵵ, ţ, ƭ, ᶵ, ƫ, ṭ, ʈ, ț, ṱ, ṯ, ⱦ, ʇ, ʧ, ʨ, ᶿ, ȶ, ŧ ]
      '/u': [ ᵤ, ᵘ, ú, ù, û, ü, ǔ, ŭ, ū, ũ, ů, ų, ű, ᶶ, ʉ, ǘ, ǜ, ǚ, ṹ, ǖ, ṻ, ủ, ȕ, ȗ, ư, ᶙ, ụ, ṳ, ứ, ừ, ṷ, ṵ, ữ, ʉ̞, ʊ, ᶷ, ᵙ, ử, ᵿ, ự, ᴝ, ᴞ, ᵫ ]
      '/v': [ ᵥ, ᵛ, ṽ, ᶹ, ᶌ, ṿ, ⱴ, ʋ, ᶺ, ʌ ]
      '/w': [ ʷ, ẃ, ẁ, ẇ, ŵ, ẅ, ẘ, ẉ, ƿ, ʍ, ⱳ ]
      '/x': [ ₓ, ᶍ, ˣ, χ, ᵪ, ᵡ ]
      '/y': [ ʸ, ý, ỳ, ẏ, ŷ, ÿ, ȳ, ỹ, ẙ, ɏ, ỷ, ƴ, ỵ, ʎ, ỿ ]
      '/z': [ ᶻ, ź, ż, ẑ, ž, ᵶ, ƶ, ȥ, ᶎ, ᶼ, ẓ, ʐ, ɀ, ẕ, ⱬ, ʑ, ᶽ, ʒ ]
  #上標、下標
      '/sb': [ ⁰, ¹, ², ³, ⁴, ⁵, ⁶, ⁷, ⁸, ⁹, ˜, ⁺, ⁻, ⁼, ⁽, ⁾, ᴬ, ᵃ, ᵄ, ᵅ, ᶛ, ᴭ, ᵆ, ᴮ, ᴯ, ᵇ, ᵝ, ᶜ, ᵓ, ᶝ, ᴰ, ᵈ, ᶞ, ᵟ, ᴱ, ᵉ, ᴲ, ᵊ, ᵋ, ᶟ, ᵌ, ᶠ, ᶡ, ᶲ, ᵠ, ᴳ, ᵍ, ᶢ, ˠ, ᵞ, ᴴ, ʰ, ᶣ, ʱ, ᴵ, ⁱ, ᶤ, ᵎ, ᶥ, ᴶ, ʲ, ᶨ, ᴷ, ᵏ, ᴸ, ᶫ, ˡ, ᶩ, ᶪ, ᴹ, ᵐ, ᶬ, ᵚ, ᶭ, ᴺ, ᴻ, ⁿ, ᵑ, ᶮ, ᶯ, ᴼ, ᵒ, ᶱ, ᴽ, ᴾ, ᵖ, ᴿ, ʳ, ʶ, ʴ, ʵ, ˢ, ᶴ, ᶳ, ᵀ, ᵗ, ᶵ, ᶿ, ᵁ, ᵘ, ᶶ, ᶷ, ᵙ, ⱽ, ᵛ, ᶺ, ᶹ, ᵂ, ʷ, ˣ, ᵡ, ʸ, ᶻ, ᶾ, ᶽ, ᶼ ]
      '/xb': [ ₀, ₁, ₂, ₃, ₄, ₅, ₆, ₇, ₈, ₉, ₊, ₋, ₌, ₍, ₎, ‸, ᴀ, ₐ, ᴁ, ʙ, ᴃ, ᵦ, ᴄ, ᴐ, ᴒ, ᴅ, ᴆ, ᴇ, ₑ, ₔ, ᵩ, ɢ, ʛ, ᴦ, ᵧ, ʜ, ₕ, ɪ, ᵻ, ᵢ, ᴊ, ⱼ, ᴋ, ₖ, ʟ, ₗ, ᴌ, ᴧ, ᴍ, ₘ, ꟺ, ɴ, ᴎ, ₙ, ᴏ, ₒ, ɶ, ʘ, ᴓ, ᴑ, ᴘ, ₚ, ᴨ, ᴪ, ʀ, ᵣ, ᴙ, ʁ, ᴚ, ᵨ, ₛ, ᴛ, ₜ, ᴜ, ᵤ, ᵾ, ᴠ, ᵥ, ᴡ, ₓ, ᵪ, ʏ, ᴢ, ᴣ ]
  #希臘
      '/xl': [ α, β, γ, δ, ε, ζ, η, θ, ι, κ, λ, μ, ν, ξ, ο, π, ρ, σ, ς, τ, υ, φ, χ, ψ, ω ]
      '/xld': [ Α, Β, Γ, Δ, Ε, Ζ, Η, Θ, Ι, Κ, Λ, Μ, Ν, Ξ, Ο, Π, Ρ, Σ, Τ, Υ, Φ, Χ, Ψ, Ω ]
  #俄語
      '/ey': [ а, б, в, г, д, е, ё, ж, з, и, й, к, л, м, н, о, п, р, с, т, у, ф, х, ц, ч, ш, щ, ъ, ы, ь, э, ю, я ]
      '/eyd': [ А, Б, В, Г, Д, Е, Ё, Ж, З, И, Й, К, Л, М, Н, О, П, Р, С, Т, У, Ф, Х, Ц, Ч, Ш, Щ, Ъ, Ы, Ь, Э, Ю, Я ]
  #月份、日期、曜日等
      '/yf': [ ㋀, ㋁, ㋂, ㋃, ㋄, ㋅, ㋆, ㋇, ㋈, ㋉, ㋊, ㋋ ]
      '/rq': [ ㏠, ㏡, ㏢, ㏣, ㏤, ㏥, ㏦, ㏧, ㏨, ㏩, ㏪, ㏫, ㏬, ㏭, ㏮, ㏯, ㏰, ㏱, ㏲, ㏳, ㏴, ㏵, ㏶, ㏷, ㏸, ㏹, ㏺, ㏻, ㏼, ㏽, ㏾ ]
      '/yr': [ 月, 火, 水, 木, 金, 土, 日, ㊊, ㊋, ㊌, ㊍, ㊎, ㊏, ㊐, ㊗, ㊡, ㈪, ㈫, ㈬, ㈭, ㈮, ㈯, ㈰, ㈷, ㉁, ㉀ ]
  #時間
      '/sj': [ ㍘, ㍙, ㍚, ㍛, ㍜, ㍝, ㍞, ㍟, ㍠, ㍡, ㍢, ㍣, ㍤, ㍥, ㍦, ㍧, ㍨, ㍩, ㍪, ㍫, ㍬, ㍭, ㍮, ㍯, ㍰ ]
  #天干、地支、干支
      '/tg': [ 甲, 乙, 丙, 丁, 戊, 己, 庚, 辛, 壬, 癸 ]
      '/dz': [ 子, 丑, 寅, 卯, 辰, 巳, 午, 未, 申, 酉, 戌, 亥 ]
      '/gz': [ 甲子, 乙丑, 丙寅, 丁卯, 戊辰, 己巳, 庚午, 辛未, 壬申, 癸酉, 甲戌, 乙亥, 丙子, 丁丑, 戊寅, 己卯, 庚辰, 辛巳, 壬午, 癸未, 甲申, 乙酉, 丙戌, 丁亥, 戊子, 己丑, 庚寅, 辛卯, 壬辰, 癸巳, 甲午, 乙未, 丙申, 丁酉, 戊戌, 己亥, 庚子, 辛丑, 壬寅, 癸卯, 甲辰, 乙巳, 丙午, 丁未, 戊申, 己酉, 庚戌, 辛亥, 壬子, 癸丑, 甲寅, 乙卯, 丙辰, 丁巳, 戊午, 己未, 庚申, 辛酉, 壬戌, 癸亥 ]
  #節氣
      '/jq': [ 立春, 雨水, 驚蟄, 春分, 清明, 穀雨, 立夏, 小滿, 芒種, 夏至, 小暑, 大暑, 立秋, 處暑, 白露, 秋分, 寒露, 霜降, 立冬, 小雪, 大雪, 冬至, 小寒, 大寒 ]
  #單位
      '/dw': [ Å, ℃, ％, ‰, ‱, °, ℉, ㏃, ㏆, ㎈, ㏄, ㏅, ㎝, ㎠, ㎤, ㏈, ㎗, ㎙, ㎓, ㎬, ㏉, ㏊, ㏋, ㎐, ㏌, ㎄, ㎅, ㎉, ㎏, ㎑, ㏍, ㎘, ㎞, ㏎, ㎢, ㎦, ㎪, ㏏, ㎸, ㎾, ㏀, ㏐, ㏓, ㎧, ㎨, ㎡, ㎥, ㎃, ㏔, ㎆, ㎎, ㎒, ㏕, ㎖, ㎜, ㎟, ㎣, ㏖, ㎫, ㎳, ㎷, ㎹, ㎽, ㎿, ㏁, ㎁, ㎋, ㎚, ㎱, ㎵, ㎻, ㏘, ㎩, ㎀, ㎊, ㏗, ㏙, ㏚, ㎰, ㎴, ㎺, ㎭, ㎮, ㎯, ㏛, ㏜, ㎔, ㏝, ㎂, ㎌, ㎍, ㎕, ㎛, ㎲, ㎶, ㎼ ]
  #貨幣
      '/hb': [ ￥, ¥, ¤, ￠, ＄, $, ￡, £, ৳, ฿, ₠, ₡, ₢, ₣, ₤, ₥, ₦, ₧, ₩, ₪, ₫, €, ₭, ₮, ₯, ₰, ₱, ₲, ₳, ₴, ₵, ₶, ₷, ₸, ₹, ₺, ₨, ﷼ ]
  #結構、偏旁、康熙（部首）、筆畫、標點
      '/jg': [ ⿰, ⿱, ⿲, ⿳, ⿴, ⿵, ⿶, ⿷, ⿸, ⿹, ⿺, ⿻, 〾 ]
      '/pp': [ 乛, 冫, 丷, 龹, ⺌, 龸, 亻, 亼, 亽, 仒, 冖, 冂, 冃, 冄, 宀, 罒, 㓁, 罓, 冈, 凵, 厶, 刂, 勹, 匚, 匸, 卩, 阝, 厂, 丆, 广, 壬, 訁, 讠, 釒, 钅, 飠, 饣, 龺, 攵, 夂, 夊, 尢, 尣, 兂, 旡, 巜, 巛, 彐, 彑, 彡, 彳, 龰, 辶, 廴, 㞢, 忄, 㣺, 扌, 爫, 龵, 廾, 歺, 癶, 氵, 氺, 火, 灬, 爿, 丬, 疒, 牜, ⺶, 犭, 豕, 豸, 虍, 艹, 卝, 龷, 丗, 龶, 芈, 丵, 菐, 黹, 礻, 衤, 糸, 糹, 纟, 龻, 镸, 髟, 襾, 覀, 吅, 㗊, 㠭, 㸚, 叕]
      '/kx': [ 一, 丨, 丶, 丿, 乙, 亅, 二, 亠, 人, 儿, 入, 八, 冂, 冖, 冫, 几, 凵, 刀, 力, 勹, 匕, 匚, 匸, 十, 卜, 卩, 厂, 厶, 又, 口, 囗, 土, 士, 夂, 夊, 夕, 大, 女, 子, 宀, 寸, 小, 尢, 尸, 屮, 山, 巛, 工, 己, 巾, 干, 幺, 广, 廴, 廾, 弋, 弓, 彐, 彡, 彳, 心, 戈, 戶, 手, 支, 攴, 文, 斗, 斤, 方, 无, 日, 曰, 月, 木, 欠, 止, 歹, 殳, 毋, 比, 毛, 氏, 气, 水, 火, 爪, 父, 爻, 爿, 片, 牙, 牛, 犬, 玄, 玉, 瓜, 瓦, 甘, 生, 用, 田, 疋, 疒, 癶, 白, 皮, 皿, 目, 矛, 矢, 石, 示, 禸, 禾, 穴, 立, 竹, 米, 糸, 缶, 网, 羊, 羽, 老, 而, 耒, 耳, 聿, 肉, 臣, 自, 至, 臼, 舌, 舛, 舟, 艮, 色, 艸, 虍, 虫, 血, 行, 衣, 襾, 見, 角, 言, 谷, 豆, 豕, 豸, 貝, 赤, 走, 足, 身, 車, 辛, 辰, 辵, 邑, 酉, 釆, 里, 金, 長, 門, 阜, 隶, 隹, 雨, 靑, 非, 面, 革, 韋, 韭, 音, 頁, 風, 飛, 食, 首, 香, 馬, 骨, 高, 髟, 鬥, 鬯, 鬲, 鬼, 魚, 鳥, 鹵, 鹿, 麥, 麻, 黃, 黍, 黑, 黹, 黽, 鼎, 鼓, 鼠, 鼻, 齊, 齒, 龍, 龜, 龠 ]
      '/bh': [ ㇀, ㇁, ㇂, ㇃, ㇄, ㇅, ㇆, ㇇, ㇈, ㇉, ㇊, ㇋, ㇌, ㇍, ㇎, ㇏, ㇐, ㇑, ㇒, ㇓, ㇔, ㇕, ㇖, ㇗, ㇘, ㇙, ㇚, ㇛, ㇜, ㇝, ㇞, ㇟, ㇠, ㇡, ㇢, ㇣ ]
      '/bd': [ ₋, ⁻, ―, ˗, ˉ, ＿, ﹍, ﹎, ．, ¡, ‼, ⁉, ¿, ؟, ⁈, ⁇, ､, ｡, 、, 。, 〃, 〄, 々, 〆, 〇, 〈, 〉, 《, 》, 「, 」, 『, 』, 【, 】, 〒, 〓, 〔, 〕, 〖, 〗, 〘, 〙, 〚, 〛, 〜, 〝, 〞, 〟, 〠, 〰, 〱, 〲, 〳, 〴, 〵, 〶, 〷, 〻, 〼, 〽 ]
      '/bdz': [ ﹅, ﹆, ﹁, ﹂, ﹃, ﹄, ︙, ︱, ︻, ︼, ︗, ︘, ︵, ︶, ︷, ︸, ︹, ︺, ︿, ﹀, ︽, ︾, ︰, ︲, ︳, ︴, ﹉, ﹊, ﹋, ﹌, ﹍, ﹎, ﹏, ﹇, ﹈, ︐, ︑, ︒, ︔, ︕, ︖ ]
  #拼音、註音、聲調
      '/py': [ ā, á, ǎ, à, ō, ó, ǒ, ò, ê, ē, é, ě, è, ī, í, ǐ, ì, ū, ú, ǔ, ù, ü, ǖ, ǘ, ǚ, ǜ, , ń, ň,  ]
      '/zy': [ ㄅ, ㄆ, ㄇ, ㄈ, ㄉ, ㄊ, ㄋ, ㄌ, ㄍ, ㄎ, ㄏ, ㄐ, ㄑ, ㄒ, ㄓ, ㄔ, ㄕ, ㄖ, ㄗ, ㄘ, ㄙ, ㄧ, ㄨ, ㄩ, ㄚ, ㄛ, ㄜ, ㄝ, ㄞ, ㄟ, ㄠ, ㄡ, ㄢ, ㄣ, ㄤ, ㄥ, ㄦ, ㄪ, ㄫ, ㄬ, ㄭ, ㆠ, ㆡ, ㆢ, ㆣ, ㆤ, ㆥ, ㆦ, ㆧ, ㆨ, ㆩ, ㆪ, ㆫ, ㆬ, ㆭ, ㆮ, ㆯ, ㆰ, ㆱ, ㆲ, ㆳ, ㆴ, ㆵ, ㆶ, ㆷ ]
      '/sd': [ ˉ, ˊ, ˇ, ˋ, ˆ, ˙, ˜, ˥, ˦, ˧, ˨, ˩, ꜀, ꜁, ꜂, ꜃, ꜄, ꜅, ꜆, ꜇ ]
  #漢字+圈/弧
      '/hzq': [ ㊀, ㊁, ㊂, ㊃, ㊄, ㊅, ㊆, ㊇, ㊈, ㊉, ㊊, ㊋, ㊌, ㊍, ㊎, ㊏, ㊐, ㊑, ㊒, ㊓, ㊔, ㊕, ㊖, ㊗, ㊘, ㊙, ㊚, ㊛, ㊜, ㊝, ㊞, ㊟, ㊠, ㊡, ㊢, ㊣, ㊤, ㊥, ㊦, ㊧, ㊨, ㊩, ㊪, ㊫, ㊬, ㊭, ㊮, ㊯, ㊰, ㉄, ㉅, ㉆, ㉇ ]
      '/hzh': [ ㈠, ㈡, ㈢, ㈣, ㈤, ㈥, ㈦, ㈧, ㈨, ㈩, ㈪, ㈫, ㈬, ㈭, ㈮, ㈯, ㈰, ㈱, ㈲, ㈳, ㈴, ㈵, ㈶, ㈷, ㈸, ㈹, ㈺, ㈻, ㈼, ㈽, ㈾, ㈿, ㉀, ㉁, ㉂, ㉃ ]
  #いろは順
      '/iro': [ い, ろ, は, に, ほ, へ, と, ち, り, ぬ, る, を, わ, か, よ, た, れ, そ, つ, ね, な, ら, む, う, ゐ, の, お, く, や, ま, け, ふ, こ, え, て, あ, さ, き, ゆ, め, み, し, ゑ, ひ, も, せ, す ]
  #假名
      '/jm': [ あ, ぁ, い, ぃ, う, ぅ, え, ぇ, お, ぉ, か, ゕ, が, き, ぎ, く, ぐ, け, ゖ, げ, こ, ご, さ, ざ, し, じ, す, ず, せ, ぜ, そ, ぞ, た, だ, ち, ぢ, つ, っ, づ, て, で, と, ど, な, に, ぬ, ね, の, は, ば, ぱ, ひ, び, ぴ, ふ, ぶ, ぷ, へ, べ, ぺ, ほ, ぼ, ぽ, ま, み, む, め, も, や, ゃ, ゆ, ゅ, よ, ょ, ら, り, る, れ, ろ, わ, ゎ, ゐ, ゔ, ゑ, を, ん, ・, ー, ゝ, ゞ, ゟ ]
      '/pjm': [ ア, ァ, イ, ィ, ウ, ゥ, エ, ェ, オ, ォ, カ, ヵ, ガ, キ, ギ, ク, グ, ケ, ヶ, ゲ, コ, ゴ, サ, ザ, シ, ジ, ス, ズ, セ, ゼ, ソ, ゾ, タ, ダ, チ, ヂ, ツ, ッ, ヅ, テ, デ, ト, ド, ナ, ニ, ヌ, ネ, ノ, ハ, バ, パ, ヒ, ビ, ピ, フ, ブ, プ, ヘ, ベ, ペ, ホ, ボ, ポ, マ, ミ, ム, メ, モ, ヤ, ャ, ユ, ュ, ヨ, ョ, ラ, リ, ル, レ, ロ, ワ, ヮ, ヰ, ヸ, ヴ, ヱ, ヹ, ヲ, ヺ, ン, ・, ー, ヽ, ヾ, ヿ, ㇰ, ㇱ, ㇲ, ㇳ, ㇴ, ㇵ, ㇶ, ㇷ, ㇸ, ㇹ, ㇺ, ㇻ, ㇼ, ㇽ, ㇾ, ㇿ ]
      '/jmk': [ か, ゕ, き, く, け, ゖ, こ, カ, ヵ, キ, ク, ケ, ヶ, コ ]
      '/jmg': [ が, ぎ, ぐ, げ, ご, ガ, ギ, グ, ゲ, ゴ ]
      '/jms': [ さ, し, す, せ, そ, サ, シ, ス, セ, ソ ]
      '/jmz': [ ざ, じ, ず, ぜ, ぞ, ザ, ジ, ズ, ゼ, ゾ ]
      '/jmt': [ た, ち, つ, っ, て, と, タ, チ, ツ, ッ, テ, ト ]
      '/jmd': [ だ, ぢ, づ, で, ど, ダ, ヂ, ヅ, デ, ド ]
      '/jmn': [ な, に, ぬ, ね, の, ん, ナ, ニ, ヌ, ネ, ノ, ン ]
      '/jmh': [ は, ひ, ふ, へ, ほ, ハ, ヒ, フ, ヘ, ホ ]
      '/jmb': [ ば, び, ぶ, べ, ぼ, バ, ビ, ブ, ベ, ボ ]
      '/jmp': [ ぱ, ぴ, ぷ, ぺ, ぽ, パ, ピ, プ, ペ, ポ ]
      '/jmm': [ ま, み, む, め, も, マ, ミ, ム, メ, モ ]
      '/jmy': [ や, ゃ, ゆ, ゅ, よ, ょ, ヤ, ャ, ユ, ュ, ヨ, ョ ]
      '/jmr': [ ら, り, る, れ, ろ, ラ, リ, ル, レ, ロ ]
      '/jmw': [ わ, ゐ, ゑ, を, ワ, ヰ, ヱ, ヲ ]
      '/jma': [ あ, か, が, さ, ざ, た, だ, な, は, ば, ぱ, ま, や, ら, わ, ア, カ, ガ, サ, ザ, タ, ダ, ナ, ハ, バ, パ, マ, ヤ, ラ, ワ ]
      '/jmi': [ い, き, ぎ, し, じ, ち, ぢ, に, ひ, び, ぴ, み, り, ゐ, イ, キ, ギ, シ, ジ, チ, ヂ, ニ, ヒ, ビ, ピ, ミ, リ, ヰ ]
      '/jmu': [ う, く, ぐ, す, ず, つ, づ, ぬ, ふ, ぶ, ぷ, む, る, ウ, ク, グ, ス, ズ, ツ, ヅ, ヌ, フ, ブ, プ, ム, ル ]
      '/jme': [ え, け, げ, せ, ぜ, て, で, ね, へ, べ, ぺ, め, れ, ゑ, エ, ケ, ゲ, セ, ゼ, テ, デ, ネ, ヘ, ベ, ペ, メ, レ, ヱ ]
      '/jmo': [ お, こ, ご, そ, ぞ, と, ど, の, ほ, ぼ, ぽ, も, ろ, を, オ, コ, ゴ, ソ, ゾ, ト, ド, ノ, ホ, ボ, ポ, モ, ロ, ヲ ]
  #假名+圈
      '/jmq': [ ㋐, ㋑, ㋒, ㋓, ㋔, ㋕, ㋖, ㋗, ㋘, ㋙, ㋚, ㋛, ㋜, ㋝, ㋞, ㋟, ㋠, ㋡, ㋢, ㋣, ㋤, ㋥, ㋦, ㋧, ㋨, ㋩, ㋪, ㋫, ㋬, ㋭, ㋮, ㋯, ㋰, ㋱, ㋲, ㋳, ㋴, ㋵, ㋶, ㋷, ㋸, ㋹, ㋺, ㋻, ㋼, ㋽, ㋾ ]
  #假名+半角
      '/jmbj': [ ｱ, ｧ, ｲ, ｨ, ｳ, ｩ, ｴ, ｪ, ｵ, ｫ, ｶ, ｷ, ｸ, ｹ, ｺ, ｻ, ｼ, ｽ, ｾ, ｿ, ﾀ, ﾁ, ﾂ, ｯ, ﾃ, ﾄ, ﾅ, ﾆ, ﾇ, ﾈ, ﾉ, ﾊ, ﾋ, ﾌ, ﾍ, ﾎ, ﾏ, ﾐ, ﾑ, ﾒ, ﾓ, ﾔ, ｬ, ﾕ, ｭ, ﾖ, ｮ, ﾗ, ﾘ, ﾙ, ﾚ, ﾛ, ﾜ, ｦ, ﾝ, ･, ｰ, ﾞ, ﾟ ]
  #韓文
      '/hw': [ ㄱ, ㄴ, ㄷ, ㄹ, ㅁ, ㅂ, ㅅ, ㅇ, ㅈ, ㅊ, ㅋ, ㅌ, ㅍ, ㅎ ]
  #韓文+圈/弧
      '/hwq': [ ㉠, ㉡, ㉢, ㉣, ㉤, ㉥, ㉦, ㉧, ㉨, ㉩, ㉪, ㉫, ㉬, ㉭, ㉮, ㉯, ㉰, ㉱, ㉲, ㉳, ㉴, ㉵, ㉶, ㉷, ㉸, ㉹, ㉺, ㉻, ㉼, ㉽, ㉾, ㉿ ]
      '/hwh': [ ㈀, ㈁, ㈂, ㈃, ㈄, ㈅, ㈆, ㈇, ㈈, ㈉, ㈊, ㈋, ㈌, ㈍, ㈎, ㈏, ㈐, ㈑, ㈒, ㈓, ㈔, ㈕, ㈖, ㈗, ㈘, ㈙, ㈚, ㈛, ㈜, ㈝, ㈞ ]
      '/zz': ["→_→", "←_←", "O(∩_∩)O", "╮(╯▽╰)╭", "┑(￣▽ ￣)┍ ", "(≧﹏ ≦)", "(￣ε ￣) ", "(*▔＾▔*)", "O__O", "(^_^)", "(╰_╯)", "ψ(￣︶￣)ψ", "-_-||", "(╯#-_-)╯╧═╧", "◔‸◔", "= =囧~~", "•﹏•"]
      '/wz': ["zhihu.com", "google.com", "gmail.com", "mail.qq.com", "zNote.html" ]
```

#### fcitx5
需要卸載之前的fcitx`sudo pacman -Rsc fcitx`

安裝fcitx5-im,包括了fcitx5、fcitx5-configtool、fcitx5-gtk、fcitx5-qt
```
sudo pacman -S fcitx5-im  # fcitx5-im 包括了 fcitx5、fcitx5-configtool、fcitx5-gtk、fcitx5-qt
yay -S fcitx5-rime
```
配置和fcitx的差不多，位置有所不同，在`~/.local/share/fcitx5/rime/`
主题：
```
cd /home/fiki/.local/share/fcitx5/themes && mkdir Material-Color && cd Material-Color
git clone https://github.com/hosxy/Fcitx5-Material-Color.git ~/.local/share/fcitx5/themes/Material-Color
ln -sf theme-blue.conf theme.conf
cd ~/.config/fcitx5/conf && vim classicui.conf # 将最后的 theme 更改 Material-Color 即可
```
候选的字体太小，在`~/.config/fcitx5/conf/classicui.conf`修改font、menufont的字号即可，建议‘PerScreenDPI=False‘

```classicui.conf
# Vertical Candidate List
Vertical Candidate List=False
# Use Per Screen DPI
PerScreenDPI=True
# Use mouse wheel to go to prev or next page
WheelForPaging=True
# Font
Font="Sans 12"
# Menu Font
MenuFont="Sans 12"
# Tray Font
TrayFont="Sans Bold 10"
# Tray Label Outline Color
TrayOutlineColor=#000000
# Tray Label Text Color
TrayTextColor=#ffffff
# Prefer Text Icon
PreferTextIcon=False
# Show Layout Name In Icon
ShowLayoutNameInIcon=True
# Use input method language to display text
UseInputMethodLangaugeToDisplayText=True
# Theme
Theme=Material-Color
```




#### 其他
fcitx 修改 luna_pinyin.custom.yaml 可以对全半角符号进行修改且有效，但是在换到fcitx5后就无效了，建议先去看 user.yaml 文件的内容
比如内容为:
```
var:
  last_build_time: 1655690864
  previously_selected_schema: luna_pinyin_simp
  schema_access_time:
    luna_pinyin_simp: 1647270274
```
则文件名为 `luna_pinyin_simp.custom.yaml`