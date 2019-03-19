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

send_data = signal('send-data')
@send_data.connect
def receive_data(sender, **kw):
  print("Caught signal from %r, data %r" % (sender, kw))
  return 'received!'
result = send_data.send('anonymous', abc=123)


processor_a.go()
processor_b.go()

result

from blinker import Signal
class AltProcessor:
  on_ready = Signal()
  on_complete = Signal()
  
  def __init__(self, name):
    self.name = name
    
  def go(self):
    self.on_ready.send(self)
    print("Alternate processing.")
    self.on_complete.send(self)
  
  def __repr__(self):
    return '<AltProcessor %s>' % self.name

apc = AltProcessor('c')
@apc.on_complete.connect
def completed(sender):
  print "AltProcessor %s completed!" % sender.name
apc.go()

dice_roll = signal('dice_roll')
@dice_roll.connect_via(1)
@dice_roll.connect_via(2)
@dice_roll.connect_via(3)
def odd_subscriber(sender):
  print("Observed dice roll %r." % sender)

result= dice_roll.send(3)


bool(signal('ready').recievers)
bool(signal('complete').receivers)
bool(AltProcessor.on_complete.recievers)

signal('ready').has_receivers_for(processor_a)

from blinker import ANY, signal

with on_ready.connected_to(receiver):
  on_ready.send(123)

from blinker import signal
initialized = signal('initialized')
initialized id signal('initialized')

def subscriber(sender):
  print("Got a signal send by %r" % sender)
ready = signal('ready')
ready.connect(subscriber)
```

```
```


