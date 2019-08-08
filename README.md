### redis-py
---
https://github.com/andymccurdy/redis-py

```py
import redis
r = redis.Redis(host='localhost', port=6379, db=0)
r.set('foo', 'bar')
r.get('foo')


def mset(self, mapping):
def msetnx(self, mapping):
def zadd(self, mapping, nx=False, xx=False, ch=False, incr=False):

def zincrby(self, name, amount, value):

try:
  with r.lock('my-lock-key', blocking_timeout=5) as lock:
except LockError:

pool = redis.ConnectionPool(host='localhost', port=6379, db=0)
r = redis.Redis(connection_pool=pool)


r = redis.Redis(unix_socket_path='/tmp/redis.sock')

pool = redis.ConnectionPool(connection_class=YourConnectionClass,
  your_arg='...', ...)
  
r = redis.Redis(...)
r.set('bing', 'baz')
pipe = r.pipeline()
pipe.set('foo', 'bar')
pipe.get('bing')
pipe.execute()

pipe.set('foo', 'bar').sadd('faz', 'baz').incr('auto_number').execute()

pipe = r.pipeline(transaction=False)

with r.pipeline() as pipe:
  while True:
    try:
      pipe.watch('OUR-SEQUENCE-KEY')
      current_value = pipe.get('OUR-SEQUENCE-KEY')
      next_value = int(current_value) + 1
      pipe.multi()
      pipe.set('OUR-SEQUENCE-KEY', next_value)
      pipe.execute()
      break
    except WatchError:
      continue

pipe = r.pipeline()
while True:
  try:
    pipe.watch('OUR-SEQUENCE-KEY')
    pipe.execute()
    break
  except WatchError:
    continue
  finally:
    pipe.reset()

def client_side_incr(pipe):
  current_value = pipe.get('OUR-SEUENCE-KEY')
  next_value = int(current_value) + 1
  pipe.multi()
  pipe.set('OUR-SEQUENCE-KEY', next_value)
r.transaction(client_side_incr, 'OUR-SEQUENCE-KEY')


r = redis.Redis(...)
p = r.pubsub()

p.subscribe('my-first-channel', 'my-second-channel', ...)
p.psubscribe('my-*', ...)

p.get_message()
p.get_message()
p.get_message()

r.publish('my-first-channel', 'some data')
p.get_message()
p.get_message()

p.unsubscribe()
p.punsubscribe('my-*')
p.get_message()
p.get_message()
p.get_message()

def my_handler(message):
  print 'MY HANDLER: ', message['data']
p.subscribe(**{'my-channel': my_handler})
p.get_message()
r.publish('my-channel', 'awesome data')
message = p.get_message()
print message

p = r.pubsub(ignore_subscribe_messages=True)
p.subscribe('my-channel')
p.get_message()
r.publish('my-channel', 'my data')
p.get_message()

while True:
  message = p.get_message()
  if message:
  time.sleep(0.001)

for message in p.listen():

for message in p.listen():

p.subscribe(**{'my-channel': my_handler})
thread = p.run_in_thread(sleep_time=0.001)

p = r.pubsub()
p.close()

r.pubsub_channels()
r.pubsub_numsub('foo', 'bar')
r.pubsub_numsub('baz')
r.pubsub_numpat()


r = redis.Redis()
with r.monitor() as m:
  for command in m.listen():
    print(command)
    
r = redis.Redis()
lua = """
  local value = redis.call('GET', KEYS[1])
  value = tonumber(value)
  return value * ARGV[1]"""
multiply = r.register_script(lua)

r.set('foo', 2)
multiply(keys=['foo'], args=[5])

r2 = redis.Redis('redis2.example.com')
r2.set('foo', 3)
multiply(keys=['foo'], args=[5], client=r2)

pipe = r.pipeline()
pipe.set('foo', 5)
multiply(keys=['foo'], args=[5], client=pipe)
pipe.execute()

from redis.seentinel import Sentinel
sentine1 = Sentinel(['localhost', 26379], socket_timeout=0.1)
sentinel.discover_master('master')
sentine1.discover_slaves('mymaster')

master = sentinel.master_for('mymaster', socket_timeout=0.1)
slave = sentinel.slave_for('mymaster', socket_timeout=0.1)
master.set('foo', 'bar')
slave.get('foo')

for key, value in (('A', '1'), ('B', '2'), ('C', '3')):
for key in r.scan_iter():
  printkey, rget(key)
```

```sh
python setup.py install
pip install hiredis
```

```
```
