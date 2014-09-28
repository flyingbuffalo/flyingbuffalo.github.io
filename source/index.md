---
title: WFDManager - API Reference

language_tabs:
  - csharp
  - java

toc_footers:
  - <a href='http://github.com/flyingbuffalo/WFDAndroid'>Go to the WFDManager repository</a>
  - <a href='http://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:

search: true
---

# Introduction

Welcome to the WFDManager API! WFDManager is WiFi Direct Library. You can use our API to access other WiFi Direct device, which can transfer data using socket connection.

We have language bindings in Android, C#(Windows 8). You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [WFDManager](http://github.com/flyingbuffalo/WFDAndroid). Feel free to edit it and use it as a base for your own API's documentation.


WFDManager API 문서 입니다! WFDManager는 WiFi Direct 라이브러리입니다. 간단한 API를 통해 다른 WiFi Direct 장치들과 데이터 전송을 할 수 있습니다.

Android와 C#(Window 8 App)을 지원합니다. 오른쪽 어두운 화면에서는 사용법을 보실 수 있고, 또한 탭을 통해 언어를 바꾸어 확인하실 수 있습니다.

#Package flying.buffalo

## Interface
 - WFDDeviceDiscoveredListener
 - WFDDeviceConnectedListener
 - WFDPairInfo.PairSocketConnectedListener

## Class
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

# WFDDeviceDiscoveredListener
WFDManager.getDevicesAsync의 결과값을 포착하는 리스너
## 1. Methods
### onDevicesDiscovered
```csharp
void onDevicesDiscovered(List<WFDDevice> deviceList)

```

```java
void onDevicesDiscovered(List<WFDDevice> deviceList)
```

`void onDevicesDiscovered(deviceList)`

장치 탐색 성공 시 deviceList를 인자로 하여 호출 됨.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
deviceList|List&lt;WFDDevice&gt;|List&lt;WFDDevice&gt;| 탐색 성공한 기기 목록 |

### onDevicesDiscoverFailed
```csharp
void onDevicesDiscoverFailed(int reasonCode)

```

```java
void onDevicesDiscoverFailed(int reasonCode)
```

`void onDevicesDiscoverFailed(reasonCode)`

장치 탐색 실패 시 호출 됨.

#### Parameters

  인자명   |          언어별 Type       ||  설명        |   
--------- | ---------- | --------------|--------------|
          |  C#        |    Java       |          
reasonCode|int         |int            | 실패 원인 코드 |



# WFDDeviceConnectedListener
WFDManager.connectAsync의 결과값을 포착하는 리스너
## 1. Methods
### onDeviceConnected
```csharp
void onDeviceConnected(WFDPairInfo pair)

```

```java
void onDeviceConnected(WFDPairInfo pair)
```

`void onDeviceConnected(WFDPairInfo pair)`

장치 연결 성공 시 호출 됨

#### Parameters

  인자명   |          언어별 Type       ||           설명          |   
--------- | ---------- | ------------- |------------------------ |
          |  C#        |    Java       |          
pair      |WFDPairInfo |   WFDPairInfo | 연결에 성공한 WFDPairInfo |

### onDeviceConnectFailed
```csharp
void onDeviceConnectFailed(int reasonCode)

```

```java
void onDeviceConnectFailed(int reasonCode)
```

`void onDeviceConnectFailed(reasonCode)`

장치 연결 실패 시 호출 됨.

#### Parameters

  인자명   |          언어별 Type     ||  설명       |   
--------- | ---------- | ---------- |------------- |
          |  C#        |    Java    |          
reasonCode|      int   |    int     | 실패 원인 코드 |



### onDeviceDisconnected
```csharp
void onDeviceDisconnected()
```

```java
void onDeviceDisconnected()
```

`void onDeviceDisconnected()`

장치 연결 종료 시 호출 됨


# PairSocketConnectedListener
WFDPairInfo.connectSocketAsync의 결과값을 포착하는 Listener
## 1. Methods
### onSocketConnected
```csharp
void onSocketConnected(StreamSocket socket)

```

