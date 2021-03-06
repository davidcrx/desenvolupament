<!-- TITLE: Programació -->
<!-- SUBTITLE: Petits recordatoris programació -->

# Programació

## Python


```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

# Author: David Creus
# STANZA FACEBOOK BOTS
# Definim un diccionari a una variable, per example data


data = {
  "object": "page",
  "entry": [
    {
      "id": "1850712351897323",
      "time": 1531210141650,
      "messaging": [
        {
          "sender": {
            "id": "1694287340686023"
          },
          "recipient": {
            "id": "1850712351897323"
          },
          "timestamp": 1531210136923,
          "message": {
            "mid": "Qpo2kpNlt3Sv8lVd5PJ66F70OoMLVYsKN8twYLQfz76Cuh8zWPErC3cJWoHhNG-yrJ5y-7twhn8uejTjoIpYXg",
            "seq": 11741,
            "text": "adeu"
          }
        }
      ]
    }
  ]
}

# = {
#   "object": "page",
#   "entry": [
#     {
#       "id": "1850712351897323",
#       "time": 1531207176013,
#       "seconds": 324243,
#       "messaging": [
#         {
#           "sender": {
#             "id": "1694287340686023"
#           },
#           "recipient": {
#             "id": "1850712351897323"
#           },
#           "timestamp": 1531145458545,
#           "message": {
#             "mid": "XoPbN4K-Q4GbFaiqmb92o170OoMLVYsKN8twYLQfz76rHNPPexDwoouyk--uRKEbiWHe-BNZhBgdK7hgO35v3A",
#             "seq": 11713,
#             "attachments": [
#               {
#                 "type": "image",
#                 "payload": {
#                   "url": "https://cdn.fbsbx.com/v/t59.2708-21/34838272_2197499890265596_9223063022547763200_n.gif?_nc_cat=0&oh=99954fee077d2112bfc197169dcd0600&oe=5B462BBC"
#                 }
#               }
#             ]
#           }
#         }
#       ]
#     }
#   ]
# }




# Comprovem iterativament els items.


entries = data['entry']
#print(str(entries))

for item in entries:
    #print(str(item['messaging']))
    msgs = item['messaging']
    for m in msgs:
        message = m['message']
        #print(str(message))
        if 'attachments' in message:
          attachments = message['attachments']
          #print(str(attachments))
          for item2 in attachments:
            if 'payload' in item2:
              payload = item2['payload']
              #print(str(payload))
              if 'url' in payload:
                url = payload['url']
                print(str(url))
        if 'text' in message:
          text = message['text']
          print(str(text))
```

Any actual:

```python
def get_year():
    """
    Retorna el any actual
    """
    import datetime
    now = datetime.datetime.now()
    return(now.year)
```

# Custom Redis


```python
import asyncio
import random
import aioredis
import logging
from quart import Quart, request, url_for, jsonify

aredis = None

async def init_redis():
    global aredis
    aredis = await aioredis.create_redis_pool(('redis-accounts', 6379), minsize=5, maxsize=20, loop=loop)


loop = asyncio.get_event_loop()
loop.run_until_complete(init_redis())


async def store_user_data(userId, data):
    """
    """
    await aredis.set('test_'+userId, data)


async def get_user_data(userId):
    """
    """
    data = await aredis.get('test_'+userId)

    if data:
        logging.info('data almacenada ---> '+str(data))
    else:
        logging.info('no s ha trobat info....')

    return dat

```

*  App. py (integració redis)

```python
@app.before_first_request
async def init():
    logging.info('INIT_APP')
    await db.init_mysql()
    await customRedis.init_redis()


@app.route('/logout')
async def logout():
    session.clear()
    return redirect('/login', 302)


@app.route('/store-redis')
async def store_redis():
    data = {
        'telf':'123123123'
    }
    await customRedis.store_user_data('user1', json.dumps(data))
    return 'stored'


@app.route('/get-redis')
async def get_redis():
    data = await customRedis.get_user_data('user1')
    print(str(data))
    return 'readed'
```

# String to float numbers



```python
values = ["100,123 €", "100.123 €", "100,000 €", "100.000 €", "89 €", "150 €", "100 €", "123,123 €"]

def testing_bench(value1, value2):

    value1 = value1.replace("€","")
    value1 = value1.replace(" ","")
    value2 = value2.replace("€","")
    value2 = value2.replace(" ","")
    
    val = float(value1.replace(',','.'))
    val2 = float(value2.replace(',','.'))
    val3 = val<=val2
    
    return val3


result = testing_bench(values[4], values[7])
print(result)

```

