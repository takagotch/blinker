### blinker
---
https://github.com/jek/blinker

```py
from blinker import signal
started = signal('round-started')
def each(round):
  print "Round %s!" % round
started.connect(each)

def round_two(round):
  print "This is round two."
started.connect(round_two, sender=2)

for round in range(1, 4):
  started.send(round)
```

```py
class Processor:
  def __init__(self, name):
    self.name = name
    
  def go(self):
    ready = signal('ready')
    ready.send(self)
    print()
    complete = signal('complete')
    complete.send(self)
  
  def __repr__(self):
    return '<Processor %s>' % self.name
    
processor_a = Processor('a')
processor_a.go()




```

```
```