```java
void onSocketConnected(Socket socket)
```

`void onSocketConnected(socket)`

connectSocketAsync의 호출로 Socket Connection 성공 시 호출 됨

#### Parameters

  인자명   |          언어별 Type        ||  설명                |   
--------- | ---------- | -------------- |----------------------|
          |  C#        |    Java        |          
socket    |StreamSocket| StreamSocket   |   연결 성공한 socket  |


# WFDManager

Wifi Direct Device를 관리하는 Base Class. Singleton으로 instance를 사용하도록 한다.

* Wifi direct를 시작하고
* 주변의 Wifi direct 장치를 찾으며
* Pairing, Socket Connection을 담당한다.

## 1. Public Constructors

```csharp
public void WFDManager(DependencyObject parent, 
						WFDDeviceDiscoveredListener wfdDeviceDiscoveredListener, 
						WFDDeviceConnectedListener wfdDeviceConnectedListener)
```

```java
public void WFDManager(Context context, 
						WFDDeviceDiscoveredListener wfdDeviceDiscoveredListener, 
						WFDDeviceConnectedListener wfdDeviceConnectedListener)
```

`public void WFDMaager(parent | context, discoveredListener, connectedListner)`

장비의 Wifi direct를 사용할 수 있도록 상태를 변경하고, connetecion 요청을 처리할 리스너를 등록한다.

### Parameters

  인자명            |          언어별 Type         |                              |  설명                     |   
------------------- | --------------------------  | ----------------------------|---------------------------|
          			|  C#        					|    Java                   |          
parent OR context	| Context  					  |  DependencyObject            | 시스템에 접근하기 위한 인자 |
discoveredListener  | WFDDeviceDiscoveredListener |  WFDDeviceDiscoveredListener | 주변 기기들을 포착         |
connectedListner    | WFDDeviceConnectedListener  |  WFDDeviceConnectedListener  | 기기 연결 이벤트를 포착    |


## 2. Public Methods

### getDevicesAsync

```csharp
public void getDevicesAsync()

```

```java
public void getDevicesAsync()
```


`void getDevicesAsync()`

주변의 wifi direct가 켜져있는 Device들을 비동기적으로 탐색한다. wfdDeviceDiscoveredListener를 통해, 성공 시 List<WFDDevice>를 반환한다. 내부적으로 Android를 탐색하기위해Windows.Devices.WiFiDirect를 사용하고, Windows를 탐색하기위해Windows.Networking.Proximity를 사용한다.  탐색 도중 작업이 취소되면 탐색된 리스트를 clear한다. 

#### Returns

onDevicesDiscovered(List<WFDDevice> deviceList)를 통해 연결된 기기의 정보가 반환

### pairAsync

```csharp
public void pairAsync()

```

```java
public void pairAsync()
```


`void pairAsync()`

device와 비동기적으로 연결한다. 
WFDDeviceConnectedListener를 통해 결과값을 알 수 있다.

#### Returns

onDeviceConnected(WFDPairInfo)를 통해 연결된 기기의 정보가 반환

### unpair

```csharp
public void unpair(WFDPairInfo pair)

```

```java
public void unpair()
```

#### Windows
`void unpair( pair )`

#### Android
`void unpair()`

연결된 device와 연결을 끊는다.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
pair      | WFDPairInfo|       | 연결을 끊을 기기 연결 정보 |

<aside class="notice">
안드로이드는 모든 연결을 해제함.
</aside>

### setWFDDeviceDiscoveredListener

```csharp
public void setWFDDeviceDiscoveredListener( WFDDeviceDiscoveredListener listener )

```

```java
public void setWFDDeviceDiscoveredListener( WFDDeviceDiscoveredListener listener )
```


`void setWFDDeviceDiscoveredListener( listener )`

WFDDeviceDiscoveredListener를 설정한다.

#### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
listener  | WFDDeviceDiscoveredListener |  WFDDeviceDiscoveredListener | 주변 기기들을 포착 |

## 3. Public Field

TODO

# WFDDevice

