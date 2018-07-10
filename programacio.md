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
