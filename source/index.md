---
title: WFDManager - API Reference

language_tabs:
  - java
  - csharp

toc_footers:
  - <a href='http://github.com/flyingbuffalo/WFDAndroid'>Go to the WFDManager repository</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the WFDManager API! WFDManager is WiFi Direct Transfer Library. You can use our API to access other WiFi Direct device, which can transfer data using socket connection.

We have language bindings in Android, C#(Windows 8). You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [WFDManager](http://github.com/flyingbuffalo/WFDAndroid). Feel free to edit it and use it as a base for your own API's documentation.

#package flyingBuffalo

##interface
 - WFDDeviceDiscoveredListener
 - WFDDeviceConnectedListener
 - WFDPairInfo.PairSocketConnectedListener

##class
 - WFDManager
 - WFDDevice
 - WFDPairInfo

#API List

Interface | Method
--------- | -----------
WFDDeviceDiscoveredListener| onDevicesDiscovered
                           | onDevicesDiscoverFailed
WFDDeviceConnectedListener | onDeviceConnected
                           | onDeviceConnectFailed
                           | onDeviceDisconnected
WFDPairInfo.PairSocketConnectedListener | onSocketConnected


Class | Method
--------- | -----------
WFDManager |getDevicesAsync
           |pairAsync
           |unpair
           |setWFDDeviceDiscoveredListener
           |setWFDDeviceConnectedListener
WFDDevice|
WFDPairInfo|getLocalAddress
           |getRemoteAddress
           |getWFDDevice
           |connectSocketAsync


#WFDDeviceDiscoveredListener
WFDManager.getDevicesAsync의 결과값을 포착하는 리스너
##1. Methods
### onDevicesDiscovered
```csharp
void onDevicesDiscovered(List<WFDDevice> deviceList)

```

```java
/*추가하삼!*/
```
void onDevicesDiscovered(deviceList)

장치 탐색 성공 시 deviceList와 함께 호출 됨.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
deviceList|List&lt;WFDDevice&gt;|List&lt;WFDDevice&gt;| 탐색 성공한 기기 목록 |


#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



### onDevicesDiscoverFailed
```csharp
void onDevicesDiscoverFailed(int reasonCode)

```

```java
/*추가하삼!*/
```
void onDevicesDiscoverFailed(reasonCode)

장치 탐색 실패 시 호출 됨.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
reasonCode|int|int| 실패 원인 코드 |


#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



#WFDDeviceConnectedListener
WFDManager.connectAsync의 결과값을 포착하는 리스너
##1. Methods
### onDeviceConnected
```csharp
void onDeviceConnected(WFDPairInfo pair)

```

```java
/*추가하삼!*/
```
void onDeviceConnected(WFDPairInfo pair)

장치 연결 성공 시 호출 됨

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
pair|WFDPairInfo|WFDPairInfo| 연결에 성공한 WFDPairInfo |


#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



### onDeviceConnectFailed
```csharp
void onDeviceConnectFailed(int reasonCode)

```

```java
/*추가하삼!*/
```
void onDeviceConnectFailed(reasonCode)

장치 연결 실패 시 호출 됨.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
reasonCode|int|int| 실패 원인 코드 |


#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          


### onDeviceDisconnected
```csharp
void onDeviceDisconnected()

```

```java
/*추가하삼!*/
```
void onDeviceDisconnected()

장치 연결 종료 시 호출 됨

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



#PairSocketConnectedListener
WFDPairInfo.connectSocketAsync의 결과값을 포착하는 리스너
##1. Methods
### onSocketConnected
```csharp
void onSocketConnected(StreamSocket socket)

```

```java
/*추가하삼!*/
```
void onSocketConnected(socket)

StreamSocket 생성 성공 시 호출 됨

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
socket|StreamSocket|StreamSocket|생성 성공한 StreamSocket


#### Return

Return name |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          



#WFDManager
1. wifi direct를 시작하고 2. 주변의 wifi direct장치를 찾으며 3. Pairing, unPairing을 담당한다. 

##1. Field
##2. Constructor
- WFDManager(DependencyObject parent,
   WFDDeviceDiscoveredListener wfdDeviceDiscoveredListener,
WFDDeviceConnectedListener wfdDeviceConnectedListener)
  : 장비의 Wifi direct를 사용할 수 있도록 상태를 변경하고, connetecion 요청을 처리할 리스너를 등록한다.

##3. Methods
###getDevicesAsync
void getDevicesAsync()
: 주변의 wifi direct가 켜져있는 Device들을 비동기적으로 탐색한다. wfdDeviceDiscoveredListener를 통해, 성공 시 List<WFDDevice>를 반환한다. 내부적으로 Android를 탐색하기위해Windows.Devices.WiFiDirect를 사용하고, Windows를 탐색하기위해Windows.Networking.Proximity를 사용한다.  탐색 도중 작업이 취소되면 탐색된 리스트를 clear한다. 

###pairAsync
void pairAsync(WFDDevice device)
: device와 비동기적으로 페어링한다. 
WFDDeviceConnectedListener를 통해 결과값을 알 수 있다. 

###unpair
void unpair(WFDPairInfo pair)
: 이미 페어링된 device와 연결을 끊는다.

###setWFDDeviceDiscoveredListener
void setWFDDeviceDiscoveredListener
(WFDDeviceDiscoveredListener wfdDeviceDiscoveredListener)
: WFDDeviceDiscoveredListener setter

###setWFDDeviceConnectedListener
void setWFDDeviceConnectedListener
(WFDDeviceConnectedListener wfdDeviceConnectedListener)
: WFDDeviceConnectedListener setter


#WFDDevice
Wifi direct를 지원하는 remote device 
##1. Field
Object WFDDeviceInfo 
: Platform에 따라 필요한 정보 반환
 -Android  : DeviceInformation
 -Windows : PeerInformation

bool IsDevice 
:  @deprecated
Platform 정보 반환 
-Android : true
-Windows : false

string Name
: 장치의 DisplayName 반환

##2. Constructor
##3. Methods

#WFDPairInfo
Wifi Direct로 페어링된 device 

##1. Field
WFDDevice device : 연결 하고자 하는 WFDDevice
##2. Constructor
- WFDPairInfo(WFDDevice device, DependencyObject parent)
: 페어링 된 Windows peer 생성자
- WFDPairInfo(WFDDevice device, EndpointPair deviceEndpointPair, DependencyObject parent)
: 페어링 된 Android peer 생성자

##3. Methods
###getLocalAddress
string getLocalAddress()
: Local Address 반환
-Android : local address
-Windows : (empty string)

###getRemoteAddress
string getRemoteAddress()
: Remote Address반환
-Android : peer의 address반환
-Windows : (empty string)

###getWFDDevice
WFDDevice getWFDDevice()
: WFDDevice 반환

###connectSocketAsync
void connectSocketAsync(PairSocketConnectedListener l)
: 페어링된 device과 통신하기 위한 socket생성.




# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace `meowmeowmeow` with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Isis",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import 'kittn'

api = Kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/3"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Isis",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">If you're not using an administrator API key, note that some kittens will return 403 Forbidden if they are hidden for admins only.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the cat to retrieve

