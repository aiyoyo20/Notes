#!/usr/bin/env python3
# Author: aiyoyoð

1ãå¯åç±»åé·é±
```
l = []
a = []
for i in range(10):
    a.append(i)
    l.append(a)
print(l)
```

```
l = []
a = {'num': 0}
for i in range(10):
    a['num'] = i
    l.append(a)
print(l)
print(a)
```

é½æ¯ç±»ä¼¼çï¼æ¯æ¬¡æ°å¢çé½æ¯åä¸ä¸ªå¯¹è±¡ï¼å¹¶å¨å¶åè¿è¡äºä¿®æ¹ï¼å¯¼è´ä¹åçä¹è¢«ä¿®æ¹ï¼è¦çï¼ã

2ãlambda é·é±
```
a = [lambda x:x+n for n in range(9)]
print(b(0) for b in a)
```

lambda ä¸­çåéä¸ºèªç±åéï¼èä¸æ¯åæ®éå½æ°é£æ ·æèªå·±çç©ºé´ï¼
æä»¥ä¸é¢çåéxæ¯ä¸ç´å¨ååçï¼ç´è³è¢«æåä¸ä¸ªè¦ç