WiFi direct를 지원하는 remote device 

## 1. Public Constructors

```csharp
public WFDDevice(PeerInformation peerInfo)		// Windows device
public WFDDevice(DeviceInformation wfdDevInfo)	// Andorid device
```

```java
public WFDDevice(WifiP2pDevice device)
```

`void WFDDevice(device)`

### Parameters

  인자명   |          언어별 Type       ||  설명   |   
--------- | ---------- | --------------|---------|
          |  C#        |    Java        |          
device    | PeerInformation |  WifiP2pDevice | 기기 정보 |
          | DeviceInformation || 기기 정보 (윈도우끼리만)|
			

## 2. Public Field

   필드명            |          언어별 Type         |                              |  설명                     |   
------------------- | --------------------------  | ----------------------------|-----------------------------|
          			|  C#        				  |    Java                     |          
wfdDeviceInfo    	| DeviceInformation OR PeerInformation	|  WifiP2pDevice    | platform 별, 주변 device 정보 |
IsDevice            | bool          |  bool                  | platform flag. true = Android, false = Windows|
Name                | string        |  string                  | 장치의 DisplayName 반환 |

# WFDPairInfo

WiFi Direct로 연결된 Device 

## 1. Public Constructors

```csharp
public WFDPairInfo(WFDDevice device, DependencyObject parent)								// Windows
public WFDPairInfo(WFDDevice device, EndpointPair deviceEndpointPair, DependencyObject parent)		// Android
```

```java
public WFDPairInfo(WifiP2pInfo info)
```

#### Windows
`void WFDPairInfo(device, parent)`

`void WFDPairInfo(device, endpointPair, parent)`

#### Android
`void WFDPairInfo(info)`

### Parameters

  인자명   |          언어별 Type              ||  설명                    |   
------------- | ---------------- | -------------- | ------------------------ |
          	  |  C#        		 |    Java        |          
device    	  | WFDDevice  		 |                | 기기 정보 				 |
parent   	  | DependencyObject |                | 시스템에 접근하기 위한 인자 |
endpointPair  | EndpointPair     |                |
info      	  |                  | WifiP2pInfo    | 연결된 기기 정보 			 |

## 2. Public Methods

### getLocalAddress
```csharp
public string getLocalAddress()
```

```java
public String getLocalAddress()
```

`string getLocalAddress()`

Local Address 반환

##### Return

         언어별 Type              ||  설명                   |   
---------------- | -------------- | ----------------------- |
      C#      	 |    Java        |          
   string        |    String      |   local address 문자열   |

### getRemoteAddress
```csharp
public string getRemoteAddress()
```

```java
public String getRemoteAddress()
```

`string getRemoteAddress()`

Remote Address 반환

##### Return

         언어별 Type              ||  설명                   |   
---------------- | -------------- | ----------------------- |
      C#      	 |    Java        |          
   string        |    String      |  remote address 문자열   |

### getWFDDevice
```csharp
public WFDDevice getWFDDevice()
```

```java 
not supported
```

`WFDDevice getWFDDevice()`

WFDDevice 반환

##### Return

         언어별 Type              ||  설명                    |   
---------------- | -------------- | ------------------------ |
      C#      	 |    Java        |          
   WFDDevice     |                | 연결 하고자 하는 WFDDevice |

<aside class="warning">
getWFDDevice()는 윈도우에서만 사용 가능!
</aside>

### connectSocketAsync
```csharp
public void connectSocketAsync(PairSocketConnectedListener listener)
```

```java
public void connectSocketAsync(PairSocketConnectedListener listener)
```

`void connectSocketAsync(listener)`

페어링된 device과 통신하기 위한 socket생성

##### Return

onSocketConnected(Socket s)에서 연결된 socket을 반환

## 3. Public Field

  필드명       |          언어별 Type              ||  설명                    |   
------------- | ---------------- | -------------- | ------------------------ |
          	  |  C#        		 |    Java        |          
listener      | PairSocketConnectedListener  		 |    PairSocketConnectedListener   | socket 연결을 받는 listener |
