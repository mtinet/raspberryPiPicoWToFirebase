# raspberryPiPicoWTofirebase

```python 
from machine import Pin, I2C
import network
import utime
# 이 파일과 같은 폴더에 secrets.py파일을 만들고, SSID, Password 파일을 넣어놓을 것
import secrets
import urequests

# Connect Internet by WiFi
wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect(secrets.SSID, secrets.PASSWORD)
print(wlan.isconnected())
print(wlan.ifconfig())

url = "https://smartfarm-f867f-default-rtdb.firebaseio.com/"

# get: 리스트 가져오기
# get+데이터 주소: 단일 데이터 가져오기
# post: 객체 등록하기
# put: 업데이트(객체 교체하기)
# patch: 업데이트(일부 값만 업데이트)
# delete: 객체 삭제

# 전체 json파일 가져오기
response = urequests.get(url+".json")
print(response.content)

# json파일 중 일부 가져오기
response = urequests.get(url+"-NIPukhnX6qkPVb-P6Eh.json")
print(response.content)

# 데이터 추가하기, 자동으로 주소가 붙고, 그 아래에 데이터를 추가함
myobj = {'somekey': 'somevalue'}
urequests.post(url+".json", json = myobj)

# 객체 교체하기, 특정 주소의 데이터가 변경됨
myobj = {'ahha': 'jaja'}
urequests.put(url+"test.json", json = myobj)

# 객체 교체하기, 특정 주소의 데이터가 변경됨
myobj = {'hhhggfggff': 'ssssssss'}
urequests.patch(url+"test.json", json = myobj)

# 객체 삭제
urequests.delete(url+"test.json")

response = urequests.get(url+".json")
print(response.content)

```
